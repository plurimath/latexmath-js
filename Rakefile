require 'bundler/setup'
require 'fileutils'
require 'closure-compiler'

task 'build' do
  sh 'git clone https://github.com/plurimath/latexmath.git || :'
  cd 'latexmath' do
    sh 'git checkout issue-6' # Temporary
    sh 'BUNDLE_GEMFILE= bundle install'
    sh 'BUNDLE_GEMFILE= bundle exec rake build-opal'
  end
  FileUtils.mkdir_p "dist"
  FileUtils.cp "latexmath/dist/latexmath.js", "dist/"

  cc = Closure::Compiler.new.compile(File.open('dist/latexmath.js', 'r'))
  File.write('dist/latexmath.min.js', cc)
end

task :default => :build
