# howto-move-linux-mount-to-a-new-disk

this is more a personal not for myself rather then a bullet-proof instruction. It worked for me though.

Still you should rather use it with care an on your own risk.

# 1.) add new disk/patition to your system and mount it to a temporary mountpoint

`mkdir /mnt/temp`

`sudo mount /dev/sdx1 /mnt/temp`


# 2.) `rsync` or `cp` content of the folder you want to move to the new mount

`rsync -azv /var/lib/docker/ /mnt/temp`   or

`cp -ar /var/lib/docker/ /mnt/temp`

#3.) unmount the temporay mounted new partition

sudo umount /mnt/temp

#4.) stop the docker daemon

`sudo service docker stop'

#5.) rename the current var/lib/docker

`sudo mv /var/lib/docker/ /var/lib/docker-legacy

#6.) mount the new artition to the location you want to replace

sudo mount /dev/sdx1 /var/lib/docker

#7.) start the docker daemon

`sudo service docker start`

#8.) check whether docker works

`docker ps -a`

`docker info`

`docker images`

`...`

#9.) delete the legacy docker folder

`sudo rm -r /var/lick/docker-legacy`
