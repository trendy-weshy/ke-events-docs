# API Errors

This sections all the types of Errors the Api can generate. Some are outside the scope of the API so we will just mention them. Some of the errors out of scope is Database related Errors, Server related Errors and Code related Errors.

> The data structure of an API Error.

```typescript
interface ApiError extends Error { /* extends Node.js Error */
    name: string;
    status: number; // HTTP Status Code
    message: string;
    level: 'error' | 'info' | 'warning'
}
```

Name | level | status |  Meaning
---------- | ------- | -------
**CreationError** | _error_ | 500 | Error occurred while trying to save data in the database
**EmptyRecord** | _warning_ | 404 | Shows the query returned an empty record, nothing was found
**QueryError** | _error_ | 500 | Shows the query request lacks some requirement for it to be a full success e.g a missing query-param
**RequestError** | _error_ | 400 | Shows during a POST, PUT or DELETE method request, some was missing hence could not complete the result
**CredentialsError** | _critical_ | 401 | Shows that there is something wrong with the apps credentials passed in the headers
**AuthorizationError** | _critical_ | 401 | Shows that there was a problem while trying to authorize app to access api data due to corrupt authentication details.
**DuplicateRecord** | _error_ | 500 | Shows that the record trying to be saved already exists and only one copy can be recorded.
**DecodeError** | _error_ | 500 | Shows that the apps hash secret could not be decoded
**PaginationError** | _warning_ | 400 | Means there was a problem with trying to paginate from the query provided. Can be due to client expecting excess page that the total number of pages
**DateRangeError** | _error_ | 500 | Shows a problem rose when a date range was being configured so as to make the database query valid

If for some reason you experience some error not documented, i.e, CastError, ValidationError, InternalServerError etc. then this is an internal error with the API. If such errors continue after several requests; <a href="mailto:waweruj00@gmail.com" __target="__blank">Make sure to contact the developer</a>
