---
title: SSO Beta

---

SSO Beta
=====


## ZeroTier Central configuration
### Get access
- Contact ZeroTier to enable SSO on your my.zerotier.com account.

### Update clients
- Download and install ZeroTier 1.8.10 or greater on clients that will use SSO.

    https://www.zerotier.com/download/


### Configure SSO in ZeroTier Central 
Visit https://my-dev.zerotier.com/account and complete the SSO configuration toward the bottom of the page.

![SSO-Account-Setup](/img/sso-account-setup.png)


### Configure SSO on individual networks. 
If you enable this on an existing network, you may accidentally block existing users. Please practice on a test network.
![SSO-Network-Enable](/img/sso-network-enable.png)


### Exclude specific devices from SSO requirements
This is useful for routers, servers, embedded devices, etc…
You can do this from the wrench icon in the Members list.


## SSO provider configuration
Visit your SSO provider and use this callback URL:
```
http://localhost:9993/sso
```

Ensure the following scopes are allowed:  `openid`, `profile`, `email`, `offline_access`.



![SSO-Member-Exclude](/img/sso-member-exclude.png)

## Provider Specific Configuration Notes
### Auth0 
Please ensure the following fields are set on your Auth0 application config:
- Application Type:  Native
- Token Endpoint Authentication Method: None
- Allowed Callback URL: http://localhost:9993/sso
- Under Advanced Settings -> Grant Types, ensure Implicit, Authorization Code, and Refresh Token are selected.

### Google
Google OAuth2/OIDC is not supported as Google does not support PKCE clients at this time.

### OneIdentity
OneIdentity may require manual whitelisting of the following scopes: `openid`, `profile`, `email`, `offline_access`.


## Customizing the SSO Completion Page

If you wish, you can customize the final view of the sso login process. 
Create the file `$ZEROTIER_HOME/sso-auth.template.html`.

You may customize the page to look however you wish. At this time there
are only two template values set by zerotier:
- networkId
- messageText

Templates must be valid HTML, and the template values must be placed inside ``{{ ...  }}` blocks like so:

    {{ networkId }}
    {{ messageText }}

More info and instructions to come.
