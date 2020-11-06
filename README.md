# ATH Móvil Business Webhooks

## Introduction
ATH Móvil Business Webhooks are a simple and secure way to notify your application of events that occur on your ATH Móvil Business account like receiving payments, receiving donations, sending refunds and more.

## Prerequisites
Before you begin, please review the following prerequisites:

#### ATH Móvil Business Account
1. An active ATH Móvil Business account is required to continue. To sign up, download "ATH Móvil Business" on the App Store or Play Store of your iOS or Android device.


2. Your ATH Móvil Business account needs to have a registered, verified and active ATH® card.

3. Have the public and private API keys of your Business account at hand. **You can view your API keys on the settings section of ATH Móvil Business for iOS or Android.**

#### Webhooks Listener
To receive notifications of events you need to first configure a webhook listener server that:
* Listens for incoming HTTP `POST` messages.
* Has a valid HTTPS certificate (not self-signed).
* Receives content in JSON format.

## Support
If you need help signing up, adding a card or have any other question please refer to https://athmovilbusiness.com/preguntas or contact our support team at (787) 773-5466. For technical support please complete the following form:  https://forms.gle/ZSeL8DtxVNP2K2iDA.

## Subscribe to Events
#### Using ATH Móvil Business
To subscribe your webhook listener to events using ATH Móvil Business for iOS or Android follow these steps:
1. Log in to ATH Móvil Business for iOS or Android.
2. Go to the Settings section.
3. Scroll down to the "Development" section and press the "Webhooks" option.
4. Provide the password of your ATH Móvil Business account on the prompt.
5. Enter the URL of your listener (endpoint URL that listens for incoming HTTP POST notification messages) on the "URL" field.
6. Toggle on or off the events to subscribe to.
7. Press "Save".

#### Using a Web Service
To subscribe your webhook listener to events you can use the following web service:
* Method:` POST`
* Headers: `Content-Type` -	`application/json`
* Endpoint: `https://www.athmovil.com/transactions/webhook/post`
* Body Example:
```javascript
{
    "publicToken": "kfejhbagflbkjlfbhnfbbf",
    "privateToken": "oiehfikjhesikjhnfiksf",
    "listenerURL": "https://your.website.com/webhook",
    "paymentReceivedEvent": true,
    "refundSentEvent": true,
    "donationReceivedEvent": true,
    "ecommercePaymentReceivedEvent": true,
    "ecommercePaymentCancelledEvent": true,
    "ecommercePaymentExpiredEvent": true
}
```
  * Provide the URL of your listener on the `listenerURL` field.
  * Subscribe or unsubscribe from events by configuring them to `true` or `false`, respectively.


## List of Events
The following is a list of the events that your webhook listener can receive along with an example of each event's JSON content.

### Simulated Payment
```javascript
{
    "transactionType" : "simulated",
    "status" : "completed",
    "date" : "2020-01-01 12:00:00.0",
    "referenceNumber" : "000000-00000000abcd",
    "dailyTransactionID" : "0001",
    "name" : "Valeria Herrero",
    "phoneNumber" : "7871234567",
    "email" : "email@example.com",
    "message" : "This is a message.",
    "total" : "3.00",
    "tax" : "1.00",
    "subtotal" : "2.00",
    "fee" : "0.06",
    "netAmount" : "0.94",
    "totalRefundedAmount" : "0.00",
    "metadata1" : "This is metadata1",
    "metadata2" : "This is metadata2",
    "items" : [
      {
        "quantity" : "1",
        "tax" : "1.00",
        "metadata" : "metadata test",
        "name" : "First Item",
        "description" : "This is a description.",
        "price" : "0.00"
      },
      {
        "quantity" : "1",
        "tax" : "1.00",
        "metadata" : "metadata test",
        "name" : "Second Item",
        "description" : "This is another description.",
        "price" : "1.00"
      }
    ]
}
```

### eCommerce Payment Completed
```javascript
{
    "transactionType" : "ecommerce",
    "status" : "completed",
    "date" : "2020-01-01 12:00:00.0",
    "referenceNumber" : "000000-00000000abcd",
    "dailyTransactionID" : "0001",
    "name" : "Valeria Herrero",
    "phoneNumber" : "7871234567",
    "email" : "email@example.com",
    "message" : "",
    "total" : "3.00",
    "tax" : "1.00",
    "subtotal" : "2.00",
    "fee" : "0.06",
    "netAmount" : "0.94",
    "totalRefundedAmount" : "0.00",
    "metadata1" : "This is metadata1",
    "metadata2" : "This is metadata2",
    "items" : [
      {
        "quantity" : "1",
        "tax" : "1.00",
        "metadata" : "metadata test",
        "name" : "First Item",
        "description" : "This is a description.",
        "price" : "0.00"
      },
      {
        "quantity" : "1",
        "tax" : "1.00",
        "metadata" : "metadata test",
        "name" : "Second Item",
        "description" : "This is another description.",
        "price" : "1.00"
      }
    ]
}
```

