# frozen_string_literal: true

# Add your own tasks in files placed in lib/tasks ending in .rake,
# for example lib/tasks/capistrano.rake, and they will automatically be available to Rake.

require File.expand_path('../config/application', __FILE__)

Rails.application.load_tasks

if Rails.env.development? || Rails.env.test?
  require 'rubocop/rake_task'
  RuboCop::RakeTask.new(:rubocop)

  task :rails_best_practices do
    sh('rails_best_practices . -e "db/schema.rb"')
  end

  task :brakeman do
    puts 'Running Brakeman'
    sh('brakeman -q -z -o tmp/brakeman.html --except SSLVerify')
  end

  task default: [:rubocop, :rails_best_practices, :brakeman, 'bundler:audit']
end

