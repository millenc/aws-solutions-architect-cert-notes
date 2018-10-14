EC2
===
* **General**:
  * Along with **Elastic MapReduce**, EC2 instance is a service that provides access to the underlying operating system.
  * [Instance metadata](https://docs.aws.amazon.com/es_es/AWSEC2/latest/UserGuide/ec2-instance-metadata.html) can be accessed with the URL: `http://169.254.169.254/latest/meta-data/`
* **Performance**:
  * To [improve disk performance](https://docs.aws.amazon.com/en_en/AWSEC2/latest/UserGuide/EBSPerformance.html) (throughout) you can: use a larger instance type or a RAID-0 configuration with multiple disks.
  * [Placement groups](https://docs.aws.amazon.com/en_en/AWSEC2/latest/UserGuide/EBSPerformance.html) can be used to improve network performance of closely related EC2 instances.
  * [Enhanced networking](https://docs.aws.amazon.com/en_en/AWSEC2/latest/UserGuide/enhanced-networking.html): can be used to improve network performance on [supported instance types](https://docs.aws.amazon.com/en_en/AWSEC2/latest/UserGuide/enhanced-networking.html#supported_instances).
* **Lifecycle**:
  * Instance-store backed EC2 instances **can not be stopped** (only running or terminated). All data is lost when such instance is terminated (ephemeral storage).
  * With **EC2-VPC** when you **stop an instance** it **retains it's associated Elastic IP address**. Also, every EBS volume keeps associated with the instance and the data persists. In most cases, the instance is migrated to different underlying hardware when it's restarted.
  * On **EC2-Classic**, however, the Elastic IP is disassociated (you are charged for not associated IP addresses).
  * You are only billed on the **running** state.
  * [Instance states](https://docs.aws.amazon.com/es_es/AWSEC2/latest/UserGuide/ec2-instance-lifecycle.html):
    * `pending` - The instance is preparing to enter the running state. An instance enters the pending state when it launches for the first time, or when it is restarted after being in the stopped state.
    * `running` - The instance is running and ready for use.
    * `stopping` - The instance is preparing to be stopped.
    * `stopped` - The instance is shut down and cannot be used. The instance can be restarted at any time.
    * `shutting-down` - The instance is preparing to be terminated.
    * `terminated` - The instance has been permanently deleted and cannot be restarted.
* **Spot instances**:
  * If the spot instance is terminated or stopped by Amazon during the first hoour, **there is no charge**.
  * If you terminate the instance, you will be **charged to the nearest second**.
  * If the Spot instance is **terminated or stopped by Amazon EC2 in any subsequent hour**, you will be charged for your usage to the **nearest second**.
  * If you are **running on Windows** and you terminate the instance yourself, you will be charged for an **entire hour**.
* **Cloudwatch monitoring**: Basically Cloudwatch can't monitor things that would require Amazon access to your EC2 instance like Memory utilization, Disk swap, etc.
  * [Available metrics](https://docs.aws.amazon.com/es_es/AWSEC2/latest/UserGuide/monitoring_ec2.html): CPU utilization, Network utilization, Disk performance and Disk Reads/Writes
  * NOT available metrics (out-of-the-box): Memory utilization, Disk swap utilization, Disk space utilization, Page file utilization, Log collection, etc.
  * There are 2 modes for monitoring: `Basic` with 5-minute period and free and `Detailed` with 1-minute period (paid). 
* **[Elastic Network Interfaces (ENIs)](https://docs.aws.amazon.com/en_en/AWSEC2/latest/UserGuide/using-eni.html)**:
  * You can attach a network interface to an instance when it's running (hot attach), when it's stopped (warm attach), or when the instance is being launched (cold attach).
  * You can detach secondary (ethN) network interfaces when the instance is running or stopped. However, you can't detach the primary (eth0) interface.
* **Limits**:
  * For new accounts, there's a soft limit of **20 EC2 instances per region** (you can contact Amazon to raise it).
