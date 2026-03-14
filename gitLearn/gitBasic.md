# Git操作

## git 取り扱い



## git コマンド
### git init
git管理したいディレクトリで実行。初回のみ。

### git add {ファイル名}
``git add .``とすると変更ファイル全てステージング。

### git commit -m "コメント"
コミット。

### git status
gitの状態を確認。

### git branch
現在あるブランチの一覧を表示

### git checkout {ブランチ名}
ブランチを切り替え

### git branch {新ブランチ名}
新しいブランチを作成。

### git checkout -b {新ブランチ名}
新しいブランチを作成してそのブランチに切り替える。

### git remote add origin https://github.com/{githubユーザー名}/{リモートリポジトリ名}.git
リモートリポジトリのURLをローカルに登録。初回のみ。

### git push origin {リモートブランチ名}
リモートブランチにローカルの内容を反映。

### git push origin {リモートブランチ名}
リモートブランチにpush。

### git commit --amend -m "変更後コメント"
直前のコミットのコミットメッセージを変更。

### git log (-{表示件数}) --oneline
コミットログを1commit1行で指定件数分表示。

### git rebase -i HEAD~{コミット数}
直前の指定数分のコミット（ローカル）を統合。
エディタが開くので、1番目以外のコミットの行を``pick``から``squash``に変更。
保存して閉じ、次の画面で統合後のコミットメッセージを編集。

### fetch origin
### checkout -b {新ローカルブランチ名} origin/{リモートブランチ名}
リモートブランチを新規ローカルブランチに作成