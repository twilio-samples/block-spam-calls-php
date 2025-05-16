<!-- markdownlint-disable MD013 -->
# Block Spam Calls with PHP and Twilio

![testing workflow][testing_workflow_url]

This project shows how to use two Twilio Add-ons ([Marchex Clean Call][marchex_clean_call_url] and [Nomorobo Spam Score][nomorobo_spam_score_url].) from [the Twilio Add-ons Marketplace][twilio_addons_url] to block unwanted voice calls.

## How Does It Work?

The application is a small web application built around the Slim Framework.
When your Twilio number receives an inbound call, this code will check the spam rating of the phone number using both of the spam Add-ons.
If both of them deem the number to be spam, then the number will be blocked.
Otherwise, if the number is **not** deemed to be spam, the call will be forwarded to the customer

## Why Use the Application?

The application is a simple example of how to integrate Add-ons from the Twilio Marketplace into your application to help you determine if inbound phone calls are spam or not, i.e., telemarketers, auto-dialers, accidental hang-ups, and outright spam callers.
By using these Add-ons, you can save wasting your time answering unnecessary calls.

## Prerequisites

To use this application, you're going to need:

- A Twilio account (either free or paid) with a [Twilio phone number][twilio_phone_number_setup_url] that can handle phone calls.
  If you are new to Twilio, [create a free account][twilio_referral_url].
- PHP 8.3
- [Composer][composer_url] installed globally
- [ngrok][ngrok_url]

## ⚡️ Quick Start

### Install the Add-ons

The following guide will help you to [install Add-ons][twilio_addons_install]. You can access the Add-ons in [the Twilio console][twilio_console_addons_url].
The Spam Filtering Add-ons that are used on this application are (as mentioned earlier):

- [Marchex Clean Call][marchex_clean_call_url]
- [Nomorobo Spam Score][nomorobo_spam_score_url]

Once you've selected the Add-on, click on the **Install** button.
Then, you will see a pop-up window where you should read and agree the terms.
After that, click the **Agree & Install** button.
For this application, you just need to handle the incoming voice calls, so make sure that the **Incoming Voice Call** box for **Use In** is checked, then click **Save**.

### Set up the Application

After the above requirements have been met, clone this repository and change into the cloned directory with the following commands:

```bash
git clone git@github.com:settermjd/block-spam-calls-php.git
cd block-spam-calls-php
```

Then, install PHP's dependencies:

```bash
composer install
```

After that, you need to set the environment variables which the application requires.
These are your Twilio Account SID, Auth Token, and phone number.
To do that, first copy _.env.example_ (which has the variables defined but not set) as _.env_.

```bash
cp .env.example .env
```

Then, you need to retrieve your Twilio from the **Account Info** panel in [the Twilio Console Dashboard][twilio_console_url].
After you've retrieved them, update _.env_ as required.

### Start the Application

Now, start the application using the following command:

```bash
composer serve
```

### Expose the Application to the Public Internet

To forward incoming calls, your development server will need to be publicly accessible.
We recommend using [ngrok][ngrok_testing_webhooks_url] to do this, by running the following command:

```bash
ngrok http 8080
```

Once ngrok's started, copy the **Forwarding** URL from the output it writes to the terminal.

Now, it's time to update your Twilio phone number's configuration.
Under Phone Numbers > Manage > Active numbers click the phone number that you're using.
Then, under Voice Configuration set:

- **Configure with** to "Webhook, TwiML Bin, Function, Studio Flow, Proxy Service"
- **A call comes in** to "Webhook"
- The **URL** field next to **A call comes in** to the ngrok **Forwarding** URL that you copied from the ngrok terminal output
- **HTTP** next to the **URL** field to "HTTP POST"

After that's done, click **Save configuration**.
That's it for the configuration.

### Test the Application

To test the application, make a phone call to your Twilio phone number.
You should hear "_Welcome to the jungle_" in a female, British voice.

## Contributing

If you want to contribute to the project, whether you have found issues with it or just want to improve it, here's how:

- [Issues][issues_url]: ask questions and submit your feature requests, bug reports, etc
- [Pull requests][pull_requests_url]: send your improvements

## Resources

- [Check out the CodeExchange repository][code_exchange_url] for more information.

## Did You Find The Project Useful?

If the project was useful and you want to say thank you and/or support its active development, here's how:

- Add a GitHub Star to the project
- Write an interesting article about the project wherever you blog

## License

[MIT][mit_license_url]

## Disclaimer

No warranty expressed or implied. Software is as is.

[code_exchange_url]: https://github.com/twilio-labs/code-exchange/
[composer_url]: https://getcomposer.org
[issues_url]: https://github.com/settermjd/block-spam-calls-php/issues
[marchex_clean_call_url]: https://console.twilio.com/us1/develop/add-ons/catalog/XBac2c99d9c684a765ced0b18cf0e5e1c7
[mit_license_url]: http://www.opensource.org/licenses/mit-license.html
[ngrok_testing_webhooks_url]: https://www.twilio.com/blog/2015/09/6-awesome-reasons-to-use-ngrok-when-testing-webhooks.html
[ngrok_url]: https://ngrok.com
[nomorobo_spam_score_url]: https://console.twilio.com/us1/develop/add-ons/catalog/XB06d5274893cc9af4198667d2f7d74d09
[pull_requests_url]: https://github.com/settermjd/block-spam-calls-php/pulls
[testing_workflow_url]: https://github.com/settermjd/block-spam-calls-php/actions/workflows/php.yml/badge.svg
[twilio_addons_install]: https://www.twilio.com/docs/add-ons/install
[twilio_addons_url]: https://twilio.com/add-ons/
[twilio_console_addons_url]: https://www.twilio.com/console/add-ons
[twilio_console_url]: https://www.twilio.com/console
[twilio_phone_number_setup_url]: https://www.twilio.com/console/phone-numbers/incoming
[twilio_referral_url]: https://www.twilio.com/try-twilio
<!-- markdownlint-enable MD013 -->
