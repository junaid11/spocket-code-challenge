# Project Name
Spocket Code Challenge

# Description

The app will create the customers for the payload received. The app will use the bulk insertion method for creating customers. App also has a scheduled worker that will complete the address information for the created customers that have missing address details. This worker will try 3 times to fetch address information for every customer that's persisted in the database. Also, to deal with the rate limit of external address API, the app first looks up addresses for provided zip code in the database and if it's not available there then the app hits the API for details. Address API is expected to restrict the app from making more than 500 requests, so we are only making this request in batches of 100 per time the worker is triggered. We will trigger the worker every 10 mins to avoid the rate limit as well. I tried on 50k requests, and its work fine for me. 

The following are the endpoints that are supported
- Endpoint to receive a list of customers data.
- Will store the address for each customer after finding it.

# System Architecture

- An endpoint to accepts a list of customers having zip-code as JSON.
- In a background worker, it will find the address for each customers whose address is not yet stored.

Advantages:
- Faster API's
- consistence results

Drawbacks:
- More dependency on viacep API

# Stack

* [Ruby](https://www.ruby-lang.org/en/)
* [Ruby on Rails](https://rubyonrails.org/)
* [RSpec](https://github.com/rspec/rspec-rails)


------------

## Getting Started

To get a local copy up and running follow these simple steps.

### Prerequisites

* `ruby 3.1.0`
* `rails 7.0.4`

### Installation

1. Extract the repo
2. Install the gems
`bundle install`
3. Start the server
`rails s`
4. Send the list
