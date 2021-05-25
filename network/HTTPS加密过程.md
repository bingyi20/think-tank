# HTTPS加密原理

## 加密原理
1. **client** 发送client-random随机密钥串与可用加密套件给 **serivce**
2. **service**发送service-random随机密钥串与加密套件以及自己的公钥给 **client**
3. **client**本地生成新的密钥 pre-master，然后用**service**返回的公钥信息对pre-master进行非对称加密之后将加密后的密钥发送给**service**, 由于是使用服务端给的公钥进行加密生成的，所以也只有服务端能对齐进行解密，其它第三方进行拦截了也解不开。
4. **service**用自己的私钥将其解开拿到pre-master。
5. 接下来**client**与**service**通过client-random + service-random + pre-master 生成密钥 master-secret，然后将master-secret作为密钥，采用对称加密对数据进行加密传输。


## 具体应用场景
1. 服务器并没有直接返回公钥给客户端，而是返回CA证书，公钥信息就在证书里面。
2. 客户端拿到证书之后，要先验证证书的有效性，然后再进行后续操作。