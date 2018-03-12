# Bing TTS - Cognitive Service Speech

## 获取STT API免费key
使用微软账户登录[认知服务官网](https://azure.microsoft.com/zh-cn/try/cognitive-services/)，可以获得30天的免费试用key，包括语音识别、图像识别、人脸识别等等。

## Sample说明
### Github url
https://github.com/Azure-Samples/Cognitive-Speech-TTS/tree/master/Android

### 官方文档
TTS使用的是Restful API调用

https://docs.microsoft.com/en-us/azure/cognitive-services/speech/api-reference-rest/bingvoiceoutput


### Sample起动注意事项
1. 添加订阅key
"res/values/strings.xml"中key为"primaryKey"中的值改为上面申请的免费试用语音识别key
2. 修改识别语种：MainActivity.java文件中。
```Java
Voice v = new Voice("en-US", "Microsoft Server Speech Text to Speech Voice (en-US, ZiraRUS)", Voice.Gender.Female, true);

//Voice v = new Voice("zh-CN", "Microsoft Server Speech Text to Speech Voice (zh-CN, HuihuiRUS)", Voice.Gender.Female, true);
```
### 代码说明 
1. 将输入的文本转换成语音
``` Java
m_syn.SpeakToAudio(getString(R.string.tts_text));
```




