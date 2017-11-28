---
title: "Log Analytics HTTP 데이터 수집기 API | Microsoft Docs"
description: "REST API를 호출할 수 있는 모든 클라이언트에서 Log Analytics HTTP 데이터 수집기 API를 사용하여 POST JSON 데이터를 Log Analytics 저장소에 추가할 수 있습니다. 이 문서는 API를 사용하는 방법을 설명하며, 다양한 프로그래밍 언어를 사용하여 데이터를 게시하는 방법을 예제로 제시합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: b0c45ff8c1d4c9d35fbb3c8839b38a20df277055
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="send-data-to-log-analytics-with-the-http-data-collector-api"></a><span data-ttu-id="9284c-104">HTTP 데이터 수집기 API로 Log Analytics에 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="9284c-104">Send data to Log Analytics with the HTTP Data Collector API</span></span>
<span data-ttu-id="9284c-105">이 문서에서는 HTTP 데이터 수집기 API를 사용하여 REST API 클라이언트에서 Log Analytics로 데이터를 전송하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-105">This article shows you how to use the HTTP Data Collector API to send data to Log Analytics from a REST API client.</span></span>  <span data-ttu-id="9284c-106">스크립트 또는 응용 프로그램에서 수집하는 데이터를 포맷하고 요청에 포함하며 해당 요청을 Log Analytics에서 승인하게 하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-106">It describes how to format data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="9284c-107">PowerShell, C# 및 Python에 예가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="9284c-108">개념</span><span class="sxs-lookup"><span data-stu-id="9284c-108">Concepts</span></span>
<span data-ttu-id="9284c-109">HTTP 데이터 수집기 API를 사용하여 REST API를 수집할 수 있는 클라이언트에서 Log Analytics로 데이터를 전송하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-109">You can use the HTTP Data Collector API to send data to Log Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="9284c-110">Azure 또는 다른 클라우드에서 관리 데이터를 수집하는 Azure Automation의 Runbook, 또는 Log Analytics를 사용하여 데이터를 통합하고 분석하는 대체 관리 시스템일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics to consolidate and analyze data.</span></span>

<span data-ttu-id="9284c-111">Log Analytics 저장소의 모든 데이터는 특정 레코드 형식의 레코드로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-111">All data in the Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="9284c-112">JSON에서 여러 레코드로 HTTP 데이터 수집기 API에 보낼 데이터의 서식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-112">You format your data to send to the HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="9284c-113">데이터를 제출하면 개별 레코드가 요청 페이로드의 각 레코드에 대한 저장소에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-113">When you submit the data, an individual record is created in the repository for each record in the request payload.</span></span>


