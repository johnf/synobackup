# Synology Hyper Backup Scheduler

The main use case for this is when just setting up a backup and it might take a
few weeks to push everything up to the cloud. While this is happening you don't
want the backups causing you latency issues during the middle of the day.

Similarly for established backups you may occasionally upload large files that
exceed a sensible backup window.

## Configuration

This docker image will pause and resume all your Hyper Backup tasks on a
schedule of your choosing.

You will need to set the following environment variables

* **DSM** - The url to your DSM e.g. https://dsm.local:5001
* **USERNAME** - A username for your DSM with HyperBackup admin rights. Default
  to admin
* **PASSWORD** - The password for the above user
* **TZ** - Times default to GMT without a timezone e.g. Australia/Sydney

You can then control start and stop in two ways, first by setting an hour of the
day

* **START_HOUR** Time of the day to start backups e.g. 1 for 1am and 13 for 1pm
* **END_HOUR** Time of the day to end backups e.g. 1 for 1am and 13 for 1pm

or you can use crontab syntax

* **START_CRON** Time of the day to start backups e.g. "30 1 * * *" for 1:30am every day
* **END_CRON** Time of the day to end backups e.g. "30 1 * * *" for 1:30am every day

## WARNING

Be mindful that you need to allow enough time for your backups to complete.

# Development

Build the docker image

    docker build -t johnf/synology-hyperbackup-schedule .

Run the docker image manually

    docker run \
      -it \
      --rm \
      --name synology-hyperbackup-schedule \
      -e DSM=https://mrsnuff.home.inodes.org \
      -e PASSWORD=password \
      -e START_HOUR=1 \
      -e END_HOUR=7 \
      -e TZ="Australia/Sydney" \
      johnf/synology-hyperbackup-schedule

