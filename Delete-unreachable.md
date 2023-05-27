## Delete unreachable objects
In this document I describe how to delete unreachable objects from a loose store in isomophic-git.

The basis algorithm is straigt forward.
- get root objects
- get reachable objects by following the root objects
- get all objects
- get unreachable objects as the difference between all and the reachable objects
- delete the unreachable objects

### Get root objects oids
To get the root objects we have to read the references under ˋ.git/refsˋ. They include local branches and remote branches which are created by sync calls.

Additionally we have to read the object ids from the ˋ.git/indexˋ file. Especially the staged objects are added to the store and have no other reference than the in the ˋ.git/indexˋ file.

It is no problem if we have additional oids.

### Get reachable objects

#### Tag
#### Tree
#### Commit
#### Blob
