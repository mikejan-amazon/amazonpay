# Overview

##### Introduction

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

##### Terminology

<table cellspacing="0" cellpadding="0">
	<tr>
		<td><strong>Term</strong></td>
		<td><strong>Description</strong></td>
	</tr>
	<tr>
		<td>Authorization</td>
		<td>An Authorization object tracks the availability of funds and secures them for future payment against the payment instruments stored in the order reference.</td>
	</tr>
	<tr>
		<td>Billing Agreement</td>
		<td>A Billing Agreement object tracks the buyer's preferred payment method, preferred shipping address, and authorization for automatic payments. A billing agreement can have an indefinite lifetime and support an indefinite number of purchases.</td>
	</tr>
	<tr>
		<td>Capture</td>
		<td>A Capture object tracks the movement of funds previously secured by authorization from the buyer's payment instruments to the merchant's account.</td>
	</tr>
	<tr>
		<td>Order Reference</td>
		<td>An Order Reference object is a record of each purchase made by the buyer. It tracks the payment method, shipping address, and the amount that the buyer agreed to pay for that purchase. For each automatic payment, an order reference is created from the shipping and payment information stored in the billing agreement. An order reference is valid for 180 days and applies to only one purchase. You may have up to 10 authorizations on an order reference.</td>
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


# Payment APIs

## Authorize

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAJKYFSJU7PEXAMPLE
  &Action=CancelOrderReference
  &AmazonOrderReferenceId=P01-1234567-1234567
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2012-12-19T19%3A01%3A11Z
  &Version=2013-01-01
  &Signature=CLZOdtJGjAo81IxaLoE7af6HqK0EXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
 <CancelOrderReferenceResponse
  xmlns="https://mws.amazonservices.com/schema/OffAmazonPayments/2013-01-01">
    <ResponseMetadata>
      <RequestId>5f20169b-7ab2-11df-bcef-d35615e2b044</RequestId>
    </ResponseMetadata>
  </CancelOrderReferenceResponse>
```

Reserves a specified amount against the payment methods stored in the order reference.

##### Description

The 'Authorize' operation reserves a specified amount against the payment methods stored in the order reference. To charge the payment methods, you must either set the CaptureNow request parameter to true or call the 'Capture' operation after you call this operation. An authorization is only valid for a particular time period, which is specified in the response of the operation. At the end of the time period, the authorization expires and a notification is sent to you if you have set up Instant Payment Notifications.

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="40%" valign="top"><p><strong>Parameter name</strong></p></td>
    <td width="60%" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="40%" valign="top"><p><span class="ph">AmazonOrderReferenceId</span></p>
    <p>Required<br>
    xs:string<br></p></td>
    <td width="60%" valign="top"><p>The order reference identifier.</p><p>This value is retrieved from the Amazon <strong>Button</strong> widget after the buyer has successfully authenticated with Amazon.</p></td>
  </tr>
  <tr>
    <td width="40%" valign="top"><p><span class="ph">AuthorizationReferenceId</span></p>
    <p>Required<br>
    xs:string<br></p></td>
    <td width="60%" valign="top"><p>The identifier for this authorization transaction that you specify. This identifier must be unique for all your authorization transactions.</p>
<p>Amazon recommends that you use only the following characters:</p>
      <ul>
        <li>lowercase a-z</li>
        <li>uppercase A-Z</li>
        <li>numbers 0-9</li>
        <li>dash (-)</li>
        <li>underscore (_)</li>
      </ul>
    <p>Maximum: 32 characters</p></td>
  </tr>
  <tr>
    <td width="40%" valign="top"><p><span class="ph">AuthorizationAmount</span></p>
    <p>Required<br>
    <a href="/us/documentation/apireference/201752720" target="_blank">Price</a><br></p></td>
    <td width="60%" valign="top"><p>Represents the amount to be authorized.</p><p>Maximum value:</p>
      <ul>
        <li>US: $150,000</li>
        <li>UK: £150,000</li>
        <li>Germany: €150,000</li>
      </ul></td>
  </tr>
  <tr>
    <td width="40%" valign="top"><p><span class="ph">SellerAuthorizationNote</span></p>
    <p>Optional<br>
    xs:string<br></p></td>
    <td width="60%" valign="top"><p>A description for the transaction that is displayed in emails to the buyer. Appears only when CaptureNow is set to <em>true<em>.</em></em></p><em><em>
<p>Maximum: 255 characters</p></em></em></td>
  </tr>
  <tr>
    <td width="40%" valign="top"><p><span class="ph">TransactionTimeout</span></p>
    <p>Optional<br>
    xs:nonnegativeInteger<br></p></td>
    <td width="60%" valign="top"><p>The maximum number of minutes allocated for the Authorize operation call to be processed, after which the authorization is automatically declined and you cannot capture funds against the authorization.</p>
<p><strong>Note:</strong> In asynchronous mode, the Authorize operation always returns the <strong>State</strong> as <em>Pending</em>. The authorization remains in this state until it is processed by Amazon. The processing time varies and can be a minute or more. After processing is complete, Amazon notifies you of the final processing status. For more information, see <a href="/us/documentation/lpwa/201909440" target="_blank">Instant Payment Notification (IPN)</a> in the <em>Amazon Pay and Login with Amazon integration guide</em>.</p>
<p>Valid values: Zero or integer values in multiples of five (5, 10, 15, etc.). Set the value to zero for synchronous mode. Set the value to greater than zero for asynchronous mode.</p>
<p><span class="ph">TransactionTimeout</span> values in synchronous mode:</p>
      <ul>
        <li>Must be <em>0</em></li>
      </ul>
      <p><span class="ph">TransactionTimeout</span> values in asynchronous mode:</p>
      <ul>
        <li>Minimum: <em>5</em></li>
        <li>Maximum: <em>1440</em></li>
        <li>Default: <em>1440</em></li>
      </ul></td>
  </tr>
  <tr>
    <td width="40%" valign="top"><p><span class="ph">CaptureNow</span></p>
    <p>Optional<br>
    xs:boolean<br></p></td>
    <td width="60%" valign="top"><p>Indicates whether to directly capture a specified amount against an order reference (without needing to call <span class="ph">Capture</span> and without waiting until the order ships). If set to true, specify the <span class="ph">SellerAuthorizationNote</span>. The captured amount is disbursed to your account in the next disbursement cycle.</p>
<p><strong>Note:</strong> The Amazon Pay policy states that you charge your buyer when you fulfill the items in the order. You should not collect funds before fulfilling the order.</p>
<p>Allowed values:</p>
      <ul>
        <li><em>false</em>—To capture the funds specified in this authorization, you must call the <span class="ph">Capture</span> operation.</li>
        <li><em>true</em>—The specified amount is directly captured. You do not need to call the <span class="ph">Capture</span> operation.</li>
      </ul>
      <p>Default: <em>false</em></p></td>
  </tr>
  <tr>
    <td width="40%" valign="top"><p><span class="ph">SoftDescriptor</span></p>
    <p>Optional<br>
    xs:string<br></p></td>
    <td width="60%" valign="top"><p>The description to be shown on the buyer's payment instrument statement if <strong>CaptureNow</strong> is set to <em>true</em>. The soft descriptor sent to the payment processor is: “AMZ* &lt;soft descriptor specified here&gt;”.</p>
    <p>Default: “AMZ*&lt;SELLER_NAME&gt; amzn.com/pmts WA”</p>
    <p>Maximum: 16 characters</p></td>
  </tr>
</tbody></table>

## CancelOrderReference

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAJKYFSJU7PEXAMPLE
  &Action=CancelOrderReference
  &AmazonOrderReferenceId=P01-1234567-1234567
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2012-12-19T19%3A01%3A11Z
  &Version=2013-01-01
  &Signature=CLZOdtJGjAo81IxaLoE7af6HqK0EXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
 <CancelOrderReferenceResponse
  xmlns="https://mws.amazonservices.com/schema/OffAmazonPayments/2013-01-01">
    <ResponseMetadata>
      <RequestId>5f20169b-7ab2-11df-bcef-d35615e2b044</RequestId>
    </ResponseMetadata>
  </CancelOrderReferenceResponse>
```

Cancels a previously confirmed order reference.

##### Description

To cancel a previously confirmed order reference, call the CancelOrderReference operation. You can cancel an Order Reference object only if there are no Completed, Closed, or Pending captures against it. If you cancel an order reference, all authorizations associated with this order reference are also closed.

