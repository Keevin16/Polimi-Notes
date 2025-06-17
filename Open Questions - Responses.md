---

---
>  Explain the concept of Wear Leveling in the context of SSD  sup=2

We know the fact that the SSDs are composed of NAND ports, which are composed of p-n junction which are worn from a massive number of accesses.
It's possible to conclude that each cell of the SSD has a limited number of w/r cycle and to make it durable as long as possible it's entered the concept of wear leveling.
The **Flash Transaction Layer** has the duty to "Wear Leveling", it will spread out the writes on blocks with lower usage, in this way there're not blocks that wear out faster than other.   

> Discuss the concept of Datacenter Availability, and define what are the diﬀerences among the Tier Levels established by the Uptime Institute.

The Datacenter Availability describe how much is **dependable** the data center, the higher is the percentage of the availability the lower is the global period of downtime during the year.- t on total data writes.
The Tier levels describes the characteristic that a data center must have in order to achieve a determinate period of up time, based on the fault tolerances that it decides to achieve; we have 4 levels (each higher level has the same property of the lower level plus other ) :
-  1 tier: The **DC doesn't have redundancy**, the power is sent to the IT department only from one path.
- 2 tier: It's duplicated the **IT capacity**, for example it's duplicated the Servers, the Storage Services, the Network Devices; as well they are connected to the power supply only from one path.
- 3 tier: Now are also **redundant the paths** from the power supply to the **IT capacity**. The IT capacity is **dual powered**.
- 4 tier: All the **cooling system is independently dual powered**.

>What are the advantages and disadvantages of using Type 1 hypervisors versus Type 2 hypervisors in a virtualized environment?

In a virtualized environment the Type 1 and the Type 2 have different characteristic.
For sure the first differences is based on what "level" they work. 
Starting from the Type 1, as well called **System Level** or **Bare Metal**, which modifies the ISA (instruction Set architecture). 
The ISA is a boundary between hardware and software, it specify which binary instructions can execute or not and the side effects.
So we can conclude that the Type 1 VM run directly on top of the hardware, the PROs are: It's good to manage multiple system VM, **minimal attack surface**, predictable **Latency** and hardware **Consistency**.
The cons is that the Hypervisor **could be not supported** from all the hardware, for this reason it must be ad hoc.
In order to conclude and to clarify all, for the hypervisor exists two types of Architecture, the **Monolithic** and **Micro kernel**. (The main difference for both is where it's done the access to the driver, in the first one the access is done in the Hypervisor, so there's not a higher flexibility, despite of this it has a better **performance** and a better **isolation**. Instead on the second are allowed the device drivers, this makes possible to achieve a greater flexibility instead of the velocity).

The Type 2 instead also called **Process level** or **Hosted Hypervisor**, it modifies the ABI (App Binary Interface). It's an unprivileged interface which user's processors rely on, it's mediated by the OS through **system call** and **libraries**.
The Type 2 is built on top of **Host OS**, which manages the hardware where the VMM run. Instead of the Type 1, it is more flexible in terms of underlying hardware and  it's easier to set up, in other hands the Cons are that the Host OS could consume many hardware resources.

>What are the implications of hardware heterogeneity on software stack development in datacenters?

The implication of hardware heterogeneity is that :
- it's easier to manage
- same software to develop 
- same ISA
- possible to buy in stock
On the other hand the cons could be if that I want to change all the It capacity I have to re-buy all the equipment, which is really expensive.

>  Describe characteristics, advantages, and disadvantages of Direct Attached Storage (DAS), Network Attached Storage (NAS) and Storage Area Networks (SAN).

- The Direct Attached Storage is a Storage Device which is directly connected to the server, it's easy to set up and efficient for local usage, the cons is that it's not scalable and it doesn't implement a structure to communicate with other devices, so in case it must be implemented.
- The NAS provides to the computer connected to the network a **file based data storage services**. The structure is composed by many servers connected to the LAN Ethernet,  which are connected with other NAS servers, which in turn have connected many Storage Devices. This is a scalable solution, because basically you can add or remove NAS Server with their Storage Devices. This is not a high speed communication, for this reason it's not feasible for a "big data" context and for users that need fast access to the data.
- The Storage Area Network is also a scalable solution with a main difference, they implement a network by their own. Instead of the NAS serves they have SAN switches, which can route to the Storage Devices. The Storage Devices will be seen as Storage. It's feasible to have a high volume accesses with an high parallelism.

>Describe, comment, and contextualize the four main types of Clouds

There're 4 main types of Clouds:
- **Private** which are used to a single organization, they can be both externally or internally hosted. In this case you have the full control of all the cloud but it's not flexible, you have all the management expenses to work with. It's more secure.
- **Public** which all the people can use it, with service "pay as you go". The final client is not interested of how the back end is developed, it's only interested that the system is dependable. 
- **Hybrid** it's a mix between at least two Clouds, For example a company that has his private data center but concomitantly to an high pick of request decides to pay for a public cloud.
- **Community** shared by many known companies.

>Provide the definition of Geographic Areas, Compute Regions, and Availability Zones in the context of data centers. What are the advantages and drawbacks of placing all compute instances for my service within a single availability zone?

The Geographical Areas is an abstraction to cluster Computer Region (at least 2 CA for each GA) in the same Geographical Areas, based on geographical boundaries (maybe they have different rules or constraints).  
The Computer Region is an abstraction of the Availability Zone(at least 3 for each CR, minimum to achieve quorum selection), it's a cluster of data center, each of them is at least 100 miles far from the others (in order to don't have problems in case of catastrophes). 
The CR is the finest grain of selection that the final user can have, because he/she cannot select a particular AZ. The AZ has at least one Datacenter and they are not more distant than 100 miles.
All the AZ in the same CR are synchronized and up to date, instead different CR could have different data, they are not synchronized.

>Discuss the role of networking in GPU-based systems within data centers. How does networking impact the performance, scalability, and eﬃciency of these systems?

The networking in GPU based system is really critical and important. 
Starting from the fact that the GPU are used in context where we have a big amount of data to compute, especially in machine learning context, and we want to make more calculus by parallelization with the help of the GPU.
After the computation of the calculus by the GPU