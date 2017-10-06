---
title: "aaaCreate 및 하이브리드 연결 관리 | Microsoft Docs"
description: "하이브리드 연결을 toocreate hello 연결을 관리 하 고 hello 하이브리드 연결 관리자를 설치 하는 방법을 알아봅니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 561d8f3dd97318130a05c3bb2874ee8022e7f417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-hybrid-connections"></a>하이브리드 연결 만들기 및 관리

> [!IMPORTANT]
> BizTalk 하이브리드 연결은 사용 중지되고 App Service 하이브리드 연결로 대체됩니다. 를 비롯 한 자세한 내용은 toomanage 기존 BizTalk 하이브리드 연결을 확인 하려면 어떻게 해야 [Azure 앱 서비스 하이브리드 연결](../app-service/app-service-hybrid-connections.md)합니다.


## <a name="overview-of-hello-steps"></a>Hello 단계의 개요
1. Hello를 입력 하 여 하이브리드 연결을 만들 **호스트 이름** 또는 **FQDN** 개인 네트워크에 hello 온-프레미스 리소스의 합니다.
2. Azure 웹 앱 또는 Azure 모바일 앱 toohello 하이브리드 연결을 연결 합니다.
3. 온-프레미스 리소스에 대해 hello 하이브리드 연결 관리자를 설치 하 고 연결 toohello 특정 하이브리드 연결 합니다. Azure 포털 hello 단일 클릭 환경을 tooinstall 제공 하 고 연결 합니다.
4. 하이브리드 연결을 관리하고 연결 키를 관리합니다.

이 항목에서는 이러한 단계를 나열합니다. 

