# Get private IP address on Mac

> From [stackexchange](http://apple.stackexchange.com/questions/60160/how-can-i-find-my-ip-address-not-my-companys-router-but-my-local-machines).

* Click System Preferences, click Network.

* ifconfig

```bash
$ ipconfig getifaddr en0 # en0 for wireless and en1 for ethernet, en3 for Thunderbolt-to-ethernet adaptor
```

* WiFi menubar: `Option + option`
