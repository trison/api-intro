# Intro to the sendwithus API

## Getting Started with sendwithus
Thanks for choosing to send emails with sendwithus! 

Sendwithus is a REST API, which uses HTTP request methods such as POST and GET
to send and retrieve information. 

Don't know what these terms mean? Don't worry! This short introduction will help guide you through understanding our API
and sending your first email. 

We will use the 'cURL' command line tool for our examples, but we also provide API Clients for:

* Python
* Ruby
* Ruby On Rails
* Node.js
* PHP
* Java

# REST API
The sendwithus API is based on the REST architectural style. This means information is transferred through HTTP requests to URLs
that have certain resources(such as customers, or email templates). REST APIs are widely used in web services and 
provide user authentication and error indication.

## HTTP
Sendwithus uses the HTTP request methods PUT, POST, GET and DELETE in its API. 

* **PUT**: Update your data *eg. change a user's name*
* **POST**: Create new data *eg.  add a new user*
* **GET**: Retrieve your data *eg.  get a list of your email templates*
* **DELETE**: Delete data *eg. remove a user*

## JSON
- Mention sendwithus uses JSON as opposed to other technologies

Sendwithus uses JSON, which is a data format that holds objects with key-value pairs. This means that
data is stored as blocks that have a set of values that can be accessed through their corresponding keys. Let's look at
an example:
```
[
    {
        "id": "Template ID",
        "name": "Template Name",
        "locale": "en-US",
        "created": "created unix timestamp",
        "versions": [
            {
                "name": "Version Name",
                "id": "Version ID",
                "created": "created unix timestamp",
                "modified": "modified unix timestamp"
            }
        ],
        "tags": ["tag1", "tag2"]
    }
]
```
This is a response from using the GET request to get email templates. We can see this template has the value *"Template ID"* corresponding to the *"id"* 
key and the value *"Template Name"* corresponding to the *"name"* key. When interacting with the API, you will send and receive JSON formatted data.

## Authentication
HTTP authentication is done by providing a username and password when making an HTTP request. Authentication with our API can be 
done with only your API key as your username. Your API key can be found by going into your dashboard and 
clicking on the **API Settings** menu tab. You can try a basic authentication command with

`curl -u <your_API_key>: https://api.sendwithus.com/api/v1`

Here we are using the cURL command with the option *-u* to supply a username to the base API URL at https://api.sendwithus.com/api/v1.

## Error Handling
HTTP provide status codes in response headers when requests are made. To include the HTTP header in the response,
enter the cURL option `-i` in your request command. The header will include status codes:

* 2xx - Success!
* 4xx - There was an error on the client side
* 5xx - There was an error on the server side

A client side error can be made from a mistyped request, an unauthorized request, an unavailable resource or more. See a full
list of 4xx errors at https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#4xx_Client_Error

A server side error can result from an unrecognizable request, server downtime, or more. A full list of 5xx errors can be found
at https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#5xx_Server_Error

We can try an authentication request using an invalid API key, which results in a 403 Forbidden error:

`curl -i -u live_1234: https://api.sendwithus.com/api/v1
`

# Sending your first email
Let's go through what we know to send your first email!

We will send an email using a purchase confirmation template. Sending an email will require using the 
POST request method to create a new email. We will send the request to

`https://api.sendwithus.com/api/v1/send`

The cURL command will then be:

```
curl -X POST \
		-u <your_API_key>: \
		-d '{
      			"template": "tem_QMpTUhsJ2RF8aZTUg9Ti6S",
      			"recipient": {
       				 "address": "<your_recipient_address>"
      			}
    		}' \
    		https://api.sendwithus.com/api/v1/send
```

Here we are using the cURL command to send a POST request, authenticating with your API key, sending the email data, which goes to the *send* URL.
