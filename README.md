# Please Stop Misunderstanding Promises
or "How I learned to stop worrying and love the chain"

## Introduction

Every four days we see another article about how complicated and convoluted Promises are and how simple async/await is. If you're lucky, the author knows enough about async/await to understand that you can get stuck in the serialization trap

## Async/Await

Async/await provides the simplicity of synchronous code to asynchronous actions. For simple or individual actions, this can be useful.

### Easy as Sync



### The Serialization Trap

```javascript
const accidentalSerialize = async (arrayOfUrls) => {
  const resources = [];
  for (let url of arrayOfUrls) {
    resources.push(await fetchData(url));
  }
};
```

When you use `await`, you stop the execution of the synchronous code, even if that synchronous code is a loop. This is great if you are working with Selenium or something that needs to behave synchronously, but most of the time that is not the case.

### Try Everything
Async/await uses try/catch blocks to deal with errors. This is consistent with synchronous code, but async logic more frequently needs error handling. Development environments can identify many possible issues with synchronous code, but has limited ability to do so for async calls. Servers can fail. Connections can be spotty. Responses can be slow. 

You may need to retry or warn the user in a variety of scenarios.

```
// Too complicated
const couldFail = async (url) => {
  try {
    return await fetchData(url);
  } catch(e) {
    // what do we do here?
  }
}
 
 const handleFailuresOutside
