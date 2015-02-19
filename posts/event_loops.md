As software engineers, we write programs that work with the kernel and the system calls it offers us (example of system calls here).

Due to the nature of operating systems and how the kernel dispatches resources or responds to these calls, our program can get bottlenecked while waiting for a response. When you go to read from a file, 


kernel = computer program that manages i/o requests from software and maps them to the cpu/gpu and other pieces of hardware. It does that by creating data processing instructions, which tell the hardware how to interact. Programs that we write interact with the kernel via system calls, since the kernel is in charge of mediating and serializing requests at the hardware level, as engineers we can imagine that it takes a bit of time for a response.

While waiting for the kernel to respond with a meaningful message from the hardware, the program being executed is essentially rendered idle, in a single threaded context. Since the program can only execute one instruction at a time, in a single threaded context, it must wait until the previous line executes. This is called procedural programming.

The event loop is one attempt at solving this problem and allowing a program to multitask while waiting for feedback from teh kernel. Usually run in two distinct threads behind the scenes, an event based program runs what is called an "event loop" which continually loops through different execution pieces of the program, checking whether or not they are ready to be called and divvying up work between different handlers. If you could imagine a program which is responsible for reading from multiple files, the event loop






Writing a web server in a dynamic programming language, usually means combatting writes to databases in a single thread. Most modern dynamically typed languages will work under what is referred to as a "Global Interpreter Lock", which is essentially the language executable's way of enforcing us to work with a single thread at a time, exclusively. Here at BuzzFeed, we primarily write services in CPython which uses the GIL to keep things thread safe, by utilizing only one thread at a time. Building a web server that needs to communicate with the file system, an outside api or database means combatting blocking calls to services outside the programs' domain. At scale, handling a single request per process and "blocking" or "waiting" for these outside services to respond becomes unacceptable. 

Asynchronous programming is a technique with which programmers can use a single thread context, yet avoid blocking an entire program while waiting for a response from an outside service. By utilizing an event loop library such as libev, libuv or libevent an asynchronous program can write code that responds to events as opposed to writing code in a procedural manner. Instructions for handling responses from calls outside of the programs execution environment can be sent to that api call, and will only be executed after a response from that call is made. Network and file calls implicitly write to a socket which is then processed by a system handle and exposed via a file descriptor at the OS level. Part of the responsibility of an event loop is to poll the correct handles and then respond to notifications from these handles. From a python programmers perspective, this means that the lower level library will be responsible for queing your callback and then executing it at a later time when the system call responds. From a high level, an event loop is simply responsible for responding to events of interest and subsequently executing the corresponding code associated with the event after the fact.

~~~ python





~~~





