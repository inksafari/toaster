# Thanks 
# https://github.com/progit/progit2/blob/master/Rakefile
# https://github.com/hnakamur/asciidoctor_template/blob/master/Rakefile
# oreillymedia/asciidoctor-htmlbook/blob/master/scripts/convert_book.rb
Rake.application.options.trace = true

require 'fileutils'
require 'pandoc-ruby'

MD_SOURCE_DIRECTORY = "mkd"
AD_OUTPUT_DIRECTORY = "adoc/_temp"
SOURCE_DIRECTORY = "adoc"
OUTPUT_DIRECTORY = "dist"
BOOK_OUTPUT_NAME = "sample"

task :default => :html

desc 'Convert Markdown files to AsciiDoc files'
task :adoc do
  Dir.glob("#{MD_SOURCE_DIRECTORY}/**/*.md") do |file|
    puts "Converting #{File.basename(file)}"
    md = File.open(file).read
    ad = PandocRuby.new(md, :from => :markdown, :to => :asciidoc)
    filename  = "#{AD_OUTPUT_DIRECTORY}/#{File.basename(file,'.*')}.adoc"
    File.open(filename, 'w') { |file| file.write(ad) }
  end
  puts 'Done!'
end

task :clean do
  FileUtils.rm_r Dir.glob("#{OUTPUT_DIRECTORY}/*.{html,pdf,png,svg,cache}"), :force => true
  FileUtils.cp "404.html", "#{OUTPUT_DIRECTORY}"
end

# https://github.com/asciidoctor/asciidoctor-pdf/blob/master/docs/theming-guide.adoc
# https://github.com/asciidoctor/asciidoctor-pdf/issues/82#issuecomment-120799563
task :pdf => :clean do
  puts 'Converting to PDF... (this one takes a while)'
  sh %Q{
    bundle exec asciidoctor-pdf \
      -r asciidoctor-pdf-cjk \
      -r asciidoctor-pdf-cjk-kai_gen_gothic \
      -a pdf-style=KaiGenGothicTW \
      -o #{OUTPUT_DIRECTORY}/#{BOOK_OUTPUT_NAME}.pdf \
      #{SOURCE_DIRECTORY}/book.adoc 2>/dev/null
  }
  puts "-- PDF  output at #{BOOK_OUTPUT_NAME}.pdf"
end

task :html => :clean do
  Dir.glob("#{SOURCE_DIRECTORY}/{site,ch**}/*.adoc") do |file|
    puts "Converting #{File.basename(file)}"
    sh %Q{
      bundle exec asciidoctor -r asciidoctor-diagram \
        -d book -a lang=zh-Hant-TW \
        -a source-highlighter=coderay \
        -a stylesdir=../../themes -a stylesheet=colony.css \
        -a idprefix! -a idseparator=- -a sectanchors \
        -o #{OUTPUT_DIRECTORY}/#{File.basename(file,'.*')}.html \
        #{file}
    }
  end
  puts 'Done!'
end

desc 'Publishing the website via rsync'
task :deploy do
  puts 'Publishing the website...'

  # $ chown -R user:group /path/to/site
  # $ chmod u+s /path/to/site 
  # digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys
  # ~/.ssh/config
  #  Host slc18
  #  HostName server_ip
  #  Port 2222
  #  User www-data
  #  IdentityFile ~/.ssh/id_rsa

  # -a, --archive; -v, --verbose; -z, --compress;   
  # -P, --partial --progress;  (src)       (dest)
  `rsync -avzP --delete -e ssh dist/ slc18:/var/www/site/`
  puts 'The website is now published!'
end
