---
title: "aaaException 처리 및 오류 로깅 시나리오-Azure 논리 앱 | Microsoft Docs"
description: "Azure Logic Apps에 대한 고급 예외 처리 및 오류 로깅에 대한 실제 사용 사례에 대해 설명합니다."
keywords: 
services: logic-apps
author: hedidin
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 63b0b843-f6b0-4d9a-98d0-17500be17385
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/29/2016
ms.author: LADocs; b-hoedid
ms.openlocfilehash: e893a7b652254dca7b8a82398e8afd571f6ccd25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="2e97c-103">시나리오: 논리 앱에 대한 예외 처리 및 오류 로깅</span><span class="sxs-lookup"><span data-stu-id="2e97c-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="2e97c-104">이 시나리오에서는 논리 앱 toobetter 지원 예외 처리를 확장 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-104">This scenario describes how you can extend a logic app toobetter support exception handling.</span></span> <span data-ttu-id="2e97c-105">실제 사용 사례 tooanswer hello 질문을 사용 했습니다: "Azure 논리 앱에서는 예외 및 오류 처리?"</span><span class="sxs-lookup"><span data-stu-id="2e97c-105">We've used a real-life use case tooanswer hello question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="2e97c-106">현재 Azure 논리 앱 스키마 hello 작업 응답에 대 한 표준 서식 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-106">hello current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="2e97c-107">이 템플릿은 API 앱에서 반환된 내부 유효성 검사 및 오류 응답을 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="2e97c-108">시나리오 및 사용 사례 개요</span><span class="sxs-lookup"><span data-stu-id="2e97c-108">Scenario and use case overview</span></span>

<span data-ttu-id="2e97c-109">이 시나리오에 대 한 사용 사례 hello로 hello 스토리 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-109">Here's hello story as hello use case for this scenario:</span></span> 

<span data-ttu-id="2e97c-110">잘 알려진 의료 조직 참여 toodevelop Microsoft Dynamics CRM Online을 사용 하 여 환자 포털을 만들 수 있는 Azure 솔루션 주세요.</span><span class="sxs-lookup"><span data-stu-id="2e97c-110">A well-known healthcare organization engaged us toodevelop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="2e97c-111">Dynamics CRM Online 환자 포털 hello와 Salesforce 사이의 toosend 약속 레코드 필요할 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-111">They needed toosend appointment records between hello Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="2e97c-112">이전 피드백 toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) 환자 모든 레코드에 대 한 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-112">We were asked toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="2e97c-113">hello 프로젝트에는 두 가지 주요 요구 사항이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-113">hello project had two major requirements:</span></span>  

* <span data-ttu-id="2e97c-114">Dynamics CRM Online 포털 hello에서 보낸 메서드 toolog 레코드</span><span class="sxs-lookup"><span data-stu-id="2e97c-114">A method toolog records sent from hello Dynamics CRM Online portal</span></span>
* <span data-ttu-id="2e97c-115">방식으로 tooview hello 워크플로 내에서 발생 한 오류</span><span class="sxs-lookup"><span data-stu-id="2e97c-115">A way tooview any errors that occurred within hello workflow</span></span>

> [!TIP]
> <span data-ttu-id="2e97c-116">이 프로젝트에 대 한 높은 수준의 비디오를 참조 하십시오. [통합 사용자 그룹](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "통합 사용자 그룹")합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-hello-problem"></a><span data-ttu-id="2e97c-117">Hello 문제 문제</span><span class="sxs-lookup"><span data-stu-id="2e97c-117">How we solved hello problem</span></span>

