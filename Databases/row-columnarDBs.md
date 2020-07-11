The Theory
----------

The major difference in both the datastores lies in the way they physically store the data on the disk. We know that persistent storage disks(hard disks?) are organized in blocks and have following usual properties for reading/write operations

> Head Seek operation is expensive in disks due to mechanical movement required. <mark>Read/Write is quite fast.</mark>

1.  The whole block with data is loaded into the memory for reading by the operating system. Any further read for data for this block will happen from memory and will be super fast.
2.  Read/Writing operations disks are not slow. only seek operation is slow. i.e. to move the head to the correct block to perform the operation.
3.  Due to the above point --- sequential read/writes are much faster on disks rather than the random access.

Here comes to major difference about row and columnar DBs

> Row oriented database tries to store whole row of the database in the same block but columnar database stores the values of the columns of subsequent in the same block

Following is an excellent diagram from Redshift's documentation[1] to understand the difference.

![](https://miro.medium.com/max/1598/1*i4_EpE4X8tELgqf4AqMQEQ.png)

Figure1: Row wise.

![](https://miro.medium.com/max/1606/1*V79BS1_Bryd8v3TZ5EErwQ.png)

Figure2: Columnar wise

In Figure-1: SSN, Name etc all other properties of a row is stored in the same block, but however in Figure-2: SSN values of 33 consecutive rows are stored together.

In Practice?
------------

So now we understand the theoretical difference in the two popular ways to organize data on disk. But how does this difference translates to performance and difference use-cases?

1.  Easy to guess --- Row oriented databases perform best for the operations on the whole row and columnar for the operations on the columns.
2.  Row oriented operations: Add/Delete/Update whole row. Retrieve the whole row.
3.  Column Oriented Operations: Update columns, Aggregations, selecting a few columns, and any other operation, stored procedures, etc. which work on the columns only. <mark>Mainly for analytics, range queries based on queries </mark>
4.  Since disk block contributes a lot to the performance it is recommended to have block size which is enough to fit the whole row for row wise DBs and for columnar <mark>keep reasonably high block size</mark> so that you can operate of more columnar data at one read.
5.  Columnar Databases are quite slow for insertions as you insert a whole row.
6.  Columnar DBs can optimize a lot of space as they keep <mark>homogenous data</mark> in a single block, so they can apply strategies to compress the data in a block. Similarly, over a huge number of columns and rows, they will have considerably less fragmentation as compared to row wise.
7.  This is one of the reasons that Columnar DBs are popular as big data DBs because less storage means fewer costs, faster reads (read fewer blocks). And since OLAP systems generally work with big data and aggregations to produce small columns as output, Columnar DBs hit the sweet spots there
8.  Due to the inherit nature of transactions, row-wise DBs are best fitted for OLTP systems.

### Features of Relational Database and HBase are as following:

| RELATIONAL DATABASE | HBASE (Columnar) |
| --- | --- |
| It is basically based on a Fixed Schema. | It is totally Schema-less. |
| It is an example of row-oriented datastore. | It is an example of column-oriented datastores. |
| It is basically designed to store normalized data. | It is basically designed to store de-normalized data. |
| It basically contains thin tables. | It basically contains wide and sparsely oriented populated tables. |
| It has no built-in support for partitioning. | It basically supports Automatic Partitioning. |