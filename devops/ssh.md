install ssh

```bash
which ssh-agent || ( apt-get update -y && apt-get install openssh-client -y )
```



在后台运行ssh-agent

```bash
eval $(ssh-agent -s)
```

把private key加入ssh-agent

```bash
echo "$SSH_PRIVATE_KEY" | tr -d '\r' | ssh-add - > /dev/null
```

or

```bash
ssh-add ~/.ssh/id_rsa
```



Create the SSH directory and give it the right permissions

```
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```





