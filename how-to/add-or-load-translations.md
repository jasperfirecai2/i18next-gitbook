# Add or Load Translations

## Add or Load Translations

There are a few options to load translations to your application instrumented by i18next. The most common approach to this adding a so called [**backend plugin**](https://www.i18next.com/overview/plugins-and-utils#backends) to i18next. The range of backends is large from loading translations in the browser using xhr request to loading translations from databases or filesystem in nodejs.

### Add on init

You can add the translations on init

```javascript
import i18next from 'i18next';

i18next
  .init({
    resources: {
      en: {
        namespace1: {
          key: 'hello from namespace 1'
        },
        namespace2: {
          key: 'hello from namespace 2'
        }
      },
      de: {
        namespace1: {
          key: 'hallo von namespace 1'
        },
        namespace2: {
          key: 'hallo von namespace 2'
        }  
      }
    }
  });
```

### Add after init

You can add the translations after init

```javascript
import i18next from 'i18next';

i18next.init({ resources: {} });
i18next.addResourceBundle('en', 'namespace1', {
  key: 'hello from namespace 1'
});
```

There are more options to adding, removing translations...learn more about [resource handling](../overview/api.md).

{% hint style="info" %}
Please make sure to at least pass in an empty resources object on init. Else i18next will try to load translations and give you a warning that you are not using a backend.
{% endhint %}

### Load using a backend plugin

Each [plugin](../principles/plugins.md) comes with a set of on configuration settings like path to load resources from. Those settings are documented on the individual readme file of each repository.

Here is a sample using the [i18next-http-backend](https://github.com/i18next/i18next-http-backend) to load resources from the server.

```javascript
import i18next from 'i18next';
import Backend from 'i18next-http-backend';

i18next
  .use(Backend)
  .init({
    backend: {
      // for all available options read the backend's repository readme file
      loadPath: '/locales/{{lng}}/{{ns}}.json'
    }
  });
```

{% hint style="danger" %}
Having a combination of [defining resources](add-or-load-translations.md#add-on-init) + [having a backend](add-or-load-translations.md#load-using-a-backend-plugin) will not implicitly take one or the other source as fallback resources.  
If you need some fallback behaviour you may use the [i18next-chained-backend](https://github.com/i18next/i18next-chained-backend). A short example can be found [here](https://github.com/i18next/i18next-http-backend/blob/master/example/fallback/app.js).  
With [i18next-chained-backend](https://github.com/i18next/i18next-chained-backend) you can also create some [caching behaviour](caching.md).
{% endhint %}

{% hint style="info" %}
[What's a plugin?](../principles/plugins.md)
{% endhint %}

