# Cloud Deployment Models

Cloud deployment models refer to the different ways in which cloud services can be deployed and accessed by users. There are four main cloud deployment models:

1. **Public Cloud**: A public cloud is a cloud deployment model where the cloud infrastructure is owned and operated by a third-party cloud service provider which is accessible to the public. Examples of public cloud providers include Amazon Web Services (AWS), Microsoft Azure, and Google Cloud Platform (GCP).

   ```mermaid
    architecture-beta
    group public_cloud(cloud)[Public Cloud]

    service db(database)[Database] in public_cloud
    service disk1(disk)[Storage A] in public_cloud
    service disk2(disk)[Storage B] in public_cloud
    service server(server)[App Server] in public_cloud

    db:L -- R:server
    disk1:T -- B:server
    disk2:T -- B:db

    group customer_group(internet)[On Premises Environment]
    service client(server)[Customer Workstation] in customer_group

    client:R -- L:server
   ```

2. **Private Cloud**: A private cloud is a cloud deployment model where the cloud infrastructure is owned and operated by a single organization. It can be hosted on-premises or by a third-party provider. Private clouds offer greater control and security compared to public clouds, making them suitable for organizations with strict compliance requirements. Examples of private cloud solutions include VMware, vSphere, and OpenStack.

   ```mermaid
   architecture-beta
   group private_cloud(cloud)[Private Cloud]

   service db(database)[Database] in private_cloud
   service disk1(disk)[Storage A] in private_cloud
   service disk2(disk)[Storage B] in private_cloud
   service server(server)[App Server] in private_cloud
   service workstation(server)[Internal User Workstation] in private_cloud

   db:L -- R:server
   disk1:T -- B:server
   disk2:T -- B:db
   workstation:R -- L:server
   ```

3. **Hybrid Cloud**: A hybrid cloud is a cloud deployment model that combines the benefits of both public and private clouds. It allows organizations to leverage the scalability and cost-effectiveness of public clouds while maintaining the control and security of private clouds. Hybrid clouds are particularly useful for organizations that have sensitive data or regulatory compliance requirements. Examples of hybrid cloud solutions include Microsoft Azure Stack, AWS Outposts, and Google Anthos.

   ```mermaid
   architecture-beta
   group public_cloud(cloud)[Public Cloud]

   service db(database)[Database] in public_cloud
   service disk1(disk)[Storage A] in public_cloud
   service disk2(disk)[Storage B] in public_cloud
   service server(server)[App Server] in public_cloud

   db:L -- R:server
   disk1:T -- B:server
   disk2:T -- B:db

   group private_cloud(cloud)[Private Cloud]

   service private_db(database)[Database] in private_cloud
   service private_disk(disk)[Storage] in private_cloud
   service private_server(server)[App Server] in private_cloud

   private_db:L -- R:private_server
   private_disk:T -- B:private_server
   private_disk:T -- B:private_db

   group customer_group(internet)[On Premises Environment]
   service client(server)[Customer Workstation] in customer_group

   client:R -- L:server
   client:R -- L:private_server
   ```

4. **Community Cloud**: A community cloud is a cloud deployment model where the cloud infrastructure is shared by several organizations that have common concerns, such as security, compliance, or jurisdiction. Community clouds can be managed by the organizations themselves or by a third-party provider. Examples of community cloud solutions include IBM Cloud for Financial Services and Microsoft Azure Government.

   ```mermaid
   architecture-beta
   group community_cloud(cloud)[Community Cloud]

   service db(database)[Database] in community_cloud
   service disk1(disk)[Storage A] in community_cloud
   service disk2(disk)[Storage B] in community_cloud
   service server(server)[App Server] in community_cloud

   db:L -- R:server
   disk1:T -- B:server
   disk2:T -- B:db

   group organization1(internet)[Organization 1]
   service client1(server)[Workstation 1] in organization1

   client1:R -- L:server

   group organization2(internet)[Organization 2]
   service client2(server)[Workstation 2] in organization2

   client2:R -- L:server
   ```
