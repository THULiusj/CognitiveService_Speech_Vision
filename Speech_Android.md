# Bing STT - Cognitive Service Speech

## 获取STT API免费key
使用微软账户登录[认知服务官网](https://azure.microsoft.com/zh-cn/try/cognitive-services/)，可以获得30天的免费试用key，包括语音识别、图像识别、人脸识别等等。

## Github url
https://github.com/Azure-Samples/Cognitive-Speech-STT-Android

## 官方文档
https://docs.microsoft.com/en-us/azure/cognitive-services/speech/getstarted/getstartedjavaandroid

### Sample起动注意事项
1. 从http://search.maven.org中下载"g:com.microsoft.projectoxford"，加载client library到环境中
2. 下载合适的JNI library libandroid_platform.so，放到路径app/src/main/jniLibs/armeabi/或者app/src/main/jniLibs/x86/

3. 添加订阅key
"res/values/strings.xml"中key为"primaryKey"中的值改为上面申请的免费试用语音识别key

4. 修改识别语种：MainActivity.java文件中，改为zh-cn。
```Java
private String getDefaultLocale() {
        return "en-us";
    }
```
5. 三种识别模式

Short-form recognition：短句模式，最长15秒。返回阶段性识别结果和最终结果N-best。

Long-form dictation：长句模式，最长10分钟。返回多次阶段性识别结果，及最终结果N-best，每次基于停顿进行识别。

Recognition with intent：采用LUIS作为语义理解识别。

### 代码说明 
1. 创建client
``` Java
SpeechRecognitionServiceFactory.createMicrophoneClient
SpeechRecognitionServiceFactory.createDataClient
```

2. 启动识别
```Java
this.micClient.startMicAndRecognition();
```

3. 结果返回

``` Java
public void onPartialResponseReceived(final String response)
public void onFinalResponseReceived(final RecognitionResult response) 
```




