#Pitchfork Client

An unofficial Node.js client for [Pitchfork](http://pitchfork.com/) reviews based on the [Pitchfork API Client for Python](https://github.com/michalczaplinski/pitchfork).

## Install

```
npm install pitchfork
var pitchfork = require('pitchfork')

```

You can then use it as a [command-line tool](#CLI) or as a [node module](#API)

##API

```
var pitchfork = require('pitchfork')
var search = new pitchfork.Search("wilco", "sky blue sky")

```

### Search

A search object

``.results``

An {Array} of {Review} objects.

``.init``

Called once when Search is instantiated to fetch results.  Not usually called directly

### Review

The {Review} constructor encapsulates methods and data relating to the Pitchfork review.


``.attributes``

An {Object} with information about the album and its text.  Sample below:

```
{
  "url": "/reviews/albums/19466-mogwai-come-on-die-young-deluxe-edition/",
  "name": "Mogwai - Come On Die Young ",
  "artist": "Mogwai",
  "album": "Come On Die Young",
  "title": "Mogwai: Come On Die Young | Album Reviews | Pitchfork",
  "label": "Chemikal Underground",
  "year": "1999/2014",
  "score": 8.3,
  "cover": "http://cdn3.pitchfork.com/albums/20688/homepage_large.2ac360a5.jpg",
  "author": "Mark Richardson",
  "date": "June 18, 2014",
  "editorial": {
    "text": " Though few of their songs contain actual words, Mogwai have always been fond of big statements. Having emerged during the late-1990s post-rock boom, the Scottish quintet used every means possible to distance themselves from the sullen stereotype that defined so many instrumental art-rock brooders o...",
    "html": "<p>Though few of their songs contain actual words, Mogwai have always been fond of big statements. Having emerged during the late-1990s post-rock boom, the Scottish quintet used every means possible to distance themselves from the sullen stereotype that defined so many instrumental art-rock brooders of their era. EP titles were <a href=\"http://en.wikipedia.org/wiki/No_Education_%3D_No_Future_(Fuck_the_Curfew)\" target=\"_blank\" rel=\"nofollow\">"
}
```

``.fetch``

This method is automatically called when the {Review} is instantiated and returns a [Promise](https://github.com/kriskowal/q).  This generally isn't called directly.

``.promise``

This stores the thennable promise object generated by .fetch for attaching .then-style callbacks.


``.verbose``

The full {Review} instance represented as JSON.


``.truncated``

The attributes of the {Review} instance with editorial.html/editorial.text condensed into the first 300 characters of of the text assigned to the key '.text'.

``.text_pretty_print``

Prints a plain-text representation of the review.


## CLI (Command-Line Interface)

Returns a review for a given artist.

```
$ pitchfork -a 'radiohead' -t 'ok computer'

{ name: }

```

### Flags

| flag(s)      |  required | argument    | description  |
| -------      | ---- | ---------   | ------------ |
| -a           |  y  | artist_name |  returns a review by given artist           |
| -t           |    | album_title |  returns a review by given album title |
| -j,--json     |   |    |  returns review attributes as un-prettified json |
| -v, --verbose  |  |    |  returns review entire object as json |
| -V, --version   |  |    | returns version number |
| -T,--truncated |  |    |  returns a truncated json object of the review attributes | 
| -tx,--text      |  |    | returns a text version of review (hint: pipe output to less ) |