After you call this operation, the order reference is moved into the Canceled state.

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="35%" valign="top"><p><strong>Parameter name</strong></p></td>
    <td width="65%" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="35%" valign="top"><p><span class="ph">AmazonOrderReferenceId</span></p>
    <p>Required<br>
    xs:string<br></p></td>
    <td width="65%" valign="top"><p>The order reference identifier.</p>
<p>This value is retrieved from the Amazon <strong>Button</strong> widget after the buyer has successfully authenticated with Amazon.</p></td>
  </tr>
  <tr>
    <td width="35%" valign="top"><p><span class="ph">CancelationReason</span></p>
    <p>Optional<br>
    xs:string<br></p></td>
    <td width="65%" valign="top"><p>Describes the reason for the cancellation. This is for informational purposes only and is never shown to the customer. The value can be retrieved in future GetOrderReferenceDetails calls.</p><p>Maximum: 1024 characters</p></td>
  </tr>
</tbody></table>

## Capture

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAFBM3LG5JEEXAMPLE
  &Action=Capture
  &AmazonAuthorizationId=P01-1234567-1234567-0000001
  &CaptureAmount.Amount=94.50
  &CaptureAmount.CurrencyCode=USD
  &CaptureReferenceId=test_capture_1
  &SellerCaptureNote=Lorem%20ipsum
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2012-11-05T19%3A01%3A11Z
  &Version=2013-01-01
  &Signature=WlQ708aqyHXMkoUBk69Hjxj8qdh3aDcqpY71hVgEXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
 <CaptureResponse xmlns="https://mws.amazonservices.com/schema/OffAmazonPayments/2013-01-01">
    <CaptureResult>
      <CaptureDetails>
        <AmazonCaptureId>P01-1234567-1234567-0000002</AmazonCaptureId>
        <CaptureReferenceId>test_capture_1</CaptureReferenceId>
        <SellerCaptureNote>Lorem ipsum</SellerCaptureNote>
        <CaptureAmount>
          <CurrencyCode>USD</CurrencyCode>
          <Amount>94.50</Amount>
        </CaptureAmount>
        <CaptureStatus>
          <State>Completed</State>
          <LastUpdateTimestamp>2012-11-03T19:10:16Z</LastUpdateTimestamp>
        </CaptureStatus>
        <CreationTimestamp>2012-11-03T19:10:16Z</CreationTimestamp>
      </CaptureDetails>
    </CaptureResult>
    <ResponseMetadata>
      <RequestId>b4ab4bc3-c9ea-44f0-9a3d-67cccef565c6</RequestId>
    </ResponseMetadata>
  </CaptureResponse>
```

Captures funds from an authorized payment instrument.

##### Description

To capture funds from an authorized payment instrument, call the Capture operation. To successfully capture a payment, you must call this operation on an Authorization object before it expires, as specified by the ExpirationTimestamp returned in response of the Authorize operation call. You must specify a capture amount, and the amount cannot exceed the original amount that was authorized.

You can query the status of a capture request by calling the GetCaptureDetails operation.

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="167" valign="top"><p><strong>Parameter name</strong></p></td>
    <td width="98" valign="top"><p><strong>Required</strong></p></td>
    <td width="84" valign="top"><p><strong>Type</strong></p></td>
    <td width="289" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">AmazonAuthorizationId</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>The authorization identifier that was generated by Amazon in the earlier call to <span class="ph">Authorize</span> or <span class="ph">AuthorizeOnBillingAgreement</span>.</p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">CaptureReferenceId</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>The identifier for this capture transaction that you specify. This identifier must be unique for all your capture transactions.</p>
<p>Amazon recommends that you use only the following characters:</p>
      <ul>
        <li>lowercase a-z</li>
        <li>uppercase A-Z</li>
        <li>numbers 0-9</li>
        <li>dash (-)</li>
        <li>underscore (_)</li>
      </ul>
    <p>Maximum: 32 characters</p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">CaptureAmount</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p><a href="/us/documentation/apireference/201752720" target="_blank">Price</a></p></td>
    <td width="289" valign="top"><p>The amount to capture in this transaction.</p>
<p>This amount cannot exceed the original amount that was authorized less any previously captured amount on this authorization.</p>
    <p>Maximumvalue:</p>
      <ul>
        <li>US: $150,000</li>
        <li>UK: £150,000</li>
        <li>Germany: €150,000</li>
      </ul></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">SellerCaptureNote</span></p></td>
    <td width="98" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>A description for the capture transaction that is shown to the buyer in emails.</p>
<p>Maximum: 255 characters</p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">SoftDescriptor</span></p></td>
    <td width="98" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>The description to be shown on the buyer's payment instrument statement. The soft descriptor sent to the payment processor is: “AMZ* &lt;soft descriptor specified here&gt;”.</p>
    <p>Default: “AMZ*&lt;SELLER_NAME&gt; amzn.com/pmts WA”</p>
    <p>Maximum: 16 characters</p></td>
  </tr>
</tbody></table>

## CloseAuthorization

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAFBM3LG5JEEXAMPLE
  &Action=CloseAuthorization
  &AmazonAuthorizationId=P01-1234567-1234567-0000001
  &ClosureReason=Closing%20the%20auhorization%20transaction
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2012-12-17T19%3A01%3A11Z
  &Version=2013-01-01
  &Signature=WlQ708aqyHXMkoUBk69Hjxj8qdh3aDcqpY71hVgEXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
<CloseAuthorizationResponse xmlns="https://mws.amazonservices.com/schema/OffAmazonPayments/2013-01-01">
    <ResponseMetadata>
      <RequestId>a9aedsd6-a10y-11t8-9a3d-67gggwd565c6</RequestId>
    </ResponseMetadata>
  </CloseAuthorizationResponse>
```

Closes an authorization.

##### Description

Call the CloseAuthorization operation only if the authorization is not going to be captured. If the authorization is captured Amazon will automatically close the authorization.

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="167" valign="top"><p><strong>Parameter name</strong></p></td>
    <td width="98" valign="top"><p><strong>Required</strong></p></td>
    <td width="84" valign="top"><p><strong>Type</strong></p></td>
    <td width="289" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">AmazonAuthorizationId</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>The authorization identifier that was generated by Amazon in the earlier call to Authorize.</p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">ClosureReason</span></p></td>
    <td width="98" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>A description for the closure that is shown in emails to the customer. </p>
<p>Maximum: 255 characters</p></td>
  </tr>
</tbody></table>


## CloseOrderReference

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAJKYFSJU7PEXAMPLE
  &Action=CloseOrderReference
  &AmazonOrderReferenceId=P01-1234567-1234567
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2012-12-19T19%3A01%3A11Z
  &Version=2013-01-01
  &Signature=CLZOdtJGjAo81IxaLoE7af6HqK0EXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
 <CloseOrderReferenceResponse
  xmlns="http://mws.amazonservices.com/schema/OffAmazonPayments/2013-01-01">
    <ResponseMetadata>
      <RequestId>5f20169b-7ab2-11df-bcef-d35615e2b044</RequestId>
    </ResponseMetadata>
  </CloseOrderReferenceResponse>
```

Confirms that an order reference has been fulfilled (fully or partially) and that you do not expect to create any new authorizations on this order reference.

##### Description

To indicate that a previously confirmed order reference has been fulfilled (fully or partially) and that you do not expect to create any new authorizations on this order reference, call the CloseOrderReference operation. You can still capture funds against open authorizations on the order reference.

After you call this operation, the order reference is moved into the Closed state.

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="167" valign="top"><p><strong>Parameter name</strong></p></td>
    <td width="98" valign="top"><p><strong>Required</strong></p></td>
    <td width="84" valign="top"><p><strong>Type</strong></p></td>
    <td width="289" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">AmazonOrderReferenceId</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>The ID of the order reference for which the details are being requested.</p>
<p>This value is retrieved from the Amazon <strong>Button</strong> widget after the buyer has successfully authenticated with Amazon.</p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">ClosureReason</span></p></td>
    <td width="98" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>Describes the reason for closing the order reference. This is for informational purposes only and is never shown to the customer. The value can be retrieved in future GetOrderReferenceDetails calls.</p><p>Maximum: 1024 characters</p></td>
  </tr>
</tbody></table>

## ConfirmOrderReference

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAJKYFSJU7PEXAMPLE
  &Action=ConfirmOrderReference
  &AmazonOrderReferenceId=P01-1234567-1234567
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2012-10-03T19%3A01%3A11Z
  &Version=2013-01-01
  &Signature=CLZOdtJGjAo81IxaLoE7af6HqK0EXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
 <ConfirmOrderReferenceResponse
  xmlns="https://mws.amazonservices.com/schema/OffAmazonPayments/2013-01-01">
    <ResponseMetadata>
      <RequestId>f42df4b1-8047-11df-8d5c-bf56a38ef3b4</RequestId>
    </ResponseMetadata>
  </ConfirmOrderReferenceResponse>
```

