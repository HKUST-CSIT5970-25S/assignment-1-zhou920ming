[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: yuming zhou
### Student Id: 21074406
### Email: yzhoufu@connect.ust.hk
---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).


 
 answer: 
 
i use sysbench. the version is sysbench 1.0.20.
    
I use command "sudo sysbench --test=cpu --cpu-max-prime=80000 run" to test the cpu performance. The task generate a lot of prime number to measure the cpu performance. The upper limit for primes generator I set is 80000. It is bigger than default value 10000. The reason I do that is that I want to set a larger value to test the limit of the cpu performance and show more obvious difference between different instance.
    
I use command "sudo sysbench --test=memory --memory-block-size=4k --memory-total-size=800M run" to test the memory performance. The task write data to memory to measure the cpu performance. The memory block size I set is 4k. It should be the power of 2 and in real world it is usually optimum size. i.e.not too big or too small . The memory total size is 800M. it is not a small value so it can show obvious difference between different instance.

For both cpu and memory performance, the results i choose from measurement are total time. i.e execution time for a given task. Because for a given task,  the less execution time is, the faster the task is. And speed is very important consideration for performance of task.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |            10.0053s     |        0.4090s            |
    | `t2.medium`  |        10.0057s         |  0.4026s                  |
    | `c5d.large` |     10.0004s            |          0.0616s          |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.


answer: 

For cpu performance, t2,medium is very similar with t2.micro. c5d.large has just a little improvement compared with t2.medium.
    
For memory performance, t2,medium has very small improvement compared with t2.micro.c5d.large has very large improvement compared with t2.medium.

it means that the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource, but very little performance improvement on CPU. it mainly improve the memory performance.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |          4.45      |          |
    | `m5.large` - `m5.large`   |                |          |
    | `c5n.large` - `c5n.large` |                |          |
    | `t3.medium` - `c5n.large` |                |          |
    | `m5.large` - `c5n.large`  |                |          |
    | `m5.large` - `t3.medium`  |                |          |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |                |          |
    | N. Virginia - N. Virginia |                |          |
    | Oregon - Oregon           |                |          |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
