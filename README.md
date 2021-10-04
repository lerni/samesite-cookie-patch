# SilverStripe 4.8 Composer installable patch for adding SameSite Cookie
This module patches according to https://github.com/silverstripe/silverstripe-framework/pull/9920

- https://www.youtube.com/watch?v=Fet6-IiX69E&list=RDCMUCnUYZLuoy1rq1aVMwx4aTzw&index=1
- https://web.dev/samesite-cookies-explained/
- https://blog.chromium.org/2020/01/building-more-private-web-path-towards.html

## How it works
For the `cweagans/composer-patches` to work you need to allow patching and probable also want to set `composer-exit-on-patch-failure` to `true` in your projects `composer.json`.

```json
    ...
    "extra": {
        "enable-patching": true,
        "composer-exit-on-patch-failure": true
    },
    ...
```

As in the PR stated you need to add...
```
// e.g. src/app/_config.php
//...
use SilverStripe\Control\Cookie;
use SilverStripe\Control\Session;
//...

// new configuration property for Cookie
Cookie::config()->set('samesite', 'Lax');

// new configuration property for Session
Session::config()->set('cookie_samesite', 'Lax');
```

## Requirements
* SilverStripe ~4.8 (just tested with that)

## Installation
Use [composer](https://getcomposer.org/):
`composer require lerni/samesite-cookie-patch`
