Rsync backup

This is a bash script that is build arround rsync.

It is used for creating backups of your data. It has the following features:
- Backups your data with the standard rsync command
- Keeps multiple backups of your data
- If data between 2 backups hasn't changed, it only is saved once (deduplication)
- You can provide multiple backup schemes to backup different data at different
  intervals
- E-mail rapports with the result of each backup

This makes sure you can fully automate your backups and keep a close eye on it
to seeif it all keeps working
