# <a name="cli-browser-preview"></a>CLI Browser Preview

## <a name="cli-bp-overview"></a>Overview

The Spck CLI includes a browser proxy that lets you open and interact with your local development server directly from the Spck Editor mobile app. When you tap **Preview** in the editor, the app opens a browser session that tunnels through the CLI connection to your project's dev server.

## <a name="cli-bp-how-it-works"></a>How It Works

The CLI acts as an HTTP proxy between the mobile app and your local dev server. Requests from the in-app browser are forwarded over the secure CLI relay connection to the CLI process, which makes the actual HTTP request to `localhost` and returns the response.

This means your dev server never needs to be exposed to the public internet — it only needs to be reachable from the machine running the CLI.

## <a name="cli-bp-config"></a>Configuration

Browser proxy is enabled by default. To disable it:

```json
{
  "browserProxy": {
    "enabled": false
  }
}
```

## <a name="cli-bp-ios-limitations"></a>iOS Limitations

iOS applies strict browser security policies that affect the in-app preview experience. Several features that work on Android or desktop are unavailable on iOS.

### Service Workers Not Supported

iOS does not allow service workers to be registered in web views that are not the top-level browser. Because the Spck Editor preview runs in a `WKWebView`, service worker registration is blocked. Apps that depend on a service worker for caching, offline support, or push notifications will not function correctly in the preview on iOS.

**Workaround**: Test service worker behavior in Safari on iOS instead of inside the app preview.

### WebSockets Not Supported

The CLI browser proxy operates over HTTP. The iOS `WKWebView` security model does not permit upgrading proxied connections to the WebSocket protocol (`ws://` / `wss://`). WebSocket connections initiated from a proxied page will fail to establish.

This affects:
- Hot Module Replacement (HMR) in bundlers such as Vite, webpack-dev-server, and Parcel
- Live reload mechanisms
- Any application feature that uses `new WebSocket(...)` directly

**Workaround**: Disable HMR or live reload when previewing on iOS. For Vite, add `server.hmr: false` while testing on iOS. For application-level WebSockets, use long-polling as a fallback.

### Cross-Domain iframe Restriction

iOS enforces strict cross-origin isolation for iframes. Because the proxy serves your app through the CLI relay domain rather than `localhost`, relative resource paths resolve correctly but absolute references to `localhost` are blocked by the same-origin policy.

To work around this, the CLI re-maps the app to a path within the same relay domain so the iframe origin matches the parent page. This means:

- **Relative paths work correctly** — assets, API calls, and page navigations using relative URLs (e.g. `./assets/logo.png`, `fetch('/api/data')`) are resolved through the proxy and function as expected.
- **Absolute `localhost` references are blocked** — hardcoded URLs such as `http://localhost:3000/api` or `ws://localhost:3000` cannot be reached from within the proxy context on iOS.

**Workaround**: Use relative paths for all resource references in pages that will be previewed on iOS. Avoid hardcoding `localhost` or any absolute origin in HTML, JavaScript, or CSS that is served to the browser.

```html
<!-- Works on iOS preview -->
<script src="/bundle.js"></script>
<img src="./images/logo.png" />

<!-- Blocked on iOS preview -->
<script src="http://localhost:3000/bundle.js"></script>
```

## <a name="cli-bp-android"></a>Android

Browser preview on Android does not have the above restrictions. Service workers, WebSockets, and absolute `localhost` URLs all work as expected inside the in-app browser on Android.

&nbsp;

&nbsp;