Confirms that the order reference is free of constraints and that all required information has been set on the order reference.

##### Description

After the order reference is free of constraints and all required information has been set on the order reference, call the ConfirmOrderReference operation. After you call this operation, the order reference is set to the Open state and you can submit authorizations against the order reference.

After you successfully call this operation, you should call the GetOrderReferenceDetails operation to get the remaining buyer information like name and shipping address. Before an order reference is confirmed, only the City, StateOrRegion, PostalCode, and CountryCode elements are returned in the call to GetOrderReferenceDetails.

Note: You can submit authorization requests only when an order reference is in the Open state.

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="208" valign="top"><p><strong>Parameter name</strong></p></td>
    <td width="93" valign="top"><p><strong>Required</strong></p></td>
    <td width="81" valign="top"><p><strong>Type</strong></p></td>
    <td width="256" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="208" valign="top"><p><span class="ph">AmazonOrderReferenceId</span></p></td>
    <td width="93" valign="top"><p>Yes</p></td>
    <td width="81" valign="top"><p>xs:string</p></td>
    <td width="256" valign="top"><p>The order reference identifier.</p><p>This value is retrieved from the Amazon <strong>Button</strong> widget after the buyer has successfully authenticated with Amazon.</p></td>
  </tr>
</tbody></table>


## GetAuthorizationDetails

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAFBM3LG5JEEXAMPLE
  &Action=GetAuthorizationDetails
  &AmazonAuthorizationId=P01-1234567-1234567-0000001
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2012-11-05T19%3A01%3A11Z
  &Version=2013-01-01
  &Signature=WlQ708aqyHXMkoUBk69Hjxj8qdh3aDcqpY71hVgEXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
 <GetAuthorizationDetailsResponse xmlns="https://mws.amazonservices.com/schema/OffAmazonPayments/2013-01-01">
    <GetAuthorizationDetailsResult>
      <AuthorizationDetails>
        <AmazonAuthorizationId>
          P01-1234567-1234567-0000001
        </AmazonAuthorizationId>
        <AuthorizationReferenceId>test_authorize_1</AuthorizationReferenceId>
        <SellerAuthorizationNote>Lorem ipsum</SellerAuthorizationNote>
        <AuthorizationAmount>
          <CurrencyCode>USD</CurrencyCode>
          <Amount>94.50</Amount>
        </AuthorizationAmount>
        <AuthorizationFee>
          <CurrencyCode>USD</CurrencyCode>
          <Amount>0</Amount>
        </AuthorizationFee>
        <AuthorizationStatus>
          <State>Open</State>
          <LastUpdateTimestamp>2012-12-10T19%3A01%3A11Z</LastUpdateTimestamp>
        </AuthorizationStatus>
        <CreationTimestamp>2012-12-10T19%3A01%3A11Z</CreationTimestamp>
        <ExpirationTimestamp>2013-01-10T19:10:16Z</ExpirationTimestamp>
      </AuthorizationDetails>
    </GetAuthorizationDetailsResult>
    <ResponseMetadata>
      <RequestId>b4ab4bc3-c9ea-44f0-9a3d-67cccef565c6</RequestId>
    </ResponseMetadata>
  </GetAuthorizationDetailsResponse>
```

Returns the status of a particular authorization and the total amount captured on the authorization.

##### Description

To query the status of a particular authorization and to retrieve information about the total amount captured on the authorization, call the GetAuthorizationDetails operation. If you received a Pending status when you called the Authorize operation, you can call this operation to get the current status.

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="199" valign="top"><p><strong>Parameter name</strong></p></td>
    <td width="95" valign="top"><p><strong>Required</strong></p></td>
    <td width="81" valign="top"><p><strong>Type</strong></p></td>
    <td width="263" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="199" valign="top"><p><span class="ph">AmazonAuthorizationId</span></p></td>
    <td width="95" valign="top"><p>Yes</p></td>
    <td width="81" valign="top"><p>xs:string</p></td>
    <td width="263" valign="top"><p>The authorization identifier that was generated by Amazon in the earlier call to Authorize.</p></td>
  </tr>
</tbody></table>


## GetCaptureDetails

Returns the status of a particular capture and the total amount refunded on the capture.

##### Description

Call the GetCaptureDetails operation to query the status of a particular capture and to retrieve information about the total amount refunded on the capture. If you received a Pending status when you called the Capture operation, you can call this operation to get the current status.

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="167" valign="top"><p><strong>Parameter Name</strong></p></td>
    <td width="98" valign="top"><p><strong>Required</strong></p></td>
    <td width="84" valign="top"><p><strong>Type</strong></p></td>
    <td width="289" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">AmazonCaptureId</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>The capture identifier that was generated by Amazon on the earlier call to Capture.</p></td>
  </tr>
</tbody></table>


## GetOrderReferenceDetails

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAJKYFSJU7PEXAMPLE
  &Action=GetOrderReferenceDetails
  &AddressConsentToken=YOUR_ACCESS_TOKEN
  &AmazonOrderReferenceId=P01-1234567-1234567
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2012-11-05T19%3A01%3A11Z
  &Version=2013-01-01
  &Signature=CLZOdtJGjAo81IxaLoE7af6HqK0EXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
 <GetOrderReferenceDetailsResponse
    xmlns="http://mws.amazonservices.com/
          schema/OffAmazonPayments/2013-01-01">
  <GetOrderReferenceDetailsResult>
    <OrderReferenceDetails>
      <AmazonOrderReferenceId>P01-1234567-1234567</AmazonOrderReferenceId>
      <CreationTimestamp>2012-11-05T20:21:19Z</CreationTimestamp>
      <ExpirationTimestamp>2013-05-07T23:21:19Z</ExpirationTimestamp>
      <OrderReferenceStatus>
        <State>Draft</State>
      </OrderReferenceStatus>
      <Destination>
        <DestinationType>Physical</DestinationType>
        <PhysicalDestination>
          <City>New York</City>
          <StateOrRegion>NY</StateOrRegion>
          <PostalCode>10101-9876</PostalCode>
          <CountryCode>US</CountryCode>
        </PhysicalDestination>
      </Destination>
      <ReleaseEnvironment>Live</ReleaseEnvironment>
    </OrderReferenceDetails>
  </GetOrderReferenceDetailsResult>
  <ResponseMetadata>
    <RequestId>5f20169b-7ab2-11df-bcef-d35615e2b044</RequestId>
  </ResponseMetadata>
  </GetOrderReferenceDetailsResponse>
```

Returns details about the Order Reference object and its current state.

##### Description

The GetOrderReferenceDetails operation returns details about the Order Reference object and its current state. An Order Reference object provides the following details about an order:

    Buyer
    Amount
    Description
    Destination (optional)
    Merchant order attributes (optional)
    List of constraints (optional)


##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="167" valign="top"><p><strong>Parameter Name</strong></p></td>
    <td width="98" valign="top"><p><strong>Required</strong></p></td>
    <td width="84" valign="top"><p><strong>Type</strong></p></td>
    <td width="289" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">AmazonOrderReferenceId</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>The order reference identifier.</p><p>This value is retrieved from the Amazon <strong>Button</strong> widget after the buyer has successfully authenticated with Amazon.</p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">AddressConsentToken</span></p></td>
    <td width="98" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>Login with Amazon Access Token.</p><p>This token is available after the buyer has successfully authenticated using Login with Amazon.</p><p>Required in order to retrieve the full shipping address before order confirmation. You must also set the additional scope parameter <span class="ph">payments:shipping_address</span>.</p></td>
  </tr>
</tbody></table>


## GetRefundDetails

> Sample Request:

Returns the status of a particular refund.

##### Description

Call the GetRefundDetails operation to query the status of a particular refund. If you received a Pending status when you called the Refund operation, you can call this operation to get the current status.

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="167" valign="top"><p><strong>Parameter Name</strong></p></td>
    <td width="98" valign="top"><p><strong>Required</strong></p></td>
    <td width="84" valign="top"><p><strong>Type</strong></p></td>
    <td width="289" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">AmazonRefundId</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>The Amazon-generated identifier for this refund transaction.</p></td>
  </tr>
