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
 -  因为aws规定 你在  www.example.com的 host zone里面没办法写 CNAME的记录, 会报错。 比如你写 www.example CNAME example.com， 写不了。因为 A CNAME record is not allowed to coexist with any other data.   CN和ns记录a记录 不能同时存在。
 - a 标签只能写 aws resources或者 ip地址，写不了域名，而且只能写一个。
 
2. 所以只能用 2个bucket的方法进行跳转。
 - bucket name就是 域名，否则你在选resources时候 选不到该bucket
 -  一个bucket叫 www.example.com 一个bucket叫 example.com
 - 然后 www.example.com这个bucket ，你写redirect到 example.com这个bucket
 - 然后 去 www.example.com的hosted zone里面写一条 A 标签，把 www.example.com  A   s3-bucket(www.example.com).
 - 当然 www.exmaple.com 和 example.com要做好 相应的 hosted zone的 delegation.
 
```
----------------------------------------------------
# 4. 如何申请 ssl 证书，在aws acm 中。
```
acm.example.com
```
## Resolved: 
```
1 先创建host zone - acm.example.com
2 再delegation - acm.example.com  &  example.com 假设你有example这个域名
3 最后再申请证书，就能10秒内下。

```
----------------------------------------------------
# 5. 正确的route 53 - hosted zone.

## Resolved: 
```
happyboy.com. --- 本身happyboy.com的4个ns， a.happyboy.com的四个ns地址，b.happyboy.com的四个ns地址， a记录-他自己去a连接的资源, ssl证书的record

a.happyboy.com --- 本身a.happyboy.com的四个ns地址， a记录-他自己去a连接的资源, ssl证书的record

b.happyboy.com --- 本身b.happyboy.com的四个ns地址， a记录-他自己去a连接的资源, ssl证书的record


```
----------------------------------------------------
# 6.  如何开放 s3

## Resolved: 
```
1. Unchecked Public Acess Block

2. Update the policy -去 example里面抄 Granting read-only permission to an anonymous user

```
----------------------------------------------------
# 7.  啥叫ACL????? Access Control List

## Resolved: 
```
Amazon S3 access control lists (ACLs) enable you to manage access to buckets and objects. Each bucket and object has an ACL attached to it as a subresource. It defines which AWS accounts or groups are granted access and the type of access. When a request is received against a resource, Amazon S3 checks the corresponding ACL to verify that the requester has the necessary access permissions.

By default, when another AWS account uploads an object to your S3 bucket, that account (the object writer) owns the object, has access to it, and can grant other users access to it through ACLs. 

A majority of modern use cases in Amazon S3 no longer require the use of ACLs, and we recommend that you disable ACLs except in unusual circumstances where you need to control access for each object individually. With Object Ownership, you can disable ACLs and rely on policies for access control. When you disable ACLs, you can easily maintain a bucket with objects uploaded by different AWS accounts. You, as the bucket owner, own all the objects in the bucket and can manage access to them using policies. 

https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html

简单来说: 1  一个控制 谁 有什么权限 对这个object 做什么事情的一个 list，一般来说 创建他的人有最高权限，可以通过这个list给别人赋予权限, 所以比如说 有别人朝你的aws账户的s3上传了一个object，如果你启用了acl，那你是没有资格控制资格object的。所以推荐disable掉，这样你就获得了所有在你s3里面的object的权限。
         2  现在都不用acl了，因为有其他aws 的policy 比如可以依赖s3 policy可以来进行object权限的配置，所以现在都 推荐 不使用 ACLs 

```
----------------------------------------------------
----------------------------------------------------
# 6.   s3里边 Block public access (bucket settings) 和 Bucket policy 有啥区别，为什么2个都要做才能开放s3.

## Resolved: 
```
 -Block public access 这个 是用来 阻止 外网访问你的 bucket的，是以bucket来说
 
 -The bucket policy, written in JSON, provides access to the objects stored in the bucket. Bucket policies don't apply to objects owned by other accounts 这个是用来 管理里面object有什么权限的，比如可以被读。
```
----------------------------------------------------
# 6.  What is the difference between OAI vs IAM 'users' on AWS?

## Resolved: 
```
A CloudFront Origin Access Identity (OAI) is not an IAM user, nor can it be used as such. An OAI is simply an identity that can be assigned to a CloudFront distribution to be used to identify requests to an S3 origin. The S3 origin bucket can then use the OAI in a bucket policy to allow only request from a CloudFront distribution with that specific OAI.

An OAI cannot be assigned any other roles, policies or permissions and an IAM user cannot be assigned to a CloudFront distribution. The only reason an OAI exists is to allow better security of S3 origins for CloudFront distributions.

