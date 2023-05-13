---
title: "How to make secondary EBS volume primary root volume with data migration"
datePublished: Sat May 13 2023 15:55:24 GMT+0000 (Coordinated Universal Time)
cuid: clhm659ad000009l78vxbameu
slug: how-to-make-secondary-ebs-volume-primary-root-volume-with-data-migration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683992799637/cd50779f-15be-4993-bdc7-0c562cc217b2.png
tags: software-development, aws, developer, devops, beginners

---

## **📍 Introduction:**

Amazon Elastic Block Store (EBS) volumes are a key component of Amazon Web Services (AWS) that provide persistent storage for EC2 instances. When launching an EC2 instance, the instance's root volume is created from an Amazon Machine Image (AMI) or snapshot, and it can be attached to additional EBS volumes to store additional data. In some cases, it may be necessary to migrate data from a secondary EBS volume to the root volume, making the second volume the primary root volume. This blog post will walk you through the process of making a secondary EBS volume the primary root volume with data migration.

## **📍** Prerequisites:

Before proceeding with the migration, you should have the following:

* An EC2 instance running on AWS
    
* A secondary EBS volume attached to the EC2 instance
    
* Familiarity with AWS CLI and Linux commands
    

## **🔹** Step 1: Verify EBS Volume Status

Before making any changes to your EC2 instance, it is important to verify the status of your EBS volumes. To do this, you can use the AWS CLI to list all the volumes attached to the instance:

```plaintext
aws ec2 describe-volumes --filters Name=attachment.instance-id,Values=<instance-id> --query "Volumes[*].Attachments[*].{ID:VolumeId,State:State}"
```

Replace `<instance-id>` with the ID of your EC2 instance. This command will return a list of all the volumes attached to your instance along with their state.

## **🔹** Step 2: Create a Snapshot of the Secondary Volume

To ensure that you don't lose any data during the migration process, you should create a snapshot of the secondary EBS volume. You can do this using the following AWS CLI command:

```plaintext
aws ec2 create-snapshot --volume-id <secondary-volume-id> --description "Snapshot of secondary volume before migration"
```

Replace `<secondary-volume-id>` with the ID of your secondary EBS volume. This command will create a snapshot of the volume and return the ID of the new snapshot.

## **🔹** Step 3: Stop the Instance

Next, you will need to stop the EC2 instance to make changes to its root volume. You can do this using the AWS CLI with the following command:

```plaintext
aws ec2 stop-instances --instance-ids <instance-id>
```

Replace `<instance-id>` with the ID of your EC2 instance. This command will stop the instance and return the new state of the instance.

## **🔹** Step 4: Detach the Root Volume

Once the instance is stopped, you can detach the root volume from the instance. You can do this using the AWS CLI with the following command:

```plaintext
aws ec2 detach-volume --volume-id <root-volume-id>
```

Replace `<root-volume-id>` with the ID of your root volume. This command will detach the root volume from the instance and return the ID of the new detached volume.

## **🔹** Step 5: Attach the Secondary Volume as the Root Volume

With the root volume detached, you can now attach the secondary EBS volume as the new root volume. You can do this using the AWS CLI with the following command:

```plaintext
aws ec2 attach-volume --volume-id <secondary-volume-id> --instance-id <instance-id> --device /dev/xvda
```

Replace `<secondary-volume-id>` with the ID of your secondary EBS volume, `<instance-id>` with the ID of your EC2 instance, and `/dev/xvda` with the device name of your new root volume. This command will attach the secondary volume as the new root volume.

## **🔹** Step 6: Start the Instance

With the new root volume attached, you can now start the EC2 instance. You can do this using the AWS CLI with the following command:

```plaintext
aws ec2 start-instances --instance-ids <instance-id>
```

Replace `<instance-id>` with the ID of your EC2 instance. This command will start the instance with the new root volume attached.

## **🔹** Step 7: Mount the Secondary Volume

Now that the secondary EBS volume is the new root volume, you will need to mount the old root volume as a secondary volume to access any data that was previously stored on it. You can do this using the following Linux commands:

1. List the available block devices to find the name of the secondary volume:
    

```plaintext
lsblk
```

1. Create a mount point for the secondary volume:
    

```plaintext
sudo mkdir /mnt/secondary
```

1. Mount the secondary volume to the mount point:
    

```plaintext
sudo mount /dev/xvdf1 /mnt/secondary
```

Replace `/dev/xvdf1` with the device name of your secondary volume.

## **🔹** Step 8: Copy Data from the Secondary Volume to the New Root Volume

With both volumes mounted, you can now copy data from the old root volume to the new root volume. You can do this using the following Linux command:

```plaintext
sudo cp -Rp /mnt/secondary/* /.
```

This command will copy all files and directories from the secondary volume to the new root volume.

## **🔹** Step 9: Update the /etc/fstab File

To ensure that the secondary volume is automatically mounted on each boot, you will need to update the `/etc/fstab` file with the following line:

```plaintext
/dev/xvdf1 /mnt/secondary ext4 defaults,nofail 0 2
```

This will mount the secondary volume to the `/mnt/secondary` directory on each boot.

## **🔹** Step 10: Remove the Old Root Volume

Finally, you can remove the old root volume to save on storage costs. You can do this using the AWS CLI with the following command:

```plaintext
aws ec2 delete-volume --volume-id <old-root-volume-id>
```

Replace `<old-root-volume-id>` with the ID of your old root volume. This command will permanently delete the old root volume.

## **📍** Conclusion:

In this blog post, we have walked through the process of making a secondary EBS volume the primary root volume with data migration. This process involves stopping the EC2 instance, detaching the old root volume, attaching the secondary volume as the new root volume, and copying data from the old root volume to the new root volume. While this process may seem complex, it is an important skill to have as it can help you optimize your AWS infrastructure and save on storage costs.

# **📍 Output:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678615052621/4226a059-e08d-4b32-a1ef-cbbb6ba17c43.png align="left")

## **🔹 Checkout GitHub Repository for projects:**

🔗 [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683909716692/b6161a02-f32e-4061-b3e2-cd707c70e44e.png?auto=compress,format&format=webp align="left")