---
title: "예외 처리 및 오류 로깅 시나리오 - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 044de27c75da93c95609110d2b73336c42f746fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="518bd-103">시나리오: 논리 앱에 대한 예외 처리 및 오류 로깅</span><span class="sxs-lookup"><span data-stu-id="518bd-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="518bd-104">이 시나리오에서는 논리 앱을 확장하여 예외 처리를 더 잘 지원할 수 있는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-104">This scenario describes how you can extend a logic app to better support exception handling.</span></span> <span data-ttu-id="518bd-105">실제 사용 사례를 사용하여 "논리 앱이 예외 및 오류 처리를 지원하나요?"라는 질문에 대해 답변을 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-105">We've used a real-life use case to answer the question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="518bd-106">최신 버전의 Azure Logic Apps 스키마는 작업 응답에 대한 표준 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-106">The current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="518bd-107">이 템플릿은 API 앱에서 반환된 내부 유효성 검사 및 오류 응답을 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="518bd-108">시나리오 및 사용 사례 개요</span><span class="sxs-lookup"><span data-stu-id="518bd-108">Scenario and use case overview</span></span>

<span data-ttu-id="518bd-109">다음은 이 시나리오에 대한 사용 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-109">Here's the story as the use case for this scenario:</span></span> 

<span data-ttu-id="518bd-110">유명한 의료 조직이 Microsoft Dynamics CRM Online을 사용하여 환자 포털을 만드는 Azure 솔루션을 개발하는 데 참여했습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-110">A well-known healthcare organization engaged us to develop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="518bd-111">Dynamics CRM Online 환자 포털과 Salesforce 간에 예약 기록을 보내야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-111">They needed to send appointment records between the Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="518bd-112">모든 환자 기록에 [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) 표준을 사용하도록 요청을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-112">We were asked to use the [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="518bd-113">이 프로젝트에는 두 가지 주요 요구 사항이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-113">The project had two major requirements:</span></span>  

* <span data-ttu-id="518bd-114">Dynamics CRM Online 포털에서 전송된 기록을 기록하는 방법</span><span class="sxs-lookup"><span data-stu-id="518bd-114">A method to log records sent from the Dynamics CRM Online portal</span></span>
* <span data-ttu-id="518bd-115">워크플로 내에서 발생한 오류를 보는 방법</span><span class="sxs-lookup"><span data-stu-id="518bd-115">A way to view any errors that occurred within the workflow</span></span>

> [!TIP]
> <span data-ttu-id="518bd-116">이 프로젝트에 대한 고급 비디오를 보려면 [통합 사용자 그룹](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group")을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="518bd-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-the-problem"></a><span data-ttu-id="518bd-117">문제를 해결한 방법</span><span class="sxs-lookup"><span data-stu-id="518bd-117">How we solved the problem</span></span>

<span data-ttu-id="518bd-118">[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB")를 로그 및 오류 레코드에 대한 리포지토리로 선택했습니다(Cosmos DB에서는 레코드를 문서로 참조함).</span><span class="sxs-lookup"><span data-stu-id="518bd-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for the log and error records (Cosmos DB refers to records as documents).</span></span> <span data-ttu-id="518bd-119">Azure Logic Apps에 모든 응답에 대한 표준 템플릿이 있으므로 사용자 지정 스키마를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-119">Because Azure Logic Apps has a standard template for all responses, we would not have to create a custom schema.</span></span> <span data-ttu-id="518bd-120">오류 및 로그 기록에 대한 **삽입** 및 **쿼리**에 API 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-120">We could create an API app to **Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="518bd-121">API 앱 내에서 각각에 대한 스키마를 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-121">We could also define a schema for each within the API app.</span></span>  

<span data-ttu-id="518bd-122">다른 요구 사항은 특정 날짜 이후 기록을 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-122">Another requirement was to purge records after a certain date.</span></span> <span data-ttu-id="518bd-123">Cosmos DB에는 TTL([Time To Live](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time To Live"))이라는 속성이 있으며, 이 속성을 사용하여 각 기록 또는 컬렉션에 대한 **Time To Live** 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-123">Cosmos DB has a property called [Time to Live](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time to Live") (TTL), which allowed us to set a **Time to Live** value for each record or collection.</span></span> <span data-ttu-id="518bd-124">이 기능 덕분에 Cosmos DB에서 레코드를 수동으로 삭제할 필요가 없어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-124">This capability eliminated the need to manually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="518bd-125">이 자습서를 완료하려면 Cosmos DB 데이터베이스와 두 개의 컬렉션(로깅 및 오류)을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-125">To complete this tutorial, you need to create a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-the-logic-app"></a><span data-ttu-id="518bd-126">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="518bd-126">Create the logic app</span></span>