</tbody></table>

## GetServiceStatus

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAEEXAMPLENGQCJLSA
  &Action=GetServiceStatus
  &SellerId=A135KKEKWF1J56
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2013-07-25T18%3A17%3A45Z
  &Version=2013-01-01
  &Signature=neUupEXAMPLEwJEJGnBfBGa2UpTSIZW3JMnVUYLsM4w%3D
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
 <?xml version="1.0"?>
  <GetServiceStatusResponse xmlns="http://mws.amazonservices.com/schema/OffAmazonPayments/2013-01-01">
    <GetServiceStatusResult>
      <Status>GREEN</Status>
      <Timestamp>2013-07-25T18:17:45.167Z</Timestamp>
    </GetServiceStatusResult>
    <ResponseMetadata>
      <RequestId>082c41fd-2f6b-4616-a518-7db14EXAMPLE</RequestId>
    </ResponseMetadata>
  </GetServiceStatusResponse>
```

Returns the operational status of the Amazon Pay API section.

##### Description

The GetServiceStatus operation returns the operational status of the Amazon Pay API section of Amazon Marketplace Web Service (Amazon MWS). Status values are GREEN, GREEN_I, YELLOW, and RED.

The GetServiceStatus operation has a maximum request quota of two and a restore rate of one request every five minutes. 

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="151" valign="top"><p><strong>Element name</strong></p></td>
    <td width="487" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="151" valign="top"><p><span class="ph">Status</span></p></td>
    <td width="487" valign="top"><p>Values returned by the <span class="ph">GetServiceStatus</span> operation:</p>
      <ul>
        <li>GREEN—The service is operating normally.</li>
        <li>GREEN_I—The service is operating normally. Additional information is provided.</li>
        <li>YELLOW—The service is experiencing higher than normal error rates or is operating with degraded performance. Additional information may be provided.</li>
        <li>RED—The service is unavailable or experiencing extremely high error rates. Additional information may be provided.</li>
      </ul>
    <p>Type: xs:string</p></td>
  </tr>
  <tr>
    <td width="151" valign="top"><p><span class="ph">Timestamp</span></p></td>
    <td width="487" valign="top"><p>Indicates the time at which the operational status was evaluated.</p><p>Type: xs:dateTime</p></td>
  </tr>
  <tr>
    <td width="151" valign="top"><p><span class="ph">MessageId</span></p></td>
    <td width="487" valign="top"><p>An Amazon-defined message identifier.</p><p>Type: xs:string</p></td>
  </tr>
  <tr>
    <td width="151" valign="top"><p><span class="ph">Messages</span></p></td>
    <td width="487" valign="top"><p>The parent element of one or more Message elements.</p></td>
  </tr>
  <tr>
    <td width="151" valign="top"><p><span class="ph">Message</span></p></td>
    <td width="487" valign="top"><p>The operational status message.</p><p>The parent element of the following child elements (both child elements are type: xs:string):</p>
      <ul>
        <li>Locale</li>
        <li>Text</li>
      </ul></td>
  </tr>
</tbody></table>



## Refund

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAFBM3LG5JEEXAMPLE
  &Action=Refund
  &AmazonCaptureId=P01-1234567-1234567-0000002
  &RefundAmount.Amount=94.50
  &RefundAmount.CurrencyCode=USD
  &RefundReferenceId=test_refund_1
  &SellerRefundNote=Lorem%20ipsum
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2012-11-05T19%3A01%3A11Z
  &Version=2013-01-01
  &Signature=WlQ708aqyHXMkoUBk69Hjxj8qdh3aDcqpY71hVgEXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
<RefundResponse xmlns="https://mws.amazonservices.com/schema/OffAmazonPayments/2013-01-01">
    <RefundResult>
      <RefundDetails>
        <AmazonRefundId>P01-1234567-1234567-0000003</AmazonRefundId>
        <RefundReferenceId>test_refund_1</RefundReferenceId>
        <SellerRefundNote>Lorem ipsum</SellerRefundNote>
        <RefundType>SellerInitiated</RefundType>
        <RefundedAmount>
          <CurrencyCode>USD</CurrencyCode>
          <Amount>94.50</Amount>
        </RefundedAmount>
        <FeeRefunded>
          <CurrencyCode>USD</CurrencyCode>
          <Amount>0</Amount>
        </FeeRefunded>
        <RefundStatus>
          <State>Pending</State>
          <LastUpdateTimestamp>2012-11-07T19:10:16Z</LastUpdateTimestamp>
        </RefundStatus>
        <CreationTimestamp>2012-11-05T19:10:16Z</CreationTimestamp>
      </RefundDetails>
    </RefundResult>
    <ResponseMetadata>
      <RequestId>b4ab4bc3-c9ea-44f0-9a3d-67cccef565c6</RequestId>
    </ResponseMetadata>
  </RefundResponse>
```

Refunds a previously captured amount.

##### Description

Call the Refund operation to refund a previously captured amount. A refund can only be requested on a capture if the refund amount does not exceed the following amounts:

    US: up to 15% or $75 (whichever is less) above the captured amount.
    UK: up to 15% or £75 (whichever is less) above the captured amount.
    DE: up to 15% or €75 (whichever is less) above the captured amount.

There is a maximum of 10 Refunds per Capture. You call the GetRefundDetails operation to query the status of a refund.

This operation has a maximum request quota of 10 and a restore rate of one request every second in the production environment. It has a maximum request quota of two and a restore rate of one request every two seconds in the sandbox environment. 

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="167" valign="top"><p><strong>Parameter Name</strong></p></td>
    <td width="98" valign="top"><p><strong>Required</strong></p></td>
    <td width="84" valign="top"><p><strong>Type</strong></p></td>
    <td width="289" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">AmazonCaptureId</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>The capture identifier that was generated by Amazon in the earlier call to <span class="ph">Capture</span>.</p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">RefundReferenceId</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>The identifier for this refund transaction that you specify. This identifier must be unique for all your refund transactions.</p><p>Amazon recommends that you use only the following characters:</p>
      <ul>
        <li>lowercase a-z</li>
        <li>uppercase A-Z</li>
        <li>numbers 0-9</li>
        <li>dash (-)</li>
        <li>underscore (_)</li>
      </ul>
    <p>Maximum: 32 characters</p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">RefundAmount</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p><a href="https://pay.amazon.com/us/documentation/apireference/201752720" target="_blank">Price</a></p></td>
    <td width="289" valign="top"><p>The amount to refund.</p>
    <p>This amount cannot exceed:</p>
      <ul>
        <li>US: the lesser of 15% or $75 above the captured amount less the amount already refunded on the capture.</li>
        <li>UK: the lesser of 15% or £75 above the captured amount for the Capture object.</li>
        <li>DE: the lesser of 15% or €75 above the captured amount for the Capture object.</li>
      </ul>
    <p>Maximum values:</p>
      <ul>
        <li>US: $150,000</li>
        <li>UK: £150,000</li>
        <li>DE: €150,000</li>
      </ul></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">SellerRefundNote</span></p></td>
    <td width="98" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>A description for the refund that is displayed in emails to the buyer.</p><p>Maximum: 255 characters</p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">SoftDescriptor</span></p></td>
    <td width="98" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>The description to be shown on the buyer's payment instrument statement. The soft descriptor sent to the payment processor is: “AMZ* &lt;soft descriptor specified here&gt;”.</p>
    <p>Default: “AMZ*&lt;SELLER_NAME&gt; amzn.com/pmts WA”</p>
    <p>Maximum: 16 characters</p></td>
  </tr>
</tbody></table>


