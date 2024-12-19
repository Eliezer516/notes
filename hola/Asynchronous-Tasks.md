Happy DOM comes with two functions built in to make it easier to manage asynchronous tasks.

## whenAsyncComplete()

Returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) that is resolved when async tasks has been completed.

```javascript
await window.happyDOM.whenAsyncComplete();
// Do something when asynchrounous tasks are completed
```

## cancelAsync()

This method will cancel all running async tasks.

```javascript
window.setTimeout(() => {
	// This timeout will be canceled
});
window.happyDOM.cancelAsync();
// Asynchrounous tasks has been aborted
```
