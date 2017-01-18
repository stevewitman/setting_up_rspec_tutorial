YOUTUBE: Setting Up Automated Testing with RSpec
https://www.youtube.com/watch?v=UggLiefD02Q

rails new MusicShop –T

*Gemfile*
```
group :development, :test do
  gem 'rspec-rails', '~> 3.5'
end
```
```
bundle install
```
```
rails g rspec:install
```

*Gemfile*
```
group :test do
  gem 'database_cleaner'
end
```

(database_cleaner cleans test database after running test
```
bundle install
```

*rails_helper.rb*
(after require 'rspec/rails' add)
```
require 'database_cleaner'
```
and scroll down and change

config.use_transactional_fixtures = true
to
```
config.use_transactional_fixtures = false
```

(for test that require JS, truncation is the preferred strategy)
(just below that add … )
```
config.before(:suite) do
  DatabaseCleaner.clean_with(:truncation)
end

config.before(:each) do |example|
  DatabaseCleaner.strategy = example.metadata[:js] ? :truncation : :transaction
  DatabaseCleaner.start
end

config.after(:each) do
  DatabaseCleaner.clean
end
```

(to write feature specs we will use Capybara to simulate how the user interacts with the app...)

*Gemfile*

(add to group :test do)
```
gem 'capybara'
```
```
bundle install
```
*rails_helper.rb*
(after require 'database_cleaner' add)
```
require 'capybara/rspec'
```
*.rspec*
(after --require spec_helper add to bottom of file)
```
--format doc
```
