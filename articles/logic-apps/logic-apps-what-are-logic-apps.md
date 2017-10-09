---
title: "aaaConnect 앱 워크플로-Azure 논리 앱과 데이터 통합 및 | Microsoft Docs"
description: "앱을 연결하고 Azure Logic Apps와 데이터를 통합하여 워크플로를 만들고 프로세스를 자동화합니다."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 07765c05-72a6-4169-a8ab-f6420bfbaf07
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: klam
ms.openlocfilehash: 53d4e165bb2205ddd56c1950719389725267ddea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-logic-apps"></a>Logic Apps란 무엇인가요?
논리 앱 방식으로 toosimplify 제공 하 고 hello 클라우드에서 확장 가능한 통합 및 워크플로 구현 합니다. 비주얼 디자이너 toomodel 제공 하 고 일련의 단계는 워크플로로 알려진 프로세스 자동화.  [많은 커넥터](../connectors/apis-list.md) hello 클라우드 및 온-프레미스 tooquickly에서 서비스 및 프로토콜 간에 통합 합니다.  논리 앱 트리거 (like '계정을 tooDynamics CRM가 추가 하 고' 하는 경우)로 시작 후 실행 작업, 변환 및 조건 논리의 여러 조합을 시작할 수 있습니다.

논리 앱을 사용 하 여 hello 장점 hello 다음 포함:  

* 쉽게 toounderstand 디자인 도구를 사용 하 여 복잡 한 프로세스를 디자인 하 여 시간 절약
* 패턴 및 워크플로 원활 하 게 구현 하는 것 어려운 tooimplement 코드에서
* 템플릿에서 신속하게 시작
* 고유의 사용자 지정 API, 코드 및 작업을 사용하여 논리 앱 사용자 지정
* 연결 하 고 온-프레미스 간에 서로 다른 시스템 동기화 클라우드 hello
* 강력한 통합 지원을 통해 BizTalk Server, API Management, Azure Functions 및 Azure Service Bus 구축

응용 프로그램 논리는 완전히 관리 되는 iPaaS (서비스로 통합 플랫폼) 때문에 개발자가 호스팅, 확장성, 가용성 및 관리를 구축 하는 방법에 대 한 toohave tooworry 되지 않습니다.  논리 앱 toomeet 필요 시 자동으로 확장 됩니다.

![흐름 앱 디자이너](media/logic-apps-what-are-logic-apps/LogicAppCapture2.png)

언급했듯이 Logic Apps와 함께 비즈니스 프로세스를 자동화할 수 있습니다. 다음은 몇 가지 예입니다.  

* 파일 이동 tooan FTP 서버를 Azure 저장소에 업로드
* 온-프레미스 및 클라우드에 걸친 프로세스 및 경로 순서
* 특정 항목에 대 한 모든 트 윗을 모니터링 하 고 hello 감성 분석 경고 및 필요한 추가 작업 항목에 대 한 작업을 만듭니다.

Hello 비주얼 디자이너에서 모두 및 코드의 한 줄도 작성 하지 않고 이러한 시나리오를 구성할 수 있습니다. [이제 논리 앱을 구축][create]을 시작합니다.  작성되면 논리 앱은 여러 환경 및 지역에 걸쳐 [신속하게 배포되고 다시 구성될](../logic-apps/logic-apps-create-deploy-template.md) 수 있습니다.

## <a name="why-logic-apps"></a>Logic Apps 사용 이유
논리 앱 hello 엔터프라이즈 통합 공간으로 속도 및 확장성을 제공합니다.  다양 한 사용 가능한 트리거 및 작업 및 강력한 관리 도구가 hello 디자이너의 사용 편의성 hello 그 어느 때 보다 더 간단 Api를 중앙에서 관리를 확인 합니다.  기업 digitalization 추구할 논리 앱을 통해 수 tooconnect 레거시 및 최첨단 시스템 함께 합니다.

뿐만 아니라 우리의 [엔터프라이즈 통합 계정] [ biztalk] 의 hello 전원이 toomature 통합 시나리오를 확장할 수 있습니다는 [XML 메시징] [ xml], [거래 업체 관리][tpm], 등입니다.

