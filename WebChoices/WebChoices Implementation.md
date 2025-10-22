# Implementation Instructions for DAA Participants to WebChoices

Implementation instructions for DAA Participants from the “[the
choice page](http://www.aboutads.info/choices/)” to WebChoices.

WebChoices allows for the transparent and reliable setting of opt-out
choice from data collection and use for IBA across major browsers.

The new feature set in WebChoices is particularly relevant when
companies use non-third party cookies (First-Party Cookies) or
cookie-less[^1]/non-cookie technologies for interest-based
advertising (“IBA”) (collectively “non-cookie technologies”).
Companies using non-cookie tech should integrate with WebChoices 2.0
as it makes setting opt outs more transparent and allows opt outs to
be set in more cases than in the current version.

If your company does NOT engage in third-party IBA using non-cookie
technologies, then you do not need to manually integrate with this
tool, as migration from the current choice page to WebChoices will
occur automatically. However, you may need to whitelist the
subdomains - <u>optout.aboutads.info and dev.aboutads.info for testing
purposes</u>.

Links to access the WebChoices Tool should point to [optout.aboutads.info](https://optout.aboutads.info).

## WebChoices

Centralized Consumer Opt-Out Platform

### PUBLISHED/UPDATED October 2025

This document describes how the opt-out platform works and how to
integrate your company’s opt-out infrastructure with the WebChoices
tool. This opt-out platform is backwards compatible with the DAA’s old
choice page.

### Onboarding and Management \| Cookies and Extension Opt Outs

Companies integrating new or updated endpoints can use
dev.aboutads.info to test their cookie-based opt outs alongside
extension-based opt outs. The development site will include a link to
the Protect My Choices extension, to which the site can write.
Companies can then install the extension to verify their ability to
read and decode the AdChoices Signal.

The WebChoices tool resides at: [optout.aboutads.info](https://optout.aboutads.info)

Some links to access the WebChoices Tool point to
[<u>www.aboutads.info/choices</u>](http://www.aboutads.info/choices),
the old URL for the DAA Choice Page. DAA will redirect to this sub
domain.

## Contents

This integration guide contains five sections:

1.  **[CONSUMER OPT-OUT EXPERIENCE](#consumer-opt-out-experience)**
An overview of the new opt-out platform additions

2.  **[WEBCHOICES DEVELOPMENT AND PRODUCTION SITES](#webchoices-development-and-production-sites)**
Company information management

3.  **[ONBOARDING PROCESS](#onboarding-process)**
Instructions for activating your organization to the new opt-out tool

4.  **[CONSUMER OPT-OUT INTEGRATION SPECIFICATION](#consumer-opt-out-integration-specification)**
- New browser status reporting
- General Requirements
- Status and Token
- Opt Out

5.  **[ESTABLISHING A FIRST PARTY TRUST RELATIONSHIP](#establishing-a-first-party-trust-relationship)**
- How to set an opt-out cookie in the “From Visited” scenario when
browsers block third-party cookies with the new opt-out tool
- Request
- Response
- Guidelines for using a Trust Cookie (session cookie)
- Guidelines for response

## I. CONSUMER OPT-OUT EXPERIENCE

The purpose of the WebChoices opt-out tool is to provide consumers with a destination to:

1.  Identify a list of companies who have committed to conducting
    responsible advertising practices in alignment with the DAA’s
    Principles;

2.  Receive a detailed report of which companies engage in
    Interest-Based Advertising on a consumer’s browser; and,

3.  Provide consumers the ability to opt out of collection and use of
    data for Interest-Based Advertising from one, several, or all of the
    companies listed on the WebChoices tool.

## II. WEBCHOICES DEVELOPMENT AND PRODUCTION SITES

This section provides instructions on how a company can access the
WebChoices development site to test integrations before deploying them
to consumers.

1.  **Access**. WebChoices is accessible at the following URLs:
- Staging & Onboarding: <https://dev.aboutads.info>
- Production: <https://optout.aboutads.info/>

2.  **Credentials**. The staging environment is essentially a sandbox
    where companies’ opt-out functionality can be tested without being
    released to the public.

## III. ONBOARDING PROCESS

This section provides information on how companies can onboard their
organization’s information and endpoints to the WebChoices opt-out
platform.

- **Step 1 - Email Contact**: Each company currently listed on the
    current choice page will receive an email invitation to start the
    onboarding process. Please ensure that your designated point of
    contact (“POC”) is aware of this email and has the necessary rights
    to start the onboarding process. While many companies use technical
    staff for this process, it is not required.

- **Step 2 - Respond to Email**: Your organization’s POC will receive
    an email from DAA to the email address you have provided. To update
    your contact email, please inform DAA staff directly.

- **Step 3**: Provide DAA with the following:

    - A URL to your organization’s website;
    - A URL to your organization’s privacy policy or privacy notice;
    - A brief description of your company (this will appear on the opt-out page);
    - A logo of your company (this will appear on the opt-out page);
    - A designation of whether you use cookie technologies for IBA;
    - A designation of whether you use non-cookie technologies for IBA;
    - A designation of whether you are able to read the AdChoices Signal in the Protect My Choices extension.;
    - The (non-unique) value of your opt-out cookie; and,
    - The URL where your Advertising ID rotation functionality exists.
        Companies who elect to extend consumer opt outs to both IBA
        **and** non-cookie technology Reporting activities are not
        required to provide a rotation mechanism.

- **Step 6**: After providing the necessary information, we will add
    your endpoint to the WebChoices onboarding site dev.aboutads.info
    where you and DAA can then test and review your endpoint. DAA staff
    will notify you of approval or with requests to repair any errors,
    if discovered.

- **Step 7**: After DAA review of your submission, you will receive a
    confirmation email indicating that your endpoint has been approved
    and activated. DAA staff will then migrate the change to the
    production environment and your endpoint will be available to
    consumers.

## IV. CONSUMER OPT-OUT INTEGRATION SPECIFICATION

This section describes what is required to implement a WebChoices
Opt-Out Service Endpoint capable of integrating with the cookie-based
WebChoices consumer opt-out tool.

### A. General Requirements

#### 1. Browser Compatibility

- No technologies shall be utilized in your implementation of an
    endpoint that will render it unable to function reliably and quickly
    on all major browser and operating system combinations on desktop
    and mobile devices which support third-party cookies.

#### 2. Opt-Out Cookies

-  Companies shall use generic values for their company's opt-out
    cookie value.
-  Opt-out cookies that are generated by a company endpoint shall have
    a minimum lifespan of 5 years and shall be renewed for at least
    another 5 years upon each subsequent opt-out request received. When
    calculating the 5-year lifespan, account for a possible two extra
    days to account for leap years.
- Cookies not required to opt out a user shall never be set by a
    company’s WebChoices endpoint. Any cookies that are necessary for a
    company’s endpoints to function (e.g., tokens) shall not persist
    past the current browser session.
- The WebChoices tool may give companies an enhanced trust
    relationship when “Action ID=5” is used to set a session cookie
    prior to setting an IBA opt-out cookie. After setting this opt-out
    cookie, the WebChoices tool is made available for companies to
    reliably set opt-out choices in third-party cookie blocking
    environments. Consistent with DAA Principles, any use of technology
    (including cookies) may still be permissible so long as the data
    cannot be collected or used for IBA after an opt-out choice. Violating 
    this requirement may result in a breach of the terms under which this tool 
    is offered to companies.
- Companies may not exploit the trusted relationship established via
    WebChoices tool. But companies may leverage their existing 1st party
    relationships or non-cookie technology for non-IBA purposes after
    opt out.
- Some companies may have multiple endpoints, each with a different
    opt-out cookie value. Please contact DAA staff if you have multiple
    opt-out cookies with differing values.
- Upon a successful opt out, all cookies related to IBA activities
    shall be expired, except those necessary to maintain the opt-out
    status of the consumer.
- Non-cookie based IBA technologies, such as IBA made possible by a
    statistical identifier (Stat ID) or HTML5 local storage, must honor
    the presence of an opt-out cookie being set, regardless of
    non-cookie technology used.

#### 3. Use of Optional Anti-CSRF Tokens

- Companies are allowed (but not required) to exchange anti-CSRF
    tokens in advance of setting an opt-out cookie as part of this
    specification for a consumer opt-out process.
- Companies seeking the additional transactions that allow the
    anti-CSRF token exchange may be asked to meet elevated performance
    SLA's (such as endpoint response times) for their endpoints to
    ensure that the company’s additional transactions do not negatively
    impact usability for consumers.
- If a request to an endpoint fails due to Anti-CSRF Token validation,
    the endpoint is required to return the appropriate error code back
    to the requestor and at no point shall it return rendered content or
    xml that is visible within a consumer's browser window.

#### 4. Opt Out Failures

- As is the case with the current choice page, all failures/errors
    must return a result back for processing, regardless of reason. Any
    failure to do so may result in your endpoint being deactivated
    automatically to preserve a fast, accurate and predictable consumer
    experience. Companies will use reasonable efforts to cure issues
    raised by DAA. Failure to address issue within a reasonable may
    result in, at the discretion of DAA, delisting a company.

#### 5. Recommendations

- Use some variation of ‘opt-out’ as the name of your company's
    opt-out cookie. This helps consumers identify which cookies are
    opt-out cookies.
- Use Request Referrers to limit access to a company’s endpoint, but
    each one must permit requests from allowable subdomains including
    dev, integrate, qa, staging, www and optout. Overly restrictive
    referrer validation logic within a company’s endpoint can interfere
    with critical quality assurance processes when onboarding new
    companies or when releasing new features to the opt-out tool.

#### 6. Performance

- Maintaining fast endpoints is becoming increasingly important with
    the implementation of additional technologies. There will be
    increased focus to ensure company endpoints are responding quickly
    to ensure a fast opt-out experience for users.
- The recommended approach for those companies that are not using
    non-cookie technologies is to use a HTTP 302 redirects whenever
    possible. Endpoints that make use of JavaScript for browser
    redirection must particularly focus on browser compatibility and
    rapid response times. Each company endpoint has a limited amount of
    time to deliver a response and JavaScript (or chained redirects) can
    add undesirable processing time and possibly even result in a
    failure being reported to the consumer due to a company’s endpoint
    not meeting a reasonable allowable transaction response time.

### B. Status (Legacy Specification) and Token

#### Request

| **Attribute** | **Description / value** |
|----|----|
| Referer | http://\<dev \| staging \| qa \| integrate \| www \| optout\>.aboutads.info/\* |
| Accept | text/html,application/xhtml+xml |

*<u>Sample Requests URLs:</u>*

`http://your.domain/with/path/to/endpoint`
`?action_id=3`
`&participant_id=10`
`&rd=http%3A%2F%2Fwww.aboutads.info`
`&nocache=223442`

| **Field** | **Data Type** | **Description** |
|----|:--:|----|
| action_id | integer | Value “3” indicates a status request and token if applicable |
| participant_id | string | Participant Identifier for the Opt-out tool to correlate your endpoint with operations. Value is subject to change without notice. |
| rd | string | hostname and protocol |
| nocache | string | Ignore: cache buster |

#### Response (Legacy Specification)

This is the existing specification and can be used by companies that
are utilizing ONLY cookie identifiers for IBA (i.e. companies NOT
employing non-cookie tech).

<table>
<colgroup>
<col style="width: 19%" />
<col style="width: 15%" />
<col style="width: 65%" />
</colgroup>
<thead>
<tr>
<th><strong>Field</strong></th>
<th style="text-align: center;"><strong>Data Type</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>rd</td>
<td style="text-align: center;">string</td>
<td><strong>rd</strong> value from request</td>
</tr>
<tr>
<td>participant_id</td>
<td style="text-align: center;">integer</td>
<td><strong>participant_id</strong> value from request</td>
</tr>
<tr>
<td>status</td>
<td style="text-align: center;">integer</td>
<td><p>1 = No IBA cookie(s) from Participant on the browser.</p>
<p>2 = IBA cookie(s) from Participant present on the browser.</p>
<p>3 = Opt-out cookie is present on the browser.</p></td>
</tr>
<tr>
<td>token</td>
<td style="text-align: center;">string</td>
<td>optional Anti-CSRF string, Must be valid ASCII characters allowed in
a URL.</td>
</tr>
</tbody>
</table>

*<u>Response URL:</u>*

\<**rd**\>/token/\<**participant_id**\>/\<**status**\>/\<**token**\>

<u>Example:</u>
`http://www.aboutads.info/token/123/1/magic_string`

#### Response (New Specification)

This response is required for participants. Companies utilizing
non-cookie technologies <u>are required</u> to provide accurate
status as specified below.

<table>
<colgroup>
<col style="width: 18%" />
<col style="width: 16%" />
<col style="width: 65%" />
</colgroup>
<thead>
<tr>
<th><strong>Field</strong></th>
<th style="text-align: center;"><strong>Data Type</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>rd</td>
<td style="text-align: center;">string</td>
<td><strong>rd</strong> value from request</td>
</tr>
<tr>
<td>participant_id</td>
<td style="text-align: center;">integer</td>
<td><strong>participant_id</strong> value from request</td>
</tr>
<tr>
<td>cookie-status</td>
<td style="text-align: center;">integer</td>
<td><p>0 = Not Applicable - Cookie Technologies are not in use</p>
<p>1 = No IBA cookie(s) from Participant on the browser</p>
<p>2 = IBA cookie(s) from Participant present on the browser.</p>
<p>3 = Opt-out cookie is present on the browser.</p></td>
</tr>
<tr>
<td>other-status</td>
<td style="text-align: center;">integer</td>
<td><p>0 = Not Applicable - Non-Cookie Technologies are not in use</p>
<p>1 = No Non-Cookie IBA Identifier from Participant present for the
browser</p>
<p>2 = Non-Cookie IBA Identifier from Participant present for the
browser.</p>
<p>3 = Non-Cookie Opt-out from Participant present for the
browser.</p></td>
</tr>
<tr>
<td>token</td>
<td style="text-align: center;">string</td>
<td>optional Anti-CSRF string, Must be valid ASCII characters allowed in
a URL.</td>
</tr>
</tbody>
</table>

<u>Response URL:</u>

\<rd\>/token/\<participant_id\>/**\<cookie-status\>-\<other-status\>**/\<token\>

Example for company using non-cookie technology:
`http://www.aboutads.info/token/123/1-1/csrftoken`

Example for company using only cookie technology:
`http://www.aboutads.info/token/123/1**-0**/csrftoken`

### C. Opt Out

Opt out a consumer from the collection and use of data for IBA by
setting an “opt-out” cookie on the consumer’s browser. **This action
reports success or failure and must be based on the actual presence of
the opt-out cookie in the consumer’s browser**. Verification of the
presence of the “opt-out” cookie is usually accomplished by
redirecting to a verification page or script before redirecting the
result signal back to the WebChoices tool. If utilizing server-side
non-cookie technologies (e.g., statistical identifiers), the opt out
must also be persisted on the company’s server.

### Request

<table>
<colgroup>
<col style="width: 15%" />
<col style="width: 84%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"><strong>Attribute</strong></th>
<th>
<p><strong>Description / value</strong></p>
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;">Referer</td>
<td>http://&lt;dev | staging | qa | integrate | www |
optout&gt;.aboutads.info/*</td>
</tr>
<tr>
<td style="text-align: center;">Accept</td>
<td>text/html,application/xhtml+xml</td>
</tr>
</tbody>
</table>

*<u>Sample Requests URL:</u>*

`http://your.domain/endpoint`
`?action_id=4&participant_id=10`
`&rd=http://www.aboutads.info`
`&token=magic_value&nocache=223442`

| **Field** | **Data Type** | **Description** |
|----|:--:|----|
| action_id | integer | Value “4” indicates an opt out request |
| participant_id | string | Participant Identifier for the Opt-out tool to correlate your endpoint with operations. Value is subject to change without notice. |
| rd | string | hostname and protocol |
| token | string | optional Anti-CSRF string if returned during the status check |
| nocache | string | Ignore: cache buster |

### Response (Legacy Specification)

This is the existing specification and can continue to be used by
companies that are utilizing only cookie-based identifiers for IBA
purposes.

<table>
<colgroup>
<col style="width: 16%" />
<col style="width: 14%" />
<col style="width: 69%" />
</colgroup>
<thead>
<tr>
<th><strong>Field</strong></th>
<th style="text-align: center;"><strong>Data Type</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>rd</td>
<td style="text-align: center;">string</td>
<td><strong>rd</strong> value from request</td>
</tr>
<tr>
<td>action_id</td>
<td style="text-align: center;">integer</td>
<td><strong>action_id</strong> value from request</td>
</tr>
<tr>
<td>participant_id</td>
<td style="text-align: center;">string</td>
<td><strong>participant_id</strong> value from request</td>
</tr>
<tr>
<td>result_id</td>
<td style="text-align: center;">integer</td>
<td><p>1 = <strong>Success:</strong> after an opt out attempt, the opt
out cookie is present on the user’s browser</p>
<p>2 = <strong>Failure:</strong> after an opt out attempt, the cookie is
not present on the user’s browser</p>
<p>3 = <strong>Failure:</strong> anti-CSRF token mismatch [4..] =
Reserved for future use</p></td>
</tr>
<tr>
<td>message</td>
<td style="text-align: center;">string</td>
<td>optional simple ascii text string fully URL compliant.</td>
</tr>
</tbody>
</table>

*<u>Response URL:</u>*

\<**rd**\>/finish/\<**participant_id**\>/\<**action_id**\>/\<**result_id**\>/\<**message**\>

<u>Example:</u>
`http://www.aboutads.info/finish/123/4/1/simple_string`

### Response (New Specification)

This response is required is for participants. Companies utilizing
non-cookie technologies are required to provide accurate opt-out
result as specified below.

<table>
<colgroup>
<col style="width: 14%" />
<col style="width: 11%" />
<col style="width: 73%" />
</colgroup>
<thead>
<tr>
<th><strong>Field</strong></th>
<th style="text-align: center;"><strong>Data Type</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>rd</td>
<td style="text-align: center;">string</td>
<td><strong>rd</strong> value from request</td>
</tr>
<tr>
<td>action_id</td>
<td style="text-align: center;">integer</td>
<td><strong>action_id</strong> value from request</td>
</tr>
<tr>
<td>participant_id</td>
<td style="text-align: center;">string</td>
<td><strong>participant_id</strong> value from request</td>
</tr>
<tr>
<td>cookie-result</td>
<td style="text-align: center;">integer</td>
<td><p>0 = <strong>Not Applicable</strong> - Cookie technologies are not
in use</p>
<p>1 = <strong>Success:</strong> after an opt out attempt, the opt out
cookie is present on the user’s browser</p>
<p>2 = <strong>Failure:</strong> after an opt out attempt, the cookie is
not present on the user’s browser</p>
<p>3 = <strong>Failure:</strong> anti-CSRF token mismatch [4..] =
Reserved for future use</p></td>
</tr>
<tr>
<td>other-result</td>
<td style="text-align: center;">integer</td>
<td><p>0 = <strong>Not Applicable</strong> - Non-Cookie technologies are
not in use</p>
<p>1 = <strong>Opt Out Success</strong>: Non Cookie Identifier for the
browser has been received by the Participants server</p>
<p>2 = <strong>Opt Out Failure</strong>: Non Cookie Identifier for the
browser was not received by the Participants server</p>
<p>3 = <strong>Failure:</strong> anti-CSRF token mismatch [4..] =
Reserved for future use</p></td>
</tr>
<tr>
<td>message</td>
<td style="text-align: center;">string</td>
<td>optional simple ascii text string fully URL compliant.</td>
</tr>
</tbody>
</table>

*<u>Response URL:</u>*

\<rd\>/finish/\<participant_id\>/\<action_id\>/\<cookie-result\>-\<other-result\>/\<message\>

<u>Example:</u>
`http://www.aboutads.info**/token/**123/1-1/magic_string`


## V. ESTABLISHING A FIRST PARTY TRUST RELATIONSHIP

This is a new feature available for all companies, regardless if they
utilize cookies exclusively or also use non-cookie technologies for
IBA. It is especially designed as a way to reliably set choice for
non-cookie tech in third-party cookie-blocking environments, but all
companies may use it to future-proof their choice systems or for other
reasons, consistent with DAA Principles.

In order to support browsers that restrict setting cookies in
third-party contexts, it has become necessary to add a new action_id
to the existing action_ids currently required from participant
endpoints.

This new request, known as action_id=5, is only used when a browser is
configured to reject third-party cookies, but allows setting
third-party cookies from sites “previously visited”. There is no
callback request or verification and it is the company’s
responsibility to maintain a responsive endpoint.

The purpose of this request is to set a session cookie so that a
temporary trust relationship is created with the browser. Any cookies
set during this process will be established in a first party context
with your domain. This will allow the subsequent opt-out request
(action_id=4) to set an opt-out cookie in a third-party context.

If the browser does not already have a first-party cookie set from the
company’s domain, this will create a trust relationship with the
browser that may not have been otherwise possible. If an enhanced
trust relationship is created as a part of this process, you may need
to indicate this in the cookie value. This will allow you to prevent
your systems from setting any additional cookies (such as frequency
capping, ad delivery & reporting) once an opt-out is set on browsers
where an enhanced trust relationship exists.

### Request

Headers

| **Attribute** | **Description / value** |
|----|----|
| Referer | http://\<dev \| staging \| qa \| integrate \| www \| optout\>.aboutads.info/\* |
| Accept | text/html,application/xhtml+xml |

*<u>Sample Requests URLs:</u>*

`http://your.domain/endpoint?action_id=5&nocache=223442`

URL Parameters

| **Field** | **Data Type** | **Description** |
|----|:--:|----|
| action_id | string | value “5” indicates establish temporary trust by setting a session cookie. |
| nocache | string | Ignore: cache buster |

### Response

1.  All cookies shall be set using HTTP headers. There is no redirect
    required as part of this request. **The use of JavaScript in this
    step is prohibited.**

### Guidelines For using a Trust Cookie (session cookie)

1.  The cookie for this step shall be a **session cookie with no
    expiration set.**

2.  This cookie shall be separate from the opt-out cookie, IBA cookies,
    and Reporting cookies.

3.  The cookie name and value shall be generic (non-unique). The best
    practice for this step shall be to use cookie name=“FPtrust” and
    cookie value=“1”

### Guidelines for response

1.  A company’s response shall be a single HTTP 200 response.

2.  Company shall set cookies using HTTP headers. **The use of
    JavaScript is prohibited.**

3.  No output shall be displayed to the screen unless for debugging
    purposes. This shall occur on: dev.aboutads.info AND NOT
    optout.aboutads.info

4.  Company’s response time shall be below 250ms. Timeouts for this step
    are very low. To facilitate a positive user experience, it is
    important that an adequate response time be maintained on all
    company endpoints to ensure timely opt-out delivery to consumers’
    browsers.



[^1]: Cookie-less technologies in this WebChoices document do
NOT include IDFA, AAID, hashed emails and phone numbers. DAA offers
different tools: AppChoices, for consumers to set preferences in the
in-app environment and YAC Token Tool for consumers to set preferences
for hashed identifiers.
