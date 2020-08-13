# DDAO: Decentralized Data Access Object

# Introduction
Data Management refers to the process of collecting, organizing, storing, processing, transmitting and retrieving different types of data. It is an important application area of the computer science. One of its goals is to efficiently store and manage complex, large amounts of data using computers, so that people can easily get access to the data. Another goal is to extract and derive valuable information from the data, and then use the information as a guidance for action and decision making.

At present, enterprises mainly use centralized databases and file systems for data management. Large Internet companies develop their own systems, such as GFS (Google File System), SQL Server, etc., and deploy local services. Small and medium-sized companies connect to cloud services such as AWS, Aliyun, and delegate data management tasks to these third parties. Local and cloud data services have their own application scenarios and they maintain the basic data of many companies.

Centralized storage is currently the main solution to data management, but there are serious storage problems in centralized databases and file systems around the world. Enterprises often store all their data and files in centralized databases and file systems. But centralized storage solutions often attract attacks from hackers, or they may be ruined by an accident. Enterprises sometimes have to face the loss of all their data resources and never get them back. Some business highly relys on data and such kind of loss may lead to huge risks. Although cloud service providers would promise to do data backup, but it has not solved the fundamental problem.

Decentralization technologies, such as blockchain and IPFS, provide a new type of solutions to data management. By using encryption and consensus, data privacy and security are guaranteed. Since data are stored in a lot of nodes, there is no need to worry about data loss caused by failure of one single node, which improves security and reliability. Encryption and segmentation technologies control the read access and guarantee data privacy. At the same time, in order to ensure scalability, cluster technology is used. A cluster is a large group of nodes that store and manage data together, and it allows new nodes to join or expanding more clusters.

However, at present, with the increasing number of decentralized systems, developers have to face high costs in selection, learning, development, deployment, and maintenance of these systems. Therefore we proposed the DDAO (Decentralized Data Access Object). Our goal is to develop a common library to access various decentralized systems with uniform interfaces, so as to perform CRUD (Create, Read, Update, Delete) operations. Through this library, developers can quickly read and write data in various decentralized systems and build their own applications without having to care about the underlying technology.

# Related Work
With the development of blockchain technology and digital currency market, decentralized data storage and management technologies receive attentions from research fields and investment markets.

## Decentralized File System
As a decentralized system, blockchain backs up data at every node, so it is not suitable for storing large-size files, such as pictures, videos and audios. In current blockchain applications, such kind of files are still stored in servers held by developers. This way leads to the centralization of these applications, which violates the essential meaning of blockchain.

Decentralized file systems mainly include IPFS (InterPlanetary File System) [1], Swarm [2], Storj [3], and so on. Their basic method is to split the uploaded file into small pieces and then store them into nodes. When downloading the file, you can use the hash value of the file as an address to make a request to a node, and then you will get all the data pieces from the node and combine them into the whole file. In this way, one file can be separately stored in many nodes in a network, which achieves decentralization.

One problem with these technologies is how to keep more nodes online to provide download services. Hence, some projects propose to add node incentive mechanisms to the decentralized file system so that online nodes can obtain revenues. In this way, the decentralized file system becomes a cloud storage service, in which users need to purchase the service during uploading and downloading processes so as to reward the nodes that provide the storage service. Several typical projects include Filecoin [4], Wolk [5], Fluence [6], and Sia [7].

# Decentralized Database
The decentralized file system enables decentralized storage of data, but after the data are uploaded, they cannot be further modified or retrieved, which limits its application in data management. Traditional centralized data management services usually use database systems such as MySQL or Redis to execute CRUD operations of data. Therefore, similar database services are required in the decentralized area.

There are several projects having research on decentralized databases, including BigchainDB [8], Bluzelle [9], Ties.DB [10] and so on. Their basic idea is to upload database write requests to the blockchain through transactions, and then use database engines such as MongoDB to perform data indexing and process read requests. Using blockchain to build decentralized databases, effectively utilizes the mature decentralized architecture of blockchain systems, and has great advantages in stability and security.

These projects are currently in their initial stages, and before their implementations mature, using smart contracts as a database service is also a viable alternative. Some projects are based on Ethereum + IPFS to develop their applications, using smart contracts written by Solidity for data management. Solidity supports data structures such as List, Map, Struct, etc., which are sufficient for common data management scenarios. These items are fully enumerated in [11].

