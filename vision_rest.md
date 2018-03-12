# Vision - Cognitive Service Vision

## Github
https://github.com/Azure-Samples/cognitive-services-javascript-computer-vision-tutorial

https://github.com/Microsoft/Cognitive-Vision-Android

## 官方文档
https://docs.microsoft.com/zh-cn/azure/cognitive-services/computer-vision/tutorials/javascript-tutorial

https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa

## Restful API说明
### Vision API说明
Vision API分析图片中超过2000种物体、生物、场景和动作。一旦分析完成，API返回一个json体，描述图片的标签、颜色和字幕。
输入方式: Raw image binary (application/octet stream) 或者是 image URL
图片格式: JPEG, PNG, GIF, BMP
图片尺寸: 小于 4MB
图片维度: 大于50 x 50 pixel
```Restful API
POST https://westus.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Description,Tags&subscription-key=<Your subscription key>
```
- Parameter - visualFeatures: Categories, Tags, Faces, ImageType, Color, Adult
- Parameter - details: Celebrities, Landmarks
- Body: {"url":"http://example.com/images/test.jpg"} 或者是raw data
