Description
=======
GCal events to HipChat

Fetching data
=======
1h CRON that will fetch events that are scheduled for next 2h.
* It will be fetched from GCal (ical)
* It will save new event records in local db.
* It will check all existing scheduled events as they appear in the local db and:
* - If they don't appear in the feed, delete them from local db
* - if they appear and their schedule datetime was changed
* -- Update the event record
* -- If the new scheduled datetime is in more than 30m then current time, reset the notify flag

Notifier
=======
* 5m CRON that will fetch all events scheduled for the (next 30m and notify = false) OR (next 10m and notify = true) from the local db
* It will send an Hipchat notification to HipChat room with the following format:
[Event Title] - in Xm
(info) The hipchat notification should be set as alert (notify all users in the room about the new message in hipchat)
* Delete all events with notify = true after sending it to hipchat
