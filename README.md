# browserify-asn1.js

Browserify ASN1.js (https://github.com/indutny/asn1.js/) library and two sets of definitions:
- **asn1.js-rfc5280** https://github.com/indutny/asn1.js/tree/master/rfc/5280
- **@sigex-kz/asn1.js-rfc5652** https://github.com/sigex-kz/asn1.js-rfc5652

## Try

Open https://sigex-kz.github.io/browserify-asn1.js (which loads browserified-asn1.js) and start hacking in web console.

## Install

Grab `bundle/browserified-asn1.js`
or include it from https://sigex-kz.github.io/browserify-asn1.js/bundle/browserified-asn1.js

## Usage

Access
- **ans1.js** via `asn1` global object,
- **asn1.js-rfc5280** via `asn1.rfc5280`,
- **@sigex-kz/asn1.js-rfc5652** via `asn1.rfc5652`,
- **Buffer** (https://github.com/feross/buffer) via `asn1.Buffer`.

```js
const dateForm = new Date().getTime();
const dateTo = dateForm + 1;

const tbsCertContent = {
  version: 'v3',
  serialNumber: dateForm,
  signature: { algorithm: '1.2.840.10045.4.3.2'.split('.') },
  issuer: {
    type: 'rdnSequence',
    value: [
      [
        { type: '2.5.4.3'.split('.'), value: UTF8Str.encode('Test', 'der')},
      ],
    ],
  },
  validity: {
    notBefore: { type: 'utcTime', value: dateForm },
    notAfter: { type: 'utcTime', value: dateTo },
  },
  subject: {
    type: 'rdnSequence',
    value: [
      [
        { type: '2.5.4.3'.split('.'), value: UTF8Str.encode('Test', 'der')},
      ],
    ],
  },
  subjectPublicKeyInfo: {
    algorithm: { algorithm: '1.2.840.10045.2.1'.split('.'), parameters: [6, 8, 42, 134, 72, 206, 61, 3, 1 ,7] },
    subjectPublicKey: {
      unused: 0,
      data: publicKeySpki,
    },
  },
  //extensions,
};

const tbsCertEncoded = asn1.rfc5280.TBSCertificate.encode(tbsCertContent, 'der');
```

## Develop

To run local http server:
```
npm run http-server
```

To build bundle:
```
npm run build
```