<span data-ttu-id="518bd-127">첫 번째 단계는 논리 앱을 만들고 논리 앱 디자이너에서 앱을 여는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-127">The first step is to create the logic app and open the app in Logic App Designer.</span></span> <span data-ttu-id="518bd-128">이 예제에서는 부모-자식 논리 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="518bd-129">부모를 이미 만들었고 하나의 자식 논리 앱을 만들려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-129">Let's assume that we have already created the parent and are going to create one child logic app.</span></span>

<span data-ttu-id="518bd-130">Dynamics CRM Online에서 나오는 기록을 로깅해야 하므로 맨 위부터 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-130">Because we are going to log the record coming out of Dynamics CRM Online, let's start at the top.</span></span> <span data-ttu-id="518bd-131">부모 논리 앱이 이 자식을 트리거하므로 **요청** 트리거를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-131">We must use a **Request** trigger because the parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="518bd-132">논리 앱 트리거</span><span class="sxs-lookup"><span data-stu-id="518bd-132">Logic app trigger</span></span>

<span data-ttu-id="518bd-133">다음 예제와 같이 **요청** 트리거를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-133">We are using a **Request** trigger as shown in the following example:</span></span>

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


## <a name="steps"></a><span data-ttu-id="518bd-134">단계</span><span class="sxs-lookup"><span data-stu-id="518bd-134">Steps</span></span>

<span data-ttu-id="518bd-135">Dynamics CRM Online 포털에서 환자 기록의 원본(요청)을 로깅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-135">We must log the source (request) of the patient record from the Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="518bd-136">먼저 Dynamics CRM Online에서 새 예약 기록을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="518bd-137">CRM에서 오는 트리거는 **CRM PatentId**, **기록 종류**, **신규 또는 업데이트된 기록**(새로운 또는 업데이트된 부울 값) 및 **SalesforceId**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-137">The trigger coming from CRM provides us with the **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="518bd-138">업데이트를 위해서만 사용되기 때문에 **SalesforceId** 는 null일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-138">The **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="518bd-139">CRM **PatientID** 및 **기록 종류**를 사용하여 CRM 기록을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-139">We get the CRM record by using the CRM **PatientID** and the **Record Type**.</span></span>

