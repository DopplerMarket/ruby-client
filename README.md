# DEPRECATED AND SCHEDULED FOR REMOVAL FROM RUBYGEMS JANUARY 15, 2021

The [doppler](https://rubygems.org/gems/doppler) and [doppler-client](https://rubygems.org/gems/doppler-client) packages are deprecated and **scheduled for removal from RubyGems** on January 15, 2021. Learn how to [migrate to the new CLI](https://docs.doppler.com/docs/saying-goodbye-to-the-doppler-client-packages-node-cli).

# Doppler Ruby Library

[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/DopplerHQ/ruby-client)
[![image](https://img.shields.io/gem/v/doppler-client.svg)](https://rubygems.org/gems/doppler-client)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/92ec3d37764c40da8dffb6a85c6cbfa4)](https://www.codacy.com/app/Doppler/ruby-client?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=DopplerHQ/ruby-client&amp;utm_campaign=Badge_Grade)

The Doppler Ruby library provides convenient access to the Doppler API from
applications written for **only** server-side code.

## Installation

Install the gem with:
``` bash
gem install doppler
```

## Usage

The package needs to be configured with your account's api key which is available in your [Doppler account](https://doppler.com/workplace/api_key), pipeline identifier and the environment name:


### Environment Variables Required
Please add these environment variables to your `.env` file in the root directory or on your infra provider.

```
DOPPLER_API_KEY = <API Key>
DOPPLER_PIPELINE = <Pipeline ID>
DOPPLER_ENVIRONMENT = <Environment Name>
```

### Lookup Priority
Doppler will look for these variables in 3 places with the following priority:

1. Passed in as initialization arguments
2. Read from environment variables
3. Read from `.env` file


### Install with Environment Variables
This installation method will expect the `DOPPLER_API_KEY`, `DOPPLER_PIPELINE`, `DOPPLER_ENVIRONMENT` as environment variables.

``` ruby
require "doppler"
Doppler::Client.new()

# Rest of Application
```

### Install with ENV File
This installation method will expect the `DOPPLER_API_KEY`, `DOPPLER_PIPELINE`, `DOPPLER_ENVIRONMENT` in a `.env` file.

``` ruby
require "doppler"

Doppler.configure do |config|
  config.env_filepath = ".env"   # Defaults to ".env"
end


Doppler::Client.new()

# Rest of Application
```

### Install with Arguments
This installation method will expect the `api_key`, `pipeline`, `environment` as arguments.

``` ruby
require "doppler"

Doppler.configure do |config|
  config.api_key = ENV["DOPPLER_API_KEY"]
  config.pipeline = ENV["DOPPLER_PIPELINE"]
  config.environment = ENV["DOPPLER_ENVIRONMENT"]
end


Doppler::Client.new()

# Rest of Application
```

## Key Best Practices

So if Doppler stores my environment variables, where should I keep my Doppler API keys?

That is a great question! We recommend storing your `DOPPLER_API_KEY`, `DOPPLER_PIPELINE`, and `DOPPLER_ENVIRONMENT` 
in a `.env` file or with your infra provider. That means the only variables you should be storing in your local environment are the Doppler keys. All other variables should be be fetched by the Doppler client.


### Disable Overriding Environment Variables
If you would like to disable overriding environment variables, use this follow field.

``` ruby
Doppler.configure do |config|
  config.override = false
end

doppler = Doppler::Client.new()

# Rest of Your Application
example_variable = doppler.get("EXAMPLE_VARIABLE")
```


## Ignoring Specific Variables

In the case you would want to ignore specific variables from Doppler, say a port set by Heroku, you can add it the `ignore_variables` field.

``` ruby
Doppler.configure do |config|
  config.ignore_variables = ["PORT"]
end
```

## Fallback to Backup

The Doppler client accepts a `backup_filepath` on init. If provided the client will write
the Doppler variables to a backup file. If the Doppler client fails to connect to our API
endpoint (very unlikely), the client will fallback to the variables provided in the backup file.

``` ruby
Doppler.configure do |config|
  config.backup_filepath = "./backup.env"
end
```

## Extra Information

- [Doppler](https://doppler.com)
- [API KEY](https://doppler.com/workplace/api_key)
