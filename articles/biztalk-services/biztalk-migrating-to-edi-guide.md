---
title: "BizTalk Server EDI 솔루션 tooBizTalk aaaMigrating 서비스 기술 가이드 | Microsoft Docs"
description: "EDI tooMABS; 마이그레이션 Microsoft Azure BizTalk 서비스"
services: biztalk-services
documentationcenter: na
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 61c179fa-3f37-495b-8016-dee7474fd3a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 34cca3c939a6a7845a860ead6858287000d03ee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-biztalk-server-edi-solutions-toobiztalk-services-technical-guide"></a>BizTalk Server EDI 솔루션 tooBizTalk Services 마이그레이션: 기술 가이드

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

작성자: Tim Wieman 및 Nitin Mehrotra

검토자: Karthik Bharthy

Microsoft Azure BizTalk 서비스를 사용하여 작성 – 2014년 2월 릴리스.

## <a name="introduction"></a>소개
전자 데이터 교환 (EDI)는 비즈니스 데이터를 교환할 전자적으로 기업 간 또는 B2B 트랜잭션 이라는 용어로 사용도 hello 가장 널리 퍼진 방법 중 하나입니다. BizTalk Server에 대 한 hello 초기 BizTalk Sever 릴리스 이후 10 년 이상 EDI 지원이 되었습니다. BizTalk 서비스와 Microsoft 계속 hello Microsoft Azure 플랫폼에서 EDI 솔루션에 대 한 hello 지원이 됩니다. B2B 트랜잭션은 대부분 외부 tooan 조직 며 따라서 보다 쉽게 tooimplement 클라우드 플랫폼에서 구현 된 경우. Microsoft Azure는 BizTalk 서비스를 통해 이 기능을 제공합니다.

일부 고객 "최적의" 플랫폼으로 새로운 EDI 솔루션에 대 한 BizTalk 서비스에 게 보이지만, 많은 고객 들이 현재 BizTalk Server EDI 솔루션 toomigrate tooAzure를 정의할 수 있습니다. BizTalk 서비스 EDI는 설계에 따라 hello 때문에 같은 BizTalk Server EDI 아키텍처 (거래 파트너, 엔터티, 규약), 가능한 toomigrate BizTalk Server EDI 아티팩트 tooBizTalk는 서비스 처럼 엔터티 키입니다.

