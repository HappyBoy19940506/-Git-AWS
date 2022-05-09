![jaja](https://img-blog.csdn.net/20180624174835949?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1NodVNoZW5nMDAwNw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

1. main branch -- No code change, only for final merge- devOps go deploying

2. dev-branch - TEST(devops)- CICD(devops)- REVIEW (Senior dev) -Merge back to mastesr (senior dev)

3. SVN - GIT  
  Git: everyone has a full copy of the repo
  SVN: only get one pacth of working-relative part for your work
4. 虽然 develop branch是masterbracnh分化来的，但是 deve不能直接 merge回main，必须先 由deve 分化出 release 或者叫test branch，然后 从test branch merge回main branch
5. 也就是说 三大branch是不变的， main 。 dev 。 test，是不变的， 但是 feature branch开发完后可以删掉。
6. 也就是说，dev branch只负责 feautre的branch开发， main branch负责hotfix， test branch负责bugfix，一旦发生bugfix， test branch要向两头都merge，（dev和main都要更新）
7. 也就是说 test branch是最麻烦的，因为他要 保持 同时向dev和mian的更新。 如何此时 dev 和 test 都发生了commit，那在merge时候就会出现冲突。
8. 如何解决冲突呢，手动解决，如果规避呢，就是比如，你在dev里做了新的branch feature merge ，同时你在 test里又做了 bug fix，那你每次在test里做commit之前，请先 merge一下dev，确保你的test branch是最新的，这样你再commit 你的bug fix一定是 fast-forward merge。 还有一种情况就是，比如 同一时间有2个featurebranch同时开发，一个先交，一个后交，那后交的那个 如果不做 预先的merge 一下dev，肯定会在pull request的时候出现conflict。
