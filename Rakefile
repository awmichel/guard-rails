require 'bundler'
Bundler::GemHelper.install_tasks

require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new(:spec)

require 'rake/version_task'
Rake::VersionTask.new do |task|
  task.with_git_tag = true
end

include Rake::DSL if defined?(Rake::DSL)
RVM_PREFIX = "rvm 1.8.7@guard-rails,1.9.3-p327@guard-rails,2.0.0@guard-rails do"


namespace :spec do
  desc "Run on three Rubies"
  task :platforms do
    exit $?.exitstatus unless system "#{RVM_PREFIX} bundle install"
    exit $?.exitstatus unless system "#{RVM_PREFIX} bundle exec rake spec"
  end
end

task :default => 'spec:platforms'

desc 'Push everywhere!'
task :publish do
  system %{git push origin}
  system %{git push guard}
  system %{git push gitcafe}
end
