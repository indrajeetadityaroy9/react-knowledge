### Basic useState()

```
function App() {
  const [count, setCount] = useState(0);

  const incrementCount = () => {
    count < 10 ? setCount(count + 1) : null;
  };

  const decrementCount = () => {
    count > 0 ? setCount(count - 1) : null;
  };

  return (
    <div className="App">
      <h4>Current Count is ...</h4>
      <h1>{count}</h1>
      <button onClick={incrementCount}>+</button>
      <button onClick={decrementCount}>-</button>
    </div>
  );
}

export default App
```

```
function LoggedIn() {
    const [isLoggedIn, setIsLoggedIn] = useState(false);

    const handleLogin = () => {
        setIsLoggedIn(true);
    };

    const handleLogout = () => {
        setIsLoggedIn(false);
    };

    return (
        <div>
            <button onClick={handleLogin}>Login</button>
            <button onClick={handleLogout}>Logout</button>
            <div>User is {isLoggedIn ? `Logged In` : `Logged Out`}</div>
        </div>
    );
}

export default LoggedIn;
```

```
type Props = {
    name: string,
    email: string
}

function User({ name, email }: Props) {
    const [user, setUser] = useState<Props>({} as Props);

    function handleLogin() {
        setUser({ name, email });
    }

    function handleLogout() {
        setUser({} as Props);
    }

    return (
        <div>
            <button onClick={handleLogin}>Login</button>
            <button onClick={handleLogout}>Logout</button>
            <div>User name: {user.name}</div>
            <div>User email: {user.email}</div>
        </div>
    );
}

export default User;
```

```
interface Item {
  quantity: number;
  name: string;
  completed: boolean;
}

function App() {
  const [inputValue, setInputValue] = useState("");
  const [items, setItems] = useState<Item[]>([]);
  const [listCompletedStatus, setListCompletedStatus] = useState(false)

  useEffect(() => {
    handleCompletedStatus()
  }, [items])

  const handleCompletedStatus = () => {
    if(items.length === 0){
      setListCompletedStatus(true)
    }else{
      setListCompletedStatus(false)
    }
  }

  const handleInput = (value: string) => {
    setInputValue(value);
  };

  const handleAddingItem = (e: React.KeyboardEvent) => {
    if (e.key === "Enter") {
      const itemIndex = items.findIndex(item => item.name === inputValue);
      
      if (itemIndex !== -1) {
        // Update quantity if item already exists
        const newItems = [...items];
        newItems[itemIndex].quantity += 1;
        setItems(newItems);
      } else {
        // Add new item if it doesn't exist
        const item = { quantity: 1, name: inputValue, completed: false }
        setItems([...items, item]);
      }

      setInputValue("");
    }
  };

  const handleDeleteItem = (itemName: string) => {
    setItems(items.filter(item => item.name !== itemName));
  };

  const handleCheckItem = (itemName: string) => {
    const newItems = items.map((item) => {
      if (item.name === itemName) {
        return { ...item, completed: !item.completed };
      }
      return item;
    });
    setItems(newItems);
  };

  return (
    <div className="App">
      {listCompletedStatus ? <h1>LIST COMPLETED</h1> : null}
      <h1>Buying List</h1>
      <input
        type="text"
        placeholder="Add an item"
        value={inputValue}
        onChange={(e) => handleInput(e.target.value)}
        onKeyDown={handleAddingItem}
      />
      <ul>
        {items.map((item) => (
          <li>
            {item.name} - Quantity: {item.quantity} - Completed: {String(item.completed)}
            <input type="checkbox" onChange={() => handleCheckItem(item.name)}/>
            <button onClick={() => handleDeleteItem(item.name)}>X</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App
```
