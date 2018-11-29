# Truffle

* [Introduction](README.md)

## 一、安装truffle

```shell
cnpm install -g truffle
truffle version
```

## 二、创建项目

```shell
mkdir truffleProject
cd truffleProject
truffle init
```

## 三、添加合约代码

```shell
在contracts文件夹下，创建合约文件，添加代码
```

## 四、编译部署在巧克力合约

```shell
truffle compile
修改truffle-config.js配置文件
truffle migrate --network ganacheNet
truffle migrate
```

## 五、开发模式

```shell
truffle develop
compile
migrate
```

## 六、truffle test

合约和函数必须以Test开头

例

```go
import "truffle/Assert.sol";
import "truffle/DeployedAddresses.sol";
import "../contracts/SimpleStorage.sol";
contract TestSimpleStorage {
    function testSet() public {
        SimpleStorage simpleStorage = SimpleStorage(DeployedAddresses.SimpleStorage());
		 simpleStorage.set(100);
        uint expected = 100;
        Assert.equal(simpleStorage.get(), expected, 'should be 100');
    }
}
```

```shell
truffle test
```

# Truffle_React

##一、集成react

```shell
truffle unbox react
truffle develop
compile
migrate
换一个终端
npm run start

```

## 二、refs

![image-20181128211605417](../../Library/Application Support/typora-user-images/image-20181128211605417.png)

# web3.js

## 二、定义

