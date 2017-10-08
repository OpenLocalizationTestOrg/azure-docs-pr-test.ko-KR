---
title: "Azure 가상 컴퓨터를 사용 하 여 자동 크기 조정 aaaAdvanced | Microsoft Docs"
description: "크기 조정 작업에 대한 전자 메일을 전송하고 웹후크 URL을 호출하는 여러 규칙 및 프로필에 Resource Manager 및 VM Scale Sets를 사용합니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a>Resource Manager 템플릿을 사용하여 VM Scale Sets에 대한 고급 자동 크기 조정 구성
되풀이 일정 또는 특정 날짜에 성능 메트릭 임계값을 기반으로 가상 컴퓨터 확장 집합의 규모를 확장 및 감축할 수 있습니다. 또한 크기 조정 동작에 대한 전자 메일 및 웹후크 알림을 구성할 수 있습니다. 이 연습에서는 VM 확장 집합에서 Resource Manager 템플릿을 사용하여 이 모든 개체를 구성하는 예를 보여 줍니다.

> [!NOTE]
> VM 크기 집합에 대 한 hello 단계를 설명 하는이 연습에서는, 동안 hello 동일한 정보 적용 tooautoscaling [클라우드 서비스](https://azure.microsoft.com/services/cloud-services/), 및 [앱 서비스-웹 응용 프로그램](https://azure.microsoft.com/services/app-service/web/)합니다.
> CPU와 같은 간단한 성능 메트릭에 기반으로 하는 간단한 소수/VM 크기 집합에 대 한 설정을, 참조 toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) 및 [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) 문서
>
>

