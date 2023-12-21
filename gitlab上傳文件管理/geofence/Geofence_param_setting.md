## 新增geofence參數

### 新增參數內容

參考PX4，新增兩個geofence參數：

| 名稱            | Description                                                  | Default |
| --------------- | ------------------------------------------------------------ | ------- |
| GF_ACTION       | 設定違反geofence採取動作<br />值：(目前只支援0,2,5，參考px4保留其餘的選項)<br />- 0：none<br />- 1：警告<br />- 2：position hold<br />- 3：return to home point<br />- 4：terminate<br />- 5：land | 0       |
| GF_MAX_HOR_DIST | 最大水平飛行範圍 （鳥籠半徑）<br />值：<br />- 0.0：默認值，GF_ACTION會強制改為none | 0.0     |

### 使用

在mav3.py中設定參數如下

```python
set_param("GF_ACTION",2)

#單位為cm，如下為輸入30公尺
set_param("GF_MAX_HOR_DIST",3000)
```

