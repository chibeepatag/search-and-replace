# search-and-replace

A simple ruby program (rake tasks) that is used to search across files and replace a given string. The 4 rake tasks do the following

1. Search in a file a string and count occurrences of the string
rake search_and_count:file -- --fsample/7.7-KB.txt -sGatsby

2. Search in a directory of files a string and count occurrences of the string
rake search_and_count:directory -- --dsample -sGatsby

3. Search in a file a string and replace it with another string
rake search_and_replace:file -- --fsample/7.7-KB.txt -sGatsby -rHero

4. Search in a directory of files a string and replace it with another string
rake search_and_replace:file -- --dsample -sGatsby -rHero

To list the rake tasks: rake -T

To show help: rake namespace:taskname -- --help