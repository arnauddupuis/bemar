# bemar (Batch Episodes Move And Rename)

## Introduction

This very simple and autonomous software does only one thing: move and rename your TV episodes automatically.
It is written in Perl.
It requires a very limited number of dependencies that should be part of the Perl distribution for any system.

The configuration file is really straightforward. It is composed of sections that gives instructions about the pattern of the files and the place to move them.
Pattern can use some variables that are automatically set (we''l cover that later).

## Why?

Because I need it! I have a very nice setting with a server on the internet with Sickrage in a docker container, a transmission not in a docker container and a Plex not in a docker container. Sickrage is super nice but lack some sorting features when interacting with transmission.
So basically this little unambitious script is here to fill the blank.

## A word about episodes naming

Episodes have to be name according to the **sXXeYY** "standard" for some variables to be properly extracted.
With:
  * **s** and **e** can be capital or not
  * **XX** is the season number
  * **YY** is the episode number
Season and episode number will then be expended as {season_number} and {episode_number} variables.

If the episode also have a quality (like "1080p" for example) it will also be captured as {episode_quality}. Bemar only recognize quality when it's a number followed by "p" or "k" (like "480p", "720p", "1080p", "4k"). It has to be a standalone string (separate from the rest by spaces or dots). 

## Variables

bemar will capture a couple of informations from the file title and make it available as variables that can be used in the moving pattern. Here is a list of the available variables:
  * {season_number}: the season number
  * {episode_number}: the episode number
  * {episode_quality}: the episode quality 
  * 
