## 微信小程序加签验签(wxapp_rsa,jsencrypt)和egg搭建的后端交互(jsrsasign,node_rsa)最全!!!

## RAS加密

​	RSA加密算法是一种非对称加密算法。

​	假设 A 与 B 通信。A 和 B 都提供一个公开的公钥。A 把需要传递的信息，先用自己的私钥签名，再用 B 的公钥加密。B 接收到这串密文后，用自己的私钥解密，用 A 提供的公钥验签。

​	为什么要先签名后加密？如果你先加密后签名，非法用户通过获取的公钥就可以破解签名，破解之后就可以替换签名。

## 数字签名

​	功能：保证信息传输的完整性、发送者的身份认证、防止交易中的抵赖发生。

​	作用：数字签名的文件的完整性是很容易验证的（不需要骑缝章，骑缝签名，也不需要笔迹专家），而且数字签名具有不可抵赖性（不可否认性）。

​	数字签名技术是将摘要信息用发送者的私钥加密，与原文一起传送给接收者。接收者只有用发送者的公钥才能解密被加密的摘要信息，然后用HASH函数对收到的原文产生一个摘要信息，与解密的摘要信息对比。

​	如果相同，则说明收到的信息是完整的，在传输过程中没有被修改，否则说明信息被修改过，因此数字签名能够验证信息的完整性。

​	发送报文时，发送方用一个哈希函数从报文文本中生成报文摘要,然后用自己的私人密钥对这个摘要进行加密，这个加密后的摘要将作为报文的数字签名和报文一起发送给接收方，接收方首先用与发送方一样的哈希函数从接收到的原始报文中计算出报文摘要。

​	接着再用发送方的公用密钥来对报文附加的数字签名进行解密，如果这两个摘要相同、那么接收方就能确认该数字签名是发送方的。

## 小程序端

### jsEncrypt.js介绍

#### 功能

一种RSA加密的解决方案。 这种加密模式被称为"非对称加密算法"。

（1）乙方生成两把密钥（公钥和私钥）。公钥是公开的，任何人都可以获得，私钥则是保密的。

（2）甲方获取乙方的公钥，然后用它对信息加密。

（3）乙方得到加密后的信息，用私钥解密。

如果公钥加密的信息只有私钥解得开，那么只要私钥不泄漏，通信就是安全的。

