
# Headers

## CORS

[CORS](https://www.youtube.com/watch?v=4KHiSt0oLJ0)

```
Access-Control-Allow-Origin: https://lupusmic.org
Access-Control-Allow-Methods: DELETE
Access-Control-Max-Age: 3600
```

## Browser user safety

[Test](https://securityheaders.com/)
[Safety mesures](https://scotthelme.co.uk/content-security-policy-an-introduction/)

```
Header set Strict-Transport-Security "max-age=31536000; includeSubDomains"
Header set Content-Security-Policy "script-src 'self'"
Header set X-Frame-Options "SAMEORIGIN"
Header set X-Xss-Protection "1; mode=block"
Header set X-Content-Type-Options "nosniff"
Header set Referrer-Policy "no-referrer-when-downgrade"
Header set Permissions-Policy "none"
```
