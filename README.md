# NAME

Dancer2::Plugin::Auth::OAuth - OAuth for your Dancer2 app

# SYNOPSIS

    # just 'use' the plugin, that's all.
    use Dancer2::Plugin::Auth::OAuth;

# DESCRIPTION

Dancer2::Plugin::Auth::OAuth is a Dancer2 plugin which tries to make OAuth
authentication easy.

The module is highly influenced by [Plack::Middleware::OAuth](https://metacpan.org/pod/Plack::Middleware::OAuth) and Dancer 1
OAuth modules, but unlike the Dancer 1 versions, this plugin only needs
configuration (look mom, no code needed!). It automatically sets up the
needed routes (defaults to `/auth/$provider` and `/auth/$provider/callback`).
So if you define the Twitter provider in your config, you should automatically
get `/auth/twitter` and `/auth/twitter/callback`.

After a successful OAuth dance, the user info is stored in the session. What
you do with it afterwards is up to you.

# CONFIGURATION

The plugin comes with support for Facebook, Google, Twitter, GitHub, Stack
Exchange and LinkedIn (other providers aren't hard to add, send me a pull
request when you add more!)

All it takes to use OAuth authentication for a given provider, is to add
the configuration for it.

The YAML below shows all available options.

    plugins:
      "Auth::OAuth":
        prefix: /auth [*]
        success_url: / [*]
        error_url: / [*]
        providers:
          Facebook:
            tokens:
              client_id: your_client_id
              client_secret: your_client_secret
            fields: id,email,name,gender,picture
          Google:
            tokens:
              client_id: your_client_id
              client_secret: your_client_secret
          Twitter:
            tokens:
              consumer_key: your_consumer_token
              consumer_secret: your_consumer_secret
          Github:
            tokens:
              client_id: your_client_id
              client_secret: your_client_secret
          Stackexchange:
            tokens:
              client_id: your_client_id
              client_secret: your_client_secret
              key: your_key
            site: stackoverflow
          Linkedin:
            tokens:
              client_id: your_client_id
              client_secret: your_client_secret
            fields: id,num-connections,picture-url,email-address
          VKontakte: # https://vk.com
            tokens:
              client_id: '...'
              client_secret: '...'
            fields: 'first_name,last_name,about,bdate,city,country,photo_max_orig,sex,site'
            api_version: '5.8'
          Odnoklassniki: # https://ok.ru
            tokens:
              client_id: your_client_id
              client_secret: your_client_secret
              application_key: your_application_key
            method: 'users.getCurrentUser'
            format: 'json'
            fields: 'email,name,gender,birthday,location,uid,pic_full'
          MailRU:
            tokens:
              client_id: your_client_id
              client_private: your_client_private
              client_secret: your_client_secret
            method: 'users.getInfo'
            format: 'json'
            secure: 1
          Yandex:
            tokens:
              client_id: your_client_id
              client_secret: your_client_secret
            format: 'json'

\[\*\] default value, may be omitted.

# AUTHOR

Menno Blom <blom@cpan.org>

# COPYRIGHT

Copyright 2014- Menno Blom

# LICENSE

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.
