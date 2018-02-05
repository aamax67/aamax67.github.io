---
layout: post
title:      "Creating a CLI gem for podcast Part 2"
date:       2018-02-05 21:15:04 +0000
permalink:  creating_a_cli_gem_for_podcast_part_2
---


Now that I had a plan, it was time to create my gem layout with Bundler.

In learn IDE, I typed bundle install “top_podcasts”

The Gem layout was in place.

Next, I created by bin file “top_podcasts,” which would eventually call my CLI class. I knew that I needed to require the bundler/setup and “top_podcasts” folders. I would need to also set a method to instantiate the CLI method “call” when executed.

