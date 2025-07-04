source "https://rubygems.org"

gem "jekyll", "~> 4.4"
gem "minima", "~> 2.5"

# Performance booster
gem "kramdown-parser-gfm"

gem "jekyll-plantuml"

group :jekyll_plugins do
  gem "asciidoctor-diagram"
  gem "asciidoctor-diagram-plantuml"
  gem "asciidoctor-diagram-ditaamini"
  gem "jekyll-asciidoc"
  gem "jekyll-feed"
  gem "jekyll-sitemap"
  gem "jekyll-seo-tag"
end

# Windows and JRuby compatibility
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Lock JRuby to specific version
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]
