# Mailcatcher Docker Image

Docker image for the [mailcatcher][1] gem to use with docker-compose.


# Usage

In your `docker-compose.yml` file:

``` yaml
services
  mailcatcher:
    image: unboxed/mailcatcher
    ports:
      - "1025:1025"
      - "1080:1080"
  
  app:
    build: .
    env:
      - SMTP_HOST=mailcatcher
      - SMTP_PORT=1025
```

In your Rails app's `config/environments/development.rb` file:

``` ruby
# Use mailcatcher if configured
if ENV['SMTP_HOSTNAME'].present?
  config.action_mailer.delivery_method = :smtp
  config.action_mailer.smtp_settings = {
    address: ENV.fetch('SMTP_HOSTNAME'),
    port: ENV.fetch('SMTP_PORT')
  }
end
```


# License

MIT License - please see the project LICENSE file for details.

[1]: https://mailcatcher.me
