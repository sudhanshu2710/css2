1) Why is hoisting?
In JavaScript, Hoisting is the default behavior of moving all the declarations at the top of the scope before code execution.

hositing is the phenomina in js by which we can access the variables and functions even before we have initialized a value on it or without putting some value in it.

Example: 
	
 console.log(x);
 greeting();  

 var x = 10;
 function greeting() {
    console.log("Hi");
 }

   In hoisting, before execution of the code the variables and functions are defined in the memory.
x = undefined
greeting: f 


2) what is scope?
	scope means where we can access specific variable or a func in our code.
	local scope and global scope.
  scope is directly related to lexical environment
Function scope:
    Function Scope: When a variable is declared inside a function, it is only accessible within that function and cannot be used outside that function. 
Block Scope: 
     A variable when declared inside the if or switch conditions or inside for or while loops, are accessible within that particular condition or loop.
Example:
function a() {
  console.log(b);
}
var b = 10;
a()

ans: 10

 Now, can we access b inside funcion a. or is var b inside a scope of function a
	the ans is: first js tries to find b in local scope that is within its function. If b is present then it prints b else it will try to find b in global scope that is outside the function 

function a() {
console.log(b);
}

a();
var b = 10;
ans: undefined


function a() {
 var b = 10;
 c();
 function c() {
 }
}
a();
console.log(b) // undefined bcoz of function scope

3)How are var, let const different?
	var declarations are globally scoped or function scoped while let and const are block scoped.var variables can be updated and re-declared within its scope; let variables can be updated but not re-declared; const variables can neither be updated nor re-declared. They are all hoisted to the top of their scope.
var a = 10;
a = 30;
var a = 20; //valid

let a = 10;
a = 20; //valid 

let a = 10;
let a = 20; //not valid;

const a = 10;
a = 20; // not valid 

const a = 10;
const a = 20; //not valid;


4)What are the two main differences in arrow functions?
	arrow functions do not have their own this. The syntax is different in arrow function and it may reduce the no.of lines of code. We cannot use arrow function in methods and constructor.

The behavior of this inside of an arrow function differs considerably from the regular function's this behavior. The arrow function doesn't define its own execution context.

In methods: 

let camera = {
	price: 3000,
	color: "black",
	description1: function () {
		console.log(this);
	},
	description2: () => {
		console.log(this);
	},
};
camera.description1(); // it will print ans
camera.description2(); // this will give {}


4)Does Call apply bind work for arrow functions?
  No, call apply bind doesnt work in arrow function, bcoz arrow function doesnt have this keyword.


5)What does call apply bind do?
  The call() method takes arguments separately. The apply() method takes arguments as an array. The apply() method is very handy if you want to use an array instead of an argument list.
Example:
let name = {
    first_name: "Siva",
    last_name: "sangari",
}
let printFullName =  function(city,state) {
    console.log(`${this.first_name} ${this.last_name} is from ${city}, ${state}`);
}
printFullName.call(name, "Trichy", "TamilNadu");
printFullName.apply(name, ["Trichy", "TamilNadu"]);

const store = printFullName.bind(name, "Trichy", "TamilNadu");
store()

7)What are closures?
	function along with its lexcial scope forms closure.The variable scope inside the parent function is maintained even if the function execution is completed.
function a() {
  let num = 1;
  function b() {
     console.log(num)
  }
  return b
}
a()()

8)Event bubbling?
	Event bubbling is a method of event propagation in the HTML DOM API when an event is in an element inside another element, and both elements have registered a handle to that event. It is a process that starts with the element that triggered the event and then bubbles up to the containing elements in the hierarchy.

Example:
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta http-equiv="X-UA-Compatible" content="IE=edge" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Document</title>
		<style>
			div {
				border: 1px solid black;
				padding: 30px;
				min-height: 200px;
				cursor: pointer;
			}
		</style>
	</head>
	<body>
		<div id="grandparent">
			<div id="parent">
				<div id="child"></div>
			</div>
		</div>
	</body>
</html>

<script>
	document.querySelector("#grandparent").addEventListener("click", () => {
        console.log("grandparent");
    });
    document.querySelector("#parent").addEventListener("click", () => {
        console.log("parent");
    });
    document.querySelector("#child").addEventListener("click", (e) => {
        e.stopPropagation()
        console.log("child");
    });
