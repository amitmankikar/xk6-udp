# xk6-udp

A k6 extension for sending strings to UDP port

## Build

To build a `k6` binary with this plugin, first ensure you have the prerequisites:

- [Go toolchain](https://go101.org/article/go-toolchain.html)
- Git

Then:

1. Install `xk6`:

  ```shell
  go install github.com/k6io/xk6/cmd/xk6@latest
  ```

2. Build the binary:

  ```shell
  xk6 build master \
    --with github.com/amitmankikar/xk6-udp
  ```

## Example

```javascript
import tcp from 'k6/x/udp';
import { check } from 'k6';

const conn = udp.connect('host:port');

export default function () {
  udp.writeLn(conn, 'Say Hello');
  let res = String.fromCharCode(...udp.read(conn, 1024))
  check (res, {
    'verify ag tag': (res) => res.includes('Hello')
  });
  udp.close(conn);
}
```