## SetOrderReferenceDetails

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=0GS7553JW74RRM612K02EXAMPLE
  &Action=SetOrderReferenceDetails // must precede &AmazonOrderReferenceId
  &AmazonOrderReferenceId=P01-1234567-1234567
  &OrderReferenceAttributes.OrderTotal.Amount=106
  &OrderReferenceAttributes.OrderTotal.CurrencyCode=USD
  &OrderReferenceAttributes.PlatformId=PLATFORM_ID_HERE
  &OrderReferenceAttributes.SellerNote=Lorem%20ipsum
  &OrderReferenceAttributes.SellerOrderAttributes.SellerOrderId=5678-23
  &OrderReferenceAttributes.SellerOrderAttributes.StoreName=YOUR_STORE_NAME 
  &SellerId=YOUR_SELLER_ID
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2012-11-05T19%3A01%3A11Z
  &Version=2013-01-01
  &Signature=2RPzkOgQmDybUjk0dA54maCEXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
 <SetOrderReferenceDetailsResponse
    xmlns="https://mws.amazonservices.com/
          schema/OffAmazonPayments/2013-01-01">
  <SetOrderReferenceDetailsResult>
    <OrderReferenceDetails>
      <AmazonOrderReferenceId>P01-1234567-1234567</AmazonOrderReferenceId>
      <OrderTotal>
        <Amount>106</Amount>
        <CurrencyCode>USD</CurrencyCode>
      </OrderTotal>
      <SellerOrderAttributes>
        <SellerOrderId>5678-23</SellerOrderId>
      </SellerOrderAttributes>
      <SellerNote>Lorem ipsum</SellerNote>
      <CreationTimestamp>2012-11-05T20:21:19Z</CreationTimestamp>
      <ExpirationTimestamp>2013-05-07T23:21:19Z</ExpirationTimestamp>
      <OrderReferenceStatus>
        <State>Draft</State>
      </OrderReferenceStatus>
      <Destination>
        <DestinationType>Physical</DestinationType>
        <PhysicalDestination>
          <City>New York</City>
          <StateOrRegion>NY</StateOrRegion>
          <PostalCode>10101-9876</PostalCode>
          <CountryCode>US</CountryCode>
        </PhysicalDestination>
      </Destination>
      <ReleaseEnvironment>Live</ReleaseEnvironment>
    </OrderReferenceDetails>
  </SetOrderReferenceDetailsResult>
  <ResponseMetadata>
    <RequestId>f42df4b1-8047-11df-8d5c-bf56a38ef3b4</RequestId>
  </ResponseMetadata>
  </SetOrderReferenceDetailsResponse>
```

Sets order reference details such as the order total and a description for the order.

##### Description

Call the SetOrderReferenceDetails operation to specify order details such as the amount of the order, a description of the order, and other order attributes.

This operation has a maximum request quota of 10 and a restore rate of one request every second in the production environment. It has a maximum request quota of two and a restore rate of one request every two seconds in the sandbox environment. 

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="167" valign="top"><p><strong>Parameter Name</strong></p></td>
    <td width="98" valign="top"><p><strong>Required</strong></p></td>
    <td width="84" valign="top"><p><strong>Type</strong></p></td>
    <td width="289" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">AmazonOrderReferenceId</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="289" valign="top"><p>This value is retrieved from the Amazon <strong>Button</strong> widget after the buyer has successfully authenticated with Amazon.</p></td>
  </tr>
  <tr>
    <td width="167" valign="top"><p><span class="ph">OrderReferenceAttributes</span></p></td>
    <td width="98" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p><a href="https://pay.amazon.com/us/documentation/apireference/201752640" target="_blank">OrderReferenceAttributes</a></p></td>
    <td width="289" valign="top"><p>The merchant-specified attributes of the order reference.</p></td>
  </tr>
</tbody></table>


# Subscription APIs

## AuthorizeOnBillingAgreement

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAJKYFSJU7PEXAMPLE
  &Action=AuthorizeOnBillingAgreement
  &AmazonBillingAgreementId=C01-1234567-1234567
  &AuthorizationAmount.Amount=10
  &AuthorizationAmount.CurrencyCode=USD
  &AuthorizationReferenceId=test_authorize_1
  &InheritShippingAddress=true
  &MWSAuthToken=amzn.mws.4ea38b7b-f563-7709-4bae-87aeaEXAMPLE
  &SellerAuthorizationNote=For November Order
  &SellerId=YOUR_SELLER_ID_HERE
  &SellerOrderAttributes.CustomInformation=Example Information
  &SellerOrderAttributes.SellerOrderId=testSellerOrderId
  &SellerOrderAttributes.StoreName=testStore
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2012-10-03T19%3A01%3A11Z
  &TransactionTimeout=60
  &Version=2013-01-01
  &Signature=WlQ708aqyHXMkoUBk69Hjxj8qdh3aDcqpY71hVgEXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
<AuthorizeOnBillingAgreementResponse
    xmlns="https://mws.amazonservices.com/
          schema/OffAmazonPayments_Sandbox/2013-01-01">
  <AuthorizeOnBillingAgreementResult>
    <AuthorizationDetails>
      <AmazonAuthorizationId>C01-1234567-1234567-A006334</AmazonAuthorizationId>
      <AuthorizationReferenceId>AuthReference4</AuthorizationReferenceId>
      <SellerAuthorizationNote>ForNovemberOrder</SellerAuthorizationNote>
      <AuthorizationAmount>
        <Amount>20.00</Amount>
        <CurrencyCode>USD</CurrencyCode>
      </AuthorizationAmount>
      <CapturedAmount>
        <Amount>0</Amount>
        <CurrencyCode>USD</CurrencyCode>
      </CapturedAmount>
      <AuthorizationFee>
         <Amount>0.00</Amount>
        <CurrencyCode>USD</CurrencyCode>
      </AuthorizationFee>
		<SoftDecline>true</SoftDecline>
		<AuthorizationStatus>
        <LastUpdateTimestamp>2013-12-05T00:21:19Z</LastUpdateTimestamp>
        <State>Pending</State>
      </AuthorizationStatus>
      <CreationTimestamp>2013-12-01T00:21:19Z</CreationTimestamp>
      <ExpirationTimestamp>2014-01-01T00:21:19Z</ExpirationTimestamp>
      <CaptureNow>false</CaptureNow>
    </AuthorizationDetails>
  <AmazonOrderReferenceId>S01-1234569-1234568</AmazonOrderReferenceId>
  </AuthorizeOnBillingAgreementResult>
  <ResponseMetadata>
    <RequestId>2649e9a4-9a1e-4097-8ce5-bcbc307e5eb8</RequestId>
  </ResponseMetadata>
  </AuthorizeOnBillingAgreementResponse>
```

Reserves a specified amount against the payment methods stored in the billing agreement.

##### Description

The AuthorizeOnBillingAgreement operation reserves a specified amount against the payment methods stored in the billing agreement. To charge the payment methods, you must either set the CaptureNow request parameter to true or call the Capture operation after you call this operation. An authorization is only valid for a particular time period, which is specified in the response of the operation. At the end of the time period, the authorization expires and a notification is sent to you if you have set up Instant Payment Notifications (IPNs). For more information about Instant Payment Notifications, see Instant Payment Notification (IPN) in the Amazon Pay and Login with Amazon integration guide. You can also query the details about an authorization by calling the GetAuthorizationDetails operation.

Note: This is a convenience operation that creates and confirms an Order Reference object, requests an authorization, and then closes the order reference.

This operation has a maximum request quota of 10 and a restore rate of one request every second in the production environment. It has a maximum request quota of two and a restore rate of one request every two seconds in the sandbox environment.

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="177" valign="top"><p><strong>Parameter name</strong></p></td>
    <td width="112" valign="top"><p><strong>Required</strong></p></td>
    <td width="84" valign="top"><p><strong>Type</strong></p></td>
    <td width="265" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">AmazonBillingAgreementId</span></p></td>
    <td width="112" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="265" valign="top"><p>The billing agreement identifier.</p><p>This value is retrieved from the Amazon <strong>Button</strong>, <strong>AddressBook</strong>, or <strong>Wallet</strong> widgets.</p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">AuthorizationReferenceId</span></p></td>
    <td width="112" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="265" valign="top"><p>The identifier for this authorization transaction that you specify. This identifier must be unique for all your authorization transactions.</p>
<p>We recommend that you use only the following characters:</p>
      <ul>
        <li>lowercase a-z,</li>
        <li>uppercase A-Z,</li>
        <li>numbers 0-9,</li>
        <li>dash (-)</li>
        <li>underscore (_)</li>
      </ul>
      <p>Maximum: 32 characters</p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">AuthorizationAmount</span></p></td>
    <td width="112" valign="top"><p>Yes</p></td>
    <td width="84" valign="top"><p><a href="/us/documentation/apireference/201752720" target="_blank">Price</a></p></td>
    <td width="265" valign="top"><p>Represents the amount to be authorized.</p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">SellerAuthorizationNote</span></p></td>
    <td width="112" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="265" valign="top"><p>A description for the transaction that is shown in emails to the buyer.</p>
