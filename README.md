# raspberry-pi-backup
Raspberry Pi Backup to S3

```
# REF: https://ownthe.cloud/posts/configure-aws-cli-on-raspberry-pi/
sudo apt-get install python3-pip
pip3 install awscli --upgrade --user
/home/pi/.local/bin/aws --version

export PATH=/home/pi/.local/bin:$PATH
aws --version

aws configure

aws s3 ls

# aws s3 sync /opt s3://landenberg-raspberrypi-backups/raspberrypi/opt/
BUCKET='s3://landenberg-raspberrypi-backups'
SERVER=$(hostname)
BACKUP_DIR=/opt
aws s3 sync $BACKUP_DIR $BUCKET/$SERVER$BACKUP_DIR

# AWS CLI supports the following environment variables:
# AWS_SHARED_CREDENTIALS_FILE – Specifies the location of the file that the AWS CLI uses to store access keys.
# AWS_CONFIG_FILE – Specifies the location of the file that the AWS CLI uses to store configuration profiles.
ls -alFh /home/pi/.aws
AWS_SHARED_CREDENTIALS_FILE=/home/pi/.aws/credentials
AWS_CONFIG_FILE=/home/pi/.aws/config
aws s3 ls $BUCKET


# Add to crontab when ready to run scheduled 
sudo bash -
pip3 install awscli --upgrade --user
crontab -e
# S3 Backups
AWS_SHARED_CREDENTIALS_FILE=/home/pi/.aws/credentials
AWS_CONFIG_FILE=/home/pi/.aws/config
BUCKET='s3://landenberg-raspberrypi-backups'
BACKUP_DIR=/opt
0 2 * * * /root/.local/bin/aws s3 sync $BACKUP_DIR $BUCKET/$(hostname)$BACKUP_DIR >> /tmp/s3_backups.log 2>&1
:wq!

# Review crontab
crontab -l

# Review logs
cat /tmp/s3_backups.log
#tail -f /tmp/s3_backups.log
```
