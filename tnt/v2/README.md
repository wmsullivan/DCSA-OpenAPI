### Track & Trace (T&T)

The DCSA Interface Standard for Track & Trace is documented on the [**DCSA TNT SwaggerHub**](https://app.swaggerhub.com/apis/dcsaorg/DCSA_TNT).

The purpose of an Event Hub is to send events and manage subscriptions. Track & Trace is a specialised Hub managing: **TransportEvents, EquipmentEvents and ShipmentEvents**. It is only possible to receive **TransportEvents, EquipmentEvents and ShipmentEvents** and subscribe to **TransportEvents, EquipmentEvents and ShipmentEvents** when implementing Track & Trace.

Publication related to this specification:
-	[DCSA Information Model 2.0](https://dcsa.org/wp-content/uploads/2020/07/DCSA-Information-model-2.0-vF.pdf)
-	[DCSA Information Model Reading Guide]( https://dcsa.org/wp-content/uploads/2020/07/DCSA-Information-Model-2.0-Reading-Guide-vF.pdf)
-	[DCSA Interface for Track and Trace 1.2]( https://dcsa.org/wp-content/uploads/2020/05/DCSA-Interface-Standard-for-Track-and-Trace-1.2.pdf)
-	[DCSA Interface for Track and Trace 1.2 Reading Guide]( https://dcsa.org/wp-content/uploads/2020/05/DCSA-Interface-Standard-for-Track-and-Trace-Reading-Guide-1.2.pdf)
-	[Glossary of Terms](https://knowledge.dcsa.org/s/glossary)

### Releasenotes

* Added `PUT /event-subscriptions/{subscriptionID}/secret` endPoint to update the shared secret used to create the `Notification-Signature`
* Split subscription body in 2:
  * One used for `POST /event-subscriptions` calls which includes the secret
  * One without the secret used for `GET /event-subscriptions/{subscriptionID}` and `PUT /event-subscriptions/{subscriptionID}`
* Callbacks updated:
  * Deprecated the `Signature` header as the new `Notification-Signature` is to be used instead
  * Added `Subscription-ID` header to include the subscriptionID causing the Event to be sent
  * Added `Notification-Signature` header which is the new Signature used to validate the authenticity of the Event
  * Added `API-Version` header to include the version of API **sending the event**
* changed definition of array-queryParameters (ex: eventType). This is now a comma (,) separated list
* Added limit and cursor queryParameter to `GET /events` and `GET /event-subscriptions`
* Added `API-Version` header to **all** endPoint responses
* Added `Current-Page`, `Next-Page`, `Prev-Page`, `Last-Page` and `First-Page` headers to `GET /events` and `GET /event-subscriptions` responses
* Added default error handling in `GET /event-subscriptions`


### [v2.0.1](https://app.swaggerhub.com/apis-docs/dcsaorg/DCSA_TNT/2.0.1)
This is supposed to be a Major update correcting errors - but at the time this API was released no one had started implementing v2.0.0 so it was decided "just" to make this a patch release

* transportCallID removed from ShipmentEvents
* shipmentID is re-introduced into ShipmentEvents
* transportCallID made mandatory on EquipmentEvents
* spelling mistake fixed in errorDateTime
* eventID format changed from string -> UUID
* scheduleID changed from number -> UUID
* transportCallID changed from number -> UUID

#### [v2.0.0](https://app.swaggerhub.com/apis-docs/dcsaorg/DCSA_TNT/2.0.0)

#### Dependencies between Track and Trace and Operational Vessel Schedules APIs
In the [Information Model 2.0](https://dcsa.org/wp-content/uploads/2020/07/DCSA-Information-model-2.0-vF.pdf), details about locations have been removed from T&T events, and added to transport calls. Instead of containing location details, events contain a reference to a transport call. Transport calls are a part of the [OVS 1.0 API](https://app.swaggerhub.com/apis/dcsaorg/DCSA_OVS/1.0.1), which means that the [Track & Trace](https://app.swaggerhub.com/apis/dcsaorg/DCSA_TNT) [v2.0.0](https://app.swaggerhub.com/apis-docs/dcsaorg/DCSA_TNT/2.0.0) and [v2.0.1](https://app.swaggerhub.com/apis-docs/dcsaorg/DCSA_TNT/2.0.1) APIs depends on functionality from the [OVS] (https://app.swaggerhub.com/apis-docs/dcsaorg/DCSA_OVS) API.

* Updated event structure to use Transport Calls
* Added Pagination
* Added Signature header to callbacks