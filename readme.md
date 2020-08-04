## #TCPDUMP #NC and #K8S fun !!

### Redirect output to stdout
This tutorial explains how to tunnel tcpdump pcap traffic from a kubernetes cluster back to a remote workstation. <br>
In the first example, `tcpdump` captures traffic to http port 80 and writes it to standard output (`-w -`).<br> 
The `-U` makes sure the traffic is send immediatly to the output (to avoid being buffered).
```
tcpdump -i any -n -U -w - port 80 >demo.pcap 
```
Hit ctrl-c to stop the capture. We can now read the capture and no errors are displayed.
```
tcpdump -r demo.pcap
```

### Redirect via netcat
Open a first terminal to capture some traffic. Std output is now redirected to netcat 
```
tcpdump -i any -n -U -w - port 80 | nc 127.0.0.1 6666
```
In a second terminal we can redirect the stream to a file and in the meanwhile monitor the traffic
```
nc -l 6666 >demo.pcap 
```
You can now read the capture
```
tcpdump -r demo.pcap
```

### Redirect via SSH reverse tunneling
Create an SSH session with the host your planning to run `tcpdump`
```
ssh -i root@remote-host -R 6666:127.0.0.1:6666
```
And now run the capture
```
tcpdump -i any -n -U -w - port 80 | nc 127.0.0.1 6666
```
On the local machine you can redirect 
```
nc -l 6666 >demo.pcap 
```
and read the captured traffic
```
tcpdump -r demo.pcap
```

