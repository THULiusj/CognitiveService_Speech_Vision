# Bing TTS - Cognitive Service Speech

## 获取TTS API免费key
使用微软账户登录[认知服务官网](https://azure.microsoft.com/zh-cn/try/cognitive-services/)，可以获得30天的免费试用key，包括语音识别、图像识别、人脸识别等等。

## Sample说明
### Github url
https://github.com/Azure-Samples/Cognitive-Speech-TTS/tree/master/Samples-Http/NodeJS

### 官方文档
TTS使用的是Restful API调用

https://docs.microsoft.com/en-us/azure/cognitive-services/speech/api-reference-rest/bingvoiceoutput


### Sample起动注意事项
1. TTSService.js中添加
``` Javascript
var apiKey = "Your api key goes here";
```

2. 修改语言和人声
``` Javascript
    var ssml_doc = xmlbuilder.create('speak')
        .att('version', '1.0')
        .att('xml:lang', 'zh-CN')
        .ele('voice')
        .att('xml:lang', 'zh-CN')
        .att('xml:gender', 'Female')
        .att('name', 'Microsoft Server Speech Text to Speech Voice (zh-CN, HuihuiRUS)')
        .txt('This is a demo to call Microsoft text to speech service.')
        .end();
```
3. 运行 node TTSSample.js




