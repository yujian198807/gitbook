# Python插件
## 1.xlrd(读取xls或者xlrd格式的表)
```python
import xlrd

# ctype : 0 empty,1 string, 2 number, 3 date, 4 boolean, 5 error
workbook = xlrd.open_workbook(path)
sheet = workbook.sheet_by_index(0)
for i in range(3, sheet.nrows):
    cell = sheet.cell(i, 2)
    value = cell.value
```
---

## 2.xlsxwriter(写xlsx格式)
```python
import xlsxwriter

workbook = xlsxwriter.Workbook('export.xlsx')
worksheet = workbook.add_worksheet()
worksheet.set_column('A:A', 150)
workformat = workbook.add_format()
workformat.set_align('left')
try:
    for i in range(len(UNREFERENCE_FILES)):
        worksheet.write('A%d' % (i+1), UNREFERENCE_FILES[i])
except Exception as identifier:
    pass
workbook.close()
```
---

## 3.requests(HTTP请求)
```python
import requests

data = json.dumps({
    'msgtype': 'text',
    'text': {
        'content': '热更新版本-%d(%s)发布' % (version, args.debug and '测试' or '正式')
    }
})
r = requests.post('https://oapi.dingtalk.com/robot/send?access_token=%s' % args.dingtoken, data, headers={
                        'Content-Type': 'application/json;charset=UTF-8;',
                        'Content-Length': str(len(data.encode('utf-8')))})
```
---

## 4.argparse(参数解析)
```python
import argparse

parser = argparse.ArgumentParser(description='执行3步流程：打包->压缩->上传')
parser.add_argument('--project', type=str,
                    default='E:/Work/IslandSurvival', help="项目路径")
parser.add_argument(
    '--cocos', type=str, default='D:/Cocos/Creator/3.3.0/CocosCreator.exe', help='Cocos引擎可执行文件的路径')
parser.add_argument(
    '--config', type=str, default='E:/Work/IslandSurvival/extensions/publish/android/build-debug.json', help='构建配置文件的路径')
parser.add_argument(
    '--info', type=str, default='E:/Work/IslandSurvival/tools/configs/AppConfig.xlsx', help='游戏配置信息')
parser.add_argument('--output', type=str,
                    default='E:/Work/IslandSurvival/build/android', help='输出路径')
parser.add_argument('--debug', action='store_true', help='是否为调试模式')
parser.add_argument('--platform', type=str, default='android', help="打包的平台")
parser.add_argument('--pack', action='store_true', help="是否为打包")
parser.add_argument(
    '--dingtoken', default='59ac40fdc4c5e5ac91e6aaea7a1ee598d5faf1a73c1f2b359c6052666e5c3e0b', help="钉钉秘钥")
args = parser.parse_args()
```
---

## 5.zipfile, gzip, base64(压缩)
```python
import zipfile
import base64
import gzip

z = zipfile.ZipFile('a.zip', 'w')
z.write('path', 'newPath', zipfile.ZIP_DEFLATED)
z.close()

gz = gzip.GzipFile('test.png', 'wb', 9, None, 1)
gz.write(original_data)
gz.close()

postData = base64.b64encode(data).decode()    
```
---

## 6.hashlib(MD5)
```python
import hashlib

md5 = hashlib.md5(data).hexdigest()  
```
---

## 7.yaml(解析YAML)

```python
import yaml

yaml.load(data, Loader=yaml.FullLoader)  
```
---

## **8.mako(模板语法))**
```python
from mako.template import Template
from mako.exceptions import RichTraceback    

try:
    t = Template(filename=os.path.join(ScriptDir, self._template))
    content = t.render(entity=self)
    return content
except:
    traceback = RichTraceback()
    for (filename, lineno, function, line) in traceback.traceback:
        print("File %s, line %s, in %s" % (filename, lineno, function))
        print(line, "\n")
    print("%s: %s" %
            (str(traceback.error.__class__.__name__), traceback.error))
```
---

## **9.pillow(图片编辑))**
```python
from PIL import Image

try:
    im = Image.open(path)
    if im.size[0] > size[0] and im.size[1] > size[1]:
        im = im.resize((size[0], size[1]))
        im.save(path)
except Exception as e:
    pass
```
---

## **10.paddlespeech(音频合成，翻译)**
```python
pip install paddlepaddle paddlespeech

# 声音分类
paddlespeech cls --input input.wav

# 语音识别
paddlespeech asr --lang zh --input input.wav

# 语音翻译
paddlespeech st --input input.wav

# 语音合成
paddlespeech tts --input "翻译内容" --output output.wav
```
---