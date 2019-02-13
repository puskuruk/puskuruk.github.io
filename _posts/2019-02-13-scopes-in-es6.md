---
title: Scopes In JavaScript(ES6) Explained With Example
layout: post
---

# What is scope really?

Scopes are basically our variable's area of influence. You can think like this: You are a game developer. If  your game is exclusive to Nintendo Switch you can only reach Nintendo Switch owners and your area of influence will limited to the Nintendo Switch users. But if your game will released to all platforms you can reach everyone.

In javascript we have three different type of variables. These are "var", "let", "const".

### const 
----
You can simply understand from it's name. It's a constant. This means you can't change after you defined a variable which you create with const. 

If we define a constant and we try to change like this example:

```javascript
const constantVariableDefinedGlobally = 4;
try{
	constantVariableDefinedGlobally =  2;
  console.log(`constantVariableDefinedGlobally: ${constantVariableDefinedGlobally}`);
}catch(error){
  console.log(`error => ${error}`);
};
```

We can't change constant variables. Because of this in this example we took this error:

```javascript
error => TypeError: Assignment to constant variable.
```

If we define a new constant inside of our function and when we try to call it:
```javascript
const constantVariableDefinedGlobally = 4;
//setted our constantVariable to use in our example

const functionBlockForConstant = () =>{
  const blockScoped = 3
  try{
    console.log(`blockScoped calling from inside`);
    console.log(`blockScoped: ${blockScoped}`);
    console.log(`constantVariableDefinedGlobally:  ${constantVariableDefinedGlobally}`);
  }catch(error){
    console.log(`error => ${error}`);
  }
}; 
```

It will give us with no errors:

```javascript
blockScoped calling from inside
blockScoped: 3
constantVariable: 4
```

[Click to see full code of constant example](https://gist.github.com/puskuruk/68851c9dac12ffeafeffcdde07d4f1f3)

### let && var
-------
You can change let and var after you defined but their scopes are different. Simply you can think like let is your Nintendo Switch's exclusive game and var is your game which will released to all platforms. But there is another thing let can't be declared one more times with let unlike var. For example
```javascript
try{
  var varVariable = 2;
	var varVariable = 3;
  console.log(varVariable)
}catch(error){
	console.log(error)
}
```
This will give us:

```javascript
2
```

```javascript

try{
  let letVariable = 2;
  let letVariable = 3;
  console.log(letVariable)
}catch(error){
	console.log(error);
}

```
This will give us:

```javascript

SyntaxError: Unexpected identifier

```

You can see their scopes in the next example. 

### Real World Example With Loops
-------
I want to show you how can be problem scopes in real life. In for loops we define a variable to stoping our loop. In this example we have two loops. One is designed with let and the other one is designed with var. 

This is the loop which is designed with let:

```javascript
const globalIndex = 3;

const functionwithLet = () =>{
  for(let i=0;globalIndex > i; i++){
    console.log(`-*>  i of functionwithLet first loop: ${i}`);
     for(let i=0;globalIndex > i; i++){
       console.log(`  --*>>  i of functionwithLet second loop: ${i}`);
     };
  };
}
```

This is an output of loop which is designed with let:

-

```javascript
========= started of functionwithLet ==============
 -------------------------------------------------
-*>  i of functionwithLet first loop: 0
  --*>>  i of functionwithLet second loop: 0
  --*>>  i of functionwithLet second loop: 1
  --*>>  i of functionwithLet second loop: 2
-*>  i of functionwithLet first loop: 1
  --*>>  i of functionwithLet second loop: 0
  --*>>  i of functionwithLet second loop: 1
  --*>>  i of functionwithLet second loop: 2
-*>  i of functionwithLet first loop: 2
  --*>>  i of functionwithLet second loop: 0
  --*>>  i of functionwithLet second loop: 1
  --*>>  i of functionwithLet second loop: 2
 -------------------------------------------------
========= finishing of functionwithLet ==============
```

This is the loop which is designed with var:

```javascript

const globalIndex = 3;

const functionwithVar = () =>{
  for(var i=0;globalIndex > i; i++){
    console.log(`-*>  i of functionwithVars first loop: ${i}`);
      for(var i=0;globalIndex > i; i++){
        console.log(`  --*>>  i of functionwithVars second loop: ${i}`);
      };
  };
}
functionwithVar(); // => calling functionwithVar

```

This is an output of loop which is designed with let:

```javascript
========= started of functionwithVar ==============
 -------------------------------------------------
-*>  i of functionwithVars first loop: 0
  --*>>  i of functionwithVars second loop: 0
  --*>>  i of functionwithVars second loop: 1
  --*>>  i of functionwithVars second loop: 2
 -------------------------------------------------
========= finishing of functionwithVar ==============
```

Did you see the problem with two examples. First one is worked how we want. Second loop's inner loop is only worked for three times and main loop is worked for one time. Second loop's problem is the scope of var. Var's scope is global and this cause inner loop can reach the main loop's "i" and it can increment the main loop's "i".

[Click to see full code of loop example](https://gist.github.com/puskuruk/7eef67dad754430c0fe36fa1aba8a531)