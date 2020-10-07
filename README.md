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

參考資料:
此篇文件Workflow 模版講的非常好，如下:https://sanonz.github.io/2020/deploy-a-hexo-blog-from-github-actions/

其他:
  - run: npm install -g yarn       #安裝yarn
  - run: yarn --version            #檢查yarn版本
	- run: npm install --save-dev start-server-and-test   #安裝npm及執行cypress相關動作。



