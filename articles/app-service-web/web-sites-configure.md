---
title: "Azure 앱 서비스의 aaaConfigure 웹 응용 프로그램"
description: "어떻게 tooconfigure Azure 앱 서비스의 웹 앱"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a>Azure 앱 서비스에서 웹 앱 구성
이 항목에서는 방법을 사용 하 여 웹 응용 프로그램 tooconfigure hello 설명 [Azure 포털]합니다.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a>응용 프로그램 설정
1. Hello에 [Azure 포털]열고 hello 웹 앱에 대 한 hello 블레이드입니다.
2. **모든 설정**을 클릭합니다
3. **응용 프로그램 설정**을 클릭합니다.

![응용 프로그램 설정][configure01]

hello **응용 프로그램 설정** 블레이드는 여러 범주로 그룹화 된 설정 합니다.

### <a name="general-settings"></a>일반 설정
**프레임워크 버전**. 앱에서 다음 프레임워크를 사용하는 경우 이러한 옵션을 설정합니다. 

* **.NET framework**: 집합 hello.NET framework 버전입니다. 
* **PHP**: 집합 hello PHP 버전 또는 **OFF** toodisable PHP 합니다. 
* **Java**: 선택 hello Java 버전 또는 **OFF** toodisable Java 합니다. 사용 하 여 hello **웹 컨테이너** Tomcat 및 Jetty 버전 간의 toochoose 옵션입니다.
* **Python**: 선택 hello Python 버전 또는 **OFF** toodisable Python 합니다.

기술적인 이유로 Java 앱에 대 한 사용할 hello.NET, PHP 및 Python 옵션이 없습니다.

<a name="platform"></a>
**플랫폼**. 응용 프로그램이 32비트 또는 64비트 환경에서 실행되는지 선택합니다. hello 64 비트 환경에 기본 또는 표준 모드가 필요합니다. 무료 및 공유 모드는 항상 32비트 환경에서 실행됩니다.

**웹 소켓**. 설정 **ON** tooenable hello WebSocket 프로토콜 예: 웹 앱을 사용 하는 경우 [ASP.NET SignalR] 또는 [socket.io]합니다.

<a name="alwayson"></a>
**Always On**. 기본적으로 웹 앱은 일정 기간 동안 유휴 상태인 경우 언로드됩니다. Hello 시스템을 리소스를 절약할 수 있습니다. 기본 또는 표준 모드에서는 사용할 수 있습니다 **Always On** tookeep hello 응용 프로그램이 항상 hello를 로드 합니다. 연속 Webjob을 실행 하는 응용 프로그램 또는 CRON 식을 사용 하 여 WebJobs 실행 발생, 설정 해야 하는 경우 **Always On**, 또는 hello 웹 작업이 안정적으로 실행 되지 않을 수 있습니다.

**관리되는 파이프라인 버전**. 집합 hello IIS [파이프라인 모드]합니다. 둡니다 이전 버전의 IIS 필요로 하는 레거시 앱이 있는 경우가 아니면이 tooIntegrated (hello 기본값)를 설정 합니다.

**자동 교체**. 배포 슬롯에 대 한 자동 전환을 사용 하도록 설정 하면 앱 서비스를 자동으로 바꾸어 hello 웹 응용 프로그램 프로덕션 환경으로 업데이트 toothat 슬롯을 푸시할 때 합니다. 자세한 내용은 참조 [toostaging 슬롯 Azure 앱 서비스의 웹 앱에 대 한 배포](web-sites-staged-publishing.md)합니다.

### <a name="debugging"></a>디버그
**원격 디버깅**. 원격 디버깅을 사용하도록 설정합니다. Hello 원격 디버거 tooyour 웹 앱을 직접 사용 하도록 설정 하면 Visual Studio tooconnect에서 사용할 수 있습니다. 원격 디버깅은 48시간 동안 사용 가능한 상태로 유지됩니다. 

### <a name="app-settings"></a>앱 설정
이 섹션에는 시작 시 웹 앱이 로드하는 이름/값 쌍을 포함합니다. 

