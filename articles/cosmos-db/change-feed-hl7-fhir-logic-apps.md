---
title: "HL7 FHIR 리소스에 대한 변경 사항 피드 - Azure Cosmos DB | Microsoft Docs"
description: "Azure Logic Apps, Azure Cosmos DB 및 Service Bus를 사용하여 HL7 FHIR 환자 의료 기록에 대한 변경 알림 설정 방법을 알아보세요."
keywords: hl7 fhir
services: cosmos-db
author: hedidin
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 0d25c11f-9197-419a-aa19-4614c6ab2d06
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: b-hoedid
ms.openlocfilehash: d2b50c0b6864af41fb9cfa051721c432772b228d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="7eaf3-104">Logic Apps 및 Azure Cosmos DB를 사용하여 환자에게 HL7 FHIR 의료 기록 변경 통지</span><span class="sxs-lookup"><span data-stu-id="7eaf3-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="7eaf3-105">Azure MVP Howard Edidin은 최근에 환자 포털에 새 기능을 추가하길 원하는 한 의료 기관으로부터 문의를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted to add new functionality to their patient portal.</span></span> <span data-ttu-id="7eaf3-106">의료 기록이 업데이트되면 환자에게 알림을 보내고 환자가 이러한 업데이트를 구독할 수 있는 기능이 필요했습니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-106">They needed to send notifications to patients when their health record was updated, and they needed patients to be able to subscribe to these updates.</span></span> 