<span data-ttu-id="2e97c-118">선택한 이유 [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") (Cosmos DB에서 참조 한 문서로 toorecords) hello 로그 및 오류 레코드에 대 한 리포지토리로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for hello log and error records (Cosmos DB refers toorecords as documents).</span></span> <span data-ttu-id="2e97c-119">Azure 논리 앱 모든 응답에 대 한 표준 서식 파일을 사용 하므로 우리는 스키마를 없는 toocreate 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-119">Because Azure Logic Apps has a standard template for all responses, we would not have toocreate a custom schema.</span></span> <span data-ttu-id="2e97c-120">API 앱 너무 만들 수**삽입** 및 **쿼리** 오류와 로그 레코드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-120">We could create an API app too**Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="2e97c-121">Hello API 앱 내에서 각각에 대 한 스키마를 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-121">We could also define a schema for each within hello API app.</span></span>  

<span data-ttu-id="2e97c-122">또 다른 요구 사항은 특정 날짜 이후에 toopurge 레코드 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-122">Another requirement was toopurge records after a certain date.</span></span> <span data-ttu-id="2e97c-123">Cosmos DB에 라는 속성이 [tooLive 시간](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "tooLive 시간") (TTL) 허용 되 면 us tooset는 **시간 tooLive** 각 레코드 또는 컬렉션에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-123">Cosmos DB has a property called [Time tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time tooLive") (TTL), which allowed us tooset a **Time tooLive** value for each record or collection.</span></span> <span data-ttu-id="2e97c-124">이 기능은 hello 필요 toomanually 레코드를 삭제 Cosmos DB에서 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-124">This capability eliminated hello need toomanually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e97c-125">toocomplete이이 자습서에서는 toocreate Cosmos DB 데이터베이스와 두 개의 컬렉션 (로깅 및 오류)가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-125">toocomplete this tutorial, you need toocreate a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-hello-logic-app"></a><span data-ttu-id="2e97c-126">Hello 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2e97c-126">Create hello logic app</span></span>

<span data-ttu-id="2e97c-127">hello 첫 단계는 toocreate hello 논리 앱 및 논리 응용 프로그램 디자이너에서 열려 hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-127">hello first step is toocreate hello logic app and open hello app in Logic App Designer.</span></span> <span data-ttu-id="2e97c-128">이 예제에서는 부모-자식 논리 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="2e97c-129">Hello 부모를 이미 만든 것 및 toocreate 하나의 자식 논리 앱 하려는 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-129">Let's assume that we have already created hello parent and are going toocreate one child logic app.</span></span>

<span data-ttu-id="2e97c-130">Dynamics CRM Online에서 들어오는 toolog hello 레코드, 하겠습니다 때문에 hello 맨 위에서 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-130">Because we are going toolog hello record coming out of Dynamics CRM Online, let's start at hello top.</span></span> <span data-ttu-id="2e97c-131">사용 해야 합니다는 **요청** 않으므로 hello 부모 논리 앱이이 자식을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-131">We must use a **Request** trigger because hello parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="2e97c-132">논리 앱 트리거</span><span class="sxs-lookup"><span data-stu-id="2e97c-132">Logic app trigger</span></span>

<span data-ttu-id="2e97c-133">사용 하는 **요청** hello 다음 예제와 같이 트리거:</span><span class="sxs-lookup"><span data-stu-id="2e97c-133">We are using a **Request** trigger as shown in hello following example:</span></span>

```` json
"triggers": {
        "request": {
          "type": "request",
          "kind": "http",
          "inputs": {
            "schema": {
              "properties": {
                "CRMid": {
                  "type": "string"
                },
                "recordType": {
                  "type": "string"
                },
                "salesforceID": {
                  "type": "string"
                },
                "update": {
                  "type": "boolean"
                }
              },
              "required": [
                "CRMid",
                "recordType",
                "salesforceID",
                "update"
              ],
              "type": "object"
            }
          }
        }
      },

````


## <a name="steps"></a><span data-ttu-id="2e97c-134">단계</span><span class="sxs-lookup"><span data-stu-id="2e97c-134">Steps</span></span>

<span data-ttu-id="2e97c-135">Hello 환자 레코드의 hello 소스 (요청) hello Dynamics CRM Online 포털에서 로그인 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-135">We must log hello source (request) of hello patient record from hello Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="2e97c-136">먼저 Dynamics CRM Online에서 새 예약 기록을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="2e97c-137">CRM에서 들어오는 hello 트리거 hello 제공 **CRM PatentId**, **레코드 종류**, **신규 또는 업데이트 된 레코드** (새 부울 값을 업데이트 하거나), 및  **SalesforceId**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-137">hello trigger coming from CRM provides us with hello **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="2e97c-138">hello **SalesforceId** 는 업데이트에만 사용 하기 때문에 null 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-138">hello **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="2e97c-139">Hello CRM 레코드 CRM hello를 사용 하 여 얻을 수 있는 **PatientID** 및 hello **레코드 종류**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-139">We get hello CRM record by using hello CRM **PatientID** and hello **Record Type**.</span></span>

2. <span data-ttu-id="2e97c-140">다음으로 필요한 tooadd DocumentDB API 앱 **InsertLogEntry** 논리가 응용 프로그램 디자이너에서 아래 그림과 같이 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-140">Next, we need tooadd our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="2e97c-141">**로그 항목 삽입**</span><span class="sxs-lookup"><span data-stu-id="2e97c-141">**Insert log entry**</span></span>

   ![로그 항목 삽입](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="2e97c-143">**오류 항목 삽입**</span><span class="sxs-lookup"><span data-stu-id="2e97c-143">**Insert error entry**</span></span>

   ![로그 항목 삽입](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="2e97c-145">**기록 만들기 실패에 대한 확인**</span><span class="sxs-lookup"><span data-stu-id="2e97c-145">**Check for create record failure**</span></span>

   ![조건](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="2e97c-147">논리 앱 소스 코드</span><span class="sxs-lookup"><span data-stu-id="2e97c-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="2e97c-148">다음 예제는 hello에는 샘플만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-148">hello following examples are samples only.</span></span> <span data-ttu-id="2e97c-149">이 자습서는 프로덕션 환경에서 이제 구현을 기반으로, 값의 hello는 **소스 노드** 관련된 tooscheduling 약속. 되는 속성이 표시 되지 않습니다 ></span><span class="sxs-lookup"><span data-stu-id="2e97c-149">Because this tutorial is based on an implementation now in production, hello value of a **Source Node** might not display properties that are related tooscheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="2e97c-150">로깅</span><span class="sxs-lookup"><span data-stu-id="2e97c-150">Logging</span></span>

<span data-ttu-id="2e97c-151">논리 앱 코드 다음 hello 샘플 표시 방법을 toohandle 로깅.</span><span class="sxs-lookup"><span data-stu-id="2e97c-151">hello following logic app code sample shows how toohandle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="2e97c-152">로그 항목</span><span class="sxs-lookup"><span data-stu-id="2e97c-152">Log entry</span></span>

<span data-ttu-id="2e97c-153">로그 항목을 삽입 하기 위한 hello 논리 앱 소스 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-153">Here is hello logic app source code for inserting a log entry.</span></span>

``` json
"InsertLogEntry": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "date": "@{outputs('Gets_NewPatientRecord')['headers']['Date']}",
            "operation": "New Patient",
            "patientId": "@{triggerBody()['CRMid']}",
            "providerId": "@{triggerBody()['providerID']}",
            "source": "@{outputs('Gets_NewPatientRecord')['headers']}"
        },
        "method": "post",
        "uri": "https://.../api/Log"
        },
        "runAfter":    {
            "Gets_NewPatientecord": ["Succeeded"]
        }
}
```

#### <a name="log-request"></a><span data-ttu-id="2e97c-154">로그 요청</span><span class="sxs-lookup"><span data-stu-id="2e97c-154">Log request</span></span>

<span data-ttu-id="2e97c-155">다음은 toohello API 앱을 게시 하는 hello 로그 요청 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-155">Here is hello log request message posted toohello API app.</span></span>

``` json
    {
    "uri": "https://.../api/Log",
    "method": "post",
    "body": {
        "date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "operation": "New Patient",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "providerId": "",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}"
        }
    }

```


#### <a name="log-response"></a><span data-ttu-id="2e97c-156">로그 응답</span><span class="sxs-lookup"><span data-stu-id="2e97c-156">Log response</span></span>

<span data-ttu-id="2e97c-157">Hello API 앱에서 hello 로그 응답 메시지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-157">Here is hello log response message from hello API app.</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:32:17 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "964",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "ttl": 2592000,
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0_1465597937",
        "_rid": "XngRAOT6IQEHAAAAAAAAAA==",
        "_self": "dbs/XngRAA==/colls/XngRAOT6IQE=/docs/XngRAOT6IQEHAAAAAAAAAA==/",
        "_ts": 1465597936,
        "_etag": "/"0400fc2f-0000-0000-0000-575b3ff00000/"",
        "patientID": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:56Z",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}",
        "operation": "New Patient",
        "salesforceId": "",
        "expired": false
    }
}

```

<span data-ttu-id="2e97c-158">이제 hello 오류 단계 처리를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-158">Now let's look at hello error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="2e97c-159">오류 처리</span><span class="sxs-lookup"><span data-stu-id="2e97c-159">Error handling</span></span>

<span data-ttu-id="2e97c-160">hello 다음 논리 앱 코드 샘플에서는 오류 처리를 구현 하는 방법을</span><span class="sxs-lookup"><span data-stu-id="2e97c-160">hello following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="2e97c-161">오류 기록 만들기</span><span class="sxs-lookup"><span data-stu-id="2e97c-161">Create error record</span></span>

<span data-ttu-id="2e97c-162">오류 레코드를 만들기 위한 hello 논리 앱 소스 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-162">Here is hello logic app source code for creating an error record.</span></span>

``` json
"actions": {
    "CreateErrorRecord": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "action": "New_Patient",
            "isError": true,
            "crmId": "@{triggerBody()['CRMid']}",
            "patientID": "@{triggerBody()['CRMid']}",
            "message": "@{body('Create_NewPatientRecord')['message']}",
            "providerId": "@{triggerBody()['providerId']}",
            "severity": 4,
            "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
            "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
            "salesforceId": "",
            "update": false
        },
        "method": "post",
        "uri": "https://.../api/CrMtoSfError"
        },
        "runAfter":
        {
            "Create_NewPatientRecord": ["Failed" ]
        }
    }
}             
```

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="2e97c-163">Cosmos DB에 삽입 오류 - 요청</span><span class="sxs-lookup"><span data-stu-id="2e97c-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="2e97c-164">Cosmos DB에 삽입 오류 - 응답</span><span class="sxs-lookup"><span data-stu-id="2e97c-164">Insert error into Cosmos DB--response</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:57 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "1561",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0-1465597917",
        "_rid": "sQx2APhVzAA8AAAAAAAAAA==",
        "_self": "dbs/sQx2AA==/colls/sQx2APhVzAA=/docs/sQx2APhVzAA8AAAAAAAAAA==/",
        "_ts": 1465597912,
        "_etag": "/"0c00eaac-0000-0000-0000-575b3fdc0000/"",
        "prescriberId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:57.3651027Z",
        "action": "New_Patient",
        "salesforceId": "",
        "update": false,
        "body": "CRM failed toocomplete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/":/"DO - Degree level is DO/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MterID_mp__c/":/"/",/"Medicis_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"XXXXXXX/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "code": 400,
        "errors": null,
        "isError": true,
        "severity": 4,
        "notes": null,
        "resolved": 0
        }
}
```

