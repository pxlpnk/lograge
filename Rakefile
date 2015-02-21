require 'bundler/gem_tasks'

require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new

require 'rubocop/rake_task'
RuboCop::RakeTask.new

desc 'Run specs, rubocop and reek'
task ci: %w(spec rubocop mutant)

task default: :ci

desc 'Mutant Testing'
task :mutant do
  require 'action_pack'
  require 'mutant'

  pattern = ENV.fetch('PATTERN', 'Lograge*')
  opts    = ENV.fetch('MUTANT_OPTS', '').split(' ')
  result  = Mutant::CLI.run(%w(-Ilib -rlograge --use rspec --score 100) + opts + [pattern])
  fail unless result == Mutant::CLI::EXIT_SUCCESS
end
