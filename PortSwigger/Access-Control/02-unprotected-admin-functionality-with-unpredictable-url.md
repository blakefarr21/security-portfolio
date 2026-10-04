# 02. Unprotected Admin Functionality with Unpredictable URL

## Vulnerability
Broken Access Control

## Objective
Delete the user `carlos`.

## What I Did
1. Inspected the application's client-side source code.
2. Found the unpredictable admin panel URL exposed in the JavaScript.
3. Navigated directly to the admin panel.
4. Confirmed the page was accessible without admin authorization.
5. Deleted the user `carlos`.

## Why It Worked
The application relied on making the admin URL difficult to guess instead of properly restricting access to it. The URL was also exposed in client-side code that any user could inspect.

## Remediation
- Require authentication for admin pages.
- Enforce server-side authorization checks.
- Restrict admin actions based on user roles.
- Do not rely on unpredictable URLs for security.
- Avoid exposing sensitive administrative routes in client-side code.

## Key Takeaway
An unpredictable endpoint is not a protected endpoint. Sensitive functionality must enforce authorization even if the URL is difficult to guess.