# 03. User Role Controlled by Request Parameter

## Vulnerability
Broken Access Control

## Objective
Access the admin panel and delete the user `carlos`.

## What I Did
1. Logged in as `wiener` and sent the `/my-account` request to Burp Repeater.
2. Inspected the request's Cookie header and found an `Admin` cookie set to `false`.
3. Edited the cookie value in Repeater to `Admin=true`.
4. Changed the request path to `/admin` and resent it — the response returned the admin panel HTML.
5. Found the delete link in the response (`/admin/delete?username=carlos`).
6. Changed the request path to `/admin/delete?username=carlos` and resent it.
7. Response confirmed the user was deleted.

## Why It Worked
The application used a separate `Admin` cookie to determine admin privileges, but never validated it server-side against the actual logged-in session. Since the cookie was just plain client-supplied data with no integrity check, it could be freely edited before the request reached the server.

## Remediation
- Do not use client-controlled cookies/parameters to determine authorization.
- Store role/permission data server-side, tied to the authenticated session.
- Re-validate admin status on every privileged request, server-side.

## Key Takeaway
If a client can set a value, a client can fake it. Authorization decisions must never depend on data the browser sends — only on what the server already knows about the authenticated session.