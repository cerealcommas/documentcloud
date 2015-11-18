# load `rake build/install/release tasks'
require 'bundler/setup'
require_relative './lib/document_cloud/version'

namespace :ruby do
  Bundler::GemHelper.install_tasks(:name => 'documentcloud')
end

require "rspec/core/rake_task"

desc "Run all specs"
RSpec::Core::RakeTask.new('spec')

desc "Run unit specs"
RSpec::Core::RakeTask.new('spec:unit') do |t|
  t.pattern = 'spec/unit/*_spec.rb'
end

desc "Run integration specs"
RSpec::Core::RakeTask.new('spec:integration') do |t|
  t.pattern = 'spec/integration/*_spec.rb'
end

desc "Run tests"
task :default => :spec
