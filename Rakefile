require 'rubygems'
require 'bundler/setup'
require 'rspec/core/rake_task'

task :default => :test
task :test => :spec

if !defined?(RSpec)
  puts "spec targets require RSpec"
else
  desc "Run all examples"
  RSpec::Core::RakeTask.new(:spec) do |t|
    t.pattern = 'spec/**/*.rb'
    t.rspec_opts = ['-cfs']
  end
end

namespace :db do
  desc 'Auto-migrate the database (destroys data)'
  task :migrate => :environment do
    DataMapper.auto_migrate!
  end

  desc 'Auto-upgrade the database (preserves data)'
  task :upgrade => :environment do
    DataMapper.auto_upgrade!
  end
  
  desc 'Seed data'
  task :seed => :migrate do
    require 'yaml'
    YAML.load_file("music.yml").each do |attributes|
      Catalogue.import(attributes)
    end
  end
end

task :environment do
  require 'environment'
end
