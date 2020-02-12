# Andesite
![loc](https://sloc.xyz/github/nektro/andesite)
[![license](https://img.shields.io/github/license/nektro/andesite.svg)](https://github.com/nektro/andesite/blob/master/LICENSE)
[![discord](https://img.shields.io/discord/551971034593755159.svg)](https://discord.gg/P6Y4zQC)
[![paypal](https://img.shields.io/badge/donate-paypal-009cdf)](https://paypal.me/nektro)
[![circleci](https://circleci.com/gh/nektro/andesite.svg?style=svg)](https://circleci.com/gh/nektro/andesite)
[![release](https://img.shields.io/github/v/release/nektro/andesite)](https://github.com/nektro/andesite/releases/latest)
[![goreportcard](https://goreportcard.com/badge/github.com/nektro/andesite)](https://goreportcard.com/report/github.com/nektro/andesite)
[![codefactor](https://www.codefactor.io/repository/github/nektro/andesite/badge)](https://www.codefactor.io/repository/github/nektro/andesite)

Share folders in an Open Directory without making your entire server public. Manages users with OAuth2.

## Getting Started
These instructions will help you get the project up and running. To obtain the binary you will use to run the app, follow the [Development](#development) or [Deployment](#deployment) sections for futher direction. Below, are general directions for all builds.


| Name | Type | Default | Description |
|------|------|---------|-------------|
| `--root` | `string` | none. | Path of root directory for `/files/`. |
| `--public` | `string` | none. | Path of root directory for `/public/`. |
| `--port` | `int` | `8000` | Port for web server to bind to. |
| `--base` | `string` | `/` | HTTP path of app root. |
### Options
Use these to configure your Andesite instance. All are optional. "Name" refers to the name of the CLI flag that may be used. "Config Name" refers to the key name inside of your `config.json`. More on that later.

### Creating Credentials
In order to create a "closed directory" with Andesite, you will need to create an app on your Identity Provider(s) of choice. See the [nektro/go.oauth2](https://github.com/nektro/go.oauth2#readme) docs for more detailed info on this process on where to go and what data you'll need.

Here you can also fill out a picture and description that will be displayed during the authorization of users on your chosen Identity Provider. When prompted for the "Redirect URI" during the app setup process, the URL to use will be `http://andesite/callback`, replacing `andesite` with any origins you wish Andesite to be usable from, such as `example.com` or `localhost:800`.

Once you have finished the app creation process you should now have a Client ID and Client Secret. These are passed into Andesite through flags as well.

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `--auth-{IDP-ID}-id` | `string` | none. | Client ID. |
| `--auth-{IDP-ID}-secret` | `string` | none. | Client Secret. |

The Identity Provider IDs can be found from the table in the [nektro/go.oauth2](https://github.com/nektro/go.oauth2#readme) documentation.

## Deployment
Pre-compiled binaries can be obtained from https://github.com/nektro/andesite/releases/latest.

## Development

### Prerequisites
- A directory you wish to proxy through Andesite
- The Go Language 1.12+ (https://golang.org/dl/)
- GCC on your PATH (for the https://github.com/mattn/go-sqlite3 installation)

### Installing
Run
```
$ go get -u github.com/nektro/andesite
```
and then make your way to `$GOPATH/src/github.com/nektro/andesite/`.

Once there, run:
```
$ go build
$ ./andesite
```

## Extras

### Discord Guild/Role Access Grant
Due to a limitation in the Discord API, in order to determine if a user has a role on a specific server, you must use a bot. To get started, go to https://discordapp.com/developers/applications/ and add a Bot user to your app and copy down the Bot Token. Now, to be able to give file/folder access to entire roles, we are going to be using more flags:

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `--discord-guild-id` | `string` | none. | Guild Snowflake. |
| `--discord-bot-token` | `string` | none. | Bot Token. |

Enabling these values will add a section to `http://andesite/admin` that you can input the role snowflakes and the path you are granting.

### Themes
Andesite supports making custom themes for the splash page and the various HTML templates throughout the program. Those are:
- `index.html` - [Default Source](./www/index.html)
    - The main page shown to all users at the root of the server.
- `response.hbs` - [Default Source](./www/response.hbs)
    - A generic page used to show errors and message to the user.
- `listing.hbs` - [Default Source](./www/listing.hbs)
    - The main directory listing page.
- `admin.hbs` - [Default Source](./www/admin.hbs)
    - The admin dashboard that allows editing the access of users
- `style.css` - [Default Source](./www/style.css)
    - Empty CSS file you can use to easily make style-only themes.

All or none of the files may be replaced when using a theme. To enable use of a theme, suppose the value passed to `--theme` was `example`. Doing this will tell Andesite to serve files from `.andesite/themes/example/`.

## Built With
- http://github.com/aymerick/raymond
- http://github.com/fsnotify/fsnotify
- http://github.com/nektro/go-util
- http://github.com/nektro/go.etc
- http://github.com/nektro/go.oauth2
- http://github.com/mitchellh/go-homedir
- http://github.com/rakyll/statik
- http://github.com/spf13/pflag
- http://github.com/valyala/fastjson

## Contributing
[![issues](https://img.shields.io/github/issues/nektro/andesite.svg)](https://github.com/nektro/andesite/issues)
[![pulls](https://img.shields.io/github/issues-pr/nektro/andesite.svg)](https://github.com/nektro/andesite/pulls)

We listen to issues all the time right here on GitHub. Labels are extensively to show the progress through the fixing process. Question issues are okay but make sure to close the issue when it has been answered! Off-topic and '+1' comments will be deleted. Please use post/comment reactions for this purpose.

When making a pull request, please have it be associated with an issue and make a comment on the issue saying that you're working on it so everyone else knows what's going on :D

## Contact
- hello@nektro.net
- Meghan#2032 on discordapp.com
- https://twitter.com/nektro

## License
Apache 2.0
