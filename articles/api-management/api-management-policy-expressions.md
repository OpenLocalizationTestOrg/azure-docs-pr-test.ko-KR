---
title: "API 관리 정책 식 aaaAzure | Microsoft Docs"
description: "Azure API Management에서 정책 식에 대해 자세히 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: ea160028-fc04-4782-aa26-4b8329df3448
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 79da0d6ca3963307ec811a33aaac3d63a7abd97d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policy-expressions"></a>API Management 정책 식
정책 식 구문은 C# 6.0입니다. 각 식에 암시적으로 제공 되는 액세스 toohello [컨텍스트](api-management-policy-expressions.md#ContextVariables) 변수와 허용 된 [하위 집합](api-management-policy-expressions.md#CLRTypes) .NET Framework 형식.  
  
> [!NOTE]
>  정책 식에 대 한 자세한 내용은 참조 hello [정책 식을](https://azure.microsoft.com/documentation/videos/policy-expressions-in-azure-api-management/) 비디오.  
>   
>  정책 식을 사용한 정책 구성에 대한 데모는 [클라우드 표지 에피소드 177: Vlad Vinogradsky와 함께 하는 추가 API Management 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)(영문)을 참조하세요. 이 비디오는 hello 정책 식 데모 다음을 포함 합니다.  
>   
>  -   10:30-hello API에서 tooapply 정책을 hello를 사용 하 여 toosupply 컨텍스트 정보 toohello 백 엔드 서비스를 평준화 하는 방법을 참조 [쿼리 문자열 매개 변수를 설정](api-management-transformation-policies.md#SetQueryStringParameter) 및 [설정 HTTP 헤더](api-management-transformation-policies.md#SetHTTPheader) 정책입니다. 12시 10분에는 데모 작업에서 이러한 정책을 볼 수 있는 hello 개발자 포털에서 작업을 호출 합니다.  
> -   13:50-참조 방법을 toouse hello [JWT의 유효성을 검사](api-management-access-restriction-policies.md#ValidateJWT) 정책 toopre-토큰 클레임을 기반으로 하는 액세스 toooperations 권한을 부여 합니다. Hello 정책 편집기에 구성 된 toosee hello 정책이 too15:00를 빨리 감기 및 too18:50 모두와 사용 하지 않는 hello hello 개발자 포털에서 호출 하는 작업의 데모에 대 한 권한 부여 토큰을 필요로 하는 다음 합니다.  
> -   21:00-참조 방법을 toouse는 [API 검사기](https://azure.microsoft.com/documentation/articles/api-management-howto-api-inspector/) toosee 방법 정책 평가 되 고 hello hello 평가의 결과 추적 합니다.  
> -   25:25-참조 방법을 사용 하 여 정책 식을 toouse hello [캐시에서 가져오기](api-management-caching-policies.md#GetFromCache) 및 [저장소 toocache](api-management-caching-policies.md#StoreToCache) 정책 tooconfigure API 관리 응답 캐싱 일치 하는 항목의 hello 응답 캐시 hello는 기간 hello에 지정 된 대로 백 엔드 서비스 백업 서비스의 `Cache-Control` 지시문입니다.  
> -   34:30-tooperform 콘텐츠 hello 응답에서 데이터 요소를 제거 하 여 필터링 hello를 사용 하 여 hello 백 엔드 서비스에서 수신 하는 방법을 참조 [제어 흐름](api-management-advanced-policies.md#choose) 및 [본문 설정](api-management-transformation-policies.md#SetBody) 정책입니다. 개요 31:50 toosee부터 시작 [어두운 Sky 예측 API hello](https://developer.forecast.io/) 이 데모에 사용 합니다.  
> -   이 비디오에서는 사용 되는 toodownload hello 정책 문을 참조 hello [api-관리-샘플/정책](https://github.com/Azure/api-management-samples/tree/master/policies) github 리포지토리 합니다.  
  
  
##  <a name="Syntax"></a> 구문  
 단일 문 식은 `@(expression)`으로 묶으며 여기서 `expression`은 올바르게 구성된 C# 식입니다.  
  
 다중 문 식은 `@{expression}`으로 묶습니다. 다중 문 식 내에 모든 코드 경로는 `return` 문으로 끝나야 합니다.  
  
##  <a name="PolicyExpressionsExamples"></a> 예  
  
```  
@(true)  
  
@((1+1).ToString())  
  
@("Hi There".Length)  
  
@(Regex.Match(context.Response.Headers.GetValueOrDefault("Cache-Control",""), @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value)  
  
@(context.Variables.ContainsKey("maxAge") ? int.Parse((string)context.Variables["maxAge"]) : 3600)  
  
@{   
  string value;   
  if (context.Request.Headers.TryGetValue("Authorization", out value))   
  {   
    return Encoding.UTF8.GetString(Convert.FromBase64String(value));  
  }   
  else   
  {   
    return null;  
  }  
}  
```  
  
##  <a name="PolicyExpressionsUsage"></a> 사용 방법  
 식을 특성 값 또는 hello API 관리의 모든 텍스트 값으로 사용할 수 있습니다 [정책](api-management-policies.md)hello 정책 참조에서 지정 하지 않는 한 합니다.  
  
> [!IMPORTANT]
>  Note 정책 식을 사용 하는 경우 한지 제한적된 으로만 확인 hello 정책 식 hello 정책 정의 되었을 경우. Hello 식이 hello 게이트웨이에서 hello 인바운드 또는 아웃 바운드 파이프라인 실행 시 실행 되는, 이후 hello 정책 식에서 생성 된 모든 런타임 예외 hello API 호출에서 런타임 오류가 발생 합니다.  
  
##  <a name="CLRTypes"></a> 정책 식에 허용된 .NET Framework 형식  
 hello 다음 표에 hello.NET Framework 형식 및 멤버 정책 식에 사용할 수 있습니다.  
  
|CLR 형식|지원되는 방식|  
|--------------|-----------------------|  
|Newtonsoft.Json.Linq.Extensions|모든 메서드 지원됨|  
|Newtonsoft.Json.Linq.JArray|모든 메서드 지원됨|  
|Newtonsoft.Json.Linq.JConstructor|모든 메서드 지원됨|  
|Newtonsoft.Json.Linq.JContainer|모든 메서드 지원됨|  
|Newtonsoft.Json.Linq.JObject|모든 메서드 지원됨|  
|Newtonsoft.Json.Linq.JProperty|모든 메서드 지원됨|  
|Newtonsoft.Json.Linq.JRaw|모든 메서드 지원됨|  
|Newtonsoft.Json.Linq.JToken|모든 메서드 지원됨|  
|Newtonsoft.Json.Linq.JTokenType|모든 메서드 지원됨|  
|Newtonsoft.Json.Linq.JValue|모든 메서드 지원됨|  
|System.Collections.Generic.IReadOnlyCollection<T\>|모두|  
|System.Collections.Generic.IReadOnlyDictionary<TKey,  TValue>|모두|  
|System.Collections.Generic.ISet<TKey, TValue>|모두|  
|System.Collections.Generic.KeyValuePair<TKey,  TValue>|키, 값|  
|System.Collections.Generic.List<TKey, TValue>|모두|  
|System.Collections.Generic.Queue<TKey, TValue>|모두|  
|System.Collections.Generic.Stack<TKey, TValue>|모두|  
|System.Convert|모두|  
|System.DateTime|모두|  
|System.DateTimeKind|Utc|  
|System.DateTimeOffset|모두|  
|System.Decimal|모두|  
|System.Double|모두|  
|System.Guid|모두|  
|System.IEnumerable<T\>|모두|  
|System.IEnumerator<T\>|모두|  
|System.Int16|모두|  
|System.Int32|모두|  
|System.Int64|모두|  
|System.Linq.Enumerable<T\>|모든 메서드 지원됨|  
|System.Math|모두|  
|System.MidpointRounding|모두|  
|System.Nullable<T\>|모두|  
|System.Random|모두|  
|System.SByte|모두|  
|System.Security.Cryptography. HMACSHA384|모두|  
|System.Security.Cryptography. HMACSHA512|모두|  
|System.Security.Cryptography.HashAlgorithm|모두|  
|System.Security.Cryptography.HMAC|모두|  
|System.Security.Cryptography.HMACMD5|모두|  
|System.Security.Cryptography.HMACSHA1|모두|  
|System.Security.Cryptography.HMACSHA256|모두|  
|System.Security.Cryptography.KeyedHashAlgorithm|모두|  
|System.Security.Cryptography.MD5|모두|  
|System.Security.Cryptography.RNGCryptoServiceProvider|모두|  
|System.Security.Cryptography.SHA1|모두|  
|System.Security.Cryptography.SHA1Managed|모두|  
|System.Security.Cryptography.SHA256|모두|  
|System.Security.Cryptography.SHA256Managed|모두|  
|System.Security.Cryptography.SHA384|모두|  
|System.Security.Cryptography.SHA384Managed|모두|  
|System.Security.Cryptography.SHA512|모두|  
|System.Security.Cryptography.SHA512Managed|모두|  
|System.Single|모두|  
|System.String|모두|  
|System.StringSplitOptions|모두|  
|System.Text.Encoding|모두|  
|System.Text.RegularExpressions.Capture|Index, Length, Value|  
|System.Text.RegularExpressions.CaptureCollection|Count, Item|  
|System.Text.RegularExpressions.Group|Captures, Success|  
|System.Text.RegularExpressions.GroupCollection|Count, Item|  
|System.Text.RegularExpressions.Match|Empty, Groups, Result|  
|System.Text.RegularExpressions.Regex|.ctor, IsMatch, Match, Matches, Replace|  
|System.Text.RegularExpressions.RegexOptions|Compiled, IgnoreCase, IgnorePatternWhitespace, Multiline, None, RightToLeft, Singleline|  
|System.TimeSpan|모두|  
|System.Tuple|모두|  
|System.UInt16|모두|  
|System.UInt32|모두|  
|System.UInt64|모두|  
|System.Uri|모두|  
|System.Xml.Linq.Extensions|모든 메서드 지원됨|  
|System.Xml.Linq.XAttribute|모든 메서드 지원됨|  
|System.Xml.Linq.XCData|모든 메서드 지원됨|  
|System.Xml.Linq.XComment|모든 메서드 지원됨|  
|System.Xml.Linq.XContainer|모든 메서드 지원됨|  
|System.Xml.Linq.XDeclaration|모든 메서드 지원됨|  
|System.Xml.Linq.XDocument|모든 메서드 지원됨|  
|System.Xml.Linq.XDocumentType|모든 메서드 지원됨|  
|System.Xml.Linq.XElement|모든 메서드 지원됨|  
|System.Xml.Linq.XName|모든 메서드 지원됨|  
|System.Xml.Linq.XNamespace|모든 메서드 지원됨|  
|System.Xml.Linq.XNode|모든 메서드 지원됨|  
|System.Xml.Linq.XNodeDocumentOrderComparer|모든 메서드 지원됨|  
|System.Xml.Linq.XNodeEqualityComparer|모든 메서드 지원됨|  
|System.Xml.Linq.XObject|모든 메서드 지원됨|  
|System.Xml.Linq.XProcessingInstruction|모든 메서드 지원됨|  
|System.Xml.Linq.XText|모든 메서드 지원됨|  
|System.Xml.XmlNodeType|모두|  
  
##  <a name="ContextVariables"></a> 컨텍스트 변수  
 `context`라는 변수는 모든 정책 [식](api-management-policy-expressions.md#Syntax)에서 암시적으로 사용할 수 있습니다. 해당 멤버 제공 정보 관련 toohello `\request`합니다. 모든 hello `context` 멤버는 읽기 전용입니다.  
  
|컨텍스트 변수|허용된 메서드, 속성 및 매개 변수 값|  
|----------------------|-------------------------------------------------------|  
|context|Api: IApi<br /><br /> 배포<br /><br /> LastError<br /><br /> 작업<br /><br /> 제품<br /><br /> 요청<br /><br /> RequestId: string<br /><br /> 응답<br /><br /> 구독<br /><br /> Tracing: bool<br /><br /> 사용자<br /><br /> Variables:IReadOnlyDictionary<string, object><br /><br /> void Trace(message: string)|  
|context.Api|Id: string<br /><br /> Name: string<br /><br /> Path: string<br /><br /> ServiceUrl: IUrl|  
|context.Deployment|Region: string<br /><br /> ServiceName: string|  
|context.LastError|Source: string<br /><br /> Reason: string<br /><br /> Message: string<br /><br /> Scope: string<br /><br /> Section: string<br /><br /> Path: string<br /><br /> PolicyId: string<br /><br /> context.LastError에 대한 자세한 내용은 [오류 처리](api-management-error-handling-policies.md)를 참조하세요.|  
|context.Operation|Id: string<br /><br /> Method: string<br /><br /> Name: string<br /><br /> UrlTemplate: string|  
|context.Product|Apis: IEnumerable<IApi\><br /><br /> ApprovalRequired: bool<br /><br /> Groups: IEnumerable<IGroup\><br /><br /> Id: string<br /><br /> Name: string<br /><br /> State: enum ProductState {NotPublished, Published}<br /><br /> SubscriptionLimit: int?<br /><br /> SubscriptionRequired: bool|  
|context.Request|Body: IMessageBody<br /><br /> Certificate: System.Security.Cryptography.X509Certificates.X509Certificate2<br /><br /> Headers: IReadOnlyDictionary<string, string[]><br /><br /> IpAddress: string<br /><br /> MatchedParameters: IReadOnlyDictionary<string, string><br /><br /> Method: string<br /><br /> OriginalUrl:IUrl<br /><br /> Url: IUrl|  
|string context.Request.Headers.GetValueOrDefault(headerName: string, defaultValue: string)|headerName: string<br /><br /> defaultValue: string<br /><br /> 반환 쉼표로 구분 된 요청 헤더 값 또는 `defaultValue` hello 헤더가 없는 경우.|  
|context.Response|Body: IMessageBody<br /><br /> Headers: IReadOnlyDictionary<string, string[]><br /><br /> StatusCode: int<br /><br /> StatusReason: string|  
|string context.Response.Headers.GetValueOrDefault(headerName: string, defaultValue: string)|headerName: string<br /><br /> defaultValue: string<br /><br /> 쉼표로 구분 된 응답 헤더 값을 반환 하거나 `defaultValue` hello 헤더가 없는 경우.|  
|context.Subscription|CreatedTime: DateTime<br /><br /> EndDate: DateTime?<br /><br /> Id: string<br /><br /> Key: string<br /><br /> Name: string<br /><br /> PrimaryKey: string<br /><br /> SecondaryKey: string<br /><br /> StartDate: DateTime?|  
|context.User|Email: string<br /><br /> FirstName: string<br /><br /> Groups: IEnumerable<IGroup\><br /><br /> Id: string<br /><br /> Identities: IEnumerable<IUserIdentity\><br /><br /> LastName: string<br /><br /> Note: string<br /><br /> RegistrationDate: DateTime|  
|IApi|Id: string<br /><br /> Name: string<br /><br /> Path: string<br /><br /> Protocols: IEnumerable<string\><br /><br /> ServiceUrl: IUrl<br /><br /> SubscriptionKeyParameterNames: ISubscriptionKeyParameterNames|  
|IGroup|Id: string<br /><br /> Name: string|  
|IMessageBody|As<T\>(preserveContent: bool = false): Where T: string, JObject, JToken, JArray, XNode, XElement, XDocument<br /><br /> hello `context.Request.Body.As<T>` 및 `context.Response.Body.As<T>` 메서드는 요청 및 응답 메시지 본문 지정된 된 형식에 사용 되는 tooread `T`합니다. 기본적으로 hello 메서드 사용 하 여 hello 원래 메시지 본문 스트림과 reneders 후 사용할 수 없는 반환 합니다. hello 메서드 함으로써에서 작동 하는 집합 hello hello 본문 스트림의 복사본 tooavoid `preserveContent` 매개 변수가 너무`true`합니다. 이동 [여기](api-management-transformation-policies.md#SetBody) toosee 예입니다.|  
|IUrl|Host: string<br /><br /> Path: string<br /><br /> Port: int<br /><br /> Query: IReadOnlyDictionary<string, string[]><br /><br /> QueryString: string<br /><br /> Scheme: string|  
|IUserIdentity|Id: string<br /><br /> Provider: string|  
|ISubscriptionKeyParameterNames|Header: string<br /><br /> Query: string|  
|string IUrl.Query.GetValueOrDefault(queryParameterName: string, defaultValue: string)|queryParameterName: string<br /><br /> defaultValue: string<br /><br /> 반환 쉼표로 구분 된 쿼리 매개 변수 값 또는 `defaultValue` hello 매개 변수가 없는 경우.|  
|T context.Variables.GetValueOrDefault<T\>(variableName: string, defaultValue: T)|variableName: string<br /><br /> defaultValue: T<br /><br /> 변수 값 캐스트 tootype 반환 `T` 또는 `defaultValue` hello 변수가 없는 경우.<br /><br /> 이 메서드는 hello 지정 된 형식 일치 하지 않는 경우 hello 실제 유형의 변수를 반환 하는 hello 예외가 throw 됩니다.|  
|BasicAuthCredentials AsBasic(input: this string)|input: string<br /><br /> Hello 메서드 반환 형식의 개체에 hello 입력된 매개 변수에 유효한 HTTP 기본 인증 권한 부여 요청 헤더 값이 있으면 `BasicAuthCredentials`; 그렇지 않으면 hello 메서드가 null을 반환 합니다.|  
|bool TryParseBasic(input: this string, result: out BasicAuthCredentials)|input: string<br /><br /> result: out BasicAuthCredentials<br /><br /> Hello 메서드가 반환 하는 경우 hello 입력된 매개 변수에 유효한 HTTP 기본 인증 권한 부여 요청 헤더 값이 포함, `true` 형식의 값을 포함 하는 hello 결과 매개 변수에 `BasicAuthCredentials`; 그렇지 않으면 hello 메서드 반환 `false`합니다.|  
|BasicAuthCredentials|Password: string<br /><br /> UserId: string|  
|Jwt AsJwt(input: this string)|input: string<br /><br /> Hello 메서드 반환 형식의 개체에 hello 입력된 매개 변수에 유효한 JWT 토큰 값이 있으면 `Jwt`; 그렇지 않으면 hello 메서드 반환 `null`합니다.|  
|bool TryParseJwt(input: this string, result: out Jwt)|input: string<br /><br /> result: out Jwt<br /><br /> Hello 메서드가 반환 하는 경우 hello 입력된 매개 변수에 유효한 JWT 토큰 값이 포함, `true` 형식의 값을 포함 하는 hello 결과 매개 변수에 `Jwt`; 그렇지 않으면 hello 메서드 반환 `false`합니다.|  
|Jwt|Algorithm: string<br /><br /> Audience: IEnumerable<string\><br /><br /> Claims: IReadOnlyDictionary<string, string[]><br /><br /> ExpirationTime: DateTime?<br /><br /> Id: string<br /><br /> Issuer: string<br /><br /> NotBefore: DateTime?<br /><br /> Subject: string<br /><br /> Type: string|  
|string Jwt.Claims.GetValueOrDefault(claimName: string, defaultValue: string)|claimName: string<br /><br /> defaultValue: string<br /><br /> 쉼표로 구분 된 클레임 값 반환 또는 `defaultValue` hello 헤더가 없는 경우.|

## <a name="next-steps"></a>다음 단계
정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.  