#### <a name="salesforce-error-response"></a><span data-ttu-id="2e97c-165">Salesforce 오류 응답</span><span class="sxs-lookup"><span data-stu-id="2e97c-165">Salesforce error response</span></span>

``` json
{
    "statusCode": 400,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "3e8e4884-288e-4633-972c-8271b2cc912c",
        "X-Content-Type-Options": "nosniff",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "Set-Cookie": "ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1",
        "Server": "Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "205",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "status": 400,
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-hello-response-back-tooparent-logic-app"></a><span data-ttu-id="2e97c-166">Hello 응답 백 tooparent 논리 앱을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-166">Return hello response back tooparent logic app</span></span>

<span data-ttu-id="2e97c-167">Hello 응답을 전달할 수 hello 응답을 가져온 후 뒤로 toohello 부모 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="2e97c-167">After you get hello response, you can pass hello response back toohello parent logic app.</span></span>

#### <a name="return-success-response-tooparent-logic-app"></a><span data-ttu-id="2e97c-168">성공 응답 tooparent 논리 앱을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-168">Return success response tooparent logic app</span></span>

``` json
"SuccessResponse": {
    "runAfter":
        {
            "UpdateNew_CRMPatientResponse": ["Succeeded"]
        },
    "inputs": {
        "body": {
            "status": "Success"
    },
    "headers": {
    "    Content-type": "application/json",
        "x-ms-date": "@utcnow()"
    },
    "statusCode": 200
    },
    "type": "Response"
}
```

#### <a name="return-error-response-tooparent-logic-app"></a><span data-ttu-id="2e97c-169">오류 응답 tooparent 논리 앱을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-169">Return error response tooparent logic app</span></span>

``` json
"ErrorResponse": {
    "runAfter":
        {
            "Create_NewPatientRecord": ["Failed"]
        },
    "inputs": {
        "body": {
            "status": "BadRequest"
        },
        "headers": {
            "Content-type": "application/json",
            "x-ms-date": "@utcnow()"
        },
        "statusCode": 400
    },
    "type": "Response"
}

