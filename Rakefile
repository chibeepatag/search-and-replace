require 'optparse'
namespace :search_and_replace do 
  desc "Reads files in a directory and replaces given text with a nominated string."
  task :run do
    puts "Search and Replace"

    options = {}
    o = OptionParser.new

    o.banner = "Usage: rake search_and_replace:run -- [options]"
    o.on("-d DIRECTORY", "--directory DIRECTORY") { |directory|
      options[:directory] = directory
    }
    o.on("-s SEARCH", "--search SEARCH") { |search|
      options[:search] = search
    }
    o.on("-rw REPLACE_WITH", "--replace_with REPLACE_WITH") { |replace_with|
      options[:replace_with] = replace_with
    }
    args = o.order!(ARGV) {}
    o.parse!(args)
    puts "directory: #{options[:directory]}"
    puts "search: #{options[:search]}"
    puts "replace_with: #{options[:replace_with]}"
  end
end

namespace :search_and_count do 
  desc "Reads files in a directory and counts occurences of a given string in each file."
  task :run do
    puts "---Search and Count---"

    options = {}
    o = OptionParser.new

    o.banner = "Usage: rake search_and_replace:run -- [options]"
    o.on("-d DIRECTORY", "--directory DIRECTORY") { |directory|
      options[:directory] = directory
    }
    o.on("-s SEARCH", "--search SEARCH") { |search|
      options[:search] = search
    }
    args = o.order!(ARGV) {}
    o.parse!(args)
    puts "Searching for #{options[:search]} in each file inside #{options[:directory]}"
    count = search_and_count(options[:directory], options[:search])
    puts "There are #{count} occurences of #{options[:search]}"
  end

  desc "Counts occurences of a given string in the given file."
  task :run_for_file do
    puts "---Search and Count---"
    options = {}
    o = OptionParser.new

    o.banner = "Usage: rake search_and_replace:run -- [options]"
    o.on("-f FILE", "--file FILE") { |file|
      options[:file] = file
    }
    o.on("-s SEARCH", "--search SEARCH") { |search|
      options[:search] = search
    }
    args = o.order!(ARGV) {}
    o.parse!(args)
    puts "Searching for #{options[:search]} in inside #{options[:file]}"
    count = serach_and_count_in_file(options[:file], options[:search])
    puts "There are #{count} occurences of #{options[:search]}"
  end

  def search_and_count directory, search
    count = 0
    filenames = Dir.entries(directory)
    filenames.each do |filename|
      next if File.directory?("#{directory}/#{filename}")
      file = File.open("#{directory}/#{filename}")
      file.readlines.each do |line|
        count += 1 if line.match(/#{Regexp.quote(search)}/) 
      end
    end
    count
  end

  def serach_and_count_in_file filename, search
    count = 0
    file = File.open(filename)
    file.readlines.each do |line|
      count += 1 if line.match(/#{Regexp.quote(search)}/) 
    end
    count
  end
end