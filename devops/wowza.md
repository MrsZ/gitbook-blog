# common errors

Your IP address \(172.17.0.1\) has been blocked

solution: [http://trickntip.com/ip-address-blocked-wowza/](http://trickntip.com/ip-address-blocked-wowza/)

config Server.xml, change `<IPWhiteList>127.0.0.1</IPWhiteList>` to `<IPWhiteList>*</IPWhiteList>,` if you want to specify your IP address then use a comma to seperate IPs like `<IPWhiteList>127.0.0.1,201.163.46.154</IPWhiteList>.`

Wowza RESTful API

basic test

```bash
curl --digest -u "user:pass" -X GET --header 'Accept:application/json; charset=utf-8' http://localhost:8087/v2/servers/_defaultServer_/vhosts/_defaultVHost_/applications
```