## <a name="walkthrough"></a>연습
이 연습을 사용 하 여 [Azure 리소스 탐색기](https://resources.azure.com/) 크기 집합에 대 한 hello 자동 크기 조정 설정 tooconfigure 및 업데이트 합니다. Azure 리소스 탐색기는 쉽게 toomanage 리소스 관리자 템플릿을 통해 Azure 리소스입니다. 새로운 tooAzure 리소스 탐색기 도구 인 경우 읽기 [이 소개](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/)합니다.

1. 기본 자동 크기 조정 설정으로 새 규모 집합을 배포합니다. 이 문서에서는 windows Azure 빠른 시작 갤러리 hello에서 hello 하나 표시줄이 기본 자동 크기 조정 템플릿을 사용 하 여 설정 합니다. Linux 배율 설정 작업 hello 동일한 방식으로 합니다.
2. Hello 크기 집합을 만든 후 Azure 리소스 탐색기에서 toohello 눈금 집합 리소스를 이동 합니다. Hello 다음 Microsoft.Insights 노드에 표시 됩니다.

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    hello 템플릿 실행 hello 이름의 기본 자동 크기 조정 설정을 만들었습니다 **'autoscalewad'**합니다. Hello 오른쪽에 hello이 자동 크기 조정 설정의 전체 정의 볼 수 있습니다. 이 경우 hello 기본 자동 크기 조정 설정 CPU % 기반 확장 및 확장의 규칙 포함 되어 있습니다.  

3. 이제 추가 프로필 및 hello 일정 또는 특정 요구 사항에 따라 규칙을 추가할 수 있습니다. 3개의 프로필로 자동 크기 조정 설정을 만듭니다. toounderstand 프로필과의 자동 크기 조정 규칙 검토 [자동 크기 조정에 대 한 유용한 정보](insights-autoscale-best-practices.md)합니다.  

    | 프로필 및 규칙 | 설명 |
    |--- | --- |
    | **프로필** |**성능/메트릭 기반** |
    | 규칙 |서비스 버스 큐 메시지 수 > x |
    | 규칙 |서비스 버스 큐 메시지 수 < y |
    | 규칙 |CPU% > n |
    | 규칙 |CPU% < p |
    | **프로필** |**평일 오전 시간(규칙 없음)** |
    | **프로필** |**제품 출시일(규칙 없음)** |

4. 이 연습에 사용할 가상의 크기 조정 시나리오는 다음과 같습니다.

    * **기반 부하** -싶습니다 tooscale 걸러 내 거 나에서 눈금 set.* 내에서 호스트 하는 응용 프로그램 내에서 hello 부하에 따라
    * **메시지 큐 크기** -hello 들어오는 메시지 toomy 응용 프로그램에 대 한 서비스 버스 큐를 사용 합니다. Hello 큐의 메시지 수 및 CPU (%)를 사용 하 고 적중 threshold.* hello 메시지 수 또는 CPU 경우 기본 프로필 tootrigger 크기 조정 작업을 구성 합니다.
    * **주 및 일의 시간** -매주 되풀이 '시간이 hello 하루 중' 기반 프로필 ' 평일 오전 시간 '를 호출 합니다. 기록 데이터에 따라, 알 수 있습니까 것이 더 나은 toohave 특정 VM 인스턴스의 수 toohandle 내 응용 프로그램의 부하가이 time.* 중
    * **특정 날짜** - '제품 출시일' 프로필을 추가했습니다. I 미리 계획 특정 날짜에 대 한 마케팅 공지 인해 준비 toohandle hello 부하 및 hello application.*에 새 제품에서는 삽입 했을 때 응용 프로그램 이므로
    * *hello 마지막 두 개의 프로필 다른 성능 메트릭 기반된 규칙 내에 있을 수도 있습니다. 이 경우 하나 toohave 하지 하기로 결정 하 고 대신 hello 기본 성능 메트릭에 toorely 기반의 규칙. 규칙은 hello 되풀이 및 날짜 기반 프로필에 대 한 선택 사항입니다.*

    Hello 프로필 및 규칙의 우선 순위를 자동 크기 조정 엔진의 hello에도 캡처된 [자동 크기 조정에 대 한 유용한 정보](insights-autoscale-best-practices.md) 문서.
    자동 크기 조정에 대한 공통 메트릭 목록은 [자동 크기 조정에 대한 공통 메트릭](insights-autoscale-common-metrics.md)을 참조하세요.

5. Hello 선택 되어 있는지 확인 **읽기/쓰기** 모드의 리소스 탐색기

    ![Autoscalewad, 기본 자동 크기 조정 설정](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. 편집을 클릭합니다. **대체** 같은 구성이 hello로 자동 크기 조정 설정에 프로필' hello' 요소:

    ![프로필](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    지원되는 필드와 해당 값은 [자동 크기 조정 REST API 설명서](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx)를 참조하세요. 이제 자동 크기 조정 설정에는 설명한 hello 3 개 프로필을 포함 합니다.

7. 마지막으로, 자동 크기 조정 hello를 살펴보고 **알림** 섹션. 자동 크기 조정 알림 하면 toodo 다음 세 가지 경우를 확장 하거나 작업에 성공적으로 트리거됩니다.
   - Admin 님 안녕하세요 및 구독의 공동 관리자에 게 알림
   - 사용자 집합에 전자 메일 보내기
   - 웹후크 호출 트리거. 발생 하면이 webhook hello 자동 크기 조정 상태에 대 한 메타 데이터 보내고 hello 눈금 리소스를 설정 합니다. 자동 크기 조정 webhook의 hello 페이로드에 대 한 자세한 정보는 toolearn 참조 [Webhook 구성 및 자동 크기 조정에 대 한 전자 메일 알림을](insights-autoscale-to-webhook-email.md)합니다.

   Hello toohello 자동 크기 조정 설정 대체 다음 추가 프로그램 **알림** 값이 null 인 요소

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
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

   적중 **배치** 리소스 탐색기 tooupdate hello 자동 크기 조정 설정에는 단추입니다.

VM 크기 집합 tooinclude에 여러 크기 조정 프로필을 설정 하는 자동 크기 조정 업데이트 및 알림을 크기를 조정 합니다.

## <a name="next-steps"></a>다음 단계
이러한 링크 toolearn 자동 크기 조정에 대 한 자세한 사용 합니다.

[가상 컴퓨터 규모 집합을 사용하여 자동 크기 조정 문제 해결](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[자동 크기 조정에 대한 공통 메트릭](insights-autoscale-common-metrics.md)

[Azure 자동 크기 조정에 대한 모범 사례](insights-autoscale-best-practices.md)

[PowerShell을 사용하여 자동 크기 조정 관리](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[CLI를 사용하여 자동 크기 조정 관리](insights-cli-samples.md#autoscale)

[자동 크기 조정의 Webhook 및 메일 알림 구성](insights-autoscale-to-webhook-email.md)