2. <span data-ttu-id="518bd-140">다음으로 논리 앱 디자이너에서 DocumentDB API 앱 **InsertLogEntry** 작업을 여기에 나온 것처럼 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-140">Next, we need to add our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="518bd-141">**로그 항목 삽입**</span><span class="sxs-lookup"><span data-stu-id="518bd-141">**Insert log entry**</span></span>

   ![로그 항목 삽입](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="518bd-143">**오류 항목 삽입**</span><span class="sxs-lookup"><span data-stu-id="518bd-143">**Insert error entry**</span></span>

   ![로그 항목 삽입](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="518bd-145">**기록 만들기 실패에 대한 확인**</span><span class="sxs-lookup"><span data-stu-id="518bd-145">**Check for create record failure**</span></span>

   ![조건](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="518bd-147">논리 앱 소스 코드</span><span class="sxs-lookup"><span data-stu-id="518bd-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="518bd-148">다음 예제는 샘플에 불과합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-148">The following examples are samples only.</span></span> <span data-ttu-id="518bd-149">이 자습서는 현재 프로덕션에서의 구현을 기반으로 하므로 **원본 노드** 의 값은 예약 일정에 관련된 속성을 표시하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-149">Because this tutorial is based on an implementation now in production, the value of a **Source Node** might not display properties that are related to scheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="518bd-150">로깅</span><span class="sxs-lookup"><span data-stu-id="518bd-150">Logging</span></span>

<span data-ttu-id="518bd-151">다음 논리 앱 코드 샘플은 로그를 처리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-151">The following logic app code sample shows how to handle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="518bd-152">로그 항목</span><span class="sxs-lookup"><span data-stu-id="518bd-152">Log entry</span></span>

<span data-ttu-id="518bd-153">로그 항목을 삽입하기 위한 논리 앱 소스 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-153">Here is the logic app source code for inserting a log entry.</span></span>

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

#### <a name="log-request"></a><span data-ttu-id="518bd-154">로그 요청</span><span class="sxs-lookup"><span data-stu-id="518bd-154">Log request</span></span>

<span data-ttu-id="518bd-155">API 앱에 게시된 로그 요청 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-155">Here is the log request message posted to the API app.</span></span>

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


#### <a name="log-response"></a><span data-ttu-id="518bd-156">로그 응답</span><span class="sxs-lookup"><span data-stu-id="518bd-156">Log response</span></span>

<span data-ttu-id="518bd-157">API 앱에서 발생한 로그 응답 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-157">Here is the log response message from the API app.</span></span>

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

<span data-ttu-id="518bd-158">이제 오류 처리 단계를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-158">Now let's look at the error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="518bd-159">오류 처리</span><span class="sxs-lookup"><span data-stu-id="518bd-159">Error handling</span></span>

<span data-ttu-id="518bd-160">다음 논리 앱 코드 샘플은 오류 처리를 구현할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-160">The following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="518bd-161">오류 기록 만들기</span><span class="sxs-lookup"><span data-stu-id="518bd-161">Create error record</span></span>

<span data-ttu-id="518bd-162">오류 기록을 만들기 위한 논리 앱 소스 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-162">Here is the logic app source code for creating an error record.</span></span>

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

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="518bd-163">Cosmos DB에 삽입 오류 - 요청</span><span class="sxs-lookup"><span data-stu-id="518bd-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="518bd-164">Cosmos DB에 삽입 오류 - 응답</span><span class="sxs-lookup"><span data-stu-id="518bd-164">Insert error into Cosmos DB--response</span></span>

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
        "body": "CRM failed to complete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
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

#### <a name="salesforce-error-response"></a><span data-ttu-id="518bd-165">Salesforce 오류 응답</span><span class="sxs-lookup"><span data-stu-id="518bd-165">Salesforce error response</span></span>

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
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-the-response-back-to-parent-logic-app"></a><span data-ttu-id="518bd-166">부모 논리 앱에 응답 반환</span><span class="sxs-lookup"><span data-stu-id="518bd-166">Return the response back to parent logic app</span></span>

<span data-ttu-id="518bd-167">응답을 받으면 부모 논리 앱으로 다시 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-167">After you get the response, you can pass the response back to the parent logic app.</span></span>

#### <a name="return-success-response-to-parent-logic-app"></a><span data-ttu-id="518bd-168">부모 논리 앱에 성공 응답 반환</span><span class="sxs-lookup"><span data-stu-id="518bd-168">Return success response to parent logic app</span></span>

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

#### <a name="return-error-response-to-parent-logic-app"></a><span data-ttu-id="518bd-169">부모 논리 앱에 오류 응답 반환</span><span class="sxs-lookup"><span data-stu-id="518bd-169">Return error response to parent logic app</span></span>

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


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="518bd-170">Cosmos DB 리포지토리 및 포털</span><span class="sxs-lookup"><span data-stu-id="518bd-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="518bd-171">솔루션은 [Cosmos DB](https://azure.microsoft.com/services/documentdb)와 관련된 기능을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="518bd-172">오류 관리 포털</span><span class="sxs-lookup"><span data-stu-id="518bd-172">Error management portal</span></span>

<span data-ttu-id="518bd-173">오류를 보기 위해 Cosmos DB의 오류 레코드를 표시하는 MVC 웹앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-173">To view the errors, you can create an MVC web app to display the error records from Cosmos DB.</span></span> <span data-ttu-id="518bd-174">현재 버전에는 **목록**, **세부 정보**, **편집** 및 **삭제** 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-174">The **List**, **Details**, **Edit**, and **Delete** operations are included in the current version.</span></span>

> [!NOTE]
> <span data-ttu-id="518bd-175">편집 작업: Cosmos DB는 전체 문서를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-175">Edit operation: Cosmos DB replaces the entire document.</span></span> <span data-ttu-id="518bd-176">**목록** 및 **세부 정보** 보기에 표시된 기록은 예제만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-176">The records shown in the **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="518bd-177">실제 환자 예약 기록이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="518bd-178">다음은 앞에서 설명한 접근 방식을 사용하여 만든 MVC 앱 정보의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-178">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="518bd-179">오류 관리 목록</span><span class="sxs-lookup"><span data-stu-id="518bd-179">Error management list</span></span>
![오류 목록](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="518bd-181">오류 관리 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="518bd-181">Error management detail view</span></span>
![오류 세부 정보](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="518bd-183">로그 관리 포털</span><span class="sxs-lookup"><span data-stu-id="518bd-183">Log management portal</span></span>

<span data-ttu-id="518bd-184">로그를 보기 위해 MVC 웹앱도 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-184">To view the logs, we also created an MVC web app.</span></span> <span data-ttu-id="518bd-185">다음은 앞에서 설명한 접근 방식을 사용하여 만든 MVC 앱 정보의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-185">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="518bd-186">샘플 로그 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="518bd-186">Sample log detail view</span></span>
![로그 세부 정보 보기](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="518bd-188">API 앱 세부 정보</span><span class="sxs-lookup"><span data-stu-id="518bd-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="518bd-189">논리 앱 예외 관리 API</span><span class="sxs-lookup"><span data-stu-id="518bd-189">Logic Apps exception management API</span></span>

<span data-ttu-id="518bd-190">오픈 소스 Azure Logic Apps 예외 관리 API 앱은 여기에서 설명한 기능을 제공합니다. 두 개의 컨트롤러가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="518bd-191">**ErrorController** 는 DocumentDB 컬렉션에 오류 기록(문서)을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="518bd-192">**LogController** 는 DocumentDB 컬렉션에 로그 기록(문서)을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="518bd-193">두 컨트롤러 모두 `async Task<dynamic>` 작업을 사용하여 작업이 런타임에 해결되도록 하므로 작업의 본문에서 DocumentDB 스키마를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-193">Both controllers use `async Task<dynamic>` operations, allowing operations to resolve at runtime, so we can create the DocumentDB schema in the body of the operation.</span></span> 
> 

<span data-ttu-id="518bd-194">DocumentDB의 모든 문서에는 고유한 ID가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="518bd-195">`PatientId` 를 사용하고 Unix 타임스탬프 값(double)으로 변환되는 타임스탬프를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-195">We are using `PatientId` and adding a timestamp that is converted to a Unix timestamp value (double).</span></span> <span data-ttu-id="518bd-196">값을 잘라서 소수 자릿수 값을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-196">We truncate the value to remove the fractional value.</span></span>

<span data-ttu-id="518bd-197">[GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs)에서 오류 컨트롤러 API의 소스 코드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-197">You can view the source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="518bd-198">다음 구문을 사용하여 논리 앱에서 API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-198">We call the API from a logic app by using the following syntax:</span></span>

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

<span data-ttu-id="518bd-199">위의 코드 예제에서 식은 *Create_NewPatientRecord* 상태, **Failed**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-199">The expression in the preceding code sample checks for the *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="518bd-200">요약</span><span class="sxs-lookup"><span data-stu-id="518bd-200">Summary</span></span>

* <span data-ttu-id="518bd-201">논리 앱에서 로깅 및 오류 처리를 쉽게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="518bd-202">DocumentDB를 로그 및 오류 기록(문서)에 대한 리포지토리로 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-202">You can use DocumentDB as the repository for log and error records (documents).</span></span>
* <span data-ttu-id="518bd-203">로그 및 오류 기록을 표시하려면 포털을 만들려면 MVC를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-203">You can use MVC to create a portal to display log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="518bd-204">소스 코드</span><span class="sxs-lookup"><span data-stu-id="518bd-204">Source code</span></span>

<span data-ttu-id="518bd-205">논리 앱 예외 관리 API 응용 프로그램에 대한 소스 코드는 이 [GitHub 리포지토리](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "논리 앱 예외 관리 API")에서 프로젝트의 높은 수준의 비디오를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="518bd-205">The source code for the Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="518bd-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="518bd-206">Next steps</span></span>

* [<span data-ttu-id="518bd-207">논리 앱 예제 및 시나리오 더 보기</span><span class="sxs-lookup"><span data-stu-id="518bd-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="518bd-208">Logic Apps 모니터링에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="518bd-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="518bd-209">Logic Apps용 자동화된 배포 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="518bd-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
