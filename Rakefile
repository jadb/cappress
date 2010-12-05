# Cappress Rakefile
#
# Author::    Jad Bitar (mailto:jadbitar@mac.com)
# Copyright:: Copyright (c) 2005-2010, WDT Media Corp (http://wdtmedia.net)
# License::   http://opensource.org/licenses/bsd-license.php The BSD License

require 'rubygems'
require 'rake'

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "cappress"
    gem.summary = "Deploy Wordpress websites using Capistrano"
    gem.description = "Deploy Wordpress websites using Capistrano"
    gem.email = "jadbitar@mac.com"
    gem.homepage = "http://github.com/jadb/cappress"
    gem.author = "Jad Bitar"
    gem.add_dependency "capistrano", ">= 2.5"
    gem.files = FileList["lib/**/*"].to_a
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: sudo gem install jeweler"
end