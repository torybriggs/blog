require 'toto'
require 'time'
require 'date'

@config = Toto::Config::Defaults

task :default => :new

desc "Create a new article."
task :new do
  title = ask('Title: ')
  category = ask('Category: ')
  if category == 'link'
    link = ask('Link: ')
  end
  slug = title.empty?? nil : title.strip.slugize

  article = {'title' => title, 'category' => category, 'link' => link, 'date' => Time.now.strftime("%d/%m/%Y"), 'timestamp' => Time.now}.to_yaml
  article << "\n"
  article << "Once upon a time...\n\n"

  path = "#{Toto::Paths[:articles]}/#{Time.now.strftime("%Y-%m-%d")}#{'-' + slug if slug}.md"

  unless File.exist? path
    File.open(path, "w") do |file|
      file.write article
    end
    toto "an article was created for you at #{path}."
  else
    toto "I can't create the article, #{path} already exists."
  end
end

desc "Publish my blog."
task :publish do
  toto "publishing your article(s)..."
  `git push heroku master`
  `git push git@github.com:torybriggs/blog.git`
end

def toto msg
  puts "\n  toto ~ #{msg}\n\n"
end

def ask message
  print message
  STDIN.gets.chomp
end

