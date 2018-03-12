# Bing STT - Cognitive Service Speech

## 获取Speech API免费key
使用微软账户登录[认知服务官网](https://azure.microsoft.com/zh-cn/try/cognitive-services/)，可以获得30天的免费试用key，包括语音识别、图像识别、人脸识别等等。

## Sample说明
### Github url
https://github.com/Azure-Samples/SpeechToText-WebSockets-Javascript
Javascript SDK基于Speech Service Websocket Protocol实现，支持同时说话并接收识别的文本，可以最长支持10分钟的连续输入。

### 官方文档
https://docs.microsoft.com/en-us/azure/cognitive-services/speech/getstarted/getstartedjswebsockets

https://docs.microsoft.com/en-us/azure/cognitive-services/speech/concepts#recognition-modes

https://docs.microsoft.com/en-us/azure/cognitive-services/speech/api-reference-rest/websocketprotocol

### Sample起动注意事项
1. 下载并运行Sample
``` javascript
git clone https://github.com/Azure-Samples/SpeechToText-WebSockets-Javascript
cd SpeechToText-WebSockets-Javascript && npm run bundle
npm install
node sample-server.js
```
注意：SDK中的TypeScript代码使用默认模块系统（CommonJS）进行编译，这意味着编译会生成许多不同的JS源文件。为了使SDK可以在浏览器中使用，首先需要“browserify”（所有JavaScript源都需要粘在一起）。

### Sample功能
打开samples\browser\Sample.html，在浏览器里输入speech key，以及识别语言，打开麦克风开始识别。
recognition mode选择不同的识别模式：

1. 在interactive模式中，用户提出简短请求，并期望应用程序执行响应操作，话语通常持续约15秒。

2. 在conversation模式中，用户正在进行人与人之间的对话，经常使用俚语和其他非正式的演讲。

3. 在dictation模式中，用户向应用程序背诵较长的话语以进一步处理，最长十分钟。

Format选择不同的输出格式：
1. simple：只显示识别状态和识别文本的简化词组。
2. detailed：识别状态和短语结果的N-最佳列表，其中每个短语结果包含全部四种识别形式(Lexical, ITN, MaskedITN即敏感词处理, Display )和置信度分数Confidence。

### 代码说明 
1. npm安装
``` Javascript
npm install microsoft-speech-browser-sdk
```
2. 添加require语句到源文件(如sample_app.js)
```javascript
var  SDK  =  require（'<path_to_speech_SDK> /Speech.Browser.Sdk.js');
```

3. recognizer
- 设置recognizer
```Javascript
function RecognizerSetup(SDK, recognitionMode, language, format, subscriptionKey)
```

- 启动recognizer
```javascript
function RecognizerStart(SDK, recognizer)
```

4. bundle

运行npm run bundle，html中添加如下：
```html
<script src="../../distrib/speech.sdk.bundle.js"></script>
```
5. token-based authentication
- key认证

```javascript
SDK.CognitiveSubscriptionKeyAuthentication(subscriptionKey)
```

- token认证
在sample_server.js中调用"api.cognitive.microsoft.com/sts/v1.0/issueToken"来获得token，返回给客户端使用，保证key的安全性。


