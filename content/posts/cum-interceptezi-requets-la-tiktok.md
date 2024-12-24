---
title: "Cum Interceptezi Requets la aplicatia Tiktok"
date: 2024-12-24T20:43:06+02:00
tags: []
---

Primul lucru pe care trebuie sal faci, este sa faci jailbrake la telefon iphone 8, folosing https://checkra.in/.

trebuie sa apesi pe home si power in acelasi timp, si dupa lasi buttonul power si tii apesat doar pe buttonul home, ca sa plece setupul la jailbrake.


Acesta comanda iti arata id procesului, in care ruleaza applicatia tiktok.
```bash
> Frida-ps -U |grep -i tiktok
```
4735 TikTok

Aceasta comanda, dezactiveaza ssl strip la applicatia tiktok.
```bash
> frida -U 4735 -l tiktokbypass.js
```



```js
/*
	This script bypasses SSL pinning that TikTok has and may change in the future.
	This is for educational purposes only.
	
	To run, run the following command:
	frida -U -f com.zhiliaoapp.musically --no-pause -l tiktoksslbypass.js

	Please note this will only work on Jailbroken iOS devices. You must have frida installed prior to running this script.

*/

Interceptor.attach(ObjC.classes.TTHttpTask["- skipSSLCertificateError"].implementation, {
onEnter: function (args) {
    
},
onLeave: function (retval) {
    console.log('Overriding -> TTHttpTask skipSSLCertificateError : ');
    retval.replace(0x1)
}
});


console.log('Successfully Initalized SSL Bypass...');

```