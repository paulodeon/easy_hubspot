# EasyHubspot
Stable: ![stable version](https://img.shields.io/badge/version-1.0.1-green)
Latest: ![latest version](https://img.shields.io/badge/version-1.0.1-yellow)
[![CI](https://github.com/oroth8/easy_hubspot/actions/workflows/ci.yml/badge.svg)](https://github.com/oroth8/easy_hubspot/actions/workflows/ci.yml)
[![Code Climate](https://codeclimate.com/github/oroth8/easy_hubspot/badges/gpa.svg)](https://codeclimate.com/github/oroth8/easy_hubspot)
[![Test Coverage](https://api.codeclimate.com/v1/badges/c55dfda6142769b8209c/test_coverage)](https://codeclimate.com/github/oroth8/easy_hubspot/test_coverage)

This is a lightweight wrapper for the Hubspot API. It is designed to be easy to use and to provide a simple setup for the most common use cases.

This gem utilizes the `v3` hubspot-api

## CRM Objects
- [Contacts](#contacts)
- [Deals](#deals)
- [Products](#products)
- [Line Items](#line-items)

- [Error Handling](#error-handling)

### Dependencies
- [gem "httparty", "~> 0.22.0"](https://github.com/jnunemaker/httparty)

### Compatibility
- `ruby >= 2.6.10`
- `rails >= 6.0`

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'easy_hubspot'
```

## Usage

Add the following to your `config/initializers/easy_hubspot.rb` file:

```ruby
EasyHubspot.config do |c|
  c.access_token = 'YOUR API KEY'
  c.base_url = 'https://api.hubapi.com/'
end
```

Or run the generator:

```bash
rails g easy_hubspot:install
```

### Contacts

Please refrence the [hubspot docs](https://developers.hubspot.com/docs/api/crm/contacts)

```ruby
# Create a contact
  # required: body
  # returns: parsed hubspot contact
  EasyHubspot::Contact.create_contact(properties: { email: '', firstname: '', lastname: '' , etc: ''})

# Update a contact
# required: contact_id, body
# - contact_id: can be a hubspot contact_id or email
# returns: parsed hubspot contact
  EasyHubspot::Contact.update_contact(123, properties: { email: '', firstname: '', lastname: '' , etc: ''})

# Get a contact
# required: contact_id
# - contact_id: can be a hubspot contact_id or email
# returns: parsed hubspot contact
  EasyHubspot::Contact.get_contact(123)
# or
  EasyHubspot::Contact.get_contact('test@gmail.com')

# Get all contacts
# returns: parsed hubspot contacts
  EasyHubspot::Contact.get_contacts

# Delete a contact
# required: contact_id
# - contact_id: can be a hubspot contact_id or email
# returns: {status: 'success'}
  EasyHubspot::Contact.delete_contact(123)
# or
  EasyHubspot::Contact.delete_contact('test@gmail.com')

# Update or Create a contact
# required: email, body
# returns: parsed hubspot contact
  EasyHubspot::Contact.update_or_create_contact(properties: { email: '', firstname: '', lastname: '' , etc: ''})


# Parse hubspot contact example
{:id=>"701",
 :properties=>
  {:createdate=>"2023-02-08T20:10:36.858Z",
  :email=>"amber_becker@quigley.io",
  :firstname=>"Amber",
  :hs_content_membership_status=>"inactive",
  :hs_is_contact=>"true",
  :hs_is_unworked=>"true",
  :hs_object_id=>"701",
  :hs_pipeline=>"contacts-lifecycle-pipeline",
  :lastmodifieddate=>"2023-02-14T18:24:07.654Z",
  :lastname=>"Quigley",
  :lifecyclestage=>"lead"},
 :createdAt=>"2023-02-08T20:10:36.858Z",
 :updatedAt=>"2023-02-14T18:24:07.654Z",
 :archived=>false}
```

### Deals
```ruby
# Create a deal
  # required: body
  # returns: parsed hubspot deal
  EasyHubspot::Deal.create_deal(properties: { dealname: '', amount: '', etc: ''})

# Update a deal
# required: deal_id, body
# - deal_id: must be a hubspot deal_id
# returns: parsed hubspot deal
  EasyHubspot::Deal.update_deal(123, properties: { dealname: '', amount: '', etc: ''})

# Get a deal
# required: deal_id
# - deal_id: must be a hubspot deal_id
# returns: parsed hubspot deal
  EasyHubspot::Deal.get_deal(123)

# Get all deals
# returns: parsed hubspot deals
  EasyHubspot::Deal.get_deals

# Delete a deal
# required: deal_id
# - deal_id: must be a hubspot deal_id
# returns: {status: 'success'}
  EasyHubspot::Deal.delete_deal(123)
```

### Products
Please refrence the [hubspot docs](https://developers.hubspot.com/docs/api/crm/products)
```ruby
# Create a product
  # required: body
  # returns: parsed hubspot product
  EasyHubspot::Product.create_product(properties: { name: '', price: '', etc: ''})

# Update a product
# required: product_id, body
# - product_id: must be a hubspot product_id
# returns: parsed hubspot product
  EasyHubspot::Product.update_product(123, properties: { name: '', price: '', etc: ''})

# Get a product
# required: product_id
# - product_id: must be a hubspot product_id
# returns: parsed hubspot product
  EasyHubspot::Product.get_product(123)

# Get all products
# returns: parsed hubspot products
  EasyHubspot::Product.get_products

# Delete a product
# required: product_id
# - product_id: must be a hubspot product_id
# returns: {status: 'success'}
  EasyHubspot::Product.delete_product(123)
```

### Line Items
Please refrence the [hubspot docs](https://developers.hubspot.com/docs/api/crm/line-items)
```ruby
# Create a line item
  # required: body
  # Use hs_product_id property to base on an existing product
  # returns: parsed hubspot line item
  EasyHubspot::LineItem.create_line_item(properties: { quantity: '', hs_product_id: '', etc: ''})

# Update a line item
# required: line_item_id, body
# - line_item_id: must be a hubspot line_item_id
# returns: parsed hubspot line item
  EasyHubspot::LineItem.update_line_item(123, properties: { quantity: '', etc: ''})

# Get a line item
# required: line_item_id
# - line_item_id: must be a hubspot line_item_id
# returns: parsed hubspot line item
  EasyHubspot::LineItem.get_line_item(123)

# Get all line items
# returns: parsed hubspot line items
  EasyHubspot::LineItem.get_line_items

# Delete a line item
# required: line_item_id
# - line_item_id: must be a hubspot line_item_id
# returns: {status: 'success'}
  EasyHubspot::LineItem.delete_line_item(123)
```

## Multiple Access Tokens

If you need to choose your access token at call time, you can pass the access token as an argument to class methods as
follows:

```ruby
# Finds the contact using the access token provided at call time instead of the one set during initialization
EasyHubspot::Contact.get_contact(123, different_access_token)
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and the created tag, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/oroth8/easy_hubspot.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
