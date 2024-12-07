---
title: なんかコンソールエラーが出る
date: 2024-12-05 23:46:11.341863700+0900
author:
    name: Ned Rihine
---

ハイドレーションって何…？

    Console Error

    Hydration failed because the server rendered HTML didn't match the client. As a result this tree will be regenerated on the client. This can happen if a SSR-ed Client Component used

    - A server/client branch `if (typeof window !== 'undefined')`.
    - Variable input such as `Date.now()` or `Math.random()` which changes each time it's called.
    - Date formatting in a user's locale which doesn't match the server.
    - External changing data without sending a snapshot of it along with the HTML.
    - Invalid HTML tag nesting.

    It can also happen if the client has a browser extension installed which messes with the HTML before React loaded.

    See more info here: https://nextjs.org/docs/messages/react-hydration-error
