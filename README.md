# toaster
>A script to convert AsciiDoc documents into HTML or PDF. Thanks [Asciidoctor](http://asciidoctor.org/).

## Requirements

* [Pandoc](http://pandoc.org/)
* [Ruby Language](https://www.ruby-lang.org/)（ I would like to recommend Ruby 2.2 or newer ）
    * [Bundler Gem](http://bundler.io/)
* [Diagramming software](https://github.com/asciidoctor/asciidoctor-diagram)

## Installation

Install project dependencies with `bundle install --jobs 4 --path vendor/bundle --binstubs vendor/bin` and `bundle exec asciidoctor-pdf-cjk-kai_gen_gothic-install`（ Download Chinese/Japanese/Korean Fonts ）

## Usage

### Project Structure

```text
.
├── adoc
│   ├── ch_ooo
│   │   ├── ch_ooo.adoc
│   │   └── sections
│   │       ├── section_1.adoc
│   │       ├── section_2.adoc
│   │       └── section_3.adoc
│   ├── ch_xxx
│   │   ├── ch_xxx.adoc
│   │   └── sections
│   │       ├── section_a.adoc
│   │       ├── section_b.adoc
│   │       └── section_c.adoc
│   ├── docinfo-footer.html
│   ├── book.adoc
│   ├── site
│   │   └── index.adoc
│   └── _temp（ Unsorted AsciiDoc Files ）
├── dist
│   ├── sample.pdf
│   ├── ch_ooo.html
│   └── ch_xxx.html
├── mkd（ Markdown Files ）
├── Rakefile
├── 404.html
└── vendor
```

### Themes

1. `cd /path/to/project`
2. `git clone https://github.com/asciidoctor/asciidoctor-stylesheet-factory asf && cd asf`
3. Editing the config.rb： 'stylesheets' -> '../themes'
4. `bundle install --path vendor && bundle exec compass compile`

### Convert Markdown files to AsciiDoc files

`bundle exec rake adoc`

### Convert AsciiiDoc files to PDF 

`bundle exec rake pdf --quiet`

### Convert AsciiiDoc files to HTML Pages

`bundle exec rake html --quiet`

### Deploying the static website

`bundle exec rake deploy`

## LICENSE

MIT License