<p>Maximum: 255 characters</p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">TransactionTimeout</span></p></td>
    <td width="112" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:nonNegativeInteger</p></td>
    <td width="265" valign="top"><p>The number of minutes after which the authorization is automatically closed and you cannot capture funds against the authorization.</p>
    <p>Valid values: Zero or integral values in multiples of five (5, 10, 15, etc.)</p>
    <p>Minimum: 0</p>
    <p>Maximum: 1440</p>
    <p>Default: 1440</p>
    <p>A value of zero always returns a synchronous <strong>Open</strong> or <strong>Declined</strong> status. A non-zero value always returns a <strong>Pending</strong> status, and you will receive the final processing status by Instant Payment Notification (IPN).</p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">CaptureNow</span></p></td>
    <td width="112" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:boolean</p></td>
    <td width="265" valign="top"><p>Indicates whether to directly capture the amount specified by the <strong>AuthorizationAmount</strong> request parameter against an order reference (without needing to call <span class="ph">Capture</span> and without waiting until the order ships). The captured amount is disbursed to your account in the next disbursement cycle.</p>
    <p>Allowed values:</p>
      <ul>
        <li><em>true</em>—The specified amount is directly captured. You do not need to call the <span class="ph">Capture</span> operation.</li>
        <li><em>false</em>—You must call the <span class="ph">Capture</span> operation to capture the funds specified in this authorization.</li>
      </ul>
      <p>Default: <em>false</em></p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">SoftDescriptor</span></p></td>
    <td width="112" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="265" valign="top"><p>The description to be shown on the buyer's payment instrument statement if <strong>CaptureNow</strong> is set to true. The soft descriptor sent to the payment processor is: “AMZ* &lt;soft descriptor specified here&gt;”.</p><p>Default: “AMZ*&lt;SELLER_NAME&gt; amzn.com/pmts WA”</p>
    <p>Maximum: 16 characters</p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">SellerNote</span></p></td>
    <td width="112" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="265" valign="top"><p>Represents a description of the order that is shown in emails to the buyer.</p>
<p>Maximum: 1024 characters</p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">PlatformId</span></p></td>
    <td width="112" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:string</p></td>
    <td width="265" valign="top"><p>Represents the SellerId of the Solution Provider that developed the ecommerce platform.</p>
<p>This value is used only by solution providers, for whom it is required. It should not be provided by merchants creating their own custom integration. Do not specify the SellerId of the merchant for this request parameter.</p><p>If you are a merchant, do not enter a PlatformId.</p><p>Type: xs:string</p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">SellerOrderAttributes</span></p></td>
    <td width="112" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p><a href="/us/documentation/apireference/201752790" target="_blank">SellerOrderAttributes</a></p></td>
    <td width="265" valign="top"><p>Provides more context about an order that is represented by an OrderReference object.</p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">InheritShippingAddress</span></p></td>
    <td width="112" valign="top"><p>No</p></td>
    <td width="84" valign="top"><p>xs:boolean</p></td>
    <td width="265" valign="top"><p>Specifies whether to inherit the shipping address details from the object represented by the Id request parameter.</p>
<p>Default: <em>true</em></p></td>
  </tr>
</tbody></table>


## CloseBillingAgreement

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAJKYFSJU7PEXAMPLE
  &Action=CloseBillingAgreement
  &AmazonBillingAgreementId=C01-8824045-7416542
  &ClosureReason=Closing%20OR%20for%20Test
  &MWSAuthToken=amzn.mws.4ea38b7b-f563-7709-4bae-87aeaEXAMPLE
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2013-12-11T12%3A32%3A42.000Z
  &Version=2013-01-01
  &Signature=yrpMpoDfGLu567t611z27v4yJ8SURIVMKcy26sJEXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
 <CloseBillingAgreementResponse
    xmlns="https://mws.amazonservices.com/
          schema/OffAmazonPayments_Sandbox/2013-01-01">
  <ResponseMetadata>
    <RequestId>2649e9a4-9a1e-4097-8ce5-bcbc307e5eb8</RequestId>
  </ResponseMetadata>
  </CloseBillingAgreementResponse>
```

Confirms that you want to terminate the billing agreement with the buyer and that you do not expect to create any new order references or authorizations on this billing agreement.

##### Description

Call the CloseBillingAgreement operation on a previously confirmed billing agreement to indicate that you want to terminate the billing agreement with the buyer and that you do not expect to create any new order references or authorizations on this billing agreement. All open authorizations on the billing agreement can still be used to capture funds.

After successfully calling this operation, the billing agreement moves to the Closed state.

This operation has a maximum request quota of 10 and a restore rate of one request every second in the production environment. It has a maximum request quota of two and a restore rate of one request every two seconds in the sandbox environment. 

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="177" valign="top"><p><strong>Parameter Name</strong></p></td>
    <td width="100" valign="top"><p><strong>Required</strong></p></td>
    <td width="90" valign="top"><p><strong>Type</strong></p></td>
    <td width="271" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">AmazonBillingAgreementId</span></p></td>
    <td width="100" valign="top"><p>Yes</p></td>
    <td width="90" valign="top"><p>xs:string</p></td>
    <td width="271" valign="top"><p>The billing agreement identifier.</p><p>This value is retrieved from the Amazon <strong>Button</strong>, <strong>AddressBook</strong>, or <strong>Wallet</strong> widgets.</p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">ClosureReason</span></p></td>
    <td width="100" valign="top"><p>No</p></td>
    <td width="90" valign="top"><p>xs:string</p></td>
    <td width="271" valign="top"><p>Describes the reason for closing the billing agreement.</p><p>Maximum: 1024 characters</p></td>
  </tr>
</tbody></table>

## ConfirmBillingAgreement

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAJKYFSJU7PEXAMPLE
  &Action=ConfirmBillingAgreement
  &AmazonBillingAgreementId=C01-8824045-7416542
  &MWSAuthToken=amzn.mws.4ea38b7b-f563-7709-4bae-87aeaEXAMPLE
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2013-12-11T11%3A37%3A19.000Z
  &Version=2013-01-01
  &Signature=ET6V00R4fr2inSDky4olLrlS1XrQfdrV9Bj%2BiWeEXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
<ConfirmBillingAgreementResponse
    xmlns="https://mws.amazonservices.com/
          schema/OffAmazonPayments_Sandbox/2013-01-01">
  <ResponseMetadata>
    <RequestId>2649e9a4-9a1e-4097-8ce5-bcbc307e5eb8</RequestId>
  </ResponseMetadata>
  </ConfirmBillingAgreementResponse>
```

Confirms that the billing agreement is free of constraints and all required information has been set on the billing agreement.

##### Description

Call the ConfirmBillingAgreement operation when the billing agreement is free of constraints, indicating that all required information has been set on the billing agreement. On successful completion of the ConfirmBillingAgreement call, the billing agreement moves to the Open state.

You cannot modify the billing agreement after it is confirmed. However, the buyer can still update the shipping address and payment method associated with the billing agreement.

AuthorizeOnBillingAgreement requests are only accepted on a billing agreement when it is in Open state. You can create multiple order references by calling the CreateOrderReferenceForId operation when the billing agreement is in the Open state.

This operation has a maximum request quota of 10 and a restore rate of one request every second in the production environment. It has a maximum request quota of two and a restore rate of one request every two seconds in the sandbox environment.

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="226" valign="top"><p><strong>Parameter Name</strong></p></td>
    <td width="100" valign="top"><p><strong>Required</strong></p></td>
    <td width="96" valign="top"><p><strong>Type</strong></p></td>
    <td width="217" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="226" valign="top"><p><span class="ph">AmazonBillingAgreementId</span></p></td>
    <td width="100" valign="top"><p>Yes</p></td>
    <td width="96" valign="top"><p>xs:string</p></td>
    <td width="217" valign="top"><p>The billing agreement identifier.</p><p>This value is retrieved from the Amazon <strong>Button</strong>, <strong>AddressBook</strong>, or <strong>Wallet</strong> widgets.</p></td>
  </tr>
</tbody></table>

## CreaterOrderReferenceForId

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAJKYFSJU7PEXAMPLE
  &Action=CreateOrderReferenceForId
  &Id=C01-1234567-1234567
  &IdType=BillingAgreement
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2012-10-03T19%3A01%3A11Z
  &Version=2013-01-01
  &Signature=WlQ708aqyHXMkoUBk69Hjxj8qdh3aDcqpY71hVgEXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
