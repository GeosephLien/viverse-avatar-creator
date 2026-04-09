# AC2 Host Integration

This package can run standalone or inside a host page `iframe`.

## Embed URL

Use:

```text
https://geosephlien.github.io/viverse-avatar-creator/index.html?embedded=1&uiMode=modal
```

## Init Message

After the iframe sends `ac2:ready`, the host page should send `ac2:init`.

Required payload fields:

- `sessionToken`
- `clientId`
- `userId`
- `exp`

Optional payload fields:

- `uiMode`
- `locale`
- `autoStart`
- `frameStyle`

Example:

```js
frame.contentWindow.postMessage({
  type: "ac2:init",
  protocol: "ac2",
  version: "1.0",
  requestId,
  payload: {
    sessionToken,
    clientId,
    userId,
    exp,
    uiMode: "modal",
    locale: "zh-TW",
    frameStyle: {
      placement: "center",
      panelWidth: 1280,
      panelHeight: 860,
      panelRadius: 24,
      mobilePanelRadius: 18,
      padding: {
        top: 12,
        right: 12,
        bottom: 12,
        left: 12
      },
      mobilePadding: {
        top: 4,
        right: 4,
        bottom: 4,
        left: 4
      }
    }
  }
}, "https://geosephlien.github.io");
```

## Frame Style

`frameStyle` is applied by AC2 itself after `ac2:init`.

Supported fields:

- `placement`: `center`, `left`, `right`, `top`, `bottom`, `fullscreen`
- `panelWidth`
- `panelHeight`
- `panelRadius`
- `mobilePanelRadius`
- `padding.top`
- `padding.right`
- `padding.bottom`
- `padding.left`
- `mobilePadding.top`
- `mobilePadding.right`
- `mobilePadding.bottom`
- `mobilePadding.left`

## AC2 Events

AC2 can post these messages back to the host:

- `ac2:ready`
- `ac2:init-ack`
- `ac2:unity-started`
- `ac2:close-request`
- `ac2:upload-vrm`
- `ac2:avatar-created`
- `ac2:export-ready`
- `ac2:error`
- `ac2:blocked`

## Notes

- `event.origin` should be checked against `https://geosephlien.github.io`
- `targetOrigin` for `postMessage` should also use `https://geosephlien.github.io`
- Do not include `/viverse-avatar-creator` in `event.origin` checks
