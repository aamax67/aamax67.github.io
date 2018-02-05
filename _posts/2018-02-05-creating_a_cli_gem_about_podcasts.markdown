---
layout: post
title:      "Creating a CLI Gem about Podcasts Part 1"
date:       2018-02-05 15:07:31 -0500
permalink:  creating_a_cli_gem_about_podcasts
---


It is an amazing feeling to feel like I am starting to "get it." I'm starting to feel like a coder. Anyway. The last week and a half has been quite a learning experience. I have just finished my CLI gem and it actually works.

Here is how it went.

# Learn by example

1. I watched the Ari's walkthrough for his "Daily Deal" gem.
2. Then I cloned the two examples of gems, "Now Playing and Best Restaurants."

I wanted to understand the structure of how gem's are laid out.
I wanted to solidify the relationships between classes and methods.
I wanted to better understand scraping.
					
Now it was time to create my own gem.

# Questions I asked myself:

1.  What is something I am interested in?
2.  What is something that changes day to day
3.  What is something that has straight forward relationships
 
The answer? PODCASTS


So, I set out to create my CLI gem about the top 200 podcasts.

Process

Plan my gem. Decide how the interface will work.


        
**A command line interface for current top 200 podcasts**

	User types top_podcasts

	User is welcomed to the top podcasts gem.
	User is asked to enter a range of ten numbers, i.e. 1-10, 11-20, etc.
	Once user enters the numbers a list of ten podcasts are shown, sorted by rank

	1. Rank, Podcast
	2. Rank, Podcast
	3. Rank, Podcast
	4. Rank, Podcast
	5. Rank, Podcast
	6. Rank, Podcast
	7. Rank, Podcast
	8. Rank, Podcast
	9. Rank, Podcast
	10. Rank, Podcast


Which podcast do you want to know more about?

	“1”

User enters the number of the podcast he/she is interested in.

User is shown the rank, title and summary of that particular podcast.

Then user is asked if he/she would like to choose another podcast?

User types Y or N

If Y then the process starts over.

If X then the user is given a goodby message.
		
**Now that I had a plan, it was time to create my gem layout with Bundler.**

In learn IDE, I typed bundle install “top_podcasts”
The Gem layout was in place.

Next, I created by bin file “top_podcasts,” which would eventually call my CLI class. I knew that I needed to require the bundler/setup and “top_podcasts” folders. I would need to also set a method to instantiate the CLI method “call” when executed.


Next, I decided to tackle the CLI class.

I started by entering what I wanted the program to do.

User enters "top_podcast, 
then the program starts with a welcome message. 
It then asks the user for input.
it iterates over data and returns a list of podcasts, based on user input
It then asks the user to enter a number for the podcast he/she is interested in
It returns the podcast with a summary of the podcast
It then asks the user if he/she would like information on another podcast.
If yes, then the process starts over, if no then the program terminates with a goodby message.

Here is the code I came up with:

```class TopPodcasts::CLI

  def call
    TopPodcasts::Scraper.new.make_podcasts
    puts "Welcome to the top 50 podcasts:"
    start
  end

  def start
    puts ""
    puts "What number podcasts would you like to see? 1-10, 11-20, 21-30, 31-40 or 41-50?"
    input = gets.strip.to_i

    print_podcasts(input)

    puts ""
    puts "What podcast would you like more information on?"
    input = gets.strip

    podcast = TopPodcasts::Podcast.find(input.to_i)

    print_podcast(podcast)

    puts ""
    puts "Would you like to see another podcast? Enter Y or N"

    input = gets.strip.downcase
      if input == "y"
          start
      else
        puts ""
        puts "Thankyou! Have a great day!"
        exit
      end
    end


  def print_podcast(podcast)
    puts ""
    puts "----------- #{podcast.rank} - #{podcast.name} -----------"
    puts ""
    puts "----------------------------Summary---------------------------"
    puts ""
    puts "#{podcast.summary}"
    puts ""
  end

  def print_podcasts(from_number)
    puts ""
    puts "---------- Podcasts #{from_number} - #{from_number+9} ----------"
    puts ""
    TopPodcasts::Podcast.all[from_number-1, 10].each.with_index(from_number) do |podcast, index|
      puts "#{podcast.rank} - #{podcast.name}"
    end
  end
end
```

# Next, Podcast class
I asked myself, what is a podcast?  What does it contain?  The answer - A name, a rank, and a summary.

Here is what I came up with:

```class TopPodcasts::Podcast

  attr_accessor :name, :rank, :summary

    @@all = []

    def self.new_from_index_page(p)
    self.new(
      p.css("h3").text.gsub(/\t/, '').strip,
      p.css(".numberImage").text.gsub(/\t/, '').strip,
      p.css("p").text.strip
      )
  end

  def initialize(name = nil, rank = nil, summary = nil)
    @name = name
    @rank = rank
    @summary = summary
    @@all << self
  end

  def self.all
    @@all
  end

  def self.find(id)
    self.all[id-1]
  end
end```












