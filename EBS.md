EBS
===
* [General](https://docs.aws.amazon.com/en_en/AWSEC2/latest/UserGuide/EBSVolumes.html):
  * When you create an EBS volume in an Availability Zone, it is automatically replicated within that zone to prevent data loss due to failure of any single hardware component. Thus, a volume can't "survive" an Availability Zone general failure (data is only replicated within one AZ).
  * An EBS volume is off-instance storage that can persist independently from the life of an instance.
  * An EBS volume can only be attached to one EC2 instance at a time in the same AZ.
  * EBS volumes support live configuration changes while in production which means that you can modify the volume type, volume size, and IOPS capacity without service interruptions. 
  * By default, EBS volumes (both EBS and instance-store) that are created and attached to an instance at launch are **deleted when that instance is terminated**. This can be changed by setting the `DeleteOnTermination` flag to `false`.
* [Types](https://docs.aws.amazon.com/en_en/AWSEC2/latest/UserGuide/EBSVolumeTypes.html):
  * General Purpose SSD (gp2): Max 10,000 IOPS. Good balance between performance and cost.
  * Provisioned IOPS SSD (io1): Max 32,000 IOPS. Best performance, most expensive.
  * Throughput Optimized HDD (st1): Max 500 IOPS. Low cost, fastest HDD available.
  * Cold HDD (sc1): Max 250 IOPS: Lowest cost, slowest disk.
  * 50:1 is the maximum ratio of provisioned IOPS to requested volume size in Gibibyte (GiB).
  * The maximum size for a EBS volume is 16TiB.
* [Snapshots](https://docs.aws.amazon.com/es_es/AWSEC2/latest/UserGuide/EBSSnapshots.html):
  * Snapshots are incremental (the first one may take a while).
  * Snapshots can be done with the volume in use (and you can keep using it while the snapshot is in progress).
  * Snapshots can be scheduled with **[Amazon Data Lifecycle Manager (Amazon DLM)](https://docs.aws.amazon.com/en_en/AWSEC2/latest/UserGuide/snapshot-lifecycle.html)**.
  * Snapshots of encrypted volumes are automatically encrypted.
  * Volumes that are created from encrypted snapshots are automatically encrypted.
  * When you copy an unencrypted snapshot that you own, you can encrypt it during the copy process.
  * When you copy an encrypted snapshot that you own, you can reencrypt it with a different key during the copy process.
  * You can create a copy of a volume on a different AZ by making a snapshot and restore it to the new volume.
* [Encryption](https://docs.aws.amazon.com/en_en/AWSEC2/latest/UserGuide/EBSEncryption.html):
  * The following data can be encrypted:
    * Data at rest inside the volume
    * All data moving between the volume and the instance
    * All snapshots created from the volume
    * All volumes created from those snapshots
  * You can use your own-keys or Amazon-managed keys to encrypt EBS volumes with KMS.
