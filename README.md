## Difference between async/await and promise

* The first things you have to understand that `async/await` syntax is just syntactic sugar which is meant to `promises`. 
* In fact the return value of an `async` function is a `promise`. 
* `async/await` syntax gives us the possibility of writing asynchronous in a synchronous manner. Here is an example:

#### `Promise` chaining:

```javascript
function logFetch(url) {
  return fetch(url)
    .then(response => response.text())
    .then(text => {
      console.log(text);
    }).catch(err => {
      console.error('fetch failed', err);
    });
}
logFetch('https://api.github.com/users/sureshalagarsamy');
```
![image](https://user-images.githubusercontent.com/6780840/223052801-1706c174-2567-4246-988e-65ad3c465fe0.png)


#### `Async` function:

```javascript
async function logFetch(url) {
  try {
    const response = await fetch(url);
    console.log(await response.text());
  }
  catch (err) {
    console.log('fetch failed', err);
  }
}
logFetch('https://api.github.com/users/sureshalagarsamy')
```
![image](https://user-images.githubusercontent.com/6780840/223052801-1706c174-2567-4246-988e-65ad3c465fe0.png)

In the above example the await waits for the promise `(fetch(url))` to be either resolved or rejected.  If the promise is resolved the value is stored in the response variable, and if the promise is rejected it would throw an error and thus enter the catch block.We can already see that using `async/await` might be more readable than `promise chaining`. This is especially true when the amount of promises which we are using increases. Both `Promise` chaining and `async/await` solve the problem of `callback`. 
