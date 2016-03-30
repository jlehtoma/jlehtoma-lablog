
require "rubygems"

require "bundler/setup"
require "jekyll"

namespace :site do

  desc "Generate blog files"
  task :generate do
    Jekyll::Site.new(Jekyll.configuration({
      "source"      => ".",
      "destination" => "_site",
      "url"         => "http://cbig.github.io/gpan-connectivity"
    })).process
  end

  desc "Run Jekyll server with production config"
  task :run => [:generate] do
    puts "Rakefile: Running Jekyll server with a production configuration."
    system "jekyll serve --watch --config _config.yml,_production_config.yml"
  end

  desc "Run Jekyll server with development config"
  task :run_dev => [:generate] do
    puts "Rakefile: Running Jekyll server with a development configuration."
    system "jekyll serve --watch --config _config.yml,_development_config.yml"
  end
end
