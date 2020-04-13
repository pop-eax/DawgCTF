# Put your thang down flip it and reverse it

so this challenge was a little bit messy 

I started by looking at the main function in Cutter:
![alt text](https://raw.githubusercontent.com/username/projectname/branch/path/to/img.png)

from here I knew that the flag length is 43

digging deeper into the app I started to feel more lost 
![alt text](https://raw.githubusercontent.com/username/projectname/branch/path/to/img.png)
each function is weirder, and more complicated

at this point I thought that writting a decoder in python will just be a pain
so I fireup ltrace

`ltrace ./missyelliott`

![alt text](https://raw.githubusercontent.com/username/projectname/branch/path/to/img.png)

in this picture we can see the encoded flag in the strcmp, but it's kinda trimeed 
so I used `ltrace -s 50 ./missyelliott`
at this point I thought of creating a dictionary based on all the alpahapet :)

after playing with some input, I relaized that the encoder can work as a decoder
it just works both ways 

![alt text](https://raw.githubusercontent.com/username/projectname/branch/path/to/img.png)

so I just threw the encoded flag and here we go:
`echo -e "A\365Q\321Ma\325\351i\211\031\335\t\021\211\313\235\311i\361m\321}\211\331\265Y\221Y\2611Ym\321\213!\235\325=\031\021y\335"| ltrace -s 50 ./missyelliott`

![alt text](https://raw.githubusercontent.com/username/projectname/branch/path/to/img.png)

`DawgCTF{.tIesreveRdnAtIpilF,nwoDgnihTyMtuP}`


and it worked :D


