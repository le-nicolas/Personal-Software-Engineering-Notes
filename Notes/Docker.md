Docker - A valuable skill, as it is a widely used tool in the software development industry, not just in robotics. 

But docker is a bit of a handle, things may go out of hand if your not aware of it. Like for instance it may consume a lot of space in your hard drive ( even consume all of it!)
Therefore, here is my cheat sheet to those kind of stuff. . . 


![1700495166720](https://github.com/user-attachments/assets/f2fcf4eb-5d47-4b3f-9a1f-39d6cffd2feb)



##  Remove All Stopped Containers

To clean up your Docker environment and remove all stopped containers, run:

```
$ docker container prune
WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
Deleted Containers:
abc123def456
ghi789jkl012 
```


## 📦 Delete Dangling (Unused) Images

Remove dangling (untagged) Docker images:

```
$ docker image prune
WARNING! This will remove all dangling images.
Are you sure you want to continue? [y/N] y
Deleted Images:
sha256:abc123...
sha256:def456...
```


``` $ docker image prune -a ```
WARNING! This will remove all images not used by any containers.




``` $ docker volume prune ```
WARNING! This will remove all unused volumes.



``` $ docker builder prune ```
WARNING! This will remove all dangling build cache.




# Bonus tips!

```
$ docker system df
sample output will be
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          5         2         3.5GB     1.2GB (34%)
Containers      3         1         300MB     200MB (66%)
Local Volumes   7         2         2.1GB     1.9GB (90%)
Build Cache     6         0         850MB     850MB (100%)
```

``` $ docker system prune -a --volumes ```
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all images without at least one container associated with them
  - all build cache
  - all unused volumes


