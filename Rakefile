# encoding: utf-8

require 'rubygems'
require 'rake'
require 'tempfile'
require 'rake/clean'

task default: [
  :clean,
  :build,
  :pages,
]

def done(msg)
  puts msg + "\n\n"
end

desc 'Delete _site directory'
task :clean do
  rm_rf '_site'
  done 'Jekyll site directory deleted'
end

desc 'Build Jekyll site'
task :build do
  if File.exist? '_site'
    done 'Jekyll site already exists in _site'
  else
    system('jekyll build')
    fail 'Jekyll failed' unless $CHILD_STATUS.success?
    done 'Jekyll site generated without issues'
  end
end

desc 'Check the existence of all critical pages'
task pages: [:build] do
  File.open('_rake/pages.txt').map(&:strip).each do |p|
    file = "_site/#{p}"
    fail "Page #{file} is not found" unless File.exist? file
    puts "#{file}: OK"
  end
  done 'All files are in place'
end
