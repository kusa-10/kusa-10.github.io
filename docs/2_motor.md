# モーター設定
## はじめに
PCセットアップを行っていない場合は以下の通りセットアップしてください。

[セットアップページ](0_setup.md)

こちらでは手順について抜粋しています。
詳細については各項目からHuggingFaceの説明に飛べるので適宜ご参照ください。

## 1. [USBポート確認](https://huggingface.co/docs/lerobot/so101#step-by-step-assembly-instructions)
USB接続、電源投入後に以下のコマンドを実行してください。

指示に従いケーブルを外し、エンターを押下するとポートのIDが表示されます。

後の過程で使うのでリーダー、フォロワーそれぞれについて行い、記録しておいてください。

``` bash
lerobot-find-port
```
## 2. [モーターID設定](https://huggingface.co/docs/lerobot/so101#2-set-the-motors-ids-and-baudrates)
### フォロワーアーム
USB接続、電源投入されていることを確認し、以下のコマンドを実行します。
```bash
lerobot-setup-motors \
    --robot.type=so101_follower \
    --robot.port={フォロワーアームのポート}
```
グリッパー側から順にモータードライバーに接続するように指示されるので一つずつ接続しEnterキーを押す。

### リーダーアーム
フォロワー同様に、以下のコマンドを実行し、順番に設定します。
```bash
lerobot-setup-motors \
    --teleop.type=so101_leader \
    --teleop.port={リーダーアームのポート}
```

## 3. [キャリブレーション](https://huggingface.co/docs/lerobot/so101#calibrate)
それぞれのアームについて以下のコマンドを実行した後、各関節で可動域全体動くように動かし終わったらEnterキーで終了します。
### フォロワーアーム
```bash
lerobot-calibrate \
    --robot.type=so101_follower \
    --robot.port={フォロワーアームのポート} \
    --robot.id={フォロワーアームのID(任意の名前)}
```
### リーダーアーム
```bash
lerobot-calibrate \
    --teleop.type=so101_leader \
    --teleop.port={リーダーアームのポート} \ 
    --teleop.id={リーダーアームのID(任意の名前)}
```