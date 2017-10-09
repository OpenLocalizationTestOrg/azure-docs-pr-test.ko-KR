---
title: "분석 HTTP 데이터 수집기 API aaaLog | Microsoft Docs"
description: "Hello 로그 분석 HTTP 데이터 수집기 API tooadd POST JSON 데이터 toohello 로그 분석 저장소 hello REST API를 호출할 수 있는 모든 클라이언트에서 사용할 수 있습니다. 이 문서에서는 설명 방법을 toouse API hello 방법의 예제는 다양 한 프로그래밍 언어를 사용 하 여 toopublish 데이터입니다."
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
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a><span data-ttu-id="3956e-104">데이터 수집기 API HTTP hello로 데이터 tooLog 분석 보내기</span><span class="sxs-lookup"><span data-stu-id="3956e-104">Send data tooLog Analytics with hello HTTP Data Collector API</span></span>
<span data-ttu-id="3956e-105">이 문서에서는 toouse REST API 클라이언트에서 HTTP 데이터 수집기 API toosend 데이터 tooLog 분석 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-105">This article shows you how toouse hello HTTP Data Collector API toosend data tooLog Analytics from a REST API client.</span></span>  <span data-ttu-id="3956e-106">스크립트나 응용 프로그램에 의해 수집 된 tooformat 데이터는 요청에 포함 하 고 로그 분석의 승인을 요청 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-106">It describes how tooformat data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="3956e-107">PowerShell, C# 및 Python에 예가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="3956e-108">개념</span><span class="sxs-lookup"><span data-stu-id="3956e-108">Concepts</span></span>
<span data-ttu-id="3956e-109">REST API를 호출할 수 있는 모든 클라이언트에서 hello HTTP 데이터 수집기 API toosend 데이터 tooLog 분석을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-109">You can use hello HTTP Data Collector API toosend data tooLog Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="3956e-110">이 runbook을 수 있습니다 관리에서 수집 하는 Azure 자동화에서 데이터에서 Azure 또는 다른 클라우드 또는 것 수 tooconsolidate 로그 분석을 사용 하는 다른 관리 시스템 하며 데이터를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics tooconsolidate and analyze data.</span></span>

<span data-ttu-id="3956e-111">Hello 로그 분석 저장소의 모든 데이터는 특정 레코드 종류를 사용 하 여 레코드로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-111">All data in hello Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="3956e-112">JSON의 여러 레코드도 데이터 toosend toohello HTTP 데이터 수집기 API를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-112">You format your data toosend toohello HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="3956e-113">Hello 데이터를 전송할 때 개별 레코드 hello 요청 페이로드의 각 레코드에 대 한 hello 리포지토리에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-113">When you submit hello data, an individual record is created in hello repository for each record in hello request payload.</span></span>


