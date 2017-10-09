---
title: "aaaScheduler 아웃 바운드 인증"
description: "스케줄러 아웃바운드 인증"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a>스케줄러 아웃바운드 인증
스케줄러 작업 toocall 인증이 필요한 tooservices 아웃 해야 합니다. 이러한 방식으로 호출된 된 서비스 hello 스케줄러 작업 리소스에 액세스할 수 있는지 확인할 수 있습니다. 이러한 서비스 중 일부에는 다른 Azure 서비스, Salesforce.com, Facebook 및 보안 사용자 지정 웹사이트가 포함됩니다.

## <a name="adding-and-removing-authentication"></a>인증 추가 및 제거
추가 인증 tooa 스케줄러 작업은 간단-JSON 자식 요소를 추가 `authentication` toohello `request` 만들거나 작업을 업데이트할 때 요소입니다. 전달 되는 암호 toohello 스케줄러 서비스 – PUT, PATCH 또는 POST 요청에 hello의 일부로 `authentication` 개체 – 응답에서 반환 되지 않습니다. 응답에서는 비밀 정보 toonull 설정 되거나 인증 hello 엔터티를 나타내는 공용 토큰을 가질 수 있습니다.

tooremove 인증 하거나 hello 작업을 명시적으로 패치 하 여 hello 설정 `authentication` toonull 개체입니다. 응답에는 인증 속성이 하나도 표시되지 않습니다.

현재 지원만 hello 인증 유형에 hello `ClientCertificate` (사용 하 여 모델 hello SSL/TLS 클라이언트 인증서), hello `Basic` (기본 인증의 경우)에 대 한 모델 및 hello `ActiveDirectoryOAuth` 모델 (Active Directory OAuth 인증용)입니다.

## <a name="request-body-for-clientcertificate-authentication"></a>ClientCertificate 인증에 대한 요청 본문
Hello를 사용 하 여 인증을 추가할 때 `ClientCertificate` 모델을 hello hello 요청 본문의 추가 요소에 다음을 지정 합니다.  

| 요소 | 설명 |
|:--- |:--- |
| *인증(부모 요소)* |SSL 클라이언트 인증서를 사용하기 위한 인증 개체 입니다. |
| *type* |필수입니다. 인증 유형입니다. SSL 클라이언트 인증서에 대 한 hello 값 이어야 합니다 `ClientCertificate`합니다. |
| *pfx* |필수입니다. Hello PFX 파일의 Base64 인코딩 콘텐츠입니다. |
| *암호* |필수입니다. Tooaccess hello PFX 파일 암호입니다. |

## <a name="response-body-for-clientcertificate-authentication"></a>ClientCertificate 인증에 대한 응답 본문
요청 인증 정보와 함께 보내면 hello 응답 hello 다음 인증 관련 요소가 포함 됩니다.

| 요소 | 설명 |
|:--- |:--- |
| *인증(부모 요소)* |SSL 클라이언트 인증서를 사용하기 위한 인증 개체 입니다. |
| *type* |인증 유형입니다. SSL 클라이언트 인증서 hello 값은 `ClientCertificate`합니다. |
| *certificateThumbprint* |hello 인증서의 지문 안녕하세요입니다. |
| *certificateSubjectName* |hello 인증서의 hello 주체의 고유 이름입니다. |
| *certificateExpiration* |hello hello 인증서의 만료 날짜입니다. |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a>ClientCertificate 인증에 대한 샘플 REST 요청
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a>ClientCertificate 인증에 대한 샘플 REST 응답
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a>기본 인증의 요청 본문
Hello를 사용 하 여 인증을 추가할 때 `Basic` 모델을 hello hello 요청 본문의 추가 요소에 다음을 지정 합니다.

| 요소 | 설명 |
|:--- |:--- |
| *인증(부모 요소)* |기본 인증을 사용 하기 위한 인증 개체입니다. |
| *type* |필수입니다. 인증 유형입니다. 기본 인증에 대 한 hello 값 이어야 합니다 `Basic`합니다. |
| *사용자 이름* |필수입니다. 사용자 이름 tooauthenticate 합니다. |
| *암호* |필수입니다. 암호 tooauthenticate 합니다. |

