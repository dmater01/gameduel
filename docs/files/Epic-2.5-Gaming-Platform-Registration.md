# Epic 2.5: Gaming Platform Registration & API Setup

## Epic Metadata

| Field                  | Value                                                    |
| ---------------------- | -------------------------------------------------------- |
| **Epic ID**            | Epic 2.5                                                 |
| **Epic Name**          | Gaming Platform Registration & API Setup                 |
| **Priority**           | P0 (Critical - Blocks Epic 3)                            |
| **Status**             | Ready for Immediate Start                                |
| **Estimated Duration** | 5-7 days (includes platform approval wait times)         |
| **Dependencies**       | Epic 0 (Project Foundation)                              |
| **Blocks**             | Epic 3 (Gaming Platform Integrations)                    |
| **Owner**              | User (Platform Registration) + Tech Lead (Configuration) |

---

## ⚠️ CRITICAL NOTICE

**This epic contains USER ACTIONS that should start IMMEDIATELY, even before Epic 1!**

Gaming platforms require account registration and approval, which can take **3-7 days**. Starting this epic early prevents blocking Epic 3 (Gaming Integration) in Week 9.

**Recommended Timeline:**

- **Week 0-1**: User registers for all three platforms (parallel to Epic 0)
- **Week 2-8**: Wait for platform approvals (happens during Epic 1 & 2)
- **Week 8**: Developer configures credentials (before Epic 3)
- **Week 9+**: Epic 3 can proceed without delays

---

## Epic Overview

### Purpose

Register GameDuel with Steam, Xbox Live, and PlayStation Network to obtain API credentials required for gaming platform integrations. This epic is split into USER actions (platform registration) and DEVELOPER actions (credential configuration).

### Business Value

- **Unblock Epic 3**: Gaming integration cannot proceed without API credentials
- **Risk Mitigation**: Platform approvals take unpredictable time (3-7 days minimum)
- **Compliance**: Ensures GameDuel operates within platform terms of service
- **Security**: Proper OAuth setup protects user gaming accounts

### Success Criteria

- ✅ Steam Web API key obtained and working
- ✅ Xbox Live application registered with client ID/secret
- ✅ PSN access strategy determined and implemented
- ✅ All credentials securely stored in environment configuration
- ✅ Test API calls succeed for each platform
- ✅ OAuth redirect URIs configured correctly

### Epic Acceptance Criteria

- [ ] User has active developer accounts on Steam and Xbox
- [ ] Steam Web API key obtained and verified
- [ ] Xbox Live application created with OAuth credentials
- [ ] PSN access approach decided (official vs unofficial API)
- [ ] Environment variables configured in Expo/EAS secrets
- [ ] Test API call succeeds for Steam (GetPlayerSummaries)
- [ ] Test OAuth flow succeeds for Xbox Live
- [ ] Documentation updated with credential setup instructions
- [ ] Security best practices followed (no credentials in git)

---

## Stories in This Epic

1. **Story 2.5.1**: Register Steam Partner Account & Obtain API Key (USER)
2. **Story 2.5.2**: Register Xbox Live Application (USER)
3. **Story 2.5.3**: Determine PSN Access Strategy (USER + DEV)
4. **Story 2.5.4**: Configure Environment Variables & Test Credentials (DEV)

---

## Story 2.5.1: Register Steam Partner Account & Obtain API Key

### Story Metadata

```yaml
id: story-2.5.1
title: Register Steam Partner Account & Obtain API Key
epic: Epic 2.5 - Gaming Platform Registration
priority: P0
estimated_effort: 1-2 hours active work + 3-7 days approval wait
dependencies: []
assignee: USER (Product Owner or designated team member)
status: Ready - START IMMEDIATELY
user_action: true
```

### User Story

**As a** GameDuel product owner  
**I want** to obtain a Steam Web API key  
**So that** our app can access user gaming data from Steam

### Context

Steam provides a Web API for accessing user profiles, game libraries, and achievements. We need an API key to authenticate our requests. This is a **USER action** - the product owner or team member with Steam account must complete this.

### Pre-requisites

