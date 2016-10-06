# netlify-subscriptions
This acts as a proxy to stripe. It exposes a very simple way to call stripe's subscription endpoints. 

## authentication
All of the endpoints rely on a JWT token. We will use the user ID set in that token for the user information to stripe.

It relies on a JWTClaims that has these extra fields:

``` json
{
    "groups": [],
    "id": "",
    "email": ""
}
```

The API as is:

    GET /subscriptions -- list all the subscptions for the user

These endpoints are all grouped by a `type` of subscription. For instance if you have a `membership` type with 
plan levels gold, silver, and bronze.  

    GET /subscriptions/:type
    POST /subscriptions/:type
    DELETE /subscriptions/:type
    
The POST endpoint takes a payload like so

``` json
    {
        "stripe_key": "xxxxx",
        "plan": "silver"
    }
```

Using this endpoint will create the plan if it doesn't exist, otherwise it will change the subscription to that plan. 
The other responses are defined in `api/subscriptions.go`.