```


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="2e97c-170">Cosmos DB 리포지토리 및 포털</span><span class="sxs-lookup"><span data-stu-id="2e97c-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="2e97c-171">솔루션은 [Cosmos DB](https://azure.microsoft.com/services/documentdb)와 관련된 기능을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="2e97c-172">오류 관리 포털</span><span class="sxs-lookup"><span data-stu-id="2e97c-172">Error management portal</span></span>

<span data-ttu-id="2e97c-173">tooview hello 오류 Cosmos DB에서 MVC 웹 응용 프로그램 toodisplay hello 오류 레코드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-173">tooview hello errors, you can create an MVC web app toodisplay hello error records from Cosmos DB.</span></span> <span data-ttu-id="2e97c-174">hello **목록**, **세부 정보**, **편집**, 및 **삭제** 작업 hello 현재 버전에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-174">hello **List**, **Details**, **Edit**, and **Delete** operations are included in hello current version.</span></span>

> [!NOTE]
> <span data-ttu-id="2e97c-175">작업 편집: Cosmos DB hello 전체 문서를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-175">Edit operation: Cosmos DB replaces hello entire document.</span></span> <span data-ttu-id="2e97c-176">hello에 표시 된 레코드 hello **목록** 및 **세부** 뷰는 예제만 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-176">hello records shown in hello **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="2e97c-177">실제 환자 예약 기록이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="2e97c-178">다음은 예제 MVC 앱의 hello를 사용 하 여 이전에 만든 세부 정보는 접근 방식을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-178">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="2e97c-179">오류 관리 목록</span><span class="sxs-lookup"><span data-stu-id="2e97c-179">Error management list</span></span>
![오류 목록](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="2e97c-181">오류 관리 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="2e97c-181">Error management detail view</span></span>
![오류 세부 정보](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="2e97c-183">로그 관리 포털</span><span class="sxs-lookup"><span data-stu-id="2e97c-183">Log management portal</span></span>

<span data-ttu-id="2e97c-184">tooview hello 로그도 만들었는지 여부는 MVC 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-184">tooview hello logs, we also created an MVC web app.</span></span> <span data-ttu-id="2e97c-185">다음은 예제 MVC 앱의 hello를 사용 하 여 이전에 만든 세부 정보는 접근 방식을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-185">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="2e97c-186">샘플 로그 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="2e97c-186">Sample log detail view</span></span>
![로그 세부 정보 보기](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="2e97c-188">API 앱 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2e97c-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="2e97c-189">논리 앱 예외 관리 API</span><span class="sxs-lookup"><span data-stu-id="2e97c-189">Logic Apps exception management API</span></span>

<span data-ttu-id="2e97c-190">오픈 소스 Azure Logic Apps 예외 관리 API 앱은 여기에서 설명한 기능을 제공합니다. 두 개의 컨트롤러가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="2e97c-191">**ErrorController** 는 DocumentDB 컬렉션에 오류 기록(문서)을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="2e97c-192">**LogController** 는 DocumentDB 컬렉션에 로그 기록(문서)을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="2e97c-193">두 컨트롤러가 모두 사용 하 여 `async Task<dynamic>` 우리를 만들 수 있도록 런타임에 작업 tooresolve 허용 작업 hello hello 작업의 hello 본문에서 DocumentDB 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-193">Both controllers use `async Task<dynamic>` operations, allowing operations tooresolve at runtime, so we can create hello DocumentDB schema in hello body of hello operation.</span></span> 
> 

<span data-ttu-id="2e97c-194">DocumentDB의 모든 문서에는 고유한 ID가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="2e97c-195">사용 하 여 `PatientId` 타임 스탬프 변환 tooa Unix 타임 스탬프 값 (double)을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-195">We are using `PatientId` and adding a timestamp that is converted tooa Unix timestamp value (double).</span></span> <span data-ttu-id="2e97c-196">Hello 값 tooremove hello 소수 자릿수 값을 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-196">We truncate hello value tooremove hello fractional value.</span></span>

<span data-ttu-id="2e97c-197">오류 컨트롤러 API의 hello 소스 코드를 볼 수 있습니다 [GitHub에서](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-197">You can view hello source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="2e97c-198">구문 다음 hello를 사용 하 여 논리 앱에서 API hello를 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-198">We call hello API from a logic app by using hello following syntax:</span></span>

``` json
 "actions": {
        "CreateErrorRecord": {
          "metadata": {
            "apiDefinitionUrl": "https://.../swagger/docs/v1",
            "swaggerSource": "website"
          },
          "type": "Http",
          "inputs": {
            "body": {
              "action": "New_Patient",
              "isError": true,
              "crmId": "@{triggerBody()['CRMid']}",
              "prescriberId": "@{triggerBody()['CRMid']}",
              "message": "@{body('Create_NewPatientRecord')['message']}",
              "salesforceId": "@{triggerBody()['salesforceID']}",
              "severity": 4,
              "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
              "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
              "update": false
            },
            "method": "post",
            "uri": "https://.../api/CrMtoSfError"
          },
          "runAfter": {
              "Create_NewPatientRecord": ["Failed"]
            }
        }
 }
