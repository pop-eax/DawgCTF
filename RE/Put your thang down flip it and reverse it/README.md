# Put your thang down flip it and reverse it

so this challenge was a little bit messy 

I started by looking at the main function in Cutter:
![main function](https://github.com/pop-eax/DawgCTF/raw/master/RE/Put%20your%20thang%20down%20flip%20it%20and%20reverse%20it/main.png)

from here I knew that the flag length is 43

digging deeper into the app I started to feel more lost 
![complexAsm](https://github.com/pop-eax/DawgCTF/raw/master/RE/Put%20your%20thang%20down%20flip%20it%20and%20reverse%20it/complex.png)
each function is weirder, and more complicated

at this point I thought that writting a decoder in python will just be a pain
so I fireup ltrace

`ltrace ./missyelliott`

![ltrace](https://github.com/pop-eax/DawgCTF/raw/master/RE/Put%20your%20thang%20down%20flip%20it%20and%20reverse%20it/ltrace.png)

in this picture we can see the encoded flag in the strcmp, but it's kinda trimeed 
so I used `ltrace -s 50 ./missyelliott`
at this point I thought of creating a dictionary based on all the alpahapet :)
after playing with some input, I relaized that the encoder can work as a decoder
it just works both ways 

![dict1](https://github.com/pop-eax/DawgCTF/raw/master/RE/Put%20your%20thang%20down%20flip%20it%20and%20reverse%20it/dict.png)
![dict2](https://github.com/pop-eax/DawgCTF/raw/master/RE/Put%20your%20thang%20down%20flip%20it%20and%20reverse%20it/image.png)
so I just threw the encoded flag and here we go:
`echo -e "A\365Q\321Ma\325\351i\211\031\335\t\021\211\313\235\311i\361m\321}\211\331\265Y\221Y\2611Ym\321\213!\235\325=\031\021y\335"| ltrace -s 50 ./missyelliott`

![decoded_flag](https://github.com/pop-eax/DawgCTF/raw/master/RE/Put%20your%20thang%20down%20flip%20it%20and%20reverse%20it/flag.png)

`DawgCTF{.tIesreveRdnAtIpilF,nwoDgnihTyMtuP}`


and it worked :D


