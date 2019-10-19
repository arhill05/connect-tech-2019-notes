# OAuth2 & OpenID-Connect
## By Stephani Chamblee
- @stephchamblee
- stepaniechamblee.com
- scamblee@thebrightlink.com
- Software developer at BrightLink
- Auth0 Ambassador

## Notes
### Overview
- Context
  - Open standards
  - Brief history of Identity

- Foundation
  - Four roles in OAuth
  - Tokens
  - Authorization Flows

### Context
- OAuth2 and OpenID Connect example images

- Open standards
  - Industry specifications and guidelines given to develop things on the internet
  - Examples
    - SAML
    - JWT
    - OAuth2
    - OpenID Connect
- History of Identity
  - Identity and authentication has been a concern for all of human history.
  - As early as 130 BC, people used watch words sort of like passwords where you had to say something in order to access a protected area
  - Passwords were introduced in the 1960's
    - Not even a year after passwords were introduced, a vulnerabilty was exposed. A researcher made everyone's passwords public on the machine
    - They worked okay until the internet was introduced because people had to be physically present at the machine to log in
  - The simple login form was introduced
    - Simple login security
      - Password strength requirements
      - Password hashing
      - Two-Factor Authentication
    - Even if you take all of these security measures, there are still vulnerabilities.
  - In the business world, another problem was introduced. If a company has multiple systems that each authenticate on their own and a user is fired, the company has to make sure all access is revoked from that user from all systems.
    - This brought the introduction of SAML in 2002 to implement single-sign-on
  - Delegated authorization
    - Allowing credentials for one site to authorize to another site
  - OAuth2 was publshed in 2012.
- OAuth is about *authorization*, not *authentication*
- Authorization vs authentication
  - **Authorization** is like a key. There is no identifier that says it belongs to one person, but it allows you to access something
  - **Authentication** is all about verifying identity. A good example is a passport - it allows you to travel to another country, but it also exposes data about the person who it belongs to.
  - Authorization can sometimes be granted with authentication, but authorization does not expose anything about a user's identity
- When people started using OAuth2 for Authentication when it's not meant for that, there became a need for a standard.
- Thus OpenID Connect was born as a standard in 2014.

### Foundation
#### Four Roles defined by OAuth2
- Resource Owner
  - End user that provides consent for scopes
  - They grant access to scopes for different pieces of user data, i.e. email, phone number, contacts list, etc
- Resource Server
  - API or application controlling the data
  - If you are authorizing with Facebook, Facebook is the resource server because they have access to the user data
- Authorization Server
  - Application handling delegated authorization decisions
  - Sort of like a gatekeeper saying "yes, I will grant this person an access token"
- Client
  - Application requesting the data
  - Relying party
  - Ex: LinkedIn. Once you allow LinkedIn to access your Google data, LinkedIn can invite your friends from your contacts list granted from Google

#### Tokens
- Access Token
  - The whole point of OAuth
  - This is how a client acquires the data about a user
  - The "key"
- Refresh Token
  - When a client is issued an access token, they are also issued a refresh token a lot of times.
  - Access tokens aren't supposed to last very long in case they are compromised.
  - The refresh token has a much longer life that is presented kind of like a membership card. It says "My access token is expired but I have this membership card, can I have another access token?:
- ID Token
  - Stores the data about the user.
  - This is the part that OpenID Connect brings to the equation.
  - ID token is a JWT
  - Sort of like a driver's license

#### JWT (JSON Web Token)
  - Encoded Claims (user data)
  - Stateless validation
    - There's no trip to a database to verify data about a user because the data is right in the token
  - Signed for authenticity
    - This makes it easy to verify that tokens haven't been tampered with
  - 3 parts to a JWT
    - Header
      - Type of token and something else
    - Payload
      - Contains user data. If you're following OpenID, there are 5 parts you must include:
        - Issuer - who issued the token
        - Sub - ?
        - Audience - the client ID that is assigned to the client before the action takes place. The authorization server will have this value stored
        - Exp - when the token expires
        - IssuedAt - when the token was issued
    - Signature
      - uses the header, the payload, and a secret to sign the token.
      - lets everyone know
  - JWT's are Base64 encoded, so it's easy to see information in them. Therefore, you have to be careful what info you put in them

#### Authorization Grants
- methods for a client application to acquire an access token which will grant access to a resource owner's data

- authorization grant flows
  - Authorization Code
  - Authorization Code + PKCE
- Front channel
  - Browser to API
  - Not so secure
  - Anything that is in the browser
  - vulnerable to things like XSS
- Back-Channel
  - Server to API
  - Very Secure
  - Server communicating to an API over SSL/TLS
- Authorization Code Flow
  - Uses BOTH back channel + front channel flows
  - The user has to be involved, so front channel is used, but granting access and refresh tokens is handled by back channel
- Authorization Code + PKCE
  - Front channel only
  - PKCE = proof key for code exchange
- Client Credentials Flow
  - Back Channel Only
  - Machine to machine
  - example: microservices

### OAuth2 & OpenID-Connect Flow
- Using the Authorization Code grant
- A. Client makes request to Resource Owner for authorization to access data
- B. Resource Owner issues authorization grant
- C. Client takes authorization grant and requests authorization code from the Authorization Server
- D. Authorization Server grants an authorization code
  - An authorization code is used by the client and can be exchanged for an access token
  - The authorization code can only be used once
- E. Client requests an access token from the authorization server to access the user data
- F. Authorization Server gives the Client an access token, a refresh token, and an ID token.
- G. Client requests user data from Resource Server with a valid access token and ID token
- E. After x amount of time, the access token expires. The Client requests another access token from the Authorization Server with the refresh token.

## Key Takeaways
- Differences between authentication and authorization
  - Authorization is like a key - it simply unlocks something. There's nothing tying it to an individual
  - Authentication has authorization, but it also holds identifying information about the user. Anything you would want to know could be stored in the auth token.
- How the OAuth2 and OIDC flow works (see relevant section)
- Four different roles associated with this flow (see relevant section)
