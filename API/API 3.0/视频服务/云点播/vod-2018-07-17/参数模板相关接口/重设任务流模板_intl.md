## 1. API Description
API domain name: vod.tencentcloudapi.com.  
This API updates the task information of an existing task flow template.  
Default API request rate limit: 100 requests/sec.

## 2. Input Parameters
The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/266/31756).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyTranscodeTemplate |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-17 |
| Region | No | String | Common parameter; optional for this API |
| Name | Yes | String | Task flow name. |
| MediaProcessTask | No | [MediaProcessTaskInput](/document/api/266/31773#MediaProcessTaskInput) | Parameter of the video processing task. |
| AiContentReviewTask | No | [AiContentReviewTaskInput](/document/api/266/31773#AiContentReviewTaskInput) | Parameter of the AI-based content review task. |
| AiAnalysisTask | No | [AiAnalysisTaskInput](/document/api/266/31773#AiAnalysisTaskInput) | Parameter of the AI-based content analysis task. |
| AiRecognitionTask | No | [AiRecognitionTaskInput](/document/api/266/31773#AiRecognitionTaskInput) | Parameter of the AI-based content recognition task. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). Input the ID of the sub-application that has the desired resources; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample
### Sample 1. Resetting a Task Flow Template
Modify a task flow template named "My Task Flow" to change its transcoding output to three formats of 220, 230, and 240.
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=ResetProcedureTemplate
&Name=My Task Flow
&MediaPrcoessTask.TranscodeTaskSet.0.Definition=220
&MediaPrcoessTask.TranscodeTaskSet.1.Definition=230
&MediaPrcoessTask.TranscodeTaskSet.2.Definition=240
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3"
  }
}
```
## 5. Developer Resources
### API Explorer
**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=PullEvents)

### SDK
TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.
* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI
* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes
The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | The error is caused internally. |
| InvalidParameter | A parameter is not valid or cannot be used for the request.  |
| InvalidParameter.ProcedureNameNotExist | The name of the task flow template does not exist.|
| InvalidParameterValue.SubAppId | The sub-application ID is invalid or unfounded. |

