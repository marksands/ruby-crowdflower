require 'rubygems'
require 'rake'

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "ruby-crowdflower"
    gem.summary = %Q{a toolkit for the CrowdFlower API}
    gem.description = <<-EOF
A toolkit for interacting with CrowdFlower via the REST API.

This is alpha software. Have fun!

EOF
    gem.email = "brian@doloreslabs.com"
    gem.homepage = "http://github.com/dolores/ruby-crowdflower"
    gem.authors = ["Brian P O'Rourke", "Chris Van Pelt"]
    gem.add_dependency 'httparty', '>= 0.4.3'
  end

rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: sudo gem install jeweler"
end

task :default => :build

task :refresh_builder => [:build] do
  cp "pkg/ruby-crowdflower-#{File.read("VERSION").strip}.gem", "../builder/gems/cache/"
  rm_rf "../builder/gems/gems/ruby-crowdflower-#{File.read("VERSION").strip}/"
  `cd ../builder && bin/thor merb:gem:redeploy`
end

require 'rake/rdoctask'
Rake::RDocTask.new do |rdoc|
  if File.exist?('VERSION.yml')
    config = YAML.load(File.read('VERSION.yml'))
    version = "#{config[:major]}.#{config[:minor]}.#{config[:patch]}"
  else
    version = ""
  end

  rdoc.rdoc_dir = 'rdoc'
  rdoc.title = "ruby-crowdflower #{version}"
  rdoc.rdoc_files.include('README*')
  rdoc.rdoc_files.include('lib/**/*.rb')
end
