---
ai_generated: true
model: "openai/gpt-5.4@2026-08"
operator: "johnmillerATcodemag-com"
chat_id: "create-ride-hailing-dispatch-orm-model-20260806"
prompt: |
  Create an ORM model for a Ride-hailing Dispatch application
started: "2026-08-06T00:00:00Z"
ended: "2026-08-06T00:20:00Z"
task_durations:
  - task: "domain modeling"
    duration: "00:12:00"
  - task: "artifact authoring"
    duration: "00:06:00"
  - task: "validation and documentation"
    duration: "00:02:00"
total_duration: "00:20:00"
ai_log: "ai-logs/2026/08/06/create-ride-hailing-dispatch-orm-model-20260806/conversation.md"
source: "user prompt"
---

# Ride-hailing Dispatch ORM Model

## Universe of Discourse

- Business boundary: Real-time ride request intake, dispatching, driver assignment, trip execution, fare capture, and completion for a ride-hailing platform.
- Primary goal: Represent the dispatch domain as fact-oriented business statements that can be validated with non-technical stakeholders before logical or physical design.

## Object Types

- Rider: A customer who requests transportation.
- Driver: A person authorized to accept and fulfill ride assignments.
- Vehicle: A car used by a driver for ride fulfillment.
- RideRequest: A rider's request for transportation from an origin to a destination.
- PickupLocation: A named or geocoded origin location.
- DropoffLocation: A named or geocoded destination location.
- Dispatch: The assignment attempt that offers a ride request to a driver.
- Trip: The fulfilled transportation service for an accepted ride request.
- Fare: The monetary charge calculated for a trip.
- Payment: The settlement event for a fare.
- ServiceZone: An operational area in which requests and drivers are managed.
- DriverStatus: The current dispatchable state of a driver.
- VehicleType: The service class of a vehicle, such as economy or XL.

## Reference Schemes

- Rider is identified by RiderId.
- Driver is identified by DriverId.
- Vehicle is identified by VehicleId.
- RideRequest is identified by RequestId.
- Dispatch is identified by DispatchId.
- Trip is identified by TripId.
- Fare is identified by FareId.
- Payment is identified by PaymentId.
- ServiceZone is identified by ZoneCode.
- DriverStatus is identified by StatusCode.
- VehicleType is identified by VehicleTypeCode.
- PickupLocation is identified by PickupLocationCode.
- DropoffLocation is identified by DropoffLocationCode.

## Elementary Fact Types

- Rider places RideRequest.
- RideRequest originates at PickupLocation.
- RideRequest ends at DropoffLocation.
- RideRequest requests VehicleType.
- RideRequest is created in ServiceZone.
- RideRequest has requested pickup time.
- RideRequest has request time.
- RideRequest has request status.
- Driver operates Vehicle.
- Vehicle is of VehicleType.
- Driver is in DriverStatus.
- Driver is currently located in ServiceZone.
- Driver is licensed for ServiceZone.
- Dispatch is for RideRequest.
- Dispatch offers RideRequest to Driver.
- Dispatch has offer time.
- Dispatch has response deadline.
- Dispatch has dispatch status.
- Driver accepts Dispatch.
- Driver declines Dispatch.
- Trip fulfills RideRequest.
- Trip is performed by Driver.
- Trip uses Vehicle.
- Trip starts at PickupLocation.
- Trip ends at DropoffLocation.
- Trip has trip start time.
- Trip has trip end time.
- Trip has trip status.
- Fare is calculated for Trip.
- Fare has base amount.
- Fare has distance amount.
- Fare has time amount.
- Fare has surge multiplier.
- Fare has total amount.
- Payment settles Fare.
- Payment is made by Rider.
- Payment has payment method.
- Payment has payment status.

## Derived Facts

- Driver is dispatchable if Driver is in DriverStatus Available and Driver is currently located in the ServiceZone of a pending RideRequest.
- Trip duration is derived from trip end time minus trip start time.
- Fare total amount is derived from base amount, distance amount, time amount, surge multiplier, and any discounts or fees.

## Constraints

### Uniqueness Constraints

