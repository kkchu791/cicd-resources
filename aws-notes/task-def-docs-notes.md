### task def docs notes

two ways to launch a task definition:

**standalone**
	
- instantiation of task definition with a cluster
*  run once, nothing restarts it
* good for one-offs like batch jobs or migrations

`aws ecs run-task --cluster my-cluster --task-definition my-td:1 -- count 2`

count 2 -  means 2 containers that always start together on the same host
![[Screenshot 2026-10-18 at 11.42.08 AM.png]]

ex: sidecar - a helper container that runs next to your main container in the same task (custom logging, sidecar reads your app's logs)

**service**

* runs and maintains your desired number of task simultaneously in an ECS cluster
* keep multiple **tasks** running, replaces any that dies
* Note: (its on the task level, not on container or ec2)

`aws ecs create-service-cluser my-cluster --service-name my-svc \ -- task-definition my-td --desired-count 2`

ex: good for long running things like APIs

**Scenario: you have 2 containers on the one host ec2, how do you ping one container vs the other**

ALB(with path targets) + path

container 1 is orders
contatiner 2 is users

to hit container 1 alb-ip.com/orders
to hit container 2 alb-ip.com/users


*No not really answering: these are all private ip stuff, but saving for reference*
awsvpc - each task gets its own ENI and IP, so every task can use the sme port with no conflict
you have a load balancer that uses IP-targets to hit the right container

ENI (elastic Network Interface) - its onw private Ip address directly to each container task within your VPC
