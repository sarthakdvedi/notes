
events: open, message, error, close
lifecylce: connecting (handshake), open, closing (closing handshake), closed



---


## readystate -
- **`readyState`** is a read-only property that indicates the current state of the WebSocket connection.
- at 1 only, we can use `.send()` command. ( kyoki send tabhi karenge jab open -- tunnel completely jud chuki ho )

| **Value** | **Constant**           | **State**      | **Description**                                                                               |
| --------- | ---------------------- | -------------- | --------------------------------------------------------------------------------------------- |
| **`0`**   | `WebSocket.CONNECTING` | **Connecting** | The connection is not yet open; the initial HTTP upgrade handshake is currently taking place. |
| **`1`**   | `WebSocket.OPEN`       | **Open**       | The handshake is complete and the connection is ready to send and receive data.               |
| **`2`**   | `WebSocket.CLOSING`    | **Closing**    | The connection is undergoing the closing handshake process.                                   |
| **`3`**   | `WebSocket.CLOSED`     | **Closed**     | The connection has been closed or could not be opened.                                        |



---


