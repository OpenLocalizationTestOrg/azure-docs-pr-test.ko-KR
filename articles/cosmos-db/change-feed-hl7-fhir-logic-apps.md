---
title: "HL7 FHIR 리소스-Azure Cosmos DB에 대 한 피드 aaaChange | Microsoft Docs"
description: "Azure 논리 앱, Azure Cosmos DB 및 서비스 버스를 사용 하 여 HL7 FHIR 환자 의료 레코드에 대 한 알림을 tooset를 변경 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: d2809bf5c6d8c193c49438d20684c56caea646bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="e0318-104">Logic Apps 및 Azure Cosmos DB를 사용하여 환자에게 HL7 FHIR 의료 기록 변경 통지</span><span class="sxs-lookup"><span data-stu-id="e0318-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="e0318-105">Azure MVP Howard Edidin tooadd 새 기능 tootheir 환자 포털 지정 하려는 의료 조직에서 최근에 연결 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted tooadd new functionality tootheir patient portal.</span></span> <span data-ttu-id="e0318-106">해당 상태 레코드가 업데이트 되었는지 환자 toobe 수 toosubscribe toothese 업데이트 필요할 때 필요할 toosend 알림 toopatients 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-106">They needed toosend notifications toopatients when their health record was updated, and they needed patients toobe able toosubscribe toothese updates.</span></span> 

