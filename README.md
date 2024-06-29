# networkeyuel.js

hustle free NetworkEyuel integration package for node

## Usage

install the package `npm i networkeyuel.js`

```javascript
const NetworkEyuel = require('networkeyuel.js')

const networkeyuel = new NetworkEyuel({
  appId: 'YOUR NetworkEyuel APP ID',
  appKey: 'YOUR NetworkEyuel APP KEY',
  shortCode: 'NetworkEyuel SHORT CODE',
  publicKey: 'YOUR NetworkEyuel PUBLIC KEY',
})
const { success, response } = await networkeyuel.makePayment({
  paymentMethod: 'web | app',
  nonce: 'a unique random string ( should be unique for each request )',
  notifyUrl: 'callback url for payment confirmation',
  totalAmount: 4.5, // amount to charge
  outTradeNo: 'unique identifier (order no)',
  receiveName: 'company name',
  returnApp: 'com.example.app', // your application package name
  returnUrl: 'https://yourwebsite.com', // redirect url after payment completion'
  subject: 'payment for',
  timeoutExpress: '120', // valid for 2 hours
})
```

## Handling callback notifications

- once user completes the payment, you'll receive an encrypted plaintext on the `notifyUrl` you provided.

- Make sure the endpoint accepts `plaintext` request body

- you need to decrypt the text to get the transaction details

```javascript
const {
  msisdn, // the phone number from which the payment was done
  outTradeNo, // unique identifier provided when creating the payment
  totalAmount,
  tradeDate,
  tradeNo,
  tradeStatus,
  transactionNo,
} = networkeyuel.getDecryptedCallbackNotification(encryptedTextFromTelebirr)
```
