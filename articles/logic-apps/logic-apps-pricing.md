---
title: "aaaPricing 청구-및 Azure 논리 앱 | Microsoft Docs"
description: "Azure Logic Apps의 가격 책정 및 대금 청구 방식에 대해 알아봅니다."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f8f528f5-51c5-4006-b571-54ef74532f32
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.openlocfilehash: fa10cbbf7657afba7fadb7c76817b7a5e4af7b42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-pricing-model"></a>논리 앱 가격 책정 모델
Azure 논리 앱 tooscale 있으며 hello 클라우드에서 통합 워크플로 실행 합니다.  다음은 hello 대금 청구 및 논리 앱에 대 한 가격 책정 모델에 대 한 세부 정보입니다.
## <a name="consumption-pricing"></a>소비 가격
새로 만든 논리 앱에서는 소비 요금제를 사용합니다. 만 hello 논리 앱 소비 가격 책정 모델을 사용 하는 것에 대 한 지불 합니다.  소비 요금제를 사용할 경우 논리 앱은 제한되지 않습니다.
논리 앱 인스턴스 실행 시 실행되는 모든 작업은 요금이 청구됩니다.
### <a name="what-are-action-executions"></a>작업 실행이란 무엇인가요?
논리 앱 정의의 모든 단계 tooconnectors 및 호출 toonative 작업을 호출 하는 트리거, until 루프, 조건, 각 루프에 대 한 범위와 마찬가지로 제어 흐름 단계를 포함 하는 작업입니다.
트리거는 특수 디자인 된 tooinstantiate 논리 앱의 새 인스턴스 될 때 작업을 특정 이벤트가 발생 합니다.  Hello 논리 앱 유료일 어떻게 영향을 줄 수 있는 트리거에 대 한 몇 가지 다른 동작이 있습니다.
* **폴링 트리거** – 논리 앱의 인스턴스를 만들기 위한 hello 기준을 충족 하는 메시지를 받을 때까지 계속 해 서이 트리거 끝점 폴링합니다.  hello 논리가 응용 프로그램 디자이너에서에서 hello 트리거에서 hello 폴링 간격을 구성할 수 있습니다.  각 폴링 요청은 논리 앱의 인스턴스를 만들지 않더라도 작업 실행으로 계산됩니다.
* **Webhook 트리거** –이 트리거 기다리는 클라이언트 toosend 것을 특정 끝점에 요청 합니다.  각 요청 전송 toohello webhook 끝점 액션 실행으로 계산 됩니다. hello 요청 및 hello HTTP Webhook 트리거는 모두 webhook 트리거입니다.
* **되풀이 트리거** –이 트리거는 트리거 hello에에서 구성 된 hello 되풀이 간격에 따라 hello 논리 앱의 인스턴스를 만듭니다.  예를 들어 되풀이 트리거 구성된 toorun도 매 분 또는 3 일 수 있습니다.

트리거 실행 hello 논리 앱 리소스 블레이드에서 hello 트리거 기록 부분에서에서 볼 수 있습니다.

실행된 모든 작업은 성공 여부에 관계없이 작업 실행으로 측정됩니다.  Tooa 조건이 충족 되지 인해 건너뛴 작업 또는 작업을 완료 하기 전에 hello 논리가 응용 프로그램 종료 때문에 실행 하지 않은 작업 실행으로 계산 되지 않습니다.

루프 내에서 실행 되는 작업은 hello 루프의 반복 당 계산 됩니다.  예를 들어, 한 번의 작업에는 각 루프에 대 한 10 개의 항목의 목록에서 반복 하는로 계산 됨 hello 항목 수 (10) hello 목록의 hello hello 루프 (1)에서 작업 수를 곱한 hello 루프의 초기화 hello에 대 한 1을 더한 는,이 예에서 그렇게 할 수 (10 * 1) + 1 = 11 동작 실행 합니다.
비활성화된 Logic Apps는 인스턴스화된 새 인스턴스를 포함할 수 없으므로 비활성화된 기간 중에는 비용이 청구되지 않습니다.  논리 앱을 비활성화 한 후이 되 고 완전히 사용 하지 않도록 설정 하기 전에 인스턴스 tooquiesce hello에 대 한 약간 시간이 걸릴 수 있습니다 주의 해야 합니다.
### <a name="integration-account-usage"></a>통합 계정 사용량
소비 기반 사용량에 포함 되는 [통합 계정](logic-apps-enterprise-integration-create-integration-account.md) 탐색, 개발 및 테스트 목적으로 있도록 toouse hello에 대 한 [B2B/EDI](logic-apps-enterprise-integration-b2b.md) 및 [XML 처리](logic-apps-enterprise-integration-xml.md)추가 비용 없이 논리 앱의 기능입니다. 수 toocreate / 지역당 한 계정의 최대 하 too10 계약 및 25 지도를 저장 합니다. 스키마, 인증서 및 파트너에는 제한이 없고 필요한 만큼 업로드할 수 있습니다.

또한 사용량 통합 계정 toohello 포함, 또한 계정을 만들 수 있습니다 표준 통합을 표준 논리 앱 SLA는 이러한 제한 하지 않고 합니다. 자세한 내용은 [Azure 가격 책정](https://azure.microsoft.com/pricing/details/logic-apps)을 참조하세요.

## <a name="app-service-plans"></a>앱 서비스 계획
이전에 참조 하는 앱 서비스 계획을 만든 논리 앱 전에 toobehave로 계속 됩니다. Hello 규정 된 매일 실행이 초과 되 되었지만 hello 작업 실행 측정기를 사용 하 여 요금을 청구 hello 계획 선택에 따라 조절 됩니다.
앱 서비스 계획에 있는 논리 앱 hello와 명시적으로 연결 된 toobe 없는 자신의 구독 EA 고객 hello 포함 된 수량 혜택을 받을 합니다.  예를 들어 표준 앱 서비스 계획에 있으면 EA 구독과 논리 앱의 hello 동일한 구독 후 (다음 표 참조) 하루에 10, 000 동작 실행 하는 데는 요금이 청구 되지 않습니다. 

앱 서비스 계획 및 일일 허용된 작업 실행:
|  | 무료/공유/기본 | 표준 | Premium |
| --- | --- | --- | --- |
| 일일 작업 실행 |200 |10000 |50,000 |
### <a name="convert-from-app-service-plan-pricing-tooconsumption"></a>앱 서비스 계획 가격 tooConsumption에서 변환
연결 된 하는 앱 서비스 계획을 가진 논리 앱 toochange tooa 소비 모델 제거 hello 참조 toohello 앱 서비스 계획 hello 논리 앱 정의에 있습니다.  이 변경은 호출 tooa PowerShell cmdlet과 함께 수행할 수 있습니다.`Set-AzureRmLogicApp -ResourceGroupName ‘rgname’ -Name ‘wfname’ –UseConsumptionModel -Force`
## <a name="pricing"></a>가격
가격 책정 세부 정보는 [Logic Apps 가격 책정](https://azure.microsoft.com/pricing/details/logic-apps)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [Logic Apps 개요][whatis]
* [첫 번째 논리 앱 만들기][create]

[pricing]: https://azure.microsoft.com/pricing/details/logic-apps/
[whatis]: logic-apps-what-are-logic-apps.md
[create]: logic-apps-create-a-logic-app.md

