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

Using props and state, we may bind data in React from one component to another. As a result, React components can exchange information and instantly update when the data changes. For example: state gets updated, the value is pushed to the history

![1](https://user-images.githubusercontent.com/63656243/197559140-3c03e400-e2fc-4575-b1ef-ebb3932f03d2.png)

and then when a history entry is selected, this entry is written back to the state.

![2](https://user-images.githubusercontent.com/63656243/197559436-39252961-7605-4162-96a5-862c4863ffb7.png)



# 4. Event listener should be removed when it’s called out. When component is disappered(=unmount) from the screen in class component, event listener is removed in componentWillUnmount. Then, how do you remove event listener in functional component where you can’t use the lifecycle method?

Add the event listener in the useEffect hook and then return a function from the useEffect hook.After that, when the component unmounts, use the removeEventListener function to remove the event listener.

# 5. Event listener should be removed when it’s called out. When component is disappered(=unmount) from the screen in class component, event listener is removed in componentWillUnmount. Then, how do you remove event listener in functional component where you can’t use the lifecycle method?

because there’s a lot of class name, afraid that will call the wrong class. if using ref it would be specified. The fact that I can only access refs by design in the context where specify them is another benefit of utilizing refs. Therefore, if need to access information outside of this context, must use props, state, and possibly storage.
And this is good because it reduces or eliminates the possibility that would break your unidirectional data flow, which would make code more difficult to manage.

# 6. Explain SPA and MPA.
Arguing about which of these two types of approaches is good and bad, will be endless, unfortunately. This is what is happening out there. In my opinion, determining which approach to use is wiser than being strict with just one kind of approach. To see which one fits the application needs, it is necessary to look at the advantages and disadvantages of these 2 types of implementation.

MPA / traditional web approach , is more profitable on the side of Search Engine Optimization . This is because on each page, all elements or sections are updated and adjusted based on what is viewed and the content and content of the page. Another advantage of this method is that the development process tends to be faster but not necessarily organized. In addition, MPA has a good dependency advantage, where MPA does not depend on the client browser in the process of providing content because almost all page content is generated from the server side to be provided to the client.

However, MPA has several weaknesses that have serious implications in many ways. The highlight is the unstoppable management of Resources. Websites will tend to be slower, not optimal in long-term website development, and lack of efficiency in UI/UX interface maintenance.

SPA

Basically, the shortcomings of MPA have been overcome by the existence of SPA. Various other benefits are the application of the MVC method into the UI design interface process, so that project maintenance becomes better and structured. Save resources so that the interconnection load on the user can be reduced, fully responsive and Mobile view oriented that can be applied easily.

The drawback of the SPA method is the difficulty of SEO optimization. So most SPA methods are applied in applications that require intra-only access. This problem can be solved by using Nuxt.js, which we will discuss in a future article. SPA is also very dependent on the browser used by the client, so the optimization of the use of this method depends on the type and version of the browser.

#. 7. Why there’s an error when you move to the page like spartacodingclub.com/login instead of spartacodingclub.com after deploying to s3 bucket?


