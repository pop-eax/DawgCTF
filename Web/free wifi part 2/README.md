# free wifi part 2

while analyzing the pcap file I captured all the pincodes in a file
```
nonce=MjAyMC0wNC0wOCAxNzowMg==;
passcode=01c7aeb1

WifiKey nonce=MjAyMC0wNC0wOCAxNzowMw==; 
passcode=097b3acf

nonce=MjAyMC0wNC0wOCAxNzoxMw== 
passcode=54f03ae2
```

while examining /staff.html I saw a cookie called wifi-alg it had the value sha1
after playing around I discovered that the pincode is just the first 8 letters of the sha1 of the base64d nonce

so I fired up python and done :D
```
>>> import hashlib
>>> hashlib.sha1("MjAyMC0wNC0xMiAxNDo1OA==".encode()).hexdigest()[:8] 
'519db8fd'
```
the flag
`DawgCTF{k3y_b@s3d_l0g1n!}`
