Software Requirements Specification

Project: Bus Agency Seat Booking System | Group: 8 (CEF 345) | Version: 0.1 | Date: 14 November 2026

1. Introduction

Purpose: To state what the system must do, so it can be built and tested.

Scope: A system for a Buea-Douala travel agency to manage buses, trips, seat bookings, parcels and daily takings, replacing paper records.

Definitions: Manager = the agency owner (can do everything an Agent can, and more). Agent = counter staff who sell tickets and record parcels. Trip = one bus on one route at one date and time. XAF = Central African CFA franc.

2. Overall description
Stakeholders: Manager, Agents, Passengers, the development group.
Users and skills: Manager and Agents use basic phones or a shared computer and are busy at the counter, so the system must be quick and simple.
Operating environment: A web app in a phone or computer browser, often on 3G.
Constraints: Delivered within the course timetable; built with JavaScript, Node.js, Express and SQLite.
Assumptions: The route is Buea-Douala. No client interview was done, so requirements come from team brainstorming and the business rules suggested for this theme. Only staff use the system, not passengers.
3. Functional requirements
ID	Requirement
FR-01	The system shall let a user log in with a username and password.
FR-02	The system shall let the Manager add, edit and delete buses, with plate number, name and number of seats.
FR-03	The system shall let the Manager create a trip with route, departure date and time, bus and ticket price in XAF.
FR-04	The system shall let an Agent view all upcoming trips with the number of free seats on each.
FR-05	The system shall let an Agent book a seat on a trip by entering the passenger's name, phone number and seat number.
FR-06	The system shall reject a booking for a seat that is already booked on that trip and show the message "Seat already taken".
FR-07	The system shall reject a booking made after the trip's departure time.
FR-08	The system shall let an Agent cancel a booking, and the seat shall become free again.
FR-09	The system shall print or display a ticket after each booking, showing the passenger, route, date, time, seat number and price.
FR-10	The system shall record the payment method (cash, MTN MoMo or Orange Money) for each booking.
FR-11	The system shall let an Agent record a parcel with sender, receiver, destination and weight, and shall calculate the fee from the weight.
FR-12	The system shall show the Manager a daily report with total tickets sold, total parcel fees and total money collected per payment method.
4. Non-functional requirements
ID	Requirement	Type
NFR-01	Booking a seat shall take no more than 30 seconds for a trained Agent.	Usability
NFR-02	Every page shall load in under 3 seconds on a 3G connection.	Performance
NFR-03	All amounts shall be shown in XAF with no decimals (for example 5 000 XAF).	Constraint
NFR-04	Only the Manager shall be able to add or delete buses and trips or change prices.	Security
NFR-05	The interface shall work in a phone browser 360 px wide.	Compatibility
5. Use case diagram and descriptions

Diagram: docs/diagrams/usecases.drawio.svg

Actors: Agent, Manager (the Manager is a specialisation of the Agent).
Agent use cases: Log in, View upcoming trips, Book seat, Cancel booking, Record parcel.
Manager-only use cases: Manage buses, Create trip, View daily report.
Relationships: Book seat <<include>> Issue ticket; Book seat <<include>> Record payment.
UC-01: Book a seat
Actors: Agent, Manager
Preconditions: User is logged in; an upcoming trip has a free seat.
Main flow: 1. User opens the upcoming trips. 2. User selects a trip. 3. User enters passenger name, phone and seat number. 4. User picks the payment method. 5. User confirms. 6. System saves the booking, marks the seat taken and shows the ticket.
Alternative 3a: Seat already booked: system shows "Seat already taken" and stays on step 3.
Alternative 5a: Departure time has passed: system refuses the booking.
Postconditions: Booking saved with date, time and user; seat unavailable; payment method stored.
Requirements covered: FR-04, FR-05, FR-06, FR-07, FR-09, FR-10
UC-02: Create a trip
Actors: Manager
Preconditions: Manager is logged in; at least one bus exists.
Main flow: 1. Manager opens "New trip". 2. Manager enters route, date and time. 3. Manager picks a bus and enters the price in XAF. 4. Manager confirms. 5. System saves the trip with all seats free.
Alternative 4a: A field is missing: system highlights it and stays on the form.
Postconditions: Trip appears in upcoming trips.
Requirements covered: FR-02, FR-03, FR-04, NFR-04
UC-03: View daily report
Actors: Manager
Preconditions: Manager is logged in.
Main flow: 1. Manager opens "Reports". 2. Manager picks a date (today by default). 3. System shows tickets sold, parcel fees and money collected per payment method, in XAF.
Alternative 3a: No sales that day: system shows zero for every figure.
Postconditions: No data is changed.
Requirements covered: FR-10, FR-11, FR-12, NFR-03, NFR-04
6. Priorities (MoSCoW)
Priority	Items
Must have	FR-01 to FR-09, FR-12
Should have	FR-10, FR-11, NFR-01 to NFR-05
Could have	Weekly sales chart
Won't have	See section 7
7. Out of scope

Online booking by passengers; Mobile Money integration (the system only records the method used); SMS or WhatsApp reminders; driver and fuel management.
