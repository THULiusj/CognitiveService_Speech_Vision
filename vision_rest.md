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

### Javascript demo说明
以Analyze.html为例，没有对其他js文件的依赖，逻辑实现在html文件中。

1. 更新analyzeButtonClick函数如下

```javascript
function analyzeButtonClick() {

    // Clear the display fields.
    $("#sourceImage").attr("src", "#");
    $("#responseTextArea").val("");
    $("#captionSpan").text("");

    // Display the image.
    var sourceImageUrl = $("#inputImage").val();
    $("#sourceImage").attr("src", sourceImageUrl);

    AnalyzeImage(sourceImageUrl, $("#responseTextArea"), $("#captionSpan"));
}
```

2. 在analyzeButtonClick函数后面添加AnalyzeImage函数

```javascript
/* Analyze the image at the specified URL by using Microsoft Cognitive Services Analyze Image API.
 * @param {string} sourceImageUrl - The URL to the image to analyze.
 * @param {<textarea> element} responseTextArea - The text area to display the JSON string returned
 *                             from the REST API call, or to display the error message if there was 
 *                             an error.
 * @param {<span> element} captionSpan - The span to display the image caption.
 */
function AnalyzeImage(sourceImageUrl, responseTextArea, captionSpan) {
    // Request parameters.
    var params = {
        "visualFeatures": "Categories,Description,Color",
        "details": "",
        "language": "en",
    };

    // Perform the REST API call.
    $.ajax({
        url: common.uriBasePreRegion + 
             $("#subscriptionRegionSelect").val() + 
             common.uriBasePostRegion + 
             common.uriBaseAnalyze +
             "?" + 
             $.param(params),

        // Request headers.
        beforeSend: function(jqXHR){
            jqXHR.setRequestHeader("Content-Type","application/json");
            jqXHR.setRequestHeader("Ocp-Apim-Subscription-Key", 
                encodeURIComponent($("#subscriptionKeyInput").val()));
        },

        type: "POST",

        // Request body.
        data: '{"url": ' + '"' + sourceImageUrl + '"}',
    })

    .done(function(data) {

        // Extract and display the caption and confidence from the first caption in the description object.
        if (data.description && data.description.captions) {
            var caption = data.description.captions[0];

            if (caption.text && caption.confidence) {
                captionSpan.text("Caption: " + caption.text +
                    " (confidence: " + caption.confidence + ").");
            }
        }
        responseTextArea.val("Caption: " + caption.text);
    })

    .fail(function(jqXHR, textStatus, errorThrown) {
        // Prepare the error string.
        var errorString = (errorThrown === "") ? "Error. " : errorThrown + " (" + jqXHR.status + "): ";
        errorString += (jqXHR.responseText === "") ? "" : (jQuery.parseJSON(jqXHR.responseText).message) ? 
            jQuery.parseJSON(jqXHR.responseText).message : jQuery.parseJSON(jqXHR.responseText).error.message;

        // Put the error JSON in the response textarea.
        responseTextArea.val(JSON.stringify(jqXHR, null, 2));

        // Show the error message.
        alert(errorString);
    });
}
```

3. 打开html页面，输入Vision key,所申请的区域，以及在线图片的url，进行测试。