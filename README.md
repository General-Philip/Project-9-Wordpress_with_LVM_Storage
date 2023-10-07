# Project-9-Wordpress_with_LVM_Storage

The Implementing Wordpress website with LVM storage with management System Project was divided into 6 steps in terms of its practical implementation

**STEP 1: WEB SERVER PREPARATION**

Below are the processes followed;

1. An ec2 instance that served as our **Webserver** was lunched.
2. Three volumes were created in the webserver ec2, each of 10GiB
3. The **webserver** was then connected to our linux terminal through rhel 9.2 using the command **ssh -i < name >.pem ec2-user@ < public ip address >**
4. The **lsblk** command was used to inspect what blocks are attached to the **webserver**
5. The **df -h** command was used to see all mount and free space on the **webserver**
6. Single partition was created on each disk using the **gdisk** command.
7. **LVM2** was installed
8.  The three disk was marked as physical volumes
9.  All three disks were added to Volumes Group
10.  lv create utility was used to create two logical volumes; **apps-lv** and **log-lv**
11.  The two logical volumes created were formatted with **mkfs.ext4**
12.  **/var/www/html** directory was created and was mounted on **apps-lv**
13.  **/home/recovery/logs** directory was created and was used to backup **/var/logs** directory using the **rsync** command
14.  **/var/log** directory was mounted on **log-lv**
15.  **/etc/fstab** was updated so that the configuration would persist after restart of the server.
16.  The configuration was tested and daemon reloaded with these two commands; **sudo mount -a** and **sudo systemctl daemom-reload**

**STEP 2: PREPARE THE DATABASE SERVER**

Below are the processes followed;

1. An ec2 instance that served as our **database server** was lunched.
2. Three volumes were created in the database server ec2, each of 10GiB
3. The **database server** was then connected to our linux terminal through rhel 9.2 using the command **ssh -i < name >.pem ec2-user@ < public ip address >**
4. The **lsblk** command was used to inspect what blocks are attached to the **database server**
5. The **df -h** command was used to see all mount and free space on the **database server**
6. Single partition was created on each disk using the **gdisk** command.
7. **LVM2** was installed
8.  The three disk was marked as physical volumes
9.  All three disks were added to Volumes Group
10.  lv create utility was used to create two logical volumes; **db-lv** and **log-lv**
11.  The two logical volumes created were formatted with **mkfs.ext4**
12.  **/db** directory was created and was mounted on **db-lv**
13.  **/home/recovery/logs** directory was created and was used to backup **/var/logs** directory using the **rsync** command
14.  **/var/log** directory was mounted on **log-lv**
15.  **/etc/fstab** was updated so that the configuration would persist after restart of the server.
16.  The configuration was tested and daemon reloaded with these two commands; **sudo mount -a** and **sudo systemctl daemom-re

**STEP 3: INSTALLING WORDPRESS ON YOUR WEBSERVER**

Below are the process followed;

1. Repository was updated
2. wget,apache and its dependencies were installed
3. Apache was started
4. PHP and its dependencies were installed
5. Wordpress was downloaded and copied to **/var/www/html**
6. SElinux policies was configured

**STEP 4: INSTALL MYSQL ON THE DATABASE SERVER**

Below are the process followed;

1. Repository was updated
2. Mysql server was installed using the command **sudo yum install mysql-server**
3. Mysql was started

**STEP 5: CONFIGURE DATABASE SERVER TO WORK ON WORDPRESS**

Below are the process followed;

1. Open mysql terminal
2. Create database
3. Create user
4. Grant all on privileges
5. Flush privileges
6. Exit mysql terminal

**STEP 6: CONFIGURE WORDPRESS TO CONNECT TO REMOTE DATABASE**

1. Port 3306 was opened on both the **webserver** and the **database server**
2. Permission and configuration was changed so apache could use wordpress
3. TCP port 80 was enabled in the **web server** to listen from anywhere
4. I accssed the browser to link to wordpress using **http:// web_server_public_ip_address/wordpress/**

The project was challenging and intresting. Below are screenshots of my journey;

![partitioning](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/4e969caa-5c52-4d45-bd36-7cfadb8c3285)
![mount confirmation](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/9100f8f7-9dae-49a8-a6c1-1d08bf5e90c8)
![logical volume created](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/072ba1aa-ba6d-4dc9-b773-8c58943b7b72)
![ext4 format](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/4f7e0019-9c0f-49e6-af2f-e6bc90c4c31f)
![SElinux configuration](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/fa0b4e71-6bf4-443d-952b-57dd88399d58)
![physical volume creation](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/0d06e015-0d96-4374-922b-433bd2c7f16a)
![physical volume check](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/91732099-3a0a-41ca-9cb3-1c04af46d850)
![php running](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/d0164183-f7c7-4476-bab0-9607210fa0f5)
![volume group](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/362199ad-7fa5-4f02-bd6f-98dc6ee5c9db)
![uuid](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/15ade496-1a19-4122-bc19-a08977b004b1)
![setup verification](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/e283d4e3-d0a5-49d4-8f40-bb6d932f4209)
![servers interating](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/9dfa0f60-08c3-4a0e-b5db-6695b1dc9f48)
![wordpress installation](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/4f240c02-1d4b-4c44-9d23-fc351240a21d)
![Wordpress home page](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/1744da5f-78c6-449f-ae41-562df505bb10)
![wget,apache and dependencies installation](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/7631cceb-66d4-4a4d-9706-5ae06b4c855d)
![Volumes created](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/b5c525e2-2441-4a9e-afbd-6e3f4af33655)
![volumes confirmation, lsblk](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/7bfed7e7-e9f0-480c-8f91-2f0c15ba3922)
![Volumes attached](https://github.com/General-Philip/Project-9-Wordpress_with_LVM_Storage/assets/141147192/088a6d32-3df5-4bce-ba01-02b65312cc36)








