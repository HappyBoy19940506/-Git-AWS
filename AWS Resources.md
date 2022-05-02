1. Introduction to AWS Services


https://www.youtube.com/watch?v=Z3SYDTMP3ME



2.  What is Docker ?

如何通俗解释Docker是什么？ - 小枣君的回答 - 知乎
https://www.zhihu.com/question/28300645/answer/560129869

3.What happens when you type a URL in the browser and press enter?
https://medium.com/@maneesha.wijesinghe1/what-happens-when-you-type-an-url-in-the-browser-and-press-enter-bb0aa2449c1a

4. AWS CLI COMMAND

  1.aws iam create-user --user-name Bobbbb
  
  2.aws sts get-caller-identity
  
  3.aws configure   
  
  4.AWS Access Key ID [****************LLG5]: AKIW
  
   -AWS Secret Access Key [****************19ki]: sss
    
   - Default region name [us-east-1]: us-east-1
    
   - Default output format [json]: json
    
  5.aws s3 ls

  6.cat ~/.aws/credentials
  
  7.cat ~/.aws/config
  
  8.
      export AWS_REGION=ap-southeast-2 (or other regions you want to authenticate into) 
export AWS_DEFAULT_REGION=ap-southeast-2 (need to match with the one above)
 export AWS_PROFILE=default (profile name need to match the one in your ~/.aws/config file)
      
   AWS looks for above environment variables in your shell to match your identity. Therefore, you need to do above steps (3 export commands) every time you opens a new terminal tab to authenticate with AWS. 
   To make this easier, you can put these commands in your ~/.bashrc or ~/.zshrc config file.
   
  9. Profile - different users in the same CLI
  A collection of settings is called a profile. By default, the AWS CLI uses the default profile. You can create and use additional named profiles with     varying credentials and settings by specifying the --profile option and assigning a name.

  The following example creates a profile named produser.

  $ aws configure --profile user1
  AWS Access Key ID [None]: 1
  AWS Secret Access Key [None]: 2
  Default region name [None]: us-east-1
  Default output format [None]: text
  You can then specify a --profile profilename and use the credentials and settings stored under that name.

  $ aws s3 ls --profile user1
  
  
  
  
  5.   https://www.youtube.com/watch?v=ZqWb5nNzTf8&t=340s  DNS工作原理 | 什么是DNS 它如何工作\
  6.   https://www.youtube.com/watch?v=m73oA0_ptxc CDN是什么 | CDN的工作机制
  7.   https://www.youtube.com/watch?v=gKI0LL15spU. 买域名 
  8.    https://www.youtube.com/watch?v=mN7aiHucHjg&t=9s  买公网ip的服务器
  9.    https://www.youtube.com/watch?v=YsOsmUUvwBA. 网站上线部署，dns解析，dns delegation，
  10.    https://www.youtube.com/watch?v=Ge-dkZgqLKg.  how to apply a SSL certificate in AWS
  11.    https://zhuanlan.zhihu.com/p/400556541. 什么是CNAME以及CDN？
  12.    https://aws.amazon.com/cn/blogs/china/amazon-cloudfront-article/ 全站加速，Amazon CloudFront 配置不求人
  13.    https://aws.amazon.com/cn/getting-started/hands-on/how-to-apply-ssl-tls-certificate/  SSL/TLS证书申请及使用方法
  14.    https://www.youtube.com/watch?v=l6haqi-aZvc  AWS CloudFront OAI | Use Origin Access Identity | Restrict Access to Your S3 
