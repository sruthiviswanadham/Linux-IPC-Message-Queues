# Linux-IPC-Message-Queues
Linux IPC-Message Queues
## Name: viswanadham venkata sai sruthi
## Reg.No: 212223100061
# AIM:
To write a C program that receives a message from message queue and display them

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux message queues API 

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## C program that receives a message from message queue and display them

## Writer.c
```
#include <stdio.h> 
#include <sys/ipc.h> 
#include <sys/msg.h> 

// structure for message queue 
struct mesg_buffer { 
	long mesg_type; 
	char mesg_text[100]; 
} message; 

int main() 
{ 
	key_t key; 
	int msgid; 

	// ftok to generate unique key 
	key = ftok("progfile", 65); 

	// msgget creates a message queue 
	// and returns identifier 
	msgid = msgget(key, 0666 | IPC_CREAT); 

	message.mesg_type = 1; 

	printf("Write Data : "); 
	fgets(message.mesg_text, sizeof(message.mesg_text), stdin); 

	// msgsnd to send message 
	msgsnd(msgid, &message, sizeof(message), 0); 

	// display the message 
	printf("Data sent is : %s \n", message.mesg_text); 

	return 0; 
} 
```
## Reader.c
```
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>

// structure for message queue
struct mesg_buffer {
	long mesg_type;
	char mesg_text[100];
} message;

int main()
{ 
	key_t key;
	int msgid;

	// ftok to generate unique key
	key = ftok("progfile", 65);

	// msgget creates a message queue
	// and returns identifier
	msgid = msgget(key, 0666 | IPC_CREAT);

	// msgrcv to receive message
	msgrcv(msgid, &message, sizeof(message), 1, 0);

	// display the message
	printf("Data Received is : %s \n", message.mesg_text);

	// to destroy the message queue
	msgctl(msgid, IPC_RMID, NULL);

	return 0;
}

```



## OUTPUT
![WhatsApp Image 2024-10-01 at 15 51 15_3558ea50](https://github.com/user-attachments/assets/f4fe87ab-e2d8-418e-be36-19e765a37b88)
![WhatsApp Image 2024-10-01 at 15 51 50_986e9a97](https://github.com/user-attachments/assets/dedf6434-2fcd-486f-87f9-c1921db4519e)





# RESULT:
The programs are executed successfully.
