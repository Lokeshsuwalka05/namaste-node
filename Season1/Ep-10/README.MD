Thread Pool:-
it handles heavy ops like file I/O(fs.readFile etc.),DNS(dns.lookup),Crypto and some user specified input:-
so in the case of Reading a file below Happens:-
➡️ Libuv Thread Pool
➡️ OS reads file
➡️ Callback placed in Poll Phase Queue
➡️ Event Loop executes callback

at os level there are so many threads but
UV_ThreadPool_size is 4 by default.
but if 5 file read call happens simultaneously then what happened??
-> the 5th call will wait for thread to be empty .
->first 4 excute at the same time but last one excute after some time.

- But you can change the thread pool size as well by using a variable
  =>process.env.THREADPOOL_SIZE=2;
  =>THE MAX LIMIT OF THREAD POLL SIZE IS 128
  =>IF YOU WRITE MORE THAN 128 THEN NODE WILL AUTOMATICALLY RESETS IT TO THE 128.

- so,is Node.js is single threaded or multi threaded?
  =>v8 engine is single threaded but libUv has thread pool but libuv uses this thread pool only for some heavy operations like file i/O,dns.
  =>it depends on the operations whether it is single threaded or multi threaded.

- Suppose there are multiple request incoming so there is a epoll sitting at the kernal level in os,there is file descriptor also knows as socket descriptor manages all the incoming request and after that os notifies the LIBUV and by using event loop(poll phase) it goes into the call stack for execution.
- epoll(for linux) and kqueue(for macos) and similary for windows.It is a scalable i/o event notification mechanisms means it notifies to the LIBUV when a i/o event is performed by external user.
- epoll behind the scene using red black tree and we are saying data structure is not important
- and these timer queue is also using min heap behind the scene.

->Read about epoll and kqueue
->read about fds(file descriptor/socket descriptor)
->read about eventmitter
->read about streams and buffer
->read about pipes

#lernings
"Don't block the main thread(call stack)"

- don't use sync methods
- Heavy json object
- complex regex
- complex calculations/loops

"Data structure is important"

"Naming is very Important"

process.nextTick() and setImmidiate()
1 tick means a full cycle and process.nextTick should call after 1 tick but what happens you know very well😂.
and setImmidiate() should be called immediately but it call after 1 tick.😂

"There's lot to learn"