# System Description
Decentralized systems have a variety of implementations, leading to high learning costs for developers. This article will design a common library for connecting upper-layer DApp applications to lower-layer decentralized systems, enabling CRUD operations for multiple decentralized systems. Developers can quickly build their own data management applications through this library without having knowledge about the underlying technology. At the same time, based on this library, a cloud service can be built to provide online CRUD interfaces of multiple decentralized systems, eliminating the cost of deploying and maintaining decentralized systems for developers.

![image](img1.png)

The system can be separated into three layers, namely DDMI (Decentralized Data Management Infrastructure), DDAO and DApp (Decentralized Application), which will be introduced as follows.

## DDMI
The DDMI layer contains a variety of decentralized systems, including blockchains, decentralized databases, decentralized file systems, and more. These decentralized systems can be launched locally by the developer or deployed on a remote server, and then connected through a descriptor with uniform format. For example, the format of *name://user:password@ip:port*, that is, connecting to a local Qtum node with port 13889 by *qtum://admin:123456@127.0.0.1:13889*, or connecting to an IPFS node in LAN with 8080 port by *ipfs://myname:mypasswd@192.168.1.2:8080*.

## DDAO
The DDAO layer is the core module proposed in this paper. Its main functions include (1) establishing connections to various decentralized systems, (2) abstracting to get compatible CRUD interfaces. For different types of decentralized systems, abstract interfaces are different:

1. For blockchain systems, interfaces contain sending transactions, querying transactions, creating contracts, reading and writing contracts.
2. For decentralized database systems, database interfaces such as create, find, insert, and update are included.
3. For decentralized file systems, main interfaces such as file upload, download, and encryption are included.

The design here needs to take into account the compatibility of different systems, so only some common functions are abstracted. At the same time, the interface used to send original commands is offered, so that developers can request some unique interfaces of each system.

## DApp
The DApp can be JavaScript scripts running on browser or programs running on server. They may also be stored in the decentralized file system and later obtained through a specific address as an entry. The DApp initiates the DDAO instance, connects local or cloud decentralized systems, and performs CRUD operations on these systems, so as to realize data management applications.

Multiple DDAO instances can be initiated within one DApp, in order to connect to multiple different decentralized systems. This allows data interaction with multiple decentralized systems in one application, enabling more features compared with traditional smart contract-based DApps. For example, cross-chain data transmission among multiple blockchains, or data visualization based on blockchain and file system.

# Application Scenario
A large number of application scenarios is the best way to describe the value of DDAO. Based on DDAO, many decentralized applications will become easy to develop and implement.

## Decentralized Content Sharing
DDAO can be used to build a blog, photo, music, video sharing platform. By using DDAO's write interfaces, users can publish texts, images, videos and other content to a decentralized file system such as IPFS, and then store their meta data (such as content address, release time, user ID, etc.) into a smart contract or a database. The DDAO read interfaces are used to filter, sort, and display the content. The advantage of such system is that the contents published by users is decentralized and cannot be tampered with.

## Decentralized Trading Platform
Based on DDAO, you can build a trading platform like Taobao and Amazon. When a merchant uses DDAO write interfaces to upload its product information, the text and image are stored in a decentralized file system, and the meta data (such as price, quantity, classification, keywords, etc.) are stored in a smart contract or a database. When a customer browses the platform, DDAO read interfaces are used to search and filter products. Finally, the customer uses DDAO to connect to the blockchain to create orders, pay orders, and complete orders. The advantage of this platform is that the product information and transaction process are transparent and the payment process is convenient.

## Decentralized Cloud Storage Service
Storage service providers register their information into a blockchain or a database via DDAO. When a user uploads a file, he needs to use blockchain tokens to purchase the service, and then uploads the file to a decentralized file system through DDAO, while the file information and address are stored in a smart contract or a database. When downloading, users browse the file information and address by using DDAO, and then download the file from the file system. The tokens consumed by the user are used to reward storage service providers, forming a complete economic ecology.

# Summary
Decentralized data management has broad application prospects. Although, at present, decentralized databases and file systems are still under development, and immature infrastructure limits its application, it is conceivable that these systems will be implemented one after another in the near future. DDAO will also be widely used just like the DAO in current centralized systems.

# References
[1] IPFS. https://ipfs.io/.

[2] Swarm. https://swarm-guide.readthedocs.io/en/latest/.

[3] Storj. https://storj.io/.

[4] Filecoin. https://filecoin.io/.

[5] Wolk. https://wolk.com/.

[6] Fluence. https://fluence.one/.

[7] Sia. https://sia.tech/.

[8] BigchainDB. https://www.bigchaindb.com/.

[9] Bluzelle. https://bluzelle.com/.

[10] Ties.DB. https://tiesdb.com/.

[11] Awesome IPFS. https://awesome.ipfs.io/.