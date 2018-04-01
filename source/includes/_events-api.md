# Events API Module

This is the main module for the api as it serves Kenyan events data. It powers Events254 app.

```typescript
interface Event {
    "_id": string, // Database ID
    "link": string, // HTTP link to learn more about the event
    "image": string, // An image link for the event's poster
    "title": string, // The title of the event
    "about": string, // An overview of the Events and its description
    "map": string, // A google maps link to the location of the event
    "location": string, // Where the event will be held (A Formatted Address)
    "twitter": string, // Twitter link for sharing about the event
    "whatsapp": string, // Deeplink for sending whatsapp message about the event
    "google_plus": string, // Google plus link for sharing about the event
    "start": Date, // When the event is supposed to start (isISOString)
    "end": Date, // When the event is supposed to end (isISOString)
    "createdAt": Date, // When was the event recorded to the database (isISOString)
    "updatedAt": Date // When was the event record last updated (isISOString)
};
```

<aside class="notice">
    Please note that for every request you make you require the following header included: **x-auth-app: [api_key]**. Please visit the <a href="#authentication-module" style='color: white;text-decoration: none;font-weight: 500;text-shadow: none;'>The Authentication Section</a> for more.
</aside>

List of Routes Available

1. **[GET]** `/api/v1/events/q/:by` - Query for a paginated list of events
2. **[GET]** `/api/v1/events/get/:by` - Get a list of events
3. **[GET]** `/api/v1/events/location` - Get a list of Event Location
4. **[GET]** `/api/v1/events/ping` - Test Events API
5. **[GET]** `/api/v1/events/:id` - Get a single event

## Test Events API

Use this route if you want to test whether the API is online and working.

> Ping interface

```typescript
interface PingObject {
    payload: string;
    timestamp: Date;
}
```

> Example ping response

```json
{
    "payload": "0chwzYWLATM34L6/2tfb",
    "timestamp": "2018-03-29T01:05:42.269Z"
}
```

### Route

`[GET] /api/v1/events/ping`

### Response Object

Parameter | DataType | Description
--------- | -------- | -----------
**payload** | String | A Base64 string
**timestamp** | Date | A Date in ISODateString

## Get list of Events

This route provides a list of events based on a *querystring* and uses either **location** or **date** as the primary query keys.

### Route

`[GET] /api/v1/events/get/:by`

### Request parameters

This is a request parameters i.e. /some-route/:by can translate to /some-route/location or /some-route/date.

Parameter | Description
--------- | -----------
**by** | has only two options **location** and **date**

### Request Query

This is a querystring i.e. /?key=1&key2=the

Parameter | Description | Status
--------- | ----------- | --------
**event_loc** | Name of location | *To be provided when the request parameter **by** above is **location***
**start_date** | Begin date of an event | *To be provided when the request parameter **by** above is **date** and should follow the format: **MM-DD-YYYY***
**end_date** | End date of an event | *Can be provided when the request parameter **by** above is **date** and should follow the format: **MM-DD-YYYY**.* This field is an **Optional Query**

### Response

If the request is successful, the route will return a list of [**Events**](#events-api-module). No pagination is done. For server paginated records please visit the **Query list of Events** section for more about this.

## Query list of Events

This route provides a list of events based on a *querystring* and uses either **location** or **date** as the query basis. This route is designed to returned paginated records. For each page requested the API provides a limited number of records.

### Route

`[GET] /api/v1/events/q/:by`

### Request parameters

Parameter | Description
--------- | -----------
**by** | has only two options `location` and `date`

### Request Query

Parameter | Description       | Status
--------- | ----------------- | --------
**curr_page** | The current page | **required** - should be a `Number`
**event_loc** | Name of location | *To be provided when the request parameter **by** above is `location`*
**start_date** | Begin date of an event | *To be provided when the request parameter **by** above is `date` and should follow the format: `MM-DD-YYYY`*
**end_date** | End date of an event | *Can be provided when the request parameter **by** above is `date` and should follow the format: `MM-DD-YYYY`.* This field is an **Optional Query**

**PLEASE NOTE:**

The **`curr_page`** querystring option should follow the zero-index rule.

That is, if your at the *first page* on your app then **`curr_page`** should be **`0`**. If your on your *fourth page* in your app **`curr_page`** should be **`3`**

### Response Object

Parameter | DataType | Description
--------- | -------- | -----------
**data** | Array[**[Event]**](#events-api-module) | Contains an array of events
**pagination** | Object | *Contains metadata about the data queried*
**pagination.totalNumOfPages** | Number | Total number of pages based on the query provided in the request and number of records per page
**pagination.totalReturnedItems** | Number | Total number of records in the present request
**pagination.isLastPage** | Boolean | Shows if the request has accessed the last page, therefore no more records can be queried for using the same query.

## Get list of Event Locations

This route provides a list of event locations by aggregating the all event records. It's the simplest events api endpoint since it has no inputs _(Requesy Body)_, no _(Query Strings)_ and no _(Request Parameters)_.

### Route

`[GET] /api/v1/events/location`

### Response

An Array of Strings which are Event Locations.

## Get Event Details

Use this route if you want a single event object.

### Route

`[GET] /api/v1/events/:id`

### Request parameters

Parameter | DataType | Description
--------- | -------- | -----------
**id** | String | The events **Database ID**

### Response

Returns an Array[**Events**](#events-api-module)