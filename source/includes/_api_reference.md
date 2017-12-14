# API Reference

## Overview & Basics

#### Introduction

The Amazon Pay API section helps you to process payments for purchases made by buyers on your website using the Amazon Pay service. This API section enables you to programmatically retrieve shipping and payment information provided by the buyer from their Amazon account. It allows you to authorize, capture, and refund payments, enabling a variety of payments scenarios.

**Note:** The Amazon Pay API section is only applicable to payments made through the Amazon Pay service offered by Amazon Pay. You cannot use this API section to process payments for Amazon Marketplace, Amazon Webstore, or Checkout by Amazon.

Using the Amazon Pay API section of Amazon Marketplace Web Service (Amazon MWS), you can:

<ul>
	<li>Create and manage a billing agreement to secure the buyer's permission to charge their selected payment method on a recurring basis without requiring their permission each time. You typically do not need a billing agreement if your buyers will visit your site each time they place an order or if you do not need to enable automatic payments. With a billing agreement, you can:</li>

	<ul>
    	<li>Obtain the shipping information from the buyer so that you can calculate shipping charges and tax for automatic payments.</li>
    	<li>Obtain information about the amount that you are allowed to charge a buyer each month using Amazon Pay.</li>
    	<li>Set the description and other optional information about the automatic payment.</li>
    	<li>Confirm the billing agreement after the buyer has signed up for automatic payments on your site.</li>
    	<li>Close the billing agreement if you or the buyer want to terminate the automatic payment relationship.</li>
	</ul>
	<li>Create and manage a limited representation of an order, hereafter referred to as an order reference or Order Reference object, through the Amazon Pay service. With an order reference, you can:</li>

	<ul>
    	<li>Obtain shipping information from the buyer so you can calculate shipping charges and tax.</li>
    	<li>Set the amount, description, and other optional information for the order.</li>
    	<li>Confirm the order after the buyer has finished placing an order on your website.</li>
   	 	<li>Cancel the order at the request of either the buyer or yourself.</li>
    	<li>Close the order after it has been processed and completed.</li>
    </ul>

	<li>Programmatically authorize, capture, and refund money for purchases made by the buyer at your website.</li>
</ul>

#### Terminology

<table cellspacing="0" cellpadding="0">
	<tr>
		<td><strong>Term</strong></td>
		<td><strong>Description</strong></td>
	</tr>
	<tr>
		<td>Billing Agreement</td>
		<td>A Billing Agreement object tracks the buyer's preferred payment method, preferred shipping address, and authorization for automatic payments. A billing agreement can have an indefinite lifetime and support an indefinite number of purchases.</td>
	</tr>
	<tr>
		<td>Order Reference</td>
		<td>An Order Reference object is a record of each purchase made by the buyer. It tracks the payment method, shipping address, and the amount that the buyer agreed to pay for that purchase. For each automatic payment, an order reference is created from the shipping and payment information stored in the billing agreement. An order reference is valid for 180 days and applies to only one purchase. You may have up to 10 authorizations on an order reference.</td>
	</tr>
	<tr>
		<td>Authorization</td>
		<td>An Authorization object tracks the availability of funds and secures them for future payment against the payment instruments stored in the order reference.</td>
	</tr>
	<tr>
		<td>Capture</td>
		<td>A Capture object tracks the movement of funds previously secured by authorization from the buyer's payment instruments to the merchant's account.</td>
	</tr>
	<tr>
		<td>Refund</td>
		<td>A Refund object tracks the movement of previously captured funds from the merchant's account to the buyer's payment instruments.</td>
	</tr>
	<tr>
		<td>Transaction</td>
		<td>A transaction is a generic term that is used for all of the types of payment events against an order reference. This includes authorizations, captures, refunds, A-to-z Claims, chargebacks, fees, and other miscellaneous transactions.</td>
	</tr>
</table>

## Endpoints

All API calls to the Amazon Pay API section service should be submitted to the following endpoints:

<ul>
    <li>Germany (DE) and United Kingdom (UK):</li>
    <ul>
        <li>Production: https://mws-eu.amazonservices.com/OffAmazonPayments/2013-01-01/</li>
        <li>Sandbox: https://mws-eu.amazonservices.com/OffAmazonPayments_Sandbox/2013-01-01/</li>
    </ul>
    <li>United States (US):</li>
    <ul>
        <li>Production: https://mws.amazonservices.com/OffAmazonPayments/2013-01-01/</li>
        <li>Sandbox: https://mws.amazonservices.com/OffAmazonPayments_Sandbox/2013-01-01/</li>
    </ul>
</ul>

## Authorization


## Payment APIs

### Authorize

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

The 'Authorize' operation reserves a specified amount against the payment methods stored in the order reference. To charge the payment methods, you must either set the CaptureNow request parameter to true or call the 'Capture' operation after you call this operation. An authorization is only valid for a particular time period, which is specified in the response of the operation. At the end of the time period, the authorization expires and a notification is sent to you if you have set up Instant Payment Notifications.

This operation has a maximum request quota of 10 and a restore rate of one request every second in the production environment. It has a maximum request quota of two and a restore rate of one request every two seconds in the sandbox environment. For definitions of throttling terminology and for a complete explanation of throttling, see <a href="http://docs.developer.amazonservices.com/en_US/dev_guide/DG_Throttling.html" target="_blank">Throttling: Limits to how often you can submit requests</a> in the Amazon MWS Developer Guide.

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### CancelOrderReference

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### Capture

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### CloseAuthorization

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### CloseOrderReference

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### ConfirmOrderReference

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### GetAuthrorizationDetails

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### GetCaptureDetails

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### GetOrderReferenceDetails

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### GetRefundDetails

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### GetServiceStatus

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### Refund

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### SetOrderReferenceDetails

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

## Subscription APIs

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### AuthorizeOnBillingAgreement

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### CloseBillingAgreement

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### ConfirmBillingAgreement

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### CreaterOrderReferenceForId

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### GetBillingAgreementDetails

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

### ValidateBillingAgreement

Reserves a specified amount against the payment methods stored in the order reference.

#### Description

#### Request Parameters

Parameter | Default | Description
--------- | ------- | -----------
xxx | xxx | xxx


```ruby

```

```python

```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript

```

> Response:

```xml

```

## API Libraries

These tools, built for your programming language, can streamline your integration.

* PHP
* Java
* Ruby
* Python
* C#
