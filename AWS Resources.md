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
   
  9. Profile -
      
