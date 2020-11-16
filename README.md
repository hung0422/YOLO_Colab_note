# YOLOv4 

## YOLOv4 設定檔

* obj.names
  * 把要訓練的類別列上去
* train.txt
  * 把要訓練的照片路徑寫上去
* valid.txt
  * 把要驗證的照片路徑寫上去
* obj.data
  * classes = 訓練類別數量
* yolov4.cfg
  * 搜尋"[yolo]"，更改所有[yolo]底下的classes = 訓練類別數量
  * 搜尋"[yolo]"，更改所有[yolo]上一層[convolutional]的"filters"改成(classes + 5) x 3
  * max_batches = 訓練類別數量*2000, 但不少於4000
  * steps = max_batches * 0.8, max_batches * 0.9
  * 如果訓練時顯示記憶體不足要調整batch和subdivisions
  * [其他詳細設定參考](https://blog.csdn.net/hrsstudy/article/details/65447947)

## Google Colab

* 登入Google Drive，點選 新增 -> 更多 -> 連結更多應用程式
* 在搜尋欄輸入"colaboratory" -> 安裝
* 點選 新增 -> 更多 -> Google colaboratory 
* 進入Google Colab後，點選左上角編輯 -> 筆記本設定 -> 硬體加速器 -> GPU -> 儲存
* 查看GPU型號
```
!nvidia-smi
```
* 下載YOLO darknet
```
!git clone https://github.com/AlexeyAB/darknet
```
* 修改參數
```
%cd darknet
!sed -i 's/GPU=0/GPU=1/' Makefile
!sed -i 's/OPENCV=0/OPENCV=1/' Makefile
!sed -i 's/GUDNN=0/GUDNN=1/' Makefile
!sed -i 's/GUDNN_HALF=0/GUDNN_HALF=1/' Makefile
```
```
!make
```
* 下載測試權重檔
```
!wget https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.weights
```
* 測試YOLO是否安裝完成
```
!.darknet detect cfg/yolov4.cfg yolov4.weights data/dog.jpg
```
```
imshow('predictions.jpg')
```
* Google Colab 和雲端硬碟連接
```
from google.colab import drive
drive.mount('/content/gdrive',force_remount=True)
```
* 將雲端硬碟檔案複製到Google Colab
```
!cp '/content/gdrive/My Drive/<檔案路徑>' /content/
```
* 將Google Colab檔案複製到雲端硬碟
```
!cp '/content/<檔案路徑>' '/content/gdrive/My Drive/<檔案路徑>' 
```
* 解壓縮檔案
```
!unzip /content/<檔案路徑>
```
* 壓縮檔案
```
!zip -r <壓縮檔名>.zip <資料夾>
```
* 在Google Colab上訓練YOLOv4模型
```
! darknet/darknet detector train /content/<路徑>/obj.data /content/<路徑>/yolov4.cfg /content/<路徑>/yolov4.conv.137(權重檔) -dont_show
```
* 在Google Colab上辨識YOLOv4影片
```
! darknet/darknet detector demo /content/<路徑>/obj.data /content/<路徑>/yolov4.cfg /content/<路徑>/<訓練完的權重檔> /content/<想辨識的影片> -dont_show -out_filename <新的影片檔名>
```
* 在Google Colab上辨識YOLOv4照片
```
! darknet/darknet detector test /content/<路徑>/obj.data /content/<路徑>/yolov4.cfg /content/<路徑>/<訓練完的權重檔> /content/<想辨識的照片> -dont_show
```

## LabelImg
* [官網下載](https://tzutalin.github.io/labelImg/)
* [官網教學](https://github.com/tzutalin/labelImg)


