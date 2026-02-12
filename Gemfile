source "https://rubygems.org"

gem "jekyll", "~> 3.9"
gem "kramdown-parser-gfm", "~> 1.1"
gem "webrick" # Ruby 3.0+ 需要

# 本地 Ruby 3.4+ 需要这些（GitHub Actions 用 Ruby 3.1 不需要，但加上不影响）
gem "base64"
gem "bigdecimal"
gem "csv"

group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-paginate"
  gem "jekyll-relative-links"
  gem "jekyll-seo-tag"
  gem "jekyll-sitemap"
end
