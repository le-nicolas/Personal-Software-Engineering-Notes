Docker - A valuable skill, as it is a widely used tool in the software development industry, not just in robotics. 

But docker is a bit of a handle, things may go out of hand if your not aware of it. Like for instance it may consume a lot of space in your hard drive ( even consume all of it!)
Therefore, here is my cheat sheet to those kind of stuff. . . 


![1700495166720](https://github.com/user-attachments/assets/f2fcf4eb-5d47-4b3f-9a1f-39d6cffd2feb)



Delete unused containers:

## 🧹 Remove All Stopped Containers

To clean up your Docker environment and remove all stopped containers, run:

```bash
$ docker container prune
WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
Deleted Containers:
abc123def456
ghi789jkl012

