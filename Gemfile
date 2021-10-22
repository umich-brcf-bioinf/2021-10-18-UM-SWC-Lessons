# frozen_string_literal: true

# "Some" VPNs (e.g. UMHS VPN) may balk at when downloading packages via https
# from rubygems. If ruby complains about not being able to download you could
# a) Temporarily suspend your VPN
# b) Switch to a more permissive VPN
# c) Switch the source to use http instead of https. Like so:
#    source 'http://rubygems.org'
# cgates 10/15/2021
source 'https://rubygems.org'
#source 'http://rubygems.org'

git_source(:github) {|repo_name| "https://github.com/#{repo_name}" }

# Synchronize with https://pages.github.com/versions
ruby '>=2.7.1'

gem 'github-pages', group: :jekyll_plugins
