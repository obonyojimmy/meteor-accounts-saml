*this package is working but may have issues with various saml providers*
see the example app `example-openidp` and http://accounts-saml-example.meteor.com/ for a demo

*you will not be able to do saml authentication when developing locally as the idp can not return to a localhost url* 

put saml settings in meteor.settings like so:

```
"saml":[{
    "provider":"openidp",
    "entryPoint":"https://openidp.feide.no/simplesaml/saml2/idp/SSOService.php",
    "issuer": "<URL OF YOUR APP>",
    "cert":"MIICizCCAfQCCQCY8tKaMc0BMjANBgkqhkiG9w0BAQUFADCBiTELMAkGA1UEBhMCTk8xEjAQBgNVBAgTCVRyb25kaGVpbTEQMA4GA1UEChMHVU5JTkVUVDEOMAwGA1UECxMFRmVpZGUxGTAXBgNVBAMTEG9wZW5pZHAuZmVpZGUubm8xKTAnBgkqhkiG9w0BCQEWGmFuZHJlYXMuc29sYmVyZ0B1bmluZXR0Lm5vMB4XDTA4MDUwODA5MjI0OFoXDTM1MDkyMzA5MjI0OFowgYkxCzAJBgNVBAYTAk5PMRIwEAYDVQQIEwlUcm9uZGhlaW0xEDAOBgNVBAoTB1VOSU5FVFQxDjAMBgNVBAsTBUZlaWRlMRkwFwYDVQQDExBvcGVuaWRwLmZlaWRlLm5vMSkwJwYJKoZIhvcNAQkBFhphbmRyZWFzLnNvbGJlcmdAdW5pbmV0dC5ubzCBnzANBgkqhkiG9w0BAQEFAAOBjQAwgYkCgYEAt8jLoqI1VTlxAZ2axiDIThWcAOXdu8KkVUWaN/SooO9O0QQ7KRUjSGKN9JK65AFRDXQkWPAu4HlnO4noYlFSLnYyDxI66LCr71x4lgFJjqLeAvB/GqBqFfIZ3YK/NrhnUqFwZu63nLrZjcUZxNaPjOOSRSDaXpv1kb5k3jOiSGECAwEAATANBgkqhkiG9w0BAQUFAAOBgQBQYj4cAafWaYfjBU2zi1ElwStIaJ5nyp/s/8B8SAPK2T79McMyccP3wSW13LHkmM1jwKe3ACFXBvqGQN0IbcH49hu0FKhYFM/GPDJcIHFBsiyMBXChpye9vBaTNEBCtU3KjjyG0hRT2mAQ9h+bkPmOvlEo/aH0xR68Z9hw4PF13w=="
  }]
```


### logging a user in
the accounts-ui loggin buttons will not include saml providers, this may be implemented as a future enhancement

in some template
```
<a href="#" class="saml-login" data-provider="openidp">OpenIDP</a>
```

in helper function
```
'click .saml-login': function(event, template){
    event.preventDefault();
    var provider = $(event.target).data('provider');
    Meteor.loginWithSaml({
	    provider:provider
	}, function(error, result){
		//handle errors and result
    });
  }
```

## credits
heavily derived from https://github.com/bergie/passport-saml
