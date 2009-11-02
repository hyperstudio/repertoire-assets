require 'rubygems'
require 'rake/gempackagetask'

require 'merb-core'
require 'merb-core/tasks/merb'

GEM_NAME = "repertoire-assets"
GEM_VERSION = "0.1.0"
AUTHOR = "Your Name"
EMAIL = "Your Email"
HOMEPAGE = "http://merbivore.com/"
SUMMARY = "Merb plugin that provides ..."

spec = Gem::Specification.new do |s|
  s.rubyforge_project = 'merb'
  s.name = GEM_NAME
  s.version = GEM_VERSION
  s.platform = Gem::Platform::RUBY
  s.has_rdoc = true
  s.extra_rdoc_files = ["README", "LICENSE", "TODO"]
  s.summary = SUMMARY
  s.description = s.summary
  s.author = AUTHOR
  s.email = EMAIL
  s.homepage = HOMEPAGE
  s.add_dependency('rack', '~>1.0.1')
  s.add_dependency('nokogiri', '~>1.4.0')
  s.require_path = 'lib'
  s.files = %w(LICENSE README Rakefile TODO) + Dir.glob("{lib,spec,templates,vendor}/**/*")
  s.post_install_message = <<-POST_INSTALL_MESSAGE
#{'*'*50}

  One of your gems uses Repertoire asset support, which runs as rack middleware in front of a
  Merb or Rails application.
  
  In order to run, make sure your config.ru or config/init.ru files load the middleware, e.g.:

  ...
  use Repertoire::Assets::Middleware::Merb
  ...
    
  Immediately before the final run statement.  Also, you may want to turn on asset bundling and
  compression in your production environment (config/environments/production.rb):
  
  ...  
  c[:precache] = :compress
  ...  
  
  See the package documentation for other application-level configuration options.
  
#{'*'*50}
POST_INSTALL_MESSAGE
end

Rake::GemPackageTask.new(spec) do |pkg|
  pkg.gem_spec = spec
end

desc "install the plugin as a gem"
task :install do
  Merb::RakeHelper.install(GEM_NAME, :version => GEM_VERSION)
end

desc "Uninstall the gem"
task :uninstall do
  Merb::RakeHelper.uninstall(GEM_NAME, :version => GEM_VERSION)
end

desc "Create a gemspec file"
task :gemspec do
  File.open("#{GEM_NAME}.gemspec", "w") do |file|
    file.puts spec.to_ruby
  end
end

begin
  require 'spec'
  require 'spec/rake/spectask'

  task :default => [ :spec ]

  desc 'Run specifications'
  Spec::Rake::SpecTask.new(:spec) do |t|
    t.spec_opts << '--options' << 'spec/spec.opts' if File.exists?('spec/spec.opts')
    t.spec_opts << '--color' << '--format' << 'specdoc'
    begin
      require 'rcov'
      t.rcov_opts << '--exclude' << 'spec'
      t.rcov_opts << '--text-summary'
      t.rcov_opts << '--sort' << 'coverage' << '--sort-reverse'
    rescue LoadError
      # rcov not installed
    end
  end
rescue LoadError
  # rspec not installed
end
