- Js engine has only one thread(Call Stack).All the codes is executing in this thread only and all the synchoronous operations are performed by this thread and for async opertaions it passes these to LIBUV.
- but Node.js has some sync functions,by using those functions we can actually block the main thread.
  for an example,
  =>readFileSync which is in the fs module which is provided by the Node.js.
- Menas Synchronous methods-Will Block the Main thread-Don't use it
- Learn in this lecture
  =>sync code
  =>Async code
  =>Blocking sync code
  =>setTimeOut(cbfn,0)=>trust issue=>only runs when global excution popped out from the call stack
  =>Non Blocking I/o=>I/o operations which are not blocking the main thread=>event loop,callBack,promises,Async-await
  =>Main thread
  =>Async I/O
  =>LIBUV Github
