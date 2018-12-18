# Add user event

## Required fields

Field | Type | Description
----- | ---- | -----------
user_id | String | User identification string used to uniquely identify users on your platform. If difficult to associate `user_id` with transactions and easier to associate `txn_instrument_id` with transactions instead, this field can be set to the empty string - in such cases `txn_instrument_id` needs to be set to a value that allows transactions to be associated with users.
registration_datetime | Numeric | The date and time that the user registered on your platform in [Epoch time format](https://en.wikipedia.org/wiki/Unix_time) (number of seconds elapsed 1 Jan 1970 00:00:00 UTC).
date_of_birth | String | User's date of birth in `DD-MM-YYYY` format.
first_name | String | The first name associated with the user.
middle_name | String | The middle name associated with the user.
last_name | String | The last name associated with the user.
primary_address | String | The main street address associated with the transaction instrument on the user's account, if applicable. **Note**: If there are multiple addresses (billing, shipping, mailing etc.) associated with the account, provide the one most representative or relevant one for risk and compliance review. In most cases, this is the billing address. If there are multiple billing addresses associated with the account, provide just one.
primary_city | String | The corresponding city for the `primary_address` field.
primary_state | String | The corresponding state for the `primary_address` field. Can provide [abbreviated form](https://en.wikipedia.org/wiki/List_of_U.S._state_abbreviations) for states in the USA, otherwise must be provided in full form.
primary_country | String | The corresponding country for the `primary_address` field. Can provide 2 character [ISO 3166-1 alpha-2 abbreviated form](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements) or in full form.
primary_zipcode | String | The corresponding zipcode for the `primary_address` field. Can provide either 5-digit ZIP Code (`99999`) or ZIP+4 Code (`99999-9999`) formats for US addresses.

## Reserved fields

Field | Type | Description
----- | ---- | -----------
description | String | Human-readable text that describes the user/account, used to provide analysts context when reviewing accounts.
username | String | Username, typically set by the end-user on your platform. **Note:** If this is the same as `user_id` and/or `user_email`, assign the same value to these fields.
gender | String | The gender associated with the user - `M` for male, `F` for female, `U` for unknown or unspecified.
user_email | String | The email address associated with the user. **Note:** If this is the same as `user_id` and/or `username`, assign the same value to these fields.
ip_address | String / List | Single or multiple IPv4 or IPv6 format IP addresses associated with the user.
payment_methods | String / List | Single or multiple payment methods associated with the user account e.g. `paypal`, `creditcard-1234`, `ach-9942` etc.
social_sign_on_types | String / List | Single or multiple social sign-on methods associated with the user account e.g. `facebook`, `google`, `openid` etc.
txn_instrument_id | String / List | Single or multiple IDs of the instrument associated with events/transactions involving this user e.g. `credit_card_id`, `savings_account_id`, `store_id` etc. (**Note**: This field associates events/transactions to user accounts. Transaction/event data should include either `user_id` or `txn_instrument_id` to enable the system to link users to transactions.)
device_id | String / List | Single or multiple device identifiers associated with the user. This can be a custom-generated fingerprint, a unique identifier provided by the mobile operating system (iOS UUID) or by a third-party vendor such as Iovation or ThreatMetrix.
user-agent | String / List | Single or multiple user-agents associated with the user.
phone_num | String | The phone number associated with the user in [E.164 format](https://en.wikipedia.org/wiki/E.164) including country calling code e.g. `+14160326712` (this [Twilio formatting guide](https://support.twilio.com/hc/en-us/articles/223183008-Formatting-International-Phone-Numbers) is helpful).
secondary_address | String | The street address of the second address associated with the account. If both billing and shipping addresses are provided, this field is usually used to represent the shipping address.
secondary_city | String | The corresponding city for the `secondary_address` field.
secondary_state | String | The corresponding state for the `secondary_address` field. Can provide [abbreviated form](https://en.wikipedia.org/wiki/List_of_U.S._state_abbreviations) for states in the USA, otherwise must be provided in full form.
secondary_country | String | The corresponding country for the `secondary_address` field. Can provide 2 character [ISO 3166-1 alpha-2 abbreviated form](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements) or in full form.
referral_user_id | String | A `user_id` field that identifies another user that referred this user to the platform. For best results, the referrer should be 
id_verified | Boolean | `True`/`False` field indicating if the user's ID has been verified by your platform or through a third-party service.
address_verified | Boolean | `True`/`False` field indicating if the user's address has been verified by your platform or through a third-party service.
phone_verified | Boolean | `True`/`False` field indicating if the user's phone number has been verified by your platform or through a third-party service.
email_verified | Boolean | `True`/`False` field indicating if the user's email has been verified by your platform or through a third-party service.

## Custom fields

Examples of custom fields that may be helpful:

* Depository/Banking
  * `account_balance`
  * `credit_score`

* Lending
  * `funding_sources`
  * `registered_loan_payees`

* Marketplaces/Rentals
  * `num_items_sold`
  * `stars`
  * `feedback_pos`
  * `feedback_neg`
  * `feedback_neutral`
  * `is_seller`
  * `store_id`
  * `primary_ship_from_addr`
  * `listing_url`
  * `square_feet`
  * `security_deposit`
  * `cleaning_fee`

* Crypto Exchanges/Payments
  * `wallet_addresses`
  * `portfolio_value`
  * `funding_sources`
