require 'optparse'
require 'byebug'
namespace :search_and_replace do 
  desc "Reads files in a directory and replaces given text with a nominated string."
  task :directory do
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
    o.on("-r REPLACE_WITH", "--replace_with REPLACE_WITH") { |replace_with|
      options[:replace_with] = replace_with
    }
    args = o.order!(ARGV) {}
    o.parse!(args)
    puts "directory: #{options[:directory]}"
    puts "search: #{options[:search]}"
    puts "replace_with: #{options[:replace_with]}"
    search_and_replace options[:directory], options[:search], options[:replace_with]
    puts "Complete! See ./output"
  end

  desc "Reads the file and replaces search param with replace_with param"
  task :file do 
    puts "Search and Replace in File"
    options = {}
    o = OptionParser.new
    o.banner = "Usage: rake search_and_replace:run -- [options]"
    o.on("-f FILE", "--file FILE") { |file|
      options[:file] = file
    }
    o.on("-s SEARCH", "--search SEARCH") { |search|
      options[:search] = search
    }
    o.on("-r REPLACE_WITH", "--replace_with REPLACE_WITH") { |replace_with|
      options[:replace_with] = replace_with
    }
    args = o.order!(ARGV) {}
    o.parse!(args)
    puts "File: #{options[:file]}"
    puts "Search: #{options[:search]}"
    puts "Replace: #{options[:replace_with]}"
    search_and_replace_in_file options[:file], options[:search], options[:replace_with]
    puts "Complete! See ./output"
  end

  def search_and_replace directory, search, replace
    filenames = Dir.glob("#{directory}/**")
    filenames.each do |filename|
      if File.directory?(filename)
        FileUtils.r_p("output/#{filename}")
        search_and_replace(filename, search, replace) 
        next
      end
      search_and_replace_in_file(filename, search, replace)
    end
  end

  def search_and_replace_in_file filename, search, replace
    count = 0
    file = File.open(filename)
    File.open("output/#{filename}", "w") do |output| 
      file.readlines.each do |line|
        next if line.nil?
        newline = line.gsub(/#{Regexp.quote(search)}/,replace)
        output.write(newline)
      end
    end
  end
end


namespace :search_and_count do 
  desc "Reads files in a directory and counts occurences of a given string in each file."
  task :directory do
    puts "---Search and Count in Directory---"

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
  task :file do
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
    count = search_and_count_in_file(options[:file], options[:search])
    puts "There are #{count} occurences of #{options[:search]}"
  end

  def search_and_count directory, search
    count = 0
    filenames = Dir.glob("#{directory}/**")
    filenames.each do |filename|
      if File.directory?(filename)
        search_and_count(filename, search) 
        next
      end
      count += search_and_count_in_file(filename, search)
    end
    count
  end

  def search_and_count_in_file filename, search
    count = 0
    file = File.open(filename)
    file.readlines.each do |line|
      count += 1 if line.match(/#{Regexp.quote(search)}/) 
    end
    count
  end
end