## <a name="response-body-for-basic-authentication"></a>기본 인증의 응답 본문
요청 인증 정보와 함께 보내면 hello 응답 hello 다음 인증 관련 요소가 포함 됩니다.

| 요소 | 설명 |
|:--- |:--- |
| *인증(부모 요소)* |기본 인증을 사용 하기 위한 인증 개체입니다. |
| *type* |인증 유형입니다. 기본 인증을 hello 값은 `Basic`합니다. |
| *사용자 이름* |hello 인증 사용자 이름. |

## <a name="sample-rest-request-for-basic-authentication"></a>기본 인증에 대한 샘플 REST 요청
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a>기본 인증에 대한 샘플 REST 응답
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a>ActiveDirectoryOAuth 인증의 요청 본문
Hello를 사용 하 여 인증을 추가할 때 `ActiveDirectoryOAuth` 모델을 hello hello 요청 본문의 추가 요소에 다음을 지정 합니다.

| 요소 | 설명 |
|:--- |:--- |
| *인증(부모 요소)* |ActiveDirectoryOAuth 인증을 사용하기 위한 인증 개체입니다. |
| *type* |필수입니다. 인증 유형입니다. ActiveDirectoryOAuth 인증에 대 한 hello 값 이어야 합니다 `ActiveDirectoryOAuth`합니다. |
| *테넌트* |필수입니다. hello hello Azure AD 테 넌 트에 대 한 테 넌 트 식별자입니다. |
| *대상* |필수입니다. 이 toohttps://management.core.windows.net/를 설정 됩니다. |
| *clientId* |필수입니다. Hello Azure AD 응용 프로그램에 대 한 hello 클라이언트 식별자를 제공 합니다. |
| *암호* |필수입니다. Hello 토큰을 요청 하는 hello 클라이언트의 암호입니다. |

### <a name="determining-your-tenant-identifier"></a>테넌트 식별자 확인
실행 하 여 hello Azure AD 테 넌 트에 대 한 hello 테 넌 트 식별자를 찾을 수 있습니다 `Get-AzureAccount` Azure PowerShell에서 합니다.

## <a name="response-body-for-activedirectoryoauth-authentication"></a>ActiveDirectoryOAuth 인증의 응답 본문
요청 인증 정보와 함께 보내면 hello 응답 hello 다음 인증 관련 요소가 포함 됩니다.

| 요소 | 설명 |
|:--- |:--- |
| *인증(부모 요소)* |ActiveDirectoryOAuth 인증을 사용하기 위한 인증 개체입니다. |
| *type* |인증 유형입니다. ActiveDirectoryOAuth 인증 hello 값은 `ActiveDirectoryOAuth`합니다. |
| *테넌트* |hello hello Azure AD 테 넌 트에 대 한 테 넌 트 식별자입니다. |
| *대상* |이 toohttps://management.core.windows.net/를 설정 됩니다. |
| *clientId* |hello hello Azure AD 응용 프로그램에 대 한 클라이언트 식별자입니다. |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a>ActiveDirectoryOAuth 인증에 대한 샘플 REST 요청
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a>ActiveDirectoryOAuth 인증에 대한 샘플 REST 응답
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a>참고 항목
 [스케줄러란?](scheduler-intro.md)

 [Azure 스케줄러 개념, 용어 및 엔터티 계층 구조](scheduler-concepts-terms.md)

 [Hello Azure 포털에서에서 스케줄러 사용 시작](scheduler-get-started-portal.md)

 [Azure 스케줄러의 버전 및 요금 청구](scheduler-plans-billing.md)

 [Azure 스케줄러 REST API 참조](https://msdn.microsoft.com/library/mt629143)

 [Azure 스케줄러 PowerShell cmdlet 참조](scheduler-powershell-reference.md)

 [Azure 스케줄러 고가용성 및 안정성](scheduler-high-availability-reliability.md)

 [Azure 스케줄러 제한, 기본값 및 오류 코드](scheduler-limits-defaults-errors.md)

