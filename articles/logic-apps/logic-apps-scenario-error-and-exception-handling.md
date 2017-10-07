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
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a>시나리오: 논리 앱에 대한 예외 처리 및 오류 로깅

이 시나리오에서는 논리 앱 toobetter 지원 예외 처리를 확장 하는 방법을 설명 합니다. 실제 사용 사례 tooanswer hello 질문을 사용 했습니다: "Azure 논리 앱에서는 예외 및 오류 처리?"

> [!NOTE]
> 현재 Azure 논리 앱 스키마 hello 작업 응답에 대 한 표준 서식 파일을 제공합니다. 이 템플릿은 API 앱에서 반환된 내부 유효성 검사 및 오류 응답을 모두 포함합니다.

## <a name="scenario-and-use-case-overview"></a>시나리오 및 사용 사례 개요

이 시나리오에 대 한 사용 사례 hello로 hello 스토리 다음과 같습니다. 

잘 알려진 의료 조직 참여 toodevelop Microsoft Dynamics CRM Online을 사용 하 여 환자 포털을 만들 수 있는 Azure 솔루션 주세요. Dynamics CRM Online 환자 포털 hello와 Salesforce 사이의 toosend 약속 레코드 필요할 합니다. 이전 피드백 toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) 환자 모든 레코드에 대 한 표준입니다.

hello 프로젝트에는 두 가지 주요 요구 사항이 있었습니다.  

* Dynamics CRM Online 포털 hello에서 보낸 메서드 toolog 레코드
* 방식으로 tooview hello 워크플로 내에서 발생 한 오류

> [!TIP]
> 이 프로젝트에 대 한 높은 수준의 비디오를 참조 하십시오. [통합 사용자 그룹](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "통합 사용자 그룹")합니다.

## <a name="how-we-solved-hello-problem"></a>Hello 문제 문제