```

<span data-ttu-id="2e97c-199">hello hello에 대 한 코드 샘플 검사 앞에 식을 hello *Create_NewPatientRecord* 상태의 **실패**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-199">hello expression in hello preceding code sample checks for hello *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="2e97c-200">요약</span><span class="sxs-lookup"><span data-stu-id="2e97c-200">Summary</span></span>

* <span data-ttu-id="2e97c-201">논리 앱에서 로깅 및 오류 처리를 쉽게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="2e97c-202">로그 및 오류 레코드 (문서)에 대 한 DocumentDB hello 리포지토리로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-202">You can use DocumentDB as hello repository for log and error records (documents).</span></span>
* <span data-ttu-id="2e97c-203">MVC toocreate 포털 toodisplay 로그 및 오류 레코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-203">You can use MVC toocreate a portal toodisplay log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="2e97c-204">소스 코드</span><span class="sxs-lookup"><span data-stu-id="2e97c-204">Source code</span></span>

<span data-ttu-id="2e97c-205">hello 논리 앱 예외 관리 API 응용 프로그램에 대 한 hello 소스 코드를이 사용할 수 있는 [GitHub 리포지토리](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "논리 앱 예외 관리 API")합니다.</span><span class="sxs-lookup"><span data-stu-id="2e97c-205">hello source code for hello Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e97c-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e97c-206">Next steps</span></span>

* [<span data-ttu-id="2e97c-207">논리 앱 예제 및 시나리오 더 보기</span><span class="sxs-lookup"><span data-stu-id="2e97c-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="2e97c-208">Logic Apps 모니터링에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="2e97c-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="2e97c-209">Logic Apps용 자동화된 배포 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="2e97c-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
