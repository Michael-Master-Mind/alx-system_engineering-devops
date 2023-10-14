Issue Summary

The web-01 server was down for six hours between 12 p.m. EAT and 6 a.m. EAT.
All services on the web server were inaccessible, but the load balancer was still sending half of the user traffic to the server, affecting about 50% of users who requested our services during the downtime.
The main cause of the issue is a memory overload caused by the server's memory and cache not being cleared regularly. In addition to that, the implementation of the new data-dog agent pushed the server beyond its capacity, resulting in a crash.

Timeline - OCT 14

11 p.m. EAT – A junior engineer attempted to implement the new data dog agent on the server.
12 a.m. EAT - After finishing up the setup process, the engineer noticed that server response time was slowing down and attempted a reboot. After the reboot, attempts to ssh into the server failed.
12:30 a.m. EAT – According to the data dog site report, the server was still online, and the engineer was working under the assumption that it was a local problem.
12:30 a.m. EAT - Tried logging in from a different device. I attempted SSH after deleting the saved known hosts.
1 a.m. EAT - Reached out for help from peers and mentors on Slack.
3 a.m. EAT – A peer suggested that they had been in a similar situation and that the situation resolved itself in about 24 hours.
5 a.m. EAT - Received a suggestion to destroy the virtual machine of the server and start over with the project from the mentor.
6 a.m. EAT - After re-initiating a new web-01 server, the setup was complete and the services were back online.

Root cause and resolution

The issue was caused by an unexpected memory overload on the server in question. Adding another service to the machine without addressing the initial memory issues caused it to crash and make it unrecoverable. After reaching out to peers and mentors, a final verdict was made to destroy the virtual machine and re-initiate a new server to solve the issue. Soon afterward, the load balancer was redirecting user traffic to the newly set up web-01 server.

Corrective and Preventative measures

Reduce the time needed to create a new server.
Use bash or puppet scripts to automate generating new servers in case they fail.
Set up a system to report if a server goes down and is unrecoverable to immediately replace it.

Prevent server crashes

Automated cache and memory clearance on the server.
Increase usable server memory.
Scheduled server update and restart.

Managing user traffic in case of a crash

Automated monitoring of server availability by load balancer
Balancing a load of requests based on availability
