require "rake"
require "rake/clean"

autoload :Jekyll, 'jekyll'

desc "Build the site"
task :build do
  Jekyll::Commands::Build.process({})
end
CLEAN.include FileList["_site"]

desc "Serve the site"
task :run do
  Jekyll::Commands::Serve.process({})
end
