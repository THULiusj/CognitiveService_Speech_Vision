# Bing TTS - Cognitive Service Speech

## 获取TTS API免费key
使用微软账户登录[认知服务官网](https://azure.microsoft.com/zh-cn/try/cognitive-services/)，可以获得30天的免费试用key，包括语音识别、图像识别、人脸识别等等。

## 官方文档
TTS使用的是Restful API调用

https://docs.microsoft.com/en-us/azure/cognitive-services/speech/api-reference-rest/bingvoiceoutput


## API说明
1. 采用JWT token作为认证，过期时间10分钟。token获取如下：
``` Restful API
POST https://api.cognitive.microsoft.com/sts/v1.0/issueToken
```
```
Header:
Content-Length: 0
Ocp-Apim-Subscription-Key: Your subscription key
```
2. 语音合成
- 认证输入：Authorization: Bearer [Base64 access_token]
- 输入content为ssml形式
- 输出语音形式为Outputformat
- X-Search-AppId：GUID
- X-Search-ClientID：GUID
- User-Agent：少于255字符的应用名
``` 
POST /synthesize
HTTP/1.1
Host: speech.platform.bing.com

X-Microsoft-OutputFormat: riff-8khz-8bit-mono-mulaw
Content-Type: application/ssml+xml
Host: speech.platform.bing.com
Content-Length: 197
Authorization: Bearer [Base64 access_token]

<speak version='1.0' xml:lang='en-US'><voice xml:lang='en-US' xml:gender='Female' name='Microsoft Server Speech Text to Speech Voice (en-US, ZiraRUS)'>Microsoft Bing Voice Output API</voice></speak>
```
3. 输入content，改变特定字符可以修改语音的发音、发声率、音量等。
```XML
<speak version='1.0' xmlns="http://www.w3.org/2001/10/synthesis" xml:lang='en-US'>
<voice  name='Microsoft Server Speech Text to Speech Voice (en-US, BenjaminRUS)'>
<phoneme alphabet="ipa" ph="t&#x259;mei&#x325;&#x27E;ou&#x325;">
<prosody rate="+30.00%">
Welcome to use Microsoft Cognitive Services 
<break time="100ms" /> 
Text-to-Speech API.
</prosody></phoneme></voice> </speak>
```



