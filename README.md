### socket 连接客户端

- socket 继承自 nodejs 的 net 模块，拥有和 new net.Socket() 完全一致的 API。
- 支持 socks5 代理，支持用户名密码
- 支持 http 代理，支持用户名密码（要求 http 代理支持 CONNECT 方法）

### 使用

```javascript
const Socket = require('socket-client-proxy');

const socket = new Socket({
  proxy: {
    host: '127.0.0.1', // 代理 ip
    port: 1080, // 代理端口
    username: '', // 用户名
    password: '', // 密码
    type: 'socks5', // 支持 socks5 和 http
  },
});

await socket.connect({
  host: 'www.google.com',
  port: 443,
});
socket.write('GET / HTTP/1.1\r\n');
// 或者
socket.connect(
  {
    host: 'www.google.com',
    port: 443,
  },
  async () => {
    console.log('Connect success');
    socket.write('GET / HTTP/1.1\r\n');
  }
);
```

### API

- new Socket(options)
  - options.proxy
    - host
    - port
    - username
    - password
    - type: 固定为 socks5 或 http
- 返回：require('net').Socket 实例

### License

MIT
