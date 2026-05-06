## Running the binary
Firt thing i do is open .exe and see what its going to behave. Thats what program is outputing:

After trying to input something program ends immediately, maybe its printing out if i succesfully logged in or no but loop ends because it have no sleep or anything to stop loop from ending.

![](screenshots/level1.1.png)


## Dissasembling with IDA
Lets put it in IDA and ispect more. First thing im doing is hitting Shift + F12 and checking strings.

![](screenshots/level1.2.png)

Nice! I can clearly see message i saw earlier. Also i see some strings used to determinate if flag is correct.
Lets take a look at this string and where and when is it used.


![](screenshots/level1.3.png)

After checking xrefs we can see in what function is it used in. Lets check that out thats where password logic probably is.

![](screenshots/level1.4.png)

There is moment where program ask for password and is using fget function with maximum size of 0x40 bytes. This mean the buffer can store up to 63 characters plus null terminator, so there is no overflow risk.
Next step is to try inputing 12345 as password and see what does program do with it and what does it compare it to.

![](screenshots/level1.5.png)

Alright so register rcx is storing a pointer to a memory region with the string we entered. Lets keep a track of it.


![](screenshots/level1.6.png)

Now its the point where program compare two strings:
First one is : CTF{CongratuLations-U_$olved-the-first_Level!}
second one is our password we entered: 12345


![](screenshots/level1.7.png)

Of course its gonna be wrong but now we know password is : CTF{CongratuLations-U_$olved-the-first_Level!}

## flag
CTF{CongratuLations-U_$olved-the-first_Level!}

![](screenshots/level1.8.png)