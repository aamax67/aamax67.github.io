---
layout: post
title:      "Creating a CLI Gem about Podcasts"
date:       2018-02-05 20:07:31 +0000
permalink:  creating_a_cli_gem_about_podcasts
---


It is an amazing feeling to feel like I am starting to "get it." I'm starting to feel like a coder. Anyway. The last week and a half has been quite a learning experience. I have just finished my CLI gem and it actually works.

Here is how it went.

**Learn by example**

1. I watched the Ari's walkthrough for his "Daily Deal" gem.
2. Then I cloned the two examples of gems, "Now Playing and Best Restaurants."

            I wanted to understand the structure of how gem's are laid out.
						I wanted to solidify the relationships between classes and methods.
						I wanted to better understand scraping.
					
Now it was time to create my own gem.

**Questions I asked myself:**

          1.  What is something I am interested in?
          2.  What is something that changes day to day
          3.  What is something that has straight forward relationships

The answer? ** PODCASTS**

So I set out to create my CLI gem about the top 200 podcasts.

**Process**

1. Plan my gem. Decide how the interface will work.
        
							- A command line interface for current top 200 podcasts

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

			1

			User enters the number of the podcast he/she is interested in.

			User is shown the rank, title and summary of that particular podcast.

			Then user is asked if he/she would like to choose another podcast?

			User types Y or N

			If Y then the process starts over.

			If X then the user is given a goodby message.
		
		
Now that I had a plan, it was time to create my gem layout with Bundler.






