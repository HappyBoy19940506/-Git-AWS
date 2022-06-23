# 1.  TTL 是什么？怎么设置

## Resolved: 
```
 1. 增大 TTL 值，以节约域名解析时间，给网站访问加速

 2. 减小 TTL 值，增加刷新解析频率，防止更换配置导致的 无法访问
 
https://jaminzhang.github.io/dns/DNS-TTL-Understanding-and-Config/
```
----------------------------------------------------
# 2.  申请到一个 domain name ，如何 绑定上 aws hosted zone？

## Resolved: 
```
1. 如果是 aws上面申请到，成功申请后它会自动 生成一个对应domain的hosted zone，里面的 四个ns 记录就是 domain management里面的该域名对应的四个ns记录。
 -- 如果误删了该hosted zone，那你重新创建一个，然后把 生成的四个新ns记录 ，重新填回 domain management那里。
 -- 注意， hosted zone创建 即会自动分配四个 ns地址，而且 在record table里面更改ns记录 不会改变 这四个ns记录，具体看 Hosted zone details
 
2. 如果是外网申请的，比如godaddy， 那你需要先创建 hosted zone，然后 把四个ns记录，去godaddy中 该域名下填写上。

相当于 你要让 这个你拥有的域名 在 公网上某个name server上有记录。
```
----------------------------------------------------
# 3. aws中如何实现url的跳转

```
比如输入 www.example.com ,用户会被redirect到 example.com

```
## Resolved: 
```
https://docs.aws.amazon.com/AmazonS3/latest/userguide/website-hosting-custom-domain-walkthrough.html
1 . 为什么不能用 cname 的方法跳转 ？
 -  因为aws规定 你在  www.example.com的 host zone里面没办法写 CNAME的记录, 会报错。 比如你写 www.example CNAME example.com， 写不了。 
 - a 标签只能写 aws resources或者 ip地址，写不了域名，而且只能写一个。
 
2. 所以只能用 2个bucket的方法进行跳转。
 - bucket name就是 域名，否则你在选resources时候 选不到该bucket
 -  一个bucket叫 www.example.com 一个bucket叫 example.com
 - 然后 www.example.com这个bucket ，你写redirect到 example.com这个bucket
 - 然后 去 www.example.com的hosted zone里面写一条 A 标签，把 www.example.com  A   s3-bucket(www.example.com).
 - 当然 www.exmaple.com 和 example.com要做好 相应的 hosted zone的 delegation.
 
```
----------------------------------------------------
# 3. 

```
Grs/jso
```
## Resolved: 
```
```
----------------------------------------------------
# 3. 

```
Grs/jso
```
## Resolved: 
```
```
----------------------------------------------------
