# Chapter6.Webアプリを動かしてみよう

## 参考サイト

- [サル先生のGit入門](https://backlog.com/ja/git-tutorial/)

- [はじめてのGitとGitHub](https://www.udemy.com/course/intro_git/)

## コマンド集

#### サンプルアプリのデプロイ手順
```bash
# Githubからクローン
git clone https://github.com/Azure-Samples/dotnet-sqldb-tutorial.git
cd dotnet-sqldb-tutorial/

# リモートリポジトリ、ユーザー名、Eメールアドレスを登録
git remote add east https://e-paas-app.scm.azurewebsites.net:443/e-paas-app.git
git remote add west https://w-paas-app.scm.azurewebsites.net:443/w-paas-app.git
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list

# リポジトリにPush
git push east master
git push west master
```

#### ナビゲーションバーの表示を修正
```bash
# コードエディタを起動
code .

# 環境変数の値をナビゲーションバーに表示するコード
@Html.ActionLink((string)Environment.GetEnvironmentVariable("WEBSITE_SITE_NAME"), "Index", new { controller = "Todos" }, new { @class = "navbar-brand" })

# 修正内容をWeb Appsに適用
git add .
git commit -m "Update Layout.cshtml"
git push east master
git push west master

```
