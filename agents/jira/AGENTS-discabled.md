# Jira Manager Agent Configuration

- agent prompt: [jira-manager](.opencode/agent/jira-manager.md) will be managing these tickets
- only focus on Jira project 'MYD: MY Software Engineering'
- only interact with Jira project 'MYD: MY Software Engineering'
- unresolved tickets only
- put the manipulated tickets with actions in [agents/jira-manager/TODO.md](agents/jira-manager/TODO.md)
- always ask which specific tickets/issue IDs to change (i.e. MYD-1, MYD-2)
- if Jira ticket is done, then remove it from [TODO.md](./TODO.md)
- if ticket summary has [SAMPLE], then add a "SAMPLE" label inside that jira ticket; if it has multiple [], then add all labels

## Tickets

### Jira Tickets Snapshot 11-19-2025

- [Jira: Current Ticket List (Google Sheet)](https://docs.google.com/spreadsheets/d/1S-w4f6N9F84pUDXVKQdRqiqqvnjcf8vGxhxujmlG8dg/edit?gid=1806480038#gid=1806480038)

* "projectIdOrKey":"MYD"

### getAccessibleAtlassianResources Output 
- use `cloud_id`: `c4b4e301-6c65-41b0-b962-37930a556a65`

### atlassianUserInfo Output use this for main account:
- `account_id`:`627a1d3ba20bd0006fd98447`
- `email`:`boaz@mindyou.com.ph`
- `name`:`Boaz Sze`,

### getTransitionsForJiraIssue Output all transitions/statuses:

| Goal        | Status Name  | Transition ID | Notes                                 |
|-------------|-------------|--------------|---------------------------------------|
| To Do       | To Do       | 11           | Moves ticket back to backlog/start.   |
| In Progress | In Progress | 21           | Starts work.                          |
| Done        | Done        | 31           | Resolves the ticket.                  |
| On Hold     | Blocked     | 51           | Moves to "Blocked" status.            |
| For QA      | Staging     | 81           | Moves to "Staging" status.            |

### Field IDs for Story Points
*   "Story point estimate": `customfield_10016`
*   "Story Points": `customfield_10026`
