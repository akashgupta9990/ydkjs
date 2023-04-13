Values & Types
1. String -> "abc"
2. Number -> 33
3. Boolean -> true
4. Undefined -> undefined
5. Object/Null -> {a:1}, typeof null also return object(weird error, can't be fixed now as so many codes now depends on this)
7. Function -> function() {}
6. Symbol(ES6)

Objects
Dot/Bracket Notations
    var obj = {
      a: "hello world",
      b: 42
    };
    var b = "a";
    obj[b]; // "hello world"
    obj["b"]; // 42

Array
Function
    var foo = function() {
      return 42
    };
    typeof foo -> function
    typeof foo() -> number
    foo.bar = "string"; typeof foo.bar -> string

  IIFE(Immediately Invoked Function Expressions) -> function will call as soon as it is defined
  (var foo = function() {console.log(this)})();

Coercions topics
Falsy conditions
1. "" Empty String
2. 0, -0, NaN 
3. null, undefined
4. false

Truthy Conditions
1. "hello"
2. 23
3. true
4. [], [1]
5. {}, {a: 2}
6. function foo() {}

String will coerce to number when == is used
Array & object are compared with refrences so two array/object will always return false when compared even if both contains the same values.
Array will be coerced to string on comparision
Comparision between string will be lexicographically (aka alphabetically like a dictionary)

var a = [1,2,3];
var b = [1,2,3];
var c = "1,2,3";
a == c; // true
b == c; // true
a == b; // false

#Function Scopes
Variable Hoisting -> at compile time all global variable is defined first then function will execute
Note: (Only variable is defined, values will be defined later, let keyword doesnt support hoisting)
Nested Scopes
Conditionals -> if else/Swith case

Strict Mode -> Javascript engine will become strict
  // Non Strict Mode
    function foo() {
      a = 1; // a is not defined here
    }
   foo();
   a -> 1

  //Strict Mode
    function foo() {
      "use strict"
      a = 1; // a is not defined here
    }
   foo();  // ReferenceError: a is not defined

#Closure
var foo = function(x) {
  var bar = function(y) {
    console.log(x+y)
  }
  return bar;
}

here bar knows what the value of x and can be assigned to other value.

  #Modules
  Module is something like it will make some functions/variables as private level which will be not visible to outside api's/functions.
  function User(){
    var username, password;
    function doLogin(user,pw) {
      username = user;
      password = pw;
    }
    var publicAPI = {
      login: doLogin
    };
    return publicAPI;
  }
  // create a `User` module instance
  var fred = User();
  fred.login( "fred", "12Battery34!" );

  every execution of User() will create a new instance which will retain the username, password variable even after the function is executed & those variable will never be changed even we have not declared those as const.

#this Keyword
  every function have a this keyword which points to an instance.
  That instance is defined on how a function is executed.

  function foo() {
    console.log( this.bar );
  }
  var bar = "global";
  var obj1 = {
    bar: "obj1",
    foo: foo
  };
  var obj2 = {
    bar: "obj2"
  };
  foo(); // "global"
  obj1.foo(); // "obj1"
  foo.call( obj2 ); // "obj2"
  new foo(); // undefined new will always creae a new instance.

#Prototypes
  When an object is created using refrence of another object it will inherit all it's properties
  var obj = {
    foo: 'bar'
  }
  var obj1 = Object.create(obj);
  obj1.bar = "foo";
  obj1.bar = "foo";
  obj1.foo -> "bar"; // foo came from protype

  the foo object is not actually present in obj1 but since it an instance of obj it will inherit all it's properties.

  obj1._proto_

#polyfilling
  Converting newer feature into old code to support it on old browser is polyfilling
  Since Number.isNaN is a new ES6 feature
  Ployfill of this is
  if (!Number.isNaN) {
    Number.isNaN = function isNaN(x) {
      return x !== x;
    };
  }
  Almost all newer code can be polyfilled but some code cann't be polyfilled so we use external libraries for those(eg -> ES5-Shim, ES6-Shim)

#transpilling(transform + compile)
  There is no way we can polyfill newer syntax as it will cause error
  For those we use transpilling, it will convert newer code to equivalent old code

  function foo(a = 2) {
    console.log( a );
  }

  Transpilled code
  function foo() {
    var a = arguments[0] !== (void 0) ? arguments[0] : 2;
    console.log( a );
  }

  Some Transpiller -> Babel, Traceur


# Non Javascript
  Some code we write is not controlled by Javascript but controlled by host(mostly browsers)
  Eg -> document.getElementById('foo');, alert, console.*

  document is a global variable handled by host and is called special object/host object
  DOM and its behaviour is implemented in C/C++
  
# Enumerable
  If enumerabke it will not be showun in Object.keys/loops.
  ```js
    var sym = Symbol("sal");
    var person = {
        name: "Bob",
        [sym]: 200
    };

    const symbols = Object.getOwnPropertySymbols(person);
    const salSym = symbols.find(sym => {
        return sym.description && sym.description.includes("sal");
    });
  ```
