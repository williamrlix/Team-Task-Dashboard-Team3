#TIL 24/10/2022

# 1. What’s the differenece between array and array-like object in javascript. How can you change each element in an array-like object?

An array is a special variable, which can hold more than one value, that we use some number as index to locate the place of value. An array-like is an object It has indexed access to the elements and a non-negative length property to know the number of elements in it. These are the only similarities it has with an array. Doesn't have any of the Array methods like, push, pop, join, map, etc.

example:
let person = {
  first_name: "John",
  last_name: "Doe",
  company: "capscode",
};

var arr_like_obj = {
  0: "we",
  1: "are",
  2: "capscode",
  length: 3,
};

as usual when we whant to change the value of array we just need to use Array methods like, push, pop, join, map, etc. but we cant do that on array-like object. but we still can change the object with map() methods that can be used to loop across an object array of objects to update an object’s property. Determine if the current object is the one that has to be modified on each iteration. If so, change the item and send back the modified version; if not, send back the original object. Example :
const arr1 = [
{id: 1, name: ‘Alice’},
{id: 1, name: ‘Bob’},
{id: 3, name: ‘Charlie’},
];
const newArr = arr1.map(obj => {
if (obj.id === 1) {
return {…obj, name: ‘Alfred’};
}

# 2. There are parent component A and child component B. Component A has {name: “Sparta"} as its state and pass down the name value to component B. Then, component B shows the name value on the screen. Please draw the lifecycle of how the value is shown on the screen when component A’s state is changed to {name: "LearningX"}

We’re gonna create a component with a name attribute in state. This component will render that name first.

class Bootcamp extends React.Component {
 state = {
 name: “Sparta”
 };
 };
 render() {
 return <div>{this.state.name}</div>;
 }
}

Now let’s create a function changeName() in the Bootcamp component. This function will change the name in state to the actual name of the Bootcamp.

class Bootcamp extends React.Component {
state = {
name: "Sparta"
};
changeName = () => {
this.setState({
name: "Learning X"
});
};
render() {
return <div>{this.state.name}</div>;
}
}

After that create the App component which will render this Bootcamp component and a button. When we click the button it gonna changes the state. We have added a function handleClick() which will get called when the user clicks the button. We need to figure out a way to update the state of the child component, that is the Bootcamp component.

We have created a function changeName() in the Bootcamp component. This function will show the next change of Bootcamp. If we can call this function from the App component, our work is done. So we will call this function. And then we can refs, let’s create a ref of the Bootcamp component in the App component using React.createRef() method and attached the ref to the Bootcamp component using the ref attribute.

Now we will be able to refer the Bootcamp node using this.bootcampELement.current. We will also be able to call the changeName() function in the Bootcamp component using this.bootcampElement.current.changeName().

Let’s update our handleClick() function in our App component to call the changeName() function.

and then..
const Bootcamp= forwardRef((_, ref) => {
const [bootcamp, setBootcamp] = useState("Sparta");
const changeName = () => {
setBootcamp("LearningX");
};
useImperativeHandle(ref, () => ({
changeName: changeName
}));
return <div>{bootcamp}</div>;
});
const FunctionApp = () => {
const bootcampElement= useRef();
const handleClick = () => {
bootcampElement.current.changeName();
};
return (
<div className="App">
<Bootcamp ref={bootcampElement} />
<button onClick={handleClick}>Change!</button>
</div>
);
};


# 3. What is two-way binding? Explain how the re-rendering is done when using two-way binding.  (Assume that there are parent component A and child component B.)
# 4. Event listener should be removed when it’s called out. When component is disappered(=unmount) from the screen in class component, event listener is removed in componentWillUnmount. Then, how do you remove event listener in functional component where you can’t use the lifecycle method?

