# Bing STT - Cognitive Service Speech

## 获取Speech API免费key
使用微软账户登录[认知服务官网](https://azure.microsoft.com/zh-cn/try/cognitive-services/)，可以获得30天的免费试用key，包括语音识别、图像识别、人脸识别等等。

## 官方文档
https://docs.microsoft.com/en-us/azure/cognitive-services/speech/getstarted/getstartedrest

https://docs.microsoft.com/en-us/azure/cognitive-services/speech/api-reference-rest/websocketprotocol


## Rest API
### Http模式
支持最长15秒语音，只能返回最终结果。
- Url
https://speech.platform.bing.com/speech/recognition/<RECOGNITION_MODE>/cognitiveservices/v1?language=<LANGUAGE_TAG>&format=<OUTPUT_FORMAT>
- Headers
``` Restful API
Accept: application/json;text/xml
Content-Type: audio/wav; codec=audio/pcm; Samplerate=16000
Ocp-Apim-Subscription-Key: YOUR_SUBSCRIPTION_KEY
Host: speech.platform.bing.com
```
### Websocket模式

一个WebSocket连接作为一个HTTP请求开始，它包含HTTP头，表明客户希望将连接升级到WebSocket而不是使用HTTP语义。服务器通过返回一个HTTP 101 Switching Protocols响应来表明它愿意参与WebSocket连接。在握手交换之后，客户端和服务都保持套接字打开并开始使用基于消息的协议来发送和接收信息，最长十分钟，非活动时间三分钟。

开始建立websocket连接，interactive表示识别模式：
```Restful API
GET /speech/recognition/interactive/cognitiveservices/v1 HTTP/1.1
Host: speech.platform.bing.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
Sec-WebSocket-Version: 13
Authorization: t=EwCIAgALBAAUWkziSCJKS1VkhugDegv7L0eAAJqBYKKTzpPZOeGk7RfZmdBhYY28jl&p=
X-ConnectionId: A140CAF92F71469FA41C72C7B5849253
Origin: https://speech.platform.bing.com
```

其中Authorization要使用JWT token:

POST https://api.cognitive.microsoft.com/sts/v1.0/issueToken

Authorization: Bearer [Base64 access_token]
