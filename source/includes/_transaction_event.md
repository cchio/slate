# Transaction event

## Transaction event types

_Transaction_ events cover a variety of different types of monetary/value transfers.

Transaction Type | Description
--------------- | -----------
\_P2P_TRANSFER | Transfer of value between users on your platform.
\_PURCHASE | Goods purchases, rentals, card network payments made by the target user.
\_REFUND | Reversal of any transaction into the target user's account.
\_CORRECTION | Alteration or modification of a previous transaction.
\_DEBIT | Monetary transfer into the target user's account.
\_LOAN_GIVEN | Loan given by the target user to the platform or a specific user.
\_LOAN_RECEIVED | Loans received by the target user.
\_LOAN_PAYMENT | Loan repayment given or received by the target user.

## Required fields

Field | Type | Description
----- | ---- | -----------
txn_type | String | _Transaction_ event type - must be one of the values provided in the _Transaction Event Types_ table above e.g. `_P2P_TRANSFER`.
user_id | String | User identification string used to uniquely identify users on your platform. If all users involved in the transaction are registered on your system, this field should indicate the user most likely to be the perpetrator of malice e.g. in a two-sided marketplace transaction, use the seller; in a card payment transaction, use the card holder; in a loan transaction, use the loan repayer. If none of the users involved in the transaction are registered on your system, this should be a string that can uniquely identify the initiator of the transaction event e.g. email address.
txn_id | String | Transaction identification string used to uniquely identify the transaction within your own internal systems.
txn_datetime | Numeric |  The date and time that the user registered on your platform in [Epoch time format](https://en.wikipedia.org/wiki/Unix_time) (number of seconds elapsed 1 Jan 1970 00:00:00 UTC).
txn_amount | Numeric | The dollar value of the transaction. Specified in the currency set in the `currency_code` field, if not set, the default currency for your organization is used.
transaction_status | String | Status of the transaction - can take on values `COMPLETED`, `UNPAID`, `INCOMPLETE`, `CANCELLED`.

## Reserved fields

Field | Type | Description
----- | ---- | -----------
ip_address | String | IPv4 or IPv6 format IP addresses associated with the action event.
user_agent | String | User-agent associated with the action event.
session_id | String | User's session identifier associated with the action triggered by the user.
message_sender | String | ID of the user or team member that sent the message, dispute, comment, or any user-entered prose associated with the action event. If the message is sent by a user, then the same value as the required field `user_id` should be used. If sender does not have an ID, email address or some other identifying name should be used.
user_email | String | The email address associated with the user. **Note:** If this is the same as `user_id`, assign the same value to both fields.
txn_instrument | String | The instrument used to make the transaction e.g. `credit_card_id`, `savings_account_id`, `store_id` etc. **Note**: This field associates events/transactions to user accounts.
post_datetime | Numeric | The date and time that the transaction was posted (but not the "final" datetime, which is specified in the `txn_datetime` field) in [Epoch time format](https://en.wikipedia.org/wiki/Unix_time) (number of seconds elapsed 1 Jan 1970 00:00:00 UTC).
currency_code | String | Currency code in [IBAN numeric or 3-letter format](https://www.iban.com/currency-codes) e.g. `USD` or `840`, or if referring to a cryptocurrency/token, this should be the most common short code for it e.g. `BTC`, `ETH`, `LTC`.
network_code | String | Transaction system network code indicating the transaction category. This code is typically provided by payment processors such as Galileo, Stripe, or Marqeta.
authorization_code | String | Typically a 5-6 character code sent by the issuing bank indicated at the end of either a Successful Sales Transaction Response or a Declined Sales Transaction Response in the course of a typical merchant credit card transaction.
merchant_id | String | A unique identifier string used to identify the merchant transacting with the user. This identifier may originate from the payment processor, the card network, or may be assigned by your own systems.
merchant_category_code | String | A 4-digit numerical code ([MCC](https://en.wikipedia.org/wiki/Merchant_category_code)) detailed in [ISO 18245](https://en.wikipedia.org/wiki/ISO_18245) indicating the merchant's business type/category. Should correspond to the merchant referred to by `merchant_id`.
merchant_country_code | String | The corresponding country for the merchant referred to by the `merchant_id` field. Can provide 2 character [ISO 3166-1 alpha-2 abbreviated form](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements) or in full form.
recipient_id | String | Unique identification string used to identify the recipient of the transaction. If the recipient is not registered in the system, this should be a string that can uniquely identify recipient e.g. email address.
recipient_country_code | String | The corresponding country for the recipient referred to by the `recipient_id` field. Can provide 2 character [ISO 3166-1 alpha-2 abbreviated form](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements) or in full form.
preadjusted_txn_amount | Numeric | The unadjusted/initial transaction amount. In credit card transactions, this is the authorized amount while `txn_amount` indicates the captured amount. Specified in the same currency as `txn_amount`.
internal_auxiliary_fee | Numeric | Additional fees associated with the transaction charged by your platform e.g. platform transaction fees, service fees. Specified in the same currency as `txn_amount`.
external_auxiliary_fee | Numeric | Additional fees associated with the transaction that is not charged by your platform or is intended to cover an external cost e.g. shipping costs, cleaning fees, cryptocurrency network transfer fees. Specified in the same currency as `txn_amount`.
interchange_fee | Numeric | Fee associated with currency or value store conversions. Specified in the same currency as `txn_amount`.
user_data_1 | String | User data associated with the transaction. In credit card transactions, this could be the [billing descriptor](https://en.wikipedia.org/wiki/Billing_descriptor), in other types of transactions, this could be a generic description field containing some details on the transaction. Used to provide analysts context when reviewing accounts.
user_data_2 | String | A continuation of `user_data_1`.

## Custom fields

Examples of custom fields that may be helpful:

* Depository/Banking
  * `payer_balance`
  * `sender_account_id`
  * `txn_failure_code`

* Lending
  * `starting_principal`
  * `principal_balance`
  * `total_repayment_period`
  * `remaining_repayment_period`

* Marketplaces/Rentals
  * `listed_on`
  * `listing_title`
  * `num_bidders`
  * `num_bids`
  * `paid_on`
  * `shipping_label_printed`

* Crypto Exchanges/Payments
  * `recipient_address`
  * `price_per_coin`
  * `funding_source`
