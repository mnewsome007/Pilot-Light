<h1>Pilot Light</h1>


<h2>Description</h2>
With the pilot light approach, you replicate your data from one Region to another and provision a copy of your core workload infrastructure. Resources required to support data replication and backup, such as databases and object storage, are always on. Other elements, such as application servers, are loaded with application code and configurations, but are “switched off” and are only used during testing or when disaster recovery failover is invoked. In the cloud, you have the flexibility to deprovision resources when you do not need them, and provision them when you do. A best practice for “switched off” is to not deploy the resource, and then create the configuration and capabilities to deploy it “switch on” when needed. Unlike the backup and restore approach, your core infrastructure is always available and you always have the option to quickly provision a full scale production environment by switching on and scaling out your application servers.
<br />

<h2>AWS Cloud Map</h2>
<p align="center">
<img src="https://i.imgur.com/rUJGwyx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />


<h2>Services Used</h2>

- <b>Amazon Aurora</b> 
- <b>CloudFormation</b>
- <b>Amazon Machine Image(AMI)</b>
- <b>Amazon EC2</b>
- <b>Primary Region</b>
- <b>Secondary Region</b>
- <b>Shell Scripting</b>

<h2>Environments Used </h2>

- <b>AWS Management Console</b>

<h2>Pilot Light walk-through:</h2>

<b>*Assume two seperate S3 buckets are already deployed in seperate regions*</b> 
- <b>Within Amazon S3 allow public access to your S3 Static website</b>
- <b>Create application in PRIMARY region by launching CloudFormation Template</b>
- <b>Create application in SECONDARY region by launching CloudFormation Template</b>
- <b>Verify the PRIMARY website and application</b>
- <b>The SECONDARY website and application should be unavailble because there are no compute instances</b>
- <b>Create the EC2 Amazon Machine Image (AMI) for the PRIMARY region</b>
- <b>COPY the EC2 Amazon Machine Image (AMI) from the PRIMARY region into the SECONDARY region</b>

<b>*Manually simulate a Regional Service Disaster in your Primary region in order to utilize our disaster recovery technique*</b> 
- <b>Within Amazon RDS Promote Amazon Aurora by removing the global database option from the SECONDARY region. The SECONDARY region will now be a Regional Cluster</b>
- <b>Within Amazon EC2 launch the instance from the AMI and choose the SECONDARY region as the VPC</b>
- <b>Verify the SECONDARY region website and application</b>



<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
