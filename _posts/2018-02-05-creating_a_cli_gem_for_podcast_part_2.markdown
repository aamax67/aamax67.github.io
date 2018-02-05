---
layout: post
title:      "Creating a CLI gem about Podcasts Part 2"
date:       2018-02-05 16:15:04 -0500
permalink:  creating_a_cli_gem_for_podcast_part_2
---


Now that I had a plan, it was time to create my gem layout with Bundler.

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

Here is what I came up with:

class TopPodcasts::CLI

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

# Next, Podcast class
I asked myself, what is a podcast?  What does it contain?  The answer - A name, a rank, and a summary.

Here is what I came up with:

class TopPodcasts::Podcast

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
end


With this in place, I knew that the self.new_from_index_page(p) method would create a new instance of a podcast with scraped data taken from the scraper class. It would initialize and each podcast would be included in the @@all array.

I also created a self.find(id) method so that one could search for podcasts by number

# Scraper class

Here is what I have for my Scraper class. Pretty straightforward. 

**Get_page** method gets the podcast website we are scraping from using Nokogiri. 
**Get_podcasts** method gets all of the data from the page.
**make_podcasts** method iterates over the **get_podcasts method** and returns a podcast with data scraped from the Podcast.new_from_index_page(p) method.


Once all of this was in place. The program magically came to life.

