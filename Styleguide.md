# Styleguide

## Right-to-left sorting

Keep the list of suffix (if more than one) in alphabetical order. Sort first by the TLD, then the first label to the left of the TLD, and so forth. For example, the following is sorted by TLD first (`com`, `invalid`, `net`, `org`, `test`), then within each TLD, sorted by the first label (`example`), then, for entries with more labels, each label is sorted, with shorter entries appearing first:

```
beta.example.com
alpha.beta.example.com   // alpha.beta has more labels than beta, and thus comes second.
delta.example.invalid    // invalid sorts between com and net
beta.example.net
delta.example.net        // delta sorts after beta, as example and net are the same
charlie.example.org      // org sorts after net, because sorting is by the right-most label, not the left-most
alpha.example.test
```

This is a simple Ruby script (called `psl-sort`) you can use to sort entries in a file:

```ruby
#!/usr/bin/env ruby

input  = STDIN.read.split("\n")
output = input.sort_by { |x| x.split(".").reverse.join(".") }

puts output.join("\n")
```

Usage:

```
$ cat file.txt | psl-sort
```
