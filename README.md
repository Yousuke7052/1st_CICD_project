# 1st_CICD_project
Practice CICD project by myself

設計了一個適用於無經驗，並從0開始搭建的CICD單人小型實踐項目，並考慮了低花費，同時也盡量避免再上傳GitHub時需要敏感信息
的操作，對於不會前後端語言的人也盡可能友好，提供每一個階段每一個動作要輸入的指令或配置文件代碼等

項目目標：在部署完成後可以在github上倉庫的action中看到代碼上傳後被自動執行了ci.yml文件中規劃的工作

1.本地倉庫
1-1.建立git文件夾
    mkdir git
    cd git
1-2.配置git:
    git config --global user.name "Your Name"
    git config --global user.email you@example.com
1-3.初始化(在項目資料夾)
    cd 1st_CICD_project
    git init
    ls -a   # 確認.git存在
    ls -al ~/.ssh   # 確認是否有SSH密鑰
1-4.生成金鑰
    ssh-keygen -t ed25519 -C "you@example.com"
1-5.查看金鑰
    cat /root/.ssh/id_ed25519.pub
    複製顯示的訊息到遠程倉庫創建SSH金鑰
1-6.確保SSH連接
    ssh -T git@github.com   # 正常會在最後回覆Hi之類的訊息
1-7.依據想在哪個資料夾部署，本例子中就部署在git文件夾；GitHub自己建好的倉庫中 有SSH連結(若是由本地倉庫建立再連結到遠程建立遠程倉庫，將跳過此步驟，本案例就是)
    git clone "SSH連結"(clone方式是在git資料夾尚未init)
1-8.創建一個新的分支並確認
    git checkout -b new-feature
    git branch
1-9.創建一個py文件，內容參閱附件
    git add .
    git commit -m "Add initial version of hello script"
    git checkout main
    git merge new-feature    # 合併分支
    git push origin main
|---這時候可以去遠程倉庫看看
|ps:檔案已經推送至遠程倉庫完成同步
|---另外python中要執行的函數名需對應到ci.yml中

2.CI/CD
2-1.創建一個新的分支並確認
    git checkout -b new-feature2
    git branch
2-2.創建.github/workflows
    mkdir .github/workflows
    vim ci.yml    # 內容參考附件
|---1.注意執行剛剛創建的python的函數名要對應到ci.yml文件中要執行的python，不然執行不了
|---2.python版本注意，範例中用了3.8
2-3.創建一個requirements.txt
    mkdir requirements.txt
|---跟執行CICD時，python裡面的需求有關，依需求增加
2-4.常規流程
    git add .
    git commit -m "Add CICD and requirements.txt"
    git checkout main
    git merge new-feature2
    git push origin main