Cloudfront -AOI - can allow to get objects from S3 bucket.

```
----------------------------------------------------
# 7. S3 Standard vs S3 Standard-IA vs S3 One Zone-IA vs S3 Glacier

## Resolved: 
```
https://www.concurrencylabs.com/blog/save-money-using-s3-infrequent-access/

1. 一个 region有几个az，为了数据不丢失， 普通s3 会在 同一个region的 不同az下 同时备份，以备不测
2. ia 就是不常访问，访问速度会变慢
3. one-zone就是 省钱 之放一个az里面，如果 One Zone IA does not. As its name implies, data is stored in a single Availability Zone, which means there is no cross-AZ data replication in the event of failure. If the AZ is destroyed, so is your data.
4. s3 glacier 就是 超长时间存储用的 几十年的垃圾数据

```


----------------------------------------------------

# 8.创建ec2

## Resolved: 
```
1.stop就是关机， terminate就是删除，删了就不能restart了

2. 用Linux (ubuntu 20.04)

3. 为什么 ssh后有点延迟。。。你region设在了Virginia了大哥，ec2在美国 当然卡

4.master用来分配工作不需要太多性能，agent需要docker所以内存硬盘都需要比较大，docker image很多1个g

```

----------------------------------------------------

# 9.  key pair

## Resolved: 
```
key pair是跟 region走的， 所以 key pair 命名最好写清楚是哪个region ，

比如 你在Virginia设置的key，在Sydney里面是搜不到的

```

----------------------------------------------------

# 10.  什么是子网掩码 Subnet Mask( prefix)？ 有什么用？

## Resolved: 
```
1. 长什么样？  192.168.0.1/24
          或者 195.168.0.1 /255.255.255.0
2. 为什么要用子网掩码呢？存在的意义是什么？
   这是一个 人为概念，物理层面的话， 13.256.33.8/22 和 13.256.33.8/25 永远是同一个ip
   假设100个人的公司有很多台电脑，他们要相连，如果你不用子网掩码的话，路由器会检索整个大网络的每一个ip然后去找到对应的，这样很费事儿，
   如果划分成了一个一个大小相等的子网，就不需要地毯式搜索了。比如/24把256个地址分成1个等分，/25把256个地址分成2个等分，/26把256个地址分成四个等分。
   如果在同一个子网，直接通信。 如果不在同一个子网，需要交给Gateway去中介通信。所以每个subnet里面 Gateway一定占一个ip位置。
3. 有什么用处呢？用这种技术，具体怎么算的 不需要太多了解
   1. 分配子网掩码，可以帮助确定这个ip地址属于哪个网段，（哪个子网的）
     比如 255.255.255.0这个掩码，也就是/24，分成1个subnet，所以他可以让192.168.0.1 划归到192.168.0.0 到 192.168.0.x （x=256)这个网段
   2.利用子网掩码可以，帮你判断这个分配到的网段里面最多有几台机器，也就是1中 x的值是多少
     比如 255.255.255.0就是255台， 比如 255.255.255.240就是8台 ,比如/26就是 64台，因为四等分了。
   3.判读子网的IP区间，直接计算出来的子网号就是最小IP，把最小IP的二进制最后N位改为1就是最大IP，N=掩码二进制里0的个数。
   如果一台109.153.208.195的IP电脑，在255.255.255.0掩码下，最小IP：109.153.208.0，最大IP就是把二进制最后八个0改为1，109.153.208.255。
   所以该ip在掩码下，这个IP所在的子网 可供选在的 ip区间是 - 就是109.153.208.0～109.153.208.225。也就是 2中的255台电脑。

总结： /24 = 255.255.255.0  1等分 
       /25 2等分
       /26 四等分
       确定ip区间的范围 ， 确定区间内 host数量， 确定指定ip地址在第几个区间内。
 
```
----------------------------------------------------

# 11.   AWS Elastic IP Explained and how to set an  ELP.

## Resolved: 
```
https://www.youtube.com/watch?v=wfyClQKSf9Q

https://www.youtube.com/watch?v=h-yOoHbH_Dw


But overall, try to aviod use ELP

Because, every account only has 5 ELPs.
You can use Route53 -Domain Name to your EC2 with random public IP == work around.
同样的效果 but more scalale.

https://medium.com/innovation-incubator/how-to-automatically-update-ip-addresses-without-using-elastic-ips-on-amazon-route-53-4593e3e61c4c
```

----------------------------------------------------

# 6.   

## Resolved: 
```

----------------------------------------------------

