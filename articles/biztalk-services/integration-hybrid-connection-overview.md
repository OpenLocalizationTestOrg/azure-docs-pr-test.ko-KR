---
title: "aaaHybrid 연결 개요 | Microsoft Docs"
description: "하이브리드 연결, 보안, TCP 포트 및 지원되는 구성에 대해 알아봅니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: 216e4927-6863-46e7-aa7c-77fec575c8a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: f092c6019aae761e1e73f13d1af8446a896515c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-connections-overview"></a>하이브리드 연결 개요

> [!IMPORTANT]
> BizTalk 하이브리드 연결은 사용 중지되고 App Service 하이브리드 연결로 대체됩니다. 를 비롯 한 자세한 내용은 toomanage 기존 BizTalk 하이브리드 연결을 확인 하려면 어떻게 해야 [Azure 앱 서비스 하이브리드 연결](../app-service/app-service-hybrid-connections.md)합니다.

목록 hello 필요한 TCP 포트 및 소개 tooHybrid 연결을 지원 hello 구성을 나열 합니다.

## <a name="what-is-a-hybrid-connection"></a>하이브리드 연결 정의
하이브리드 연결은 Azure BizTalk 서비스의 기능입니다. 하이브리드 연결 Azure 앱 서비스 (이전의 웹 사이트)에 있는 간편 하 고 편리한 tooconnect hello 웹 응용 프로그램 기능이 및 Azure 앱 서비스 (이전의 모바일 서비스) tooon 온-프레미스 리소스 방화벽 뒤의 hello 모바일 앱 기능을 제공합니다.

![하이브리드 연결][HCImage]

하이브리드 연결은 다음과 같은 이점을 제공합니다.

* 웹앱 및 모바일 앱은 기존 온-프레미스 데이터 및 서비스에 안전하게 액세스할 수 있습니다.
* 여러 웹 응용 프로그램 또는 모바일 앱에 하이브리드 연결 tooaccess 온-프레미스 리소스를 공유할 수 있습니다.
* 최소한의 TCP 포트는 필요한 tooaccess 네트워크입니다.
* 하이브리드 연결을 사용 하 여 응용 프로그램 리소스에 액세스할만 hello 특정 온-프레미스 게시 된 hello 하이브리드 연결을 통해.
* SQL Server, MySQL, HTTP 웹 Api 및 대부분의 사용자 지정 웹 서비스와 같은 정적 TCP 포트를 사용 하 여 tooany 온-프레미스 리소스를 연결할 수 있습니다.
  
  > [!NOTE]
  > 동적 포트(예: FTP 수동 모드 또는 확장 수동 모드)를 사용하는 TCP 기반 서비스는 현재 지원되지 않습니다. LDAP도 지원되지 않습니다. LDAP는 고정 TCP 포트를 사용하지만 UDP도 사용할 수 있기 때문에 지원되지 않습니다.
  > 
  > 
* 웹앱에서 지원하는 모든 프레임워크(.NET, PHP, Java, Python, Node.js) 및 모바일 앱에서 지원하는 모든 프레임워크(Node.js, .NET)에서 사용할 수 있습니다.
* 웹 앱 및 모바일 앱 정확 하 게 hello에서 온-프레미스 리소스에 액세스할 수 같은 방식으로 hello 웹 또는 모바일 앱에 있으면 로컬 네트워크입니다. 예를 들어 hello 동일한 연결 문자열 사용 되는 온-프레미스 Azure에서 사용할 수도 있습니다.

또한 하이브리드 연결 된 제어 및 포함 하는 하이브리드 응용 프로그램에서 액세스 하는 hello 회사 리소스에 대 한 가시성 엔터프라이즈 관리자를 제공 합니다.

* 사용 하 여 그룹 정책 설정 관리자 수 hello 네트워크에서 하이브리드 연결을 허용 및 하이브리드 응용 프로그램에서 액세스할 수 있는 리소스를 지정할 수도 있습니다.
* Hello 회사 네트워크에 이벤트 및 감사 로그 하이브리드 연결에서 액세스 하는 hello 리소스에 대 한 가시성을 제공 합니다.

## <a name="example-scenarios"></a>예제 시나리오
하이브리드 연결 프레임 워크 및 응용 프로그램 조합을 다음 hello를 지원 합니다.

* .NET framework 액세스 tooSQL 서버
* .NET framework 액세스 tooHTTP/HTTPS 웹 클라이언트와 서비스
* PHP 액세스 tooSQL Server, MySQL
* Java 액세스 tooSQL Server, MySQL 및 Oracle
* Java 액세스 tooHTTP/HTTPS 서비스

경우 tooaccess 하이브리드 연결을 사용 하 여 온-프레미스 SQL Server에 hello 다음을 고려 합니다.

