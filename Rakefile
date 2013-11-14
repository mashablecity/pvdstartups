#!/usr/bin/env rake

require 'crunchbase'
require 'yaml'

task :fetch_startups do
  Crunchbase::API.key = 'rw2uxnbdxphm5kq9ntjdn2x6' # ENV['CRUNCHBASE_API_KEY']

  city = Crunchbase::API.get_json_response('http://api.crunchbase.com/v/1/search.js?geo=providence')
  zip = Crunchbase::API.get_json_response('http://api.crunchbase.com/v/1/search.js?geo=02903')
  state = Crunchbase::API.get_json_response('http://api.crunchbase.com/v/1/search.js?geo=ri')

  startups = (city['results'] + zip['results'] + state['results']).uniq.
    select{|h| 'company' == h['namespace']}.sort_by{|h| h['name']}

  File.open('_data/startups.yml', 'w') do |file|
    file << startups.to_yaml
  end
end
