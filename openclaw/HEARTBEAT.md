# HEARTBEAT.md — Pending Tasks Checklist

Checked every 30 minutes by the agent. Update this file with tasks you want the agent to action during the next heartbeat.

## Pending Tasks

_[Add tasks here — agent will process and remove when done]_

- [ ] Check RSS for new blog posts
- [ ] Verify all scheduled posts were published successfully
- [ ] Update MEMORY.md with any new learnings

## Completed Tasks Log

_[Agent moves completed tasks here with timestamp]_

| Timestamp | Task | Status |
|---|---|---|
| | | |

## How to Use

To queue a task for the agent:
1. Add a `- [ ] task description` line under **Pending Tasks**
2. Agent picks it up at next heartbeat (within 30 mins)
3. Agent moves it to Completed Tasks Log when done

## Emergency Stop

To pause all automation, add this line to Pending Tasks:
```
- [ ] PAUSE_ALL: stop all automation until further notice
```
