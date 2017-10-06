---
title: "hello Azure 포털에서에서 Azure BizTalk 서비스 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 tooprovision hello; Azure 포털에서에서 Azure BizTalk 서비스를 만들거나 MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 BizTalk 서비스 만들기

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> toohello Azure 포털에서에서 toosign, Azure 계정 및 Azure 구독 해야합니다. 계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. [Azure 무료 평가판](http://go.microsoft.com/fwlink/p/?LinkID=239738)을 참조하세요.


## <a name="CreateService"></a>BizTalk 서비스 만들기
Hello 선택한 버전에 따라 BizTalk 서비스 설정의 일부만 사용할 수 있습니다.

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.
2. Hello 아래쪽 탐색 창에서 선택 **새로**:  
   ![Hello 새로 만들기 단추를 선택 합니다.][NEWButton]
3. **APP SERVICES** > **BIZTALK SERVICE** > **사용자 지정 만들기**를 선택합니다.  
   ![BizTalk 서비스 선택 및 사용자 지정 만들기 선택][NewBizTalkService]
4. Hello BizTalk 서비스 설정을 입력 합니다.
   
    <table border="1">
    <tr>
    <td><strong>BizTalk 서비스 이름</strong></td>
    <td>아무 이름이나 입력할 수 있지만 구체적이어야 합니다. 일부 사례:<br/><br/>
    <em>mycompany</em>.biztalk.windows.net<br/>
    <em>mycompanymyapplication</em>.biztalk.windows.net<br/>
    <em>myapplication</em>.biztalk.windows.net<br/><br/>". biztalk.windows.net" 입력 하면 자동으로 추가 된 toohello 이름입니다. 이렇게 하면 URL을 같은 BizTalk 서비스를 사용 하는 tooaccess 만들어집니다 <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>합니다.
    </td>
    </tr>
    <tr>
    <td><strong>에디션</strong></td>
    <td>Hello 테스트/개발 단계에 있는 경우 선택 <strong>개발자</strong>합니다. Hello 프로덕션 단계에 있는 경우 사용 하 여 hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk 서비스: 버전 차트</a> toodetermine 경우 <strong>프리미엄</strong>, <strong>표준</strong>, 또는 <strong>Basic</strong>hello 비즈니스 시나리오에 대 한 올바른 선택 됩니다.
    </td>
    </tr>
    <tr>
    <td><strong>지역</strong></td>
    <td>지리적인 지역의 toohost hello BizTalk 서비스를 선택 합니다.</td>
    </tr>
    <tr>
    <td><strong>도메인 URL</strong></td>
    <td><strong>옵션</strong>. 기본적으로 hello 도메인 URL은 <em>m e</em>. biztalk.windows.net 합니다. 사용자 지정 도메인을 입력할 수도 있습니다. 예를 들어 도메인이 <em>contoso</em>이면 다음과 같이 입력할 수 있습니다. <br/><br/>
    <em>MyCompany</em>.contoso.com<br/>
    <em>MyCompanyMyApplication</em>.contoso.com<br/>
    <em>MyApplication</em>.contoso.com<br/>
    <em>YourBizTalkServiceName</em>.contoso.com<br/>
    </td>
    </tr>
    </table>
Hello 다음 화살표를 선택 합니다.
5. Hello 저장소 및 데이터베이스 설정을 입력 합니다.  <table border="1">
    <tr>
    <td><strong>저장소 계정 모니터링/보관</strong></td>
    <td>기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다. <br/><br/>새 저장소 계정을 만드는 경우 입력 hello <strong>저장소 계정 이름</strong>합니다.</td>
    </tr>
    <tr>
    <td><strong>데이터베이스 추적</strong></td>
    <td>기존 Azure SQL 데이터베이스를 사용하는 경우 다른 BizTalk 서비스에서는 이 데이터베이스를 사용할 수 없습니다. Hello 로그인 이름 및 Azure SQL 데이터베이스 서버를 만들 때 입력 한 암호가 필요.<br/><br/><strong>팁</strong> hello 추적 데이터베이스 만들기 및 모니터링/보관 저장소 계정에 동일한 지역으로 BizTalk 서비스 hello hello 합니다.</td>
    </tr>
    </table>
Hello 다음 화살표를 선택 합니다.
6. Hello 데이터베이스 설정을 입력 합니다.  <table border="1">
    <tr>
    <td><strong>Name</strong></td>
    <td>경우에 사용 가능한 <strong>새 SQL 데이터베이스 인스턴스를 만들고</strong> hello 이전 화면에서를 선택 합니다.
    <br/><br/>
BizTalk 서비스에서 사용 하는 SQL 데이터베이스 이름 toobe를 입력 합니다.</td>
    </tr>
    <tr>
    <td><strong>서버</strong></td>
    <td>경우에 사용 가능한 <strong>새 SQL 데이터베이스 인스턴스를 만들고</strong> hello 이전 화면에서를 선택 합니다.
    <br/><br/>
기존 SQL Database 서버를 선택하거나 새 SQL Database 서버를 만듭니다.</td>
    </tr>
    <tr>
    <td><strong>서버 로그인 이름</strong></td>
    <td>Hello 로그인 사용자 이름을 입력 합니다.</td>
    </tr>
    <tr>
    <td><strong>서버 로그인 암호</strong></td>
    <td>Hello 로그인 암호를 입력 합니다.</td>
    </tr>
    <tr>
    <td><strong>지역</strong></td>
    <td><strong>새 SQL Database 인스턴스 만들기</strong>를 선택한 경우에 사용할 수 있습니다. 지리적인 지역의 toohost hello SQL 데이터베이스를 선택 합니다.</td>
    </tr>
    </table>

Hello 확인 표시가 toocomplete hello 마법사를 선택 합니다. hello 진행률 아이콘이 나타납니다.  
![완료 시 진행률 아이콘 표시][ProgressComplete]

완료 되 면 생성 되 고 응용 프로그램에 대 한 준비 hello Azure BizTalk 서비스는 합니다. hello 기본 설정을 사용 됩니다. Toochange hello 기본 설정을 선택 **BIZTALK 서비스** 왼쪽된 탐색 창의 hello와 BizTalk 서비스를 선택 합니다. 추가 설정은 hello에 표시 됩니다 [대시보드, 모니터 및 배율 탭](biztalk-dashboard-monitor-scale-tabs.md) hello 위쪽에 있습니다.

Hello hello BizTalk 서비스의 상태에 따라 완료할 수 없는 일부 작업은 합니다. 이러한 작업의 목록에 대 한 이동 너무[BizTalk Services 상태 차트](biztalk-service-state-chart.md)합니다.

## <a name="post-provisioning-steps"></a>프로비전 후 단계
* [로컬 컴퓨터에 hello 인증서 설치](#InstallCert)
* [프로덕션이 준비된 인증서 추가](#AddCert)
* [Hello 액세스 제어 네임 스페이스 가져오기](#ACS)

#### <a name="InstallCert"></a>로컬 컴퓨터에 hello 인증서 설치
BizTalk 서비스 프로비전의 일부로 자체 서명된 인증서가 만들어지고 BizTalk 서비스 구독에 연결됩니다. 이 인증서를 다운로드 하 여 BizTalk 서비스 응용 프로그램을 배포 하거나 송신 메시지 tooa BizTalk 서비스 끝점에서 컴퓨터에 설치 해야 합니다.

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.
2. 선택 **BIZTALK 서비스** 왼쪽된 탐색 창의 hello와 BizTalk 서비스 구독을 선택 합니다.
3. 선택 hello **대시보드** 탭 합니다.
4. **SSL 인증서 다운로드**를 선택합니다.  
   ![SSL 인증서 수정][QuickGlance]
5. Hello 인증서를 두 번 클릭 하 고 hello 마법사 tooinstall hello 인증서를 통해 실행 합니다. Hello 아래의 hello 인증서가 설치 되었는지 확인 **신뢰할 수 있는 루트 인증 기관** 저장 합니다.

#### <a name="AddCert"></a>프로덕션이 준비된 인증서 추가
hello 자체 서명 된 인증서를 개발 환경 에서만 사용 하기 위한 BizTalk 서비스를 만들 때 자동으로 만들어집니다. 프로덕션 시나리오의 경우 이 인증서를 프로덕션이 준비된 인증서로 대체합니다.

1. Hello에 **대시보드** 탭에서 **업데이트 SSL 인증서**합니다.
2. SSL 인증서를 개인 tooyour 찾아보기 (*CertificateName*.pfx) BizTalk 서비스 이름을 포함 하, hello 암호를 입력 한 다음 hello 확인 표시를 클릭 합니다.

#### <a name="ACS"></a>Hello 액세스 제어 네임 스페이스 가져오기
1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.
2. 선택 **BIZTALK 서비스** 왼쪽된 탐색 창의 hello와 BizTalk 서비스를 선택 합니다.
3. Hello 작업 표시줄에서 선택 **연결 정보**:  
   ![연결 정보 선택][ACSConnectInfo]
4. Hello 액세스 제어 값을 복사 합니다.

Visual Studio에서 BizTalk 서비스를 배포할 때 이 액세스 제어 네임스페이스를 입력합니다. BizTalk 서비스에 대 한 액세스 제어 네임 스페이스 hello 자동으로 만들어집니다.

hello 액세스 제어 값 응용 프로그램과 함께 사용할 수 있습니다. Azure BizTalk 서비스를 만들면이 액세스 제어 네임 스페이스는 BizTalk 서비스 배포와 hello 인증을 제어 합니다. Toochange hello 구독 hello 네임 스페이스를 관리할 경우 선택 **ACTIVE DIRECTORY** 왼쪽된 탐색 창의 hello와 네임 스페이스를 선택 합니다. 작업 표시줄 hello 옵션을 나열합니다.

클릭 하면 **관리** 열립니다 hello 액세스 제어 관리 포털. Hello 액세스 제어 관리 포털에서에서 BizTalk 서비스 사용 하 여 hello **서비스 id**:  
![Hello 액세스 제어 관리 포털의에서 ACS 서비스 Id][ACSServiceIdentities]

hello 액세스 제어 서비스 id는 토큰을 수신 하 고 응용 프로그램이 나 클라이언트 tooauthenticate 액세스 제어와 함께 직접 사용할 수 있는 자격 증명의 집합입니다.

> [!IMPORTANT]
> hello BizTalk 서비스는 **소유자** hello 기본 서비스 id 및 hello에 대 한 **암호** 값입니다. Hello 암호 값 대신 hello 대칭 키 값을 사용 하는 경우 hello 다음과 같은 오류가 발생할 수 있습니다.<br/><br/>*지정 된 hello로 toohello 액세스 제어 관리 서비스 계정을 연결할 수 없습니다. 자격 증명*
> 
> 

[ACS 네임스페이스 관리](https://msdn.microsoft.com/library/azure/hh674478.aspx) 에는 일부 지침 및 권장 사항이 나열되어 있습니다.

## <a name="requirements-explained"></a>요구 사항 설명
이러한 요구 사항을 toohello 적용 되지 않는 무료 버전입니다.

<table border="1">
<tr bgcolor="FAF9F9">
        <td><strong>필요한 항목</strong></td>
        <td><strong>필요한 이유</strong></td>
</tr>
<tr>
<td>Azure 구독</td>
<td>hello 구독 toohello Azure 포털에에서 로그인 하려면 사용자를 결정 합니다. hello 계정 보유자에 hello 구독을 만듭니다 <a HREF="https://account.windowsazure.com/Subscriptions"> Azure 구독</a>합니다.
<br/><br/>
hello Azure 계정 구독이 여러 개 있을 수 있습니다 및 허용 되는 사용자가 관리할 수 있습니다. 예를 들어 Azure 계정 소유자 이라는 구독을 만들고 <em>BizTalkServiceSubscription</em> 제공 회사 내에서 BizTalk 관리자 hello 및 (예를 들어 ContosoBTSAdmins@live.com) toothis 구독에 액세스 합니다. 이 시나리오에서는 hello BizTalk 관리자 toohello Azure 포털에에서 로그인 한 전체 관리자 권한 tooall hello 호스팅된 서비스의 Azure BizTalk 서비스를 포함 하 여 hello 구독 합니다. hello BizTalk 관리자 hello Azure 계정 소유자에 게 없는 tooany 청구 정보에 액세스할 했으므로 하지 않습니다.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Hello Azure 포털에서에서 구독 및 저장소 계정 관리</a> 자세한 정보를 제공 합니다.
</td>
</tr>
<tr>
<td>Azure SQL Database</td>
<td>Hello 테이블, 뷰 및 hello hello 추적 데이터를 포함 하는 BizTalk 서비스에서 사용 하는 저장된 프로시저를 저장 합니다.
<br/><br/>
BizTalk 서비스를 만들 때 기존 Azure SQL Server, Azure SQL 데이터베이스를 사용하거나 새로운 서버 또는 데이터베이스를 자동으로 만들 수 있습니다.
<br/><br/>
SQL 데이터베이스의 크기 조정 hello 자동으로 구성 됩니다. 일반적으로 hello 기본 소수 자릿수는 BizTalk 서비스에 대 한 충분 합니다. 변경 hello 눈금 가격에 영향을 줍니다. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Azure SQL Database의 계정 및 대금 청구</a>
 참조<br/><br/>
<strong>참고</strong>
<br/>
<ul>
<li> 새 Azure SQL Server 및 데이터베이스를 만들면 Azure 서비스가 자동으로 사용하도록 설정됩니다. Azure 서비스를 필요로 하는 hello BizTalk 서비스가 사용 하도록 설정 합니다.</li>
<li>기존 Azure SQL Server에 새 Azure SQL 데이터베이스를 만들면 hello 방화벽 규칙의 hello 서버 변경 되지 않습니다. 결과적으로, 있기 다른 Azure 서비스 액세스 toohello 서버 데이터베이스를 허용 되지 않습니다.</li>
</ul>
</td>
</tr>
<tr>
<td>Azure 액세스 제어 네임스페이스</td>
<td>Azure BizTalk 서비스로 인증합니다. Visual Studio에서 BizTalk 서비스를 배포할 때 이 액세스 제어 네임스페이스를 입력합니다. BizTalk 서비스를 만들면 hello Access Control 네임 스페이스 자동으로 만들어집니다.</td>
</tr>

<tr>
<td>Azure Storage 계정</td>
<td>제공은 tootables, blob 및 큐에 BizTalk 서비스 toosave hello 다음에서 사용 하 여 액세스 합니다.

<ul>
<li>로그 파일을 해당 모니터 hello BizTalk 서비스 합니다. 출력을 모니터링 하는 hello hello에도 표시 됩니다 **모니터링** hello Azure 포털에서에서 탭 합니다.</li>
<li>X12 또는 파트너 간에 AS2 규약을 만들 때 hello 보관 기능 toostore 메시지 속성을 설정할 수 있습니다. 이 데이터는 hello 저장소 계정에에서 저장 됩니다.</li>
</ul>
<br/>
BizTalk 서비스를 만들 때 기존 저장소 계정을 사용하거나 새 저장소 계정을 자동으로 만들 수 있습니다.
<br/><br/>
BizTalk 서비스에 대 한 hello 기본 저장소 설정이 됩니다.
<br/><br/>
저장소 계정을 만들면 기본 키와 보조 키가 자동으로 만들어집니다. 이러한 키는 저장소 계정 액세스 tooyour를 제어합니다. hello BizTalk 서비스는 hello 기본 키를 자동으로 사용 합니다.
<br/><br/>
자세한 내용은 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">저장소</a>를 참조하세요.
</td>
</tr>

<tr>
<td>SSL 개인 인증서</td>
<td>
Azure BizTalk 서비스가 만들어지면 BizTalk 서비스 이름이 포함된 HTTPS URL도 만들어집니다. 이 URL은 자동으로 구성 된 toouse 자체 서명 된 개발 전용 인증서입니다. 프로덕션의 경우 개인 SSL 인증서가 필요합니다.
<br/><br/>
<strong>중요 SSL 인증서 정보</strong>

<ul>
<li>hello 인증서 만료 날짜가 5 년 미만인 이어야 합니다.</li>
<li>모든 개인 인증서에는 암호가 필요합니다. 이 암호를 확인하고 관리자와 공유하는 것이 좋습니다.</li>
<li>자체 서명된 인증서는 테스트/개발 환경에서 사용됩니다. 자체 서명 된 인증서를 사용할 때 hello 인증서 tooyour 개인 인증서 저장소를 가져오고 hello 신뢰할 수 있는 루트 인증 기관 인증서 저장소입니다.</li>
</ul>
<br/>Hello 프로덕션 인증서 요청 tooyour 인증 기관을 보낼 때 다음과 같은 인증서 속성 hello를 제공 합니다.
<br/>

<ul>
<li><strong>확장된 키 사용</strong>: Azure BizTalk Services는 최소한 서버 인증이 필요합니다.</li>
<li><strong>일반 이름</strong>: hello 정규화 된 도메인 이름 (FQDN) Azure BizTalk 서비스 URL을 입력 합니다. 이 문서의 <a HREF="#CreateService">BizTalk 서비스 만들기</a>를 참조하세요.</li>
</ul>
<br/>
Hello BizTalk 서비스가 만들어지면 새롭거나 다른 인증서를 추가할 수 있습니다.
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a>하이브리드 연결
Azure BizTalk 서비스를 만들 때 hello **하이브리드 연결** 탭을 사용할 수 있습니다.

![하이브리드 연결 탭][HybridConnectionTab]

하이브리드 연결을 사용 하는 tooconnect Azure 웹 포털 또는 Azure 모바일 서비스 tooany 온-프레미스 SQL Server, MySQL, HTTP 웹 Api, 모바일 서비스 및 대부분의 사용자 지정 웹 서비스와 같은 정적 TCP 포트를 사용 하는 리소스입니다.  하이브리드 연결와 hello BizTalk 어댑터 서비스는 다릅니다. hello BizTalk 어댑터 서비스는 사용 되는 tooconnect Azure BizTalk 서비스 tooan 온-프레미스 업무 (LOB) 시스템입니다.

 참조 [하이브리드 연결](integration-hybrid-connection-overview.md) toolearn 더 만들기 및 관리 하이브리드 연결을 포함 합니다.

## <a name="next-steps"></a>다음 단계
BizTalk 서비스를 만들면 했으므로 숙지 다른 hello [BizTalk 서비스: 대시보드, 모니터 및 배율 탭](biztalk-dashboard-monitor-scale-tabs.md)합니다. 응용 프로그램에 BizTalk 서비스를 사용할 준비가 되었습니다. 응용 프로그램을 이동 너무 만들 toostart[Azure BizTalk 서비스](http://go.microsoft.com/fwlink/p/?LinkID=235197)합니다.

## <a name="see-also"></a>참고 항목
* [BizTalk 서비스: Editions 차트](biztalk-editions-feature-chart.md)<br/>
* [BizTalk Services: 상태 차트](biztalk-service-state-chart.md)<br/>
* [BizTalk 서비스: 백업 및 복원](biztalk-backup-restore.md)<br/>
* [BizTalk 서비스: 제한](biztalk-throttling-thresholds.md)<br/>
* [BizTalk 서비스: 발급자 이름 및 발급자 키](biztalk-issuer-name-issuer-key.md)<br/>
* [Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [VNet](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
