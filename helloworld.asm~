; hello world in x86_64 assembler
; Befehl zum Assemblieren: nasm -f elf64 helloworld.asm && ld -o helloworld helloworld.o
; Syntax higlighting in vim: set syntax=nasm

section .data

		msg2 db "in Assembler!",0x0a			; string 2, carriage return (0a)
		len2 equ $-msg2							; length of string 2
		msg1 db "Hallo Welt "               	; string 1 without return
		len1 equ $-msg2-msg1                    ; length of string 1

section .text

	global _start:                        		; must be declared for linker (ld)

	_start:                                     ; tell linker entry point

		mov ax,0								; initialize stack for loop count
		push word ax

	_loop:

		mov rax,4                               ; system call number (sys_write)
		mov rbx,1								; write to file descriptor 1 = stdout
		mov rcx,msg1                            ; message to write
		mov rdx,len1                            ; message length
		int 0x80                                ; call kernel

		mov rax,4								; analog "in Assembler"
		mov rbx,1								;
		mov rcx,msg2							;
		mov rdx,len2							;
		int 0x80								;
		
		pop word ax								; look at loop counter
		add ax,1								; increment loop counter
		push word ax							; remember incremented loop counter

		cmp ax,10								; 10 loop counts reached?
		jne _loop								; not -> again
		jmp _end								; else -> end

	_end:
	
		add sp,2								; reset stack pointer (1 word = 2 bytes)

		mov rax,1                               ; sys_exit
		mov rbx,0								; clear file dscriptor
		int 0x80                                ; call kernel


