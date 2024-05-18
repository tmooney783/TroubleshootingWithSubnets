<h2>In this project I learned how to use a subnet to troubleshoot a host computer with no internet access. </h2>

In this project I learned how to reverse subnet in order to troubleshoot a host (**Host 2**) with no network access.


               router: 
              172.17.0.1
                  |
                  |
               switch
            /           \  
          /               \
       Host 1             Host 2
    172.17.12.101        172.17.16.255
    255.255.240.0        255.255.240.0
 
------------------------------------------------------------------------------------------------------------------------

First I converted the subnet mask to binary:

   255  .  255   .  240   .   0
11111111.11111111.11110000.00000000

and found the increment (the last 1 in the network segment converted back to decimal):
 

11111111.11111111.11111111. 1  1  1  1  0  0  0  0
                          128 64 32 16  8  4  2  1
                                     ^

Then used the binary subnet mask and increment to determine the network ranges:

172.17.0.0  - 172.17.15.255
172.17.16.0 - 172.17.31.255
172.17.32.0 - 172.17.47.255
           ...
172.17.239.255 - 172.17.255.255


This showed me that the host I'm troubleshooting is on the network with a range of 172.17.16.0 - 172.17.31.255

so then I could see the problem was that the host was not on the same network as the default gateway, which is 
on the range 172.17.0.0 - 172.17.15.255

and reconfiguring the host's ip address to be on the same network fixed the issue

*diagram*








