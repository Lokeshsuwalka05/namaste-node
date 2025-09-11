EPISODE-3=>

- Node.js is a js run time environment because when you go to terminal and write node and then hit enter.after that you can run any js code.
- Node REPL(read,evaluate,print loop)the code
- Node js behind the scene using v8 to execute the code
- Chrome Browser has it's own global object which is know as (this,self,window,frames) And the global object has so many things inside it like setTimeOut,setInterval,fetch and many things.
  console.log(this);
- Node.js is also have a global object which is known as global itself.
  it gives us some feature which is in Browser.
  run console.log(global) for node.js and you are able to see the superPowers.
- Global is not the part of V8 engine.It is one of the super power which is provided by the Node.js.

- so in the case of Node.js 'This' is an empty Object.
  console.log(this)->empty object

- there are so conflict for this global object because every browser has its own global object and have different-different name so open js foundation comes with a name which is (globalThis) to remove this conflict and now we can refer globalThis as an global object everywhere.
