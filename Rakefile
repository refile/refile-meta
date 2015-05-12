require "bundler"

task :update do
  sh "git submodule foreach git pull origin master"
end

task :spec do
  repos = `git config --list --file .gitmodules`.lines.map { |line| line.split(".")[1] }.uniq

  repos.each do |repo|
    path = File.expand_path("./#{repo}", File.dirname(__FILE__))
    Bundler.with_clean_env do
      cd path
      sh "bundle install"
      sh "bundle exec rake"
    end
  end
end

task default: :spec