<CreateOrderReferenceForIdResponse
    xmlns="http://mws.amazonservices.com/
          schema/OffAmazonPayments_Sandbox/2013-01-01">
  <CreateOrderReferenceForIdResult>
    <OrderReferenceDetails>
      <AmazonOrderReferenceId>S01-1234567-1234567</AmazonOrderReferenceId>
      <CreationTimestamp>2013-12-05T00:21:19Z</CreationTimestamp>
      <ExpirationTimestamp>2014-05-05T00:21:19Z</ExpirationTimestamp>
      <OrderReferenceStatus>
        <State>Draft</State>
      </OrderReferenceStatus>
      <Destination>
        <DestinationType>Physical</DestinationType>
        <PhysicalDestination>
          <City>New York</City>
          <StateOrRegion>NY</StateOrRegion>
          <PostalCode>10101-9876</PostalCode>
          <CountryCode>US</CountryCode>
        </PhysicalDestination>
      </Destination>
      <ReleaseEnvironment>Live</ReleaseEnvironment>
    </OrderReferenceDetails>
  </CreateOrderReferenceForIdResult>
  <ResponseMetadata>
    <RequestId>5f20169b-7ab2-11df-bcef-d35615e2b044</RequestId>
  </ResponseMetadata>
  </CreateOrderReferenceForIdResponse>
```

Creates an order reference for the given object.

##### Description

The CreateOrderReferenceForId operation is used to create an Order Reference object from the object represented by the Id and IdType request parameters.

For order references created from a Billing Agreement object, only one order reference can be created while the billing agreement is in the Draft state. Any number of order references can be created when the billing agreement is in the Open state. The buyer, shipping address, and payment method for the order reference are populated from the billing agreement. To create an Order Reference object in the Confirmed state, set the ConfirmNow request parameter to true.

This operation has a maximum request quota of 10 and a restore rate of one request every second in the production environment. It has a maximum request quota of two and a restore rate of one request every two seconds in the sandbox environment. 

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="35%" valign="top"><p><strong>Parameter Name</strong></p></td>
    <td width="65%" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="35%" valign="top">
      <p><span class="ph">Id</span></p>
      <p>Required<br>
      xs:string<br></p>
    </td>
    <td width="65%" valign="top"><p>The identifier of the object to be used to create an order reference.</p><p>Currently, the only accepted value is a billing agreement identifier. This value is retrieved from the Amazon <strong>Button</strong>, <strong>AddressBook</strong>,    or <strong>Wallet</strong> widgets.</p></td>
  </tr>
  <tr>
    <td width="35%" valign="top">
      <p><span class="ph">IdType</span></p>
      <p>Required<br>
      xs:string<br></p>
    </td>
    <td width="65%" valign="top"><p>The type of the object represented by the Id request parameter.</p><p>A value of <em>BillingAgreement</em> specifies that <strong>Id</strong> is a Billing Agreement identifier.</p></td>
  </tr>
  <tr>
    <td width="35%" valign="top">
      <p><span class="ph">InheritShippingAddress</span></p>
      <p>Optional<br>
      xs:boolean<br></p>
    </td>
    <td width="65%" valign="top"><p>Specifies whether to inherit the shipping address details from the object represented by the Id request parameter.</p><p>Default: <em>true</em></p></td>
  </tr>
  <tr>
    <td width="35%" valign="top">
      <p><span class="ph">ConfirmNow</span></p>
      <p>Optional<br>
      xs:boolean<br></p>
    </td>
    <td width="65%" valign="top"><p>Indicates whether to directly confirm the requested order reference.</p>
      <ul>
        <li><em>true</em>—The order reference is directly confirmed. You do not need to call the <span class="ph">ConfirmOrderReference</span> operation.</li>
        <li><em>false</em>—You must call the <span class="ph">ConfirmOrderReference</span> operation to confirm the order reference.</li>
      </ul>
      <p>Default: <em>false</em></p></td>
  </tr>
  <tr>
    <td width="35%" valign="top">
      <p><span class="ph">OrderReferenceAttributes</span></p>
      <p>Required only if <strong>ConfirmNow</strong> is <em>true</em><br>
      <a href="https://pay.amazon.com/us/documentation/apireference/201752640" target="_blank">OrderReferenceAttributes</a><br></p>
      </td>
    <td width="65%" valign="top"><p>The merchant-specified attributes of the order reference.</p></td>
  </tr>
</tbody></table>


## GetBillingAgreementDetails

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

AWSAccessKeyId=AKIAJKYFSJU7PEXAMPLE
  &Action=GetBillingAgreementDetails
  &AmazonBillingAgreementId=C01-8824045-7416542
  &MWSAuthToken=amzn.mws.4ea38b7b-f563-7709-4bae-87aeaEXAMPLE
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2013-12-11T10%3A38%3A44.000Z
  &Version=2013-01-01
  &Signature=gP11oEBaaiQdASWsLDyid18Wn%2BB%2FKZQQtKgpHCtEXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
<GetBillingAgreementDetailsResponse
    xmlns="https://mws.amazonservices.com/
          schema/OffAmazonPayments_Sandbox/2013-01-01">
  <GetBillingAgreementDetailsResult>
    <BillingAgreementDetails>
      <AmazonBillingAgreementId>C01-8824045-7416542</AmazonBillingAgreementId>
      <Constraints>
        <ConstraintID>BuyerConsentNotSet</ConstraintID>
        <Description>
          Buyer has not given consent for this Billing Agreement.
        </Description>
      </Constraints>
      <CreationTimestamp>2013-12-05T00:21:19Z</CreationTimestamp>
      <Destination>
        <DestinationType>Physical</DestinationType>
        <PhysicalDestination>
          <City>Seattle</City>
          <CountryCode>US</CountryCode>
          <PostalCode>98104</PostalCode>
          <StateOrRegion>WA</StateOrRegion>
        </PhysicalDestination>
      </Destination>
       <BillingAgreementLimits>
        <AmountLimitPerTimePeriod>
          <CurrencyCode>USD</CurrencyCode>
          <Amount>500</Amount>
        </AmountLimitPerTimePeriod>
        <TimePeriodStartDate>2013-12-01T00:00:00Z</TimePeriodStartDate>
        <TimePeriodEndDate>2014-01-01T00:00:00Z</TimePeriodEndDate>
        <CurrentRemainingBalance>
          <CurrencyCode>USD</CurrencyCode>
          <Amount>94.50</Amount>
        </CurrentRemainingBalance>
      </BillingAgreementLimits>
      <BillingAgreementStatus>
        <State>Draft</State>
      </BillingAgreementStatus>
      <ReleaseEnvironment>Sandbox</ReleaseEnvironment>
    </BillingAgreementDetails>
  </GetBillingAgreementDetailsResult>
  <ResponseMetadata>
    <RequestId>4a08624e-fffa-4fe7-bc19-ef9330c42f6a</RequestId>
  </ResponseMetadata>
  </GetBillingAgreementDetailsResponse>
```

Returns details about the Billing Agreement object and its current state.

##### Description

The GetBillingAgreementDetails operation returns details about the Billing Agreement object and its current state. A Billing Agreement object provides details about the following:

    Buyer
    Description
    Destination (optional)
    Merchant billing agreement details (optional)
    List of constraints (optional)

This operation has a maximum request quota of 20 and a restore rate of two requests every second in the production environment. It has a maximum request quota of five and a restore rate of one request every second in the sandbox environment.

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="177" valign="top"><p><strong>Parameter Name</strong></p></td>
    <td width="100" valign="top"><p><strong>Required</strong></p></td>
    <td width="102" valign="top"><p><strong>Type</strong></p></td>
    <td width="259" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">AmazonBillingAgreementId</span></p></td>
    <td width="100" valign="top"><p>Yes</p></td>
    <td width="102" valign="top"><p>xs:string</p></td>
    <td width="259" valign="top"><p>The billing agreement identifier.</p><p>This value is retrieved from the Amazon <strong>Button</strong>, <strong>AddressBook</strong>, or <strong>Wallet</strong> widgets.</p></td>
  </tr>
  <tr>
    <td width="177" valign="top"><p><span class="ph">AddressConsentToken</span></p></td>
    <td width="100" valign="top"><p>No</p></td>
    <td width="102" valign="top"><p>xs:string</p></td>
    <td width="259" valign="top"><p>The buyer address consent token. You must provide a valid <strong>AddressConsentToken</strong> if you want to get the full shipping address before the billing agreement is confirmed. Otherwise you will only receive the city, state, postal code, and country before you confirm the billing agreement.</p><p>This value is retrieved from the Amazon <strong>Button</strong> widget after the buyer has successfully authenticated with Amazon.</p></td>
  </tr>
