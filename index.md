# SFTP @Visual Studio Code

## プラグインのインストール

1. Visual Studio Code （以下 VSCode）を開く。
2. Extensions（拡張機能）で SFTP を追加
   - 公式リンクからインストールする場合: [公式リンク](https://marketplace.visualstudio.com/items?itemName=Natizyskunk.sftp)
   - VSCode 内でインストールする場合: Extensions → Search Field → "SFTP" （検索した場合複数 Hit するので、作者"Natizyskunk"のものを選択）

## 設定

1. 予め接続したい PRJ 毎にローカル開発環境ではフォルダ分けしておく  
    **ex.:**  
    `
	local folder  
	├projectA  
	├projectB  
	├projectC  
	├projectD  
	└projectE
	`
1. VSCode で project フォルダを開く
1. VSCode で project フォルダを開いた状態で、コマンドパレットを開く（Shortcut: cmd + shift + p）
1. "SFTP: config"を選択（コマンドパレットを開いた際に SFTP と叩けば予想変換で出てくる）
1. コマンド入力後に開く SFTP.json に、接続したいサーバの情報を入力・設定する。  
    **ex.:**

```
{
  "name": "任意の名前（PRJ名が一番わかりやすいかと）",
  "host": "サーバのホスト",
  "protocol": "ftp",
  "port": 21,
  "username": "いつもの",
  "password": "いつもの",
  "remotePath": "接続した際に自動で繋ぎたいパス。**ex.:** /P00**_***_Test",
  "uploadOnSave": false, // ファイル保存時に自動でuploadするか。false推奨。
  "ignore": [ // ignore設定したいファイル拡張子を設定
    "**/.vscode/**",
    "**/.git/**",
    "**/.DS_Store",
    ".gitignore"
  ]
}
```

1. 再度コマンドパレットを開く（Shortcut: cmd + shift + p）
1. "SFTP: List"を選択
1. 最初に SFTP.json の name で設定した任意の名前が出てくるので Enter
1. 次に表示されるリストが接続したいサーバの内容と一致していれば成功（間違っていれば設定を見直す）

## 使用方法

1. 設定の項と同様、編集を行う PRJ のフォルダを VSCode で開く
1. コマンドパレット →SFTP: List→name→ 任意のファイルまで検索しながら進み、Enter で DL  
   **ex.:**
   ```
   SFTP: List
   ↓
   PRJ:A
   ↓
   Form
   ↓
   common
   ↓
   DefaultPageMaster.aspx
   ↓
   Enter
   ↓↓↓
   DefaultPageMaster.aspx がエディタ上に表示、保存で DL 完了
   ```
1. 編集後、コマンドパレット "SFTP: Upload Active File"を選択で、サーバへファイルを Upload

## 応用/余談

1. 使用方法 3 のアップロード、毎回コマンドパレットを開くのが面倒な場合、VSCode の標準機能のショートカットキー登録を活用すると楽です。
   1. コマンドパレット "Preferences: Open Keyboard Shortcuts" or cmd + K, cmd + S
   1. Search Field で "SFTP"で検索
   1. "SFTP: Upload Active File"の項目で、任意のショートカットを登録（そこそこ大事なコマンドなので、誤操作のないよう普通入力しないような組み合わせがオススメです）
   1. 動作確認 → 完了
1. SFTP を使って接続できるかどうかは、IP アドレスに委ねられてます。IP 制限のかかっている環境ではどうあがいても接続はできないので、管理者に解除してもらうかその他の方法をご検討ください・・・。
