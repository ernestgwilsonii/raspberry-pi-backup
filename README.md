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
```