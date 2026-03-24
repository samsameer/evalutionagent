# Organization Policies & Seat Management

**Module 11, Lesson 3 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

For teams and organizations, Copilot admin controls let you manage who has access, what features are enabled, and how Copilot behaves across your organization.

---

## Seat Management

### Assigning Seats

1. Go to **Organization Settings** → **Copilot** → **Access**
2. Choose assignment method:

| Method | Description |
|--------|-------------|
| **All members** | Every org member gets Copilot access |
| **Selected teams** | Only members of specific teams get access |
| **Selected members** | Individually assign seats |

### Monitoring Seat Usage

The admin dashboard shows:
- Total seats purchased vs. assigned
- Active users (used Copilot in the last 30 days)
- Inactive seats (assigned but not used)
- Pending invitations

---

## Policy Controls

### Feature Policies

| Policy | Options | Default |
|--------|---------|---------|
| **Code completions** | Enabled / Disabled | Enabled |
| **Copilot Chat** | Enabled / Disabled | Enabled |
| **Copilot CLI** | Enabled / Disabled | Enabled |
| **Agent mode** | Enabled / Disabled | Enabled |
| **Copilot Edits** | Enabled / Disabled | Enabled |
| **Coding Agent** | Enabled / Disabled | Disabled |
| **Public code filter** | Block / Allow / Warn | Warn |
| **Model selection** | Allow all / Restrict models | Allow all |

### Public Code Filter

Controls how Copilot handles suggestions that match public code:

| Setting | Behavior |
|---------|----------|
| **Block** | Suggestions matching public code are not shown |
| **Allow** | All suggestions shown, with reference info when matching |
| **Warn** | Show suggestion with a warning about public code match |

---

## Audit Logs

Business and Enterprise plans include **audit logs** for Copilot activity:

| Event Logged | Description |
|-------------|-------------|
| Seat assigned | A Copilot seat was assigned to a member |
| Seat removed | A Copilot seat was removed |
| Policy changed | An admin changed a Copilot policy |
| Content exclusion updated | Exclusion rules were modified |
| Feature toggled | A feature was enabled or disabled |

Access audit logs at: **Organization Settings** → **Audit Log** → filter by "copilot"

---

## Best Practices for Org Admins

1. **Start with a pilot** — Roll out to one team first, gather feedback
2. **Monitor adoption** — Track active vs. inactive seats monthly
3. **Enable public code filter** — Protect against license issues
4. **Configure content exclusions** — Identify sensitive repos immediately
5. **Set up SSO** — For Enterprise, integrate with your identity provider
6. **Communicate policies** — Let developers know what is enabled and why
7. **Review audit logs** — Monthly review of Copilot-related events

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 11: Security & Admin](README.md) |
| Previous Lesson | [Content Exclusions](content-exclusions.md) |
| Next Lesson | [IP Indemnity & Code Referencing](ip-indemnity.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
