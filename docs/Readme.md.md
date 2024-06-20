# Setup nfs server

## Server side
### Install nfs server
```
apt update && apt install nfs-kernel-server -y
```
![alt text](image.png)

### Create the folder to share
```
mkdir <Path_To_Share_Folder>
```
![alt text](image-1.png)
### export the nfs server
```
vi /etc/exports
```
```
<Path_To_Share_Folder> <Client_Server_IP>(rw,sync,no_subtree_check)
```
![alt text](image-3.png)
![alt text](image-2.png)

### Restart the NFS service
```
systemctl restart nfs-server.service && systemctl status nfs-server.service
```
![alt text](image-4.png)

### Check that the share folder as been exported
```
exportfs -v
```
![alt text](image-5.png)

## Client Side
### Install nfs client
```
apt update && apt install nfs-common -y
```
![alt text](image-6.png)

### Create a directory on the client machine where you want to mount the NFS share
```
sudo mkdir -p <Path_To_Mount_Point>
```
![alt text](image-7.png)

### Mount the nfs volume
```
mount <nfs_server_ip>:<remote_path> <Path_To_Mount_Point>
```
![alt text](image-8.png)

### To make the mount persistent across reboots, add an entry to the /etc/fstab
```
vi /etc/fstab
```
```
<nfs_server_ip>:<remote_path> <Path_To_Mount_Point> nfs defaults 0 0 
```
![alt text](image-10.png)
![alt text](image-9.png)

### Run the following command to mount all file Systems specified in /etc/fstab
```
mount -a
```
![alt text](image-11.png)