# AI App Authorization Security Checklist

A practical pre-launch audit for vibe-coded apps.

## The core rule

**Authentication** answers "Who are you?"\
**Authorization** answers "What are you allowed to access or change?"

A logged-in user must not be able to access another user's records by
changing an ID in a URL, request body, or API call.

## 1. Audit every endpoint

-   [ ] List every API route, server action, RPC, and data-access
    function.
-   [ ] Mark which routes require login and which are intentionally
    public.
-   [ ] For every route that reads, creates, updates, downloads, or
    deletes data, identify the resource owner and authorization rule.
-   [ ] Check alternate paths too: exports, file downloads, search, bulk
    actions, nested routes, and admin endpoints.

## 2. Enforce ownership on the server

-   [ ] Verify authorization on the server for every request; never rely
    on hidden buttons or frontend checks.
-   [ ] Before returning or changing a record, confirm the authenticated
    user is allowed to access that exact record.
-   [ ] Scope database queries to the current user or authorized tenant
    where possible (for example, query by both record ID and owner ID).
-   [ ] Do not trust user-supplied `user_id`, `owner_id`, `role`,
    `tenant_id`, or `account_id` from request parameters or request
    bodies.
-   [ ] Apply the same checks to reads, updates, deletes, uploads,
    exports, and nested resources.

## 3. Check roles and tenant boundaries

-   [ ] Verify role-based permissions server-side (user, manager, admin,
    etc.).
-   [ ] Ensure tenant or organization boundaries are enforced on every
    relevant query.
-   [ ] Prevent users from granting themselves admin roles or changing
    ownership fields.
-   [ ] Use explicit, least-privilege permissions; deny access by
    default when authorization is unclear.

## 4. Test with two accounts

-   [ ] Create User A and User B, each with separate private records.
-   [ ] Sign in as User A and access User A's records normally; confirm
    expected actions work.
-   [ ] While signed in as User A, replace User A's record ID with User
    B's ID in the URL and API request.
-   [ ] Try reading, editing, deleting, exporting, and downloading User
    B's records.
-   [ ] Repeat with IDs in request bodies, query parameters, nested
    routes, and file URLs.
-   [ ] Expected result: no unauthorized data is returned or changed.
    Use a consistent `403` or `404` response according to your app's
    policy.

## 5. Check sessions and sensitive actions

-   [ ] Confirm every protected endpoint validates the current
    session/token and does not accept expired or invalid credentials.
-   [ ] Re-check permissions on sensitive actions; do not assume a
    previous page check is enough.
-   [ ] Ensure logs and error messages do not expose private records,
    tokens, or secrets.
-   [ ] Check that cached responses cannot be served to the wrong user.

## 6. Fix and retest

-   [ ] Fix the server-side authorization rule---not just the UI.
-   [ ] Add automated regression tests for cross-user and cross-tenant
    access.
-   [ ] Re-run the tests after changes and before every release.
-   [ ] Review any failed test before launch; do not treat a hidden
    button as a security fix.

## Copy-paste prompt for your AI coding agent

``` text
Act as a security engineer. Audit this application for broken access control and insecure direct object references (IDOR). Inventory every API endpoint, server action, RPC, and data-access path that reads or changes data. For each one, identify the authenticated principal, resource owner, tenant boundary, and required permission. Enforce authorization server-side for every read, create, update, delete, upload, download, export, and nested-resource operation. Do not trust client-supplied owner IDs, roles, or tenant IDs. Add tests using two separate accounts that attempt cross-user and cross-tenant access by changing IDs in URLs, query parameters, request bodies, and file references. Verify unauthorized requests return no protected data and make no changes. Report findings by severity, show the relevant code and tests, implement fixes, and re-run the tests. Do not claim the app is secure unless the tests actually pass. Work only within this authorized codebase and test environment.
```

## Important note

This checklist reduces common authorization risks but is not a guarantee
of security. Test only systems and data you own or have explicit
permission to assess. Have a qualified reviewer assess high-risk
applications before launch.