教程：[官方文档](https://github.com/ethereum/wiki/wiki/JavaScript-API#web3ethaccounts)

web3.js是开发以太坊去中⼼心化应⽤用(DApp)必备的JavaScript库，提供了了⽤用于与geth通讯的
JavaScript API，web3.js使⽤用了了JSON-RPC协议与geth进⾏行行通信。
JSON-RPC是⼀一个⽆无状态，轻量量级的远程调⽤用协议(RPC)，允许使⽤用http，socket等协议进⾏行行
通讯，使⽤用JSON作为数据格式。
Web3.js可以与所有⽀支持JSON-RPC的节点进⾏行行通信，包括以太坊⽣生态中的其他节点，如
Whisper(⼀一个集成以太坊的⾮非实时性消息系统)和Swarm(⼀一个去中⼼心化的存储系统)
Web3.js⽆无法直接连接到以太坊⽹网络， 只能连接到以太坊节点，如:geth

## 三、安装web3

```shell
cnpm install web3 --save
```

### 版本问题

旧版本（0.xx）

1.官方文档：https://github.com/ethereum/wiki/wiki/JavaScript-API#web3ethaccounts

2.特点：支持同步调用，只能通过回调函数调用

新版本

1.官方文档：https://web3js.readthedocs.io/en/1.0/web3-eth-accounts.html#eth-accounts

2.特点：不支持同步调用，支持回调方式，返回值都是promise

## 四、web3包含的模块

![image-20181129094808026](../../Library/Application Support/typora-user-images/image-20181129094808026.png)

## 五、基础API

### 1.BigNumber

#### 安装

```shell
cnpm i --save bignumber.js
```

#### 使用方式

##### 第一种

```javascript
let BigNumber = require('bignumber.js')
let v = new BigNumber('123213213213213213213213213')
```

##### 第二种

```javascript
let Web3 = require('web3')
let web3 = new Web3()
let v = web3.utils.toBN(v)
```

#### 算数运算

```javascript
console.log('====加法====')
m = new BigNumber(10101, 2);
n = new BigNumber("ABCD", 16); console.log(m.plus(n)) console.log(m.plus(n).toString())

console.log('====减法====')
x = new BigNumber(0.5)
y = new BigNumber(0.4) console.log(0.5 - 0.4) console.log(x.minus(y).toString())

console.log('====乘法====')
x = new BigNumber('2222222222222222222222222222222222')
y = new BigNumber('7777777777777777777777777777777777', 16) console.log(x.times(y).toString())

console.log('====除法====') console.log(x.div(y).toString()) console.log(x.div(y).toFixed(6).toString())
console.log('==== x = -123.456====')
x = new BigNumber(-123.456)
console.log(x)
console.log("尾数x.c:",x.c) console.log("指数x.e:",x.e) console.log("符号x.s:",x.s)
```

### 2.utils工具包

#### 单位转换

```javascript
web3.utils.fromWei('12345567890876433', 'ether')
web3.utils.fromWei('12345567890876433', 'Gwei')
web3.utils.fromWei('12345567890876433', 'Mwei')

web3.utils.toWei('1', 'ether')
web3.utils.toWei('1', 'Gwei')
web3.utils.toWei('1', 'Mwei')
```

#### 进制转换

```javascript
web3.utils.toHex('a')
JSON.stringify({name:'Duke'})
```

#### ASCII与十六进制

```javascript
console.log("先将字符串串'xyz'转换为ascii，然后转化为⼗十六进制") var str = web3.utils.fromAscii('xyz')
console.log(str)
console.log("先将⼗十六进制转换为ascii，然后转化为字符串串") str = web3.utils.toAscii('0x78797a') console.log(str)
```

#### hash

```javascript
web3.utils.sha3(hash0)
```

#### 其它

```javascript
web3.utils.toDecimal()
web3.utils.toBigNumber()
web3.utils.isAddress(add1)
```

## 六、web3工作模式

![image-20181129101226738](../../Library/Application Support/typora-user-images/image-20181129101226738.png)

![image-20181129101252417](../../Library/Application Support/typora-user-images/image-20181129101252417.png)

## 七、其它相关函数

### 1.获取账户

#### 第一种（回调函数）

```javascript
web3.eth.getAccounts((err,res)=>{
	accounts = res
})
```

#### 第二种（then）

```javascript
web3.eth.getAccounts().then(accounts=>{
    console.log(accounts)
})
```

#### 第三种（promise）

```javascript
test() = async()=>{
    accounts = await web3.eth.getAccounts()
    console.log(accounts)
}
test()
```

### 2.基础API

| api                               | 含义                 | 备注 |
| --------------------------------- | -------------------- | ---- |
| web3.utils.fromWei(1000, 'ether') | 由1000wei转成ether   |      |
| web3.utils.toWei(1, 'ether')      | 由1ether转成wei      |      |
| bignumber                         | 能够处理理⼤大的数据 |      |
| web3.utils.toHex                  | 转成16进制           |      |
| web3.utils.fromAscii              | 由ascii转成16进制    |      |
| web3.utils.isAddress              | 判断是否为地址       |      |
| web3.utils.sha3                   | sha3哈希函数         |      |
| web3.utils.toDecimal              | 转成10进制           |      |
|                                   |                      |      |

| api                        | 含义               | 备注                              |
| -------------------------- | ------------------ | --------------------------------- |
| web3.eth.getAccounts()     | 获取当前的账户     | `⼀一般只返回当前助记词的主账户 ` |
| web3.eth.getBalance()      | 获取指定地址的余额 |                                   |
| web3.eth.defaultAccount()  | 默认区块           |                                   |
| web3.eth.sendTransaction() | 转账               |                                   |
|                            |                    |                                   |
|                            |                    |                                   |

| api                                                  | 含义                   | 备注 |
| ---------------------------------------------------- | ---------------------- | ---- |
| web3.eth.Contract( JSON.parse(interface)).deploy()   | 部署合约               |      |
| web3.eth.⽅方法.send()                               | 调⽤用函数向合约写数据 |      |
| web3.eth.⽅方法.call()                               | 调⽤用函数向合约读数据 |      |
| Web3.providers.HttpProvider("http://localhost:8545") | 创建provider           |      |
| window.web3.currentProvider                          | 获取当前的provider     |      |
|                                                      |                        |      |



# IPFS

## 一、定义

IPFS是⼀一种点对点的超媒体⽂文件存储、索引、交换协议。

参考链接:http://www.ipfs.cn/news/info-100173.html

### 二、安装IPFS

#### 1.修改host文件

```shell
217.182.195.23 ipfs.io
```

#### 2.二进制安装

[官网下载](https://ipfs.io/)

```shell
tar xvfz go-ipfs.tar.gz
cd go-ipfs
./install.sh
```

#### 3.源码安装

```shell
git clone https://github.com/ipfs/go-ipfs.git
make install
```

### 三、项目配置

#### 1.创建本地项目节点

ipfs init会在home目录下创建一个隐藏文件夹.ipfs

```shell
ipfs init
ls .ipfs/
```

#### 2.修改默认存储空间

打开配置文件

```shell
vi .ipfs/config//第一种

//第二种
export EDITOR=/usr/bin/vim
ipfs config
```

修改

```shell
},
  "Datastore": {
"StorageMax": "20GB", //<<<---------这⾥里里!!!!默认10G此处修改为20G，可 根据需要⾃自⾏行行调整
    "StorageGCWatermark": 90,
    "GCPeriod": "1h",
    "Spec": {
"mounts": [ {
"child": {
     "path": "blocks",
    "shardFunc": "/repo/flatfs/shard/v1/next-to-last/2",
    "sync": true,
    "type": "flatfs"
  },
  "mountpoint": "/blocks",
  "prefix": "flatfs.datastore",
  "type": "measure"
}, {
"child": {
  "compression": "none",
  "path": "datastore",
  "type": "levelds"
},
"mountpoint": "/",
"prefix": "leveldb.datastore",
"type": "measure"
```

### 四、启动服务

```shell
ipfs daemon
```

### 五、基本命令

|            基本命令            |             解释              |
| :----------------------------: | :---------------------------: |
|              add               |           添加文件            |
|              cat               |           查看文件            |
|           get(-c -o)           |           下载文件            |
|               ls               |         查看文件属性          |
|              refs              |        查看被引用哈希         |
|              文件              |                               |
|        ipfs files mkdir        |                               |
|         ipfs files cp          |                               |
|       ipfs files flush[]       |                               |
|        pfs files ls []         |                               |
|         ipfs files mv          |                               |
|        ipfs files read         |                               |
|         ipfs files rm          |                               |
|        ipfs files stat         |                               |
|        ipfs files write        |                               |
|              后台              |                               |
|          ipfs daemon           |           连接公网            |
|     ipfs daemon --offline      |        连接到本地网络         |
|            name解析            |                               |
| ipfs name publish <目录的哈希> | IPNS 注意使用ipns，而不是ipfs |

### 六、设置跨域资源

为了⽅便后续开发，我们需要对ipfs的跨域资源共享(CORS)进行配置，(请执行ctrl+c退出刚刚启动的 daemon服务)，直接在命令行行行如下命令。 

使用ipfs-api的时候会⽤到这里 

``` shell
ipfsconfig--jsonAPI.HTTPHeaders.Access-Control-Allow-Methods '["PUT","GET", "POST", "OPTIONS"]'
ipfsconfig--jsonAPI.HTTPHeaders.Access-Control-Allow-Origin'["*"]'
ipfsconfig--jsonAPI.HTTPHeaders.Access-Control-Allow-Credentials '["true"]'
ipfsconfig--jsonAPI.HTTPHeaders.Access-Control-Allow-Headers '["Authorization"]'
ipfsconfig--jsonAPI.HTTPHeaders.Access-Control-Expose-Headers '["Location"]'
```

###七、IPFS_API

#### 获取ipfs      

```javascript
let ipfsAPI = require('ipfs-api')
const ipfs = ipfsAPI('localhost','5001',{protocol:'http'})
```

### add,cat,ls

```javascript
let test = async()=>{
    let res = await ipfs.files.add(Buffer.from('helloworld'))
    
    res = await ipfs.files.cat(res[0].hash)
    
    let files = await ipfs.files.ls('/box')
}
```