</tbody></table>

## SetBillingAgreementDetails

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAJKYFSJU7PEXAMPLE
  &Action=SetBillingAgreementDetails
  &AmazonBillingAgreementId=C01-8824045-7416542
  &BillingAgreementAttributes.PlatformId=PLATFORM_ID_HERE
  &BillingAgreementAttributes.SellerNote=APPROVE%20LITE%20APPROVE%20HEAVY
  &BillingAgreementAttributes.SellerBillingAgreementAttributes
    .CustomInformation=Example%20Customer%20Info
  &BillingAgreementAttributes.SellerBillingAgreementAttributes
    .StoreName=Test%20Store%20Name
  &MWSAuthToken=amzn.mws.4ea38b7b-f563-7709-4bae-87aeaEXAMPLE
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2013-12-11T10%3A57%3A18.000Z
  &Version=2013-01-01
  &Signature=Z0ZVgWu0ICF4FLxt1mTjyK%2BjdYG6Kmm8JxLTfsQEXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
<SetBillingAgreementDetailsResponse
    xmlns="https://mws.amazonservices.com/
          schema/OffAmazonPayments_Sandbox/2013-01-01">
  <SetBillingAgreementDetailsResult>
    <BillingAgreementDetails>
      <AmazonBillingAgreementId>C01-8824045-7416542</AmazonBillingAgreementId>
      <CreationTimestamp>2013-12-05T00:21:19Z</CreationTimestamp>
      <Destination>
        <DestinationType>Physical</DestinationType>
        <PhysicalDestination>
          <City>Seattle</City>
          <CountryCode>US</CountryCode>
          <PostalCode>98104</PostalCode>
          <StateOrRegion>WA</StateOrRegion>
        </PhysicalDestination>
      </Destination>
      <BillingAgreementConsent>true</BillingAgreementConsent>
      <BillingAgreementStatus>
        <State>Draft</State>
      </BillingAgreementStatus>
      <BillingAgreementLimits>
        <AmountLimitPerTimePeriod>
          <CurrencyCode>USD</CurrencyCode>
          <Amount>500</Amount>
        </AmountLimitPerTimePeriod>
        <TimePeriodStartDate>2013-12-01T00:00:00Z</TimePeriodStartDate>
        <TimePeriodEndDate>2013-12-23T23:59:59Z</TimePeriodEndDate>
        <CurrentRemainingBalance>
          <CurrencyCode>USD</CurrencyCode>
          <Amount>94.50</Amount>
        </CurrentRemainingBalance>
      </BillingAgreementLimits>
      <ReleaseEnvironment>Sandbox</ReleaseEnvironment>
      <SellerNote>APPROVE  LITE APPROVE HEAVY</SellerNote>
      <SellerBillingAgreementAttributes>
        <CustomInformation>Example Customer Info</CustomInformation>
        <StoreName>Test Store Name</StoreName>
      </SellerBillingAgreementAttributes>
    </BillingAgreementDetails>
  </SetBillingAgreementDetailsResult>
  <ResponseMetadata>
    <RequestId>bab23c81-f7c9-4d1a-b76b-fbcec07e47f5</RequestId>
  </ResponseMetadata>
  </SetBillingAgreementDetailsResponse>
```

Sets billing agreement details such as a description of the agreement and other information about the merchant.

##### Description

Call the SetBillingAgreementDetails operation to specify billing agreement details such as a description of the agreement and other information about the merchant.

This operation has a maximum request quota of 10 and a restore rate of one request every second in the production environment. It has a maximum request quota of two and a restore rate of one request every two seconds in the sandbox environment. 

##### Request Parameters

<table cellspacing="0" cellpadding="5" border="1">
  <tbody><tr>
    <td width="243" valign="top"><p><strong>Parameter Name</strong></p></td>
    <td width="101" valign="top"><p><strong>Required</strong></p></td>
    <td width="95" valign="top"><p><strong>Type</strong></p></td>
    <td width="199" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="243" valign="top"><p><span class="ph">AmazonBillingAgreementId</span></p></td>
    <td width="101" valign="top"><p>Yes</p></td>
    <td width="95" valign="top"><p>xs:string</p></td>
    <td width="199" valign="top"><p>The billing agreement identifier.</p><p>This value is retrieved from the Amazon <strong>Button</strong>, <strong>AddressBook</strong>, or <strong>Wallet</strong> widgets.</p></td>
  </tr>
  <tr>
    <td width="243" valign="top"><p><span class="ph">BillingAgreementAttributes</span></p></td>
    <td width="101" valign="top"><p>Yes</p></td>
    <td width="95" valign="top"><p><a href="https://pay.amazon.com/us/documentation/apireference/201752480" target="_blank">BillingAgreementAttributes</a></p></td>
    <td width="199" valign="top"><p>The merchant-specified attributes of the billing agreement.</p></td>
  </tr>
</tbody></table>

## ValidateBillingAgreement

> Sample Request:

```shell
curl "/OffAmazonPayments/2013-01-01"
  -H "Content-Type: x-www-form-urlencoded"
  -H "Host: mws.amazonservices.com"

  AWSAccessKeyId=AKIAJKYFSJU7PEXAMPLE
  &Action=ValidateBillingAgreement
  &AmazonBillingAgreementId=C01-8824045-7416542
  &MWSAuthToken=amzn.mws.4ea38b7b-f563-7709-4bae-87aeaEXAMPLE
  &SellerId=YOUR_SELLER_ID_HERE
  &SignatureMethod=HmacSHA256
  &SignatureVersion=2
  &Timestamp=2013-12-11T10%3A38%3A44.000Z
  &Version=2013-01-01
  &Signature=gP11oEBaaiQdASWsLDyid18Wn%2BB%2FKZQQtKgpHCtEXAMPLE
```

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```csharp
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

> Sample Response:

```xml
 <ValidateBillingAgreementResponse
    xmlns="https://mws.amazonservices.com/
          schema/OffAmazonPayments_Sandbox/2013-01-01">
  <ValidateBillingAgreementResult>
    <ValidationResult>Failure</ValidationResult>
    <FailureReasonCode>InvalidPaymentMethod</FailureReasonCode>
    <BillingAgreementStatus>
      <LastUpdateTimestamp>2013-12-05T00:21:19Z</LastUpdateTimestamp>
      <State>Suspended</State>
      <ReasonCode>InvalidPaymentMethod</ReasonCode>
      <ReasonDescription>Payment method is not valid.</ReasonDescription>
    </BillingAgreementStatus>
  </ValidateBillingAgreementResult>
  <ResponseMetadata>
    <RequestId>f42df4b1-8047-11df-8d5c-bf56a38ef3b4</RequestId>
  </ResponseMetadata>
  </ValidateBillingAgreementResponse>
```

Validates the status of the BillingAgreement object and the payment method associated with it.

##### Description

Call the ValidateBillingAgreement operation when the billing agreement moves to the Open state (that is, after a successful call to the ConfirmBillingAgreement operation). This operation validates the status of the billing agreement and the validity of the payment method associated with the billing agreement.

This operation has a maximum request quota of 10 and a restore rate of one request every second in the production environment. It has a maximum request quota of two and a restore rate of one request every two seconds in the sandbox environment. 

##### Request Parameters

<table cellspacing="0" border="1">
  <tbody><tr>
    <td width="226" valign="top"><p><strong>Parameter Name</strong></p></td>
    <td width="93" valign="top"><p><strong>Required</strong></p></td>
    <td width="90" valign="top"><p><strong>Type</strong></p></td>
    <td width="229" valign="top"><p><strong>Description</strong></p></td>
  </tr>
  <tr>
    <td width="226" valign="top"><p><span class="ph">AmazonBillingAgreementId</span></p></td>
    <td width="93" valign="top"><p>Yes</p></td>
    <td width="90" valign="top"><p>xs:string</p></td>
    <td width="229" valign="top"><p>The billing agreement identifier.</p><p>This value is retrieved from the Amazon <strong>Button</strong>, <strong>AddressBook</strong>, or <strong>Wallet</strong> widgets.</p></td>
  </tr>
</tbody></table>

