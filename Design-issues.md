This page collects all the issues affecting the current design of today's PSL. The goal is to have a better understanding of the limitations to (hopefully) come with a better one.

## Issues

- Static list (akin to hosts.txt) vs Server-Based

  This is a static list.  When list is infrequently updated this is a speed enhancement as a local source file, but when updates occur it can lead to stale behavior (a common example of this was during the 2014+ nTLDs sometimes being sent to search vs DNS by omnibox browsers with an old version of PSL locally, where an OS or software update that would update to catch up and remedy may have had long spans between)

- Finite resource

  This makes harder to consider patches such as https://github.com/publicsuffix/list/pull/277 that requires the merge of 19k `.NAME` rules.

- More richful format

  Use something different than a simple list of strings, that allows extensibility and extra fields. A possible alternative is either JSON or YAML.

- List metadata

  As for previous point, a different format may allow metadata to be added to the list (e.g. last update).

- Split private vs non-private

  There have been an increasing demand to separate the two lists for better management and reduce on-the-fly parsing.

- Convert to A-labels

  No UTF-8 please.

- Wildcard

  Clarify the use of wildcard. Today we implicitly support any wildcards, but all implementations support only left-outermost wildcard.

