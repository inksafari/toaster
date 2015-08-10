# toaster
> An experimental project.

## Requirements

* [Pandoc](http://pandoc.org/)
* [Ruby Language](https://www.ruby-lang.org/)（ I would like to recommend Ruby 2.2 or newer ）

## Installation

Install project dependencies with `bundle install --jobs 4 --path vendor/bundle --binstubs vendor/bin` and `bundle exec asciidoctor-pdf-cjk-kai_gen_gothic-install`（ Download Chinese/Japanese/Korean Fonts ）

## Usage

### My Project Structure

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
│   ├── sample_pdf.adoc
│   ├── site
│   │   └── index.adoc
│   └── _temp（ Unsorted Asciidoc Files ）
├── dist
│   ├── sample.pdf
│   ├── ch_ooo.html
│   └── ch_xxx.html
├── mkd（ Markdown Files ）
├── Rakefile
├── README.md
├── themes（ copy from themes_base/stylesheets dir ）
│   ├── asciidoctor.css
│   ├── colony.css
│   └── golo.css
├── themes_base
│   ├── [asciidoctor-stylesheet-factory repo](https://github.com/asciidoctor/asciidoctor-stylesheet-factory)
│   └── stylesheets dir
└── vendor
```

### Convert Markdown files to AsciiDoc files

`bundle exec rake adoc`

### Convert AsciiiDoc files to PDF files

`bundle exec rake pdf --quiet`

### Convert AsciiiDoc files to HTML files

`bundle exec rake html --quiet`

### Deploying the website

`bundle exec rake deploy`

## LICENSE

MIT License
