# ------------------------------------------------------------------------------
# Environment variables:
#   SIMP_GEM_SERVERS | a space/comma delimited list of rubygem servers
#   PUPPET_VERSION   | specifies the version of the puppet gem to load
# ------------------------------------------------------------------------------
# NOTE: SIMP Puppet rake tasks support ruby 2.0 and ruby 2.1
# ------------------------------------------------------------------------------
puppetversion = ENV.key?('PUPPET_VERSION') ? "#{ENV['PUPPET_VERSION']}" : '~>3'
gem_sources   = ENV.key?('SIMP_GEM_SERVERS') ? ENV['SIMP_GEM_SERVERS'].split(/[, ]+/) : ['https://rubygems.org']

gem_sources.each { |gem_source| source gem_source }

group :test do
  gem "rake"
  gem 'puppet', puppetversion
  gem "rspec", '< 3.2.0'
  gem "rspec-puppet"
  gem "hiera-puppet-helper"
  gem "puppetlabs_spec_helper"
  gem "metadata-json-lint"
  gem "simp-rspec-puppet-facts", "~> 1.3"


  # simp-rake-helpers does not suport puppet 2.7.X
  if "#{ENV['PUPPET_VERSION']}".scan(/\d+/).first != '2' &&
      # simp-rake-helpers and ruby 1.8.7 bomb Travis tests
      # TODO: fix upstream deps (parallel in simp-rake-helpers)
      RUBY_VERSION.sub(/\.\d+$/,'') != '1.8'
    gem 'simp-rake-helpers'
  end
end

group :development, :unit_tests do
  gem 'rake', ' < 11.0',                                   :require => false if RUBY_VERSION =~ /^1\.8/
  gem 'rspec', '< 3.2',                                    :require => false if RUBY_VERSION =~ /^1\.8/
  gem 'json', '< 2.0',                                     :require => false if RUBY_VERSION =~ /^1\.[89]/
  gem 'json_pure', '< 2.0',                                :require => false if RUBY_VERSION =~ /^1\.[89]/
  gem 'rspec-puppet',                                      :require => false
  gem 'puppetlabs_spec_helper',                            :require => false
  gem 'metadata-json-lint',                                :require => false
  gem 'puppet-lint',                                       :require => false
  gem 'puppet-lint-unquoted_string-check',                 :require => false
  gem 'puppet-lint-empty_string-check',                    :require => false
  gem 'puppet-lint-spaceship_operator_without_tag-check',  :require => false
  gem 'puppet-lint-variable_contains_upcase',              :require => false
  gem 'puppet-lint-absolute_classname-check',              :require => false
  gem 'puppet-lint-undef_in_function-check',               :require => false
  gem 'puppet-lint-leading_zero-check',                    :require => false
  gem 'puppet-lint-trailing_comma-check',                  :require => false
  gem 'puppet-lint-file_ensure-check',                     :require => false
  gem 'puppet-lint-version_comparison-check',              :require => false
  gem 'rspec-puppet-facts',                                :require => false

  gem 'coveralls',                                         :require => false unless RUBY_VERSION =~ /^1\.8/
  gem 'simplecov', '~> 0.7.0',                             :require => false
  gem 'yard',                                              :require => false
  gem 'redcarpet', '~> 2.0',                               :require => false

  # mime-types-data requires Ruby version >= 2.0
  gem 'mime-types', '2.6.2' if RUBY_VERSION =~ /^1\.9/
end