> [!IMPORTANT]
> 가능한 tooset 하이브리드 연결 끝점 tooan IP 주소는 IP 주소를 사용 하는 경우 있거나 클라이언트에 따라 hello 온-프레미스 리소스에 도달 하지 않을 수 있습니다. 하이브리드 연결 hello DNS 조회를 수행 하는 hello 클라이언트에 따라 달라 집니다. 대부분의 경우에서 hello **클라이언트** 응용 프로그램 코드입니다. 클라이언트에서 DNS 조회를 수행 하지 않습니다, (시도 하지 않습니다 tooresolve hello IP 주소는 도메인 이름 (x.x.x.x) 하는 경우), 경우 hello 다음 hello 하이브리드 연결을 통해 트래픽을 전송 되지 않습니다.
> 
> 예를 들어, **10.4.5.6** (의사 코드)을 온-프레미스 호스트로 정의합니다.
> 
> **다음 시나리오 작동 hello:**  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves too127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> **시나리오를 따르는 hello 작동 하지 않습니다.**  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route toohost`
> 
> 

## <a name="CreateHybridConnection"></a>하이브리드 연결 만들기
하이브리드 연결을 만들 수 있습니다 hello 웹 응용 프로그램을 사용 하 여 Azure 포털 **또는** BizTalk 서비스를 사용 하 여 합니다. 

**웹 앱을 사용 하 여 하이브리드 연결 toocreate**, 참조 [Azure 웹 앱 연결 tooan 온-프레미스 리소스](../app-service-web/web-sites-hybrid-connection-get-started.md)합니다. 또한 기본 hello 메서드인 웹 앱에서 하이브리드 연결 관리자 (HCM) hello를 설치할 수 있습니다. 

**BizTalk 서비스에 하이브리드 연결이 toocreate**:

1. Toohello 로그인 [Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.
2. Hello 왼쪽된 탐색 창에서 선택 **BizTalk 서비스** 한 다음 BizTalk 서비스를 선택 합니다. 
   
    기존 BizTalk 서비스가 없는 경우 [BizTalk 서비스를 만들 수](biztalk-provision-services.md)있습니다.
3. 선택 hello **하이브리드 연결** 탭:  
   ![하이브리드 연결 탭][HybridConnectionTab]
4. 선택 **하이브리드 연결을 만들** 또는 선택 hello **추가** hello 작업 표시줄에서 단추입니다. Hello 다음을 입력 합니다.
   
   | 속성 | 설명 |
   | --- | --- |
   | 이름 |hello 하이브리드 연결 이름은 고유 해야 하며 hello 수 없습니다 이름이 hello BizTalk 서비스입니다. 어떤 이름을 입력해도 괜찮지만 용도에 맞는 구체적인 이름을 입력하는 것이 좋습니다. 이러한 예로 다음이 포함됩니다.<br/><br/>Payroll*SQLServer*<br/>SupplyList*SharepointServer*<br/>Customers*OracleServer* |
   | 호스트 이름 |Hello 호스트 이름만 hello 정규화 된 호스트 이름을 입력 하거나 hello hello 온-프레미스 리소스의 IPv4 주소입니다. 예를 들면 다음과 같습니다.<br/><br/>mySQLServer<br/>*mySQLServer*.*Domain*.corp.*yourCompany*.com<br/>*myHTTPSharePointServer*<br/>*myHTTPSharePointServer*.*yourCompany*.com<br/>10.100.10.10<br/><br/>Hello IPv4 주소를 사용 하면 note 클라이언트 또는 응용 프로그램 코드 hello IP 주소를 확인 하지 않을 수 있습니다. Hello 중요 참조 hello 위쪽이 항목의 참고 합니다. |
   | 포트 |Hello 온-프레미스 리소스의 hello 포트 번호를 입력 합니다. 예를들어, 웹앱을 사용하는 경우 포트 80 또는 443을 입력합니다. SQL Server를 사용하는 경우 포트 1433을 입력합니다. |
5. Hello 확인 표시가 toocomplete hello 설치 프로그램을 선택 합니다. 

#### <a name="additional"></a>추가 항목
* 하이브리드 연결을 여러 개 만들 수 있습니다. Hello 참조 [BizTalk 서비스: 버전 차트](biztalk-editions-feature-chart.md) hello 수가 허용 되는 연결에 대 한 합니다. 
* 각 하이브리드 연결은 송신하는 응용 프로그램 키와 수신하는 온-프레미스 키, 연결 문자열 쌍으로 생성됩니다. 각 쌍에는 기본 및 보조 키가 있습니다. 

## <a name="LinkWebSite"></a>Azure App Service Web App 또는 Mobile App 연결
Azure 앱 서비스 tooan 기존 하이브리드 연결의에서 웹 응용 프로그램 또는 모바일 앱 toolink 선택 **기존 하이브리드 연결을 사용 하 여** hello 하이브리드 연결 블레이드에서 합니다. [Azure App Service에서 하이브리드 연결을 사용하여 온-프레미스 리소스에 액세스](../app-service-web/web-sites-hybrid-connection-get-started.md)를 참조하세요.

## <a name="InstallHCM"></a>Hello 하이브리드 연결 관리자 온-프레미스를 설치 합니다.
하이브리드 연결을 만든 후 hello 온-프레미스 리소스에 hello 하이브리드 연결 관리자를 설치 합니다. 이 관리자는 Azure 웹앱이나 BizTalk 서비스에서 다운로드할 수 있습니다. BizTalk 서비스 단계는 다음과 같습니다. 

1. Toohello 로그인 [Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.
2. Hello 왼쪽된 탐색 창에서 선택 **BizTalk 서비스** 한 다음 BizTalk 서비스를 선택 합니다. 
3. 선택 hello **하이브리드 연결** 탭:  
   ![하이브리드 연결 탭][HybridConnectionTab]
4. Hello 작업 표시줄에서 선택 **온-프레미스 설정과**:  
   ![온-프레미스 설치][HCOnPremSetup]
5. 선택 **설치 및 구성** toorun 또는 다운로드 hello 하이브리드 연결 관리자 hello에 온-프레미스 시스템입니다. 
6. Hello 확인 표시가 toostart hello 설치를 선택 합니다. 

<!--
You can also download hello Hybrid Connection Manager MSI file and copy hello file tooyour on-premises resource. Specific steps:

1. Copy hello on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for hello specific steps.
2. Download hello Hybrid Connection Manager MSI file. 
3. On hello on-premises resource, install hello Hybrid Connection Manager from hello MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a>추가 항목
* 하이브리드 연결 관리자 hello 다음 운영 체제에 설치할 수 있습니다.
  
  * Windows Server 2008 R2(.NET Framework 4.5+ 및 Windows Management Framework 4.0+ 필수)
  * Windows Server 2012 (Windows Management Framework 4.0+ 필수)
  * Windows Server 2012 R2
* Hello 하이브리드 연결 관리자를 설치한 후에 hello 다음과 같은 결과가 발생 합니다. 
  
  * Azure에서 호스팅되는 하이브리드 연결 hello는 자동으로 구성 된 toouse hello 기본 응용 프로그램 연결 문자열입니다. 
  * hello 온-프레미스 리소스는 자동으로 구성 된 toouse hello 기본 온-프레미스 연결 문자열입니다.
* hello 하이브리드 연결 관리자는 권한 부여에 대 한 유효한 온-프레미스 연결 문자열을 사용 해야 합니다. hello Azure 웹 앱 또는 모바일 앱 권한 부여에 대 한 올바른 응용 프로그램 연결 문자열을 사용 해야 합니다.
* Hello 하이브리드 연결 관리자의 다른 인스턴스가 다른 서버에 설치 하 여 하이브리드 연결을 확장할 수 있습니다. 첫 번째 온-프레미스 수신기 hello로 hello 온-프레미스 수신기 toouse hello 동일한 주소를 구성 합니다. 이 경우 hello 트래픽을 임의로 분산된 (라운드 로빈) hello 활성 온-프레미스 수신기 간에 경우 

## <a name="ManageHybridConnection"></a>하이브리드 연결 관리
toomanage 하이브리드 연결을 할 수 있습니다.

* Hello Azure 포털을 사용 하 하며 tooyour BizTalk 서비스를 이동. 
* [REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)를 사용합니다.

#### <a name="copyregenerate-hello-hybrid-connection-strings"></a>Hello 하이브리드 연결 문자열을 복사/재생성 합니다.
1. Toohello 로그인 [Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.
2. Hello 왼쪽된 탐색 창에서 선택 **BizTalk 서비스** 한 다음 BizTalk 서비스를 선택 합니다. 
3. 선택 hello **하이브리드 연결** 탭:  
   ![하이브리드 연결 탭][HybridConnectionTab]
4. Hello 하이브리드 연결을 선택 합니다. Hello 작업 표시줄에서 선택 **연결 관리**:  
   ![옵션 관리][HCManageConnection]
   
    **연결을 관리** 목록 hello 응용 프로그램 및 온-프레미스 연결 문자열입니다. Hello 연결 문자열을 복사 하거나 hello hello 연결 문자열에 사용 되는 액세스 키를 다시 생성할 수 있습니다. 
   
    **다시 생성을 선택 하는 경우**, hello 연결 문자열이 변경 된 hello 내에서 사용 되는 공유 액세스 키입니다. 다음 hello지 않습니다.
   
   * Hello Azure 클래식 포털에서에서 선택 **키 동기화** hello Azure 응용 프로그램에에서 있습니다.
   * 다시 실행 하는 hello **온-프레미스 설정과**합니다. Hello를 다시 실행 하는 경우 온-프레미스 설정, 온-프레미스 리소스를 자동으로 hello toouse 업데이트 hello 기본 연결 문자열 구성.

#### <a name="use-group-policy-toocontrol-hello-on-premises-resources-used-by-a-hybrid-connection"></a>사용 하 여 그룹 정책 toocontrol hello 온-프레미스 하이브리드 연결을 사용 하는 리소스
1. Hello 다운로드 [하이브리드 연결 관리자 관리 템플릿](http://www.microsoft.com/download/details.aspx?id=42963)합니다.
2. Hello 파일을 추출 합니다.
3. 그룹 정책을 수정 하는 hello 컴퓨터에서 수행 hello를 수행 합니다.  
   
   * Hello를 복사 합니다. ADMX 파일 toohello *%WINROOT%\PolicyDefinitions* 폴더입니다.
   * Hello를 복사 합니다. ADML 파일 toohello *%WINROOT%\PolicyDefinitions\en-us* 폴더입니다.

그룹 정책 편집기 toochange hello 정책을 사용 하 여 복사 합니다.

## <a name="next"></a>다음
[Azure 웹 앱 tooan 연결 온-프레미스 리소스](../app-service-web/web-sites-hybrid-connection-get-started.md)  
[Azure 웹 앱에서 tooon 온-프레미스 SQL Server 연결](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)   
[하이브리드 연결 개요](integration-hybrid-connection-overview.md)

## <a name="see-also"></a>참고 항목
[Microsoft Azure의 BizTalk Services를 관리하기 위한 REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[BizTalk 서비스: Editions 차트](biztalk-editions-feature-chart.md)  
[Azure 클래식 포털을 사용하여 BizTalk 서비스 만들기](biztalk-provision-services.md)  
[BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