이 문서에서는 BizTalk Server EDI 아티팩트 tooBizTalk 마이그레이션와 관련 된 hello 차이점 중 일부 서비스입니다. 이 문서에서는 BizTalk Server EDI 처리 및 거래 파트너 규약에 대한 실무 지식이 있다고 가정 합니다. BizTalk Server EDI에 대한 자세한 내용은 [BizTalk Server를 사용하여 거래 파트너 관리](https://msdn.microsoft.com/library/bb259970.aspx)를 참조하세요.

## <a name="which-version-of-biztalk-server-edi-artifacts-can-be-migrated-toobiztalk-services"></a>TooBizTalk 서비스를 마이그레이션할 어떤 버전의 BizTalk Server EDI 아티팩트 수 있습니까?
hello BizTalk Server EDI 모듈 리 모델링 된 tooinclude 파트너, 프로필 및 규약 되었을 때 BizTalk Server 2010에 대해 크게 향상 되었습니다. BizTalk 서비스에서 사용 하는 거래 업체는 동일한 모델 tooorganize hello hello 및 해당 거래 파트너 내 사업 부서 hello 합니다. 아티팩트를 BizTalk Server 2010 및 이후 버전 tooBizTalk EDI 마이그레이션 결과적으로, 서비스, 과정이 훨씬 더 간단 합니다. 버전 이전 tooBizTalk Server 2010와 관련 된 toomigrate EDI 아티팩트 먼저 tooBizTalk Server 2010을 업그레이드 한 다음 EDI 아티팩트를 마이그레이션할 해야 tooBizTalk 서비스입니다.

## <a name="scenariosmessage-flow"></a>시나리오/메시지 흐름
BizTalk Server와 함께 BizTalk Server의 EDI 처리는 TPM(거래 파트너 관리) 솔루션 주위에 설치됩니다. hello TPM 솔루션에는 다음과 같은 주요 구성 요소가 hello에 있습니다.

* 거래 파트너는 B2B 트랜잭션의 조직을 나타냅니다.
* 프로필은 거래 파트너 내의 부서를 나타냅니다.
* 거래 파트너 계약 (또는 계약) 있으며이 두 파트너/프로필 간의 사업 규약 hello을 나타냅니다.

hello 다음 그림은 BizTalk Server EDI 솔루션 및 BizTalk 서비스 EDI 솔루션 간의 차이 뿐만 아니라 hello 유사점을 보여 줍니다.

![][EDImessageflow]

주요 차이점 및 유사점, BizTalk Server에서 EDI 솔루션 흐름 hello 및 BizTalk 서비스:

* 에 EDI 메시지 및 EDISend 파이프라인 toosend EDI 메시지는 EDIReceive 파이프라인 tooreceive BizTalk Server에 사용 하는 것 처럼 BizTalk 서비스 EDI 수신 브리지 tooreceive 및 EDI 메시지를 EDI 송신 브리지 toosend 사용 합니다. BizTalk Server에서 hello 파이프라인은 송신을 사용 하 여 규약과 연결 된 수신 포트 또는 합니다. BizTalk 서비스의 자체 hello 계약 나타냅니다 hello 송신 또는 수신 브리지입니다.
* BizTalk Server에서 EDI 메시지를 hello hello EDIReceive 파이프라인 프로세스 후 hello 메시지 덤프 tooa SQL Server 데이터베이스입니다. hello EdiSend 파이프라인 다음 hello SQL Server 데이터베이스에서 hello 메시지를 선택 하 고 처리 한 다음 거래 업체 toohello 외부로 전송 합니다.
  
    BizTalk 서비스의 hello EDI 브리지 프로세스 hello EDI 메시지를 받은 후 hello 메시지 tooan 외부 프로세스를 라우팅합니다. hello 외부 프로세스는 Microsoft Azure 또는 온-프레미스에서 실행 될 수 있습니다. hello 외부 프로세스에 EDI 송신 브리지로; hello 메시지 toohello를 라우팅해야 합니다. hello 송신 브리지는 hello 메시지를 기본적으로 끌어 오지 않습니다. Hello 메시지를 처리 하 고, 후 EDI 송신 브리지로 hello hello 메시지 toohello 거래 업체를 라우팅합니다.

BizTalk 서비스를 사용 하기 쉬운 구성 환경을 tooquickly 제공 인스턴스 (웹 또는 작업자 역할)를 Microsoft Azure 계산 구성 하지 않고 거래 업체, 모든 Microsoft Azure SQL 데이터베이스 또는 모든 간에 B2B 규약 만들기 및 배포 Microsoft Azure 저장소 계정입니다. 보다 복잡 한 시나리오를 전후해 서 워크플로 또는 기타 서비스 처리 연결에서는 "hello 가장자리 주위", 즉 거래 파트너 계약의 거래 파트너 계약 EDI 브리지 처리 전후. 자세히 hello 다음 이벤트 시퀀스가 발생 하는 동안 BizTalk 서비스에서 처리는 EDI 메시지.

1. EDI 메시지가 거래 파트너인 Fabrikam에서 수신됩니다.  거래 파트너로부터 EDI 메시지를 수신하는 경우 BizTalk 서비스는 FTP, SFTP, AS2 및 HTTP/S.와 같은 전송 프로토콜 지원합니다.
2. 거래 파트너 규약의 수신 측 처리 hello hello EDI 메시지 tooXML 형식을 디스어셈블 합니다.  서비스 버스 릴레이 끝점, 서비스 버스 주제, 서비스 버스 큐 또는 BizTalk 서비스 브리지와 같은 hello 디스어셈블된 EDI 메시지 (XML 형식) tooService 버스 끝점으로 라우팅할 수 있습니다.
3. hello 디스어셈블된 XML 메시지 다음 수신할 수 사용자 지정 처리를 위해 hello 끝점에서 합니다.  이러한 끝점은 온-프레미스 구성 요소별 또는 Microsoft Azure 계산 인스턴스 toofurther 프로세스 hello 메시지를 Windows WF (Workflow) 또는 Windows Communication Foundation (WCF) 서비스에서 처리할 수 없습니다.
4. hello hello 거래 파트너 계약의 "송신 쪽 처리" hello XML 메시지를 EDI 형식으로 어셈블하고 하 고 tootrading 업체인 Contoso 보냅니다.  BizTalk 서비스 EDI 메시지를 보내기 하 tootrading 파트너에 대 한 EDI 메시지를 수신 하기 위해 사용 되는 프로토콜을 통해 동일한 hello를 지원 합니다.

이 문서에 개념적 지침도 제공 서비스 hello 다른 BizTalk Server EDI 아티팩트 tooBizTalk의 일부 마이그레이션.

## <a name="sendreceive-ports-tootrading-partners"></a>송신/수신 포트 tooTrading 파트너
BizTalk Server에서 설정한 수신 위치 및 수신 포트 tooreceive EDI/XML 메시지를 거래 파트너 로부터 및 송신 포트 toosend EDI/XML 메시지 tootrading 파트너를 설정 합니다. 그런 다음 거래 파트너 규약 hello BizTalk Server 관리 콘솔을 사용 하 여 이러한 포트 tooa를 연결 합니다. BizTalk 서비스의 hello hello BizTalk 서비스 포털에서에서 거래 파트너와 메시지 tootrading 파트너가 hello 거래 업체 규약 (전송 설정의 일부로) 자체의 일부로 구성 되며을 전송 하는 위치에서 메시지를 받는 위치 위치 .  따라서 실제로 않아도 hello 개념 "송신 포트" 및 "수신 위치" 본질적으로 BizTalk 서비스의 합니다. 자세한 내용은 [규약 만들기](https://msdn.microsoft.com/library/windowsazure/hh689908.aspx)를 참조하세요.

## <a name="pipelines-bridges"></a>파이프라인 (브리지)
BizTalk Server EDI에서 파이프라인은 hello 응용 프로그램 요구에 따라 특정 처리 능력에 대 한 사용자 지정 논리를 포함할 수 있는 메시지 처리 엔터티입니다. BizTalk 서비스에 대 한 해당 하는 hello EDI 브리지는 합니다. 그러나 지금은 BizTalk 서비스의 hello EDI 브리지는 "닫혀" 있습니다.  즉, 사용자 고유의 사용자 지정 활동 tooan EDI 브리지를 추가할 수 없습니다. 모든 사용자 지정 처리 hello 메시지 hello 거래 파트너 계약의 일부로 구성 하는 hello 브리지 입력 전후 응용 프로그램에서 EDI 브리지 hello 밖에 서 수행 해야 합니다. 포함 된 EAI 연결 hello 옵션 toodo 사용자 지정 처리 하는 합니다. 사용자 지정 처리 하려는 경우에 hello 메시지를 hello EDI 브리지 처리 전후 EAI 브리지를 사용할 수 있습니다. 자세한 내용은 참조 [브리지에 사용자 지정 코드를 tooInclude 방법](https://msdn.microsoft.com/library/azure/dn232389.aspx)합니다.

사용자 지정 코드 및/또는 서비스 버스 메시징 큐 및 항목 거래 업체 규약 hello hello 메시지를 수신 하기 전이나 후 hello 계약이 hello 메시지를 처리 하 고 tooa 서비스 버스 끝점 경로 사용 하 여 게시/구독 흐름을 삽입할 수 있습니다.

참조 **시나리오/메시지 흐름** hello 메시지 흐름 패턴에 대 한이 항목의 합니다.

## <a name="agreements"></a>규약
BizTalk Server 2010 거래 파트너 계약 EDI 처리에 사용 되는 hello에 익숙한 경우 BizTalk 서비스 거래 파트너 계약이 친숙 하 게 보일 합니다. 대부분의 설정이 동일한 hello는 hello 계약 및 사용 하 여 동일한 용어가 hello 합니다. 경우에 따라 규약 설정 hello 훨씬 더 간단 비교 toohello BizTalk Server에서 동일한 설정 됩니다. Microsoft Azure BizTalk 서비스는 x12, EDIFACT 및 AS2 전송을 지원합니다.

또한 Microsoft Azure BizTalk 서비스는 제공 된 **TPM 데이터 마이그레이션** toomigrate 거래 파트너와 BizTalk Server 거래 파트너 모듈 tooBizTalk 서비스 포털에서에서 계약 도구입니다. hello TPM 데이터 마이그레이션 도구는 hello에서 다운로드할 수 있는 도구 패키지의 일부로 [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057)합니다. hello 패키지에는 어떻게 toouse hello 도구 및 기본 문제 해결 정보에 대 한 hello 도구에 지침을 제공 하는 추가 포함 됩니다.

## <a name="schemas"></a>스키마
BizTalk 서비스는 BizTalk 서비스 솔루션에서 사용할 수 있는 EDI 스키마를 제공합니다.  또한 BizTalk Server EDI 스키마도 되므로 사용할 수 있습니다 BizTalk 서비스와 BizTalk 서비스 뿐 아니라 BizTalk Server 간에 hello EDI 스키마의 hello 루트 노드는 동일한 합니다. 따라서 있습니다 수 toodirectly 내용이 BizTalk Server EDI 스키마 되며 BizTalk 서비스를 사용 하 여 개발 하는 hello EDI 솔루션에서 사용 합니다. Hello에서 hello 스키마를 다운로드할 수도 [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057)합니다.

## <a name="maps-transforms"></a>매핑(변환)
BizTalk Server의 매핑은 BizTalk 서비스의 변환이라고 합니다. BizTalk Server tooBizTalk 서비스 중 하나일 수에서 맵을 마이그레이션하는 작업 (맵 복잡성)에 따라 더 복잡 한 작업 tooachieve를 hello 합니다. BizTalk 서비스에 사용 되는 hello 매핑 도구는 hello BizTalk 맵 편집기와에서 다릅니다. Hello 매퍼 보이지만 대부분 동일 hello, hello 기본 맵 형식이 다릅니다. 펑 토이 드 hello (호출 **매핑 작업** BizTalk 서비스에서) 사용할 수 있는 toohello 사용자도 서로 합니다.  실제로 BizTalk 서비스에서 직접 BizTalk 매핑을 사용할 수 없습니다. 또한 일부 hello 펑 토이 드 BizTalk Server에서 사용할 수 있는 BizTalk 서비스의 맵 작업으로 사용할 수 있습니다.

### <a name="new-transform-operations"></a>새로운 변환 작업
사용 가능한 변환 맵 작업 목록이 hello hello BizTalk Server 맵 편집기와에서 크게 다르게 보일 수 있지만에 동일한 작업 hello 수행 새로운 방식을 갖고 BizTalk 서비스 변환 합니다. 예를들어, BizTalk 서비스 변환에서는 **목록 작업** 을 사용할 수 있습니다. Hello BizTalk 맵 편집기에서 사용할 수 없습니다.  hello **목록 작업** toocreate 사용 하면 고 목록은 일련의 항목 (또는 "행") 하 고 각 항목에는 여러 명의 멤버 (라고도 "열") 있을 수 있습니다는 "목록"에 대해 작동 합니다.  Hello 목록, 조건에 따라 선택 항목을 정렬할 수 있습니다.

BizTalk 서비스 변환의 새로운 기능의 또 다른 예로 hello **루프 작업**합니다.  어려운 toocreate 중첩 루프 hello BizTalk Server 맵 편집기에는  따라서 hello 루프 매핑 작업은 BizTalk 서비스 변환 hello에 대 한 추가 됩니다.

또 다른 예 hello **If Then Else** 식 맵 작업입니다.  If 다음 다른 작업을 수행 hello BizTalk 맵 편집기에서 가능 하지만 여러 펑 토이 드 tooaccomplish 간단해 보이는 작업 필요.

### <a name="migrating-biztalk-server-maps"></a>BizTalk Server 맵 마이그레이션
Microsoft Azure BizTalk 서비스 도구 toomigrate BizTalk Server 맵 tooBizTalk 서비스 변환을 제공 합니다. hello **BTMMigrationTool** ´ ï ´ hello의 일부로 **도구** hello와 함께 제공 되는 패키지 [BizTalk 서비스 SDK 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=235057)합니다. Hello 도구에 대 한 자세한 내용은 참조 [BizTalk 서비스 변환 하는 BizTalk 맵 tooa 변환](https://msdn.microsoft.com/library/windowsazure/hh949812.aspx)합니다.

찾아볼 수도 있습니다는 예제를 Sandro pereira가 제공, BizTalk MVP에 어떻게 너무[BizTalk Server 맵 tooBizTalk 서비스 변환을 마이그레이션할](http://social.technet.microsoft.com/wiki/contents/articles/23220.migrating-biztalk-server-maps-to-windows-azure-biztalk-services-wabs-maps.aspx)합니다.

## <a name="orchestrations"></a>오케스트레이션
BizTalk Server 오케스트레이션 처리 tooMicrosoft Azure toomigrate 해야 할 경우 hello 오케스트레이션 toobe Microsoft Azure에서 BizTalk Server 오케스트레이션 실행을 지원 하지 않으므로 다시 작성 해야 합니다.  Hello 오케스트레이션 기능은 Windows Workflow Foundation 4.0 (WF4) 서비스에서를 다시 작성할 수 있습니다.  마이그레이션이 현재 BizTalk Server 오케스트레이션 tooWF4에서으로 완전히 다시 작성 해야가 됩니다. 다음은 Windows 워크플로에 대한 몇가지 리소스입니다.

* [*어떻게 toointegrate WCF 워크플로 서비스를 서비스 버스 큐 및 주제* ](https://msdn.microsoft.com/library/azure/hh709041.aspx) Paolo salvatori. 
* [*Windows Workflow Foundation 및 Azure로 앱 빌드* 세션](http://go.microsoft.com/fwlink/p/?LinkId=237314) hello 2011 빌드 컨퍼런스에서 합니다.
* MSDN의 [*Windows Workflow Foundation 개발자 센터*](http://go.microsoft.com/fwlink/p/?LinkId=237315).
* MSDN의 [*WF4(Windows Workflow Foundation 4) 설명서*](https://msdn.microsoft.com/library/dd489441.aspx).

## <a name="other-considerations"></a>기타 고려 사항
BizTalk 서비스를 사용하는 동안 확인 해야 하는 몇가지 고려 사항은 다음과 같습니다.

### <a name="fallback-agreements"></a>대체(fallback) 계약
BizTalk Server EDI 처리에는 "대체 계약" hello 개념이 있습니다.  BizTalk 서비스에는 지금까지 대체 규약 개념이 **없습니다** .  BizTalk 설명서 항목을 참조 [EDI 처리에서 계약의 역할 hello](http://go.microsoft.com/fwlink/p/?LinkId=237317) 및 [전역 구성 또는 대체 (fallback) 규약 속성](https://msdn.microsoft.com/library/bb245981.aspx) BizTalk에서는 대체 계약을 사용 하는 방법에 대 한 내용은 서버입니다.

### <a name="routing-toomultiple-destinations"></a>라우팅 toomultiple 대상
BizTalk 서비스 브리지, 현재 상태에서 지원 하지 않습니다는 게시를 사용 하는 라우팅 메시지 toomultiple 대상-구독 모델입니다. 대신 BizTalk 서비스 브리지 tooa 서비스 버스 항목에서 둘 이상의 끝점에서 여러 구독 tooreceive hello 메시지를 가질 수 있는 메시지를 라우팅할 수 있습니다.

## <a name="conclusion"></a>결론
Microsoft Azure BizTalk 서비스는 일반적인 중요 시점 tooadd 업데이트 더 많은 기능 및 특성입니다. 각 업데이트 의견에 귀 toosupporting 증가 기능 toofacilitate BizTalk 서비스 및 기타 Azure 기술을 사용 하 여 종단 간 솔루션을 만들기.

## <a name="see-also"></a>참고 항목
[Azure로 엔터프라이즈 응용 프로그램 개발](https://msdn.microsoft.com/library/azure/hh674490.aspx)

[EDImessageflow]: ./media/biztalk-migrating-to-edi-guide/IC719455.png
