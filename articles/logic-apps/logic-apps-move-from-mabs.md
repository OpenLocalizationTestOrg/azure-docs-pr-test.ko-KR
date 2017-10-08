---
title: "BizTalk 서비스 tooAzure 논리 앱의에서 앱을 aaaMove | Microsoft Docs"
description: "Azure BizTalk Services MABS tooLogic 앱을 마이그레이션하거나 이동"
services: logic-apps
documentationcenter: 
author: jonfancey
manager: anneta
editor: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: ladocs; jonfan; mandia
ms.openlocfilehash: b3b065b90a37002f72305b0fc866c24231fb5f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-from-biztalk-services-toologic-apps"></a>BizTalk 서비스 tooLogic 앱에서 이동

MABS(Microsoft Azure BizTalk Services)가 사용 중지됩니다. 이 항목 toomove MABS 통합 솔루션 tooAzure 논리 앱을 사용 합니다. 

## <a name="overview"></a>개요

BizTalk Services는 다음 두 하위 서비스로 구성됩니다.

1.  Microsoft BizTalk Services 하이브리드 연결
2.  EAI 및 EDI 브리지 기반 통합

찾고 있는 경우 toomove 하이브리드 연결의 경우 다음 [Azure 앱 서비스 하이브리드 연결](../app-service/app-service-hybrid-connections.md) hello 변경 내용 및이 서비스의 기능에 설명 합니다. Azure 하이브리드 연결이 BizTalk Services 하이브리드 연결을 대체합니다. Azure 하이브리드 연결 Azure 앱 서비스를 사용할 수 있으며 hello Azure 포털에서에서 제공 됩니다. 만드는 새 하이브리드 연결 hello 포털 및 azure의 하이브리드 연결에는 또한 기존 BizTalk 서비스 하이브리드 연결을 새 하이브리드 연결 관리자 toomanage 제공 합니다. Azure App Service 하이브리드 연결이 출시(GA)됩니다.

EAI 및 EDI 브리지 기반 통합을 위해 논리 앱은 hello 대체. 논리 앱 모든 hello BizTalk 서비스 등과 같은 기능을 제공 합니다. 논리 앱 소비 기반 워크플로 및 오케스트레이션 기능 tooquickly 쉽게 브라우저를 사용 하 여 또는 Visual Studio 내에서 도구를 사용 하 여 복잡 한 통합 솔루션을 작성 하 고이 허용 하는 클라우드 규모를 제공 합니다.

다음 표에서 hello tooLogic 앱 관계가 정리 BizTalk 서비스를 제공 합니다.

| BizTalk 서비스   | Logic Apps            | 목적                  |
| ------------------ | --------------------- | ---------------------------- |
| 커넥터          | 커넥터             | 데이터 송수신   |
| 브리지             | 논리 앱             | 파이프라인 프로세서           |
| 유효성 검사 단계     | XML 유효성 검사 작업      | 스키마에 대해 XML 문서 유효성 검사             |
| 보강 단계       | 데이터 토큰      | 속성을 메시지로 또는 라우팅 결정을 위해 승격             |
| 변환 단계    | 변환 작업      | 형식 tooanother에서 XML 메시지 변환             |
| 디코딩 단계       | 플랫 파일 디코딩 작업      | 플랫 파일 tooXML에서 변환             |
| 인코딩 단계       |  플랫 파일 인코딩 작업      | XML tooflat 파일에서 변환             |
| 메시지 검사기       |  Azure Functions 또는 API Apps      | 통합에서 사용자 지정 코드 실행             |
| 라우팅 작업      |  조건 또는 스위치      | hello 메시지 tooone 경로 커넥터 지정             |

BizTalk Services에는 여러 형식의 아티팩트가 있습니다.

## <a name="connectors"></a>커넥터
BizTalk 서비스에서 커넥터 브리지 toosend 허용 및 요청/응답 HTTP 기반 상호 작용을 사용 하도록 설정 하는 양방향 브리지를 포함 하 여 데이터를 수신 합니다. 논리 앱 hello 동일한 용어가 사용 됩니다. 논리 앱의 커넥터 hello 동일한 용도 위해, 항목과 tooa의 광범위 한 기술과 서비스를 연결할 수 있는 140 넘는 포함을 제공 하십시오 온-프레미스를 사용 하 여 hello (BizTalk 어댑터 서비스 BizTalk 서비스에서 사용 하는 hello 교체) 온-프레미스 데이터 게이트웨이 및 OneDrive, office 365, Dynamics CRM 및 더 많은 같은 SaaS 및 PaaS 서비스 클라우드입니다.

