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
