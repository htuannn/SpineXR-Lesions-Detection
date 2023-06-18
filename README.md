# SpineXR-Lesions-Detection

## Chuẩn bị dữ liệu

**Bước 1**: Tải bộ dữ liệu VinDr-SpineXR từ link: https://physionet.org/content/vindr-spinexr/1.0.0/. Bộ dữ liệu sau khi tải xuống sẽ có cấu trúc như bên dưới:

```
"project-home"/data
├── annotation
│   ├── train.json
|   └── test.json
├── train_images
│   ├── 00073745e02e69432c002b527c565151.dicom
│   ├── ...
|   └── fffa8adcc5e692cdb816051b6202870d.dicom
└── test_images
    ├── 004004095d8a302b1c0815ccb044c018.dicom
    ├── ...
    └── ff6a81f9fa386401ce11a0eb74e1f661.dicom
```

**Bước 2**: Chuyển định dạng file DICOM sang PNG bằng cách run bash script:

    bash convert_dicom.sh

Cấu trúc của data folder sau khi chạy lệnh:

```
"project-home"/data
├── annotation
├── train_images
├── test_images
├── train_pngs
│   ├── 00073745e02e69432c002b527c565151.png
│   ├── ...
|   └── fffa8adcc5e692cdb816051b6202870d.png
└── test_pngs
    ├── 004004095d8a302b1c0815ccb044c018.png
    ├── ...
    └── ff6a81f9fa386401ce11a0eb74e1f661.png
```

**Bước 3**: Chuyển annotation thành định dạng YOLO format.

**Bước 4**: Chuyển dữ liệu từ PNG sang JPG (làm nhẹ bộ dữ liệu để dễ dàng huấn luyện)

_Nhóm đã xử lý dữ liệu và up lên drive file (data.zip)_

## Phương pháp
Trong dự án này, nhóm sử dụng 3 phương pháp (YOLOv5, YOLOv8, YOLO_NAS) là các phiên bản khác nhau của YOLO (You Only Look Once). 3 folder (YOLOv5, YOLOv8, YOLO_NAS) là source code tương ứng với 3 thuật toán đã trình bày.

### YOLOv5
Folder YOLOv5 chứa source code do nhóm reimplement lại thuật toán YOLOv5. Công việc huấn luyện, kiểm thử và dự đoán đều được thực hiện trực tiếp bằng file notebook SpineXR_YOLOv5.ipynb.
### YOLOv8
Folder YOLOv8 có cấu trúc như sau:

```
./YOLOv8
├── data.yaml
├── SpineXR_YOLOv8.ipynb
├── yolov8-65.3.pt
└── inference_results
    ├── 0a02fcb99f78a525dd29f446af7d179d.jpg
    ├── ...
    └── b374367ada898c0a0ec1e1cd724efbb1.jpg
```

- Chạy tất cả dòng lệnh (cells) trong file notebook SpineXR_YOLOv8.ipynb (có thể chạy bằng Colab) để train, test và predict. 
- File yolov8-65.3.pt là file trọng số của mô hình sau khi huấn luyện.
- Folder inference_results để visualize các kết quả khi dùng mô hình predict trên tập dữ liệu test 

### YOLO_NAS
Folder YOLO_NAS có cấu trúc như sau:

```
./YOLO_NAS
├── data.yaml
├── SpineXR_YOLO_NAS.ipynb
├── ckpt_best.pth
└── inference_results
    ├── 0a02fcb99f78a525dd29f446af7d179d.jpg
    ├── ...
    └── b374367ada898c0a0ec1e1cd724efbb1.jpg
```

- Chạy tất cả dòng lệnh (cells) trong file notebook SpineXR_YOLO_NAS.ipynb (có thể chạy bằng Colab) để train, test và predict. 
- File ckpt_best.pth là file trọng số của mô hình sau khi huấn luyện.
- Folder inference_results để visualize các kết quả khi dùng mô hình predict trên tập dữ liệu test

_Tất cả các kết quả khi chạy code (huấn luyện và kiểm thử) đều được mô tả kỹ càng trong các file notebook (.ipynb). Chi tiết về bài toán, bộ dữ liệu, phương pháp tiếp cận, thực nghiệm, kết luận ... được trình bày cụ thể trong file báo cáo DS312_SpineXR_report.pdf_
