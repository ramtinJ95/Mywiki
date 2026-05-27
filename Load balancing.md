In essence load balancing is about distributing computational workloads between
two or more computers.

There are 2 main ways of running load balancing when its software based:
* Static load balancing - These are algorithms such as round robin or client
side random load balancing. Here we assign workloads based on a predetermined
plan and do not take into consideration if the server we are going to assign to
has problems or is experiencing higher load because the previously assigned
workloads were unusually heavy etc, we just assign and move on. 
* Dynamic load balancing - This type of load balancing takes server health,
availability and workload. This is obviously more difficult to do then the static
approach. Some approaches for this are; least connection, weighted least
connection, resource based and geolocation-based load balancing. 

Its important to realise that dynamic load balancers must be aware of sever
health: Their current status how well they are performing etc. As such dynamic
load balancers monitor server metrics with health checks etc. 