선택한 이유 [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") (Cosmos DB에서 참조 한 문서로 toorecords) hello 로그 및 오류 레코드에 대 한 리포지토리로 합니다. Azure 논리 앱 모든 응답에 대 한 표준 서식 파일을 사용 하므로 우리는 스키마를 없는 toocreate 사용자 지정 합니다. API 앱 너무 만들 수**삽입** 및 **쿼리** 오류와 로그 레코드에 대 한 합니다. Hello API 앱 내에서 각각에 대 한 스키마를 정의할 수도 있습니다.  

또 다른 요구 사항은 특정 날짜 이후에 toopurge 레코드 했습니다. Cosmos DB에 라는 속성이 [tooLive 시간](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "tooLive 시간") (TTL) 허용 되 면 us tooset는 **시간 tooLive** 각 레코드 또는 컬렉션에 대 한 값입니다. 이 기능은 hello 필요 toomanually 레코드를 삭제 Cosmos DB에서 제거 되었습니다.

> [!IMPORTANT]
> toocomplete이이 자습서에서는 toocreate Cosmos DB 데이터베이스와 두 개의 컬렉션 (로깅 및 오류)가 필요 합니다.

## <a name="create-hello-logic-app"></a>Hello 논리 앱 만들기

hello 첫 단계는 toocreate hello 논리 앱 및 논리 응용 프로그램 디자이너에서 열려 hello 응용 프로그램입니다. 이 예제에서는 부모-자식 논리 앱을 사용합니다. Hello 부모를 이미 만든 것 및 toocreate 하나의 자식 논리 앱 하려는 가정해 보겠습니다.

Dynamics CRM Online에서 들어오는 toolog hello 레코드, 하겠습니다 때문에 hello 맨 위에서 시작 해 보겠습니다. 사용 해야 합니다는 **요청** 않으므로 hello 부모 논리 앱이이 자식을 트리거합니다.

### <a name="logic-app-trigger"></a>논리 앱 트리거

사용 하는 **요청** hello 다음 예제와 같이 트리거:

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


## <a name="steps"></a>단계

Hello 환자 레코드의 hello 소스 (요청) hello Dynamics CRM Online 포털에서 로그인 해야 했습니다.

1. 먼저 Dynamics CRM Online에서 새 예약 기록을 가져와야 합니다.

   CRM에서 들어오는 hello 트리거 hello 제공 **CRM PatentId**, **레코드 종류**, **신규 또는 업데이트 된 레코드** (새 부울 값을 업데이트 하거나), 및  **SalesforceId**합니다. hello **SalesforceId** 는 업데이트에만 사용 하기 때문에 null 일 수 있습니다.
   Hello CRM 레코드 CRM hello를 사용 하 여 얻을 수 있는 **PatientID** 및 hello **레코드 종류**합니다.

2. 다음으로 필요한 tooadd DocumentDB API 앱 **InsertLogEntry** 논리가 응용 프로그램 디자이너에서 아래 그림과 같이 작업 합니다.

   **로그 항목 삽입**

   ![로그 항목 삽입](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   **오류 항목 삽입**

   ![로그 항목 삽입](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   **기록 만들기 실패에 대한 확인**

   ![조건](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a>논리 앱 소스 코드

> [!NOTE]
> 다음 예제는 hello에는 샘플만 있습니다. 이 자습서는 프로덕션 환경에서 이제 구현을 기반으로, 값의 hello는 **소스 노드** 관련된 tooscheduling 약속. 되는 속성이 표시 되지 않습니다 > 

### <a name="logging"></a>로깅

논리 앱 코드 다음 hello 샘플 표시 방법을 toohandle 로깅.

#### <a name="log-entry"></a>로그 항목

로그 항목을 삽입 하기 위한 hello 논리 앱 소스 코드는 다음과 같습니다.

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

#### <a name="log-request"></a>로그 요청

다음은 toohello API 앱을 게시 하는 hello 로그 요청 메시지입니다.

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


#### <a name="log-response"></a>로그 응답

Hello API 앱에서 hello 로그 응답 메시지는 다음과 같습니다.

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

이제 hello 오류 단계 처리를 살펴보겠습니다.

### <a name="error-handling"></a>오류 처리

hello 다음 논리 앱 코드 샘플에서는 오류 처리를 구현 하는 방법을

#### <a name="create-error-record"></a>오류 기록 만들기

오류 레코드를 만들기 위한 hello 논리 앱 소스 코드는 다음과 같습니다.

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

#### <a name="insert-error-into-cosmos-db--request"></a>Cosmos DB에 삽입 오류 - 요청

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

#### <a name="insert-error-into-cosmos-db--response"></a>Cosmos DB에 삽입 오류 - 응답

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

#### <a name="salesforce-error-response"></a>Salesforce 오류 응답

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

### <a name="return-hello-response-back-tooparent-logic-app"></a>Hello 응답 백 tooparent 논리 앱을 반환 합니다.

Hello 응답을 전달할 수 hello 응답을 가져온 후 뒤로 toohello 부모 논리 앱.

#### <a name="return-success-response-tooparent-logic-app"></a>성공 응답 tooparent 논리 앱을 반환 합니다.

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

#### <a name="return-error-response-tooparent-logic-app"></a>오류 응답 tooparent 논리 앱을 반환 합니다.

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


## <a name="cosmos-db-repository-and-portal"></a>Cosmos DB 리포지토리 및 포털

솔루션은 [Cosmos DB](https://azure.microsoft.com/services/documentdb)와 관련된 기능을 추가했습니다.

### <a name="error-management-portal"></a>오류 관리 포털

tooview hello 오류 Cosmos DB에서 MVC 웹 응용 프로그램 toodisplay hello 오류 레코드를 만들 수 있습니다. hello **목록**, **세부 정보**, **편집**, 및 **삭제** 작업 hello 현재 버전에 포함 됩니다.

> [!NOTE]
> 작업 편집: Cosmos DB hello 전체 문서를 대체 합니다. hello에 표시 된 레코드 hello **목록** 및 **세부** 뷰는 예제만 합니다. 실제 환자 예약 기록이 없습니다.

다음은 예제 MVC 앱의 hello를 사용 하 여 이전에 만든 세부 정보는 접근 방식을 설명 합니다.

#### <a name="error-management-list"></a>오류 관리 목록
![오류 목록](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a>오류 관리 세부 정보 보기
![오류 세부 정보](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a>로그 관리 포털

tooview hello 로그도 만들었는지 여부는 MVC 웹 응용 프로그램입니다. 다음은 예제 MVC 앱의 hello를 사용 하 여 이전에 만든 세부 정보는 접근 방식을 설명 합니다.

#### <a name="sample-log-detail-view"></a>샘플 로그 세부 정보 보기
![로그 세부 정보 보기](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a>API 앱 세부 정보

#### <a name="logic-apps-exception-management-api"></a>논리 앱 예외 관리 API

오픈 소스 Azure Logic Apps 예외 관리 API 앱은 여기에서 설명한 기능을 제공합니다. 두 개의 컨트롤러가 있습니다.

* **ErrorController** 는 DocumentDB 컬렉션에 오류 기록(문서)을 삽입합니다.
* **LogController** 는 DocumentDB 컬렉션에 로그 기록(문서)을 삽입합니다.

> [!TIP]
> 두 컨트롤러가 모두 사용 하 여 `async Task<dynamic>` 우리를 만들 수 있도록 런타임에 작업 tooresolve 허용 작업 hello hello 작업의 hello 본문에서 DocumentDB 스키마입니다. 
> 

DocumentDB의 모든 문서에는 고유한 ID가 있어야 합니다. 사용 하 여 `PatientId` 타임 스탬프 변환 tooa Unix 타임 스탬프 값 (double)을 추가 합니다. Hello 값 tooremove hello 소수 자릿수 값을 자릅니다.

오류 컨트롤러 API의 hello 소스 코드를 볼 수 있습니다 [GitHub에서](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs)합니다.

구문 다음 hello를 사용 하 여 논리 앱에서 API hello를 이라고 합니다.

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

hello hello에 대 한 코드 샘플 검사 앞에 식을 hello *Create_NewPatientRecord* 상태의 **실패**합니다.

## <a name="summary"></a>요약

* 논리 앱에서 로깅 및 오류 처리를 쉽게 구현할 수 있습니다.
* 로그 및 오류 레코드 (문서)에 대 한 DocumentDB hello 리포지토리로 사용할 수 있습니다.
* MVC toocreate 포털 toodisplay 로그 및 오류 레코드를 사용할 수 있습니다.

### <a name="source-code"></a>소스 코드

hello 논리 앱 예외 관리 API 응용 프로그램에 대 한 hello 소스 코드를이 사용할 수 있는 [GitHub 리포지토리](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "논리 앱 예외 관리 API")합니다.

## <a name="next-steps"></a>다음 단계

* [논리 앱 예제 및 시나리오 더 보기](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Logic Apps 모니터링에 대해 알아보기](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Logic Apps용 자동화된 배포 템플릿 만들기](../logic-apps/logic-apps-create-deploy-template.md)