<span data-ttu-id="e0318-107">이 문서에서는 Azure Cosmos DB, 논리 앱 및 서비스 버스를 사용 하 여이 의료 조직에 대해 생성 하는 hello 변경 피드 알림 솔루션을 통해 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-107">This article walks through hello change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="e0318-108">프로젝트 요구 사항</span><span class="sxs-lookup"><span data-stu-id="e0318-108">Project requirements</span></span>
- <span data-ttu-id="e0318-109">공급자는 XML 형식으로 HL7 통합-임상 문서 아키텍처(C-CDA) 문서를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="e0318-110">C-CDA 문서는 가족 이력, 예방접종 기록 등의 임상 문서는 물론 관리, 워크플로 및 재무 서류를 포함한 모든 유형의 임상 문서를 포괄하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="e0318-111">C CDA 문서 너무 변환할지[HL7 FHIR 리소스](http://hl7.org/fhir/2017Jan/resourcelist.html) JSON 형식에서입니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-111">C-CDA documents are converted too[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="e0318-112">수정된 FHIR 리소스 문서는 JSON 형식으로 전자 메일을 통해 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="e0318-113">솔루션 워크플로</span><span class="sxs-lookup"><span data-stu-id="e0318-113">Solution workflow</span></span> 

<span data-ttu-id="e0318-114">상위 수준 hello 프로젝트 hello 워크플로 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-114">At a high level, hello project required hello following workflow steps:</span></span> 
1. <span data-ttu-id="e0318-115">C CDA 문서 tooFHIR 리소스를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-115">Convert C-CDA documents tooFHIR resources.</span></span>
2. <span data-ttu-id="e0318-116">수정된 FHIR 리소스에 대한 반복 트리거 폴링을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="e0318-117">새롭거나 수정 된 문서에 대 한 사용자 지정 응용 프로그램, FhirNotificationApi, tooconnect tooAzure Cosmos DB 및 쿼리를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-117">Call a custom app, FhirNotificationApi, tooconnect tooAzure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="e0318-118">Hello 응답 tootoohello 서비스 버스 큐를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-118">Save hello response tootoohello Service Bus queue.</span></span>
4. <span data-ttu-id="e0318-119">Hello 서비스 버스 큐에서 새 메시지에 대 한 설문 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-119">Poll for new messages in hello Service Bus queue.</span></span>
5. <span data-ttu-id="e0318-120">전자 메일 알림을 toopatients를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-120">Send email notifications toopatients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="e0318-121">솔루션 아키텍처</span><span class="sxs-lookup"><span data-stu-id="e0318-121">Solution architecture</span></span>
<span data-ttu-id="e0318-122">이 솔루션에는 세 가지 논리 앱 toomeet hello 요구 사항 및 전체 hello 솔루션 워크플로 위에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-122">This solution requires three Logic Apps toomeet hello above requirements and complete hello solution workflow.</span></span> <span data-ttu-id="e0318-123">세 개의 논리 앱 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-123">hello three logic apps are:</span></span>
1. <span data-ttu-id="e0318-124">**HL7 FHIR 매핑 앱**: hello HL7 C CDA 문서를 수신한를 toohello FHIR 리소스 변환 다음 tooAzure Cosmos DB 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-124">**HL7-FHIR-Mapping app**: Receives hello HL7 C-CDA document, transforms it toohello FHIR Resource, then saves it tooAzure Cosmos DB.</span></span>
2. <span data-ttu-id="e0318-125">**EHR 앱**: hello Azure Cosmos DB FHIR 저장소를 쿼리하고 hello 응답 tooa 서비스 버스 큐를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-125">**EHR app**: Queries hello Azure Cosmos DB FHIR repository and saves hello response tooa Service Bus queue.</span></span> <span data-ttu-id="e0318-126">이 논리 앱에서 사용 하는 [API 앱](#api-app) tooretrieve 새로운 기능과 변경 된 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-126">This logic app uses an [API app](#api-app) tooretrieve new and changed documents.</span></span>
3. <span data-ttu-id="e0318-127">**알림 응용 프로그램 프로세스**: hello 본문에 hello FHIR 리소스 문서와 전자 메일 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-127">**Process notification app**: Sends an email notification with hello FHIR resource documents in hello body.</span></span>

![이 HL7 FHIR 의료 솔루션에서 사용 하는 hello 3 논리 앱](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a><span data-ttu-id="e0318-129">Hello 솔루션에서 사용 되는 azure 서비스</span><span class="sxs-lookup"><span data-stu-id="e0318-129">Azure services used in hello solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="e0318-130">Azure Cosmos DB DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="e0318-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="e0318-131">Hello 다음 그림에에서 나와 있는 것 처럼 azure Cosmos DB는 hello FHIR 리소스에 대 한 hello 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-131">Azure Cosmos DB is hello repository for hello FHIR resources as shown in hello following figure.</span></span>

![이 HL7 FHIR 의료 자습서에 사용 되는 hello Azure Cosmos DB 계정](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="e0318-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e0318-133">Logic Apps</span></span>
<span data-ttu-id="e0318-134">논리 앱 hello 워크플로 프로세스를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-134">Logic Apps handle hello workflow process.</span></span> <span data-ttu-id="e0318-135">hello 다음 스크린샷에서 보여 hello 논리 앱이이 솔루션에 대해 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-135">hello following screenshots show hello Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="e0318-136">**HL7 FHIR 매핑 앱**: hello HL7 C CDA 문서를 수신 하 고 엔터프라이즈 통합 팩 hello를 사용 하 여 논리 앱에 대 한 tooan FHIR 리소스를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-136">**HL7-FHIR-Mapping app**: Receive hello HL7 C-CDA document and transform it tooan FHIR resource using hello Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="e0318-137">엔터프라이즈 통합 팩 hello C CDA tooFHIR 리소스 hello에서 매핑 hello를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-137">hello Enterprise Integration Pack handles hello mapping from hello C-CDA tooFHIR resources.</span></span>

    ![tooreceive HL7 FHIR 의료 레코드를 사용 하는 hello 논리 앱](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="e0318-139">**EHR 앱**: hello Azure Cosmos DB FHIR 저장소를 쿼리하고 저장 hello 응답 tooa 서비스 버스 큐에 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-139">**EHR app**: Query hello Azure Cosmos DB FHIR repository and save hello response tooa Service Bus queue.</span></span> <span data-ttu-id="e0318-140">hello GetNewOrModifiedFHIRDocuments 앱에 대 한 hello 코드 보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-140">hello code for hello GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![tooquery Azure Cosmos DB를 사용 하는 hello 논리 앱](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="e0318-142">**알림 응용 프로그램 프로세스**: hello 본문에 hello FHIR 리소스 문서와 전자 메일 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-142">**Process notification app**: Send an email notification with hello FHIR resource documents in hello body.</span></span>

    ![hello hello 본문에 hello HL7 FHIR 리소스와 환자 전자 메일을 보내면 논리 앱](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="e0318-144">서비스 버스</span><span class="sxs-lookup"><span data-stu-id="e0318-144">Service Bus</span></span>
<span data-ttu-id="e0318-145">다음 그림에서는 hello 환자 큐 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-145">hello following figure shows hello patients queue.</span></span> <span data-ttu-id="e0318-146">Tag 속성 값 hello hello 메일 제목에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-146">hello Tag property value is used for hello email subject.</span></span>

![hello이 HL7 FHIR 자습서에 사용 되는 서비스 버스 큐](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="e0318-148">API 앱</span><span class="sxs-lookup"><span data-stu-id="e0318-148">API app</span></span>
<span data-ttu-id="e0318-149">API 앱 tooAzure Cosmos DB 및 리소스 유형에 따라 새 또는 수정 된 FHIR 문서에 대 한 쿼리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-149">An API app connects tooAzure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="e0318-150">이 앱에는 하나의 작업 **GetNewOrModifiedFhirDocuments**가 있는 하나의 컨트롤러 **FhirNotificationApi**가 있습니다. [API 앱의 소스](#api-app-source)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0318-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="e0318-151">Hello 사용 하 여 [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) hello Azure Cosmos DB DocumentDB.NET API에서에서 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-151">We are using hello [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from hello Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="e0318-152">자세한 내용은 참조 hello [변경 피드 문서](change-feed.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-152">For more information, see hello [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="e0318-153">GetNewOrModifiedFhirDocuments 작업</span><span class="sxs-lookup"><span data-stu-id="e0318-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="e0318-154">**입력**</span><span class="sxs-lookup"><span data-stu-id="e0318-154">**Inputs**</span></span>
- <span data-ttu-id="e0318-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="e0318-155">DatabaseId</span></span>
- <span data-ttu-id="e0318-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="e0318-156">CollectionId</span></span>
- <span data-ttu-id="e0318-157">HL7 FHIR 리소스 종류 이름</span><span class="sxs-lookup"><span data-stu-id="e0318-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="e0318-158">부울: 처음부터 시작</span><span class="sxs-lookup"><span data-stu-id="e0318-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="e0318-159">Int: 반환된 문서 수</span><span class="sxs-lookup"><span data-stu-id="e0318-159">Int: Number of documents returned</span></span>

<span data-ttu-id="e0318-160">**Outputs**</span><span class="sxs-lookup"><span data-stu-id="e0318-160">**Outputs**</span></span>
- <span data-ttu-id="e0318-161">성공: 상태 코드: 200, 응답: 문서 목록(JSON 배열)</span><span class="sxs-lookup"><span data-stu-id="e0318-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="e0318-162">실패: 상태 코드: 404, 응답: "'*resource name'* 리소스 유형에 대한 문서를 찾을 수 없음"</span><span class="sxs-lookup"><span data-stu-id="e0318-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="e0318-163">**Hello API 앱에 대 한 소스**</span><span class="sxs-lookup"><span data-stu-id="e0318-163">**Source for hello API app**</span></span>

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
            ///     Gets hello new or modified FHIR documents from Last Run Date 
            ///     or create date of hello collection
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

### <a name="testing-hello-fhirnotificationapi"></a><span data-ttu-id="e0318-164">테스트 FhirNotificationApi 문자열</span><span class="sxs-lookup"><span data-stu-id="e0318-164">Testing hello FhirNotificationApi</span></span> 

<span data-ttu-id="e0318-165">hello 다음 이미지에서는 swagger 사용된 tootootest hello 어 떠 [FhirNotificationApi](#api-app-source)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-165">hello following image demonstrates how swagger was used tootootest hello [FhirNotificationApi](#api-app-source).</span></span>

![tootest hello API 앱을 사용 하는 hello Swagger 파일](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="e0318-167">Azure 포털 대시보드</span><span class="sxs-lookup"><span data-stu-id="e0318-167">Azure portal dashboard</span></span>

<span data-ttu-id="e0318-168">다음 이미지는 hello hello Azure 포털에서에서 실행 되는이 솔루션에 대 한 Azure 서비스에 모든 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-168">hello following image shows all of hello Azure services for this solution running in hello Azure portal.</span></span>

![hello이 HL7 FHIR 자습서에 사용 되는 모든 hello 서비스를 표시 하는 Azure 포털](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="e0318-170">요약</span><span class="sxs-lookup"><span data-stu-id="e0318-170">Summary</span></span>

- <span data-ttu-id="e0318-171">Azure Cosmos DB에는 새 알림에 대 한 기본 지원 또는 수정 된 문서와 얼마나 쉬운지 toouse 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is toouse.</span></span> 
- <span data-ttu-id="e0318-172">Logic Apps를 활용하여 코드를 쓰지 않아도 워크플로를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="e0318-173">Azure 서비스 버스 큐 toohandle hello 분포를 사용 하 여 hello HL7 FHIR 문서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-173">Using Azure Service Bus Queues toohandle hello distribution for hello HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0318-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0318-174">Next steps</span></span>
<span data-ttu-id="e0318-175">Azure Cosmos DB에 대 한 자세한 내용은 참조 hello [Azure Cosmos DB 홈 페이지](https://azure.microsoft.com/services/cosmos-db/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0318-175">For more information about Azure Cosmos DB, see hello [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="e0318-176">Logic Apps에 대한 자세한 내용은 [Logic Apps](https://azure.microsoft.com/services/logic-apps/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0318-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


