# Archived

This project is archived. If someone has a working and _maintained_ fork please let me know and I will point people there. Thank you to all of you. This was a fun project and a technique that yieled (and still yields) interesting research. 

# oxml_xxe
This tool is meant to help test XXE vulnerabilities in ~~OXML document~~ file formats. Currently supported:

- DOCX/XLSX/PPTX
- ODT/ODG/ODP/ODS
- SVG
- XML
- PDF (experimental)
- JPG (experimental)
- GIF (experimental)

BH USA 2015 Presentation:

[Exploiting XXE in File Upload Functionality (Slides)](http://oxmlxxe.github.io/reveal.js/slides.html#/) [(Recorded Webcast)](https://www.blackhat.com/html/webcast/11192015-exploiting-xml-entity-vulnerabilities-in-file-parsing-functionality.html)

Blog Posts on the topic:

[Exploiting XXE Vulnerabilities in OXML Documents - Part 1](http://www.silentrobots.com/blog/2015/03/04/oxml_xxe/)

[Exploiting CVE-2016-4264 With OXML_XXE](https://www.silentrobots.com/blog/2016/10/02/exploiting-cve-2016-4264-with-oxml-xxe/)

# Build base docker

```
docker pull ruby:2.3.5
docker run -dit -p 4567:4567 ruby:2.3.5
docker exec -it container_id /bin/bash
apt-get update
apt-get install -y vim git
git clone https://github.com/BuffaloWill/oxml_xxe.git
cd oxml_xxe
vim Gemfile (Replace all content)
```
```
source 'https://rubygems.org'

ruby "2.3.5"

gem 'sinatra', '1.4.8'
gem 'haml'
gem 'rubyzip'
gem 'json','1.8.6' 
gem 'nokogiri'
gem 'data_mapper', '1.2.0'
gem 'dm-sqlite-adapter', '1.2.0'
```
```
gem install bundler
bundle install
ruby server.rb -o 0.0.0.0
```
Open http://localhost:4567

# Main Modes

There are two main modes:

## Build a File

Build mode adds a DOCTYPE and inserts the XML Entity into the file of the users choice.

## String Replace in File

String replacement mode goes through and looks for the symbol § in the document. The XML Entity ("&xxe;") replaces any instances of this symbol. Note, you can open the document in and insert § anywhere to have it replaced. The common use case would be a web application which reads in a xlsx and then prints the results to the screen. Exploiting the XXE it would be possible to have the contents printed to the screen.

