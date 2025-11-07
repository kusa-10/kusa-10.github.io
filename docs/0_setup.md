# PCセットアップ

## はじめに

標準のPython+venv環境での方法を記載していますがAnacondaなど別の環境を利用されている場合は適宜読み替えてください．
GPUを利用する場合はPyTorchなどのインストールが必要になります．

## 1. Pythonのインストール
まず、Pythonをインストールします。LeRobotはPython 3.8以降を推奨しています。
筆者はPython 3.12.7で動作確認しています．

Pythonのダウンロード:
Python公式サイトにアクセスし、最新の安定版Python 3.xインストーラー（通常は "Windows installer (64-bit)" を選択）をダウンロードします。

インストーラーの実行:
ダウンロードしたインストーラーファイルを実行します。

「Add Python X.Y to PATH」のチェックボックスを必ずオンにしてください。 これにより、PowerShellからPythonを簡単に実行できるようになります。
「Install Now」をクリックしてインストールを開始します。
インストールの確認:
PowerShellで以下のコマンドを実行しインストールされたか確認します。
```
python --version
```
Pythonのバージョンが表示されれば成功です。

## 2. 仮想環境の作成（推奨）

プロジェクトごとに独立したPython環境を作るために、仮想環境を使用することを強く推奨します。これにより、環境間の依存関係の競合を防ぐことができます。

1.  **プロジェクトディレクトリの作成**:
    LeRobot関連のファイルを保存するディレクトリを作成します。例えば、`C:\LeRobot_Project` など。
    

```bash
    mkdir C:\LeRobot_Project
    cd C:\LeRobot_Project
```

2.  **仮想環境の作成**:
    作成したディレクトリ内で以下のコマンドを実行し、`venv` という名前の仮想環境を作成します。
    

```bash
    python -m venv venv
```



3.  **仮想環境のアクティベート**:
    以下のコマンドを実行して仮想環境をアクティベートします。

    

```bash
    .\venv\Scripts\activate
```


    PowerShellの先頭に `(venv)` と表示されれば、仮想環境がアクティベートされています。

## 3. LeRobotのインストール

LeRobotをインストールします。

1.  **LeRobotのインストール**:
    以下のコマンドを**仮想環境がアクティベートされた状態のPowerShell**で実行します。
    

```bash
    pip install lerobot[feetech]
```
