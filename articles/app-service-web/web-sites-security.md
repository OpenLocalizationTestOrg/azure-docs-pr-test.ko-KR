---
title: "Azure 앱 서비스의 앱 aaaSecure"
description: "자세한 내용은 방법 toosecure 웹 앱, 모바일 앱 백 엔드, 또는 Azure 앱 서비스에서 API 앱."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 5ce560b4-42d7-4b20-935c-0445fd539e39
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: fceef7963b29516f33602dcd50591d14309bf188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>Azure 앱 서비스에서 앱 보안
이 문서는 웹앱, 모바일 앱 백 엔드 또는 Azure 앱 서비스의 API 앱 보안 설정을 시작할 때 도움이 됩니다. 

Azure 앱 서비스의 보안에는 두 가지 수준이 있습니다. 

* **인프라 및 플랫폼 보안** -트러스트 Azure toohave hello 서비스 hello 클라우드에 안전 하 게 실행 tooactually 가지가 필요 합니다.
* **응용 프로그램 보안** -toodesign hello 앱 자체를 안전 하 게 해야 합니다. 여기에 Azure Active Directory와 통합 하는 방법, 인증서를 관리 하는 방법 및 어떻게 해야 안전 하 게 toodifferent 서비스 대화할 수 있습니다. 

#### <a name="infrastructure-and-platform-security"></a>인프라 및 플랫폼 보안
앱 서비스는 hello Azure Vm, 저장소, 네트워크 연결, 웹 프레임 워크, 관리 및 통합 기능 및 더 많은 유지 하기 때문에 적극적으로 보호 되며 확정 있도록 규정 준수를 통해 이동 하 고 지속적으로 toomake에 있는지 확인 입니다.

* 앱 서비스 앱이 두 hello 인터넷에서에서 격리 하 고에서 hello 다른 고객의 Azure 리소스입니다.
* 앱 서비스 앱 및 기타 리소스 그룹의 Azure 리소스(예: SQL 데이터베이스) 간의 비밀 정보(예: 연결 문자열) 통신이 Azure 내에 유지되고 다른 네트워크 경계를 벗어나지 않습니다. 비밀 정보는 항상 암호화됩니다.
* 앱 서비스 앱 및 외부 리소스(예: PowerShell 관리, 명령줄 인터페이스, Azure SDK, REST API 및 하이브리드 연결) 간의 모든 통신은 적절하게 암호화됩니다.
* 24시간 위협 관리를 통해 맬웨어, DDoS(배포된 서비스 거부), MITM(메시지 가로채기) 및 기타 위협으로부터 앱 서비스 리소스를 보호합니다. 

