---
title: "aaaUse 자동 크기 조정 작업 toosend 전자 메일 및 webhook 경고 알림입니다. | Microsoft Docs"
description: "Toouse 자동 크기 조정 작업 toocall 웹 Url 또는 Azure 모니터에서 전자 메일 알림을 보내는 방법을 참조 하십시오. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a>Azure 모니터에서 자동 크기 조정 작업 toosend 전자 메일 및 webhook 경고 알림 사용
이 문서에서는 Azure에서 크기 자동 조정 작업을 기준으로 특정 웹 URL을 호출하거나 전자 메일을 보낼 수 있도록 트리거를 설정하는 방법을 설명합니다.  

## <a name="webhooks"></a>Webhook
Webhook 사후 처리 또는 사용자 지정 알림을 tooroute hello Azure 경고 알림 tooother 시스템을 허용 합니다. 예를 들어는 들어오는 웹 요청 toosend SMS, 로그 버그를 처리할 수 있는 라우팅 hello 경고 tooservices 팀 채팅을 사용 하 여 또는 메시징 서비스 알림, 등 hello webhook URI는 유효한 HTTP 또는 HTTPS 끝점 이어야 합니다.

## <a name="email"></a>Email
전자 메일 tooany 유효한 전자 메일 주소를 보낼 수 있습니다. 관리자와 hello 규칙 실행 되 고 있는 hello 구독의 공동 관리자 알림을 받게 됩니다.

## <a name="cloud-services-and-web-apps"></a>클라우드 서비스 및 웹 앱
있습니다 수 옵트인 hello Azure 포털에서에서 클라우드 서비스 및 서버 팜 (웹 앱).

* Hello 선택 **하 여 확장할** 메트릭.

![배율 기준](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a>가상 컴퓨터 확장 집합
Resource Manager(가상 컴퓨터 확장 집합)로 만든 새 가상 컴퓨터의 경우 REST API, Resource Manager 템플릿, PowerShell 및 CLI를 사용하여 구성할 수 있습니다. 포털 인터페이스는 아직 제공되지 않습니다.
Hello REST API 또는 리소스 관리자 템플릿을 사용 하는 경우 다음 옵션 hello로 hello 알림을 요소를 포함 합니다.

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| 필드 | 필수? | 설명 |
| --- | --- | --- |
| operation |yes |값은 "Scale"이어야 합니다. |
| sendToSubscriptionAdministrator |yes |값은 "true" 또는 "false"여야 합니다. |
| sendToSubscriptionCoAdministrators |yes |값은 "true" 또는 "false"여야 합니다. |
| customEmails |yes |값에 null [] 또는 전자 메일 문자열 배열을 사용할 수 있습니다. |
| Webhook |yes |값은 null이거나 올바른 URI일 수 있습니다. |
| serviceUri |yes |유효한 https URI |
| properties |yes |값은 비어 있거나{} 키-값 쌍을 포함할 수 있습니다. |

## <a name="authentication-in-webhooks"></a>Webhook의 인증
hello webhook 토큰 기반 인증을 사용 하 여 쿼리 매개 변수로 토큰 ID를 가진 hello webhook URI를 저장할 위치를 인증할 수 있습니다. 예를 들어 https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue입니다.

## <a name="autoscale-notification-webhook-payload-schema"></a>크기 자동 조정 알림 Webhook 페이로드 스키마
Hello 자동 크기 조정 알림 생성 되 면 hello 다음과 같은 메타 데이터에에서 연결 되어 hello webhook 페이로드:

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| 필드 | 필수? | 설명 |
| --- | --- | --- |
| status |yes |자동 크기 조정 작업 생성 했음을 나타내는 hello 상태 |
| operation |yes |인스턴스가 증가하면 "규모 확장"되고 인스턴스가 감소하면 "규모 감축"됩니다. |
| context |yes |hello 자동 크기 조정 작업 컨텍스트 |
| timestamp |yes |Hello 자동 크기 조정 작업 트리거 되었을 때의 타임 스탬프 |
| id |예 |Hello 자동 크기 조정 설정의 리소스 관리자 ID |
| name |예 |hello 자동 크기 조정 설정의 hello 이름 |
| 세부 정보 |예 |자동 크기 조정 서비스 hello hello 동작의 설명에는 적용 하 고 hello hello 인스턴스 수 변경 |
| subscriptionId |예 |크기가 조정 되는 hello 대상 리소스의 구독 ID |
| resourceGroupName |예 |크기가 조정 되는 hello 대상 리소스의 리소스 그룹 이름 |
| resourceName |예 |크기가 조정 되는 hello 대상 리소스의 이름 |
| resourceType |예 |지원 되는 세 가지 값 hello: "microsoft.classiccompute/domainnames/slots/roles"-클라우드 서비스 역할과 가상 컴퓨터 크기 집합 "microsoft.compute/virtualmachinescalesets"-"microsoft.web/serverfarms"-웹 응용 프로그램 |
| resourceId |예 |크기가 조정 되는 hello 대상 리소스의 리소스 관리자 ID |
| portalLink |예 |Azure 포털 링크 toohello hello 대상 리소스의 요약 페이지 |
| oldCapacity |예 |hello 현재 (이전) 인스턴스 수가 자동 크기 조정 크기 조정 작업 시간 |
| newCapacity |예 |자동 크기 조정 hello 리소스를 너무 확장 있다는 hello 새 인스턴스 수|
| properties |아니요 |선택 사항입니다. <키, 값> 쌍 집합(예: Dictionary <문자열, 문자열>). hello 속성 필드는 선택 사항입니다. 사용자 지정 사용자 인터페이스 또는 논리 앱 기반 워크플로 hello 페이로드를 사용 하 여 전달할 수 있는 키와 값을 입력할 수 있습니다. 사용자 지정 속성 toopass 다시 toohello 보내는 webhook 호출 하는 다른 방법은 것 toouse hello webhook (쿼리 매개 변수)으로 자체 URI |
