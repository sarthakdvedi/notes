
## Create Higher Order Function -
to check different data with (against) different minLength.


### POOR APPROACH -
```js
### 1. The Single-Function Approach (Direct Approach) If you only need to validate a specific piece of data once, a simple function works fine:

function validateUsername(username)
{ if (username.length >= 5) 
	{ return true; // Validation succeeded
	} else { 
		throw new Error("Username must be at least 5 characters long.");
	}
}
// How you run it:
validateUsername("alex"); // Throws Error
```



### NEW -
```js
// Step 1: Outer function configures the rule
function createMinLengthValidator(minLength) {
  
  // Step 2: Inner function actually performs the check when you pass data to it
  return function(value) {
    if (value.length >= minLength) {
      return true;
    } else {
      throw new Error(`Input must be at least ${minLength} characters.`);
    }
  };
}
```

USE IT --->
```js
// You "build" specific validators tailored to your needs:
const validateUsername = createMinLengthValidator(5);
const validatePassword = createMinLengthValidator(8);

// Later in your code, you just run the returned functions:
try {
  validateUsername("alex"); // Fails (less than 5)
} catch (error) {
  console.error(error.message);
}

try {
  validatePassword("secret123"); // Passes (at least 8)
} catch (error) {
  console.error(error.message);
}
```