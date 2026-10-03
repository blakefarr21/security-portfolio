# 01. Unprotected Admin Functionality

## Vulnerability
Broken Access Control

## Objective
Delete the user `carlos`.

## What I Did
1. Opened `/robots.txt`.
2. Found the hidden admin path.
3. Navigated directly to the admin panel.
4. Confirmed the page was accessible without admin authentication.
5. Deleted the user `carlos`.

## Why It Worked
The application relied on hiding the admin URL instead of properly restricting access to it.

## Remediation
- Require authentication for admin pages.
- Enforce server-side authorization checks.
- Restrict admin actions based on user roles.
- Do not rely on hidden URLs for security.

## Key Takeaway
A hidden endpoint is not a protected endpoint. Sensitive functionality must enforce authorization regardless of whether the URL is publicly linked.