>Manages the **file system namespace** and regulates the **access to files by clients**.
>Clients always interacts with the Namenode in order to locate the data.

It stores data as **metadata** in RAM for fast access.
- List of files and directories.
- Mapping of files to blocks.
- Locations of block replicas.
- Creation/replication times.
- Transaction log (of all operations).

### Secondary Namenode
**Function:** Not a hot standby; it periodically merges the Namenode's `FsImage` (file system metadata snapshot) with the `Transaction Log` (changes since the last snapshot) to create a new, updated `FsImage`. 
This **prevents** the **transaction log from growing too large** and helps in Namenode recovery.

### Standby Namenode
**Function:** A hot standby that is always ready to take over if the active Namenode fails, providing high availability. 
It functions **similarly to the Secondary Namenode** but for **disaster recovery**.
