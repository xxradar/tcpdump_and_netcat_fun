## TCPdump and NetCat fun !!

### Redirect output to std out
This tutorial will guide in tunneling tcpdump pcap traffic fro; a kubernetes cluster to your notebook. <br>
In first example, tcpdump captures traffic to http port 80 and writes it to standard output (-w -).,<br> 
The -U makes sure the traffic is send immediatly to the output (to avoid being buffered).

```
tcpdump -i any -n  --immediate-mode  -U -w - port 80 >demo.pcap 
```
Hit ctrl-c to stop the capture. We can now read the capture and no errors are displayed.
```
tcpdump -r demo.pcap
```