* **디자인 도구를 쉽게 toouse** -논리 앱 디자인된에 종단 간 hello 브라우저에서 또는 Visual Studio 도구를 사용 될 수 있습니다. GitHub 문제 만들어질 단순 일정 toowhen 트리거-로 시작 합니다. 그런 다음 개수에 관계 없이 커넥터의 hello 풍부한 갤러리를 사용 하 여 작업을 오케스트레이션 합니다.
* **Api를 쉽게 연결** -짝수 컴퍼지션 작업을 쉽게 toodescribe는 코드에서 어려운 tooimplement 합니다. 논리 앱 쉽게 tooconnect 서로 다른 시스템이 있습니다. 원하는 tooconnect 솔루션 마케팅 클라우드 tooyour 온-프레미스 청구 시스템? Toocentralize Api 및 엔터프라이즈 서비스 버스와 시스템 간에 메시지를 선택 하십시오. 논리 앱은 hello 가장 빠르고 가장 안정적인 방법을 toodeliver toothese 문제 해결 방법입니다.
* **템플릿에서 빠르게 시작** -제공 했습니다 toohelp 시작 하는 데는 [템플릿 갤러리] [ templates] 수 있는 toorapidly 몇 가지 일반적인 솔루션을 만듭니다. 고급 정책 B2B 솔루션 toosimple SaaS 연결 하 고는 몇 '를'-hello 갤러리는 hello 가장 빠른 방법은 tooget hello 활용 논리 앱을 시작 합니다.
* **확장성에 구운** -필요한 hello 커넥터 표시 되지 않는? 응용 프로그램 논리는 직접 Api 및 코드; 설계 된 toowork 쉽게 사용자 지정 커넥터도 자신의 API 앱 toouse 만들 수도 있고 불러일으킬는 [Azure 함수](https://functions.azure.com) tooexecute 가져온 조각을 요청 시 코드입니다. 
* **진정한 통합 능력** - 쉽게 시작되고 필요에 따라 확장됩니다. 논리 앱에는 Microsoft의 업계 선두 통합 솔루션 tooenable 통합 전문가 toobuild hello 솔루션 필요한 BizTalk의 hello 전원을 활용할 쉽게 수 있습니다. Hello에 대 한 자세한 내용을 알아보려면 [엔터프라이즈 통합 팩](../logic-apps/logic-apps-enterprise-integration-overview.md)합니다.

## <a name="logic-app-concepts"></a>논리 앱 개념
hello 논리 앱 환경을 구성 하는 hello 주요 정보가 hello 다음과가 같습니다. 

* **워크플로** -논리 앱 제공 그래픽 방식으로 toomodel 비즈니스 프로세스를 일련의 단계 또는 워크플로 합니다.
* **Managed 커넥터** -논리 앱 toodata 및 서비스에 액세스 해야 합니다. 관리 되는 커넥터가 특히 tooaid 만들어집니다 tooand 데이터 작업을 연결 하는 있습니다. 커넥터에 현재 사용할 수의 hello 목록을 [managed 커넥터][managedapis]합니다.
* **트리거** - 일부 관리 커넥터는 트리거로도 작동할 수 있습니다. 트리거는 hello 도착 전자 메일 또는 Azure 저장소 계정에 변경 등의 특정 이벤트를 기반으로 하는 워크플로의 새 인스턴스를 시작 합니다.
* **작업** -워크플로에서 hello 트리거는 동작 호출 후에 각 단계입니다. 각 작업에는 일반적으로 관리 되는 커넥터 또는 사용자 지정 API 앱에서 tooan 작업이 매핑됩니다.
* **엔터프라이즈 통합 팩** - 고급 통합 시나리오를 위해 Logic Apps에는 BizTalk의 기능이 포함됩니다. BizTalk는 Microsoft의 업계 선도적인 통합 플랫폼입니다. hello 엔터프라이즈 통합 팩 커넥터를 사용 하면 tooeasily tooyour 논리 앱 워크플로에서 유효성 검사, 변환 등을 포함 합니다.

## <a name="getting-started"></a>시작하기
* 논리 앱 시작 tooget hello에 따라 [논리 앱을 만드는] [ create] 자습서입니다.  
* [일반적인 예제 및 시나리오 보기](../logic-apps/logic-apps-examples-and-scenarios.md)
* [논리 앱으로 비즈니스 프로세스를 자동화할 수 있습니다](http://channel9.msdn.com/Events/Build/2016/T694) 
* [자세한 내용은 방법 tooIntegrate 논리 앱 시스템](http://channel9.msdn.com/Events/Build/2016/P462)

[biztalk]: logic-apps-enterprise-integration-accounts.md
[appservice]: ../app-service/app-service-value-prop-what-is.md
[create]: logic-apps-create-a-logic-app.md
[managedapis]: ../connectors/apis-list.md
[tpm]: logic-apps-enterprise-integration-accounts.md
[xml]: logic-apps-enterprise-integration-b2b.md
[templates]: logic-apps-use-logic-app-templates.md
