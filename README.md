# 交通标志检测 —— YOLOv8 系列模型实验

> **姓名：王文华 &nbsp;&nbsp; 学号：112304260148 &nbsp;&nbsp; 班级：数据1231**

---

## 实验概述

本项目使用 YOLOv8 系列目标检测模型（v8n / v8s / v8m）完成交通标志检测任务，共经历三轮迭代优化，最终 mAP50 达到 **0.979**。

| 轮次 | 模型 | 输入尺寸 | mAP50 | 提交分数 | 推理方式 |
|:----:|------|:------:|:-----:|:------:|------|
| 1 | YOLOv8n | 640 | 0.955 | 0.897691 | 普通推理 |
| 2 | YOLOv8s | 640 | 0.974 | 0.972114 | TTA |
| 3 | YOLOv8m | 960 | **0.979** | 待提交 | TTA |

完整实验报告见：[第四次实验报告.md](第四次实验报告.md)

---

## Task
Train an object detection model with the provided YOLO dataset and predict objects on the hidden-label test set.

## Classes
Green Light, Red Light, Speed Limit 10, Speed Limit 100, Speed Limit 110, Speed Limit 120, Speed Limit 20, Speed Limit 30, Speed Limit 40, Speed Limit 50, Speed Limit 60, Speed Limit 70, Speed Limit 80, Speed Limit 90, Stop

## Directory
- `train/`: training images and labels
- `val/`: validation images and labels
- `test/images/`: test images only
- `data.yaml`: Ultralytics training config
- `sample_submission.csv`: submission schema
- `baseline_infer.py`: example inference-to-CSV script

## Submission
Submit one `submission.csv` file with these columns:
- `image_id`
- `class_id`
- `x_center`
- `y_center`
- `width`
- `height`
- `confidence`

All coordinates must be YOLO-style normalized values in `[0, 1]`.

## Metric
Ranking metric: `mAP@0.5`

## Example training
```bash
yolo detect train data=data.yaml model=yolov8n.pt epochs=50 imgsz=416
```

## Example submission generation
```bash
python baseline_infer.py --model runs/detect/train/weights/best.pt --test-dir test/images --output submission.csv
```