![HTTP 데이터 수집기 개요](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="3956e-115">요청 만들기</span><span class="sxs-lookup"><span data-stu-id="3956e-115">Create a request</span></span>
<span data-ttu-id="3956e-116">toouse hello HTTP 데이터 수집기 API hello 데이터 toosend에서 개체 JSON (JavaScript Notation)을 포함 하는 POST 요청을 만들 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-116">toouse hello HTTP Data Collector API, you create a POST request that includes hello data toosend in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="3956e-117">각 요청에 필요한 다음 세 개의 테이블 목록 hello 특성 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-117">hello next three tables list hello attributes that are required for each request.</span></span> <span data-ttu-id="3956e-118">각 특성 hello 문서의 뒷부분에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-118">We describe each attribute in more detail later in hello article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="3956e-119">요청 URI</span><span class="sxs-lookup"><span data-stu-id="3956e-119">Request URI</span></span>
| <span data-ttu-id="3956e-120">특성</span><span class="sxs-lookup"><span data-stu-id="3956e-120">Attribute</span></span> | <span data-ttu-id="3956e-121">속성</span><span class="sxs-lookup"><span data-stu-id="3956e-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="3956e-122">메서드</span><span class="sxs-lookup"><span data-stu-id="3956e-122">Method</span></span> |<span data-ttu-id="3956e-123">POST</span><span class="sxs-lookup"><span data-stu-id="3956e-123">POST</span></span> |
| <span data-ttu-id="3956e-124">URI</span><span class="sxs-lookup"><span data-stu-id="3956e-124">URI</span></span> |<span data-ttu-id="3956e-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="3956e-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="3956e-126">콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="3956e-126">Content type</span></span> |<span data-ttu-id="3956e-127">application/json</span><span class="sxs-lookup"><span data-stu-id="3956e-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="3956e-128">URI 매개 변수 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-128">Request URI parameters</span></span>
| <span data-ttu-id="3956e-129">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3956e-129">Parameter</span></span> | <span data-ttu-id="3956e-130">설명</span><span class="sxs-lookup"><span data-stu-id="3956e-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3956e-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="3956e-131">CustomerID</span></span> |<span data-ttu-id="3956e-132">hello hello Microsoft Operations Management Suite 작업 영역에 대 한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-132">hello unique identifier for hello Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="3956e-133">리소스</span><span class="sxs-lookup"><span data-stu-id="3956e-133">Resource</span></span> |<span data-ttu-id="3956e-134">hello API 리소스 이름: / api/로그입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-134">hello API resource name: /api/logs.</span></span> |
| <span data-ttu-id="3956e-135">API 버전</span><span class="sxs-lookup"><span data-stu-id="3956e-135">API Version</span></span> |<span data-ttu-id="3956e-136">이 요청으로 hello API toouse의 hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-136">hello version of hello API toouse with this request.</span></span> <span data-ttu-id="3956e-137">현재 2016-04-01입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3956e-138">헤더 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-138">Request headers</span></span>
| <span data-ttu-id="3956e-139">헤더</span><span class="sxs-lookup"><span data-stu-id="3956e-139">Header</span></span> | <span data-ttu-id="3956e-140">설명</span><span class="sxs-lookup"><span data-stu-id="3956e-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3956e-141">권한 부여</span><span class="sxs-lookup"><span data-stu-id="3956e-141">Authorization</span></span> |<span data-ttu-id="3956e-142">hello 권한 부여 서명입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-142">hello authorization signature.</span></span> <span data-ttu-id="3956e-143">Hello 문서의 뒷부분에 나오는 방법에 대 한 읽을 수 있습니다는 hmac-sha256 toocreate 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-143">Later in hello article, you can read about how toocreate an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="3956e-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="3956e-144">Log-Type</span></span> |<span data-ttu-id="3956e-145">전송 하는 hello 데이터의 hello 레코드 종류를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-145">Specify hello record type of hello data that is being submitted.</span></span> <span data-ttu-id="3956e-146">현재 hello 로그 형식은 영숫자 문자로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-146">Currently, hello log type supports only alpha characters.</span></span> <span data-ttu-id="3956e-147">숫자 또는 특수 문자는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="3956e-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="3956e-148">x-ms-date</span></span> |<span data-ttu-id="3956e-149">hello 날짜 RFC 1123 형식으로 해당 hello 요청이 처리 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-149">hello date that hello request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="3956e-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="3956e-150">time-generated-field</span></span> |<span data-ttu-id="3956e-151">hello 데이터 항목의 hello 타임 스탬프를 포함 하는 hello 데이터에 있는 필드의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-151">hello name of a field in hello data that contains hello timestamp of hello data item.</span></span> <span data-ttu-id="3956e-152">필드를 지정하면 그 내용이 **TimeGenerated**에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="3956e-153">이 필드를 지정 하지 않으면 hello에 대 한 기본 **TimeGenerated** hello 시간에는 해당 hello 메시지는 수집 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-153">If this field isn’t specified, hello default for **TimeGenerated** is hello time that hello message is ingested.</span></span> <span data-ttu-id="3956e-154">hello 메시지 필드의 내용을 hello hello ISO 8601 형식 따라야 합니다.-m M-DDThh:mm:ssZ 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-154">hello contents of hello message field should follow hello ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="3956e-155">권한 부여</span><span class="sxs-lookup"><span data-stu-id="3956e-155">Authorization</span></span>
<span data-ttu-id="3956e-156">모든 요청 toohello 로그 분석 데이터 수집기 API HTTP 권한 부여 헤더를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-156">Any request toohello Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="3956e-157">요청을 tooauthenticate 주 hello 또는 hello hello 요청을 수행 하는 hello 작업 영역에 대 한 보조 키 중 하나를 사용 하 여 hello 요청에 서명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-157">tooauthenticate a request, you must sign hello request with either hello primary or hello secondary key for hello workspace that is making hello request.</span></span> <span data-ttu-id="3956e-158">그런 다음 해당 서명 hello 요청의 일부분으로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-158">Then, pass that signature as part of hello request.</span></span>   

<span data-ttu-id="3956e-159">다음은 hello 권한 부여 헤더에 대 한 hello 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-159">Here's hello format for hello authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="3956e-160">*WorkspaceID* hello hello Operations Management Suite 작업 영역에 대 한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-160">*WorkspaceID* is hello unique identifier for hello Operations Management Suite workspace.</span></span> <span data-ttu-id="3956e-161">*서명* 는 [HMAC 해시 기반 메시지 인증 코드 ()](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) 있는 hello 요청에서 구현 되 고 다음 hello를 사용 하 여 계산 [SHA256 알고리즘](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from hello request and then computed by using hello [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="3956e-162">그런 다음 Base64 인코딩을 사용하여 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="3956e-163">이 형식 tooencode hello를 사용 하 여 **에서 SharedKey** 서명 문자열:</span><span class="sxs-lookup"><span data-stu-id="3956e-163">Use this format tooencode hello **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="3956e-164">서명 문자열의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="3956e-165">Hello 서명 문자열을 사용 하 여 인코딩할를 보유 하는 경우 hello u t F-8로 인코딩된 문자열에서 hmac-sha256 알고리즘 hello 하 고 Base64 hello 결과 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="3956e-165">When you have hello signature string, encode it by using hello HMAC-SHA256 algorithm on hello UTF-8-encoded string, and then encode hello result as Base64.</span></span> <span data-ttu-id="3956e-166">이 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="3956e-167">hello 샘플 hello 다음 섹션의 샘플 코드 toohelp 권한 부여 헤더를 만들 수 있으며</span><span class="sxs-lookup"><span data-stu-id="3956e-167">hello samples in hello next sections have sample code toohelp you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="3956e-168">요청 본문</span><span class="sxs-lookup"><span data-stu-id="3956e-168">Request body</span></span>
<span data-ttu-id="3956e-169">hello hello 메시지 본문은 JSON에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-169">hello body of hello message must be in JSON.</span></span> <span data-ttu-id="3956e-170">이 형식으로 hello 속성 이름 및 값 쌍이 있는 레코드를 하나 이상 포함 되어야.</span><span class="sxs-lookup"><span data-stu-id="3956e-170">It must include one or more records with hello property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="3956e-171">형식에 따라 hello를 사용 하 여 단일 요청에서 함께 여러 레코드를 일괄 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-171">You can batch multiple records together in a single request by using hello following format.</span></span> <span data-ttu-id="3956e-172">모든 hello 레코드 hello 여야 합니다. 동일한 레코드 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-172">All hello records must be hello same record type.</span></span>

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

## <a name="record-type-and-properties"></a><span data-ttu-id="3956e-173">레코드 유형 및 속성</span><span class="sxs-lookup"><span data-stu-id="3956e-173">Record type and properties</span></span>
<span data-ttu-id="3956e-174">Hello 로그 분석 HTTP 데이터 수집기 API를 통해 데이터를 전송할 때에 사용자 지정 레코드 종류를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-174">You define a custom record type when you submit data through hello Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="3956e-175">현재, 다른 데이터 형식 및 솔루션에 의해 생성 된 레코드 종류 tooexisting 데이터를 쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-175">Currently, you can't write data tooexisting record types that were created by other data types and solutions.</span></span> <span data-ttu-id="3956e-176">로그 분석 hello 들어오는 데이터를 읽고 하 한 다음 입력 한 hello 값의 hello 데이터 형식과 일치 하는 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-176">Log Analytics reads hello incoming data and then creates properties that match hello data types of hello values that you enter.</span></span>

<span data-ttu-id="3956e-177">로그 분석 API를 포함 해야 하는 각 요청 toohello는 **로그 유형** hello 레코드 종류에 대 한 hello 이름 가진 헤더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-177">Each request toohello Log Analytics API must include a **Log-Type** header with hello name for hello record type.</span></span> <span data-ttu-id="3956e-178">hello 접미사 **_CL** toodistinguish 다른 로그에서 사용자 지정 로그도 형식을 입력 하면 자동으로 추가 된 toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-178">hello suffix **_CL** is automatically appended toohello name you enter toodistinguish it from other log types as a custom log.</span></span> <span data-ttu-id="3956e-179">예를 들어, hello 이름을 입력 하면 **MyNewRecordType**, 로그 분석 hello 형식을 가진 레코드를 만듭니다. **MyNewRecordType_CL**합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-179">For example, if you enter hello name **MyNewRecordType**, Log Analytics creates a record with hello type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="3956e-180">이렇게 하면 사용자가 만든 형식 이름과 Microsoft가 현재 또는 향후에 포함한 이름 사이의 충돌을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="3956e-181">tooidentify 속성의 데이터 형식, 로그 분석 접미사 toohello 속성 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-181">tooidentify a property's data type, Log Analytics adds a suffix toohello property name.</span></span> <span data-ttu-id="3956e-182">속성에 null 값이 있으면 hello 속성 해당 레코드에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-182">If a property contains a null value, hello property is not included in that record.</span></span> <span data-ttu-id="3956e-183">이 표에서 hello 속성 데이터 형식 및 해당 접미사를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-183">This table lists hello property data type and corresponding suffix:</span></span>

| <span data-ttu-id="3956e-184">속성 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="3956e-184">Property data type</span></span> | <span data-ttu-id="3956e-185">접미사</span><span class="sxs-lookup"><span data-stu-id="3956e-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="3956e-186">문자열</span><span class="sxs-lookup"><span data-stu-id="3956e-186">String</span></span> |<span data-ttu-id="3956e-187">_s</span><span class="sxs-lookup"><span data-stu-id="3956e-187">_s</span></span> |
| <span data-ttu-id="3956e-188">Boolean</span><span class="sxs-lookup"><span data-stu-id="3956e-188">Boolean</span></span> |<span data-ttu-id="3956e-189">_b</span><span class="sxs-lookup"><span data-stu-id="3956e-189">_b</span></span> |
| <span data-ttu-id="3956e-190">Double</span><span class="sxs-lookup"><span data-stu-id="3956e-190">Double</span></span> |<span data-ttu-id="3956e-191">_d</span><span class="sxs-lookup"><span data-stu-id="3956e-191">_d</span></span> |
| <span data-ttu-id="3956e-192">날짜/시간</span><span class="sxs-lookup"><span data-stu-id="3956e-192">Date/time</span></span> |<span data-ttu-id="3956e-193">_t</span><span class="sxs-lookup"><span data-stu-id="3956e-193">_t</span></span> |
| <span data-ttu-id="3956e-194">GUID</span><span class="sxs-lookup"><span data-stu-id="3956e-194">GUID</span></span> |<span data-ttu-id="3956e-195">_g</span><span class="sxs-lookup"><span data-stu-id="3956e-195">_g</span></span> |

<span data-ttu-id="3956e-196">각 속성에 대 한 로그 분석을 사용 하는 hello 데이터 형식을 hello 레코드 종류 hello 새 레코드에 대해 이미 존재 하는지 여부에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-196">hello data type that Log Analytics uses for each property depends on whether hello record type for hello new record already exists.</span></span>

* <span data-ttu-id="3956e-197">로그 분석 hello 레코드 종류가 없는 경우 새 브러시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-197">If hello record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="3956e-198">로그 분석 hello 새 레코드에 대 한 각 속성에 대 한 hello JSON 형식 유추 toodetermine hello 데이터 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-198">Log Analytics uses hello JSON type inference toodetermine hello data type for each property for hello new record.</span></span>
* <span data-ttu-id="3956e-199">Hello 레코드 종류가 있으면 로그 분석 toocreate 기존 속성에 따라 새 레코드를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-199">If hello record type does exist, Log Analytics attempts toocreate a new record based on existing properties.</span></span> <span data-ttu-id="3956e-200">Hello hello 새 레코드의 속성에 대 한 데이터 형식 및 하지 않는 경우 일치 하 고 없습니다 기존 형식, 변환 된 toohello 수 경우 hello 존재 하지 않는 속성을 포함 하는 레코드, 로그 분석의 새 속성을 만들고 hello 관련 접미사를 포함 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-200">If hello data type for a property in hello new record doesn’t match and can’t be converted toohello existing type, or if hello record includes a property that doesn’t exist, Log Analytics creates a new property that has hello relevant suffix.</span></span>

<span data-ttu-id="3956e-201">예를 들어, 이 제출 항목은 **number_d**, **boolean_b**, **string_s** 등의 세 가지 속성이 있는 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![샘플 레코드 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="3956e-203">다음 문자열 형식으로 지정 하는 모든 값이 다음 항목을 제출 하는 경우에 hello 속성 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-203">If you then submitted this next entry, with all values formatted as strings, hello properties would not change.</span></span> <span data-ttu-id="3956e-204">이러한 값에 변환 된 tooexisting 데이터 형식이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-204">These values can be converted tooexisting data types:</span></span>

![샘플 레코드 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="3956e-206">하지만 그런 다음이 다음 전송을 수행한 경우 로그 분석은 hello 새 속성을 만들 **boolean_d** 및 **string_d**합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-206">But, if you then made this next submission, Log Analytics would create hello new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="3956e-207">이 값은 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-207">These values can't be converted:</span></span>

![샘플 레코드 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="3956e-209">로그 분석은 세 가지 속성 사용 레코드를 만듭니다 hello hello 레코드 종류를 만들기 전에 항목을 다음에 다음 제출 **number_s**, **boolean_s**, 및 **string_s**.</span><span class="sxs-lookup"><span data-stu-id="3956e-209">If you then submitted hello following entry, before hello record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="3956e-210">이 항목에서 문자열로 형식이 각 hello 초기 값:</span><span class="sxs-lookup"><span data-stu-id="3956e-210">In this entry, each of hello initial values is formatted as a string:</span></span>

![샘플 레코드 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="3956e-212">데이터 제한</span><span class="sxs-lookup"><span data-stu-id="3956e-212">Data limits</span></span>
<span data-ttu-id="3956e-213">로그 분석 데이터 컬렉션 API toohello 게시 hello 데이터에 대 한 몇 가지 제약 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-213">There are some constraints around hello data posted toohello Log Analytics Data collection API.</span></span>

* <span data-ttu-id="3956e-214">30MB post tooLog 분석 데이터 수집기 API 당 최대입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-214">Maximum of 30 MB per post tooLog Analytics Data Collector API.</span></span> <span data-ttu-id="3956e-215">이는 단일 게시물에 대한 크기 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-215">This is a size limit for a single post.</span></span> <span data-ttu-id="3956e-216">경우 30 MB를 초과 하는 단일 게시에서 hello 데이터를 분할 해야 hello 데이터 크기의 toosmaller 분할 하 고 동시에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-216">If hello data from a single post that exceeds 30 MB, you should split hello data up toosmaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="3956e-217">최대 32KB의 필드 값 제한.</span><span class="sxs-lookup"><span data-stu-id="3956e-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="3956e-218">Hello 필드 값 32KB 보다 클 경우 hello 데이터가 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-218">If hello field value is greater than 32 KB, hello data will be truncated.</span></span>
* <span data-ttu-id="3956e-219">지정된 형식의 권장되는 최대 필드 수는 50개입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="3956e-220">이는 사용 편의성 및 검색 환경 관점에서의 실용적인 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="3956e-221">반환 코드</span><span class="sxs-lookup"><span data-stu-id="3956e-221">Return codes</span></span>
<span data-ttu-id="3956e-222">HTTP 상태 코드 200 hello 처리를 위해 해당 hello 요청을 수신 했음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-222">hello HTTP status code 200 means that hello request has been received for processing.</span></span> <span data-ttu-id="3956e-223">이 hello 작업이 성공적으로 완료를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-223">This indicates that hello operation completed successfully.</span></span>

<span data-ttu-id="3956e-224">이 표에서 hello hello 서비스를 반환할 수 있는 상태 코드의 전체 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-224">This table lists hello complete set of status codes that hello service might return:</span></span>

| <span data-ttu-id="3956e-225">코드</span><span class="sxs-lookup"><span data-stu-id="3956e-225">Code</span></span> | <span data-ttu-id="3956e-226">가동 상태</span><span class="sxs-lookup"><span data-stu-id="3956e-226">Status</span></span> | <span data-ttu-id="3956e-227">오류 코드</span><span class="sxs-lookup"><span data-stu-id="3956e-227">Error code</span></span> | <span data-ttu-id="3956e-228">설명</span><span class="sxs-lookup"><span data-stu-id="3956e-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3956e-229">200</span><span class="sxs-lookup"><span data-stu-id="3956e-229">200</span></span> |<span data-ttu-id="3956e-230">확인</span><span class="sxs-lookup"><span data-stu-id="3956e-230">OK</span></span> | |<span data-ttu-id="3956e-231">hello 요청이 성공적으로 수락 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-231">hello request was successfully accepted.</span></span> |
| <span data-ttu-id="3956e-232">400</span><span class="sxs-lookup"><span data-stu-id="3956e-232">400</span></span> |<span data-ttu-id="3956e-233">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-233">Bad request</span></span> |<span data-ttu-id="3956e-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="3956e-234">InactiveCustomer</span></span> |<span data-ttu-id="3956e-235">작업 영역 hello 종료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-235">hello workspace has been closed.</span></span> |
| <span data-ttu-id="3956e-236">400</span><span class="sxs-lookup"><span data-stu-id="3956e-236">400</span></span> |<span data-ttu-id="3956e-237">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-237">Bad request</span></span> |<span data-ttu-id="3956e-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="3956e-238">InvalidApiVersion</span></span> |<span data-ttu-id="3956e-239">지정한 hello API 버전 hello 서비스에서 인식할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-239">hello API version that you specified was not recognized by hello service.</span></span> |
| <span data-ttu-id="3956e-240">400</span><span class="sxs-lookup"><span data-stu-id="3956e-240">400</span></span> |<span data-ttu-id="3956e-241">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-241">Bad request</span></span> |<span data-ttu-id="3956e-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="3956e-242">InvalidCustomerId</span></span> |<span data-ttu-id="3956e-243">지정 된 hello 작업 영역 ID 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-243">hello workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="3956e-244">400</span><span class="sxs-lookup"><span data-stu-id="3956e-244">400</span></span> |<span data-ttu-id="3956e-245">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-245">Bad request</span></span> |<span data-ttu-id="3956e-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="3956e-246">InvalidDataFormat</span></span> |<span data-ttu-id="3956e-247">잘못된 JSON이 제출되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="3956e-248">hello 응답 본문 tooresolve 오류 hello 하는 방법에 대 한 자세한 내용은 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-248">hello response body might contain more information about how tooresolve hello error.</span></span> |
| <span data-ttu-id="3956e-249">400</span><span class="sxs-lookup"><span data-stu-id="3956e-249">400</span></span> |<span data-ttu-id="3956e-250">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-250">Bad request</span></span> |<span data-ttu-id="3956e-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="3956e-251">InvalidLogType</span></span> |<span data-ttu-id="3956e-252">hello 로그 형식이 포함 된 특수 문자 또는 숫자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-252">hello log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="3956e-253">400</span><span class="sxs-lookup"><span data-stu-id="3956e-253">400</span></span> |<span data-ttu-id="3956e-254">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-254">Bad request</span></span> |<span data-ttu-id="3956e-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="3956e-255">MissingApiVersion</span></span> |<span data-ttu-id="3956e-256">hello API 버전이 지정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-256">hello API version wasn’t specified.</span></span> |
| <span data-ttu-id="3956e-257">400</span><span class="sxs-lookup"><span data-stu-id="3956e-257">400</span></span> |<span data-ttu-id="3956e-258">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-258">Bad request</span></span> |<span data-ttu-id="3956e-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="3956e-259">MissingContentType</span></span> |<span data-ttu-id="3956e-260">hello 콘텐츠 형식이 지정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-260">hello content type wasn’t specified.</span></span> |
| <span data-ttu-id="3956e-261">400</span><span class="sxs-lookup"><span data-stu-id="3956e-261">400</span></span> |<span data-ttu-id="3956e-262">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-262">Bad request</span></span> |<span data-ttu-id="3956e-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="3956e-263">MissingLogType</span></span> |<span data-ttu-id="3956e-264">hello 값 로그 형식이 지정 되지 않은 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-264">hello required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="3956e-265">400</span><span class="sxs-lookup"><span data-stu-id="3956e-265">400</span></span> |<span data-ttu-id="3956e-266">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-266">Bad request</span></span> |<span data-ttu-id="3956e-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="3956e-267">UnsupportedContentType</span></span> |<span data-ttu-id="3956e-268">hello 콘텐츠 형식이 너무 설정 되지 않았습니다.**응용 프로그램/json**합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-268">hello content type was not set too**application/json**.</span></span> |
| <span data-ttu-id="3956e-269">403</span><span class="sxs-lookup"><span data-stu-id="3956e-269">403</span></span> |<span data-ttu-id="3956e-270">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="3956e-270">Forbidden</span></span> |<span data-ttu-id="3956e-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="3956e-271">InvalidAuthorization</span></span> |<span data-ttu-id="3956e-272">hello 서비스 tooauthenticate hello 요청을 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-272">hello service failed tooauthenticate hello request.</span></span> <span data-ttu-id="3956e-273">해당 hello 작업 영역 ID 및 연결 키 올바른지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3956e-273">Verify that hello workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="3956e-274">404</span><span class="sxs-lookup"><span data-stu-id="3956e-274">404</span></span> |<span data-ttu-id="3956e-275">찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="3956e-275">Not Found</span></span> | | <span data-ttu-id="3956e-276">제공 된 hello URL 잘못 되었거나 hello 요청이 너무 많습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-276">Either hello URL provided is incorrect, or hello request is too large.</span></span> |
| <span data-ttu-id="3956e-277">429</span><span class="sxs-lookup"><span data-stu-id="3956e-277">429</span></span> |<span data-ttu-id="3956e-278">너무 많은 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-278">Too Many Requests</span></span> | | <span data-ttu-id="3956e-279">hello 서비스 계정에서 데이터 양이 많기 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-279">hello service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="3956e-280">Hello 요청을 나중에 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3956e-280">Please retry hello request later.</span></span> |
| <span data-ttu-id="3956e-281">500</span><span class="sxs-lookup"><span data-stu-id="3956e-281">500</span></span> |<span data-ttu-id="3956e-282">내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="3956e-282">Internal Server Error</span></span> |<span data-ttu-id="3956e-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="3956e-283">UnspecifiedError</span></span> |<span data-ttu-id="3956e-284">hello 서비스 내부 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-284">hello service encountered an internal error.</span></span> <span data-ttu-id="3956e-285">Hello 요청을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3956e-285">Please retry hello request.</span></span> |
| <span data-ttu-id="3956e-286">503</span><span class="sxs-lookup"><span data-stu-id="3956e-286">503</span></span> |<span data-ttu-id="3956e-287">서비스를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="3956e-287">Service Unavailable</span></span> |<span data-ttu-id="3956e-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="3956e-288">ServiceUnavailable</span></span> |<span data-ttu-id="3956e-289">hello 서비스는 현재 사용할 수 없는 tooreceive 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-289">hello service currently is unavailable tooreceive requests.</span></span> <span data-ttu-id="3956e-290">요청을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="3956e-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="3956e-291">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="3956e-291">Query data</span></span>
<span data-ttu-id="3956e-292">로그 분석 HTTP 데이터 수집기 API, 검색 된 레코드에 대 한 hello 제출한 tooquery 데이터 **형식** 같은 toohello 즉 **LogType** 추가 되므로 사용자가 지정한 값 **_CL**.</span><span class="sxs-lookup"><span data-stu-id="3956e-292">tooquery data submitted by hello Log Analytics HTTP Data Collector API, search for records with **Type** that is equal toohello **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="3956e-293">예를 들어, **MyCustomLog**를 사용한 경우**Type=MyCustomLog_CL**을 갖는 모든 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="3956e-294">작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-294">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="3956e-295">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="3956e-295">Sample requests</span></span>
<span data-ttu-id="3956e-296">Hello의 다음 섹션에서 방법 보여 주는 예제를 찾을 수 있습니다 다른 프로그래밍 언어를 사용 하 여 toosubmit 데이터 toohello 로그 분석 HTTP 데이터 수집기 API입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-296">In hello next sections, you'll find samples of how toosubmit data toohello Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="3956e-297">각 샘플에 대해 다음이 단계를 수행 hello 권한 부여 헤더에 대 한 tooset hello 변수:</span><span class="sxs-lookup"><span data-stu-id="3956e-297">For each sample, do these steps tooset hello variables for hello authorization header:</span></span>

1. <span data-ttu-id="3956e-298">Hello Operations Management Suite 포털에서 선택 hello **설정** 타일을 선택한 후 hello **연결 된 원본** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-298">In hello Operations Management Suite portal, select hello **Settings** tile, and then select hello **Connected Sources** tab.</span></span>
2. <span data-ttu-id="3956e-299">오른쪽 toohello **작업 영역 ID**hello 복사 아이콘을 선택한 다음 hello ID hello의 hello 값으로 붙여 **고객 ID** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-299">toohello right of **Workspace ID**, select hello copy icon, and then paste hello ID as hello value of hello **Customer ID** variable.</span></span>
3. <span data-ttu-id="3956e-300">오른쪽 toohello **기본 키**hello 복사 아이콘을 선택한 다음 hello ID hello의 hello 값으로 붙여 **공유 키** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-300">toohello right of **Primary Key**, select hello copy icon, and then paste hello ID as hello value of hello **Shared Key** variable.</span></span>

<span data-ttu-id="3956e-301">또는 hello 로그 유형 및 JSON 데이터에 대 한 hello 변수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-301">Alternatively, you can change hello variables for hello log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="3956e-302">PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="3956e-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
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

# Create hello function toocreate hello authorization signature
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


# Create hello function toocreate and post hello request
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

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="3956e-303">C# 샘플</span><span class="sxs-lookup"><span data-stu-id="3956e-303">C# sample</span></span>
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

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
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

        // Send a request toohello POST API endpoint
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

### <a name="python-sample"></a><span data-ttu-id="3956e-304">Python 샘플</span><span class="sxs-lookup"><span data-stu-id="3956e-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
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

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
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

## <a name="next-steps"></a><span data-ttu-id="3956e-305">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3956e-305">Next steps</span></span>
- <span data-ttu-id="3956e-306">사용 하 여 hello [로그 검색 API](log-analytics-log-search-api.md) hello 로그 분석 저장소에서 tooretrieve 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3956e-306">Use hello [Log Search API](log-analytics-log-search-api.md) tooretrieve data from hello Log Analytics repository.</span></span>
