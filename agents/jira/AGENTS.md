# Jira Manager Agent Configuration

* agent prompt: [jira-manager](.opencode/agent/jira-manager.md) will be managing these tickets
* only focus on Jira project 'MYD: MY Software Engineering'
* only interact with Jira project 'MYD: MY Software Engineering'
* unresolved tickets only
* put the manipulated tickets with actions in [agents/jira-manager/TODO.md](agents/jira-manager/TODO.md)
* always ask which specific tickets/issue IDs to change (i.e. MYD-1, MYD-2)

## Tickets

### Jira Tickets Snapshot 11-19-2025

[Jira: Current Ticket List (Google Sheet)](https://docs.google.com/spreadsheets/d/1S-w4f6N9F84pUDXVKQdRqiqqvnjcf8vGxhxujmlG8dg/edit?gid=1806480038#gid=1806480038)

### Jira API Reference

* "projectIdOrKey":"MYD"

### getAccessibleAtlassianResources Output
```json
[{"id":"c4b4e301-6c65-41b0-b962-37930a556a65","url":"https://mindyou.atlassian.net","name":"mindyou","scopes":["read:jira-work","write:jira-work"],"avatarUrl":"https://site-admin-avatar-cdn.prod.public.atl-paas.net/avatars/240/jersey.png"}]
```

### atlassianUserInfo Output
```json
{"account_id":"627a1d3ba20bd0006fd98447","email":"boaz@mindyou.com.ph","name":"Boaz Sze","picture":"https://avatar-management--avatars.us-west-2.prod.public.atl-paas.net/627a1d3ba20bd0006fd98447/6c7ca1eb-692d-4b62-a99d-dddcfa048ffd/128","account_status":"active","characteristics":{"not_mentionable":false},"last_updated":"2024-06-26T17:04:32.227Z","created_at":"2022-05-10T08:07:23.335Z","nickname":"Boaz Sze","zoneinfo":"Asia/Singapore","locale":"en-US","extended_profile":{"job_title":"Lead Software Engineer","organization":"Mind You Mental Health Systems","department":"Tech","location":"Manila, Philippines","phone_numbers":[],"team_type":"Software Development"},"account_type":"atlassian","email_verified":true}
```

### getTransitionsForJiraIssue Output (Sample using MYD-601)
```json
{
  "expand": "transitions",
  "transitions": [
    {
      "id": "11",
      "name": "To Do",
      "to": {
        "self": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/rest/api/3/status/10000",
        "description": "",
        "iconUrl": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/",
        "name": "To Do",
        "id": "10000",
        "statusCategory": {
          "self": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/rest/api/3/statuscategory/2",
          "id": 2,
          "key": "new",
          "colorName": "blue-gray",
          "name": "To Do"
        }
      },
      "hasScreen": false,
      "isGlobal": true,
      "isInitial": false,
      "isAvailable": true,
      "isConditional": false,
      "isLooped": false
    },
    {
      "id": "21",
      "name": "In Progress",
      "to": {
        "self": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/rest/api/3/status/3",
        "description": "This work item is being actively worked on at the moment by the assignee.",
        "iconUrl": "https://mindyou.atlassian.net/images/icons/statuses/inprogress.png",
        "name": "In Progress",
        "id": "3",
        "statusCategory": {
          "self": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/rest/api/3/statuscategory/4",
          "id": 4,
          "key": "indeterminate",
          "colorName": "yellow",
          "name": "In Progress"
        }
      },
      "hasScreen": false,
      "isGlobal": true,
      "isInitial": false,
      "isAvailable": true,
      "isConditional": false,
      "isLooped": false
    },
    {
      "id": "31",
      "name": "Done",
      "to": {
        "self": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/rest/api/3/status/10001",
        "description": "",
        "iconUrl": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/",
        "name": "Done",
        "id": "10001",
        "statusCategory": {
          "self": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/rest/api/3/statuscategory/3",
          "id": 3,
          "key": "done",
          "colorName": "green",
          "name": "Done"
        }
      },
      "hasScreen": false,
      "isGlobal": true,
      "isInitial": false,
      "isAvailable": true,
      "isConditional": false,
      "isLooped": false
    },
    {
      "id": "51",
      "name": "On Hold",
      "to": {
        "self": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/rest/api/3/status/10010",
        "description": "This is when issues cannot be solved without extra actions outside the assigned",
        "iconUrl": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/",
        "name": "Blocked",
        "id": "10010",
        "statusCategory": {
          "self": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/rest/api/3/statuscategory/4",
          "id": 4,
          "key": "indeterminate",
          "colorName": "yellow",
          "name": "In Progress"
        }
      },
      "hasScreen": false,
      "isGlobal": true,
      "isInitial": false,
      "isAvailable": true,
      "isConditional": false,
      "isLooped": false
    },
    {
      "id": "81",
      "name": "For QA",
      "to": {
        "self": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/rest/api/3/status/10029",
        "description": "This status is for testing and review",
        "iconUrl": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/",
        "name": "Staging",
        "id": "10029",
        "statusCategory": {
          "self": "https://api.atlassian.com/ex/jira/c4b4e301-6c65-41b0-b962-37930a556a65/rest/api/3/statuscategory/4",
          "id": 4,
          "key": "indeterminate",
          "colorName": "yellow",
          "name": "In Progress"
        }
      },
      "hasScreen": false,
      "isGlobal": true,
      "isInitial": false,
      "isAvailable": true,
      "isConditional": false,
      "isLooped": false
    }
  ]
}
```

## Statuses
*from `statuses.json`*

| ID | Name |
|---|---|
| 10000 | To Do |
| 3 | In Progress |
| 10001 | Done |
| 10010 | Blocked |
| 10029 | Staging |