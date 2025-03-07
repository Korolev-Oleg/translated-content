---
title: Notification.renotify
slug: Web/API/Notification/renotify
page-type: web-api-instance-property
tags:
  - API
  - Experimental
  - Notifications
  - Property
  - Reference
  - renotify
browser-compat: api.Notification.renotify
translation_of: Web/API/Notification/renotify
---
{{APIRef("Web Notifications")}}{{AvailableInWorkers}}{{securecontext_header}}

**`renotify`** は {{domxref("Notification")}} インターフェイスの読み取り専用プロパティで、 {{domxref("Notification.Notification","Notification()")}} コンストラクターの `renotify` オプションで指定され、新しい通知が古い通知を置き換えたときにユーザーに通知されるかどうかを指定します。

## 値

論理値です。 `false` が既定値です。 `true` でこの通知がユーザーへ再通知されます。

## 例

次のスニペットは静かな通知を発行するためのものです。単純な `options` オブジェクトが生成され、通知が `Notification()` コンストラクターを使用して発行されます。

```js
const options = {
  body: 'Do you like my Notification?',
  renotify: true
}

const n = new Notification('Test notification', options);

console.log(n.renotify) // should log true
```

## 仕様書

{{Specifications}}

## ブラウザーの互換性

{{Compat}}

## 関連情報

- [通知 API の使用](/ja/docs/Web/API/Notifications_API/Using_the_Notifications_API)
