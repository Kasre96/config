# Deploying a Laravel application on Heroku

## Prerequisites
- Some PHP and Laravel Knowldege - [Getting Started with Laravel](https://laravel.com/)
- Heroku account. Its free and instant - [Heroku Sign Up](https://signup.heroku.com/signup/dc)
- Composer installed locally
- Git

## 1. Crafting a Laravel application
If you already have your Laravel application, you can skip this step. If not, craft a new Laravel application into your local computer.

`composer create-project laravel/laravel --prefer-dist my-laravel-app`

## 2. Install Heroku CLI
You'll need heroku CLI to deploy to heroku. 

If you are on Linux, run this quick command to install instantly

`sudo snap install --classic heroku`

If on windows/mac, follow the instructions [here](https://devcenter.heroku.com/articles/heroku-cli).

## 3. Deploy to Heroku
### Add Git
`cd into the my-laravel-app`

`git init`

`git add .`

`git commit -m "my new laravel app"`

### Login to heroku CLI
From your terminal, run `heroku login` and follow the instructions to login.

### Create heroku app
Now its time to create your heroku app. This acts like your heroku git repository.

Run `heroku create my-laravel-app`

### Create a Procfile in your project
By default, Heroku will launch an Apache web server together with PHP to serve applications from the root directory of the project.

However, your application’s document root is the public/ subdirectory, so you need to create a Procfile that [configures the correct document root:](https://devcenter.heroku.com/articles/custom-php-settings#setting-the-document-root)

From your Terminal, run:

`echo "web: vendor/bin/heroku-php-apache2 public/" > Procfile`

`git add .`

`git comit -m "add procfile for heroku"`

### Set Laravel encryption key
The application’s encryption key is used by Laravel to encrypt user sessions and other information. Its value will be read from the `APP_KEY` environment variable.

As it must comply with the rules of the selected cipher in the configuration, the easiest way to generate a valid key is using the `php artisan key:generate --show` command, which will print a key that you can copy and then paste into the next step.

You can simply [set environment variables using the `heroku config command`](https://devcenter.heroku.com/articles/config-vars), so run a heroku `config:set` as the last step before deploying your app for the first time:

From your terminal:

`heroku config:set APP_KEY=$(php artisan --no-ansi key:generate --show)`

### Push to heroku
`git push heroku master`

### Run any php commands from heroku bash
To run any commands on heroku, you'll need to open heroku bash

`heroku run bash`

Then run any wished comand

`composer install`

## Run
To run the app, run `heroku open` from your terminal or navigate to `my-laravel-app.herokuapp.com` in your browser.

## Reference
[Heroku Dev Center](https://devcenter.heroku.com/articles/getting-started-with-laravel)

# Yours Truly
[Isaac Mutie](https://github.com/Kasre96)
