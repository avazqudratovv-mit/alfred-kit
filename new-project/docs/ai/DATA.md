# Data and API contract

<!-- The shapes of the data the screens show. Written before the UI, so the UI can use mock data
     with the same shapes, and the backend later only has to fill them. -->

## Entities
### <Event>
| Field | Type | Notes |
|---|---|---|
| id | string | |
| title | string | max 120 |
| startAt | ISO date | |
| <...> | | |

## Relationships
- <An Organizer has many Events; an Event has many TicketTypes; ...>

## Main operations (API)
| Operation | Input | Output | Who |
|---|---|---|---|
| <getEvents> | <filters, page> | <Event[] + total> | everyone |
| <createOrder> | <eventId, items> | <Order> | signed-in buyer |

## Mock data
Mock files live in `<src/mocks/>` and follow these shapes exactly. When the backend is ready, only the data source changes, not the components.
