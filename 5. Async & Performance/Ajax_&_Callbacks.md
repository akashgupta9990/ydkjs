Ajax

Ajax uses callback or any other method to get data.

###
You may have heard that it’s possible to make synchronous Ajax requests. While that’s technically true, you should never, ever do it, under any circumstances, because it locks the browser UI (buttons, menus, scrolling, etc.) and prevents any user interaction whatsoever. This is a terrible idea, and should always be avoided.

Async Console

Sometimes console I/O is deferred becoz it is very slow & blocking part of many program(not just JS), so browser handle console I/O asyncronously
ex

var a = {
  index: 1
}; //Step 1
console.log( a ); // ?? // Step 2
a.index++; // Step 3

Normal flow Step1 -> Step2 -> Step3 // {index: 1}
Sometimes Step1 -> Step3 -> Step2 // {index: 2}

EventLoop
Adding functions in stack and execute one by one.
Settimeout doesn't add function in stack but after timer complete it then places the function in stack, which may already have some functions.
Till es5 JS runs under hosting environment(browser) which handle stacking of function.

Something changes From ES6

Paraller Threading

Run to completion/race condition
1. Two function is async and independent
2. Both start running
3. run-to-completion is completion of any function before other function completes.

EX
var a = 1;
var b = 2;
function foo() {
  a++;
  b = b * a;
  a = b + 3;
}
function bar() {
  b--;
  a = 8 + b;
  b = a * 2;
}
// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );

Concurrency
Means the execution of multiple tasks over a period of time
2 Types
1. Blocking Blocking a thread and waith for other thread to complete.(works in multi thread)
2. Non-Blocking(Event-Loop) - Halt the execution of function & resume after some time - Eg -> Promise, Async/Await, Generators

Noninteracting & Interaction
Two function call async and doesn't depend with each other is Noninteracting.
Vice-Versa - Interacting.

Cooperation
