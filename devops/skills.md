SSH Key Forwarding

```bash
# set ssh agent
ssh-agent bash

# move key to ~/.ssh folder
# add key to ssh agent
chmod 400 ~/.ssh/awsnetcourse.pem
ssh-add ~/.sshawsnetcourse.pem

# connect to first server with -A option
ssh -A ec2-user@52.14.126.230

# connect to second server
ssh ec2-user@10.111.2.238
```



