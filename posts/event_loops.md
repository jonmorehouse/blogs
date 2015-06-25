Writing a web server in a dynamic programming language, usually means
combatting sometimes slow responses to outside systems while handling a
moderate level of requests. Most modern dynamically typed languages will work
under what is referred to as a "Global Interpreter Lock", which is the language
executable's way of enforcing us to work with a single thread at a time.  Here
at BuzzFeed, we primarily write services in CPython which uses the GIL to keep
things thread safe, by utilizing only one thread at a time. While a single
threaded environment keeps code simple and the memory namespace unobstructed,
it does limit true concurrency. Without true concurrency, engineers use
asynchronous programming patterns to account for slow system calls while still
handling as many requests as possible.

Asynchronous programming is a technique with which programs can "multitask" and
work through other computer instructions while waiting for sometimes slow
system calls to respond. What this means, as a programmer, is that one slow
call to a database will not bring an entire server to a halt. Async programs
are commonly implemented using what is called the Reactor pattern. The reactor
pattern uses what is referred to as an event loop to poll multiple file
descriptors at the operating system level, and process their responses as they
arbitrarily finish. An event loop is a system in which computer instructions
are queued for later execution, so as to allow a program to act freely while a
network or filesystem call respond. Once a socket finishes transferring data, a
file descriptor is signalled as ready and the operating system will signal a
notification, which the event loop then serializes into an executable task,
essentially finishing the original caller's job.

Libuv, libevent and libev are common C libraries that are wrapped and exposed
to higher level languages. Python is rich with asynchronous libraries, most of
which work to provide Python friendly api's on top of these lower level
libraries. Pyuv is a wrapper around libuv, exposing a reactor pattern based
event loop in python. 

# example 1 gist here


