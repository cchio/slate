# Data types

Unit21's systems accepts three different types of events:

1. **Add user event** - provides details on new users that you onboard.
  * Should be sent whenever you onboard new users to your platform, or provided in bulk when you first integrate with Unit21.
  * This event type is only used for new additions of users to the system. Modifications or deletions made to existing users should be expressed in a User action event.
2. **Action event** - provides details on non-transaction events triggered by an established user on your system, or updates made to a user's profile or status.
  * User logins, app access events, payment method updates, account deletion, user communications/disputes with your customer interaction teams etc. all fall into this category.
3. **Transaction event** - provides details on any finalized transfers of monetary value involving users in the system.
  * This event type is only used for transaction-related events. If a single transaction involves multiple events (i.e. charge reversals, authorization, status changes), each of these events should be dispatched to Unit21 as discrete events.

We designed Unit21's integrations for minimal disruption to our customer's business and engineering workflows. Because we service a wide range of businesses each interacting with and recording different kinds of data, we adopt a semi-flexible schema that can adapt to all relevant use-cases.

Each event is made up of a list of fields. Some fields are required, some are reserved, and the rest are custom:

1. **Required fields** - critical information that needs to be provided to Unit21, without which events will be rejected.
2. **Reserved fields** - standard fields that Unit21 accepts but does not require. We perform advanced processing on these fields to provide your organization with an enhanced experience. Modeling your data with reserved fields will ensure that you get the most out of Unit21. Some reserved fields specified in the data specification may be specific to industries/use-cases that may be irrelevant for your business - you can safely ignore these.
3. **Custom fields** - any additional data you capture within your system that may be helpful to risk/compliance decisioning. Any such fields that do not exist as reserved fields should be sent as a custom field. **Note**: You are free to name custom fields freely, with the exception of names already used by required or reserved fields.

All of required and reserved fields in the system have a `type` associated with them:

* `String` for any text (unicode) data.
* `Numeric` for any whole numbers, or numbers with decimal places. Also used to represent timestamps in the system.
* `Boolean` for any `True`/`False` type data.
* `List` for any multiple-valued fields. **Note**: When `String / List` is specified as the field type, list values will be parsed as `Strings`. When it is `Numeric / List`, list values will be parsed as `Numerics`.
