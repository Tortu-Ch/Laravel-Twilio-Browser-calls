<a  href="https://www.twilio.com">
<img  src="https://static0.twilio.com/marketing/bundles/marketing/img/logos/wordmark-red.svg"  alt="Twilio"  width="250"  />
</a>

# Browser Calls (Laravel)

[![Build Status](https://github.com/TwilioDevEd/browser-calls-laravel/workflows/Laravel%20CI/badge.svg)](https://github.com/TwilioDevEd/browser-calls-laravel/actions)

> We are currently in the process of updating this sample template. If you are encountering any issues with the sample, please open an issue at [github.com/twilio-labs/code-exchange/issues](https://github.com/twilio-labs/code-exchange/issues) and we'll try to help you.

Learn how to use [Twilio Client](https://www.twilio.com/client) to
make browser-to-phone and browser-to-browser calls with ease. The
unsatisfied customers of the Birchwood Bicycle Polo Co. need your
help!

[Read the full tutorial here](https://www.twilio.com/docs/tutorials/walkthrough/browser-calls/php/laravel)!

### Create a TwiML App

This project is configured to use a **TwiML App**, which allows us to easily set the voice URLs for all Twilio phone numbers we purchase in this app.

Create a new TwiML app at https://www.twilio.com/console/voice/twiml/apps and use its `Sid` as the `TWILIO_APPLICATION_SID` environment variable wherever you run this app.

Once you have created your TwiML app, configure your Twilio phone number to use it ([instructions here](https://www.twilio.com/help/faq/twilio-client/how-do-i-create-a-twiml-app)).

If you don't have a Twilio phone number yet, you can purchase a new number in your [Twilio Account Dashboard](https://www.twilio.com/user/account/phone-numbers/incoming).

### Run the application

1. Clone the repository and `cd` into it.
1. Install the application's php dependencies with [Composer](https://getcomposer.org/)

   ```bash
   $ composer install
   ```
1. The application uses [SQLite](https://www.sqlite.org/index.html) as the persistence layer. If you
   don't have it already, you should install it. On OSX and Linux you can install it using the corresponding OS package manager (OSX 10.4 and up ship with SQLite by default).
   Also check that you have the PHP SQLite driver installed (`php7.X-sqlite3`). 

1. Install the application's JavaScript dependencies with [NodeJS](https://nodejs.org/en/):
   ```bash
   $ npm install
   ```

1. Create a database.

   ```bash
   $ touch database/database.sqlite
   ```
1. Copy the sample configuration file and edit it to match your configuration.

    ```bash
    $ cp .env.example .env
    ```

   You can find your `TWILIO_ACCOUNT_SID` under your
   [Twilio Account Settings](https://www.twilio.com/user/account/settings). Set
   `TWILIO_APPLICATION_SID` to the app SID you created
   before. `TWILIO_NUMBER` should be set to the phone number you
   purchased above.

   The `API_KEY` and `API_SECRET` values are your REST API Key information needed
   to create an [Access Token](https://www.twilio.com/docs/iam/access-tokens).
   You can create [one here](https://www.twilio.com/console/project/api-keys).

1. Generate an `APP_KEY`:

   ```bash
   $ php artisan key:generate
   ```
1. Run the migrations:

   ```bash
   $ php artisan migrate
   ```
1. Load the seed data:

   ```bash
   $ php artisan db:seed
   ```
1. Build front-end assets.

   ```bash
   $ npm run dev
   ```
1. Run the application using Artisan.

   ```bash
   $ php artisan serve
   ```

   It is `artisan serve` default behavior to use `http://localhost:8000`
   when
   the application is run. This means that the ip addresses where your
   app will be reachable on you local machine will vary depending on the
   operating system.

   The most common scenario, is that your app will be reachable through
   address `http://127.0.0.1:8000`, and this is important because ngrok
   creates the tunnel using only that address. So, if `http://127.0.0.1:8000`
   is not reachable in your local machine when you run the app, you must
   tell artisan to use this address, like this:

   ```bash
   $ php artisan serve --host=127.0.0.1
   ```

1. Expose the application to the wider Internet using [ngrok](https://ngrok.com/)

   ```bash
   $ ngrok http 8000
   ```
   Once you have started ngrok, update your TwiML app's voice URL
   setting to use your ngrok hostname, so it will look something like
   this:

   ```
   https://<your-ngrok-subdomain>.ngrok.io/support/call
   ```

### Try it out

1. To create a support ticket go to the home page.
   On this page you could fill some fields and create a ticket or you can call to support.

   ```
   https://<your-ngrok-subdomain>.ngrok.io
   ```

   __Note:__ Make sure you use the `https` version of your ngrok URL as some
   browsers won't allow access to the microphone unless you are using a secure
   SSL connection.

1. To respond to support tickets go to the `dashboard` page (you should open two windows or tabs).
   On this page you could call customers and answers phone calls.

   ```
   https://<your-ngrok-subdomain>.ngrok.io/dashboard
   ```

### Dependencies

This application uses this Twilio helper library:
* [twilio-php](https://github.com/twilio/twilio-php)

### Run the tests

1. Run at the top-level directory:

   ```bash
   $ php artisan test
   ```

## Meta

* No warranty expressed or implied. Software is as is. Diggity.
* The CodeExchange repository can be found [here](https://github.com/twilio-labs/code-exchange/).
* MIT License
* Lovingly crafted by Twilio Developer Education.
