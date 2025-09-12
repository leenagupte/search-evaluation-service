source "https://rubygems.org"

gem "rails", "8.0.1"

gem "bootsnap"
gem "google-cloud-discovery_engine", "<= 2.2.0"
gem "google-cloud-discovery_engine-v1beta", "<= 0.22.1"
gem "google-cloud-storage"
gem "govuk_app_config"
gem "plek"
gem "prometheus-client"
gem "railties"

group :test do
  gem "climate_control"
  gem "grpc_mock"
  gem "json_schemer"
  gem "simplecov", require: false
  gem "timecop"
end

group :development, :test do
  gem "brakeman", require: false
  gem "byebug"
  gem "govuk_test"
  gem "rspec-rails"
  gem "rubocop-govuk"
end
