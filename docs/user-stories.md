# User Stories

User stories are grouped by persona. Acceptance criteria are written in the *Given / When / Then* format.

---

## Citizen (General Member)

### US-01 — Register an account

**As a** citizen,  
**I want to** create an account with my email and a password,  
**so that** I can participate in votes.

**Acceptance criteria**

- **Given** I provide a valid email and a password meeting the strength requirements,  
  **When** I submit the registration form,  
  **Then** my account is created and I receive a confirmation email.
- **Given** I provide an email that is already registered,  
  **When** I submit the form,  
  **Then** I see an error message telling me the email is already in use (without revealing that an account exists, to prevent enumeration — a generic "check your inbox" response is acceptable).

---

### US-02 — Log in

**As a** citizen,  
**I want to** log in with my email and password,  
**so that** I can access my account and vote.

**Acceptance criteria**

- **Given** I provide correct credentials,  
  **When** I submit the login form,  
  **Then** I am authenticated and redirected to the home feed.
- **Given** I provide incorrect credentials,  
  **When** I submit the form,  
  **Then** I see a generic error (no hint as to which field is wrong) and am not logged in.
- **Given** I have MFA enabled,  
  **When** I provide correct credentials,  
  **Then** I am prompted for my TOTP code before being authenticated.

---

### US-03 — Browse proposals

**As a** citizen,  
**I want to** see a list of open proposals,  
**so that** I can decide which ones to participate in.

**Acceptance criteria**

- **Given** I am on the home feed,  
  **When** the page loads,  
  **Then** I see all currently open proposals ordered by closing date (soonest first).
- **Given** I apply a topic filter,  
  **When** the filter is applied,  
  **Then** only proposals in that topic are shown.

---

### US-04 — Cast a vote

**As a** citizen,  
**I want to** vote on an open proposal,  
**so that** my preference is counted.

**Acceptance criteria**

- **Given** I am authenticated and the proposal is open,  
  **When** I select an option and confirm,  
  **Then** my ballot is recorded and the tally updates in real time.
- **Given** I have already voted,  
  **When** I open the proposal,  
  **Then** my current choice is highlighted and I can change it while the proposal is still open.
- **Given** I change my vote,  
  **When** I confirm the change,  
  **Then** the old vote is replaced and the tally reflects the new choice.

---

### US-05 — Delegate a vote

**As a** citizen,  
**I want to** delegate my vote to a trusted person for a specific topic,  
**so that** my vote is still counted even when I don't have time to engage.

**Acceptance criteria**

- **Given** I search for another user by name,  
  **When** I select them and choose a scope (global, topic, or proposal),  
  **Then** a delegation is created and I see it in my delegation list.
- **Given** I have an active delegation and I vote directly on a proposal in that scope,  
  **When** my vote is recorded,  
  **Then** my direct vote takes precedence over the delegation for that proposal.

---

### US-06 — Revoke a delegation

**As a** citizen,  
**I want to** revoke a delegation I have previously granted,  
**so that** I regain full control of my vote.

**Acceptance criteria**

- **Given** I have an active delegation,  
  **When** I revoke it,  
  **Then** the delegation is immediately inactive and the delegate no longer holds my voting weight.

---

### US-07 — View the audit log

**As a** citizen,  
**I want to** view the audit log for a closed proposal,  
**so that** I can independently verify the result.

**Acceptance criteria**

- **Given** a proposal is closed,  
  **When** I navigate to the audit section,  
  **Then** I can see the hash-chained event list and verify the cryptographic chain.

---

## Delegate

### US-08 — View delegated weight

**As a** delegate,  
**I want to** see how much total voting weight I currently hold,  
**so that** I understand the responsibility placed on me.

**Acceptance criteria**

- **Given** I am a delegate,  
  **When** I view my profile or delegation dashboard,  
  **Then** I see the number of delegators and the total weight per topic and globally.

---

### US-09 — Vote on behalf of delegators

**As a** delegate,  
**I want to** cast a vote that automatically applies my delegated weight,  
**so that** all delegators are counted without individual action.

**Acceptance criteria**

- **Given** I cast a vote on a proposal,  
  **When** the ballot is recorded,  
  **Then** the option's tally includes my own vote plus all transitive delegated weight that has not been overridden by a direct vote.

---

## Administrator

### US-10 — Create a topic

**As an** administrator,  
**I want to** create and manage topic categories,  
**so that** proposals can be organised and delegations can be scoped.

**Acceptance criteria**

- **Given** I provide a unique topic name,  
  **When** I create the topic,  
  **Then** it appears in the topic list and can be assigned to proposals and delegations.

---

### US-11 — Moderate a proposal

**As an** administrator,  
**I want to** be able to close or archive any proposal,  
**so that** inappropriate content is removed promptly.

**Acceptance criteria**

- **Given** a proposal is open,  
  **When** I force-close it as an administrator,  
  **Then** no new votes can be cast and an audit event is recorded.

---

### US-12 — Manage user accounts

**As an** administrator,  
**I want to** deactivate a user account without deleting it,  
**so that** the audit history is preserved while access is revoked.

**Acceptance criteria**

- **Given** I deactivate a user account,  
  **When** that user attempts to log in,  
  **Then** they receive an "account deactivated" message and cannot access the platform.