</script>

9)What is event loop?
	Js is a synchronous, single threaded language. But there will be some kind of code which will take long time to execute(example: fetching data). All the code are executed inside a call stack. So those code which takes time will register a callback inside webAPI once it fetches data successfully it goes inside callback queue. The fetched data will wait inside callbackqueue. The event looop will monitor callstack and callback queue, once callstack is empty the event loop will push fetched data into call stack.

10)Explain promises to a 5 year old, with simple examples
   When there is a dependency b/w success and failure. The result is unknown i.e., it can be success or failue.
   A promise is used to handle the asynchronous result of an operation. JavaScript is designed to not wait for an asynchronous block of code to completely execute before other synchronous parts of the code can run. With Promises, we can defer the execution of a code block until an async request is completed. 

example:
function one() {
	return 1;
}

let two = () => {
	return new Promise((resolve, reject) => {
		setTimeout(function () {
			resolve(2);
		}, 3000);
	});
};

function three() {
	return 3;
}

const print = async () => {
	var valOne = one();
	console.log(valOne);

	var valTwo = await two();
	console.log(valTwo);

	var valThree = three();
	console.log(valThree);
};

print()

11)what does async await mean?
  An async function is a function declared with the async keyword, and the await keyword is permitted within it.
Async: It simply allows us to write promises based code as if it was synchronous and it checks that we are not breaking the execution thread.
The async keyword is used to define an asynchronous function, which returns a AsyncFunction object. The await keyword is used to pause async function execution until a Promise is fulfilled, that is resolved or rejected, and to resume execution of the async function after fulfillment.

12)What does the this keyword mean?
For all regular function calls, this points to window object.
function hello() {
    console.log(this);
} //here this points to global obj

hello();
const camera = {
  price: 321,
  description: function () {
     console.log(this); //here this points to camera
     console.log(this.price); //here this points                                           to camera.price
     },
};
camera.description()

console.log(this) //in node {}
console.log(this) //in browser window 

Whenever a js code is executed, a global execution context is created. The js engine creates window obj along with it it creates "This" keyword.
When the function being referenced is a regular function, “this” references the global object. 
window: window is a global obj which is created along with global execution context.

so whenever any js code is running, a global obj is created, global execution context is created along with the execution context, this keyword is also created.

At the global level this is equal to window

this === window => ans: true

example:
function hello() {
    console.log(this);
}

hello();


write a program to flatten an array?
var arr = [1, [2, 3], [3], [[[5]], 6]];

const flatten = (arr) => {
    someNewArr = arr.reduce((acc, item) => {
		if (Array.isArray(item)) {
			acc = acc.concat(flatten(item));
		} else {
			acc.push(item);
		}
		return acc;
	}, []);
    return someNewArr;
}

console.log(flatten(arr));

function currying?
  currying is when a function — instead of taking all arguments at one time — takes the first one and returns a new function, which takes the second one and returns a new function, which takes the third one, etc. until all arguments are completed.
  Currying is helpful when we have to frequently call a function with a fixed argument.
  It can be done using bind method or closure.

Examples:
let multiple = function (x,y) {
    return x*y
}
let multipleByThree = multiple.bind(this, 3)
console.log(multipleByThree(2));

const sendRequest = (greet) => (name) => (message) =>
	`${greet} ${name}, ${message}`;
console.log(sendRequest("Hello")("John")("Please can you add me to your Linkedin network?"));

let mul = function (x) {
	return function (y) {
		return x * y;
	};
};
let multiplyByTwo = mul(2);
console.log(multiplyByTwo(3))

debouncing?
  In JavaScript, a debounce function makes sure that your code is only triggered once per user input.
Example: search box

Debouncing and throttling both used for optimization and performance of a webapp.

sometimes our function is called lot of times. So we could limit the rate of execution and optimize the performance of web app.

how ofter or how freqently user is resizing the window then throttling is better. IF we want to know how many times user resized then debouncing is better


Pure function and impure function:
pure function:
function x(a, b) {
    return a + b;
}

console.log(x(1, 2));
console.log(x(1, 2));

impure function:
var global = 0
function x(a, b) {
    global = global + a + b
    return global
}

console.log(x(1, 2));
console.log(x(1, 2));
console.log(x(1, 2));