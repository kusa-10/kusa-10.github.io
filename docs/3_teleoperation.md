# テレオペレーション
## 1. テレオペレーション
以下のコマンドを実行します。
```
lerobot-teleoperate \
    --robot.type=so101_follower \
    --robot.port={フォロワーアームのポート} \
    --robot.id={フォロワーアームのID} \
    --teleop.type=so101_leader \
    --teleop.port={リーダーアームのポート} \
    --teleop.id={リーダーアームのID}
```

## 2. カメラ設定
Webカメラでの手順を説明します。（Intel Realsenseの利用も可能です。）
以下のコマンドを実行すると利用可能なカメラの情報が表示されます。
```
lerobot-find-cameras opencv
```

## 3. テレオペレーション（カメラ有）
--robot.camerasに2で得られた情報を反映して実行します。
```
lerobot-teleoperate \
    --robot.type=so101_follower \
    --robot.port={フォロワーアームのポート} \
    --robot.id={フォロワーアームのID} \
    --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 1920, height: 1080, fps: 30}}" \
    --teleop.type=so101_leader \
    --teleop.port={リーダーアームのポート} \
    --teleop.id={リーダーアームのID} \
    --display_data=true
```

## 4. データセット取得
編集中