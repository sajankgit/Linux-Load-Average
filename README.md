# Linux-Load-Average

Linux Load Average is one of the most critical metrics that determines how well your server is performing. All system administrators should be well cautious and aware of this metrics.

## System load

Before coming to Load Average, let’s understand what is system load.

The load of a system is essentially the number of processes active at any given time.

When idle, the load is 0.

When a process starts, the load is incremented by 1. A terminating process decrements the load by 1.

Besides running processes, any process that’s queued up is also counted.

So, when one process is actively using the CPU, and two are waiting their turn, the load is 3.

The load fluctuates quickly because of short-lived processes and can jump from zero to 5 in milliseconds and back again the next instant. Because of this volatility, it’s more useful to look at the average load over time, which gives a better overview of the load the system has been under.

Ref: https://blog.appsignal.com/2018/03/28/understanding-system-load-and-load-averages.html

## Load averages

Now that we know how system load is counted, we can take a look at load averages. As we’ve seen, the load the system is under is usually shown as an average over time.

Generally, single-core CPU can handle one process at a time. An average load of 1.0 would mean that one core is busy 100% of the time. If the load average drops to 0.5, the CPU has been idle for 50% of the time.

If the load average rises to 1.5, the CPU was busy all the time while there was (on average) one other process waiting for 50% of the time, giving the CPU more work than it can handle.

Ref: https://blog.appsignal.com/2018/03/28/understanding-system-load-and-load-averages.html

## Monitor Linux System Load Average

One of the common command used to get load average is uptime

```
$ uptime
 07:16:18 up 118 days, 13:01,  1 user,  load average: 0.11, 0.03, 0.01
Here you can see load average for the past 1, 5 and 15 mins.
```

Other tools such as top also shows load averages.

```
$ top
top - 07:23:36 up 118 days, 13:08,  1 user,  load average: 0.00, 0.00, 0.00
Tasks: 112 total,   2 running,  67 sleeping,   0 stopped,   0 zombie
%Cpu(s): 10.0 us, 20.8 sy,  0.0 ni, 69.2 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  3772884 total,   313520 free,   317320 used,  3142044 buff/cache
KiB Swap:        0 total,        0 free,        0 used.  3177308 avail Mem
PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND
 1120 root      20   0  388652  39156   2844 R 10.9  1.0  37:41.31 cmd_daemon
   10 root      20   0       0      0      0 S  0.5  0.0   8:17.18 ksoftirqd/0
    1 root      20   0  225540   5960   3292 S  0.0  0.2   2:30.96 systemd
```

## Optimum Load Average

One of the most common question is what should be the threshold of load average one should keep for alerting.

Since it is average of all process, it’s difficult to determine such threshold. Ideally for a system with a single core load average of 1 can be fine. If the load average prevails greater than 1 for more than 10–15 mins, we can assume there is something to be checked.

Above is just an ideal case. In real life, it depends on how well your application performs with a certain amount of load. As an example, say I have a website deployed in a single core server. If I am not facing any issue with my website (slowness, not reachable etc..) with a load of 4, then it is safe to set the threshold of the load average to be 4.

## Conclusion

Load Average is certainly a critical metric that needs to be monitored and alerted. This metrics will tell you how well you server performs which in turn will have effect on your application deployed in the server.

Hope the reading has given you an overall idea on load average.
