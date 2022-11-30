---
description: This page describes how to install Apphud JS Script to your own landing page.
---

# Script Install

{% hint style="info" %}
Use this guide only if you have your own landing page.

For landing pages created in Apphud Landing Page Editor, follow [this](landing-page-editor.md) guide.
{% endhint %}

## Facebook

1. **Remove the following lines** from your landing page's Facebook Pixel code because we will add them later with Apphud Pixel JS Code:

```
fbq('init', '{your-pixel-id-goes-here}');
fbq('track', 'PageView');
```

2\. Go to Facebook Conversions API integration page and **copy** the entire JS script and add it to your landing page **after** Facebook Pixel code.&#x20;

![](<../.gitbook/assets/image (5).png>)

3\. Verify Installation. Here is full **example** of scripts in your landing page. You **shoud not** add this script directly to your page, because it contains different identifiers:

```javascript
<!-- Facebook Pixel Code -->
    <script>
      !(function (f, b, e, v, n, t, s) {
        if (f.fbq) return;
        n = f.fbq = function () {
          n.callMethod
            ? n.callMethod.apply(n, arguments)
            : n.queue.push(arguments);
        };
        if (!f._fbq) f._fbq = n;
        n.push = n;
        n.loaded = !0;
        n.version = "2.0";
        n.queue = [];
        t = b.createElement(e);
        t.async = !0;
        t.src = v;
        s = b.getElementsByTagName(e)[0];
        s.parentNode.insertBefore(t, s);
      })(
        window,
        document,
        "script",
        "https://connect.facebook.net/en_US/fbevents.js"
      );
    </script>
    <noscript>
      <img height="1" width="1" style="display: none" src="https://www.facebook.com/tr?id={your-pixel-id-goes-here}&ev=PageView&noscript=1" />
    </noscript>
    <!-- End Facebook Pixel Code -->

    <script type="text/javascript">
  (function (a, p, _p, h, u, d) {
    u = a.aph = function () {
      u.callMethod
        ? u.callMethod.apply(u, arguments)
        : u.queue.push(arguments);
    };
    u.loaded = 1;
    u.version = "1.0";
    u.queue = [];
    (d = p.createElement(_p)),
      (y = p.getElementsByTagName(_p)[0]),
      (d.async = 1),
      (d.src = h),
      y.parentNode.insertBefore(d, y);
  })(window, document, "script", "https://cdn.apphud.com/pixel.js");
  aph("init", "f127c4c1-f15e-4b19-9dad-12356e8f6ef9");
  aph("fb", "{your-pixel-id-goes-here}");
</script>
```

## TikTok

1.  **Remove the following lines** from your landing page's TikTok Pixel code because we will add them later with Apphud Pixel JS Code:

    ```
    ttq.load('YOUR-PIXEL-ID');
    ttq.page();
    ```
2. Go to TikTok Events API integration page and **copy** the entire JS script and add it to your landing page **after** TikTok Pixel code.&#x20;

![](<../.gitbook/assets/image (3).png>)

3\. Verify Installation. Here is full **example** of scripts in your landing page. You **shoud not** add this script directly to your page, because it contains different identifiers:

```javascript
<script>
!function (w, d, t) {
  w.TiktokAnalyticsObject=t;var ttq=w[t]=w[t]||[];ttq.methods=["page","track","identify","instances","debug","on","off","once","ready","alias","group","enableCookie","disableCookie"],ttq.setAndDefer=function(t,e){t[e]=function(){t.push([e].concat(Array.prototype.slice.call(arguments,0)))}};for(var i=0;i<ttq.methods.length;i++)ttq.setAndDefer(ttq,ttq.methods[i]);ttq.instance=function(t){for(var e=ttq._i[t]||[],n=0;n<ttq.methods.length;n++)ttq.setAndDefer(e,ttq.methods[n]);return e},ttq.load=function(e,n){var i="https://analytics.tiktok.com/i18n/pixel/events.js";ttq._i=ttq._i||{},ttq._i[e]=[],ttq._i[e]._u=i,ttq._t=ttq._t||{},ttq._t[e]=+new Date,ttq._o=ttq._o||{},ttq._o[e]=n||{};var o=document.createElement("script");o.type="text/javascript",o.async=!0,o.src=i+"?sdkid="+e+"&lib="+t;var a=document.getElementsByTagName("script")[0];a.parentNode.insertBefore(o,a)};
}(window, document, 'ttq');
</script>

<script type="text/javascript">
  (function (a, p, _p, h, u, d) {
    u = a.aph = function () {
      u.callMethod
        ? u.callMethod.apply(u, arguments)
        : u.queue.push(arguments);
    };
    u.loaded = 1;
    u.version = "1.0";
    u.queue = [];
    (d = p.createElement(_p)),
      (y = p.getElementsByTagName(_p)[0]),
      (d.async = 1),
      (d.src = h),
      y.parentNode.insertBefore(d, y);
  })(window, document, "script", "https://static.apphud.com/pixel.js");
  aph("init", "b1d1b4fa-0627-4355-0000-d823789f97a6");
  aph("tt", "00BJVJ001SKIVFQVKOP0");
</script>

```