BizTalk Services의 소스 제한 tooFTP, SFTP 및 서비스 버스 큐 또는 항목 구독 됩니다.

![](media/logic-apps-move-from-mabs/sources.png)

각 브리지는 hello 런타임 주소 및 hello 브리지의 상대 주소 속성 hello로 구성 된 기본적으로 HTTP 끝점을 있습니다. tooachieve 논리 앱을 사용 하 여 hello 동일 hello [요청 및 응답](../connectors/connectors-native-reqres.md) 동작 합니다.

## <a name="xml-processing-and-bridges"></a>XML 처리 및 브리지
BizTalk 서비스의 브리지 유사 tooa 처리 파이프라인입니다. 브리지는 커넥터에서 받은 데이터를 사용할 수 있고 hello 데이터로 작업을 수행한 다음 tooanother 시스템 보냅니다. 동일한 파이프라인 기반 상호 작용 패턴을 BizTalk 서비스로 및 다양 한 다른 통합 패턴 제공 hello를 지원 하 여 논리 앱 같은 hello지 않습니다. hello [XML 요청-회신 브리지](https://msdn.microsoft.com/library/azure/hh689781.aspx) BizTalk 서비스에서 수행할 수 있는 단계의 구성 된 VETER 파이프라인으로 알려집니다.

* (V) 유효성 검사
* (E) 보강
* (T) 변환
* (E) 보강
* (R) 라우팅

다음 이미지는 hello와 같이 hello 처리 요청 및 회신 하기, 분할 및 hello 요청 및 hello 제어할 별도로 (예: 각 지도 사용 하 여) 회신 경로 수 있습니다.

![](media/logic-apps-move-from-mabs/xml-request-reply.png)

또한 XML 단방향 브리지 처리의 hello 시작 및 끝에 디코딩 및 인코딩 단계를 추가 하 고 단일 보강 단계를 포함 하는 hello 통과 연결 합니다.

### <a name="message-processing-and-decodingencoding"></a>메시지 처리 및 디코딩/인코딩
BizTalk 서비스의 다양 한 유형의 XML 메시지를 수신 고 hello 수신 hello 메시지에 대해 일치 하는 스키마를 결정 합니다. Hello에서 수행 됩니다이 **메시지 유형** hello 단계의 처리 파이프라인을 수신 합니다. 그런 다음 hello 디코드 단계 사용 감지 hello 메시지 유형 toodecode hello 제공 된 스키마를 사용 하 여 합니다. Hello 스키마 flatfile 스키마 이면 hello 들어오는 flatfile tooXML 변환 합니다. 

Logic Apps가 비슷한 기능을 제공합니다. 다양 한 hello 다른 커넥터 트리거 (파일 시스템, FTP, HTTP, 및 등)를 사용 하 여 서로 다른 프로토콜을 통해 한 flatfile를 수신 하 고 hello를 사용 하 여 [플랫 파일 디코딩](../logic-apps/logic-apps-enterprise-integration-flatfile.md) 동작 tooconvert hello 들어오는 데이터 tooXML 합니다. 기존 플랫 파일 스키마 toologic 앱 하나 필요 없이 변경 되 고 다음 업로드 하는 스키마 tooyour 통합 계정을 직접 이동할 수 있습니다.

### <a name="validation"></a>유효성 검사
Hello 들어오는 데이터를 변환 된 tooXML (또는 XML hello 메시지 형식을 수신 된 경우) 유효성 검사 hello 메시지 tooyour XSD 스키마를 준수 하는 경우 toodetermine를 실행 됩니다. toodo이 논리 앱을 사용 하 여 hello [XML 유효성 검사](../logic-apps/logic-apps-enterprise-integration-xml-validation.md) 동작 합니다. 사용할 수는 다시 BizTalk 서비스에서 동일한 스키마를 변경 하지 않고 hello 합니다.

### <a name="transform-messages"></a>메시지 변환
BizTalk 서비스 hello 변환 단계는 하나의 XML 기반 메시지 형식 tooanother를 변환합니다. 이 hello TRFM 기반 맵 편집기를 사용 하 여 맵을 적용 하 여 수행 됩니다. 논리 앱에서 hello 프로세스와 비슷합니다. 변환 작업 hello 통합 계정에서 지도 실행합니다. hello 주요 차이점 논리 앱의 지도 XSLT 형식입니다. XSLT를 이미 있는 펑 토이 드를 포함 하는 BizTalk Server에 대해 만든 맵을 포함 하 여 XSLT 기존 hello 기능 tooreuse 포함 되어 있습니다. 

### <a name="routing-rules"></a>라우팅 규칙
BizTalk 서비스 끝점/커넥터 toosend 수신 메시지/데이터는 라우팅 결정을 내립니다. hello 기능 tooselect 다양 한 미리 구성 된 끝점 중 하나는 hello 라우팅 필터 옵션을 사용 하 여 가능 합니다.

![](media/logic-apps-move-from-mabs/route-filter.png)

Logic Apps는 [조건](../logic-apps/logic-apps-use-logic-app-features.md) 및 [스위치](../logic-apps/logic-apps-switch-case.md)를 통해 보다 정교한 논리 기능을 제공하므로 고급 제어 흐름 및 라우팅이 가능합니다. *만약* 두 가지 옵션만 있으면 **조건**을 사용할 때 BizTalk Services의 라우팅 필터 변환이 가장 잘 수행됩니다. 세 개 이상 있으면 **스위치**를 사용합니다.

### <a name="enrich"></a>보강
hello 처리 하는 BizTalk 서비스에서 보강 단계 속성 toohello 메시지 컨텍스트에 수신 hello 데이터와 관련 된 추가 합니다. 예를 들어 (아래 설명 참조)는 XPath 식을 사용 하는 값을 추출 하 여 또는 데이터베이스 조회에서 라우팅에 대 한 속성 toouse를 승격 합니다. 논리 앱 액세스 tooall 컨텍스트 데이터 출력을 제공 이전 작업 항목에서 동일한 동작 hello 간단 tooreplicate 하 합니다. 예를 들어 hello를 사용 하 여 `Get Row` SQL 연결 작업을 반환 하는 SQL Server 데이터베이스에서 데이터 및 사용 하 여 hello 데이터 라우팅에 대 한 의사 결정 동작에 있습니다. 마찬가지로, 서비스 버스 들어오는 속성 대기 중인 메시지 트리거에 의해 hello xpath 워크플로 정의 언어 식을 사용 하 여 XPath 뿐만 아니라 주소가 지정 됩니다.

### <a name="use-custom-code"></a>사용자 지정 코드 사용
BizTalk 서비스는 hello 기능 너무 제공[사용자 지정 코드를 실행할](https://msdn.microsoft.com/library/azure/dn232389.aspx) 고유한 어셈블리에 업로드 합니다. 이 hello 동일한 [IMessageInspector](https://msdn.microsoft.com/library/microsoft.biztalk.services.imessageinspector.aspx) 인터페이스입니다. Hello 브리지의 각 단계는 hello.Net 유형을 만든이 인터페이스를 구현 하는 제공 하는 두 개의 속성 (On Enter Inspector, 및 On Exit Inspector)를 포함 합니다. 사용자 지정 코드 사용 하면 tooperform 더 복잡 한 hello 데이터 뿐만 아니라 일반적인 비즈니스 논리를 수행 하는 어셈블리의 다시 사용할 수 있도록 기존 코드에 대 한 처리. 

논리 앱 제공 두 가지 사용자 지정 코드 tooexecute: Azure 함수 및 API 앱. Azure Functions는 Logic Apps에서 만들고 호출할 수 있습니다. [Azure Functions를 통해 Logic Apps에 대한 사용자 지정 코드 추가 및 실행](../logic-apps/logic-apps-azure-functions.md)을 참조하세요. API 앱, toocreate Azure 앱 서비스의 일부를 사용 하 여 사용자 고유의 트리거 및 작업. 에 대 한 자세한 내용은 [논리 앱을 사용 하 여 사용자 지정 API toouse 만들기](../logic-apps/logic-apps-create-api-app.md)합니다. 

사용자 지정 코드에서 BizTalk 서비스를 호출 하는 assmeblies에 있으면 이동할 수 있습니다이 tooAzure 동작 하는 코드 또는 사용자 지정 Api; API 앱 만들기 구현 하 고에 따라. 예를 들어 논리 앱 커넥터 없는 다른 서비스를 래핑하는 코드를 있는 경우 다음 API 앱 만들기 및 API 앱 논리 앱 내에서 제공 하는 hello 동작을 사용 합니다. 도우미 함수 또는 라이브러리를 설정한 경우 Azure 기능 될 가능성이 hello 가장 적합 합니다.

### <a name="edi-processing-and-trading-partner-management"></a>EDI 처리 및 거래 업체 관리
BizTalk Services는 AS2(Applicability Statement 2), X12 및 EDIFACT를 지원하는 EDI 및 B2B 처리를 포함합니다. Logic Apps도 그렇습니다. BizTalk 서비스의 프로그램 EDI 브리지를 만들고 만들기/관리 거래 파트너와 규약 hello 전용된 추적 및 관리 포털에서 합니다.

논리 앱에서이 기능은 hello에 포함 된 [엔터프라이즈 통합 팩](../logic-apps/logic-apps-enterprise-integration-overview.md)합니다. B2B 및 EDI 처리에 대 한 hello 통합 계정 및 B2B 작업 구성 됩니다. hello [통합 계정](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) 사용된 toocreate 있으며 관리할 [거래 업체](../logic-apps/logic-apps-enterprise-integration-partners.md) 및 [계약](../logic-apps/logic-apps-enterprise-integration-agreements.md)합니다. 통합 계정을 만든 후 하나 이상의 논리 앱 toohello 계정을 연결할 수 있습니다. 에 연결 되 면 hello B2B 작업 tooaccess 거래 업체 정보 논리 앱 내에서 사용할 수 있습니다. 작업을 수행 하는 hello 제공 됩니다.

* AS2 인코딩
* AS2 디코딩
* X12 인코딩
* X12 디코딩
* EDIFACT 인코딩
* EDIFACT 디코딩

BizTalk 서비스와는 달리 이러한 작업은 hello 전송 프로토콜에서 분리 됩니다. 따라서 논리 앱을 만들 때가 좀더 유연한 어떤 커넥터에 toosend를 사용 하 고이 데이터를 수신 합니다. 예를 들어 전자 메일의 첨부 파일을 사용 하 여 가능한 tooreceive X12 파일은 및 논리 앱에서 이러한 파일을 처리 합니다. 

## <a name="manage-and-monitor"></a>관리 및 모니터링
거래 업체 관리, 뿐만 아니라 hello 전용 포털 BizTalk 서비스에 대 한 제공 기능 toomonitor를 추적 하 고 문제를 해결 합니다. 

논리 앱을 다양 한 추적 및 모니터링 기능 hello에 제공 [Azure 포털](../logic-apps/logic-apps-monitor-your-logic-apps.md), 및 hello로 [Operations Management Suite B2B 솔루션](../logic-apps/logic-apps-monitor-b2b-message.md)워크플로가 작업에 대 한 모바일 앱을 비롯 하 여, hello 하 고 이동 합니다.

## <a name="high-availability"></a>고가용성
tooachieve 고가용성 (HA) BizTalk 서비스의 부하를 처리 하는 지정 된 지역 tooshare hello에서 둘 이상의 인스턴스가 사용 합니다. Logic Apps를 사용하면 지역 내 HA가 기본 제공되므로 추가 비용이 들지 않습니다. BizTalk Services에서 B2B 처리를 위한 지역 외 재해 복구의 경우 백업 및 복원 프로세스가 필요합니다. 논리 앱에서 지역 간 액티브/패시브 [DR 기능](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md) 를 제공 하도록 hello B2B 데이터 동기화 통합 계정 비즈니스 연속성에 대 한 다른 지역에 걸쳐 있습니다.

## <a name="next"></a>다음
* [Logic Apps란?](logic-apps-what-are-logic-apps.md)
* [첫 번째 논리 앱 만들기](logic-apps-create-a-logic-app.md) 또는 [미리 빌드된 템플릿](logic-apps-use-logic-app-templates.md)을 사용하여 신속하게 시작  
* [사용 가능한 커넥터 hello 모든 보기](../connectors/apis-list.md) 논리 앱에서 사용할 수 있습니다
