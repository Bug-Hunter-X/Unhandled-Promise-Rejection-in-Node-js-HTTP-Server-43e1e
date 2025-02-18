# Unhandled Promise Rejection in Node.js HTTP Server

This repository demonstrates a common error in Node.js where an unhandled promise rejection within an HTTP server's request handler can lead to unexpected behavior.  The server may appear to be running without throwing any errors, but it may fail to respond properly to requests.

## Bug Description
The bug lies in the asynchronous nature of the request handling. If an error is thrown within a `Promise` in the request handler, and that error is not caught, Node.js will emit an 'unhandledRejection' event, but the response to the client will likely be incomplete or missing, resulting in a broken connection or an error for the client.

## Bug Solution
The solution involves properly handling potential errors within the `Promise` chain using a `.catch()` block.  The `.catch()` block should handle the error gracefully, ensuring that the client receives a proper response (even if it's an error response).