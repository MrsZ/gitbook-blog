pexpect module

can be used to control interact command line

```python
def login_ssh_passwd(port="", user="", host="", passwd=""):
    if port and user and host and passwd:
        ssh = pexpect.spawn('ssh -p %s %s@%s' % (port, user, host)
        i = ssh.expect(['password:', 'continue connecting (yes/no)?'], timeout = 5000)
        if i == 0:
            ssh.sendline(passwd)
        elif i == 1:
            ssh.sendline('yes\n')
            ssh.expect('password: ')
            ssh.sendline(passwd)
        index = ssh.expect(['#', pexpect.EOF, pexpect.TIMEOUT])

        if index == 0:
            print "logging in as root!"
        elif index == 1:
            print "logging process exit!"
        elif index == 2:
            print "logging timeout exit"
    else:
        print "wrong parameters!"
```

paramiko 专门用于ssh连接的Module

