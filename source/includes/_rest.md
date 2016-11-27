# RESTful API

## Authentication

> <h3 class='toc-ignore'>Getting The Credentials</h3>

```shell
curl -u "john@doe.com:osamayor" https://api.fonoster.com/v1/users/credentials
```

`GET https://api.fonoster.com/v1/users/credentials`

Obtain your _Account Id_ and _Token_ by making a call to the `credentials` resource. You
will use this later to perform BasicAuthentication. Your credentials are also 
available in Fonoster's console.

## Make a call

> <h3 class='toc-ignore'>Call Example</h3>

```shell
curl -vkH "Content-Type: application/json" \
-u "5678c1a440307c529ceb66c5:61b17c2f33834c429ac53a2f8a1ff333" \
-XPOST --data '{"appId":"5678f0ee40307c6728f60c4b", \
                "from":"+17066041487", \
                "to":"+17065935971"}' \
https://api.fonoster.com/v1/accounts/5678c1a440307c529ceb66c5/calls
```

`POST https://api.fonoster.com/v1/accounts/{Account Id}/calls`

Making a call with Fonoster is easy with _curl_. You must send the following parameters.

Attribute      | Description    | Optional
-------------- | -------------- | --------------
appId          | Find this in the dashboard | No
from           | Origin in E.164 format     | No
to             | Destination in E.164 format| No
sendDigits     | Play DTMF before call| Yes
timeout        | Hangup after timeout elapsed(default is 60 seconds)| Yes
record         | Whether should record the call| Yes
autoanwser     | Tells the engine whether or it should answer this call (use in combination with the *Answer* verb) | Yes

