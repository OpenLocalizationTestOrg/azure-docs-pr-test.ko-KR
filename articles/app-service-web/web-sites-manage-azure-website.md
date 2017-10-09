---
title: "Azure 앱 서비스의 웹 앱 aaaManage"
description: "Azure 앱 서비스의 웹 앱을 관리 하기 위한 링크 tooresources 합니다."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a>Azure 앱 서비스에서 웹 앱 관리
이 항목에서는의 웹 앱을 관리 하기 위한 링크 tooresources [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)합니다. 관리에 웹 앱을 원활 하 게 실행 상태로 유지 하는 hello 작업을 모두 포함 됩니다. 

웹 앱의 hello 동안 초기 배포 toonormal 운영, 유지 관리 및 업데이트에서 이동 하면 다른 관리 작업을 수행 합니다.

Hello Azure 포털에서에서 다양 한 웹 앱 관리 작업을 수행할 수 있습니다.

## <a name="before-you-deploy-your-web-app-tooproduction"></a>웹 앱 tooproduction를 배포 하기 전에
### <a name="choose-a-tier"></a>계층 선택
Azure 앱 서비스는 5개의 계층, 무료, 공유, 기본, 표준 및 프리미엄으로 제공됩니다. Hello 기능 및 각 계층에 대 한 가격 책정에 대 한 정보를 참조 하십시오. [가격 정보](https://azure.microsoft.com/pricing/details/app-service/)합니다. 

* [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) hello에서 여러 웹 앱을 그룹화 할 수와 동일한 계층입니다.
* 웹 앱을 만든 후에 언제든지 [계층을 전환](web-sites-scale.md) 할 수 있습니다.

### <a name="configuration"></a>구성
사용 하 여 hello [Azure 포털](https://portal.azure.com/) tooset 다양 한 구성 옵션입니다. 자세한 내용은 [Azure 앱 서비스에서 웹 앱 구성](web-sites-configure.md)을 참조하세요. 아래에 간단한 검사 목록이 나와 있습니다.

* 필요에 따라 .NET, PHP, Java 또는 Python의 **런타임 버전** 을 선택합니다.
* 사용 하도록 설정 **Websocket** 웹 앱 hello WebSocket 프로토콜을 사용 하는 경우. 여기에는 [ASP.NET SignalR](http://www.asp.net/signalr) 또는 [socket.io](web-sites-nodejs-chat-app-socketio.md)를 사용하는 앱이 포함됩니다.
* 연속적인 웹 작업을 실행하는 경우 **무중단**을 사용하도록 설정합니다.
* 집합 hello **기본 문서**, index.html 등입니다.

또한 toothese 기본 구성 설정을 tooconfigure hello 다음을 사용할 수 있습니다.

* **SSL(Secure Socket Layer)** 암호화. 사용자 지정 도메인 이름과 함께 SSL을 toouse, 가져와야 하는 SSL 인증서 및 웹 응용 프로그램 toouse 구성할 것입니다. [Azure 앱 서비스에서 웹 앱에 대한 HTTPS를 사용하도록 설정](app-service-web-tutorial-custom-ssl.md)을 참조하세요.
* **사용자 지정 도메인 이름.** 웹 앱에는 자동으로 azurewebsites.net 하위 도메인이 있습니다. Contoso.com 등의 사용자 지정 도메인 이름을 연결할 수 있습니다. [Azure 앱 서비스에서 사용자 지정 도메인 이름 구성](app-service-web-tutorial-custom-domain.md)을 참조하세요.

언어별 구성:

* **PHP**: [Azure 앱 서비스 웹 앱에서 PHP를 구성합니다.](web-sites-php-configure.md)
* **Python**: [Azure 앱 서비스 웹 앱에서 Python을 구성합니다.](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>웹 앱을 실행하는 동안 수행할 작업
웹 앱이 실행 되는 동안 원하는 toomake toomeet 사용자 트래픽을 확장 하 고를 사용할 수 있습니다. Tootroubleshoot 오류 할 수도 있습니다.

### <a name="monitoring"></a>모니터링
* 수 hello Azure 포털을 통해 [성능 메트릭 추가](web-sites-monitor.md) 예: CPU 사용량 및 클라이언트 요청 수입니다.
* [웹 앱의 크기를 조정](web-sites-scale.md) 응답 tootraffic에 있습니다. 에서는 계층에 따라 Vm hello 수 및/또는 hello hello VM 인스턴스 크기를 확장할 수 있습니다. Hello 표준 및 프리미엄 계층에서 설정할 수 있습니다 또한 자동 크기 조정, 응답 tooload 또는 고정된 된 일정에서 웹 앱을 자동으로 확장 하도록 합니다.  

### <a name="backups"></a>백업
* 웹 앱의 [자동 백업](web-sites-backup.md) 을 설정합니다. 백업에 대해 자세히 알아보려면 [이 비디오](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/)를 시청하세요.
* Hello 옵션에 대 한 자세한 내용은 [데이터베이스 복구](../sql-database/sql-database-business-continuity.md) Azure SQL 데이터베이스에 있습니다.

### <a name="troubleshooting"></a>문제 해결
* 문제가 발생 하는 경우 다음을 할 수 있습니다 [Visual Studio에서 문제를 해결](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)진단 로그를 사용 하 여을 라이브 hello 클라우드에서 디버깅 합니다. 
* Visual Studio 외부에서 다양 한 방법으로 toocollect 진단 로그입니다. [Azure 앱 서비스에서 웹 앱에 대한 진단 로깅 설정](web-sites-enable-diagnostic-log.md)을 참조하세요.
* Node.js 응용 프로그램에 대 한 참조 [어떻게 toodebug는 Node.js 웹 Azure 앱 서비스의 앱](web-sites-nodejs-debug.md)합니다.

### <a name="restoring-data"></a>데이터 복원
* [복원](web-sites-restore.md) 합니다.

## <a name="when-you-update-your-web-app"></a>웹 앱을 업데이트하는 시기
자동 백업을 사용하도록 설정하지 않은 경우 [수동 백업](web-sites-backup.md)을 만들 수 있습니다.

[단계적 배포](web-sites-staged-publishing.md)를 사용할 수 있습니다. 이 옵션을 사용 하면 게시-나란히 실행 하는 배포를 준비 하는 업데이트 tooa 프로덕션 배포에 합니다. 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


