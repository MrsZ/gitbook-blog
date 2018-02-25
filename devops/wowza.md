# common errors

Your IP address \(172.17.0.1\) has been blocked

solution: http://trickntip.com/ip-address-blocked-wowza/

config Server.xml, change `<IPWhiteList>127.0.0.1</IPWhiteList>` to `<IPWhiteList>*</IPWhiteList>,` if you want to specify your IP address then use a comma to seperate IPs like `<IPWhiteList>127.0.0.1,201.163.46.154</IPWhiteList>.`



Wowza RESTful API

