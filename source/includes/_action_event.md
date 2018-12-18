# Action event

## Action event types

_Action_ events cover a variety of different types of events that may affect the risk and compliance decisioning process. These events may be initiated by users on your platform, but may also be initiated by external users such as unregistered users or your own team members.

Event Type | Description
---------- | -----------
\_USER_LOGIN | Event log of a registered user logging in to your platform.
\_USER_LOGOUT | Event log of a registered user logging out of your platform.
\_USER_ACCESS | Event log of a registered user accessing 
\_USER_PROFILE_UPDATE | Update event of a user's profile e.g. a user updating their shipping address.
\_USER_DELETION | Permanent user deletion from the platform.
\_USER_BLOCKED | User blocked on the platform.
\_USER_SUSPENDED | Temporary suspension of the user on the platform.
\_COMMUNICATION | Event log detailing a communication/messaging event involving users on your platform and/or your customer contact teams.
\_DISPUTE | Event log detailing disputes and complaints filed user on your platform.
\_USER_REFERRAL | Event log detailing any referral activity initiated by existing users on your platform.
\_PROMOTION_APPLIED | Event log detailing any application of promotions to a user on your platform.

## Required fields

Field | Type | Description
----- | ---- | -----------
event_type | String | _Action_ event type - must be one of the values provided in the _Action Event Types_ table above e.g. `_USER_PROFILE_UPDATE`.
user_id | String | User identification string used to uniquely identify users on your platform. If all users involved in the event are registered on your system, this field should indicate the user most likely to be the perpetrator of malice. If none of the users involved in the action are registered on your system, this should be a string that can uniquely identify the initiator of the action event e.g. email address.
event_datetime | Numeric | The date and time that the user registered on your platform in [Epoch time format](https://en.wikipedia.org/wiki/Unix_time) (number of seconds elapsed 1 Jan 1970 00:00:00 UTC).

## Reserved fields

Field | Type | Description
----- | ---- | -----------
description | String | Human-readable text that describes the user/account, used to provide analysts context when reviewing accounts.
ip_address | String | IPv4 or IPv6 format IP addresses associated with the action event.
user_agent | String | User-agent associated with the action event.
session_id | String | User's session identifier associated with the action triggered by the user.
message_sender | String | ID of the user or team member that sent the message, dispute, comment, or any user-entered prose associated with the action event. If the message is sent by a user, then the same value as the required field `user_id` should be used. If sender does not have an ID, email address or some other identifying name should be used.
message_recipient | String | Recipient of the message. If the message is received by a user, then the same value as the required field `user_id` should be used. If recipient does not have an ID, email address or some other identifying name should be used.
message_subject | String | Subject of the message.
message_body | String | Body text of the message.
message_attachment_urls | String / List | Single or multiple links to attachments associated with the message. Descriptions of each attachment should be included as postamble in the `message_body`.
field_deleted_name | String | Name of the field that is to be deleted.
field_mutated_name | String | Name of the field that is to be changed.
field_mutated_value | String | New value of the field that is to be changed. This is provided as a string but will be conditionally parsed into `Numeric` or `Boolean` type based on the original type of the field provided in _Add User_ events.

## Custom fields

Custom fields that may be helpful include those associated with these business-specific actions:

* Depository/Banking
  * Card requested
  * New account opened
  * Added new wire transfer recipient

* Lending
  * Applied for new loan
  * Loan application successful/failure
  * Added/removed linked bank account

* Marketplaces/Rentals
  * Added/removed payment method
  * Added new payee
  * Listed item in store
  * Listed property for rent

* Crypto Exchanges/Payments
  * Added/removed wallet address
  * Added/removed payment method
  * Loaded funds
