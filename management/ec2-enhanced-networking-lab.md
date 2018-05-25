We will look at transfer speed between enhanced and non-enhanced instances. Then we will adjust MTU settings to see the effect. 



commands

```bash
# generate 1G file for testing transfer speed
fallocate -l 1G test.img

# test speed
scp test.img 10.0.0.13:~

# change pmtu
sudo ip link set dev eth0 mtu 1500

# then test speed again
scp test.img 10.0.0.13:~

```



