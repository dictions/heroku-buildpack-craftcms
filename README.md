# Heroku Buildpack for CraftCMS

> DISCLAIMER: This is not supported code, use at your own risk.

This is a helper buildpack for installing and keeping an updated version of CraftCMS without committing it to your repo.

## Requirements
Ensure that you're using the default Craft folder structure:

```
app/
	craft/
	public/
```

Also ensure that you have a `db.php` in your `craft/config` directory.

## Installation

### Add the Buildpack

Add this buildpack as the last buildpack in your heroku settings, after `heroku/php`

```
heroku buildpacks:set heroku/php
heroku buildpacks:add --index 1 https://github.com/dictions/heroku-buildpack-craftcms
```

> **Buildpack Requirements**
>
> This buildpack just manages Craft installation. As such, it relies on the `heroku/php` buildpack for PHP, Composer, and NGINX.

### Add Procfile

Add a Procfile in your app's root directory:

```
web: bin/start.sh
```

### Add Composer.json

Add a composer.json file in your app's root directory:

```json
{
	"require": {
		"php": "^5.3.0",
		"ext-mbstring": "*",
		"ext-imagick": "*"
	},
	"require-dev": {
		"heroku/heroku-buildpack-php": "*"
	}
}
```

## TODO
Improvements to be made later.

1. Better Procfile detection. Right now there will always be a Procfile in the root because of `heroku/php`.
2. Better support for choosing between NGINX/Apache
3. Install needed dependencies & composer plugins autonomously. I don't think composer.json is actually installing dependencies because composer runs before the Craft buildpack.