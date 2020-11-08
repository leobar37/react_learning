## Hooks

### ¿what is hooks?

con hooks puedes extraer la lógica del estado
de un componente de tal forma que esta pueda ser
probado y re-usado independientemente. 
Los hooks te permiten reutilizar 
lógica de estado sin cambiar la jerarquía 
de tu componenente

# what is custom hooks

a custom hook allows you to extract some components
logic into a reusable component  logic into a reusable
function a custom hook is a javascript that starts with use
and that call can other hoooks

Remember that components and hooks are functions
, so we are really not create new concept here

## useState

permite manipular el estado de la variables

## useEffect 

te permite llevar acabo efectos 
secundarios en componentes funcionales 

> Hay dos tipos de de efectos secundarios en los componentes
de react :  aquellos que no necesitan una operacione de saneamiento 
y los que si los necesitan

> cuando usamos este hook le estamos 
diciendo a react  que el componente tiene 
que hacer algo despues de renderizarse 

> se ejecuta cuando se carga el componente 
y cuando se actualiza

**Efectos sin saneamiento:**

Decidimos esto por que podemos ejecutarlo y olvidarnos
de ellos inmediatamente 

**Efectos con saneamiento:**

si en el `useEffect` devuelve una
función react la ejecutara despues de realizar el saneamiento

*¿Cuándo sanea React el efecto exactamente?*
sanea el efecto cuando el componente se desmonta
. Sin embargo como hemos aprendido anteriormente, los efectos 
no se ejecutan 
*Omite efectos para optimizar el rendimiento:*

Este requerimiento: es tan común que esta incorporado en la API
del hook de useEffect. Le indicas a react 
que omita aplicar un efecto si ciertos valores no han cambiado
```js
  useEffect(()=>{
       
  } , [count]) // solo se ejecuta si count cambiar
```

## https://es.reactjs.org/docs/hooks-custom.html


## useCallback

**memoization:**
in computing or memoization 
is an optimization technique used 
primarily to speed up computer

**Definition:**
pasa un calback 
en línea y un arreglo de dependencias 
`useCallback`  devolvera una version memorizada 
de callback que solo cambia si una de las
dependencias ha cambiado, Esto es util
cuando se tranfiere callbacks 
a comoponentes hijos 

## useCallback vs useMemo

`useCallbak` gives you referential equality 
between reder functions. `useMemo` gives 
you referential equality between render for values 

`useCallback` and `useMemo` both expect a functions and array 
of dependences the difference is that `useCallback`
retun its function when the dependences change while
`useMemo` calls its function and returns the result

Since JavaScript has first-class functions, useCallback(fn, deps) is equivalent to useMemo(() => fn, deps).

## referential equality

```js
const greeting = 'hello';
const otherGreeting = 'hello';

function foo() {
  return 'bar';
}
const otherFoo = function() {
  return `bar`;
};
const anotherFoo = () => 'bar';
function sameFoo() {
  return 'bar';
}
const fooReference = foo;

'hello' === 'hello'; // true
greeting === otherGreeting; // true

foo === foo; // true
foo === otherFoo; // false
foo === anotherFoo; // false
 /*
    return false , this because for : 
     -  and functions are objects in javascript
     -  two distinct objects are never equal for either strict 
       o abstract comparisions
 */
foo === sameFoo; // false
foo === fooReference; // true
```
## Api

**useCallback** 
--- 
returns its function uncalled so you can 
it later 

**useMemo:**
--- 
calls its function and returns the results :)

## casos de uso 

**Esto es ineficaz:**

```js

import React, { useEffect, useState } from 'react';
import ListItem from '@material-ui/core/ListItem';
import ListItemText from '@material-ui/core/ListItemText';

function User({ userId }) {
  const [user, setUser] = useState({ name: '', email: '' });

  const fetchUser = async () => {
    const res = await fetch(
      `https://jsonplaceholder.typicode.com/users/${userId}`
    );
    const newUser = await res.json();
    setUser(newUser);
  };
//
  useEffect(() => {
    fetchUser();
  }, []);
  return (
    <ListItem dense divider>
      <ListItemText primary={user.name} secondary={user.email} />
    </ListItem>
  );
}

export default User;
```

**se solucionaria asi:**

```js
useEffect(() => {
  const fetchUser = async () => {
    const res = await fetch(
      `https://jsonplaceholder.typicode.com/users/${userId}`
    );
    const newUser = await res.json();
    setUser(newUser); // Triggers re-render, but ...
  };

  fetchUser();
}, [userId])

```

## como estamos usando useCallback  y useMemo 

```js
const fetchUser = useCallback(async () => {
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/users/${userId}`
  );
  const newUser = await res.json();
  setUser(newUser);
}, [userId]);

useEffect(() => {
  fetchUser();
}, [fetchUser]);
```

## cuando utilizo useEffect

supongamos que filtra los usuarios y los muestra en una lista 


```js
// Some FP magic 🧙🏼‍♂️
const filter = (f, arr) => arr.filter(f);
const prop = key => obj => obj[key];
const getName = prop('name');
const strIncludes = query => str => str.includes(query);
const toLower = str => str.toLowerCase();
const pipe = (...fns) => x => fns.reduce((y, f) => f(y), x);
const nameIncludes = query =>
  pipe(
    getName,
    toLower,
    strIncludes(toLower(query))
  );

function UserList({ query, users }) {
  // 🔴 Recalculated on every render
  const filteredUsers = filter(nameIncludes(query), users);
  // ...
}
```
esto se recalculara en cada render y pues no se quiere eso 
como solución se agregaria useMemo y coomo dependercia los
argumentos entonces solo retorna un resultado cundo 
ha habido un cambio en estas variables

```js
function UserList({ query, users }) {
  // ✅ Recalculated when query or users change
  const filteredUsers = useMemo(
    () => filter(nameIncludes(query), users),
    [query, users]
  );
  // ...
}

```
 