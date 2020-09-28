# signalR-wx
修改后的signalR.js 3.  微信小程序可以直接使用  使用方法与官方一致。
## 示例 示例比较生硬，毕竟使用的话还是要去看官网文档最好。
### 1、创建
```
  const signalr = require("./signalr/index");
  let connection = new signalr.HubConnectionBuilder()
    .withUrl(`${url}hub`, {
        accessTokenFactory: token,
    })
    .withAutomaticReconnect()
    .configureLogging(signalr.LogLevel.Information)
    .build();
```
### 2、开启链接
```
  async function start() {
      try {
          await that.connection.start()
          this.initevent()
      } catch (err) {
          setTimeout(start, 5000);
      }
  }
  start();
```
### 3，都是官方的写法，这里的内容官方文档更加详细
```
  const initevent = () => {
    connection.onclose((res: any) => {
          console.log("signalr 已关闭！");
    });
    this.connection.onreconnected((res: any) => {
        console.log("signalr 重新链接");
    });
    // SendUser("用户id",“消息内容json对象，跟以前一样的”)
    this.connection.on("ReceiveMessage", ( message: any) => {   
         console.log('signalr 收到消息:', message)
    });
  }
  try {
    await connection.invoke("SendMessage", user, message);
  } catch (err) {
    console.error(err);
  }
```
