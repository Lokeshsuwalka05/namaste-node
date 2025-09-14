- module is collection of javascript code which is separate and private to itself.

- IIFE(immediately invoked function expression)
  =>()();

  =>(function(name){
  console.log(name)
  })("lokesh");

- in node.js how the iife works??
  =>(all of the code of a module is written inside it when we are calling the require() function then outside parantheses called this function immediately)();

- How are variable and function private in different module??
  =>so the answer is IIFE-->()()
  =>all of the code of a module is written inside it when we are calling the require() function then outside parantheses called this function immediately.

- So,how do you get access to module.exports??
  =>because node.js passess (module) as a parameter to the IIFE.require is also passed in it.

- And went Deep dive into the node.js repository
