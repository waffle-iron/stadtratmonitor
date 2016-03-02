# Stadtratmonitor

## Setup

1. Install Ruby, Bundler, Elasticsearch
1. Start Elasticsearch: `elasticsearch`
1. Setup Rails app: `bundle && bundle exec rake db:setup`
1. Start Rails server: `bundle exec rails s`
1. Visit [http://localhost:3000](http://localhost:3000)

### Using docker

1. Install docker and docker-compose: https://docs.docker.com/compose/install/
1. Start the app: `docker-compose up`
1. TODO db:migrate, import data, setup index
1. Get the address of the docker host: `docker-machine ip default`
1. Point your browser to: 'http://\<IP of docker host\>:3000'

## Adding a data source (web scraper)
Example scraper: https://morph.io/ahx/city_council_leipzig_recent_papers

Scrapers are stored inside the database (see "Importer" model). To Add a new scraper, you have to create a new Importer record and set it's url field to Morph.io's [API URL field](https://morph.io/documentation/api?scraper=ahx%2Fcity_council_leipzig_recent_papers).

Adding a scraper manually:

1. Start Rails console `bundle exec rails console`
2. `Import.create(url: "https://api.morph.io/[scraper]/data.json?key=[api_key]&query=[sql]")`
3. `exit`

Now import everything via `bundle exec rake import_papers`.

[![Build Status](https://travis-ci.org/joergreichert/stadtratmonitor.png?branch=travis-docker)](https://travis-ci.org/joergreichert/stadtratmonitor)
