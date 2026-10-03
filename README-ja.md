# VRChat Status

VRChatのステータスをNoctaliaのバーに表示し、パネルから変更できるプラグインです。

## プラグイン


| Field | Value |
| --- | --- |
| ID | `surumeika1987/vrchat-status` |
| Entries | Bar widget:`status`;panel:`status-panel` |


## 必要要件

本プラグインを使用するには、`vrchat-status-helper`が必要です。

`vrchat-status-helper`を`PATH`の通った場所に配置するか、プラグイン設定から実行ファイルの場所を指定してください。

## 使用方法

### 1. バックグラウンドデーモンをセットアップする

`vrchat-status-helper`をリポジトリからダウンロードするか、ソースコードからビルドしてください。

[noctalia-vrchat-status-helper](https://github.com/surumeika1987/noctalia-vrchat-status-helper)

`vrchat-status-helper`を`PATH`の通った場所に配置します。

例:

```sh
${HOME}/.local/bin/vrchat-status-helper
```

次に、以下のコマンドを実行してVRChatにログインしてください。

```sh
vrchat-status-helper login
```

ログイン後、`vrchat-status-helper`がバックグラウンドで起動するよう設定します。

Hyprlandなどのデスクトップ環境・コンポジタの起動時に`vrchat-status-helper`を実行するよう設定してください。  
Hyprlandの例
```lua
hl.on("hyprland.start", function()
    hl.exec_cmd("noctalia")
    hl.exec_cmd("/home/<your name>/.local/bin/vrchat-status-helper")
end)
```

### 2. プラグインを有効にする

プラグインマネージャーから本プラグインをインストールしてください。

手動でインストールする場合はリポジトリをダウンロードし、`vrchat-status`フォルダを以下のディレクトリにコピーします。

```text
${HOME}/.local/share/noctalia/plugins/
```

その後、Noctaliaの設定画面から`surumeika1987/vrchat-status`を有効にします。

バーの設定から`VRChat Status`を追加してください。

### パネルを開く

パネルはバーの`VRChat Status`ウィジェットから開くことができます。

IPCから直接開く場合は、以下のコマンドを使用します。

```sh
noctalia msg panel-toggle surumeika1987/vrchat-status:status-panel
```

## 注意事項

本プラグインではVRChat APIを使用します。

VRChat APIの利用によって発生した問題について、本プラグインの開発者は責任を負いません。

`vrchat-status-helper`および本プラグインは自己責任で使用してください。

## 開発者向け

`vrchat-status-helper`から本プラグインへのデータ送信には、NoctaliaのIPC機能を使用しています。

以下のコマンドで、外部プログラムからステータス情報をプラグインへ送信できます。

```sh
noctalia msg plugin surumeika1987/vrchat-status:status all push-status '<payload>'
```

`payload`の形式は以下のとおりです。

```text
<Status Number>:<Status Message>
```

`Status Number`には`0`から`4`までの1桁の数字を指定します。

- `4`: `Join Me`
- `3`: `Online`
- `2`: `Ask Me`
- `1`: `Do Not Disturb`
- `0`: `Offline`

たとえば、ステータスを`Join Me`、ステータスメッセージを`Test Message`にする場合は以下のようになります。

```sh
noctalia msg plugin surumeika1987/vrchat-status:status all push-status '4:Test Message'
```

## ノート
**API**: 非公式の`VRChatAPI`を利用しています。  
**認証**: クッキーを`${HOME}/.cache/noctalia/vrchat-status`に保存しています。  
**プロセス**: 外部ソフトウェア`vrchat-status-helper`が必要です。  