![HTTP 데이터 수집기 개요](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="9284c-115">요청 만들기</span><span class="sxs-lookup"><span data-stu-id="9284c-115">Create a request</span></span>
<span data-ttu-id="9284c-116">HTTP 데이터 수집기 API를 사용하려면 JSON(JavaScript Object Notation)에서 전송할 데이터가 포함된 POST 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-116">To use the HTTP Data Collector API, you create a POST request that includes the data to send in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="9284c-117">다음 세 개 표에는 각 요청에 필요한 속성이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-117">The next three tables list the attributes that are required for each request.</span></span> <span data-ttu-id="9284c-118">이 문서의 뒷부분에서 각각의 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-118">We describe each attribute in more detail later in the article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="9284c-119">요청 URI</span><span class="sxs-lookup"><span data-stu-id="9284c-119">Request URI</span></span>
| <span data-ttu-id="9284c-120">특성</span><span class="sxs-lookup"><span data-stu-id="9284c-120">Attribute</span></span> | <span data-ttu-id="9284c-121">속성</span><span class="sxs-lookup"><span data-stu-id="9284c-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="9284c-122">메서드</span><span class="sxs-lookup"><span data-stu-id="9284c-122">Method</span></span> |<span data-ttu-id="9284c-123">POST</span><span class="sxs-lookup"><span data-stu-id="9284c-123">POST</span></span> |
| <span data-ttu-id="9284c-124">URI</span><span class="sxs-lookup"><span data-stu-id="9284c-124">URI</span></span> |<span data-ttu-id="9284c-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="9284c-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="9284c-126">콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="9284c-126">Content type</span></span> |<span data-ttu-id="9284c-127">application/json</span><span class="sxs-lookup"><span data-stu-id="9284c-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="9284c-128">URI 매개 변수 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-128">Request URI parameters</span></span>
| <span data-ttu-id="9284c-129">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9284c-129">Parameter</span></span> | <span data-ttu-id="9284c-130">설명</span><span class="sxs-lookup"><span data-stu-id="9284c-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9284c-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="9284c-131">CustomerID</span></span> |<span data-ttu-id="9284c-132">Microsoft Operations Management Suite 작업 영역에 대한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-132">The unique identifier for the Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="9284c-133">리소스</span><span class="sxs-lookup"><span data-stu-id="9284c-133">Resource</span></span> |<span data-ttu-id="9284c-134">API 리소스 이름: /api/logs</span><span class="sxs-lookup"><span data-stu-id="9284c-134">The API resource name: /api/logs.</span></span> |
| <span data-ttu-id="9284c-135">API 버전</span><span class="sxs-lookup"><span data-stu-id="9284c-135">API Version</span></span> |<span data-ttu-id="9284c-136">이 요청에 사용하는 API의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-136">The version of the API to use with this request.</span></span> <span data-ttu-id="9284c-137">현재 2016-04-01입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9284c-138">헤더 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-138">Request headers</span></span>
| <span data-ttu-id="9284c-139">헤더</span><span class="sxs-lookup"><span data-stu-id="9284c-139">Header</span></span> | <span data-ttu-id="9284c-140">설명</span><span class="sxs-lookup"><span data-stu-id="9284c-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9284c-141">권한 부여</span><span class="sxs-lookup"><span data-stu-id="9284c-141">Authorization</span></span> |<span data-ttu-id="9284c-142">권한 부여 서명입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-142">The authorization signature.</span></span> <span data-ttu-id="9284c-143">문서의 뒷부분에 HMAC-SHA256 헤더를 만드는 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-143">Later in the article, you can read about how to create an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="9284c-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="9284c-144">Log-Type</span></span> |<span data-ttu-id="9284c-145">제출 중인 데이터의 레코드 종류를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-145">Specify the record type of the data that is being submitted.</span></span> <span data-ttu-id="9284c-146">현재는 로그 형식에서 영문자만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-146">Currently, the log type supports only alpha characters.</span></span> <span data-ttu-id="9284c-147">숫자 또는 특수 문자는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="9284c-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="9284c-148">x-ms-date</span></span> |<span data-ttu-id="9284c-149">RFC 1123 형식의 요청이 처리된 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-149">The date that the request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="9284c-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="9284c-150">time-generated-field</span></span> |<span data-ttu-id="9284c-151">데이터 항목의 타임스탬프가 포함된 데이터의 필드 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-151">The name of a field in the data that contains the timestamp of the data item.</span></span> <span data-ttu-id="9284c-152">필드를 지정하면 그 내용이 **TimeGenerated**에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="9284c-153">이 필드를 지정하지 않으면 **TimeGenerated**의 기본값은 메시지가 수집된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-153">If this field isn’t specified, the default for **TimeGenerated** is the time that the message is ingested.</span></span> <span data-ttu-id="9284c-154">메시지 필드의 내용은 ISO 8601 형식 YYYY-MM-DDThh:mm:ssZ를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-154">The contents of the message field should follow the ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="9284c-155">권한 부여</span><span class="sxs-lookup"><span data-stu-id="9284c-155">Authorization</span></span>
<span data-ttu-id="9284c-156">Log Analytics HTTP 데이터 수집기 API에 대한 모든 요청에는 권한 부여 헤더가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-156">Any request to the Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="9284c-157">요청을 인증하려면 요청을 수행하는 작업 영역에 대한 기본 키 또는 보조 키를 통해 요청을 서명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-157">To authenticate a request, you must sign the request with either the primary or the secondary key for the workspace that is making the request.</span></span> <span data-ttu-id="9284c-158">그런 다음 요청의 일부로 해당 서명을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-158">Then, pass that signature as part of the request.</span></span>   

<span data-ttu-id="9284c-159">권한 부여 헤더의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-159">Here's the format for the authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="9284c-160">*WorkspaceID*는 Operations Management Suite 작업 영역에 대한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-160">*WorkspaceID* is the unique identifier for the Operations Management Suite workspace.</span></span> <span data-ttu-id="9284c-161">*서명*은 요청에서 구성되고 [SHA256 알고리즘](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx)을 사용하여 계산된 [해시 기반 메시지 인증 코드(HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from the request and then computed by using the [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="9284c-162">그런 다음 Base64 인코딩을 사용하여 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="9284c-163">이 형식을 사용하여 **SharedKey** 서명 문자열을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-163">Use this format to encode the **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="9284c-164">서명 문자열의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="9284c-165">서명 문자열이 있을 때는 UTF-8 문자열에서 HMAC-SHA256 알고리즘을 사용하여 인코딩한 다음 결과를 Base64로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-165">When you have the signature string, encode it by using the HMAC-SHA256 algorithm on the UTF-8-encoded string, and then encode the result as Base64.</span></span> <span data-ttu-id="9284c-166">이 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="9284c-167">다음 섹션의 샘플은 권한 부여 헤더를 만드는 데 도움이 되는 예제 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-167">The samples in the next sections have sample code to help you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="9284c-168">요청 본문</span><span class="sxs-lookup"><span data-stu-id="9284c-168">Request body</span></span>
<span data-ttu-id="9284c-169">메시지의 본문은 JSON에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-169">The body of the message must be in JSON.</span></span> <span data-ttu-id="9284c-170">다음 형식으로 속성 이름과 값 쌍을 갖는 하나 이상의 레코드를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-170">It must include one or more records with the property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="9284c-171">다음 형식을 사용하여 단일 요청에서 여러 레코드를 일괄 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-171">You can batch multiple records together in a single request by using the following format.</span></span> <span data-ttu-id="9284c-172">모든 레코드는 동일한 레코드 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-172">All the records must be the same record type.</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a><span data-ttu-id="9284c-173">레코드 유형 및 속성</span><span class="sxs-lookup"><span data-stu-id="9284c-173">Record type and properties</span></span>
<span data-ttu-id="9284c-174">Log Analytics HTTP 데이터 수집기 API를 통해 데이터를 제출할 때 사용자 지정 레코드 유형을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-174">You define a custom record type when you submit data through the Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="9284c-175">현재는 다른 데이터 형식과 솔루션으로 만든 기존 레코드 형식에 데이터를 쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-175">Currently, you can't write data to existing record types that were created by other data types and solutions.</span></span> <span data-ttu-id="9284c-176">Log Analytics가 드러오는 데이터를 읽은 다음 입력한 값의 데이터 형식과 일치하는 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-176">Log Analytics reads the incoming data and then creates properties that match the data types of the values that you enter.</span></span>

<span data-ttu-id="9284c-177">Log Analytics API에 대한 각각의 요청은 레코드 형식의 이름과 함께 **Log-Type** 헤더를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-177">Each request to the Log Analytics API must include a **Log-Type** header with the name for the record type.</span></span> <span data-ttu-id="9284c-178">이 사용자 지정 로그를 다른 로그 형식과 구분하기 위해 입력한 이름에는 접미사 **_CL**이 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-178">The suffix **_CL** is automatically appended to the name you enter to distinguish it from other log types as a custom log.</span></span> <span data-ttu-id="9284c-179">예를 들어 **MyNewRecordType**을 입력하면 Log Analytics가 **MyNewRecordType_CL** 형식의 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-179">For example, if you enter the name **MyNewRecordType**, Log Analytics creates a record with the type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="9284c-180">이렇게 하면 사용자가 만든 형식 이름과 Microsoft가 현재 또는 향후에 포함한 이름 사이의 충돌을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="9284c-181">속성의 데이터 형식을 식별하기 위해 Log Analytics가 속성 이름에 접미사를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-181">To identify a property's data type, Log Analytics adds a suffix to the property name.</span></span> <span data-ttu-id="9284c-182">속성에 null 값이 있으면 속성이 해당 레코드에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-182">If a property contains a null value, the property is not included in that record.</span></span> <span data-ttu-id="9284c-183">이 표는 속성 데이터 형식과 해당하는 접미사를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-183">This table lists the property data type and corresponding suffix:</span></span>

| <span data-ttu-id="9284c-184">속성 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="9284c-184">Property data type</span></span> | <span data-ttu-id="9284c-185">접미사</span><span class="sxs-lookup"><span data-stu-id="9284c-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="9284c-186">문자열</span><span class="sxs-lookup"><span data-stu-id="9284c-186">String</span></span> |<span data-ttu-id="9284c-187">_s</span><span class="sxs-lookup"><span data-stu-id="9284c-187">_s</span></span> |
| <span data-ttu-id="9284c-188">Boolean</span><span class="sxs-lookup"><span data-stu-id="9284c-188">Boolean</span></span> |<span data-ttu-id="9284c-189">_b</span><span class="sxs-lookup"><span data-stu-id="9284c-189">_b</span></span> |
| <span data-ttu-id="9284c-190">Double</span><span class="sxs-lookup"><span data-stu-id="9284c-190">Double</span></span> |<span data-ttu-id="9284c-191">_d</span><span class="sxs-lookup"><span data-stu-id="9284c-191">_d</span></span> |
| <span data-ttu-id="9284c-192">날짜/시간</span><span class="sxs-lookup"><span data-stu-id="9284c-192">Date/time</span></span> |<span data-ttu-id="9284c-193">_t</span><span class="sxs-lookup"><span data-stu-id="9284c-193">_t</span></span> |
| <span data-ttu-id="9284c-194">GUID</span><span class="sxs-lookup"><span data-stu-id="9284c-194">GUID</span></span> |<span data-ttu-id="9284c-195">_g</span><span class="sxs-lookup"><span data-stu-id="9284c-195">_g</span></span> |

<span data-ttu-id="9284c-196">Log Analytics가 각 속성에 사용하는 데이터 형식은 새 레코드에 대한 레코드 형식이 이미 존재하는지 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-196">The data type that Log Analytics uses for each property depends on whether the record type for the new record already exists.</span></span>

* <span data-ttu-id="9284c-197">레코드 형식이 없으면 Log Analytics가 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-197">If the record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="9284c-198">Log Analytics는 JSON 형식을 사용하여 새 레코드에 대한 각 속성의 데이터 형식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-198">Log Analytics uses the JSON type inference to determine the data type for each property for the new record.</span></span>
* <span data-ttu-id="9284c-199">레코드 형식이 없으면 Log Analytics가 기존 속성에 따라 새 레코드를 만들려 합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-199">If the record type does exist, Log Analytics attempts to create a new record based on existing properties.</span></span> <span data-ttu-id="9284c-200">새 레코드에서 속성에 대한 데이터 형식이 일치하지 않고 기존 형식으로 변환할 수 없거나, 레코드가 존재하지 않는 속성을 포함하는 경우 Log Analytics는 관련 접미사가 있는 새 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-200">If the data type for a property in the new record doesn’t match and can’t be converted to the existing type, or if the record includes a property that doesn’t exist, Log Analytics creates a new property that has the relevant suffix.</span></span>

<span data-ttu-id="9284c-201">예를 들어, 이 제출 항목은 **number_d**, **boolean_b**, **string_s** 등의 세 가지 속성이 있는 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![샘플 레코드 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="9284c-203">이후 모든 값을 문자열 형식으로 지정하여 다음 항목을 제출하면 속성이 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-203">If you then submitted this next entry, with all values formatted as strings, the properties would not change.</span></span> <span data-ttu-id="9284c-204">이러한 값은 기존 데이터 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-204">These values can be converted to existing data types:</span></span>

![샘플 레코드 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="9284c-206">그러나 이 다음 제출을 실행하면 Log Analytics가 새 속성 **boolean_d** 및 **string_d**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-206">But, if you then made this next submission, Log Analytics would create the new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="9284c-207">이 값은 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-207">These values can't be converted:</span></span>

![샘플 레코드 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="9284c-209">이후 다음 항목을 제출하면 레코드 형식을 만들기 전에 Log Analytics가 **number_s**, **boolean_s** 및 **string_s** 등의 세 가지 속성으로 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-209">If you then submitted the following entry, before the record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="9284c-210">이 항목에서 각각의 초기 값은 문자열 형식이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-210">In this entry, each of the initial values is formatted as a string:</span></span>

![샘플 레코드 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="9284c-212">데이터 제한</span><span class="sxs-lookup"><span data-stu-id="9284c-212">Data limits</span></span>
<span data-ttu-id="9284c-213">Log Analytics 데이터 수집 API에 게시된 데이터에 대한 몇 가지 제약 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-213">There are some constraints around the data posted to the Log Analytics Data collection API.</span></span>

* <span data-ttu-id="9284c-214">Log Analytics 데이터 수집기 API의 게시물당 최대 30MB.</span><span class="sxs-lookup"><span data-stu-id="9284c-214">Maximum of 30 MB per post to Log Analytics Data Collector API.</span></span> <span data-ttu-id="9284c-215">이는 단일 게시물에 대한 크기 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-215">This is a size limit for a single post.</span></span> <span data-ttu-id="9284c-216">단일 게시물의 데이터가 30MB를 초과하는 경우 보다 작은 크기의 청크로 분할하여 동시에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-216">If the data from a single post that exceeds 30 MB, you should split the data up to smaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="9284c-217">최대 32KB의 필드 값 제한.</span><span class="sxs-lookup"><span data-stu-id="9284c-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="9284c-218">필드 값이 32KB보다 크면 데이터가 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-218">If the field value is greater than 32 KB, the data will be truncated.</span></span>
* <span data-ttu-id="9284c-219">지정된 형식의 권장되는 최대 필드 수는 50개입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="9284c-220">이는 사용 편의성 및 검색 환경 관점에서의 실용적인 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="9284c-221">반환 코드</span><span class="sxs-lookup"><span data-stu-id="9284c-221">Return codes</span></span>
<span data-ttu-id="9284c-222">HTTP 상태 코드 200는 처리를 위한 요청을 받았다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-222">The HTTP status code 200 means that the request has been received for processing.</span></span> <span data-ttu-id="9284c-223">이 항목은 작업이 성공적으로 완료되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-223">This indicates that the operation completed successfully.</span></span>

<span data-ttu-id="9284c-224">이 표는 서비스에서 반환할 수 있는 전체 상태 코드 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-224">This table lists the complete set of status codes that the service might return:</span></span>

| <span data-ttu-id="9284c-225">코드</span><span class="sxs-lookup"><span data-stu-id="9284c-225">Code</span></span> | <span data-ttu-id="9284c-226">가동 상태</span><span class="sxs-lookup"><span data-stu-id="9284c-226">Status</span></span> | <span data-ttu-id="9284c-227">오류 코드</span><span class="sxs-lookup"><span data-stu-id="9284c-227">Error code</span></span> | <span data-ttu-id="9284c-228">설명</span><span class="sxs-lookup"><span data-stu-id="9284c-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9284c-229">200</span><span class="sxs-lookup"><span data-stu-id="9284c-229">200</span></span> |<span data-ttu-id="9284c-230">확인</span><span class="sxs-lookup"><span data-stu-id="9284c-230">OK</span></span> | |<span data-ttu-id="9284c-231">요청이 성공적으로 수락되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-231">The request was successfully accepted.</span></span> |
| <span data-ttu-id="9284c-232">400</span><span class="sxs-lookup"><span data-stu-id="9284c-232">400</span></span> |<span data-ttu-id="9284c-233">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-233">Bad request</span></span> |<span data-ttu-id="9284c-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="9284c-234">InactiveCustomer</span></span> |<span data-ttu-id="9284c-235">작업 영역이 닫혔습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-235">The workspace has been closed.</span></span> |
| <span data-ttu-id="9284c-236">400</span><span class="sxs-lookup"><span data-stu-id="9284c-236">400</span></span> |<span data-ttu-id="9284c-237">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-237">Bad request</span></span> |<span data-ttu-id="9284c-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="9284c-238">InvalidApiVersion</span></span> |<span data-ttu-id="9284c-239">지정한 API 버전이 서비스에서 인식되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-239">The API version that you specified was not recognized by the service.</span></span> |
| <span data-ttu-id="9284c-240">400</span><span class="sxs-lookup"><span data-stu-id="9284c-240">400</span></span> |<span data-ttu-id="9284c-241">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-241">Bad request</span></span> |<span data-ttu-id="9284c-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="9284c-242">InvalidCustomerId</span></span> |<span data-ttu-id="9284c-243">지정된 작업 영역 ID가 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-243">The workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="9284c-244">400</span><span class="sxs-lookup"><span data-stu-id="9284c-244">400</span></span> |<span data-ttu-id="9284c-245">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-245">Bad request</span></span> |<span data-ttu-id="9284c-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="9284c-246">InvalidDataFormat</span></span> |<span data-ttu-id="9284c-247">잘못된 JSON이 제출되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="9284c-248">응답 본문에 오류 해결 방법에 관한 추가 정보가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-248">The response body might contain more information about how to resolve the error.</span></span> |
| <span data-ttu-id="9284c-249">400</span><span class="sxs-lookup"><span data-stu-id="9284c-249">400</span></span> |<span data-ttu-id="9284c-250">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-250">Bad request</span></span> |<span data-ttu-id="9284c-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="9284c-251">InvalidLogType</span></span> |<span data-ttu-id="9284c-252">지정한 로그 형식이 특수 문자나 숫자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-252">The log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="9284c-253">400</span><span class="sxs-lookup"><span data-stu-id="9284c-253">400</span></span> |<span data-ttu-id="9284c-254">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-254">Bad request</span></span> |<span data-ttu-id="9284c-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="9284c-255">MissingApiVersion</span></span> |<span data-ttu-id="9284c-256">API 버전을 지정하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-256">The API version wasn’t specified.</span></span> |
| <span data-ttu-id="9284c-257">400</span><span class="sxs-lookup"><span data-stu-id="9284c-257">400</span></span> |<span data-ttu-id="9284c-258">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-258">Bad request</span></span> |<span data-ttu-id="9284c-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="9284c-259">MissingContentType</span></span> |<span data-ttu-id="9284c-260">콘텐츠 형식을 지정하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-260">The content type wasn’t specified.</span></span> |
| <span data-ttu-id="9284c-261">400</span><span class="sxs-lookup"><span data-stu-id="9284c-261">400</span></span> |<span data-ttu-id="9284c-262">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-262">Bad request</span></span> |<span data-ttu-id="9284c-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="9284c-263">MissingLogType</span></span> |<span data-ttu-id="9284c-264">필요한 값 로그 형식을 지정하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-264">The required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="9284c-265">400</span><span class="sxs-lookup"><span data-stu-id="9284c-265">400</span></span> |<span data-ttu-id="9284c-266">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-266">Bad request</span></span> |<span data-ttu-id="9284c-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="9284c-267">UnsupportedContentType</span></span> |<span data-ttu-id="9284c-268">콘텐츠 형식이 **application/json**으로 설정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-268">The content type was not set to **application/json**.</span></span> |
| <span data-ttu-id="9284c-269">403</span><span class="sxs-lookup"><span data-stu-id="9284c-269">403</span></span> |<span data-ttu-id="9284c-270">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="9284c-270">Forbidden</span></span> |<span data-ttu-id="9284c-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="9284c-271">InvalidAuthorization</span></span> |<span data-ttu-id="9284c-272">서비스가 요청을 인증하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-272">The service failed to authenticate the request.</span></span> <span data-ttu-id="9284c-273">작업 영역 ID 및 연결 키가 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-273">Verify that the workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="9284c-274">404</span><span class="sxs-lookup"><span data-stu-id="9284c-274">404</span></span> |<span data-ttu-id="9284c-275">찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="9284c-275">Not Found</span></span> | | <span data-ttu-id="9284c-276">제공된 URL이 잘못되었거나 요청이 너무 큽니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-276">Either the URL provided is incorrect, or the request is too large.</span></span> |
| <span data-ttu-id="9284c-277">429</span><span class="sxs-lookup"><span data-stu-id="9284c-277">429</span></span> |<span data-ttu-id="9284c-278">너무 많은 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-278">Too Many Requests</span></span> | | <span data-ttu-id="9284c-279">서비스 계정에서 많은 양의 데이터가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-279">The service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="9284c-280">요청을 나중에 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="9284c-280">Please retry the request later.</span></span> |
| <span data-ttu-id="9284c-281">500</span><span class="sxs-lookup"><span data-stu-id="9284c-281">500</span></span> |<span data-ttu-id="9284c-282">내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="9284c-282">Internal Server Error</span></span> |<span data-ttu-id="9284c-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="9284c-283">UnspecifiedError</span></span> |<span data-ttu-id="9284c-284">서비스에 내부 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-284">The service encountered an internal error.</span></span> <span data-ttu-id="9284c-285">요청을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="9284c-285">Please retry the request.</span></span> |
| <span data-ttu-id="9284c-286">503</span><span class="sxs-lookup"><span data-stu-id="9284c-286">503</span></span> |<span data-ttu-id="9284c-287">서비스를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="9284c-287">Service Unavailable</span></span> |<span data-ttu-id="9284c-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="9284c-288">ServiceUnavailable</span></span> |<span data-ttu-id="9284c-289">현재 서비스가 요청을 받을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-289">The service currently is unavailable to receive requests.</span></span> <span data-ttu-id="9284c-290">요청을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="9284c-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="9284c-291">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="9284c-291">Query data</span></span>
<span data-ttu-id="9284c-292">Log Analytics HTTP 데이터 수집기 API에서 제출한 데이터를 쿼리하려면 지정한 **LogType** 값에 **_CL**을 첨부한 것과 같은 **형식**의 레코드를 검색하십시오.</span><span class="sxs-lookup"><span data-stu-id="9284c-292">To query data submitted by the Log Analytics HTTP Data Collector API, search for records with **Type** that is equal to the **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="9284c-293">예를 들어, **MyCustomLog**를 사용한 경우**Type=MyCustomLog_CL**을 갖는 모든 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="9284c-294">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 위 쿼리가 다음과 같이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-294">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="9284c-295">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="9284c-295">Sample requests</span></span>
<span data-ttu-id="9284c-296">다음 섹션에서는 다양한 프로그래밍 언어를 사용하여 Log Analytics HTTP 데이터 수집기에 데이터를 제출하는 방법의 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-296">In the next sections, you'll find samples of how to submit data to the Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="9284c-297">각각의 샘플에서 다음 절차를 통해 권한 부여 헤더에 대한 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-297">For each sample, do these steps to set the variables for the authorization header:</span></span>

1. <span data-ttu-id="9284c-298">Operations Management Suite 포털에서 **설정** 타일을 선택하고 **연결 원본** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-298">In the Operations Management Suite portal, select the **Settings** tile, and then select the **Connected Sources** tab.</span></span>
2. <span data-ttu-id="9284c-299">**작업 영역 ID** 오른쪽에서 복사 아이콘을 선택한 다음 이 ID를 **고객 ID** 변수의 값으로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-299">To the right of **Workspace ID**, select the copy icon, and then paste the ID as the value of the **Customer ID** variable.</span></span>
3. <span data-ttu-id="9284c-300">**기본 키** 오른쪽에서 복사 아이콘을 선택한 다음 이 ID를 **공유 키** 변수의 값으로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-300">To the right of **Primary Key**, select the copy icon, and then paste the ID as the value of the **Shared Key** variable.</span></span>

<span data-ttu-id="9284c-301">또는 로그 형식 및 JSON 데이터에 대한 변수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-301">Alternatively, you can change the variables for the log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="9284c-302">PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="9284c-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify the name of the record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with the created time for the records
$TimeStampField = "DateValue"


# Create two records with the same set of properties to create
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create the function to create the authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create the function to create and post the request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit the data to the API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="9284c-303">C# 샘플</span><span class="sxs-lookup"><span data-stu-id="9284c-303">C# sample</span></span>
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId to your Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either the primary or the secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of the event type that is being submitted to Log Analytics
        static string LogName = "DemoExample";

        // You can use an optional field to specify the timestamp from the data. If the time field is not specified, Log Analytics assumes the time is the message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for the API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build the API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request to the POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a><span data-ttu-id="9284c-304">Python 샘플</span><span class="sxs-lookup"><span data-stu-id="9284c-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update the customer ID to your Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For the shared key, use either the primary or the secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# The log type is the name of the event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build the API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request to the POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a><span data-ttu-id="9284c-305">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9284c-305">Next steps</span></span>
- <span data-ttu-id="9284c-306">Log Analytics 저장소에서 데이터를 검색하려면 [Log Search API](log-analytics-log-search-api.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9284c-306">Use the [Log Search API](log-analytics-log-search-api.md) to retrieve data from the Log Analytics repository.</span></span>
