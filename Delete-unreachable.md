## Delete unreachable objects
In this document I describe how to delete unreachable loose objects in isomophic-git.

The basis algorithm is straigt forward.
- get a list of root object ids
- get a list of reachable object ids by following the root objects
- get all object ids
- get a list of unreachable object ids, which is: list of all - list of reachable
- delete the unreachable objects

### Get root objects oids
To get a list of root object oids we have to read the references under `.git/refs`. They include:

- local branches
- local tags
- remote branches
- remote tags

Especially when you sync the repository, you can get objects which are only reachable from newly created remote branches.

Additionally we have to read the object ids from the `.git/index` file. Especially the staged objects are added to the store and have no other reference than the in the `.git/index` file.

It is no problem if we have additional oids.

### Get reachable objects oids
To get the reachable object oids we walk through to store starting with the root oids and follow the objects. We maintain a set of reachable oids. Before we read an object, we check if the oid is already in the set. If not we read the object and add its oid to the set.

The object has one of the four types:

#### Tag
We follow the oid in the tag object, which is a root tree.
#### Tree
We loop through the entries of the tree object. We follow the tree entities. We add the oids of the blobs to the reachable set. We do not need to read blobs.
#### Commit
We check if the commit is a shallow commit. If not we follow the oid, which is a root tree and we follow the parent commits.
#### Blob
We do not read blob objects, so we should never be here.

### Get all object ids
To get all oids we have to get a list of loose objects and and a list of objects from the packed object store.

To get the loose objects we have to walk through the `.git/objects` directory and collect all object file name (oids).

To get the packed object oids we have to read all packed index files, which contain the oids.

### Get unreachable oids
To get unreachable oids we have to get the difference of all oids and the reachable oids.

### Delete oids from loose store
Deleting loose objects is simply deleting the object files assosiated with the object id. 

To delete objects from the packed object store requires to create an new packed object store and delete the old one. This is out of scope for this document.

The better way is to cleanup the repository before you create a packed store. 
