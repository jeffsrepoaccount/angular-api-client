# jrl-api

This is an AngularJS API Client that provides client-side caching services.

## Dependencies

This project depends on `jrl.utils`.  It also depends on a `jrl.config` module.  As the name implies, it is a configuration module used solely for constructing a single constant.  It should look something like this:

```javascript
(function() {
    'use strict';

    var module = angular.module('jrl.config', []);

    module.constant('jrl.config', {
        app: {
            debug:              true,
            caching_enabled:    true,
            cache_ttl:          60,
            gc_timeout:         15
        }
        api: {
            provider:   'http://my.api.com/api',
            version:    'v1',
        }
    });
})();

```

## Usage

```javascript
angular.module('my-module', ['jrl-api'])
    .controller('MyCtrl', [
        'api',
        function(api) {
            // Build request.  This request will hit the '/resource?number=42&cursor=MTc=' endpoint
            var request = { endpoint: 'resource', params: { cursor: 'MTc=', number: 42 } };

            api.get(request).then(
                function(data) {
                    console.log('data', data.data);
                    console.log('meta', data.meta);
                }
            );
        }
    ])
;
```

## Installation

Install via bower by adding the following to the `dependencies` key in `bower.json`:

```bash
dependencies: {
    "jrl-chat": "git@bitbucket.org:jefflikeschicken/angular-api.git",
}
```
## License

This package is released under the [MIT License](https://opensource.org/licenses/MIT).  For full details refer to LICENSE
