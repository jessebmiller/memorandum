# memorandum
Simple tools for wrangling my notes and ideas from where they reside

# Design Goals

* full user soverignty
  * Code simple enough to come back to, understand, and easily add functionality
  * Everything in human readable and editable text for portability, version control, and self ownership
  * No dependency on any company or other individual
* Capture notes from the places I put them
  * In google keep
  * In notebooks
  * In email I send to myself
  * Google docs
  * Files on the filesystem
* Make them usable
  * Remind me to look at them
  * Categorize them
  * Group them
  * Archive them
  * Associate them with contexts they would be useful in
  * Let me refine them
  
# System Design

## When working in a text file
I write myself memos in line with what I'm doing and then the system runs through them and ingests them. Removing them from the file and putting them in the right place.

Memo syntax (single paragraph)

{Memo Prefix} {Memo Type} {Any amount of memo text terminated with an empty line}

**Memo Prefix** is considered to be anything on the line before the memo type and is stripped from all lines in the memo text
**Memo Type** is any string matching any registered memo types

## Other sources
When working somewhere other than a text file it may be more difficult to get the syntax exactly right (mobile for instance).
So I may want to associate certain sources with specific memo types by default. For instance google keep notes might all get the type "TODO" or Note.

In any case I want to have different ingestion procedures for different sources and want to be able to expand with more

## The Interfaces

lol it's ETL but Read, Parse, Commit

### Reader
`Memo Source -> [Line of Text]`

How can we make reading idempotent? What happens when we make a small change to the source memo? is that a new memo?

### Identifier
`[Lines of Text] -> Content Addressed ID`

### Parser
`[Line of text] -> [memo]`
Parses text and extracts memos

### Committer
`[memo] -> ()`
Appends memos to The Log
