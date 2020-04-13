# the hacker one

This challenge was one of the weirdest challenges, I have ever done
so let's begin:

we have the challenge url: https://umbc.h1ctf.com/
I started by a dirsearch 
and found the following endpoints 
![dirsearch](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/dirS1.png)

from here I started to look at the endpoints

`/login`
![login-1](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/login-1.png)

`/register`
![register](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/register-1.png)

`/profile`
![profile](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/profile-1.png)

`/debug`
![debug](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/profile-1.png)

`/profile and /debug` caught my eye, so I started crafting a jwt token to see the contents 
and after a lot of trial and error and pain it worked 

`eyJhbGciOiJIUzI1NiJ9.eyJpZGVudGl0eSI6ImFkbWluIn0.VT1uf1w7wH4IZ7o2VddMipUJahZ44KtwUMkkOkqTFlc`


![profile-2](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/chromeDev-1.png)
![profile-2](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/profile-2.png)
![debug-2](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/debug-2.png)


**at this point I thought that's it, that's the whole thing isn't it ?**
**and it turns out no that was nothing :(**

after sometime I got frustrated and needed some help so I talked to my teammate https://twitter.com/ianonhulk
and we kept on trying and trying for hours and nothing helped 

so we just started from the beginning and backtracked our tracks :)
I was just taking a look again at /profile and I was like `hmmmmm is that a f***ing VHOST`

![vhost](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/vhost-2.png)

I added all the weird domains to my `/etc/hosts` and started playing around 
and it didn't work like WTF, so I tried with the vhost from `/debug` and it worked :P

![vhost](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/vhost-3.png)
![api](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/api-1.png)
after this amazing discovery I started fuzzing the api
and I got some other endpoints 

![disearch-api](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/apiFuzz-1.png)

now only `/reports` caught my eye but it's forbiden **hmmmmmmmmmm**:

![api-reports](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/apiReports-1.png.png)

I also guessed `/reporters` because you know it makes sense, it's also forbiden :(

after examining the header we found out that we can bypass the protection with the api key from the /debug on the first domain, with some trial and error we found out that it's the `api-key` header 

![reports](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/apiReports-2.png)
![reporters](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/reporters.png)

**so are we done yet ?**
**NO** 

it turns out the api is useless nothing unique 

we kept on banging our heads until I read the hints about different castles and docs ..etc
so this challenge is inspired by hackerone and stuff so the api docs should be like this https://api.hackerone.com/v1/api-docs/v1/swagger.json


after a couple of hours of pain and a lot of hard metal music we found out the right vhost and path
http://swagger.rbtrust.internal/swagger.json
I just started screaming because it was the only thing I wanted for hours 

![docs](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/apiDocs-1.png)

so from the docs we found out that there's a hidden param in the api for /debug
http://api.rbtrust.internal/debug?url_48902=file:///etc/passwd

![etc/passwd](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/etcpasswd-1.png)
we can see `/home/jobert` so the flag should be `/home/jobert/flag.txt` 

**YES YES, STILL ARE WE F\*\*\*CKING DONE YET **
**NO, there's still alot of pain and sacrifice**

at this point there was still 30 minutes for the CTF and I need the flag

so the hints have something to do with `$CLOUD_SERVER` or whatever
from the /debug we can clearly see it's an aws, so we started playing around with aws stuff
the only useful thing we found was this http://api.rbtrust.internal/debug?url_48902=http://169.254.169.254/latest/meta-data/identity-credentials/ec2/security-credentials/ec2-instance


![dirsearch](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/awsSecrets-1.png)

**STILL WHERE'S THE FLAG GUYS**

there was no flag or anything important so we got a good idea about s3 buckets
anddddd the keys for the s3 was wrong :(

15 mins left and still nothing WTF, my teammate was like `I need the f***ing flag`

so after reading some writeups and stuff we discovered that the aws keys are in `/home/jobert/.aws/credentials`
and it worked :P

![creds](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/jobert.png)

![ssts](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/awsStss-1.png)

**ARE WE DONE YET SRSLY GUYS**

still no, we had another thing, at that time we didn't know about the tool to bruteForce for the right bucket
so we had to guess, we had 6 mins left for the CTF my hands were shaking and I didn't know how to type.

and it was rbtrust-internal


![flag](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/S3-flag.png)

**YES YES, but wait a minute how can I read the flag hmmmmmmmm?**

I didn't know what to do, so I had to break it whatever it costs
after some trial and error I got it 

`aws s3 cp s3://rbtrust-internal/flag.txt ./1 `
and done
submitted 2 mins before the ctf ends :D


![flag](https://github.com/pop-eax/DawgCTF/raw/master/Web/the%20hacker%20one/imgs/Final-flag.png)

`flag{get_em_uPy4TWP1SQlcaukrU8GPe}`  
