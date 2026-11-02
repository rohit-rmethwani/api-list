# Bucketlist Dream of the Day

A free, keyless JSON API returning one daily experience with an image and source URL. The selection follows the Europe/Amsterdam calendar day; it is not a fresh random choice on each request.

## Request

`GET https://bucketlist.nl/api/droom-van-de-dag`

The default response uses Dutch and Netherlands scope. The published specification also documents optional language (`nl`, `en`, `de`, `fr`, `es`), scope (`nederland`, `wereld`) and theme parameters.

## JavaScript example (Node.js 18+)

No package installation, account, API key or purchase is required for this example.

```javascript
const response = await fetch('https://bucketlist.nl/api/droom-van-de-dag', {
  signal: AbortSignal.timeout(15000),
  redirect: 'error',
  headers: { 'User-Agent': 'Bucketlist.nl public API example (+https://bucketlist.nl/contact)' },
});
if (!response.ok) throw new Error('HTTP ' + response.status);
const data = await response.json();
console.log(JSON.stringify({
  status: response.status, cors: response.headers.get('access-control-allow-origin'),
  date: data.date, language: data.language, scope: data.scope,
  title: data.dream.title, imageUrl: data.dream.image.url, url: data.dream.canonicalUrl,
}));
```

The response includes `date`, `scope`, `language` and a `dream` object with `title`, `image` and `canonicalUrl`. The example prints the response fields and observed CORS header; handle request failures in your application.

## Documentation and usage

- [OpenAPI specification](https://bucketlist.nl/brand/droom-van-de-dag.openapi.json)
- [Provider documentation](https://bucketlist.nl/samenwerken)

Free access does not establish an image redistribution licence or blanket commercial-use permission. Consult the provider terms before reusing content. No numerical quota or uptime guarantee is asserted. Some linked experience pages include optional affiliate booking links.
