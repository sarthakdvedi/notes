
### Access modify -
- in a constructor, the data initialised via `this` keyword is public
- to have a private prop or method. simply make them a normal variable within the constructor function scope.
- so outside of the constructor, they won't be accessible as out of scope

```js
function createCircle(radius){
	let self = this;
	this.radius = radius;
	
	// now area is a private method
	const area = function (){
		return Math.PI * self.radius * self.radius;
		// using self and not this as this method got nothing with 'this'
		//means even if we create an obj with this fn, this method will not be in that object.
	}
	
	this.areaMultiple = function (multiple){
		return area() * multiple;
	}
}
```


---



### get / set keywords -

```js
function circle(radius){
	this.radius = radius;
	
	let location = { // private member
		x: 5;
		y: 7;
	}
	
	this.getLocation = function (){
		return location;
	}
}

const c1 = new circle(5);
c1.getLocation(); // access the method to get the value
```

#### Problems -
- we don't want to use method to get a property data.
- rather we want to use it just like an object property.
- But if we simply do that, it will no longer stay private and anyone can change it
- so we use `get` and `set` special keywords ->

```js
function circle(radius){
	this.radius = radius;
	
	let location = { // private member
		x: 5;
		y: 7;
	}
	
	Object.defineProperty(this,'myLocation',{
		get: function(){
			return location;
		}
		set: function(value){
			// any logic can be also done here
			location = value;
		}
	})
}

const c1 = new circle(5);
const locationValue = c1.myLocation; // get value as if like a property
c1.myLocation = {x: 2, y: 8}; // set value
```