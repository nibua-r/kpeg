# -*- ruby -*-

require 'rubygems'
require 'hoe'

Hoe.plugin :bundler
Hoe.plugin :gemspec
Hoe.plugin :git
Hoe.plugin :minitest
Hoe.plugin :travis

Hoe.spec 'kpeg' do
  self.readme_file = "README.rdoc"
  developer 'Evan Phoenix', 'evan@fallingsnow.net'
end

task :test => :parser

task :grammar do
  require 'kpeg'
  require 'kpeg/format'
  require 'kpeg/grammar_renderer'

  gr = KPeg::GrammarRenderer.new(KPeg::FORMAT)
  gr.render(STDOUT)
end

rule ".rb" => ".kpeg" do |t|
  ruby "-Ilib bin/kpeg -s -o #{t.name} -f #{t.source}"
end

PARSER_FILES = %w[
  lib/kpeg/string_escape.rb
  lib/kpeg/format_parser.rb
]

PARSER_FILES.map do |parser_file|
  file parser_file => 'lib/kpeg/compiled_parser.rb'
end

desc "build the parser"
task :parser => PARSER_FILES

# vim: syntax=ruby
