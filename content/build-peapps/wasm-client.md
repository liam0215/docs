---
title: "Webassembly client"
weight: 45
description: "How to integrate the Nym webassembly client into your own applications to enable strong privacy for your users"
---

The Nym webassembly client allows any webassembly-capable runtime to build and send Sphinx packets to the Nym network. 

You can install [@nymproject/nym-client-wasm](https://www.npmjs.com/package/@nymproject/nym-client-wasm) from NPM from its package page, or `npm i @nymproject/nym-client-wasm`. 

The `nym-client-wasm` package allows easy usage of Sphinx from (a) mobile apps and (b) client-side apps (e.g. Electron or similar). Things like browser extensions should also work fine, although we haven't tried to build one yet.

As the [quickstart example](/docs/quickstart/send-some-packets) shows, it's possible to deliver web apps that build and send Sphinx packets in a browser window. However, note that all the normal constraints of [browser-based key storage](https://pomcor.com/2017/06/02/keys-in-browser/) and same-origin rules (which are there for good reason) make it difficult to structure pure webapps apps securely. We are still assessing what can be done here, if anything.

### SURBs

Anonymous replies using surbs don't yet exist in the WebAssembly client, but should be available in the next release (0.8.0).

### JSON

Sending JSON is fairly simple. If you're playing with the quickstart wasm example app, just stick it into the message box and send it (or send it programmatically if you're writing an application of your own).

### Think about what you're sending!

{{% notice warning %}}
Think about what information your app sends. That goes for whatever you put into your Sphinx packet messages as well as what your app's environment may leak.
{{% /notice %}}

Whenever you write client peaps using HTML/JavaScript, we recommend that you do not load external resources from CDNs. Webapp developers do this all the time, to save load time for common resources, or just for convenience. But when you're writing privacy apps it's better not to make these kinds of requests. Pack everything locally.

If you use only local resources within your Electron app or your browser extensions, explicitly encoding request data in a Sphinx packet does protect you from the normal leakage that gets sent in a browser HTTP request. [There's a lot of stuff that leaks when you make an HTTP request from a browser window](https://panopticlick.eff.org/).

This is a big advantage of Nym: as an application developer, when you pack messages into Sphinx packets, you're only sending info that you determine secure to send (whitelist), rather than sending a whole browser environment by default. The security model ends up being pretty simple.