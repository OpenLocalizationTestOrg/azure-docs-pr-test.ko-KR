---
title: "aaaDiagnose 실패-Azure 논리 앱 | Microsoft Docs"
description: "논리 앱 실패 하는 일반적인 방법으로 toounderstand"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a>논리 앱 오류 진단
논리 앱 문제 또는 실패를 발생 하는 경우의 몇 가지 접근 방식을 hello 오류에서 생성 되는 위치를 더 잘 이해 하는 데 도움이 수는 없습니다.  

## <a name="azure-portal-tools"></a>Azure 포털 도구
Azure 포털 hello 많은 도구 toodiagnose 각 단계에서 각 논리 앱을 제공합니다.

### <a name="trigger-history"></a>트리거 기록

각 논리 앱에는 하나 이상의 트리거가 있습니다. 앱 실행 되지 않습니다 발견 하는 경우 자세한 정보에 대 한 hello 트리거 기록을 지를 먼저 확인 합니다. Hello 트리거 기록 hello 논리 app'ss 주 블레이드를 액세스할 수 있습니다.

![Hello 트리거 기록 찾기][1]

hello 트리거 기록 논리 앱 수행한 모든 트리거 시도 나열 합니다. 모든 입력 클릭할 수 있는 각 트리거 시도 toodrill hello 세부 정보를 구체적으로, 또는 트리거 시도 hello는 출력을 생성 합니다. 실패 한 트리거를 찾을 경우 hello 트리거 시도 선택 하 고 hello 선택 **출력** tooreview 생성 된 오류 메시지, 예를 들어, 유효 하지 않은 FTP 자격 증명에 대 한 연결 합니다.

hello 다른 상태가 표시 될 표시 될 수 있습니다.

* **생략**. hello 끝점 데이터에 대 한 폴링된 toocheck 였으며 사용할 수 있는 데이터가 없는 없음을 응답을 받았습니다.
* **성공**. hello 트리거 데이터를 사용할 수 있는 응답을 받았습니다. 이 상태는 수동 트리거, 되풀이 트리거 또는 폴링 트리거로 발생할 수 있습니다. 이 상태는 일반적으로 hello 함께 **시작** 상태, 하지만 해야 SplitOn 명령 또는 조건을 충족 되지 않은 코드 뷰에서 수 없습니다.
* **실패**. 오류가 발생했습니다.

#### <a name="start-a-trigger-manually"></a>트리거 수동 시작

Hello 논리 앱 toocheck hello 다음 되풀이 기다리지 않고 즉시 사용 가능한 트리거는에 대 한 원하는 클릭 **트리거 선택** hello 주 블레이드 tooforce 확인을에 있습니다. 예를 들어 Dropbox 트리거이 링크를 클릭 합니다. 새 파일에 대 한 hello 워크플로 tooimmediately 폴링 Dropbox 하면 됩니다.

### <a name="run-history"></a>실행 기록

발생한 트리거는 모두 실행 중에 발생합니다. Hello 워크플로 중에 발생 한 시간을 이해 하는 데 도움이 되는 많은 세부 정보를 포함 하는 hello 주 블레이드에서 실행된 정보를 액세스할 수 있습니다.

![실행 기록 hello 찾기][2]

실행 하는 hello 다음 상태 중 하나가 표시 됩니다.

* **성공**. 모든 작업에 성공했습니다. 오류가 발생 하는 경우 해당 오류 hello 워크플로 뒷부분에 나오는 발생 하는 작업에 의해 처리 되었는지 합니다. 즉, toorun은 실패 한 작업 후에 설정 된 작업에서 hello 오류 처리 되었습니다.
* **실패**. 작업을 하나 이상 hello 워크플로 뒷부분에 나오는 동작에 의해 처리 되지 않은 오류가 발생을 했습니다.
* **취소**. hello 워크플로 실행 하지만 취소 요청을 받았습니다.
* **실행 중**. hello 워크플로 실행 중입니다. 이 상태는 제한 된 워크플로, 또는 계획 가격 책정 현재 hello로 인해 발생할 수 있습니다. 자세한 내용은 참조 [hello 가격 책정 페이지 작업 제한](https://azure.microsoft.com/pricing/details/app-service/plans/)합니다. 또한 진단 (실행 기록이 hello 아래에 나타나는 hello 차트) 구성 발생 하는 모든 제한 이벤트에 대 한 정보를 제공할 수 있습니다.

실행 기록에서 자세한 내용을 확인할 수 있습니다.  

#### <a name="trigger-outputs"></a>트리거 출력

트리거 출력 hello 트리거에서 제공 된 hello 데이터를 표시 합니다. 이러한 출력은 모든 속성이 예상대로 반환되었는지 확인하는 데 도움이 됩니다.

> [!NOTE]
> 이해할 수 없는 콘텐츠가 있는 경우 Azure Logic Apps에서 [다양한 콘텐츠 유형을 처리](../logic-apps/logic-apps-content-type.md)하는 방법을 알아봅니다.
> 

![트리거 출력 예제][3]

#### <a name="action-inputs-and-outputs"></a>작업 입력 및 출력

Hello 입 / 출력 작업 받은 드릴 수 있습니다. 이 데이터는 hello 출력의 hello 크기와 셰이프를 이해 하는 데 및 생성 된 모든 오류 메시지를 찾는 데 유용 합니다.

![작업 입력 및 출력][4]

## <a name="debug-workflow-runtime"></a>워크플로 런타임 디버그

Hello 입력, 출력 및 트리거 실행을 모니터링 하는 외 디버깅에 도움이 되는 몇 가지 단계 tooa 워크플로 추가할 수 있습니다. 
[RequestBin](http://requestb.in) 이 있습니다. RequestBin를 사용 하 여는 HTTP 요청 검사기 toodetermine hello 정확한 크기, 모양 및 HTTP 요청 형식과를 설정할 수 있습니다. RequestBin를 만들 수 있으며 논리 앱 tootest, 예를 들어 지정 하는 본문 내용을, 식 또는 단계 출력을 다른 HTTP POST 작업에서에서 hello URL을 붙여 넣습니다. Hello 논리 앱을 실행 한 후 프로그램 RequestBin toosee 어떻게 hello 요청이 설정 된 hello 논리 앱 엔진에서 생성 될 때 새로 고칠 수 있습니다.

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