* SQL Express 명명 된 인스턴스에 고정 포트 구성된 toouse 이어야 합니다. 기본적으로 SQL Express 명명된 인스턴스는 동적 포트를 사용합니다.
* SQL Express 기본 인스턴스는 정적 포트를 사용하지만 TCP를 사용하도록 설정해야 합니다. 기본적으로 TCP는 사용되도록 설정되어 있지 않습니다.
* 클러스터링 또는 가용성 그룹을 사용 하는 경우 hello `MultiSubnetFailover=true` 모드 현재 지원 되지 않습니다.
* hello `ApplicationIntent=ReadOnly` 현재 지원 되지 않습니다.
* SQL 인증 hello Azure 응용 프로그램 및 hello 온-프레미스 SQL server에서 지 원하는 hello 종단 간 인증 방법으로 필요할 수 있습니다.

## <a name="security-and-ports"></a>보안 및 포트
공유 액세스 서명 (SAS) 권한 부여 toosecure hello 연결을 사용 하는 하이브리드 연결 hello Azure에서에서 응용 프로그램 및 hello 온-프레미스 하이브리드 연결 관리자 toohello 하이브리드 연결 합니다. Hello 응용 프로그램에 대 한 별도 연결 키는 만들어집니다 및 hello 온-프레미스 하이브리드 연결 관리자입니다. 이러한 연결 키는 별도로 롤오버되고 해지됩니다.

하이브리드 연결의 hello 키 toohello 응용 프로그램 원활 하 고 안전한 배포를 위해 제공 하 고 hello 온-프레미스 하이브리드 연결 관리자.

[하이브리드 연결 만들기 및 관리](integration-hybrid-connection-create-manage.md)(영문)를 참조하세요.

*응용 프로그램 권한 부여는 hello 하이브리드 연결을 별도로*합니다. 적절한 어떤 권한 부여 방법도 사용될 수 있습니다. hello 권한 부여 방법 hello Azure 클라우드 및 온-프레미스 구성 요소 hello 간에 지원 hello 종단 간 권한 부여 방법에 따라 달라 집니다. 예를 들어 Azure 응용 프로그램은 온-프레미스 SQL Server에 액세스합니다. 이 시나리오에서는 SQL 권한 부여를 지원된 하려면 종단 간 hello 권한 부여 방법 수도 있습니다.

#### <a name="tcp-ports"></a>TCP 포트
하이브리드 연결에는 개인 네트워크의 아웃바운드 TCP 또는 HTTP 연결만 필요합니다. Tooopen 모든 방화벽 포트가 필요 또는 네트워크에 네트워크 경계 구성 tooallow 프로그램 모든 인바운드 연결을 변경 하지 않는 합니다.

하이브리드 연결에서 TCP 포트를 수행 하는 hello 사용 됩니다.

| 포트 | 필요한 이유 |
| --- | --- |
| 9350 - 9354 |이러한 포트는 데이터 전송에 사용됩니다. 서비스 버스 릴레이 관리자 hello TCP 연결을 사용할 수 있는 경우 포트 9350 toodetermine를 조사 합니다. 사용 가능한 경우 포트 9352도 사용 가능한 것으로 가정합니다. 데이터 트래픽이 포트 9352를 통해 이동합니다. <br/><br/>아웃 바운드 연결 toothese 포트를 허용 합니다. |
| 5671 |포트가 9352 데이터 트래픽에 사용 하는 경우 포트 5671 hello 컨트롤 채널으로 사용 됩니다. <br/><br/>Toothis 포트 아웃 바운드 연결을 허용 합니다. |
| 80, 443 |이러한 포트는 일부 데이터 요청 tooAzure에 사용 됩니다. 또한 9352 및 5671 포트를 사용할 수 없는 경우, *다음* 포트 80 및 443 포트가 hello 대체 hello 컨트롤 채널 및 데이터 전송에 사용 합니다.<br/><br/>아웃 바운드 연결 toothese 포트를 허용 합니다. <br/><br/>**참고** 없으면 hello 대신 대체 포트를 다른 TCP 포트 hello으로 toouse 이러한 권장 합니다. HTTP/WebSocket hello 데이터 채널에 대 한 기본 TCP 대신 hello 프로토콜로 사용 됩니다. 성능이 저하될 수 있습니다. |

## <a name="next-steps"></a>다음 단계
[Create and manage Hybrid Connections](integration-hybrid-connection-create-manage.md)<br/>
[Azure 웹 앱 tooan 연결 온-프레미스 리소스](../app-service-web/web-sites-hybrid-connection-get-started.md)<br/>
[Azure 웹 앱에서 tooon 온-프레미스 SQL Server 연결](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)<br/>

## <a name="see-also"></a>참고 항목
[Microsoft Azure의 BizTalk Services를 관리하기 위한 REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[BizTalk Services: 버전 차트](biztalk-editions-feature-chart.md)<br/>
[Azure Portal을 사용하여 BizTalk Service 만들기](biztalk-provision-services.md)<br/>
[BizTalk Services: 대시보드, 모니터링 및 크기 조정 탭](biztalk-dashboard-monitor-scale-tabs.md)<br/>

[HCImage]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionImage.png
[HybridConnectionTab]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionManageConn.png