* .NET 앱의 경우, 이 설정은 런타임 시 .NET 구성 `AppSettings`으로 주입되어 기존 설정을 재정의합니다. 
* PHP, Python, Java 및 Node 응용 프로그램에서는 런타임에 환경 변수로 이러한 설정에 액세스할 수 있습니다. 각 응용 프로그램 설정에 대해 두 개의 환경 변수 만들어집니다. hello 지정 된 이름의 hello 응용 프로그램 설정 항목 및 APPSETTING_의 접두사와 함께 다른 하나입니다. 둘 다 포함 hello 동일한 값입니다.

### <a name="connection-strings"></a>연결 문자열
연결된 리소스의 연결 문자열입니다. 

.NET 응용 프로그램에 대 한이 연결 문자열은.NET 구성에 삽입 `connectionStrings` hello 키가 동일한 기존 항목을 재정의 하는 런타임 시 설정 hello 연결 된 데이터베이스 이름입니다. 

PHP, Python, Java 및 노드 응용 프로그램의 경우 이러한 설정이 hello 연결 유형 접두사로 런타임 시 환경 변수로 사용 됩니다. hello 환경 변수 접두사는 다음과 같습니다. 

* SQL Server: `SQLCONNSTR_`
* MySQL: `MYSQLCONNSTR_`
* SQL 데이터베이스: `SQLAZURECONNSTR_`
* 사용자 지정: `CUSTOMCONNSTR_`

MySql 연결 문자열 이름이 지정 된 경우 등 `connectionstring1`, hello 환경 변수를 통해 액세스 됩니다 `MYSQLCONNSTR_connectionString1`합니다.

### <a name="default-documents"></a>기본 문서
hello 기본 문서는 웹 사이트에 대 한 hello 루트 URL에 표시 되는 hello 웹 페이지입니다.  hello hello 목록에서 첫 번째 일치 하는 파일 사용 됩니다. 

웹 앱에서는 정적 콘텐츠를 제공하는 대신 URL을 기반으로 라우팅되는 모듈을 사용할 수 있으며, 이 경우에도 기본 문서는 없습니다.    

### <a name="handler-mappings"></a>처리기 매핑
이 영역 tooadd 사용자 지정 스크립트 프로세서 toohandle 요청을 사용 하 여 특정 파일 확장명에 대 한 합니다. 

* **확장명**. 예: *.php 또는 handler.fcgi hello 파일 확장명 toobe 처리합니다. 
* **스크립트 프로세서 경로**. hello hello 스크립트 프로세서의 절대 경로입니다. Hello 파일 확장명과 일치 하는 요청 toofiles hello 스크립트 프로세서에 의해 처리 됩니다. Hello 경로 사용 `D:\home\site\wwwroot` toorefer tooyour 응용 프로그램의 루트 디렉터리입니다.
* **추가 인수**. Hello 스크립트 프로세서에 대 한 선택적인 명령줄 인수 

### <a name="virtual-applications-and-directories"></a>가상 응용 프로그램 및 디렉터리
tooconfigure 가상 응용 프로그램 및 디렉터리의 경우 각 가상 디렉터리와 그에 해당 하는 실제 경로 상대 toohello 웹 사이트 루트를 지정 합니다. 필요에 따라 hello를 선택할 수 있습니다 **응용 프로그램** 확인란 toomark 응용 프로그램으로 가상 디렉터리입니다.

## <a name="enabling-diagnostic-logs"></a>진단 로그를 사용하도록 설정
tooenable 진단 로그:

1. 웹 앱에 대 한 hello 블레이드에서 클릭 **모든 설정을**합니다.
2. **진단 로그**를 클릭합니다. 

로깅을 지원하는 웹 응용 프로그램의 진단 정보를 기록하는 옵션입니다. 

* **응용 프로그램 로깅**. Toohello 파일 시스템 응용 프로그램 로그를 기록합니다. 로깅은 12시간 동안 유지됩니다. 

**수준**. 응용 프로그램 로깅을 사용 하는 경우이 옵션 hello 기록 된 (오류, 경고, 정보 또는 Verbose) 되는 정보의 양을 지정 합니다.

**웹 서버 로깅**. 로그는 hello W3C 확장된 로그 파일 형식에 저장 됩니다. 

**자세한 오류 메시지**. 자세한 오류 메시지는.htm 파일로 저장됩니다. hello 파일 /LogFiles/DetailedErrors 아래 저장 됩니다. 

