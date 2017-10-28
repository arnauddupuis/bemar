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

If the episode also have a quality (like "1080p" for example) it will also be captured as {episode_quality}. Bemar only recognize quality when it's a number followed by "p" or "k" (like "480p", "720p", "1080p", "4k"). It has to be a standalone string (separate from the rest by spaces, "()", "[]" or dots). 

## Variables

bemar will capture a couple of informations from the file title and make it available as variables that can be used in the moving pattern. Here is a list of the available variables:
  * {season_number}: the season number
  * {episode_number}: the episode number
  * {episode_quality}: the episode quality 
  * {file_extension}: the file extension (mp4, mkv, etc.)
  * {serie_name}: the serie name. **Warning**: bemar will try to extract the serie name but you should not trust it too much...
  
## Configuration file

The configuration file has 2 separate typeof sections the \[general\] and the series ones. It looks like that:
```
[general]
# scan is the list of directories to scan for series episodes. This is a comma separated list.
scan=/home/plex/Downloads,/home/plex/BT/Series

[The Flash]
# The pattern is a PCRE (Perl Compatible Regular Expression) pattern. It is case insensitive.
pattern=The\.\Flash\.2014\..*
# destination is (obviously) the destination of the file that match the pattern.
destination=/home/plex/Medias/Series/The.Flash.2014/Season_{season_number}/The.Flash.2014.S{season_number}E{episode_number}.{episode_quality}.{file_extension}
# post_cleaning allow for extra characters removing or replacement. This is a yes/no value.
post_cleaning=yes
# these are post cleaning rules the form is <characters to replace>:<characters replacement>. It is a comma separated list. The following is the default value.
post_cleaning_rules=..:.,...:.,\s:.
# If file_only is set to yes, bemar will only move and rename files within directories. For example if you have a directory structure like this:
# 'The.Big.Bang.Theory.S11E05.1080p.HDTV.X264-DIMENSION[rarbg]/':
#          RARBG.txt  
#          The.Big.Bang.Theory.S11E05.1080p.HDTV.X264-DIMENSION.mkv  
#          the.big.bang.theory.1105.1080-dimension.nfo
#
# With file_only=yes the only thing that is going to be moved is The.Big.Bang.Theory.S11E05.1080p.HDTV.X264-DIMENSION.mkv according to the pattern.
file_only=yes

[Star Trek Discovery]
pattern=Star\.\Trek\.Discovery\..*
destination=/home/plex/Medias/Series/Star.Trek.Discovery/Season_{season_number}/Star.Trek.Discovery.S{season_number}E{episode_number}.{episode_quality}.{file_extension}
post_cleaning=yes
post_cleaning_rules=..:.,...:.,\s:.
file_only=yes

```
