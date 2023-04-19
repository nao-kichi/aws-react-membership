# Amplify URL　/ GitHubソースリポジトリ

#IAMユーザー・Amplifyアプリ名は.envに記述している

#Amplify URL
https://main.d3mclth3yz9sof.amplifyapp.com 

#GitHubソースリポジトリ
https://github.com/nao-kichi/aws-react-membership/tree/main


## 概要
・AWS AmplifyとReactアプリで会員機能サイトを作成
・Register.js / Login.js / Mypage.jsで各々ファイルを作成する。
・SPA構築をして、各ページを閲覧できるようにする。
・データベースは、NoSQLとなっている。メールアドレスとパスワードを格納する。
・オブジェクトストレージはS3を使用して、プロフィール画像などを保存する
・AWS UIサポートは後に検討をする


### 必要なコマンドと手順

#Reactディレクトリを作成する
create-react-app aws-react-member

#先にReactアプリに移動
cd aws-react-member

#GitHubにpush作業をする
#このGitHubのリポジトリを選択してデプロイを行う。

#Amplifyでブラウザでデプロイ作業を行う。

#AWS CLIをインストール
brew update
brew install awscli

#AWS CLIの次に、Amplify CLIをインストール
npm install -g @aws-amplify/cli

#インストール確認
amplify -v

#Reactアプリ内で、Amplifyを使用可能状態にする
amplify init

#Reactアプリ内でAmplify UIを使用可能状態を作成する
npm install aws-amplify @aws-amplify/ui-react

#amplify設定構築(既に完了している場合は、initへ行く)
#事前にIAMユーザーのアクスキーとシークレットキーが必要
#出力内容が異なる時があるので、注意する
amplify configure

#Reactアプリ内で、Amplifyを使用可能状態にする
#事前に、IAMユーザーに権限付与・必要なポリシーを作成
#こちらでどのユーザーか指定している。
amplify init

#認証機能を追加する(Default,Username,No)
amplify add auth

#S3ストレージの設定(事前にバケットを作成とポリシー作成)
→Auth users only(Auth and guest usersかも),create / update, Lambda No
amplify add storage

#DynamoDBの設定(テーブル作成とポリシー作成)
→GraphQL, continue, Single object with fields
amplify add api

#全ての設定が終了したタイミングでpushする
→Yes, Js or Ts , Yes, Enter
amplify push

#React・Amplifyのコード修正を行う。

#再デプロイについて
GitHubに連携されている状態で、既にブラザウでデプロイをしている場合
GitHubにpushするだけでAmplifyに対する再デプロイは完了している。
ただし、GitHubにpushするとAmplifuyのmainページが更新されているので完了するまで待つ。

こちらのコマンドは、GitHubと連携していない場合などに
使用されると思う。こちらのREADME通りに行うと不要だが
心配なため残しておく。
amplify publish
amplify hosting add



#### 注意点と料金発生について

#accesskeyとsecretkeyついて
access keyとsecret keyはセットで作成されている。
access keyとsecret keyの確認方法は新規作成時かDLしかない

#料金発生について
Amplifyの料金は、一定のAuth,S3,Route53などを超えた際に発生する。

#Reactアプリ名・Amplifyアプリ名・GitHubリポジトリ名はほぼ同じものにする
#IAMユーザー名は特に気にする必要はない。
#S3バケットは、Amplifyアプリを作成(init)した時に自動で生成される。