---
description: This article explains 2FA implementation in Aidbox
---

# Two Factor Authentication

{% hint style="warning" %}
This feature is in beta right now. If you have any feedback or comments, reach out to us!
{% endhint %}

{% hint style="info" %}
Two Factor Authentication is not supported for external OAuth 2.0 providers
{% endhint %}

Aidbox supports Two Factor Authentication with TOTP \(time-based one-time passwords\). This article explains how to enable 2FA for a user, login with one-time password, and get an access token for your application. Familiarity with [OAuth 2.0](https://tools.ietf.org/html/rfc6749) and [TOTP](https://tools.ietf.org/html/rfc6238) is suggested. All examples are executable in Aidbox REST console.

#### Create configuration resources

We have to create three resources to implement 2FA: User, Client, and AuthConfig. Client is needed to enable desired OAuth 2.0 flow for your application and AuthConfig stores 2FA settings. Refer to the specific OAuth flow article to understand how to create Client resource suitable for your use case.

{% tabs %}
{% tab title="Example AuthConfig" %}
```
PUT /AuthConfig/myconfig

twoFactor:
 issuerName: my-app 
 validPastTokensCount: 3 
 webhook:
  endpoint: https://my-app.com
  timeout: 500
```
{% endtab %}

{% tab title="Example Client" %}
```text
PUT /Client/mywebapp

secret: verysecret
first_party: true
grant_types:
  - code
auth:
  authorization_code:
    redirect_uri: 'http://localhost:3001'
    access_token_expiration: 360
    token_format: jwt
    secret_required: true
    refresh_token: true
```
{% endtab %}

{% tab title="Example User" %}
```
PUT /User/my-user

id: my-user
password: password
```
{% endtab %}
{% endtabs %}

| AuthConfig attribute | meaning |
| :--- | :--- |
| twoFactor.issuerName | Name of the TOTP token issuer that is shown in authenticator |
| twoFactor.validPastTokensCount | Number of previous tokens that are considered valid. Used to improve user experience if standard 30 seconds token lifetime is not enough. |
| twoFactor.webhook.endpoint | Endpoint to send the TOTP token to during login. Used to support scenarios when it's not possible to use the mobile authenticator. For instance, a service integrated with twilio may listen on this address.  |
| twoFactor.webhook.timeout | Timeout for webhook in milliseconds |
| twoFactor.webhook.headers | Key-value headers for webhook |
| theme.styleUrl | URL to external stylesheet to customise how the authentication form looks like |
| theme.title | Title to use on the authentication form |
| theme.brand | Application name to display on the authentication page |

#### Enable 2FA

Redirect the user to the following URL to establish TOTP authentication. The user should already be logged into Aidbox.

```text
GET /auth/two-factor/enable
```

When the user scans the QR code and enters the token, they will get redirected to the 2FA settings page. Aidbox saves that 2Fa is enabled for this user into the User.twoFactor attribute.

#### Login into Aidbox

Next time when the user log ins into the system, the TOTP authentication page will be shown. Using the mobile authenticator \(or any other transport\) the user enters the code and gets redirected to your application. You can configure which OAuth 2.0 flow to use by changing Client configuration and login endpoint query parameters. Refer to the specific OAuth flow article if you need further explanation.

```text
GET /auth/login?client_id=mywebapp&response_type=code
```

#### Disable 2FA

Redirect the user to the following URL to disable 2FA. When the user enters a token, they get redirected to 2FA settings page. Aidbox sets User.twoFactor.enabled to false.

```text
GET /auth/two-factor/disable
```
