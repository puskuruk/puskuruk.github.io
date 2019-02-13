---
title: Default Parameter in ES6
layout: post
---

For example we store user credientals in object but user couldn't logged in then we must have a default parameters.

```javascript
let defaultUserCredientals = {
	userId: ' ',
	email: ' '
}

const userLoggedIn = ( userCredientals = defaultUserCredientals) =>{
	let userId = userCredientals.userId;
	let email = userCredientals.email;
	if(userId !== ' ' && email !== ' '){
		console.log('Succesfully Logged In')
	}
	else{
	console.log('There is a problem with login');
	}
}

userLoggedIn();
```

Output of this code:

```javascript
There is a problem with login
```