# Authentication Module

The Events254 API provides developer authentication and authorization. It will also provide user authentication
as well as user management features with access control in built.

<aside class="warning">
    User authentication and authorization is not yet implemented. See roadmap for more details.
</aside>

## Developer Apps API

<aside class="notice">
    You require an **appID** and **appSecret** in order to access the API. They are provided by the developer.
    <a href='mailto:waweruj00@gmail.com' target='__blank' style='color: white;text-decoration: none;font-weight: 500;text-shadow: none;'>Request for a Developer Key</a>
</aside>

### Request Headers

Parameter | Description | Status
--------- | ----------- | -------  
**x-auth-app-id** | This should contain your app id | **required**
**x-auth-app-token** | This should container your app token | **required**

<aside class="notice">
    The above stated headers are required in order to consume the API. It ensures that the requests being sent to the API are secure and from trusted sources.
    If you haven't yet got your **appID** and **appSecret**, please contact the developer:-
    <a href='mailto:waweruj00@gmail.com' target='__blank' style='color: white;text-decoration: none;font-weight: 500;text-shadow: none;'>Request for a Developer Key</a>
</aside>