- Personal Steam account (can be created at https://store.steampowered.com)
- Valid email address
- Domain name for GameDuel (or localhost for development)

### Acceptance Criteria

- [ ] Steam developer account created at https://steamcommunity.com/dev
- [ ] Steam Web API key generated
- [ ] API key domain configured (or set to localhost for development)
- [ ] API key securely shared with development team (via secure channel, never committed to git)
- [ ] Test API call made to verify key works
- [ ] API key copied to secure location for handoff to developers

### Step-by-Step Instructions

#### Step 1: Create/Login to Steam Account

1. Go to https://store.steampowered.com
2. If you don't have a Steam account:
   - Click "Join Steam" (top right)
   - Complete registration with valid email
   - Verify email address
   - Complete Steam Guard setup (2FA recommended)
3. If you have an account, simply log in

#### Step 2: Access Steam Web API Registration

1. Go to https://steamcommunity.com/dev
2. You should see "Steam Web API - Publisher Authentication Key"
3. If prompted, log in with your Steam account

#### Step 3: Generate API Key

1. Read and accept the Steam Web API Terms of Use
2. In the "Domain Name" field, enter:
   - For development: `localhost` or `127.0.0.1`
   - For production (later): `gameduel.app` or your actual domain
   - **Note**: You can change this later, so use `localhost` for now
3. Click "Register" or "Request API Key"
4. **Your API key will be displayed** - it looks like: `XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX` (32 hex characters)

#### Step 4: Document the API Key

**CRITICAL**: Do NOT commit this key to git or share it publicly!

Create a secure note with the following information:

```
Steam Web API Credentials
==========================
API Key: [YOUR 32-CHARACTER KEY]
Domain: localhost (for development)
Account Email: [your steam email]
Date Obtained: [today's date]
Documentation: https://partner.steamgames.com/doc/webapi_overview

Test Endpoint:
https://api.steampowered.com/ISteamWebAPIUtil/GetSupportedAPIList/v1/?key=[YOUR_KEY]
```

#### Step 5: Test the API Key

1. Open browser or use curl to test:

```bash
curl "https://api.steampowered.com/ISteamWebAPIUtil/GetSupportedAPIList/v1/?key=YOUR_API_KEY_HERE"
```

2. You should receive a JSON response listing available APIs
3. If you get an error "Access Denied" or "Invalid Key", double-check the key

#### Step 6: Share with Development Team

Share the API key securely via:

- Password manager (1Password, LastPass, Bitwarden)
- Encrypted messaging (Signal, encrypted email)
- Team secrets manager (AWS Secrets Manager, Azure Key Vault)

**NEVER:**

- ❌ Commit to git
- ❌ Send via plain email
- ❌ Post in Slack/Discord/public channels
- ❌ Include in screenshots

### Verification Steps

1. API key obtained successfully
2. Test endpoint returns valid JSON
3. Key shared securely with development team
4. Documentation saved in secure location

### Definition of Done

- [ ] Steam Web API key obtained
- [ ] Test API call successful
- [ ] Key securely documented
- [ ] Key shared with development team
- [ ] Screenshot/proof saved (with key redacted)

### Troubleshooting

**"I can't access steamcommunity.com/dev"**

- Ensure you're logged into Steam
- Try a different browser
- Disable VPN if active
- Clear browser cache

**"The page says I need a Steam purchase"**

- Some regions require a purchase history
- Buy the cheapest game (usually < $5)
- Alternative: Ask a team member with existing Steam account

**"I lost my API key"**

- Go back to https://steamcommunity.com/dev
- Your existing key will be displayed
- You can regenerate a new key if needed (old key will stop working)

### Time Estimate

- **Active work**: 15-30 minutes
- **Wait time**: Immediate (instant approval)
- **Total**: 30 minutes

### Notes

- **Start this IMMEDIATELY** - no blockers
- API key is tied to your Steam account
- Keep the account credentials secure (2FA enabled)
- This key will be used in Epic 3 Story 3.2 (Steam OAuth Implementation)

---

## Story 2.5.2: Register Xbox Live Application

### Story Metadata

```yaml
id: story-2.5.2
title: Register Xbox Live Application with Microsoft Azure
epic: Epic 2.5 - Gaming Platform Registration
priority: P0
estimated_effort: 2-3 hours active work + 3-7 days approval wait
dependencies: []
assignee: USER (Product Owner or designated team member)
status: Ready - START IMMEDIATELY
user_action: true
```

### User Story

**As a** GameDuel product owner  
**I want** to register GameDuel as an Xbox Live application  
**So that** our app can authenticate users and access their Xbox gaming data

### Context

Xbox Live API access requires registering an application through Azure Active Directory. This process is more complex than Steam and may require organizational approval. This is a **USER action**.

### Pre-requisites

- Microsoft account (can be personal or work account)
- Access to Azure Portal (free tier is sufficient)
- Organization approval (if using work account)
- Valid email for verification

### Acceptance Criteria

- [ ] Microsoft Azure account created/accessed
- [ ] Xbox Live application registered in Azure Portal
- [ ] Application (Client) ID obtained
- [ ] Client Secret created and saved
- [ ] Redirect URIs configured for OAuth
- [ ] API permissions granted (Xbox Live APIs)
- [ ] Test credentials documented
- [ ] Credentials securely shared with development team

### Step-by-Step Instructions

#### Step 1: Create Microsoft Azure Account

1. Go to https://portal.azure.com
2. Sign in with Microsoft account (or create one at https://account.microsoft.com)
3. If first time: Complete Azure free account setup
   - No credit card required for free tier
   - Provide basic information
   - Verify email address

#### Step 2: Navigate to Azure Active Directory

1. In Azure Portal, search for "Azure Active Directory" in top search bar
2. Click on "Azure Active Directory" in results
3. In left sidebar, click "App registrations"

#### Step 3: Register New Application

1. Click "+ New registration" (top of page)
2. Fill in application details:
   - **Name**: `GameDuel`
   - **Supported account types**: Select "Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)"
   - **Redirect URI**:
     - Platform: `Public client/native (mobile & desktop)`
     - URI: `exp://localhost:19000` (for Expo development)
     - Click "Add URI" and add: `gameduel://auth/xbox/callback`
3. Click "Register"

#### Step 4: Save Application (Client) ID

1. After registration, you'll see the "Overview" page
2. **Copy and save the "Application (client) ID"**
   - Looks like: `12345678-1234-1234-1234-123456789abc` (GUID format)
3. Also note the "Directory (tenant) ID" (you'll need this too)

#### Step 5: Create Client Secret

1. In left sidebar, click "Certificates & secrets"
2. Under "Client secrets", click "+ New client secret"
3. Add description: `GameDuel Development Secret`
4. Set expiration: `24 months` (maximum)
5. Click "Add"
6. **CRITICAL**: Copy the secret VALUE immediately (you can't see it again!)
   - Looks like: `abc123~DEF456.GHI789-JKL012_MNO345`
7. Save this securely with the Client ID

#### Step 6: Configure API Permissions

1. In left sidebar, click "API permissions"
2. Click "+ Add a permission"
3. Select "APIs my organization uses"
4. Search for "Xbox" (you may need to request access)
5. If Xbox Live API is not available:
   - Alternative: We'll use Microsoft Graph API for basic Xbox profile
   - Select "Microsoft Graph"
   - Choose "Delegated permissions"
   - Add: `User.Read`, `XboxLive.signin`, `XboxLive.offline_access`
6. Click "Add permissions"
7. **Important**: Click "Grant admin consent" (if you have permissions)

#### Step 7: Configure Authentication Settings

1. In left sidebar, click "Authentication"
2. Under "Platform configurations", verify your redirect URIs
3. Under "Advanced settings":
   - Enable "Allow public client flows": **Yes**
4. Click "Save"

#### Step 8: Document Credentials

Create a secure note with:

```
Xbox Live API Credentials
=========================
Application (Client) ID: [YOUR CLIENT ID GUID]
Directory (Tenant) ID: [YOUR TENANT ID GUID]
Client Secret: [YOUR SECRET VALUE]
Secret Expiration: [DATE 24 months from now]

Redirect URIs:
- exp://localhost:19000 (development)
- gameduel://auth/xbox/callback (production)

Permissions:
- User.Read
- XboxLive.signin
- XboxLive.offline_access

Documentation:
- https://docs.microsoft.com/en-us/gaming/xbox-live/

Created: [TODAY'S DATE]
Created By: [YOUR NAME]
```

#### Step 9: Test Configuration (Optional but Recommended)

While you can't fully test until developers implement OAuth, you can verify:

1. Client ID is valid GUID format
2. Secret is copied correctly
3. Application appears in Azure Portal under "App registrations"

### Verification Steps

1. Application registered in Azure Portal
2. Client ID and Secret obtained
3. Redirect URIs configured
4. API permissions granted
5. Credentials securely documented
6. Credentials shared with development team

### Definition of Done

- [ ] Azure account created/accessed
- [ ] Xbox Live application registered
- [ ] Client ID and Secret obtained
- [ ] Redirect URIs configured
- [ ] API permissions granted
- [ ] Credentials securely documented and shared
- [ ] Screenshot saved (with secrets redacted)

### Troubleshooting

**"I don't have access to Azure Active Directory"**

- Use personal Microsoft account (not work account)
- Create new Microsoft account at https://account.microsoft.com
- Sign up for free Azure tier

**"Xbox Live API not showing in permissions"**

- Use Microsoft Graph API as alternative
- Add permissions: `User.Read`, `XboxLive.signin`
- This provides basic Xbox profile access

**"Need admin consent but I'm not admin"**

- If using work account, request IT admin to grant consent
- Alternative: Use personal Microsoft account
- For development, some permissions work without admin consent

**"Can't see Client Secret value"**

- You can only see it once when created
- If lost, create a new secret (old one can be deleted)
- Update development team with new secret

**"Redirect URI validation error"**

- Ensure exact match: `exp://localhost:19000`
- For Expo, the scheme is `exp://` not `http://`
- Second URI should be: `gameduel://auth/xbox/callback`

### Time Estimate

- **Active work**: 1-2 hours (first time)
- **Wait time**: Usually immediate, but organizational approval may take 1-3 days
- **Total**: 1-2 hours to 3 days

### Important Notes

- **Start this IMMEDIATELY** - organizational approvals may delay
- Client Secret expires in 24 months - calendar reminder!
- Keep Azure account credentials secure (enable 2FA)
- This will be used in Epic 3 Story 3.5 (Xbox Live OAuth Implementation)
- If using work account, ensure your organization allows Xbox Live API access

### Additional Resources

- [Microsoft Identity Platform Documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/)
- [Xbox Live API Overview](https://docs.microsoft.com/en-us/gaming/xbox-live/)
- [Register an Azure AD App](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app)

---

## Story 2.5.3: Determine PSN Access Strategy

### Story Metadata

```yaml
id: story-2.5.3
title: Research and Determine PlayStation Network API Access Strategy
epic: Epic 2.5 - Gaming Platform Registration
priority: P1
estimated_effort: 3-4 hours research + decision time
dependencies: []
assignee: USER (Product Owner) + Tech Lead
status: Ready
user_action: true (with technical consultation)
```

### User Story

**As a** GameDuel product owner  
**I want** to determine the best approach for PlayStation Network integration  
**So that** we can access PSN trophy data and game information legally and reliably

### Context

Unlike Steam and Xbox, Sony does NOT provide an official public API for PlayStation Network. This story involves researching options, assessing legal/technical risks, and making a strategic decision. This requires collaboration between USER (business/legal decision) and DEVELOPER (technical feasibility).

### Pre-requisites

- Understanding of PSN integration goals (Architecture Section 9.1.3)
- Legal/compliance review capability
- Technical evaluation of unofficial APIs
- Risk tolerance assessment

### Acceptance Criteria

- [ ] Official PSN API status confirmed (expected: not available)
- [ ] Unofficial API options researched and documented
- [ ] Legal risks assessed and documented
- [ ] Technical feasibility evaluated
- [ ] Decision made: Official partnership, unofficial API, or defer to post-MVP
- [ ] If unofficial API chosen: specific library/service selected
- [ ] If deferring: clear post-MVP plan documented
- [ ] Decision documented and approved by stakeholders
- [ ] Development team informed of approach

### Research Areas

#### Option 1: Official Sony Partnership

**What to investigate:**

- Sony Developer Program requirements
- Timeline for approval (typically 6+ months)
- Costs involved (likely significant)
- Application requirements
- Contact: https://www.playstation.com/en-us/dev-program/

**Pros:**

- Fully legal and supported
- Reliable API access
- Official documentation
- Sony marketing opportunities

**Cons:**

- 6-12 month approval process
- Likely requires existing game or significant app
- May require revenue sharing or fees
- Blocks MVP timeline

**Recommendation for MVP:** ❌ Too slow for MVP timeline

#### Option 2: Unofficial API Libraries

**What to investigate:**
Research these community-maintained libraries:

1. **PSN-API (Node.js)**
   - GitHub: https://github.com/achievements-app/psn-api
   - npm: `psn-api`
   - Authentication: Uses NPSSO tokens
   - Capabilities: Profile, trophies, games, friends
   - Risk level: MEDIUM

2. **PlayStation-API (Python)**
   - GitHub: https://github.com/isFakeAccount/psnawp
   - Capabilities: Trophy data, game titles
   - Authentication: NPSSO token
   - Risk level: MEDIUM

3. **Direct API Calls**
   - Reverse-engineered endpoints
   - Authentication: Complex OAuth flow
   - Capabilities: Limited
   - Risk level: HIGH

**How unofficial APIs work:**

- User provides NPSSO token from their PSN account
- Library makes authenticated requests to PSN endpoints
- No official API key or registration
- Relies on undocumented endpoints

**Pros:**

- Available immediately
- No Sony approval needed
- Free to use
- Community support

**Cons:**

- Violates Sony Terms of Service (technically)
- Could break without notice
- No official support
- Potential account ban risk for users
- Legal gray area

#### Option 3: Defer to Post-MVP

**What this means:**

- Launch MVP with Steam + Xbox only
- Add PSN in Phase 2 after proving concept
- Pursue official partnership with demo app
- Reevaluate unofficial options

**Pros:**

- Focuses MVP on achievable features
- Reduces legal risk
- Allows time for Sony partnership application
- Steam + Xbox cover 70%+ of target market

**Cons:**

- Missing PlayStation audience (20-25% of gamers)
- Incomplete gaming platform coverage
- Potential user disappointment

### Decision Framework

**Questions to answer:**

1. **Legal Risk Tolerance**
   - Q: Is GameDuel venture-backed or bootstrapped?
   - Q: Do we have legal counsel to review ToS violations?
   - Q: What's the worst case if Sony objects?

2. **Technical Risk Tolerance**
   - Q: Can we handle API breakage gracefully?
   - Q: Do we have engineering time to maintain unofficial integration?
   - Q: Can we build fallback mechanisms?

3. **Business Priority**
   - Q: How important is PSN for MVP success?
   - Q: What % of target users are PlayStation-only?
   - Q: Can we market successfully with Steam + Xbox only?

4. **Timeline Constraints**
   - Q: Can MVP ship without PSN?
   - Q: When can we pursue official partnership?
   - Q: Is unofficial API acceptable as temporary solution?

### Recommended Approach (for bootstrapped startup)

**For MVP: Option 2 (Unofficial API) with clear user disclaimers**

Rationale:

- PSN represents 20-25% of gaming market
- Unofficial API provides basic trophy/game data
- Can be implemented in MVP timeline
- Include clear disclaimers about unofficial status
- Plan migration to official API post-MVP

**Implementation guidelines if choosing unofficial API:**

1. Use established library (psn-api is most mature)
2. Include clear disclaimers in app:
   - "PlayStation Network integration uses unofficial methods"
   - "Sony may change access at any time"
   - "Your PSN account security is your responsibility"
3. Never store PSN credentials - only NPSSO tokens
4. Implement graceful degradation if API fails
5. Document exit strategy for official API migration
6. Begin Sony partnership application immediately after MVP launch

### Step-by-Step Instructions

#### Step 1: Research Official Partnership (2 hours)

1. Visit https://www.playstation.com/en-us/dev-program/
2. Review requirements and timeline
3. Document findings in decision document

#### Step 2: Evaluate Unofficial APIs (2 hours)

1. Review psn-api GitHub repository
2. Check recent issues/activity (is it maintained?)
3. Test with personal PSN account (if possible)
4. Document capabilities and limitations

#### Step 3: Assess Legal Risk (1 hour + legal consultation)

1. Review Sony's PlayStation Network Terms of Service
2. Consult with legal counsel (if available)
3. Document potential risks and mitigations

#### Step 4: Make Decision (1 hour stakeholder meeting)

1. Present options to stakeholders
2. Discuss risk tolerance and priorities
3. Make and document decision
4. Define implementation plan

#### Step 5: Document Decision

Create decision document:

```markdown
# PSN Integration Strategy Decision

## Decision

[Official Partnership / Unofficial API / Defer to Post-MVP]

## Rationale

[Why this decision was made]

## Risks

- [List identified risks]

## Mitigations

- [How we'll address risks]

## Implementation Plan

- [Technical approach]
- [Timeline]
- [Resources needed]

## Exit Strategy

- [How we'll migrate to official API if/when available]

## Approval

- Product Owner: [Name/Date]
- Tech Lead: [Name/Date]
- Legal (if applicable): [Name/Date]
```

### Verification Steps

1. Research completed for all options
2. Legal risks documented
3. Technical feasibility assessed
4. Decision made and documented
5. Development team informed
6. Implementation plan created

### Definition of Done

- [ ] Official partnership option researched
- [ ] Unofficial API options evaluated
- [ ] Legal risks assessed
- [ ] Business priorities considered
- [ ] Decision made and documented
- [ ] Implementation plan created
- [ ] Stakeholders approved decision
- [ ] Development team briefed

### Troubleshooting

**"Can't find Sony developer contact"**

- Start here: https://www.playstation.com/en-us/dev-program/
- Alternative: https://partners.playstation.net/
- Note: Typically requires existing game or significant app

**"Unofficial API seems risky"**

- Correct assessment - there ARE risks
- Consider deferring to post-MVP
- Steam + Xbox cover majority of market
- Can launch MVP without PSN

**"Legal counsel says ToS violation is concerning"**

- Strong signal to defer to post-MVP
- Pursue official partnership
- Launch with Steam + Xbox only

### Time Estimate

- **Research**: 3-4 hours
- **Legal consultation**: 1-2 hours (if needed)
- **Decision meeting**: 1 hour
- **Documentation**: 1 hour
- **Total**: 6-8 hours spread over 2-3 days

### Important Notes

- **This is a strategic decision** - involves business, legal, and technical
- No single "right" answer - depends on risk tolerance
- **Can defer to post-MVP** - not blocking Epic 1-2
- If choosing unofficial API, start Sony partnership application immediately
- Document decision thoroughly for future reference

### Recommended Decision for Most Teams

**Defer to Post-MVP** unless:

- You have existing Sony relationship
- Legal counsel approves unofficial API use
- PSN is critical for target market (e.g., PlayStation-focused app)

**Rationale:**

- Reduces risk
- Focuses MVP
- Steam + Xbox cover 70%+ market
- Allows time for official partnership pursuit

---

## Story 2.5.4: Configure Environment Variables & Test Credentials

### Story Metadata

```yaml
id: story-2.5.4
title: Configure Environment Variables and Test Gaming API Credentials
epic: Epic 2.5 - Gaming Platform Registration
priority: P0
estimated_effort: 2-3 hours
dependencies: [story-2.5.1, story-2.5.2, story-2.5.3]
assignee: Tech Lead or Senior Developer
status: Blocked (waiting for credentials from 2.5.1, 2.5.2, 2.5.3)
user_action: false (developer task)
```

### User Story

**As a** developer  
**I want** gaming platform credentials securely configured  
**So that** I can test API integrations without exposing secrets

### Context

Once credentials are obtained from Stories 2.5.1-2.5.3, we need to configure them securely in our development and production environments. This follows Architecture Section 8.2 (Data Security) and Section 12.2 (Environment Configuration).

### Pre-requisites

- Epic 0 complete (project initialized)
- Credentials from Story 2.5.1 (Steam API key)
- Credentials from Story 2.5.2 (Xbox Client ID/Secret)
- Decision from Story 2.5.3 (PSN approach)
- Expo project set up

### Acceptance Criteria

- [ ] `.env` file created with all credentials (gitignored)
- [ ] `.env.example` created with placeholder values (committed to git)
- [ ] Expo secrets configured for EAS builds
- [ ] Environment configuration service created
- [ ] Test script created to verify all credentials
- [ ] All API test calls succeed (Steam, Xbox, PSN if applicable)
- [ ] Documentation updated with credential setup instructions
- [ ] Team members can easily set up their local environments

### Technical Implementation Notes

#### Step 1: Create Environment Configuration

**Create `.env` file** (root directory):

```bash
# Gaming Platform API Credentials
# ================================
# CRITICAL: This file is gitignored and should NEVER be committed

# Steam Web API
STEAM_API_KEY=YOUR_32_CHARACTER_STEAM_KEY_HERE

# Xbox Live (Azure AD)
XBOX_CLIENT_ID=YOUR_XBOX_CLIENT_ID_GUID_HERE
XBOX_CLIENT_SECRET=YOUR_XBOX_CLIENT_SECRET_HERE
XBOX_TENANT_ID=YOUR_TENANT_ID_GUID_HERE

# PlayStation Network (if using unofficial API)
PSN_ENABLED=false
# PSN_NPSSO_TOKEN=  # User-provided, not stored here

# App Configuration
APP_ENV=development
API_TIMEOUT=10000
```

**Create `.env.example`** (root directory - this IS committed):

```bash
# Gaming Platform API Credentials - Example Configuration
# =========================================================
# Copy this file to .env and fill in your actual values
# Never commit .env file to git!

# Steam Web API
# Get your key from: https://steamcommunity.com/dev
STEAM_API_KEY=your_steam_api_key_here

# Xbox Live (Azure AD)
# Register app at: https://portal.azure.com -> App Registrations
XBOX_CLIENT_ID=your_xbox_client_id_guid
XBOX_CLIENT_SECRET=your_xbox_client_secret
XBOX_TENANT_ID=your_tenant_id_guid

# PlayStation Network
PSN_ENABLED=false

# App Configuration
APP_ENV=development
API_TIMEOUT=10000
```

**Update `.gitignore`:**

```bash
# Environment variables
.env
.env.local
.env.*.local

# Expo
.expo/
dist/
web-build/

# Node
node_modules/
```

#### Step 2: Install Environment Variable Packages

```bash
npm install react-native-dotenv
npm install --save-dev @types/react-native-dotenv
```

**Configure babel.config.js:**

```javascript
module.exports = function (api) {
  api.cache(true);
  return {
    presets: ['babel-preset-expo'],
    plugins: [
      [
        'module:react-native-dotenv',
        {
          moduleName: '@env',
          path: '.env',
          safe: false,
          allowUndefined: true,
        },
      ],
    ],
  };
};
```

**Create TypeScript types** (src/types/env.d.ts):

```typescript
declare module '@env' {
  export const STEAM_API_KEY: string;
  export const XBOX_CLIENT_ID: string;
  export const XBOX_CLIENT_SECRET: string;
  export const XBOX_TENANT_ID: string;
  export const PSN_ENABLED: string;
  export const APP_ENV: string;
  export const API_TIMEOUT: string;
}
```

#### Step 3: Create Environment Configuration Service

**Create config service** (src/config/environment.ts):

```typescript
import {
  STEAM_API_KEY,
  XBOX_CLIENT_ID,
  XBOX_CLIENT_SECRET,
  XBOX_TENANT_ID,
  PSN_ENABLED,
  APP_ENV,
  API_TIMEOUT,
} from '@env';

interface EnvironmentConfig {
  steam: {
    apiKey: string;
    baseUrl: string;
  };
  xbox: {
    clientId: string;
    clientSecret: string;
    tenantId: string;
    redirectUri: string;
  };
  psn: {
    enabled: boolean;
  };
  app: {
    environment: string;
    apiTimeout: number;
  };
}

class Environment {
  private config: EnvironmentConfig;

  constructor() {
    this.config = {
      steam: {
        apiKey: STEAM_API_KEY || '',
        baseUrl: 'https://api.steampowered.com',
      },
      xbox: {
        clientId: XBOX_CLIENT_ID || '',
        clientSecret: XBOX_CLIENT_SECRET || '',
        tenantId: XBOX_TENANT_ID || '',
        redirectUri: 'exp://localhost:19000', // Update for production
      },
      psn: {
        enabled: PSN_ENABLED === 'true',
      },
      app: {
        environment: APP_ENV || 'development',
        apiTimeout: parseInt(API_TIMEOUT || '10000', 10),
      },
    };

    this.validateConfig();
  }

  private validateConfig(): void {
    const errors: string[] = [];

    if (!this.config.steam.apiKey) {
      errors.push('STEAM_API_KEY is not configured');
    }

    if (!this.config.xbox.clientId) {
      errors.push('XBOX_CLIENT_ID is not configured');
    }

    if (!this.config.xbox.clientSecret) {
      errors.push('XBOX_CLIENT_SECRET is not configured');
    }

    if (errors.length > 0 && this.config.app.environment !== 'test') {
      console.warn('⚠️ Environment configuration warnings:');
      errors.forEach((error) => console.warn(`  - ${error}`));
    }
  }

  get steam() {
    return this.config.steam;
  }

  get xbox() {
    return this.config.xbox;
  }

  get psn() {
    return this.config.psn;
  }

  get app() {
    return this.config.app;
  }

  isConfigured(platform: 'steam' | 'xbox' | 'psn'): boolean {
    switch (platform) {
      case 'steam':
        return !!this.config.steam.apiKey;
      case 'xbox':
        return !!this.config.xbox.clientId && !!this.config.xbox.clientSecret;
      case 'psn':
        return this.config.psn.enabled;
      default:
        return false;
    }
  }
}

export const ENV = new Environment();
export default ENV;
```

#### Step 4: Create Credential Test Script

**Create test script** (src/config/testCredentials.ts):

```typescript
import axios from 'axios';
import ENV from './environment';

export async function testSteamCredentials(): Promise<boolean> {
  console.log('🧪 Testing Steam API credentials...');

  if (!ENV.steam.apiKey) {
    console.error('❌ Steam API key not configured');
    return false;
  }

  try {
    const response = await axios.get(
      `${ENV.steam.baseUrl}/ISteamWebAPIUtil/GetSupportedAPIList/v1/`,
      {
        params: { key: ENV.steam.apiKey },
        timeout: ENV.app.apiTimeout,
      }
    );

    if (response.status === 200 && response.data) {
      console.log('✅ Steam API key is valid');
      return true;
    } else {
      console.error('❌ Steam API returned unexpected response');
      return false;
    }
  } catch (error) {
    console.error('❌ Steam API test failed:', (error as Error).message);
    return false;
  }
}

export async function testXboxCredentials(): Promise<boolean> {
  console.log('🧪 Testing Xbox Live credentials...');

  if (!ENV.xbox.clientId || !ENV.xbox.clientSecret) {
    console.error('❌ Xbox credentials not configured');
    return false;
  }

  // Note: Full OAuth test requires user interaction
  // This just validates credentials are present and formatted correctly
  const guidRegex = /^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/i;

  if (!guidRegex.test(ENV.xbox.clientId)) {
    console.error('❌ Xbox Client ID is not a valid GUID format');
    return false;
  }

  if (!guidRegex.test(ENV.xbox.tenantId)) {
    console.error('❌ Xbox Tenant ID is not a valid GUID format');
    return false;
  }

  console.log('✅ Xbox credentials are properly formatted');
  console.log('   (Full OAuth test requires user interaction)');
  return true;
}

export async function testPSNConfiguration(): Promise<boolean> {
  console.log('🧪 Checking PSN configuration...');

  if (!ENV.psn.enabled) {
    console.log('ℹ️  PSN integration is disabled');
    return true;
  }

  console.log('✅ PSN integration is enabled');
  console.log('   (Will require user-provided NPSSO token at runtime)');
  return true;
}

export async function testAllCredentials(): Promise<void> {
  console.log('\n🔐 Testing Gaming Platform Credentials\n');
  console.log('='.repeat(50));

  const steamOk = await testSteamCredentials();
  const xboxOk = await testXboxCredentials();
  const psnOk = await testPSNConfiguration();

  console.log('='.repeat(50));
  console.log('\n📊 Test Results:');
  console.log(`  Steam:  ${steamOk ? '✅ PASS' : '❌ FAIL'}`);
  console.log(`  Xbox:   ${xboxOk ? '✅ PASS' : '❌ FAIL'}`);
  console.log(`  PSN:    ${psnOk ? '✅ PASS' : 'ℹ️  N/A'}`);

  const allPassed = steamOk && xboxOk && psnOk;
  console.log(`\n${allPassed ? '✅ All tests passed!' : '❌ Some tests failed'}\n`);

  if (!allPassed) {
    console.log('💡 To fix configuration issues:');
    console.log('   1. Check your .env file exists');
    console.log('   2. Verify all credentials are correct');
    console.log('   3. Restart Metro bundler after .env changes');
    console.log('   4. See docs/SETUP.md for detailed instructions\n');
  }
}

// Run tests if executed directly
if (require.main === module) {
  testAllCredentials();
}
```

**Add npm script** (package.json):

```json
{
  "scripts": {
    "test:credentials": "ts-node src/config/testCredentials.ts"
  }
}
```

#### Step 5: Configure EAS Secrets (for Production Builds)

```bash
# Install EAS CLI if not already installed
npm install -g eas-cli

# Login to Expo
eas login

# Configure secrets for production
eas secret:create --scope project --name STEAM_API_KEY --value "your_steam_key"
eas secret:create --scope project --name XBOX_CLIENT_ID --value "your_xbox_client_id"
eas secret:create --scope project --name XBOX_CLIENT_SECRET --value "your_xbox_secret"
eas secret:create --scope project --name XBOX_TENANT_ID --value "your_tenant_id"
```

**Update app.config.js** (or app.json → app.config.js):

```javascript
module.exports = {
  expo: {
    name: 'GameDuel',
    // ... other config
    extra: {
      steamApiKey: process.env.STEAM_API_KEY,
      xboxClientId: process.env.XBOX_CLIENT_ID,
      xboxClientSecret: process.env.XBOX_CLIENT_SECRET,
      xboxTenantId: process.env.XBOX_TENANT_ID,
      psnEnabled: process.env.PSN_ENABLED || 'false',
    },
  },
};
```

#### Step 6: Update Documentation

**Create docs/CREDENTIAL_SETUP.md:**

```markdown
# Gaming Platform Credential Setup

## Overview

This guide explains how to configure gaming platform API credentials for local development.

## Prerequisites

- Completed Epic 2.5 Stories 2.5.1 and 2.5.2
- Obtained Steam API key
- Obtained Xbox Live credentials

## Setup Instructions

### 1. Copy Environment Template

\`\`\`bash
cp .env.example .env
\`\`\`

### 2. Fill in Credentials

Edit `.env` and add your actual credentials:

- Steam API key from Story 2.5.1
- Xbox Client ID, Secret, Tenant ID from Story 2.5.2

### 3. Test Configuration

\`\`\`bash
npm run test:credentials
\`\`\`

You should see ✅ for Steam and Xbox if configured correctly.

### 4. Restart Metro Bundler

After changing .env:
\`\`\`bash

# Stop Metro (Ctrl+C)

npm start -- --reset-cache
\`\`\`

## Troubleshooting

**"All tests fail"**

- Check .env file exists in project root
- Verify credentials are correct (no extra spaces)
- Restart Metro bundler

**"Steam API key invalid"**

- Verify key at https://steamcommunity.com/dev
- Ensure no spaces or quotes in .env

**"Xbox GUIDs invalid format"**

- Check Client ID and Tenant ID are proper GUIDs
- Copy directly from Azure Portal

## Security Notes

- NEVER commit .env file to git
- Share credentials via secure channel only
- Rotate secrets if accidentally exposed
```

### Verification Steps

1. `.env` file created with real credentials
2. `.env.example` committed to git
3. `npm run test:credentials` passes for Steam and Xbox
4. Team members can set up using documentation
5. Metro bundler recognizes environment variables

### Definition of Done

- [ ] Environment configuration created
- [ ] All credentials tested and working
- [ ] EAS secrets configured
- [ ] Documentation updated
- [ ] Team onboarded
- [ ] Security best practices followed
- [ ] Code reviewed and merged

### Blockers / Dependencies

- **Requires**: Story 2.5.1 (Steam credentials)
- **Requires**: Story 2.5.2 (Xbox credentials)
- **Requires**: Story 2.5.3 (PSN decision)
- **Requires**: Epic 0 complete (project initialized)

### Troubleshooting

**"Environment variables not loading"**

```bash
# Clear Metro cache
npm start -- --reset-cache

# Verify babel.config.js includes react-native-dotenv plugin
```

**"TypeScript errors on @env imports"**

```bash
# Ensure src/types/env.d.ts exists
# Restart TypeScript server in VS Code: Cmd+Shift+P → "Reload Window"
```

**"Test script fails to run"**

```bash
# Install ts-node if not present
npm install --save-dev ts-node

# Run with explicit loader
npx ts-node src/config/testCredentials.ts
```

### Time Estimate

- **Setup**: 1-2 hours
- **Testing**: 30 minutes
- **Documentation**: 30 minutes
- **Total**: 2-3 hours

### Important Notes

- This must be completed BEFORE Epic 3 starts
- All team members need to complete setup
- Credentials should be rotated periodically
- Keep EAS secrets in sync with latest credentials
- Document any credential changes in team notes

---

## Epic 2.5 Summary

### Timeline Overview

```
Week 0-1:  Stories 2.5.1, 2.5.2 (START IMMEDIATELY - USER ACTIONS)
  ├─ Day 1: Register Steam API key (15-30 min)
  └─ Day 2-3: Register Xbox Live app (2-3 hours)

Week 1-8:  Wait for platform approvals (happens during Epic 1 & 2)
  ├─ Steam: Instant approval ✅
  ├─ Xbox: Usually instant, may take 1-3 days ⏱️
  └─ Story 2.5.3: Research PSN options (ongoing)

Week 8:    Story 2.5.4 (BEFORE Epic 3)
  └─ Configure environment variables (2-3 hours)

Week 9+:   Epic 3 can proceed without blockers ✅
```

### Total Estimated Effort

- **User Actions**: 3-5 hours active work
- **Wait Time**: 0-7 days (platform approvals)
- **Developer Actions**: 2-3 hours (Story 2.5.4)
- **Total Calendar Time**: 1-2 weeks (if started in Week 0)

### Critical Success Factors

✅ **Start immediately** - don't wait for Epic 0 to finish  
✅ **Secure credential handling** - never commit secrets  
✅ **Complete before Week 8** - must not block Epic 3  
✅ **Document everything** - team needs clear setup guide  
✅ **Test thoroughly** - verify all credentials work

### Story Dependencies

```
2.5.1 (Steam) ────┐
2.5.2 (Xbox)  ────┼────> 2.5.4 (Configure)
2.5.3 (PSN)   ────┘
```

### Post-Epic Deliverables

- ✅ Steam Web API key obtained and working
- ✅ Xbox Live application registered with OAuth credentials
- ✅ PSN strategy decided and documented
- ✅ All credentials securely configured in development environment
- ✅ Test scripts verify credentials work
- ✅ Team documentation complete
- ✅ Epic 3 (Gaming Integration) unblocked

### Risks & Mitigations

| Risk                      | Likelihood | Impact | Mitigation                              |
| ------------------------- | ---------- | ------ | --------------------------------------- |
| Platform approval delays  | Low        | High   | Start Week 0, have fallback plan        |
| Credentials lost/exposed  | Low        | High   | Secure storage, rotation process        |
| PSN unofficial API breaks | Medium     | Medium | Graceful degradation, defer to post-MVP |
| Team setup confusion      | Low        | Medium | Clear documentation, support process    |

---

## Handoff Notes

### To Development Team

Once Epic 2.5 is complete, you'll have:

- ✅ Steam API key ready to use in Epic 3 Story 3.2
- ✅ Xbox credentials ready for Epic 3 Story 3.5
- ✅ PSN approach decided for Epic 3 Story 3.7
- ✅ Environment configuration working locally
- ✅ Test scripts to verify setup

### To Product Owner

Remember to:

- 🔄 Rotate credentials every 12-24 months
- 📅 Calendar reminder for Xbox secret expiration (24 months)
- 📊 Track if PSN absence impacts user adoption
- 🤝 Begin Sony partnership application after MVP launch (if needed)

### Next Epic

**Epic 3: Gaming Platform Integrations** can now proceed without credential blockers!

---

**Epic 2.5 Status**: ✅ Ready to Start (IMMEDIATELY)  
**Last Updated**: 2025-10-23  
**Epic Owner**: Product Owner (User Actions) + Tech Lead (Developer Actions)  
**CRITICAL**: Start Stories 2.5.1 and 2.5.2 THIS WEEK!
