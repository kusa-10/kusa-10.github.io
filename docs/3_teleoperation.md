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
```
lerobot-record \
    --robot.type=so101_follower \
    --robot.port={フォロワーアームのポート} \
    --robot.id={フォロワーアームのID} \
    --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 1920, height: 1080, fps: 30}}" \
    --teleop.type=so101_leader \
    --teleop.port={リーダーアームのポート} \
    --teleop.id={リーダーアームのID} \
    --display_data=true \
    --dataset.repo_id={HuggingFaceのユーザ名}/{データセット名} \
    --dataset.num_episodes=5 \
    --dataset.single_task="{タスクの説明}" \
    --private=True
```
## 5. 学習
GPUつきのマシンで以下を実行します。GPUのスペックや手法によりますが数時間程度かかります。
--dataset.repo_idには前の項目で指定したのと同じ値を指定します。
--policy.typeには使用する手法を指定します。(例：act, diffusion)

```
lerobot-train \
  --dataset.repo_id={HuggingFaceのユーザ名}/{データセット名} \
  --policy.type=act \
  --output_dir={ローカルの保存先} \
  --job_name=act_so101_test \
  --policy.device=cuda \
  --wandb.enable=false \
  --policy.repo_id={HuggingFaceのユーザ名}/{ポリシー名}
```

## 6. ロールアウト
出力結果のデータセット名は"eval_"からはじまる必要があります。
```
lerobot-record  \
    --robot.type=so101_follower \
    --robot.port={フォロワーアームのポート} \
    --robot.id={フォロワーアームのID} \
    --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 1920, height: 1080, fps: 30}}" \
    --display_data=false \
    --dataset.repo_id={HuggingFaceのユーザ名}/{出力結果のデータセット名}
    --dataset.single_task="{タスクの説明}" \
    --policy.path={HuggingFaceのユーザ名}/{ポリシー名} \
    --private=True
```
