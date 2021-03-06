# Accepting a card payment

Cards are one of the most popular ways to pay online. Stripe offers several ways to accept card payments, depending on your business needs. This repository demonstrates how to use the Stripe Payments API to accept payments using a single-page application (selling a children's book).


## How to run locally

This sample includes a Node implementation of the server for the webhooks integration type: [using-webhooks](/using-webhooks) 

Follow the steps below to run locally.

**1. Clone and configure the sample**

Manually clone and configure the sample yourself, by opening a terminal window then cloning the accept-a-card-payment repo:

```
git clone https://github.com/vladarino/accept-a-card-payment
```

Go to the newly created `accept-a-card-payment` folder, then copy the .env.example file into a file named .env in the using-webhooks/server/node folder. 
For example:

```
cd accept-a-card-payment
cp .env.example using-webhooks/server/node/.env
```

You will need a Stripe account in order to run the demo. Once you set up your account, go to the Stripe [developer dashboard](https://stripe.com/docs/development#api-keys) to find your API keys.

Replace the Keys in the .env file created above with your keys:

```
STRIPE_PUBLISHABLE_KEY=<replace-with-your-publishable-key>
STRIPE_SECRET_KEY=<replace-with-your-secret-key>
```

You will set the ```STRIPE_WEBHOOK_SECRET``` entry in step 3 below
  

**2. Run the application:**

To run the Node server in `using-webhooks`:

```
cd using-webhooks/server/node
npm install
npm run start
```

If you see any errors in the terminal after executing the ``npm run start`` command, kill any running ``node`` processes then try again.

**3. Run a webhook locally:**

To test the `using-webhooks` integration with a local webhook on your machine, you can use the Stripe CLI to easily spin one up.

First, [install the CLI](https://stripe.com/docs/stripe-cli) and [link your Stripe account](https://stripe.com/docs/stripe-cli#link-account).

Second, open a new terminal window and execute the following:

```
stripe listen --forward-to localhost:4242/webhook
```

The CLI will print a webhook secret key to the console. Set `STRIPE_WEBHOOK_SECRET` to this value in your .env file mentioned above and restart the server (CTRL-C, then repeat Step 2).

You should see events logged in the console where the CLI is running.


**4. Access the application from a web browser:**

Submit test transactions using a desktop web browser (Chrome preferred):
http://localhost:4242/

After entering payment credentials and submitting an order, you may refresh the page to place additional orders.

**5: View results**

The terminal listening to webhooks (Step 3) will show webhook invocations.
The terminal running the server (Step 2) will show an entry for each attempted transaction.
The ``using-webhooks/server/node/log.txt`` log file will include a new line of transaction details for each completed transaction.



Credits:
[@vladandral](https://linkedin.com/in/vandral)


Code modified from https://github.com/stripe-samples/accept-a-card-payment Github repo, created by:
[@adreyfus-stripe](https://twitter.com/adrind)
[@bg-stripe](https://github.com/bg-stripe)
[@yuki-stripe](https://github.com/yuki-stripe)
[@thorsten-stripe](https://twitter.com/thorwebdev)