**[jsencrypt源码](https://github.com/travist/jsencrypt/blob/master/bin/jsencrypt.js)不支持小程序端需要做一定的兼容处理,可查看: [jsencrypt小程序兼容处理](https://developers.weixin.qq.com/community/develop/doc/000068b497cfc00619b7bcfdc51004)或直接在此处[下载已兼容和压缩后的jsencrypt](https://images-1300732204.cos.ap-chengdu.myqcloud.com/jsencrypt.min.js),将js文件加入到小程序根目录的`/utils`文件夹下**

#### 第一步: 客户端获取公钥和私钥

```js
// app根目录/util/create_rsa.js
const Encrypt = require('./jsencrypt.min.js')
//生成公钥和私钥
export function generateKeys() {
  var crypt = new Encrypt({
    default_key_size: 2048 //设置秘钥的长度需要和服务器端保持一致
  });
  crypt.getKey();
  var publicKey = crypt.getPublicKey();
  var privateKey = crypt.getPrivateKey();
  // 去除-----*** RSA **** KEY----- 和空格换行
  // publicKey = (publicKey.split('-----'))[2];
  // publicKey = publicKey.replace(/\n/g, "").replace(/\r/g, "").replace(/\t/g, "").replace(/\s*/g, "");
  // privateKey = (privateKey.split('-----'))[2];
  // privateKey = privateKey.replace(/\n/g, "").replace(/\r/g, "").replace(/\t/g, "").replace(/\s*/g, "");

  // 返回生成的秘钥对
  return [publicKey, privateKey];
}
export const [publicKey, privateKey] = generateKeys();
```

### wxapp_rsa加签和验签

#### 第二步: 待传输数据的加签和验签

​	这里使用这个库: **[wxapp_rsa](https://github.com/zhangzhaopds/WeixinApp_RSA_Signature)** (相关代码可以直接参考github)

​	这里下载签名需要的js文件[wxapp.rsa.js](https://github.com/zhangzhaopds/WeixinApp_RSA_Signature/blob/master/utils/wxapp_rsa.js)

```js
// app根目录下/utils/rsa.js
const {publicKey, privateKey} = require('./create_rsa.js')
const RSA = require('./wxapp_rsa.js')

// 使用客户端私钥加签
export function sign(data) {
  var sign_rsa = new RSA.RSAKey();
  sign_rsa = RSA.KEYUTIL.getKey(privateKey);
  var hSig = sign_rsa.signString(data, 'sha256'); //支持sha1 , sha256等
  return RSA.hex2b64(hSig); // hex 转 b64
}
// 使用服务器端私钥验签
export function verify(){
 var verify_rsa = new RSA.RSAKey();
verify_rsa = RSA.KEYUTIL.getKey(publicKey);
console.log('验签RSA:')
console.log(verify_rsa)
hSig = RSA.b64tohex(hSig) var ver = verify_rsa.verifyString("signData", hSig) console.log('验签结果：' + ver)   
}
```

#### 第三步待传输数据的加密

​	首先无论是jsEncrypt或者是wxapp_rsa对数据进行加密都会有长度限制,117Bytes,超过此长度便会报错因此我们需要将加密的数据进行分段处理,可以参见: [RSA加密超长数据](https://blog.csdn.net/mobile18611667978/article/details/104436559);

​	我已将代码合并到了[jsencrypt.min.js](https://images-1300732204.cos.ap-chengdu.myqcloud.com/jsencrypt.min.js)中,可以直接下载

```js
// app根目录下/utils/rsa.js
//直接encrypt只能支持117，为JSEncrypt添加方法encryptLong2可以支持任意长度
export function encrypt(data) {
  let encrypt = new JSEncrypt();
  encrypt.setPublicKey(publicKey);
  return encrypt.encryptLong2(data);
}

export function decrypt(data) {
  let decrypt = new JSEncrypt();
  decrypt.setPrivateKey(privateKey);
  return decrypt.decryptLong2(res2)
}

```

## egg搭建的服务器

### rsa刷新

​	为保证rsa秘钥和安全和不可破解我在egg中开启了rsa定时刷新的定时任务,任务如下

​	`app/schedule` 目录下创建一个 `update_rsa.js` 文件

```js
const Subscription = require('egg').Subscription;
const NodeRSA = require('node-rsa')
class UpdateRsa extends Subscription {
    // 通过 schedule 属性来设置定时任务的执行间隔等配置
    static get schedule() {
        return {
            interval: '1d', // 1 天钟间隔 h:小时 m:分钟 s:秒可以使用cron
            type: 'all', // 指定所有的 worker 都需要执行
            immediate: true, //立即执行定时任务
            disable: false
        };
    }
    // subscribe 是真正定时任务执行时被运行的函数
    async subscribe(ctx) {
        var key = new NodeRSA({ b: 2048 })
        key.setOptions({ encryptionScheme: 'pkcs1' })
        const privatePem = key.exportKey('pkcs1-private-pem'),
            publicPem = key.exportKey('pkcs1-public-pem');
        console.log('====================================');
        console.log('RSA秘钥已更新');
        console.log('====================================');
        this.ctx.app.rsa  = { privatePem, publicPem };//将私钥和公钥放到了全局变量rsa中,此后可以通过app.rsa获取
    }
}

module.exports = UpdateRsa;
```

**起初尝试过在小程序端构建npm的node-rsa,经过尝试,构建出的代码包远远大于2m,已经超过了小程序规定的大小**

### egg的加签验签

#### jsrsasign

##### 第五步： 服务器端加签和验签

​	加签: 创建秘钥实例 -> 构建Signature实例 -> 传入秘钥实例, 初始化 -> 签名

`npm i -s node-rsa jsrsasign`

```js
const { KJUR, hextob64, b64tohex } = require('jsrsasign')
/**
     * 数字签名
     * @param {string|object} data 签名数据
     * @param {object} op 签名设置
     * @returns string base64
     */
    signature(data, op) {
        const { app } = this, { privatePem } = app.rsa ? app.rsa : defaultPrivatePem
        signature = new KJUR.crypto.Signature({
            alg: "SHA256withRSA",
            prvkeypem: privatePem,
            ...op
        });
        signature.updateString(data);
        const res = signature.sign();
        return hextob64(res)
    },
    /**
     * 签名验证
     * @param {string|object} data 待验证数据 
     * @param {object} op 指定验证设置
     * @returns 
     */
    verify(data, op) {
        const { app } = this, { publicPem } = app.rsa ? app.rsa : defaultPublicPem
        let signatureVf = new KJUR.crypto.Signature({
            alg: "SHA256withRSA",
            prvkeypem: publicPem,
            ...op
        });
        //接受的参数是16进制字符串!
        return signatureVf.verify(b64tohex(data));
    },
```

![支持的算法](https://images-1300732204.cos.ap-chengdu.myqcloud.com/20201203092527358.png)

#### node-rsa

##### 第六步：传输数据的解密

```js
const NodeRSA = require('node-rsa)
/**
     * rsa加密
     * @param {string} publicPem 客户端公钥
     * @param {string|object} data 待加密数据
     * @param {string} encode 编码方式
     * @returns string rsa
     */
encrypt(publicPem, data, encode) {
        const { app } = this; let publicKey;
        try {
            publicKey = new NodeRSA(publicPem)
        } catch (e) { return { err: e, data: data } }
        //使用客户端的公钥加密
        return publicKey.encrypt(data, encode || 'base64');
    },
    /**
     * rsa解密
     * @param {*} data 待解密的数据
     * @param {string} encode 编码
     * @returns data
     */
    decrypt(data, encode) {
        const { app } = this, privatePem = app.rsa ? app.rsa.privatePem : defaultPrivatePem
        let privateKey;
        try {
            privateKey = new NodeRSA(privatePem)
        } catch (e) { return { err: e, data: data } }
        return privateKey.decrypt(data, encode || 'utf8');
    },
```

​	**本以为这样就能完成服务器和客户端间的通信了,但但但是!!!万万万没有想到JSEncrypt和node-rsa加密解密的方式不一样,就连同样数据加密出来的字符串长度都不一样,看了源码我才知道,没有办法小程序不能使用node-rsa只好在服务器端使用jsencrypt加解密了,加密和解密方式和小程序端一样直接引入即可,代码都可以直接copy**

​	**有木有什么办法可以使用第三方库并且兼容小程序?这就是下的wxmp-rsa**

## wxmp-rsa兼容小程序可支持长文本加密

​	**首先,小程序是不能直接使用npm的,需要先构建**方法是:

	1. 在小程序的根目录下,打开命令行,输入`npm init -y` *要是根目录哈,不然不好引入js,虽然网上都说可以在任意的地方或子目录下安装第三方库,但是我发现引入的时候开发者工具会找不到第三方库,当然也可能是版本的原因,你如果没有这个问题可以跳过*
	2. 接着输入`npm i -S wxmp-rsa`
	3. 打开开发者工具右上角选择`工具->构建npm`

```js
//如果需要引入第三方库下的组件需要修改.json文件添加useComponents字段,请自行百度
//其他的照常引入就行
// utlts/rsa.js
const WxmpRsa = require('wxmp-rsa);
```

​	*构建方法也可以自行百度,网上教程很多*

​	这里放上wxmp-rsa的npm库 [wxmp-rsa](https://www.npmjs.com/package/wxmp-rsa)

​	另外我找到一个比较不错的小程序加密库也是官方的demo[github地址](https://github.com/wechat-miniprogram/sm-crypto)

**接下来小程序加签,验签,加密解密和服务器就都一样了**

```js
//因为wxmp-rsa使用的jsencrypt所以代码什么的都和jsencrypt一样啦
let res1= new WxmpRsa.JSEncrypt();
res1.setPublicKey(clientPublicKey);
let res2=res1.encryptLong2(data);//encryptLong2是我自己加上去的方法
console.log(res2);
let res3 = new WxmpRsa.JSEncrypt();
res3.setPrivateKey(clientPrivateKey);
let res4 =res3.decryptLong2(res2); //decryptLong2是我加上去的方法
console.log(res4);
```

​	**但是哈,wxmp-rsa加密出来的字符串蛮大的,一个原始长度490的字符串加密后长达2392,而jsencrypt加密后才1708,node-rsa才1024,呜呜呜我想用node-rsa,奈何构建出的js文件太大,于是我将jsencrypt里面的加密方法放到了wxmp-rsa中**

 **但是egg不支持import语法所以还是不能使用这个库**

