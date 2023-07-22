<h1 align='center'>🥸 팀 분모자 🥸</h1>
<h3 align='center'>:camera_flash: 분류 모자이크 :camera_flash:</h3>

<img align='center' src='https://user-images.githubusercontent.com/42334717/227575043-5c65230c-f283-46b0-a46c-0569ee20cd56.gif'/>

<h3 align='center'> ✨ 기여자 (Contributors) ✨ </h3>

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table align='center'>
  <tr>
    <td align="center"><a href="https://github.com/Zerohertz"><img src="https://avatars.githubusercontent.com/u/42334717" width="100px;" alt=""/><br/><sub><b>BOAZ 19기 분석 오효근</b></sub></a><br/><a href="https://github.com/BOAZ-bigdata" title="BOAZ">🐘</a></td>
    <td align="center"><a href="https://github.com/seedspirit"><img src="https://avatars.githubusercontent.com/u/109015852" width="100px;" alt=""/><br/><sub><b>BOAZ 19기 분석 김보겸</b></sub></a><br/><a href="https://github.com/BOAZ-bigdata" title="BOAZ">🐘</a></td>
    <td align="center"><a href="https://github.com/yejincode"><img src="https://avatars.githubusercontent.com/u/69861207" width="100px;" alt=""/><br/><sub><b>BOAZ 19기 분석 송예진</b></sub></a><br/><a href="https://github.com/BOAZ-bigdata" title="BOAZ">🐘</a></td>
    <td align="center"><a href="https://github.com/woo-ara"><img src="https://avatars.githubusercontent.com/u/69287689" width="100px;" alt=""/><br/><sub><b>BOAZ 19기 분석 우아라</b></sub></a><br /><a href="https://github.com/BOAZ-bigdata" title="BOAZ">🐘</a></td>
    <td align="center"><a href="https://github.com/seohl16"><img src="https://avatars.githubusercontent.com/u/68208055" width="100px;" alt=""/><br/><sub><b>BOAZ 19기 분석 임서현</b></sub></a><br/><a href="https://github.com/BOAZ-bigdata" title="BOAZ">🐘</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

<h3 align='center'>:calendar: <a href="https://github.com/Team-BoonMoSa/.github/blob/main/README.md#calendar-schedule-calendar">Schedule of Team BoonMoSa</a> :calendar:</h3>

<h3 align='center'>:seedling: <a href="https://github.com/Team-BoonMoSa/.github/blob/main/README.md#seedling-process-seedling">Process of Team BoonMoSa</a> :seedling:</h3>

---

# [Model: YOLOv5](https://github.com/Team-BoonMoSa/YOLOv5)

<details>
<summary>
<h2>
<a href="https://github.com/Team-BoonMoSa/MakeData">
Data Setting for YOLOv5
</a>
</h2>
</summary>

```shell
Parent/datasets/MakeData$ python saveData.py
100%|████████████████████████████████████████████████████████████████████████| 2235/2235 [00:45<00:00, 49.47it/s]
==============================
No. Total Data:  2235
==============================
Training Data: No. Images 1861
Training Data: No. GT 1861
Validation Data: No. Images 187
Validation Data: No. GT 187
Test Data: No. Images 187
Test Data: No. GT 187
==============================
No. Total Image Data:  2235
No. Total GT Data:  2235
==============================
```

```shell
Parent/datasets/MakeData$ python labelme2YOLOv5.py
100%|█████████████████████████████████████████████| 5/5 [00:00<00:00,  9.03it/s]
==============================
No. Total Data:  5
==============================
Training Data: No. Images 3
Training Data: No. GT 3
Validation Data: No. Images 2
Validation Data: No. GT 2
==============================
No. Total Image Data:  5
No. Total GT Data:  5
==============================
```

</details>

<details>
<summary>
<h2>
Train, Validation, Test 
</h2>
</summary>

### Train

> FlickrLogos_47

```shell
Parent/YOLOv5$ python segment/train.py --data LogoRec.yaml --epochs ${epoch} --batch-size ${batch_size} --weights yolov5${모델 버전}-seg.pt #--resume
```

> labelme

```shell
Parent/YOLOv5$ python segment/train.py --data labelme.yaml --epochs ${epoch} --batch-size ${batch_size} --weights ${weights}.pt
```

+ `--data`: 데이터의 정보가 저장된 `.yaml` 파일 지정
+ `--epochs`: Training 시 사용될 epoch의 수 지정
+ `--batch-size`: Training 시 사용될 batch size 지정
+ `--weights`: Fine-tuning에 사용될 pre-trained 가중치
+ `--resume`: Training을 이어서 할 수 있는 옵션

### Validation

```shell
Parent/YOLOv5$ python segment/val.py --data LogoRec.yaml --batch-size ${batch_size} --weights ${weights}
```

+ `--data`: 데이터의 정보가 저장된 `.yaml` 파일 지정
+ `--batch-size`: Validation 시 사용될 batch size 지정
+ `--weights`: Validation을 위해 사용할 가중치

### Test

> Detection

```shell
Parent/YOLOv5$ python segment/predict.py --weights runs/train-seg/${훈련된 가중치}/weights/best.pt --source ../datasets/LogoRec/images/test --conf-thres ${threshold} --bms 0
```

> Segmentation

```shell
Parent/YOLOv5$ python segment/predict.py --weights runs/train-seg/${훈련된 가중치}/weights/best.pt --source ../datasets/LogoRec/images/test --conf-thres ${threshold} --bms 1
```

> Mosaic

```shell
Parent/YOLOv5$ python segment/predict.py --weights runs/train-seg/${훈련된 가중치}/weights/best.pt --source ../datasets/LogoRec/images/test --conf-thres ${threshold} --bms 2
```

> :tada: [Demo!](https://github.com/Team-BoonMoSa/YOLOv5/pull/5) :tada:

```shell
Parent/YOLOv5$ python segment/predict.py --weights runs/train-seg/${훈련된 가중치}/weights/best.pt --source 0 --conf-thres ${threshold} --bms 3
```

+ `--weights`: Test를 위해 사용할 가중치
+ `--source`: Test를 위해 사용할 데이터 (`0`으로 지정 시 캠 사용)
+ `--conf-thres`: Confidence threshold
+ `--bms`: BoonMoSa! (For Real-Time Operation)
  + `0`: Detection
  + `1`: Segmentation
  + `2`: Mosaic
  + `3`: Demo (Raw Image -> Detection -> Segmentation -> Mosaic)

</details>

---

# [Model Serving: AWS EC2 Inf1](https://github.com/Team-BoonMoSa/Amazon-EC2-Inf1)

![Amazon_EC2_Inf1](https://github.com/Zerohertz/zerohertz.github.io/assets/42334717/d1cbc5e5-e0a1-4763-adeb-6657568a6a85)

![END](https://github.com/Zerohertz/zerohertz.github.io/assets/42334717/62db6a0b-ce2d-4e4b-92a9-75598d0de5b3)