Azure의 인프라 및 플랫폼 보안에 대한 자세한 내용은 [Azure 보안 센터](https://azure.microsoft.com/support/trust-center/security/)를 참조하세요.

#### <a name="application-security"></a>응용 프로그램 보안
Azure hello 인프라 및 응용 프로그램에서 실행 되는 플랫폼에 보안 설정에 대 한 책임이 책임 toosecure는 자체 응용 프로그램입니다. Toodevelop, 필요한 즉, 배포 하 고 안전 하 게에서 응용 프로그램 코드와 콘텐츠를 관리 합니다. 이렇게 하지 않으면 응용 프로그램 코드 또는 콘텐츠 여전히 취약 toothreats 같은 수: 있습니다.

* SQL 삽입
* 세션 하이재킹
* 교차 사이트 스크립팅
* 응용 프로그램 수준 MITM
* 응용 프로그램 수준 DDoS

웹 기반 응용 프로그램에 대 한 보안 고려 사항에 대 한 자세한 내용은이 문서의 hello 범위를 벗어납니다. 응용 프로그램 보안에 대 한 자세한 지침에 대 한 시작 점으로 hello 참조 [열기 웹 응용 프로그램 보안 프로젝트 (OWASP)](https://www.owasp.org/index.php/Main_Page), 특히 hello [상위 10 개의 프로젝트.](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), 어떤 목록에는 현재 상위 10 hello 중요 한 웹 응용 프로그램 보안 결함을 OWASP 멤버를 기준으로 합니다.

## <a name="perform-penetration-testing-on-your-app"></a>앱에 대한 침투 테스트 수행
앱 서비스 앱에 대 한 취약점 toouse hello에 대 한 테스트로 시작 하는 가장 쉬운 방법으로 tooget hello 중 하나 [와 Tinfoil Security 통합](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) tooperform 한 번의 클릭 취약점 응용 프로그램에서 검색 합니다. 이해 하기 쉬운 보고서에 hello 테스트 결과 검토 하 고 알아볼 수 있습니다 어떻게 toofix 단계별 지침이 포함 된 각 취약점입니다.

사용자 고유의 침투 테스트 또는 toouse 다른 스캐너 제품군 또는 공급자를 hello 따라야 tooperform 선호 하는 경우 [승인 프로세스를 테스트 하는 Azure 침투](https://security-forms.azure.com/penetration-testing/terms) 가져오고, 사전 승인 tooperform 원하는 hello 침투 테스트 합니다.

## <a name="https"></a> 고객과 보안 통신
Hello를 사용 하는 경우  **\*. azurewebsites.net** 도메인 이름, 앱 서비스 앱에 대해 만든 모든 SSL 인증서를 제공 하는 HTTPS를 즉시 사용할 수 있습니다  **\*. azurewebsites.net** 도메인 이름입니다. 사이트를 사용 하는 경우는 [사용자 지정 도메인 이름을](app-service-web-tutorial-custom-domain.md), 너무 SSL 인증서를 업로드할 수[HTTPS를 활성화](app-service-web-tutorial-custom-ssl.md) hello 사용자 지정 도메인에 대 한 합니다.

사용 하도록 설정 [HTTPS](https://en.wikipedia.org/wiki/HTTPS) 앱과 사용자 간의 통신 hello에 대 한 MITM 공격 으로부터 보호할 수 있습니다.

## <a name="secure-data-tier"></a>데이터 계층 보안
앱 서비스는 항상 SQL 데이터베이스와 통합 되어, hello 이러한 앱에서 실행 한 모든 hello 연결 문자열 hello 보드 간에 암호화 된 hello VM에만 암호가 해독 됩니다 *및* 만 때 앱이 실행을 hello 합니다. 또한 Azure SQL 데이터베이스는 기본적으로 포함 하는 사이버 위협 요소 로부터 응용 프로그램 데이터를 보호 하는 많은 보안 기능 toohelp [휴지 암호화](https://msdn.microsoft.com/library/dn948096.aspx), [항상 암호화](https://msdn.microsoft.com/library/mt163865.aspx), [ 동적 데이터 마스킹](../sql-database/sql-database-dynamic-data-masking-get-started.md), 및 [위협 검색](../sql-database/sql-database-threat-detection.md)합니다. 중요 한 데이터 또는 규정 준수 요구 하는 경우 참조 [SQL 데이터베이스를 보호](../sql-database/sql-database-security-overview.md) 방법에 대 한 자세한 내용은 toosecure 데이터입니다.

ClearDB, 등의 제 3 자 데이터베이스 공급자를 사용 하는 경우 보안 모범 사례에 직접 hello 공급자의 설명서를 참조 하십시오.  

## <a name="develop"></a> 개발 및 배포 보안
### <a name="publishing-profiles-and-publish-settings"></a>게시 프로필 및 게시 설정
응용 프로그램을 개발할 때는 관리 작업을 수행 하거나와 같은 유틸리티를 사용 하 여 작업 자동화 **Visual Studio**, **웹 매트릭스**, **Azure PowerShell** 또는 hello **Azure CLI (명령줄 인터페이스 Azure)**, 하나를 사용할 수는 *게시 설정* 파일 또는 *게시 프로필*합니다. 두 파일 형식을 azure를 인증 하 고 tooprevent 무단 액세스를 보호 해야 합니다.

* **게시 설정** 파일에 포함된 내용
  
  * Azure 구독 ID
  * 구독에 대 한 tooperform 관리 작업을 허용 하는 관리 인증서 *계정 이름 또는 암호가 tooprovide 필요 없이*합니다.
* **게시 프로필** 파일에 포함된 내용
  
  * Tooyour 앱 게시에 대 한 정보

게시 설정 파일 또는 게시 프로필 파일을 사용 하는 유틸리티를 사용 하는 경우 hello 게시 설정을 포함 하는 hello 파일을 가져오거나 hello 유틸리티에 프로 파일링 차례로 **삭제** hello 파일입니다. Hello 파일을 유지 해야 하는 경우 tooshare hello 프로젝트에서 작업 하는 예를 들어 다른 사용자와 저장을 안전한 위치에 같은 *암호화 된* 권한이 제한 된 디렉터리입니다.

또한 hello 가져온 자격 증명은 보호 되어 있는지 확인 해야 합니다. 예를 들어 **Azure PowerShell** 및 hello **Azure CLI (명령줄 인터페이스 Azure)** 둘 다에서 가져온된 정보를 저장소 프로그램 **홈 디렉터리** ( *~*  Linux 또는 OS X 시스템에서 및 */사용자/yourusername* Windows 시스템에서.) 추가적인 보안을 지정할 수 있습니다 너무**암호화** 중인 운영 체제에 사용할 수 있는 암호화 도구를 사용 하 여 이러한 위치입니다.

### <a name="configuration-settings-and-connection-strings"></a>구성 설정 및 연결 문자열
일반적인 연습 toostore 연결 문자열, 인증 자격 증명 및 구성 파일의 다른 중요 한 정보는 합니다. 불행히도 이러한 파일은 웹 사이트에 노출되거나 공용 저장소에 체크 인되어 이 정보가 노출될 수 있습니다. 간단히 검색 [GitHub](https://github.com), 예를 들어 hello 공용 저장소에 노출 된 비밀 정보를 사용 하 여 다양 한 구성 파일을 확인할 수 있습니다.

가장 좋은 방법은 hello tookeep 응용 프로그램의 구성 파일에서이 정보는 합니다. 앱 서비스를 사용 하면 hello 런타임 환경으로의 일부로 구성 정보를 저장할 **앱 설정** 및 **연결 문자열**합니다. hello 값을 통해 런타임에 노출된 tooyour 응용 프로그램은 *환경 변수* 대부분의 프로그래밍 언어에 대 한 합니다. .NET 응용 프로그램의 경우에는 이러한 값이 런타임에 .NET 구성에 주입됩니다. 이러한 경우 외에도 이러한 구성 설정은 유지 됩니다 암호화 된 확인 하거나 구성 하지 않는 한 hello를 사용 하 여 [Azure 포털](https://portal.azure.com) 또는 PowerShell 또는 Azure CLI hello와 같은 유틸리티입니다. 

앱 서비스의 구성 정보를 저장 하면 hello 응용 프로그램의 관리자 toolock 다운 hello 프로덕션 앱에 대 한 중요 한 정보에 대 한 가능한 있습니다. 개발자는 앱 개발에 대 한 별도의 구성 설정 집합을 사용할 수 있습니다 및 hello 설정을 자동으로 앱 서비스에서 구성 된 hello 설정으로 대체 될 수 있습니다. 포함 hello 개발자 tooknow hello 비밀 hello 프로덕션 앱에 대해 구성 해야 합니다. 앱 서비스에서 앱 설정 및 연결 문자열 구성에 대한 자세한 내용은 [웹앱 구성](web-sites-configure.md)을 참조하세요.

### <a name="ftps"></a>FTPS
Azure 앱 서비스를 통해 응용 프로그램에 대 한 보안 FTP 액세스 toohello 파일 시스템 제공 **FTPS**합니다. 이렇게 하면 진단: hello 웹 앱에 대 한 액세스 hello 응용 프로그램 코드 toosecurely 로그 합니다. FTP 대신 FTPS를 항상 사용하는 것이 좋습니다. 

단계를 수행 하는 hello로 응용 프로그램에 대 한 hello FTPS 링크를 찾을 수 있습니다.

1. 열기 hello [Azure 포털](https://portal.azure.com)합니다.
2. **모두 찾아보기**를 선택합니다.
3. Hello에서 **찾아보기** 블레이드를 **응용 프로그램 서비스**합니다.
4. Hello에서 **응용 프로그램 서비스** 블레이드, 선택 hello 필요한 앱입니다.
5. Hello 앱 블레이드에서 선택 **모든 설정을**합니다.
6. Hello에서 **설정** 블레이드를 **속성**합니다.
7. hello FTP 및 FTPS 링크에서 제공 되는 hello **설정을** 블레이드입니다. 

FTPS에 대한 자세한 내용은 [File Transfer Protocol](http://en.wikipedia.org/wiki/File_Transfer_Protocol)(영문)을 참조하세요.

## <a name="next-steps"></a>다음 단계
보고 하는 방법은 hello Azure 플랫폼의 hello 보안에 대 한 자세한 내용은 **보안 문제나 남용**, 또는 tooinform 수행 하려는 Microsoft **침투** 의 사용자 사이트의 hello hello 보안 섹션을 참조 하십시오 [Microsoft Azure 보안 센터](https://azure.microsoft.com/support/trust-center/security/)합니다.

앱 서비스 앱의 **web.config** 또는 **applicationhost.config** 파일에 대한 자세한 내용은 [Azure App Service 웹앱에서 잠금 해제된 구성 옵션](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/)을 참조하세요.

공격을 감지하는 데 유용할 수 있는 앱 서비스 앱의 로깅 정보에 대한 자세한 내용은 [진단 로깅 사용](web-sites-enable-diagnostic-log.md)을 참조하세요.

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 앱 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

