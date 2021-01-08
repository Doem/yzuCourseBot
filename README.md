# yzuCourseBot 元智選課機器人

## Update log

- 2021/01/09
	- [修改] 修改點擊選課後 alertMsg 的取得方式 (`.text` -> `.string`)，似乎是選課系統有修改，原本的方式 (`.text`) 無法獲取訊息
	- [新增] 判斷帳號密碼是否輸入錯誤 (僅比較帳號密碼錯誤及登入成功的訊息，不確定是否還有其他種情況也符合這個條件)
	- [新增] 判斷使用者是否不在選課時程內
- 2020/06/25
	- [更新] 把22號的更動改回來，我不知道暑修的網址跟一般修課的網址是否有差，還是資服處嗯真的一直改檔名。
- 2020/06/22
	- [更新] 因資服處更改檔名 (`SelCurr.aspx` -> `SelSc.aspx`)，所以更新登入檢查的String
	- [說明] 因為這個Bot其實沒什麼用(有更好的方式可以搶課)，加上我要畢業了，所以不打算再做太大的更動，歡迎學弟妹們發PR來維護，有任何想討論的請來信 aa0917954358@gmail.com 謝謝
- 2020/02/26
	- [新增] 異常登入判斷，會休息10分鐘後再繼續 
	- [新增] 系所編號判斷，填錯會報錯誤訊息
	- [新增] 新增delay功能，預設為1秒 (太快容易被server判定為異常request，請自行斟酌)
- 2019/12/11 
	- [修改] 優化判斷是否登入成功的方式
	- [修改] 優化部分hard code的地方
	- [新增] 判斷使用者的課程ID是否存在 

## Introduction
最近在整理code丟上github，況且上學期還訓練了一個高辨識率的model(請參考 [CNN-model-for-YZU-cpatcha-OCR](https://github.com/Doem/CNN-model-for-YZU-cpatcha-OCR))，所以就順手將之前寫的選課機器人從pytesseract替換成自己訓練的CNN model，並移除selenium的依賴改純用requests的方式去模擬選課動作。由於改寫的時間不是很多並沒有寫得很好，歡迎各位提交Bug上來我會再找時間修正的。

## Dependencies
|Name|
|----|
|lxml|
|keras|
|numpy|
|opencv|
|requests|
|configparser|
|BeautifulSoup|

### For Ubuntu
```
apt-get install -y libsm6 libxext6 libxrender-dev
pip3 install opencv-python beautifulsoup4 keras tensorflow lxml
```

## Remind
請斟酌使用本機器人程式，並自行負責使用後所造成的損失!

## Usage

### 1. 新增 `accounts.ini` 存放Portal帳密的檔案，格式如下:
```
[Default]
Account= your account
Password= your password
```

### 2. 修改 `yzuCourseBot.py` 中的`coursesList`變數新增想選的課程清單，格式如下:
```
coursesList = [
    '304,CS352A', 
    '901,LS239A', 
    '304,CS354A'
]
```

**304**: 為系所編號

**CS352A**: 為課程編號加上班級編號，CS352 + A

以上資訊都能在課程查詢網站或是選課系統中得知的訊息

### 3. 執行 `yzuCourseBot.py`
```
$ python yzuCourseBot.py
```

**請用Python3以上的版本執行**


## Bug Report
請來信 aa0917954358@gmail.com 或是開issue，謝謝!
