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
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a>Logic Apps 및 Azure Cosmos DB를 사용하여 환자에게 HL7 FHIR 의료 기록 변경 통지

Azure MVP Howard Edidin tooadd 새 기능 tootheir 환자 포털 지정 하려는 의료 조직에서 최근에 연결 않았습니다. 해당 상태 레코드가 업데이트 되었는지 환자 toobe 수 toosubscribe toothese 업데이트 필요할 때 필요할 toosend 알림 toopatients 합니다. 

이 문서에서는 Azure Cosmos DB, 논리 앱 및 서비스 버스를 사용 하 여이 의료 조직에 대해 생성 하는 hello 변경 피드 알림 솔루션을 통해 안내 합니다. 

## <a name="project-requirements"></a>프로젝트 요구 사항
- 공급자는 XML 형식으로 HL7 통합-임상 문서 아키텍처(C-CDA) 문서를 보냅니다. C-CDA 문서는 가족 이력, 예방접종 기록 등의 임상 문서는 물론 관리, 워크플로 및 재무 서류를 포함한 모든 유형의 임상 문서를 포괄하고 있습니다. 
- C CDA 문서 너무 변환할지[HL7 FHIR 리소스](http://hl7.org/fhir/2017Jan/resourcelist.html) JSON 형식에서입니다.
- 수정된 FHIR 리소스 문서는 JSON 형식으로 전자 메일을 통해 전송됩니다.

## <a name="solution-workflow"></a>솔루션 워크플로 

상위 수준 hello 프로젝트 hello 워크플로 단계를 수행 해야 합니다. 
1. C CDA 문서 tooFHIR 리소스를 변환 합니다.
2. 수정된 FHIR 리소스에 대한 반복 트리거 폴링을 수행합니다. 
2. 새롭거나 수정 된 문서에 대 한 사용자 지정 응용 프로그램, FhirNotificationApi, tooconnect tooAzure Cosmos DB 및 쿼리를 호출 합니다.
3. Hello 응답 tootoohello 서비스 버스 큐를 저장 합니다.
4. Hello 서비스 버스 큐에서 새 메시지에 대 한 설문 조사 합니다.
5. 전자 메일 알림을 toopatients를 보냅니다.

## <a name="solution-architecture"></a>솔루션 아키텍처
이 솔루션에는 세 가지 논리 앱 toomeet hello 요구 사항 및 전체 hello 솔루션 워크플로 위에 필요합니다. 세 개의 논리 앱 hello 됩니다.
1. **HL7 FHIR 매핑 앱**: hello HL7 C CDA 문서를 수신한를 toohello FHIR 리소스 변환 다음 tooAzure Cosmos DB 저장 합니다.
2. **EHR 앱**: hello Azure Cosmos DB FHIR 저장소를 쿼리하고 hello 응답 tooa 서비스 버스 큐를 저장 합니다. 이 논리 앱에서 사용 하는 [API 앱](#api-app) tooretrieve 새로운 기능과 변경 된 문서입니다.
3. **알림 응용 프로그램 프로세스**: hello 본문에 hello FHIR 리소스 문서와 전자 메일 알림을 보냅니다.

![이 HL7 FHIR 의료 솔루션에서 사용 하는 hello 3 논리 앱](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a>Hello 솔루션에서 사용 되는 azure 서비스

#### <a name="azure-cosmos-db-documentdb-api"></a>Azure Cosmos DB DocumentDB API
Hello 다음 그림에에서 나와 있는 것 처럼 azure Cosmos DB는 hello FHIR 리소스에 대 한 hello 리포지토리입니다.

![이 HL7 FHIR 의료 자습서에 사용 되는 hello Azure Cosmos DB 계정](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a>Logic Apps
논리 앱 hello 워크플로 프로세스를 처리 합니다. hello 다음 스크린샷에서 보여 hello 논리 앱이이 솔루션에 대해 생성 합니다. 


1. **HL7 FHIR 매핑 앱**: hello HL7 C CDA 문서를 수신 하 고 엔터프라이즈 통합 팩 hello를 사용 하 여 논리 앱에 대 한 tooan FHIR 리소스를 변환 합니다. 엔터프라이즈 통합 팩 hello C CDA tooFHIR 리소스 hello에서 매핑 hello를 처리 합니다.

    ![tooreceive HL7 FHIR 의료 레코드를 사용 하는 hello 논리 앱](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. **EHR 앱**: hello Azure Cosmos DB FHIR 저장소를 쿼리하고 저장 hello 응답 tooa 서비스 버스 큐에 대기 합니다. hello GetNewOrModifiedFHIRDocuments 앱에 대 한 hello 코드 보다 작습니다.

    ![tooquery Azure Cosmos DB를 사용 하는 hello 논리 앱](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. **알림 응용 프로그램 프로세스**: hello 본문에 hello FHIR 리소스 문서와 전자 메일 알림을 보냅니다.

    ![hello hello 본문에 hello HL7 FHIR 리소스와 환자 전자 메일을 보내면 논리 앱](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a>서비스 버스
다음 그림에서는 hello 환자 큐 번호입니다. Tag 속성 값 hello hello 메일 제목에 사용 됩니다.

![hello이 HL7 FHIR 자습서에 사용 되는 서비스 버스 큐](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a>API 앱
API 앱 tooAzure Cosmos DB 및 리소스 유형에 따라 새 또는 수정 된 FHIR 문서에 대 한 쿼리를 연결합니다. 이 앱에는 하나의 작업 **GetNewOrModifiedFhirDocuments**가 있는 하나의 컨트롤러 **FhirNotificationApi**가 있습니다. [API 앱의 소스](#api-app-source)를 참조하세요.

Hello 사용 하 여 [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) hello Azure Cosmos DB DocumentDB.NET API에서에서 클래스입니다. 자세한 내용은 참조 hello [변경 피드 문서](change-feed.md)합니다. 

##### <a name="getnewormodifiedfhirdocuments-operation"></a>GetNewOrModifiedFhirDocuments 작업

**입력**
- DatabaseId
- CollectionId
- HL7 FHIR 리소스 종류 이름
- 부울: 처음부터 시작
- Int: 반환된 문서 수

**Outputs**
- 성공: 상태 코드: 200, 응답: 문서 목록(JSON 배열)
- 실패: 상태 코드: 404, 응답: "'*resource name'* 리소스 유형에 대한 문서를 찾을 수 없음"

<a id="api-app-source"></a>

**Hello API 앱에 대 한 소스**

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

### <a name="testing-hello-fhirnotificationapi"></a>테스트 FhirNotificationApi 문자열 

hello 다음 이미지에서는 swagger 사용된 tootootest hello 어 떠 [FhirNotificationApi](#api-app-source)합니다.

![tootest hello API 앱을 사용 하는 hello Swagger 파일](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a>Azure 포털 대시보드

다음 이미지는 hello hello Azure 포털에서에서 실행 되는이 솔루션에 대 한 Azure 서비스에 모든 hello 표시 됩니다.

![hello이 HL7 FHIR 자습서에 사용 되는 모든 hello 서비스를 표시 하는 Azure 포털](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a>요약

- Azure Cosmos DB에는 새 알림에 대 한 기본 지원 또는 수정 된 문서와 얼마나 쉬운지 toouse 방법을 배웠습니다. 
- Logic Apps를 활용하여 코드를 쓰지 않아도 워크플로를 만들 수 있습니다.
- Azure 서비스 버스 큐 toohandle hello 분포를 사용 하 여 hello HL7 FHIR 문서에 대 한 합니다.

## <a name="next-steps"></a>다음 단계
Azure Cosmos DB에 대 한 자세한 내용은 참조 hello [Azure Cosmos DB 홈 페이지](https://azure.microsoft.com/services/cosmos-db/)합니다. Logic Apps에 대한 자세한 내용은 [Logic Apps](https://azure.microsoft.com/services/logic-apps/)를 참조하세요.


