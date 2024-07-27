# Amazon EC2 Instance Storage and Amazon Elastic Block Store

When an EC2 instance is initialized it is necessary to have an associated block storage, this can either be a local unit for booting the system, or a remote volume. Similarly to the internal and external storage that can be used in a computer, in EC2 the corresponding parts are EC2 instance store and EBS (Elastic block store).

The lifecycle of the instance store is associated with the instance itself, so if the latter is terminated then the data stored on the former is lost. Thus, this is also called ephemeral storage.

The choice between instance store and EBS usually relates to the necessity of persistence of the data, while which EBS type of storage leads to another line of questioning. Basically, these are divided into two main categories: SSD backed volumes and HDD backed volumes.

# Reading 3.2: Amazon EC2 Instance Storage and Amazon Elastic Block Store

## Amazon EC2 Instance Store

Amazon EC2 Instance Store provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer. This ties the lifecycle of your data to the lifecycle of your EC2 instance. If you delete your instance, the instance store is deleted as well. Due to this, instance store is considered ephemeral storage. Read more about it in the [AWS documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html).

Instance store is ideal if you are hosting applications that replicate data to other EC2 instances, such as Hadoop clusters. For these cluster-based workloads, having the speed of locally attached volumes and the resiliency of replicated data helps you achieve data distribution at high performance. It’s also ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content.

## Amazon Elastic Block Storage (Amazon EBS)

As the name implies, Amazon EBS is a block-level storage device that you can attach to an Amazon EC2 instance. These storage devices are called Amazon EBS volumes. EBS volumes are essentially drives of a user-configured size attached to an EC2 instance, similar to how you might attach an external drive to your laptop.

EBS volumes act similarly to external drives in more than one way:

- Most Amazon EBS volumes can only be connected with one computer at a time. Most EBS volumes have a one-to-one relationship with EC2 instances, so they cannot be shared by or attached to multiple instances at one time. Note: Recently, AWS announced the Amazon EBS multi-attach feature that enables volumes to be attached to multiple EC2 instances at one time. This feature is not available for all instance types and all instances must be in the same Availability Zone. Read more about this scenario in the [EBS documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes-multi.html).
- You can detach an EBS volume from one EC2 instance and attach it to another EC2 instance in the same Availability Zone, to access the data on it.
- The external drive is separate from the computer. That means, if an accident happens and the computer goes down, you still have your data on your external drive. The same is true for EBS volumes.
- You’re limited to the size of the external drive, since it has a fixed limit to how scalable it can be. For example, you may have a 2 TB external drive and that means you can only have 2 TB of content on there. This relates to EBS as well, since volumes also have a max limitation of how much content you can store on the volume.

### Scale Amazon EBS Volumes

You can scale Amazon EBS volumes in two ways:

- Increase the volume size, as long as it doesn’t increase above the maximum size limit. For EBS volumes, the maximum amount of storage you can have is 16 TB. That means if you provision a 5 TB EBS volume, you can choose to increase the size of your volume until you get to 16 TB.
- Attach multiple volumes to a single Amazon EC2 instance. EC2 has a one-to-many relationship with EBS volumes. You can add these additional volumes during or after EC2 instance creation to provide more storage capacity for your hosts.

### Amazon EBS Use Cases

Amazon EBS is useful when you need to retrieve data quickly and have data persist long-term. Volumes are commonly used in the following scenarios:

- **Operating systems:** Boot/root volumes to store an operating system. The root device for an instance launched from an Amazon Machine Image (AMI) is typically an Amazon EBS volume. These are commonly referred to as EBS-backed AMIs.
- **Databases:** A storage layer for databases running on Amazon EC2 that rely on transactional reads and writes.
- **Enterprise applications:** Amazon EBS provides reliable block storage to run business-critical applications.
- **Throughput-intensive applications:** Applications that perform long, continuous reads and writes.

### Amazon EBS Volume Types

| Volume Type                  | Description                                                                                  | Use Cases                                                          | Volume Size   | Max IOPS/Volume | Max Throughput/Volume |
|------------------------------|----------------------------------------------------------------------------------------------|--------------------------------------------------------------------|---------------|------------------|------------------------|
| EBS Provisioned IOPS SSD     | Highest performance SSD designed for latency-sensitive transactional workloads               | I/O-intensive NoSQL and relational databases                       | 4 GB-16 TB    | 64,000           | 1,000 MB/s             |
| EBS General Purpose SSD      | General purpose SSD that balances price and performance for a wide variety of transactional workloads | Boot volumes, low-latency interactive apps, development, and test  | 1 GB-16 TB    | 16,000           | 250 MB/s               |
| Throughput Optimized HDD     | Low-cost HDD designed for frequently accessed, throughput intensive workloads                | Big data, data warehouses, log processing                          | 500 GB-16 TB  | 500              | 500 MB/s               |
| Cold HDD                     | Lowest cost HDD designed for less frequently accessed workloads                              | Colder data requiring fewer scans per day                          | 500 GB-16 TB  | 250              | 250 MB/s               |

There are two main categories of Amazon EBS volumes: solid-state drives (SSDs) and hard-disk drives (HDDs). SSDs provide strong performance for random input/output (I/O), while HDDs provide strong performance for sequential I/O. AWS offers two types of each. The following chart can help you decide which EBS volume is the right option for your workload.

### Benefits of Using Amazon EBS

Here are the following benefits of using Amazon EBS (in case you need a quick cheat sheet):

- **High availability:** When you create an EBS volume, it is automatically replicated within its Availability Zone to prevent data loss from single points of failure.
- **Data persistence:** The storage persists even when your instance doesn’t.
- **Data encryption:** All EBS volumes support encryption.
- **Flexibility:** EBS volumes support on-the-fly changes. You can modify volume type, volume size, and input/output operations per second (IOPS) capacity without stopping your instance.
- **Backups:** Amazon EBS provides you the ability to create backups of any EBS volume.

## EBS Snapshots

Errors happen. One of those errors is not backing up data, and then, inevitably losing that data. To prevent this from happening to you, you should back up your data—even in AWS. Since your EBS volumes consist of the data from your Amazon EC2 instance, you’ll want to take backups of these volumes, called snapshots.

EBS snapshots are incremental backups that only save the blocks on the volume that have changed after your most recent snapshot. For example, if you have 10 GB of data on a volume, and only 2 GB of data have been modified since your last snapshot, only the 2 GB that have been changed are written to Amazon Simple Storage Service (Amazon S3).

When you take a snapshot of any of your EBS volumes, these backups are stored redundantly in multiple Availability Zones using Amazon S3. This aspect of storing the backup in Amazon S3 will be handled by AWS, so you won’t need to interact with Amazon S3 to work with your EBS snapshots. You simply manage them in the EBS console (which is part of the EC2 console).

EBS snapshots can be used to create multiple new volumes, whether they’re in the same Availability Zone or a different one. When you create a new volume from a snapshot, it’s an exact copy of the original volume at the time the snapshot was taken.
