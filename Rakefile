$:.unshift(File.join(File.dirname(__FILE__), 'lib'))

require 'rubygems'
require 'hoe'
require 'rake'
require 'spec/rake/spectask'
require 'roodi'

Hoe.plugin :gemspec
Hoe.spec 'roodi' do
  developer('Marty Andrews', 'marty@cogentconsulting.com.au')
  extra_deps << 'ruby_parse'
  remote_rdoc_dir = ''
end

def roodi(ruby_files)
  roodi = Roodi::Core::Runner.new
  ruby_files.each { |file| roodi.check_file(file) }
  roodi.errors.each {|error| puts error}
  puts "\nFound #{roodi.errors.size} errors."
end

desc "Run all specs"
Spec::Rake::SpecTask.new('spec') do |t|
  t.spec_files = FileList['spec/**/*spec.rb']
end

desc "Run Roodi against all source files"
task :roodi do
  pattern = File.join(File.dirname(__FILE__), "**", "*.rb")
  roodi(Dir.glob(pattern))
end

task :default => :spec
