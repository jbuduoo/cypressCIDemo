# cypressCIDemo
Cypress cicd 測試



```
name: Node.js CI  #測試文件的名稱

on: [push]  #冒號要一定要有一個空白

jobs:
  build:

    runs-on: ubuntu-latest   #使用的系統windows-latest,macos-latest

    strategy:
      matrix:
        node-version: [8.x, 10.x, 12.x]       #測試的node.js的版本，這裡會測試三次。

    steps:
    - uses: actions/checkout@v2                       #actions/checkout@v2 可以实现 Checkout 一个 git 仓库到容器。
    - name: Use Node.js ${{ matrix.node-version }}    #安裝node.js及它的版本,name可以不要，那系統會用uses當它的名字。
      uses: actions/setup-node@v1                     #可以配置容器 Node.js 环境。
      with:
        node-version: ${{ matrix.node-version }}
    - run: npm install                                #安裝npm
    - run: npm run build --if-present
    - run: npm test
      env:
        CI: true
```

參考資料:https://sanonz.github.io/2020/deploy-a-hexo-blog-from-github-actions/
此篇文件Workflow 模版講的非常好，如下:

模版参数说明
name 为此 Action 的名字
on 触发条件，当满足条件时会触发此任务，这里的 on.push.branches.$.master 是指当 master 分支收到 push 后执行任务。
env 为环境变量对象
env.GIT_USER 为 Hexo 编译后使用此 git 用户部署到仓库。
env.GIT_EMAIL 为 Hexo 编译后使用此 git 邮箱部署到仓库。
env.THEME_REPO 为您的 Hexo 所使用的主题的仓库，这里为 sanonz/hexo-theme-concise。
env.THEME_BRANCH 为您的 Hexo 所使用的主题仓库的版本，可以是：branch、tag 或者 SHA。
env.DEPLOY_REPO 为 Hexo 编译后要部署的仓库，例如：sanonz/sanonz.github.io。
env.DEPLOY_BRANCH 为 Hexo 编译后要部署到的分支，例如：master。
jobs 为此 Action 下的任务列表
jobs.{job}.name 任务名称
jobs.{job}.runs-on 任务所需容器，可选值：ubuntu-latest、windows-latest、macos-latest。
jobs.{job}.strategy 策略下可以写 array 格式，此 job 会遍历此数组执行。
jobs.{job}.steps 一个步骤数组，可以把所要干的事分步骤放到这里。
jobs.{job}.steps.$.name 步骤名，编译时会会以 LOG 形式输出。
jobs.{job}.steps.$.uses 所要调用的 Action，可以到 https://github.com/actions 查看更多。
jobs.{job}.steps.$.with 一个对象，调用 Action 传的参数，具体可以查看所使用 Action 的说明。
