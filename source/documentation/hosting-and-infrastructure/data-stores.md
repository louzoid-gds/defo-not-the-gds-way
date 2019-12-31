# Use data stores

When designing your services you may need to use a data store, for example to collect and store data, such as user details, from your app.

Read [the Service Manual](https://www.gov.uk/service-manual/technology) for more information about choosing technology, development, integration, hosting, testing, security and maintenance.

## Storage technology

Data stores use common storage techniques like:

- [relational databases](https://aws.amazon.com/relational-database/) - a traditional structured database like SQL
- [object database management system (ODMS)](http://www.odbms.org/introduction-to-odbms/definition/) -  sometimes called [NoSQL](https://www.mongodb.com/nosql-explained) or unstructured databases
- [key-value pairs](https://aws.amazon.com/nosql/key-value/) - usually implemented as in-memory data stores
- [file-based](https://tutorialink.com/dbms/advantage-and-disadvantages-of-file-oriented-system.dbms) - data stores offered as a file system

There are data stores for specific situations or those which combine common tools or extend them. For example, [PostGIS](https://postgis.net/) is a [PostgreSQL database](https://www.postgresql.org/) supporting spatial and geographic objects.

### Example use cases

Depending on your use case, base your data store on the behaviours and performance of each technology. For example:

- Create shared values
- Store images and metadata
- Relational data

#### Create shared values

If you need to create a set of shared values across the different elements of your data store, choose key-value pairs stored in memory. Key-value pairs provide high performance while scaling large amounts of data.

#### Store images and metadata

Although you can store images and metadata in different data stores, you should use an object database. Object databases search large data sets of unstructured data and you can combine them with a file-based store.

#### Relational data

If you have a lot of relational data in a structured form, you should use a relational database because they search, index and manage large volumes of data.

##Types of data store

There are 2 distinct classes of data store implementation, known as managed and unmanaged.

### Managed

GDS recommends using a managed service like [Amazon Web Services (AWS)](https://aws.amazon.com/products/databases/?nc2=h_m1).

Managed services are easier to put in place than unmanaged because they’re usually offered as a service. This means you do not need to manage the underlying data store technology.

Managed services handle complicated aspects of data stores for you like:

- replication and backups
- operating system updates
- update and patches to the data store software

### Unmanaged

With an unmanaged service, it’s your responsibility to install and manage the:

- data store software
- underlying or associated technologies

Use an unmanaged data store if a managed service would be more complicated to put in place and maintain. For example, with an unmanaged service you could store all aspects of the data store using real or virtual machines which you’ll need to manage.
