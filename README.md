# useLocalStorage

This is a library that provides an easy way to manage localStorage, having the possibility to connect changes through different components.

- [Installing](#installing)
- [Import](#import)
- [Use](#use)
  - [Use in multiple components](#use-in-multiple-components)
- [Developer](#developer)
- [Repositories](#repositories)

## Installing

Using npm:

```bash
npm i uselocalstoragenextjs
```

## Import

```javascript
import { useLocalStorage } from "uselocalstoragenextjs";
```

## Use

```javascript
const {
  value, //Value of element in localStorage
  setLocalStorage, //function for modify localStorage
  load, //if the value has been loaded or not
} = useLocalStorage({
  name: "cart", //name of element in localStorage
  defaultValue: [], //defaulValue if element in localStorage if null
  parse: (v: any) => {
    //function for modify value after get of localStorage
    return JSON.parse(v == "" ? "[]" : v);
  },
  updateValue(oldValue, newValue) {
    //function for modify value before set of localStorage
    return [...oldValue, newValue];
  },
});
```

### Use in multiple components

```javascript
import { useLocalStorage } from "uselocalstoragenextjs";
import Component from "./component";

const Home = () => {
  const { value, setLocalStorage, load } = useLocalStorage({
    name: "cart",
    defaultValue: [],
    parse: (v: any) => {
      return JSON.parse(v == "" ? "[]" : v);
    },
    updateValue(olValue, newValue) {
      return [...olValue, newValue];
    },
  });
  return (
    <div>
      Cart
      <div>{JSON.stringify(value)}</div>
      <br />
      <button
        onClick={() => {
          setLocalStorage({ p: 1 });
        }}
      >
        Add New Product
      </button>
      <Component />
    </div>
  );
};

export default Home;
```

```javascript
import { useLocalStorage } from "uselocalstoragenextjs";

export default () => {
  const { value, load } = useLocalStorage({
    name: "cart",
    defaultValue: [],
    parse: (v: any) => {
      return JSON.parse(v == "" ? "[]" : v);
    },
  });
  return (
    <>
      {load && (
        <>
          N Items in Cart
          <br />
          {value.length}
        </>
      )}
    </>
  );
};
```

## Use typescript

```ts
//interface of value
interface notification_interface {
  type?: "ok" | "error" | "warning";
  msg?: string;
}
const {
  value, //Value of element in localStorage
  setLocalStorage, //function for modify localStorage
  load, //if the value has been loaded or not
} = useLocalStorage<notification_interface>({
  name: "notification", //name of element in localStorage
  defaultValue: {}, //defaulValue if element in localStorage if null
  parse: (v: any) => {
    //function for modify value after get of localStorage
    return JSON.parse(v == "" ? "{}" : v);
  },
});
```

## Developer

[Francisco Blanco](https://franciscoblanco.vercel.app/)

[Gitlab franciscoblancojn](https://gitlab.com/franciscoblancojn)

[Email blancofrancisco34@gmail.com](mailto:blancofrancisco34@gmail.com)

## Repositories

- [Gitlab](https://gitlab.com/franciscoblancojn/use-localstorage-nextjs)
