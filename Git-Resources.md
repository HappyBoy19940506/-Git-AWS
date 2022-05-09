![jaja](https://img-blog.csdn.net/20180624174835949?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1NodVNoZW5nMDAwNw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

1. main branch -- No code change, only for final merge- devOps go deploying

2. dev-branch - TEST(devops)- CICD(devops)- REVIEW (Senior dev) -Merge back to mastesr (senior dev)

3. SVN - GIT  
  Git: everyone has a full copy of the repo
  SVN: only get one pacth of working-relative part for your work
4. 虽然 develop branch是masterbracnh分化来的，但是 deve不能merge回main，必须先 deve 分化出 release 或者叫test，然后 从test merge回main branch
