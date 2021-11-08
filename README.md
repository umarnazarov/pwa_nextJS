## PWA Proektda Ishlatish🤠
Shu erda siz PWA tez va osson web saytingizda ishlatishni o'rganasiz 😃

## PWA bizga nima beradi ❓

Pwa - Progrssive Web App web-saytimizni juda tez ishlatip beradi cache yordamida. Qachonki user saytimizga kirganida PWA ishga tushadi (agar ishlatse), PWA serverdan kevotkan hamma ma'lumotlani (HTML, CSS, JS, ...) browserimizga cache qiladi va bu yordamida user kengi safar web ilovamizga kirganida malumotlani serverdan mas balki browserdagi cache ni oladi va bu sayt juda tez oqiydi degani. PWA hamma browser da ishlidi va sayt offline da ham ishlaydi.

## PWA Webda qollash 💪

PWA install qilish kerak

```bash
npm i next-pwa # npm
# yoki
yarn add next-pwa # yarn
```
## Manifest.json yaratish 🚀

Manifest ni tez yaratish uchun [Simicart](https://www.simicart.com/manifest-generator.html/) saytini shlatishingiz mumkun. Siz saytingiz haqida malumotlar bilan toldiring va standalone optiyasini tanlshni unutmang. 

![image](https://user-images.githubusercontent.com/83394723/140694656-75d46c8d-504b-4b1d-8842-400c7f7daee0.png)

To'ldirip bo'lganingizdan so'ng zip fayldagi hamma faylarni `/public` pobkaga joylang va `manifest.webmanifest` ni `webmanifest.json` ga o'zgartiring.
Shundan so'ng `public` pobkasi shunga oxshgan bo'lishi kerak

![image](https://user-images.githubusercontent.com/83394723/140695354-5811a704-5278-4034-82d8-6f6381e24e5d.png)

## `_document.js` ni yaratish 📄

`_document.js` ni `/pages` pobkada yarating va shu kodni yozing:

```bash
import Document, { Html, Head, Main, NextScript } from "next/document";

class MyDocument extends Document {
  render() {
    return (
      <Html>
        <Head>
          <link rel="manifest" href="/manifest.json" />
          <link rel="apple-touch-icon" href="/icon.png"></link>
          <meta name="theme-color" content="#fff" />
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    );
  }
}

export default MyDocument;
```
Agar sizda `_document.js` bo'lsa shu kodni: 
```bash
<link rel="manifest" href="/manifest.json" />
``` 
`<Head></Head>` ni ichiga yozing.

## PWA ni Next configda sozlash 🥣

`next.config.js` faylga shu kodni yozing: 
```bash
const withPWA = require("next-pwa");

module.exports = withPWA({
  pwa: {
    dest: "public",
    register: true,
    skipWaiting: true,
  },
});
```
Agar boshqa configlaringiz bo'lsa ularni pwa object dan keyin yozsangis bo'ladi: 

```bash
const withPWA = require("next-pwa");

module.exports = withPWA({
  pwa: {
    dest: "public",
    register: true,
    skipWaiting: true,
  },
  boshqaConfig: ...
});
```

`npm run build` ni terminalga yozing, undan so'ng `npm run start` 

## Vanihoyat PWA endi sizning web-saytingizda!!!🎉

==========================================

Agar sezgan bo'lsangiz `/public` pobkaga bir nechta faylar qoshildi:

![image](https://user-images.githubusercontent.com/83394723/140710937-30d16a2c-d1c4-40e1-9202-0bf69d1def91.png)

Ularni biza gitignore ga qoship qoyishimiz kerak chunki ular ozgaruvchan:

```bash
# PWA files
**/public/sw.js
**/public/workbox-*.js
**/public/worker-*.js
**/public/sw.js.map
**/public/workbox-*.js.map
**/public/worker-*.js.map
```

PWA ni biza development da ochirip qoysak yaxshi chunki ko'p console.log chiqaradi: 

```bash 
module.exports = withPWA({
  pwa: {
    dest: "public",
    register: true,
    skipWaiting: true,
    disable: process.env.NODE_ENV === "development",
  },
});
```
