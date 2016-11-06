# Fanfiction Scraper
This repository contains scraping tools for [FanFiction.Net](http://fanfiction.net). These tools are meant to be used for non-commercial, research purposes. They were originally created for the following paper; please cite if you use this software for your research:

Smitha Milli and David Bamman, "Beyond Canonical Texts: A Computational Analysis of Fanfiction" EMNLP 2016.

We have imposed a rate limit of a page per second in these tools in order to comply with the fanfiction.net terms of service:
> E. You agree not to use or launch any automated system, including without limitation, "robots," "spiders," or "offline readers," that accesses the Website in a manner that  sends more request messages to the FanFiction.Net servers in a given period of time than a human can reasonably produce in the same period by using a conventional on-line web browser.

If you want fanfiction from Archive of Our Own instead, check out [@radiolarian's Archive of Our Own scraper](https://github.com/radiolarian/AO3Scraper).

# Usage

## Install
    pip install fanfiction

## Example
    from fanfiction import Scraper
    scraper = Scraper()
    metadata = scraper.scrape_story_metadata(STORY_ID)

# Documentation
```
fanfiction.Scraper.get_story_metadata(story_id)
```
  Returns a dictionary with the metadata for the story.

  Attributes:

  * **id** [int]: The id of the story
  * **canon_type** [str]: The type of canon
  * **canon** [str]: The name of the canon
  * **author_id** [int]: The user id of the author
  * **title** [int]: The title of the story
  * **updated** [int]: The timestamp of the last time the story was updated
  * **published** [int]: The timestamp of when the story was originally published
  * **lang** [str]: The language the story is written in
  * **genres** [list]: A list of the genres that the author categorized the story as
  * **num_reviews** [int]
  * **num_favs** [int]
  * **num_follows** [int]
  * **num_words** [int]: Total number of words in all chapters of the story
  * **rated** [str]: The story's fiction rating. i.e. K, K+, T, M

```
fanfiction.Scraper.scrape_story(story_id, keep_html=False)
```

  Returns a dictionary with the metadata, chapters, and reviews of the story. The dictionary has the same attributes as the metadata attributes listed above plus the additional attributes:

  * **chapters** [dict]: A dictionary mapping from the chapter id (where the chapter id for the n-th chapter of the story is n) to the text of the chapter. The text is either stripped of HTML if keep_html is False or with the HTML intact if keep_html is True.
  * **reviews** [dict]: A dictionary mapping from the chapter id to a list of review dictionaries (see ```fanfiction.Scraper.scrape_reviews_for_chapter(story_id, chapter_id)```)

```
fanfiction.Scraper.scrape_chapter(story_id, chapter_id, keep_html=False)
```
  Returns the text of the chapter either stripped of the HTML if keep_html is False or with the HTML intact if keep_html is True.

```
fanfiction.Scraper.scrape_reviews_for_chapter(story_id, chapter_id)
```
  Returns a list of review dictionaries. Each review dictionary has the following attributes:

  * **user_id** [int]: The user id of the reviewer. If the review came from an unregistered user, then user_id is set to None.
  * **time** [int]: The timestamp of the review.
  * **review** [int]: The text of the review.
