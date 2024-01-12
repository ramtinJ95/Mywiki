# Storage and databases

__Instance stores__ is memory for an EC2 instance that will be lost as soon as
the connected EC2 instance is stopped/terminated.

__Amazon Elastic block store (Amazon EBS)__ is a service that provides storage
with EC2 instances which presist even when the connected EC2 instance is
stopped/terminated. EBS supports both full backups and incremental snapshots
since we may want to persist the data we have in EBS.

EBS is very well suited for when we haver larege files and we only change small
parts of those files. Because since everything is broken down to blocks we can
do delta updates which is not possible in a object store type system like s3.

__Amazon Elastic file system (Amazon EFS)__ is a file storage system. In such a
system multiple clients (such as users, applications servers and so on) can
access data that is stored in shared file folders. In this approch a storage
server uses block storage with a local file system to organize files. Clients
accesss data through file paths. Compared to object and block storage, file
storage is ideal for use caese in which a large number of services and resourses
need to access the sme data at the same time.

Amazon EFS is a scalable file system used with aws cloud services and
on-premises resources. As you add and remove files, Amazon EFS grows and shrinks
automatically. It van scale on demand to petabytes without disrupting
applications.