- Each RiderId identifies at most one Rider.
- Each DriverId identifies at most one Driver.
- Each VehicleId identifies at most one Vehicle.
- Each RequestId identifies at most one RideRequest.
- Each DispatchId identifies at most one Dispatch.
- Each TripId identifies at most one Trip.
- Each FareId identifies at most one Fare.
- Each PaymentId identifies at most one Payment.
- Each RideRequest is placed by exactly one Rider.
- Each RideRequest originates at exactly one PickupLocation.
- Each RideRequest ends at exactly one DropoffLocation.
- Each RideRequest requests exactly one VehicleType.
- Each RideRequest is created in exactly one ServiceZone.
- Each Dispatch is for exactly one RideRequest.
- Each Dispatch offers the RideRequest to exactly one Driver.
- Each Trip fulfills exactly one RideRequest.
- Each Trip is performed by exactly one Driver.
- Each Trip uses exactly one Vehicle.
- Each Fare is calculated for exactly one Trip.
- Each Payment settles exactly one Fare.

### Mandatory Role Constraints

- Every RideRequest must be placed by a Rider.
- Every RideRequest must have an origin and destination.
- Every Dispatch must be for a RideRequest and offered to a Driver.
- Every accepted RideRequest that is fulfilled must correspond to a Trip.
- Every completed Trip must have a Fare.

### Subset and Equality Constraints

- Every Driver that accepts a Dispatch must be the Driver to whom that Dispatch was offered.
- Every Trip start location must equal the PickupLocation of the fulfilled RideRequest.
- Every Trip end location must equal the DropoffLocation of the fulfilled RideRequest.
- Every Vehicle used by a Trip must be operated by the Driver performing that Trip. <-- TODO

### Exclusion Constraints

- A Dispatch cannot be both accepted and declined.
- A RideRequest cannot be both canceled and completed.
- A Driver cannot be both Available and OnTrip at the same time.

### Frequency Constraints

- A pending RideRequest may be offered to many Drivers over time, but each Dispatch offers it to only one Driver.
- A Driver may operate many Trips over time, but a Trip has exactly one Driver.
- A Driver may operate many Vehicles over time, but at any point in time a Driver operates at most one active Vehicle for dispatch.

### Ring Constraints

- The relation Driver is backup for Driver is asymmetric.
- The relation Driver mentors Driver is acyclic.

## Objectification

- Objectified fact type: Driver accepts Dispatch.
- Object type: AcceptanceEvent.
- Rationale: Acceptance may need its own timestamp, app version, geolocation snapshot, and fraud-review outcome without overloading Dispatch.

## Typical Verbalizations

- Each ride request is placed by exactly one rider.
- Each dispatch offers one ride request to one driver.
- A driver who accepts a dispatch must be the same driver to whom the dispatch was offered.
- Each completed trip has exactly one fare.
- Each payment settles exactly one fare.

## Conceptual Queries

- Which available drivers in a service zone can satisfy a pending ride request for a requested vehicle type?
- Which ride requests were offered to more than three drivers before acceptance?
- Which drivers declined more than five dispatches in the last hour?
- Which trips started more than ten minutes after the requested pickup time?
- Which completed trips have a fare but no successful payment?
- Which service zones currently have pending ride requests with no dispatchable drivers?

## Assumptions and Open Issues

- Assumption: Surge pricing is calculated after driver acceptance but before payment settlement.
- Assumption: A ride request represents a single requested trip, not pooled or multi-stop travel.
- Assumption: Real-time driver location is reduced to the current service zone at the conceptual level.
- Open issue: Whether pooled rides should be modeled as one Trip serving multiple RideRequests.
- Open issue: Whether driver re-assignment after acceptance is allowed or prohibited by policy.
- Open issue: Whether cancellations incur a Fare or a separate CancellationCharge object type.

## Suggested Relational Mapping Notes

- Map core object types to tables keyed by their reference schemes.
- Keep Dispatch separate from RideRequest to preserve the history of multiple assignment attempts.
- Model constrained enumerations such as DriverStatus and VehicleType as reference tables.
- Evaluate whether AcceptanceEvent should be materialized as its own table based on audit requirements.

## Validation Checklist

- [ ] Confirm service-zone semantics with dispatch stakeholders.
- [ ] Confirm whether declined, expired, and timed-out dispatch offers need separate status object types.
- [ ] Confirm whether vehicle eligibility depends only on vehicle type or also on accessibility and equipment attributes.
- [ ] Confirm payment retry and split-payment behavior.
- [ ] Review all verbalizations with a domain expert before logical design.
