[ ![Codeship Status for christophe-hidutyfree/mangopay-ruby-sdk](https://codeship.io/projects/ce1d6490-e5a3-0131-6d1f-46277ec996ce/status)](https://codeship.io/projects/25775)

# MangoPay2 Ruby SDK

The gem for interacting with the version 2 of the MangoPay API.
See the [API documentation](http://docs.mangopay.com/api-references/)
for more details on the API.

Tested on the following versions of Ruby: 1.9.2, 1.9.3, 2.0.0

## NEWS

### Version 3.*
** BREAKING CHANGES **
This version (3.*) of the gem is targeting the MangoPay API Version 2.
It has a brand new structure to make the api calls easier to use
and is not backward compatible with 2.* series.

## Usage

### Install
* Install the gem by either running ```gem install mangopay```
or by adding it to your Gemfile ```gem 'mangopay'```

* The Rails users will be happy to know that there is a new generator script
that will help you configure your access to the MangoPay API version 2.
Simply run ``rails generate mangopay:install CLIENT_ID CLIENT_NAME CLIENT_EMAIL``
where CLIENT_ID is the id you will use to connect to the api
and CLIENT_NAME is a full name that will be use to identify all communications
between you and the MangoPay Team.

* Otherwise, call ```MangoPay.configure``` in your script as shown in the snippet below.

### Examples

```ruby
require 'mangopay'

# configuration (not required if Rails generator fired as above)
MangoPay.configure do |c|
  c.preproduction = true
  c.client_id = 'YOUR_CLIENT_ID'
  c.client_passphrase = 'YOUR_CLIENT_PASSWORD'
end

# get some user by id
john = MangoPay::User.fetch(john_id) # => {FirstName"=>"John", "LastName"=>"Doe", ...}

# update some of his data
MangoPay::NaturalUser.update(john_id, {'LastName' => 'CHANGED'}) # => {FirstName"=>"John", "LastName"=>"CHANGED", ...}

# get all users (with pagination)
pagination = {'page' => 1, 'per_page' => 8} # get 1st page, 8 items per page
users = MangoPay::User.fetch(pagination) # => [{...}, ...]: list of 8 users data hashes
pagination # => {"page"=>1, "per_page"=>8, "total_pages"=>748, "total_items"=>5978}

# get John's bank accounts
accounts = MangoPay::BankAccount.fetch(john_id) # => [{...}, ...]: list of accounts data hashes (10 per page by default)
```

### Tests
Make sure that you have run: ```bundle install```
Then you just have to run rspec ```rspec``` to run all the test suite.
Feel free to report any test failure by creating an issue
on the [Gem's Github](https://github.com/MangoPay/mangopay2-ruby-sdk/issues)

## Contributing

1. Fork the repo.

2. Run the tests. We only take pull requests with passing tests, and it's great
to know that you have a clean slate: `bundle && bundle exec rake`

3. Add a test for your change. Only refactoring and documentation changes
require no new tests. If you are adding functionality or fixing a bug, we need
a test!

4. Make the test pass.

5. Push to your fork and submit a pull request.

At this point you're waiting on us. We like to at least comment on, if not
accept, pull requests within three business days (and, typically, one business
day). We may suggest some changes or improvements or alternatives.

Syntax:

* Two spaces, no tabs.
* No trailing whitespace. Blank lines should not have any space.
* Prefer &&/|| over and/or.
* MyClass.my_method(my_arg) not my_method( my_arg ) or my_method my_arg.
* a = b and not a=b.
* Follow the conventions you see used in the source already.

A contribution can also be as simple as a +1 on issues tickets to show us
what you would like to see in this gem.

That's it for now. Good Hacking...
