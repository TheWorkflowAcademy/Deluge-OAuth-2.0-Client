# Deluge-OAuth-2.0-Client
Connect to an API with OAuth 2.0 authentication in a Deluge function.

## Introduction
Zoho has many pre-built connections and you can create custom connections. These are often the right solution to a problem, but limits the control you have on the connection.

There are two scripts in this repository.
1. Request Refresh Token (This will only be executed one time)
2. Refresh Access Token

## OAuth 2.0
OAuth 2.0 is an authentication framework for web apps and APIs. Though each API may implement some details differently, OAuth 2.0 services generally work the same.
1. User generates an "authorization code" by making a GET request to the API.
2. Client app (Zoho in this case) uses the recently received `code`, `client_id`, and `client_secret` to receive a `refresh_token`.
3. The client app then uses the `refresh_token` to get a new `access_token`, which is the key to let you call the API. Access tokens generally expire after 60 minutes.

## Configuration
### Find your API Documentation and Register Your App
API documentation is a must if you're going to continue with this script. Without it you will not get anywhere.

You will need to register your application with the software you are trying to connect with Zoho CRM. This will give you a `client_id` and a `client_secret` in exchange for a `redirect_uri`.

### Generate an Authorization Code
You can find out how to get an authorization code in the Authentication section of your API documentation. Construct the URL by combining the `base_url` with the query parameters like so: `https://www.example.com/authorize?client_id=YOUR_CLIENT_ID&response_type=code&redirect_uri=YOUR_REDIRECT_URI`. Paste this into your browser, then check the URL. It should looks something like `https://testing.com?code=abc...123`. Copy and paste that code, because you will need it in the script. This code usually expires within an hour, so you will want to rerun this after you implement the scripts.

### Generate a Refresh Token
If you know how to generate a `refresh_token` yourself in a tool like Postman, go crazy. Otherwise, there is a provided Deluge script to help you do this. You will need the `client_id`, `client_secret`, and authorization `code` to do this. Be sure to match the parameters and names to your APIs specs, then run it. This will provide you with the `refresh_token`. Copy this `refresh_token` and paste it locally on your computer.

### Set Up Your CRM Variables
This script relies on CRM Variables for the following fields:
- `client_id`
- `client_secret`
- `refresh_token`

You can name these what you want, but be sure to change the names of them in the script.

### Take Note at Parameter Names
As mentioned earlier, not every OAuth 2.0 authentication will look the same. Be very thorough with naming conventions for urls, headers, and parameters.

### Get a Refreshed Access Token
This script relies on CRM Variables, if you do not want to store these values as CRM Variables, you can reconfigure this to store them as string literals in your Deluge code. Again, pay VERY close attention to parameter names, URLs, and headers in your API documentation.
