link-state-monitor
==================

link-state monitor

Script usage follows,
 
1. Copy the script link-monitor.py to bootflash:
The script takes the following three mandatory arguments,
                -m   <Interfaces to monitor>
                -a    <Interface to act on (shutdown/bringup)>
                -l     <Syslog that matched the eem event pattern
 
2. Configure eem as below to detect link UP/DOWN,
event manager applet link_monitor
event syslog pattern "IF_UP:|IF_.*DOWN:"
action 1 cli local python link-monitor.py -m "eth1/5-6 eth1/11 eth1/48" -a "eth1/1-4  Eth1/8-9  Ethernet1/25-32 eth1/51-52" -l "$command"
 
 
Example Usage of the script,
link-monitor.py -m "eth1/1-10" -a "eth1/13-20" -l "$command"
link-monitor.py -m "eth1/1 Eth1/2 Eth1/3" -a "eth1/20" -l "$command"
link-monitor.py -m "eth1/1-10 Eth1/15-20" -a "eth1/30-32 eth1/37-38" -l "$command"
 
 
This Script,
1. Shuts down all the interfaces mentioned in the –a options, when all the interface mentioned in –m option is down
2. Brings up all the interfaces mentioned in the –a options, when at least one of the interface mentioned in –m option is back up
