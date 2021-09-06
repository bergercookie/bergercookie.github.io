---
layout: page-no-banner
title: Taskwarrior - GCal Sync
permalink: /projects/taskw-gcal-sync
published: true
---

<p align="center">
   <img src="/images/taskwarrior.png" width="30%" />
</p>

Synchronization between Taskwarrior tasks and Google Calendar events-reminders.

## Overview

`taskw_gcal_sync` provides a solution for bidirectional synchronisation between
Taskwarrior and Google Calendar. Given a Calendar name for Google Calendar and a
filter for Taskwarrior (currently only a single tag is supported and tested)
synchronise all the events between them.

Overall, it supports synchronisation on the following events:

- Creation of an event
- Modification of events
- Deletion of an event

The aforementioned features should work bidirectional, meaning a reminder
created, modified, or deleted from Google Calendar should also be created,
modified, or deleted respectively in TaskWarrior and vice-versa.

For more info see the repository on Github.

## Links

- [Code Repository](https://github.com/bergercookie/taskw_gcal_sync)
- [Privacy Policy](/taskw-gcal-sync-privacy-policy)
