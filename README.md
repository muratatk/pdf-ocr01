import io
import os.path
import sys
print(sys.executable)

from google.oauth2 import  service_account

from google.cloud import vision

#from PIL import Image

credentials = service_account.Credentials.from_service_account_file('C:/Users/knk01040/Desktop/ocr-01-403800-d598553fc09f.json')

client = vision.ImageAnnotatorClient(credentials=credentials)

input_file= os.path.abspath('C:/Users/knk01040/Desktop/input/3343_001-1.png')

# https://techplay.jp/column/1641

#file = open(input_file, 'rb')
#text=file.read()
#print(text)
#content=text
#image=vision.Image(content=content)

# ローカル画像を読み込み、imageオブジェクト作成
with io.open(input_file, 'rb') as image_file:
    content = image_file.read()
image = vision.Image(content=content)

# Cloud Vision APIにアクセスして、テキスト検出結果を受け取り表示
response = client.text_detection(image=image)
print(response.text_annotations[0].description)




file = open('C:/Users/knk01040/Desktop/text/test.txt', "w+", encoding="utf-8")
# 文字列の書き込み
file.write(response.text_annotations[0].description)
# ファイルを閉じる（クローズ）
file.close()
