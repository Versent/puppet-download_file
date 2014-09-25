require 'puppetlabs_spec_helper/rake_tasks'
require 'puppet-lint/tasks/puppet-lint'
require 'puppet-syntax/tasks/puppet-syntax'
require 'puppet_blacksmith/rake_tasks'


if ENV['PUPPET_GEM_VERSION'] =~ /3.4/ && ENV['RUBY_VERSION'] !~ /1.8/
  require 'puppet-doc-lint/rake_task'
end


PuppetLint.configuration.fail_on_warnings
PuppetLint.configuration.relative = true
PuppetLint.configuration.send('disable_80chars')
PuppetLint.configuration.send('disable_class_inherits_from_params_class')
PuppetLint.configuration.send('disable_class_parameter_defaults')
PuppetLint.configuration.send('disable_documentation')
PuppetLint.configuration.send('disable_single_quote_string_with_variables')

Rake::Task[:lint].clear
PuppetLint::RakeTask.new :lint do |config|
  config.ignore_paths = ["**/spec/**/*.pp", "**/vendor/**/*.pp"]
  config.log_format = '%{path}:%{linenumber}:%{KIND}: %{message}'
end

exclude_paths = [
  "**/pkg/**/*.{pp,erb}",
  "**/vendor/**/*.{pp,erb}",
  "**/spec/**/*.{pp,erb}"
]

PuppetSyntax.exclude_paths = exclude_paths

desc "Run syntax, lint, and spec tests."
task :test => [
  "syntax:manifests",
  :lint,
  :spec
]
