---
title: 如何建置自己的Hexo Blog
date: 2023-01-16 10:32:01
tags: 
 - hexo
 - hexo next theme
 - github pages
---

# 簡述
因為想要用來放一些公開的筆記，因此找了很多方案，最終決定使用省錢的HEXO搭配`github pages`，並把建置過程記錄下來。
<!--more-->
# 準備
 - [x] nodejs + npm
 - [x] vscode

# 安裝
1. 自行安裝好nodejs及vscode，建議使用LTS版。
2. 到[HEXO官網](https://hexo.io/zh-tw/)查看安裝指令
    
    ```bash
    # 安裝hexo-cli工具
    npm install hexo-cli -g
    # 建立專案
    hexo init blog
    # 進入專案
    cd blog
    # 安裝依賴包
    npm install
    # 啟動伺服器，用來看結果
    hexo server
    ```
# 設定
## 主題
為了簡單搭配全文搜尋，用了[NexT主題](https://theme-next.js.org/)
1. 下載zip放入`路徑\themes\hexo-theme-next-8.14.1`，資料夾可以自行命名但我採用zip原始名稱。
2. 設定主題
   > 修改`檔案\_config.yml`theme節點值改為資料夾名稱
    ```yml
    theme: hexo-theme-next-8.14.1
    ```

## 全文查詢
1. 安裝套件
    ```bash
    npm install hexo-generator-search --save
    ```
2. NexT主題開啟全文查詢
    > `檔案\themes\hexo-theme-next-8.14.1\_config.yml`local_search下enable改為true
    ```yml
    local_search:
        enable: true
    ```
3. 全文查詢快取以json儲存
    > 修改`檔案\_config.yml`
    ```yml
    search:
        path: search.json
        field: post
        content: true
    ```
4. 產生查詢快取json
    ```bash
    # 啟動伺服器，用來看結果
    hexo server

    # 清除舊專案並發布
    hexo clean              # 有安裝新的package或大改動才清理舊專案
    hexo generate           # 產生靜態網頁跟全文查詢快取json
    hexo deploy             # 設定完成就能下此指令發布
    ```

# 三、發佈
## 儲存程式碼
在github上`建立兩個儲存庫`
1. 儲存nmp source code，名稱隨意
2. 儲存hexo發布的靜態文件，名稱<username>.github.io

## 發佈 github pages
> 如果剛好你也是個貧窮開發者，沒錢購買VM，github pages是個好地方
1. 安裝 hexo-deployer-git。
    ```bash
    npm install hexo-deployer-git --save
    ```
2. 修改`檔案\_config.yml`
    ```yml
    deploy:
        type: git
        repo: <repository url>
        branch: [branch]
        message: [message]
    ```
3. 發布url 
  > https://orange9982239.github.io/

# REF
* https://www.youtube.com/watch?v=RcJxnNpj64k&ab_channel=PegasusWang
* https://hexo.io/zh-tw/docs/one-command-deployment.html