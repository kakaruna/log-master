# log-master 1.0.0
简单的Log定时切割工具。可切割正在被写入的log文件，并保持完整性。

不支持window平台。

## 安装
`npm install log-master`
## 使用方法
### split

将本机上所有log用时间分割，汇集到一个文件夹里。
```javascript
var logMaster = require('log-master');
logMaster.split({ //切割，目前唯一的功能
  "from": { //源文件夹，可多选。
    "forever": "/root/.forever",
    "app1": "/app1logdir",
    "app2": "/app2logdir"
  },
  "Suffix": [".log"], //要切割的文件类型，可多选。默认 [".log"]
  "to": __dirname, //目标文件夹,log都会到这里。
  "Interval": 1000 * 60 * 60 * 24, //切割时间间隔，默认一天。
  "timeFormat": "yyyy年MM月dd日HH时mm分ss秒", //时间格式(生成的文件夹名),默认为yyyy年MM月dd日HH时mm分ss秒
  "startTime": "00:00" //开始时间，默认零点,精确到秒的话就："00:00:00"
});
```
## 运行
`nohup node youapp.js &`

或用其它守护进程比如：`pm2`, `forever`
## 注意
手动输出Log时需要使用 **>>** 而不是 **>** 符号。例：

### 使用 **>** 将会得到：

`nohup node ./loop.js >/somedir/you.log &`

![image](https://github.com/hezedu/SomethingBoring/blob/master/log-master/log-master-error.png?raw=true)<br>
在vim下看，切割后的文件会包含之前被清空的占位符，并且体积逐渐增大。


###  使用 **>>** 才会得到你想要的结果。

`nohup node ./loop.js >>/somedir/you.log &`

![image](https://github.com/hezedu/SomethingBoring/blob/master/log-master/log-master-ok.png?raw=true)
