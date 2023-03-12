# systemd - Service for Backup

On plugging a prepared USB-Stick into the laptop (and it being decrypted by the OS), The GNUMED backup script is triggered to write onto the stick.

## Steps to follow

1. Prepare USB-Stick. Ideally LUKS-encrypted with a defined partition-name. The constraints are 11 chars, no spaces, and no hyphen as it ends up encoded and by that makes life harder in a few minutes). Write down the path the media is linked to, might be something like `run/media/username/given_name`.
1. Update `BACKUP_DIR` in `/etc/gnumed/gnumed-backup.conf` to the directory from above.
1. Check the actual name with `systemctl list-units -t mount` - should be something like `run-media-<username>-<the-given-name>`.
1. Update `Requires`, `After` and `WantedBy` in `gnumed-backup.service` with the actual name of the last step.
1. Copy `gnumed-backup.service` to `/etc/systemd/system`.
1. Remove USB-Stick (if not already done) and execute `systemctl enable gnumed-backup`

If you now enter the USB-Stick (after entering the password in case of LUKS), a new backup-file should show up after some seconds in case of a fresh gnumed-database. If not, check `journalctl -xe` or `systemctl status gnumed-backup` for potential reasons.

