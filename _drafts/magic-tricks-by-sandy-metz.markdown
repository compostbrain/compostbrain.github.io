---
layout: "post"
title: "Magic Tricks by Sandy Metz"
date: "2017-10-23 12:10"
---

## Unit Tests

### Goals:

- Thorough
- Stable
- Fast
- Few

#### Objects are simple

- Blackbox
- Focus on Messages
- Incoming
- Outgoing
- Sent to Self
- queries
- commands
- be careful when mixing

### Type is either query or command

#### Test incoming query messages by making assertions about what they send back

#### Test interface not the implementation
#### Don't test private methods except for early on to get it working
- if you must keep them: put a comment to delete if they fail

#### outgoing query methods