<span data-ttu-id="7eaf3-107">이 문서는 Azure Cosmos DB, Logic Apps 및 Service Bus를 사용하여 이 의료 기관용으로 만든 변경 사항 피드 알림 솔루션을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-107">This article walks through the change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="7eaf3-108">프로젝트 요구 사항</span><span class="sxs-lookup"><span data-stu-id="7eaf3-108">Project requirements</span></span>
- <span data-ttu-id="7eaf3-109">공급자는 XML 형식으로 HL7 통합-임상 문서 아키텍처(C-CDA) 문서를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="7eaf3-110">C-CDA 문서는 가족 이력, 예방접종 기록 등의 임상 문서는 물론 관리, 워크플로 및 재무 서류를 포함한 모든 유형의 임상 문서를 포괄하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="7eaf3-111">C-CDA 문서는 JSON 형식으로 [HL7 FHIR 리소스](http://hl7.org/fhir/2017Jan/resourcelist.html)로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-111">C-CDA documents are converted to [HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="7eaf3-112">수정된 FHIR 리소스 문서는 JSON 형식으로 전자 메일을 통해 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="7eaf3-113">솔루션 워크플로</span><span class="sxs-lookup"><span data-stu-id="7eaf3-113">Solution workflow</span></span> 

<span data-ttu-id="7eaf3-114">높은 수준에서 프로젝트에 다음 워크플로 단계가 필요했습니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-114">At a high level, the project required the following workflow steps:</span></span> 
1. <span data-ttu-id="7eaf3-115">C-CDA 문서를 FHIR 리소스로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-115">Convert C-CDA documents to FHIR resources.</span></span>
2. <span data-ttu-id="7eaf3-116">수정된 FHIR 리소스에 대한 반복 트리거 폴링을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="7eaf3-117">사용자 지정 앱인 FhirNotificationApi를 호출하여 Azure Cosmos DB에 연결하고 새롭거나 수정된 문서를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-117">Call a custom app, FhirNotificationApi, to connect to Azure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="7eaf3-118">해당 응답을 Service Bus 큐에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-118">Save the response to to the Service Bus queue.</span></span>
4. <span data-ttu-id="7eaf3-119">Service Bus 큐에서 새 메시지를 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-119">Poll for new messages in the Service Bus queue.</span></span>
5. <span data-ttu-id="7eaf3-120">환자에게 전자 메일 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-120">Send email notifications to patients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="7eaf3-121">솔루션 아키텍처</span><span class="sxs-lookup"><span data-stu-id="7eaf3-121">Solution architecture</span></span>
<span data-ttu-id="7eaf3-122">이 솔루션에는 위의 요구 사항을 충족하고 솔루션 워크플로를 완성하기 위해 세 개의 Logic Apps가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-122">This solution requires three Logic Apps to meet the above requirements and complete the solution workflow.</span></span> <span data-ttu-id="7eaf3-123">세 가지 논리 앱은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-123">The three logic apps are:</span></span>
1. <span data-ttu-id="7eaf3-124">**HL7-FHIR-매핑 앱**: HL7 C-CDA 문서를 수신하여 FHIR 리소스로 변환한 다음 Azure Cosmos DB에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-124">**HL7-FHIR-Mapping app**: Receives the HL7 C-CDA document, transforms it to the FHIR Resource, then saves it to Azure Cosmos DB.</span></span>
2. <span data-ttu-id="7eaf3-125">**EHR 앱**: Azure Cosmos DB FHIR 리포지토리를 쿼리하고 해당 응답을 Service Bus 큐에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-125">**EHR app**: Queries the Azure Cosmos DB FHIR repository and saves the response to a Service Bus queue.</span></span> <span data-ttu-id="7eaf3-126">이 논리 앱에서는 [API 앱](#api-app)을 사용하여 새롭고 변경된 문서를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-126">This logic app uses an [API app](#api-app) to retrieve new and changed documents.</span></span>
3. <span data-ttu-id="7eaf3-127">**프로세스 알림 앱**: 본문에 FHIR 리소스 문서가 포함된 전자 메일 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-127">**Process notification app**: Sends an email notification with the FHIR resource documents in the body.</span></span>

![이 HL7 FHIR 의료 솔루션에 사용된 세 가지 Logic Apps](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-the-solution"></a><span data-ttu-id="7eaf3-129">솔루션에 사용된 Azure 서비스</span><span class="sxs-lookup"><span data-stu-id="7eaf3-129">Azure services used in the solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="7eaf3-130">Azure Cosmos DB DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="7eaf3-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="7eaf3-131">Azure Cosmos DB는 다음 그림과 같이 FHIR 리소스에 대한 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-131">Azure Cosmos DB is the repository for the FHIR resources as shown in the following figure.</span></span>

![이 HL7 FHIR 의료 자습서에서 사용된 Azure Cosmos DB 계정](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="7eaf3-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="7eaf3-133">Logic Apps</span></span>
<span data-ttu-id="7eaf3-134">Logic Apps는 워크플로 프로세스를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-134">Logic Apps handle the workflow process.</span></span> <span data-ttu-id="7eaf3-135">다음 스크린샷은 이 솔루션용으로 만든 Logic Apps를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-135">The following screenshots show the Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="7eaf3-136">**HL7-FHIR-매핑 앱**: Logic Apps용 엔터프라이즈 통합 팩을 사용하여 HL7 C-CDA 문서를 수신하고 FHIR 리소스로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-136">**HL7-FHIR-Mapping app**: Receive the HL7 C-CDA document and transform it to an FHIR resource using the Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="7eaf3-137">엔터프라이즈 통합 팩은 C-CDA에서 FHIR 리소스로의 매핑을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-137">The Enterprise Integration Pack handles the mapping from the C-CDA to FHIR resources.</span></span>

    ![HL7 FHIR 의료 레코드를 수신하는 데 사용한 논리 앱](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="7eaf3-139">**EHR 앱**: Azure Cosmos DB FHIR 리포지토리를 쿼리하고 해당 응답을 Service Bus 큐에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-139">**EHR app**: Query the Azure Cosmos DB FHIR repository and save the response to a Service Bus queue.</span></span> <span data-ttu-id="7eaf3-140">GetNewOrModifiedFHIRDocuments 앱에 대한 코드는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-140">The code for the GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![Azure Cosmos DB를 쿼리하는 데 사용한 논리 앱](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="7eaf3-142">**프로세스 알림 앱**: 본문에 FHIR 리소스 문서가 포함된 전자 메일 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-142">**Process notification app**: Send an email notification with the FHIR resource documents in the body.</span></span>

    ![본문에 HL7 FHIR 리소스가 포함된 환자 전자 메일을 보내는 논리 앱](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="7eaf3-144">서비스 버스</span><span class="sxs-lookup"><span data-stu-id="7eaf3-144">Service Bus</span></span>
<span data-ttu-id="7eaf3-145">다음 그림에서는 환자 큐를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-145">The following figure shows the patients queue.</span></span> <span data-ttu-id="7eaf3-146">태그 속성 값은 전자 메일 제목에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-146">The Tag property value is used for the email subject.</span></span>

![이 HL7 FHIR 자습서에서 사용한 Service Bus 큐](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="7eaf3-148">API 앱</span><span class="sxs-lookup"><span data-stu-id="7eaf3-148">API app</span></span>
<span data-ttu-id="7eaf3-149">API 앱은 Azure Cosmos DB에 연결해서 리소스 유형별로 새롭거나 수정된 FHIR 문서를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-149">An API app connects to Azure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="7eaf3-150">이 앱에는 하나의 작업 **GetNewOrModifiedFhirDocuments**가 있는 하나의 컨트롤러 **FhirNotificationApi**가 있습니다. [API 앱의 소스](#api-app-source)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="7eaf3-151">Azure Cosmos DB DocumentDB .NET API에서 [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) 클래스를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-151">We are using the [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from the Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="7eaf3-152">자세한 내용은 [변경 사항 피드 문서](change-feed.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-152">For more information, see the [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="7eaf3-153">GetNewOrModifiedFhirDocuments 작업</span><span class="sxs-lookup"><span data-stu-id="7eaf3-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="7eaf3-154">**입력**</span><span class="sxs-lookup"><span data-stu-id="7eaf3-154">**Inputs**</span></span>
- <span data-ttu-id="7eaf3-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="7eaf3-155">DatabaseId</span></span>
- <span data-ttu-id="7eaf3-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="7eaf3-156">CollectionId</span></span>
- <span data-ttu-id="7eaf3-157">HL7 FHIR 리소스 종류 이름</span><span class="sxs-lookup"><span data-stu-id="7eaf3-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="7eaf3-158">부울: 처음부터 시작</span><span class="sxs-lookup"><span data-stu-id="7eaf3-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="7eaf3-159">Int: 반환된 문서 수</span><span class="sxs-lookup"><span data-stu-id="7eaf3-159">Int: Number of documents returned</span></span>

<span data-ttu-id="7eaf3-160">**Outputs**</span><span class="sxs-lookup"><span data-stu-id="7eaf3-160">**Outputs**</span></span>
- <span data-ttu-id="7eaf3-161">성공: 상태 코드: 200, 응답: 문서 목록(JSON 배열)</span><span class="sxs-lookup"><span data-stu-id="7eaf3-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="7eaf3-162">실패: 상태 코드: 404, 응답: "'*resource name'* 리소스 유형에 대한 문서를 찾을 수 없음"</span><span class="sxs-lookup"><span data-stu-id="7eaf3-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="7eaf3-163">**API 앱에 대한 원본**</span><span class="sxs-lookup"><span data-stu-id="7eaf3-163">**Source for the API app**</span></span>

```C#

    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web.Http;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Swashbuckle.Swagger.Annotations;
    using TRex.Metadata;
    
    namespace FhirNotificationApi.Controllers
    {
        /// <summary>
        ///     FHIR Resource Type Controller
        /// </summary>
        /// <seealso cref="System.Web.Http.ApiController" />
        public class FhirResourceTypeController : ApiController
        {
            /// <summary>
            ///     Gets the new or modified FHIR documents from Last Run Date 
            ///     or create date of the collection
            /// </summary>
            /// <param name="databaseId"></param>
            /// <param name="collectionId"></param>
            /// <param name="resourceType"></param>
            /// <param name="startfromBeginning"></param>
            /// <param name="maximumItemCount">-1 returns all (default)</param>
            /// <returns></returns>
            [Metadata("Get New or Modified FHIR Documents",
                "Query for new or modifed FHIR Documents By Resource Type " +
                "from Last Run Date or Begining of Collection creation"
            )]
            [SwaggerResponse(HttpStatusCode.OK, type: typeof(Task<dynamic>))]
            [SwaggerResponse(HttpStatusCode.NotFound, "No New or Modifed Documents found")]
            [SwaggerOperation("GetNewOrModifiedFHIRDocuments")]
            public async Task<dynamic> GetNewOrModifiedFhirDocuments(
                [Metadata("Database Id", "Database Id")] string databaseId,
                [Metadata("Collection Id", "Collection Id")] string collectionId,
                [Metadata("Resource Type", "FHIR resource type name")] string resourceType,
                [Metadata("Start from Beginning ", "Change Feed Option")] bool startfromBeginning,
                [Metadata("Maximum Item Count", "Number of documents returned. '-1 returns all' (default)")] int maximumItemCount = -1
            )
            {
                var collectionLink = UriFactory.CreateDocumentCollectionUri(databaseId, collectionId);
    
                var context = new DocumentDbContext();  
    
                var docs = new List<dynamic>();
    
                var partitionKeyRanges = new List<PartitionKeyRange>();
                FeedResponse<PartitionKeyRange> pkRangesResponse;
    
                do
                {
                    pkRangesResponse = await context.Client.ReadPartitionKeyRangeFeedAsync(collectionLink);
                    partitionKeyRanges.AddRange(pkRangesResponse);
                } while (pkRangesResponse.ResponseContinuation != null);
    
                foreach (var pkRange in partitionKeyRanges)
                {
                    var changeFeedOptions = new ChangeFeedOptions
                    {
                        StartFromBeginning = startfromBeginning,
                        RequestContinuation = null,
                        MaxItemCount = maximumItemCount,
                        PartitionKeyRangeId = pkRange.Id
                    };
    
                    using (var query = context.Client.CreateDocumentChangeFeedQuery(collectionLink, changeFeedOptions))
                    {
                        do
                        {
                            if (query != null)
                            {
                                var results = await query.ExecuteNextAsync<dynamic>().ConfigureAwait(false);
                                if (results.Count > 0)
                                    docs.AddRange(results.Where(doc => doc.resourceType == resourceType));
                            }
                            else
                            {
                                throw new HttpResponseException(new HttpResponseMessage(HttpStatusCode.NotFound));
                            }
                        } while (query.HasMoreResults);
                    }
                }
                if (docs.Count > 0)
                    return docs;
                var msg = new StringContent("No documents found for " + resourceType + " Resource");
                var response = new HttpResponseMessage
                {
                    StatusCode = HttpStatusCode.NotFound,
                    Content = msg
                };
                return response;
            }
        }
    }
    
```

### <a name="testing-the-fhirnotificationapi"></a><span data-ttu-id="7eaf3-164">FhirNotificationApi 테스트</span><span class="sxs-lookup"><span data-stu-id="7eaf3-164">Testing the FhirNotificationApi</span></span> 

<span data-ttu-id="7eaf3-165">다음 이미지는 [FhirNotificationApi](#api-app-source)를 테스트하기 위해 Swagger가 사용되는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-165">The following image demonstrates how swagger was used to to test the [FhirNotificationApi](#api-app-source).</span></span>

![API 앱을 테스트하는 데 사용한 Swagger 파일](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="7eaf3-167">Azure 포털 대시보드</span><span class="sxs-lookup"><span data-stu-id="7eaf3-167">Azure portal dashboard</span></span>

<span data-ttu-id="7eaf3-168">다음 이미지는 Azure Portal에서 실행되는 이 솔루션에 대한 모든 Azure 서비스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-168">The following image shows all of the Azure services for this solution running in the Azure portal.</span></span>

![이 HL7 FHIR 자습서에서 사용한 모든 서비스를 보여 주는 Azure Portal](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="7eaf3-170">요약</span><span class="sxs-lookup"><span data-stu-id="7eaf3-170">Summary</span></span>

- <span data-ttu-id="7eaf3-171">Azure Cosmos DB에서 새롭거나 수정된 문서에 대한 알림이 기본 지원되고 이 기능이 얼마나 사용하기 쉬운지 알게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is to use.</span></span> 
- <span data-ttu-id="7eaf3-172">Logic Apps를 활용하여 코드를 쓰지 않아도 워크플로를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="7eaf3-173">Azure Service Bus 큐를 사용하여 HL7 FHIR 문서 배포 처리</span><span class="sxs-lookup"><span data-stu-id="7eaf3-173">Using Azure Service Bus Queues to handle the distribution for the HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7eaf3-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7eaf3-174">Next steps</span></span>
<span data-ttu-id="7eaf3-175">Azure Cosmos DB에 대한 자세한 내용은 [Azure Cosmos DB 홈페이지](https://azure.microsoft.com/services/cosmos-db/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-175">For more information about Azure Cosmos DB, see the [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="7eaf3-176">Logic Apps에 대한 자세한 내용은 [Logic Apps](https://azure.microsoft.com/services/logic-apps/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7eaf3-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


