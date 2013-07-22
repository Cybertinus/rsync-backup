Rsync backup

This is a bash script that is build arround rsync.

It is used for creating backups of your data. It has the following features:
- Backups your data with the standard rsync command.
- Keeps multiple backups of your data.
- If data between 2 backups hasn't changed, it is only saved once (deduplication).
- You can provide multiple backup schemes to backup different data at different
  intervals.
- E-mail rapports with the result of each backup.

This makes sure you can fully automate your backups and keep a close eye on it
to see if it all keeps working.

You need an external configurationfile before this script works. This file can
be named anything you want and placed everywhere you like (I find /etc/rsyncbackup/
a valid location). You tell this sript via the first argument where it can find
the external backupfile.
In this configfile you define what should be backupped and how long it should be
saved. In other words: This configfile is the core of your backups. The reason
this is a seperate file is that you can define more then one of them, and via
the first argument you specify which configfile you want to use in this run.
This way you can create multiple backup schemes and retention times easily.
This external configuration file doesn't have a lot of options, but it is
essential that you understand them good, to prevent bad things happening with
your backup. The options:
BACKUPDIRS: a comma seperated list of all the directories you want backupped.
            note: spaces in directories are supported.
SAVETIME:   the retention time you want on this particular backup. This consist
            of two parts: a number and a letter. The first is just a number,
			which tells 'how long' it should be saved.
			The second part is a letter that defines what the number represents.
			There are only a few letters valid for the second position:
			w: the number represents weeks
			d: the number represents days
			h: the number represents hours
			When a backup is stored longer then specified time here, it will be
			removed at the next run of the backup. But only when this external
			configurationfile is specified, not with other configfiles
To help you understand the external configurationfile better, here is an examplefile:
BACKUPDIRS="/etc,/root/,/home/user/Personal documents/"
SAVETIME="2d"

This file will backup the three directories name /etc, /root and
/home/user/Personal documents/
And when the backup is older as two days, it will be removed.

The deduplication of the data works with hardlinks. It is all based on the --link-dest
option of rsync. So see man rsync for all the details on how this works.

The directory you specify as BASEDESTDIR needs to be a seperate mountpoint. If
there isn't anything mounted on BASEDESTDIR, your backup will fail (with a
message reminding you of this).
This is done to prevent accidentally backing up a big directory from the /
partition to the / partition, causing the backup to loose most of it's value
(not on a seperate partition/other machine) and it could cause the / partition
to fill up completly (yes: been there, done that, got the t-shirt ;), when this
check wasn't in the script yet).

Hope this helps to make you understand the script better. When you have questions
please contact me via Github.