**실패한 요청 추적**. 로그 요청 tooXML 파일에 실패 했습니다. hello 파일 저장 된/로그 파일이/W3SVC*xxx*여기서 xxx는 고유 식별자입니다. 이 폴더에는 하나의 XSL 파일 및 하나 이상의 XML 파일이 포함되어 있습니다. 서식을 지정 하 고 hello XML 파일의 내용을 hello 필터링 기능을 제공 하기 때문에 있는지 toodownload hello XSL 파일을 확인 합니다.

tooview hello 로그 파일을 만들어야 합니다 FTP 자격 증명 다음과 같습니다.

1. 웹 앱에 대 한 hello 블레이드에서 클릭 **모든 설정을**합니다.
2. **배포 자격 증명**을 클릭합니다.
3. 사용자 이름 및 암호를 입력합니다.
4. **Save**를 클릭합니다.

![배포 자격 증명 설정][configure03]

hello 전체 FTP 사용자 이름이 "app\username" 여기서 *앱* hello 웹 응용 프로그램 이름입니다. hello 사용자 이름에에서 나열 된 hello 웹 앱 블레이드 아래 **Essentials**합니다.  

![FTP 배포 자격 증명][configure02]

## <a name="other-configuration-tasks"></a>기타 구성 작업
### <a name="ssl"></a>SSL
기본 또는 표준 모드에서는 사용자 지정 도메인에 대해 SSL 인증서를 업로드할 수 있습니다. 자세한 내용은 [웹 앱에 대한 HTTPS 사용]을 참조하세요. 

tooview 업로드 된 인증서를 클릭 하 여 **모든 설정을** > **사용자 지정 도메인 및 SSL**합니다.

### <a name="domain-names"></a>도메인 이름
웹 앱에 대한 사용자 지정 도메인 이름을 추가합니다. 자세한 내용은 [Azure 앱 서비스에서 웹 앱에 대한 사용자 지정 도메인 이름 구성]을 참조하세요.

tooview 도메인 이름, 클릭 **모든 설정을** > **사용자 지정 도메인 및 SSL**합니다.

### <a name="deployments"></a>배포
* 연속 배포를 설정합니다. 참조 [Git를 사용 하 여 toodeploy Azure 앱 서비스에서 웹 앱](web-sites-deploy.md)합니다.
* 배포 슬롯입니다. 참조 [tooStaging 환경을 Azure 앱 서비스의 웹 앱에 대 한 배포]합니다.

tooview 배포 슬롯을 클릭 하 여 **모든 설정을** > **배포 슬롯**합니다.

### <a name="monitoring"></a>모니터링
기본 또는 표준 모드에서 HTTP 또는 HTTPS 끝점의 가용성을 hello toothree 지리적으로 분산 된 위치를 테스트할 수 있습니다. Hello HTTP 응답 코드는 오류 (4xx 또는 5xx) 이거나 hello 응답 하는 데 30 초 이상 모니터링 테스트가 실패 합니다. 끝점에서 모든 hello 모니터링 테스트가 성공 하는 경우 사용할 수 있는 것으로 간주 됩니다 hello 위치를 지정 합니다. 

자세한 내용은 [방법: 웹 끝점 모니터링]을 참조하세요.

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도]앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* [Azure 앱 서비스에서 사용자 지정 도메인 이름 구성]
* [Azure 앱 서비스에서 앱에 대한 HTTPS를 사용하도록 설정]
* [Azure 앱 서비스에서 웹 앱 크기 조정]
* [Azure 앱 서비스에서 웹 앱에 대한 기본 사항 모니터링]

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure 포털]: https://portal.azure.com/
[Azure 앱 서비스에서 사용자 지정 도메인 이름 구성]: ./app-service-web-tutorial-custom-domain.md
[tooStaging 환경을 Azure 앱 서비스의 웹 앱에 대 한 배포]: ./web-sites-staged-publishing.md
[Azure 앱 서비스에서 앱에 대한 HTTPS를 사용하도록 설정]: ./app-service-web-tutorial-custom-ssl.md
[방법: 웹 끝점 모니터링]: http://go.microsoft.com/fwLink/?LinkID=279906
[Azure 앱 서비스에서 웹 앱에 대한 기본 사항 모니터링]: ./web-sites-monitor.md
[파이프라인 모드]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Azure 앱 서비스에서 웹 앱 크기 조정]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[앱 서비스 시도]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
