## <mark> State Management

```
import React from 'react'
// Your task is to explain why the console.log shows the older value of count
function App() {
  const [count, setCount] = React.useState(0);

  const handleClick = () => {
    setCount(count + 1);
    console.log(count); // You will see the older value of count in console
  };

  return (
    <div>
      <p>Button is clicked {count} times</p>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

export default App
```

- In This Above code ,When you click the button it re-renders the components but schedules the updation...because of async behaviour of setCount.That's whey when you console log count in handelClick function it give the older value of count .

## Multiple State Updates

```
import React from 'react'

// Your task is to explain why count value is not updated to 3 as expected
function App() {
  const [count, setCount] = React.useState(0);

  const handleClick = () => {
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);
		console.log(count);
  };

  return (
    <div>
      <p>Button is clicked {count} times</p>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

export default App
```
- In this code , when you click the button it re-renders the components and you will get 1 ...no matter how many times you call the setCount . Due to React's batching, all these updates are processed together. As a result, count increases only by 1, not 3, even though setCount is called three times.

####Solution :
- This can be solved by using callback funtion in setCount 
```
function App() {
  const [count, setCount] = React.useState(0);

  const handleClick = () => {
    setCount((prevCount) => prevCount + 1);
    setCount((prevCount) => prevCount + 1);
    setCount((prevCount) => prevCount + 1);
    console.log(count);
  };

  return (
    <div>
      <p>Button is clicked {count} times</p>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

const reactRoot = ReactDOM.createRoot(document.getElementById("root"));
reactRoot.render(<App />);
```

- In this Above code, I am using callBack function that takes the most resent value of count . The count value not taken by this line - `const [count, setCount] = React.useState(0);`. React internally storing this state value and invoking it . Due to this we get count value as 3 not 1.