### eCommerce Payment Cancelled
```javascript
{
    "transactionType" : "ecommerce",
    "status" : "cancelled",
    "date" : "2020-01-01 12:00:00.0",
    "referenceNumber" : "",
    "dailyTransactionID" : "",
    "name" : "",
    "phoneNumber" : "",
    "email" : "",
    "message" : "",
    "total" : "3.00",
    "tax" : "1.00",
    "subtotal" : "2.00",
    "fee" : "0.00",
    "netAmount" : "0.00",
    "totalRefundedAmount" : "0.00",
    "metadata1" : "This is metadata1",
    "metadata2" : "This is metadata2",
    "items" : [
      {
        "quantity" : "1",
        "tax" : "1.00",
        "metadata" : "metadata test",
        "name" : "First Item",
        "description" : "This is a description.",
        "price" : "0.00"
      },
      {
        "quantity" : "1",
        "tax" : "1.00",
        "metadata" : "metadata test",
        "name" : "Second Item",
        "description" : "This is another description.",
        "price" : "1.00"
      }
    ]
}
```
*This event is only sent when end users cancel the web payment process. Payments cancelled on the iOS or Android integration do not trigger this event.*

### eCommerce Payment Expired
```javascript
{
    "transactionType" : "ecommerce",
    "status" : "expired",
    "date" : "2020-01-01 12:00:00.0",
    "referenceNumber" : "",
    "dailyTransactionID" : "",
    "name" : "",
    "phoneNumber" : "",
    "email" : "",
    "message" : "",
    "total" : "3.00",
    "tax" : "1.00",
    "subtotal" : "2.00",
    "fee" : "0.00",
    "netAmount" : "0.00",
    "totalRefundedAmount" : "0.00",
    "metadata1" : "This is metadata1",
    "metadata2" : "This is metadata2",
    "items" : [
      {
        "quantity" : "1",
        "tax" : "1.00",
        "metadata" : "metadata test",
        "name" : "First Item",
        "description" : "This is a description.",
        "price" : "0.00"
      },
      {
        "quantity" : "1",
        "tax" : "1.00",
        "metadata" : "metadata test",
        "name" : "Second Item",
        "description" : "This is another description.",
        "price" : "1.00"
      }
    ]
}
```
*This event is only sent when payments expire on web. Payments expired on the iOS or Android integration do not trigger this event.*

### Payment Received
```javascript
{
    "transactionType" : "payment",
    "status" : "completed",
    "date" : "2020-01-01 12:00:00.0",
    "referenceNumber" : "000000-00000000abcd",
    "dailyTransactionID" : "0001",
    "name" : "Valeria Herrero",
    "phoneNumber" : "7871234567",
    "email" : "email@example.com",
    "message" : "This is a message.",
    "total" : "1.00",
    "tax" : "0.00",
    "subtotal" : "0.00",
    "fee" : "0.06",
    "netAmount" : "0.94",
    "totalRefundedAmount" : "0.00",
    "metadata1" : "",
    "metadata2" : "",
    "items" : []
}
```

### Donation Received
```javascript
{
    "transactionType" : "donation",
    "status" : "completed",
    "date" : "2020-01-01 12:00:00.0",
    "referenceNumber" : "000000-00000000abcd",
    "dailyTransactionID" : "0001",
    "name" : "Valeria Herrero",
    "phoneNumber" : "7871234567",
    "email" : "email@example.com",
    "message" : "This is a message.",
    "total" : "1.00",
    "tax" : "0.00",
    "subtotal" : "0.00",
    "fee" : "0.06",
    "netAmount" : "0.94",
    "totalRefundedAmount" : "0.00",
    "metadata1" : "",
    "metadata2" : "",
    "items" : []
}
```

### Refund Sent
```javascript
{
    "transactionType" : "refund",
    "status" : "completed",
    "date" : "2020-01-01 12:00:00.0",
    "referenceNumber" : "000000-00000000abcd",
    "dailyTransactionID" : "0001",
    "name" : "Valeria Herrero",
    "phoneNumber" : "7871234567",
    "email" : "email@example.com",
    "message" : "This is a message.",
    "total" : "1.00",
    "tax" : "0.00",
    "subtotal" : "0.00",
    "fee" : "0.00",
    "netAmount" : "0.00",
    "totalRefundedAmount" : "0.00",
    "metadata1" : "",
    "metadata2" : "",
    "items" : []
}
```

## Legal
The use of this API and any related documentation is governed by and must be used in accordance with the Terms and Conditions of Use of ATH Móvi Business ®, which may be found at: https://athmovilbusiness.com/terminos.
