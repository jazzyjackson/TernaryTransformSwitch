# Ternary Transform Switch

It goes something like this:
```js
http.createServer((req, res) => (route => {
    req.pipe(new route).pipe(res)
})(
    req.method == 'GET'    ? PathRead   :
    req.method == 'PUT'    ? PathWrite  :
    req.method == 'DELETE' ? PathUnlink :
                             Transflect
))
```



### Purpose

This repository serves to introduce NodeJS transform streams as a standard means of handling web requests.

It includes tests with embedded markup to walk through the available interfaces of NodeJS streams and the runtime behavior of pipelines. This includes order of execution, what events are emitted, and how resources are managed when streams are halted due to errors.

I hope it will be a useful resource for learning streams from scratch in order to write web servers whose behavior is fully comprehensible.

### Description

A server that handles each request through a chain of conditions: once a condition returns true, the corresponding route is selected to transform incoming requests into outgoing responses.

When the transform stream implementing a route's functionality emits an error, it will destroy itself in order to free up resources.

### Introduction
