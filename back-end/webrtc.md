Basic P2P, SFU and MCU

jitsi: SFU

[https://github.com/jitsi/jitsi-meet](https://github.com/jitsi/jitsi-meet)

quick install jitsi

in /etc/init.d/

```
./prosody restart && \
./jitsi-videobridge restart && \
./jicofo restart && \
./nginx restart
```

hublin: based on janus

[https://github.com/linagora/hublin](https://github.com/linagora/hublin)

kurento

```bash
docker run --name kms -p 8888:8888 -d kurento/kurento-media-server
```



