---
title: "aaaAzure AD Connect Health Agent 설치 | Microsoft Docs"
description: "동기화 및 AD FS에 대 한 hello 에이전트 설치를 설명 하는 hello Azure AD Connect Health 페이지입니다."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1cc8ae90-607d-4925-9c30-6770a4bd1b4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9019628ec1d4c477496e08910cfd668ed1933a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-agent-installation"></a>Azure AD Connect Health Agent 설치
이 문서에서는 설치 하 고 hello Azure AD Connect Health Agent를 구성 합니다. hello 에이전트를 다운로드할 수 있습니다 [여기](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent)합니다.

## <a name="requirements"></a>요구 사항
다음 표에 hello은 Azure AD Connect Health를 사용 하기 위한 요구 사항 목록입니다.

| 요구 사항 | 설명 |
| --- | --- |
| Azure AD Premium |Azure AD Connect Health는 Azure AD Premium 기능이기 때문에 Azure AD Premium이 필요합니다. </br></br>자세한 내용은 [Azure AD Premium 시작](../active-directory-get-started-premium.md)을 참조하세요. </br>무료 30 일 평가판을 toostart 참조 [평가판을 시작 합니다.](https://azure.microsoft.com/trial/get-started-active-directory/) |
| 전역 해야 Azure AD Connect Health의 Azure AD tooget 관리자 시작 |기본적으로 hello 전역 관리자만 수 및 설치 및 구성 hello 상태 에이전트 tooget 시작 액세스 hello 포털, Azure AD Connect Health 내에서 작업을 수행 합니다. 자세한 내용은 [Azure AD 디렉터리 관리](../active-directory-administer.md)를 참조하세요. <br><br> 역할 기반 액세스 제어를 사용 하 여 액세스 허용할 수 있습니다 tooAzure AD Connect Health tooother 사용자 조직에 있습니다. 자세한 내용은 [Azure AD Connect Health용 역할 기반 Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)을 참조하세요. </br></br>**중요:** hello 회사 또는 학교 계정 이어야 합니다 hello 에이전트를 설치할 때 사용 되는 계정입니다. Microsoft 계정은 사용할 수 없습니다. 자세한 내용은 [조직으로 Azure 등록](../sign-up-organization.md)을 참조하세요. |
| Azure AD Connect Health Agent는 각 대상 서버에 설치됩니다. | Azure AD Connect Health 바이러스 hello Health Agent toobe를 설치 하 고 대상된 서버 tooreceive hello 데이터에 구성 및 hello 모니터링 및 분석 기능을 제공 </br></br>예를 들어 hello 에이전트는 AD FS 인프라에서 tooget 데이터 hello AD FS 및 웹 응용 프로그램 프록시 서버에 설치 되어야 합니다. 마찬가지로, tooget 데이터를 온-프레미스 AD DS 인프라 hello 에이전트 hello 도메인 컨트롤러에 설치 해야 합니다. </br></br> |
| 아웃 바운드 연결 toohello Azure 서비스 끝점 | 설치 및 런타임 시 hello 에이전트 연결 tooAzure AD Connect Health 서비스 끝점에 필요 합니다. 방화벽을 사용 하 여 아웃 바운드 연결 차단 되 면 확인 끝점 뒤 해당 hello toohello 허용 목록에 추가 됩니다. </br></br><li>&#42;.blob.core.windows.net </li><li>&#42;.servicebus.windows.net - Port: 5671 </li><li>&#42;.adhybridhealth.azure.com/</li><li>https://management.azure.com </li><li>https://policykeyservice.dc.ad.msft.net/</li><li>https://login.windows.net</li><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li> |
|IP 주소를 기반으로 하는 아웃바운드 연결 | IP 주소 기반 toohello 참조 방화벽에 대 한 필터링 [Azure IP 범위](https://www.microsoft.com/en-us/download/details.aspx?id=41653)합니다.|
| 아웃바운드 트래픽에 대한 SSL 조사가 필터링 또는 해제됨 | SSL 검사 또는 hello 네트워크 계층에서 아웃 바운드 트래픽에 대 한 종료 hello 에이전트 등록 단계 또는 데이터 업로드 작업이 실패할 수 있습니다. |
| Hello 에이전트를 실행 하는 hello 서버에서 방화벽 포트입니다. |hello 에이전트 방화벽 포트 toobe hello 에이전트 toocommunicate hello Azure AD Health 서비스 끝점에 대 한 순서에 열을 다음 hello가 필요 합니다.</br></br><li>TCP 포트 443</li><li>TCP 포트 5671</li> |
| IE 보안 강화가 사용 하는 경우 웹 사이트를 따라 hello 허용 |IE 보안 강화를 사용 하는 경우 다음 hello 다음 웹 사이트 수 있어야 하락 toohave hello 에이전트가 설치 된 hello 서버의 합니다.</br></br><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li><li>https://login.windows.net</li><li>hello Azure Active Directory에서 신뢰할 수 있는 조직의 페더레이션 서버입니다. 예: https://sts.contoso.com</li> |
|FIPS 사용 안 함|FIPS는 Azure AD Connect Health 에이전트에서 지원되지 않습니다.|

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-fs"></a>Hello AD FS에 대 한 Azure AD Connect Health Agent 설치
toostart hello 에이전트를 설치, 다운로드 한 hello.exe 파일을 두 번 클릭 합니다. Hello 첫 번째 화면에서 설치를 클릭 합니다.

![Azure AD Connect Health 확인](./media/active-directory-aadconnect-health-requirements/install1.png)

Hello 설치가 완료 되 면 지금 구성를 클릭 합니다.

![Azure AD Connect Health 확인](./media/active-directory-aadconnect-health-requirements/install2.png)

이것은 PowerShell 창 tooinitiate hello 에이전트 등록 프로세스를 시작 합니다. 메시지가 표시 되 면 액세스 tooperform 에이전트 등록에 있는 Azure AD 계정으로 로그인 합니다. 기본적으로 hello 전역 관리자 계정에 액세스할 수 있습니다.

![Azure AD Connect Health 확인](./media/active-directory-aadconnect-health-requirements/install3.png)

로그인한 후 PowerShell이 계속됩니다. 완료 되 면 PowerShell을 닫을 수 있습니다 및 hello 구성이 완료 되었습니다.

이 시점에서 hello 서비스 수 있어야 하는 에이전트 수 있도록 자동으로 hello 에이전트 업로드 hello 필요한 데이터 toohello 클라우드 서비스를 시작 안전 하 게에서 합니다.

Hello 이전 섹션에 설명 된 모든 hello 필수 조건을 충족 하지 않은 경우 경고 hello PowerShell 창에 나타납니다. 수 있는지 toocomplete hello [요구 사항](active-directory-aadconnect-health-agent-install.md#requirements) hello 에이전트를 설치 하기 전에. hello 스크린 샷 다음은 이러한 오류의 예입니다.

![Azure AD Connect Health 확인](./media/active-directory-aadconnect-health-requirements/install4.png)

tooverify hello 에이전트 설치가 완료 된 후, 다음 hello 서버의 서비스는 hello를 찾아보십시오. Hello 구성을 완료 실행 이미 합니다. 그렇지 않으면 hello 구성이 완료 될 때까지 중지 합니다.

* Azure AD Connect Health AD FS Diagnostics Service
* Azure AD Connect Health AD FS Insights Service
* Azure AD Connect Health AD FS Monitoring Service

![Azure AD Connect Health 확인](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a>Windows Server 2008 R2 서버에서 에이전트 설치
Windows Server 2008 R2 서버에 대한 단계:

1. 서비스 팩 1 이상 실행 되 고 해당 hello 서버를 확인 합니다.
2. 에이전트 설치에 대해 IE ESC를 끕니다.
3. 각 hello AD Health agent를 설치 하는 미리 hello 서버에 Windows PowerShell 4.0을 설치 합니다. Windows PowerShell 4.0 tooinstall:
   * 설치 [Microsoft.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779) hello 다음 링크 toodownload hello 오프 라인 설치 관리자를 사용 하 여 합니다.
   * Windows 기능에서 PowerShell ISE를 설치합니다.
   * Hello 설치 [Windows Management Framework 4.0입니다.](https://www.microsoft.com/download/details.aspx?id=40855)
   * 설치 Internet Explorer 버전 10 이상 hello 서버에 있습니다. (Azure 관리자 자격 증명을 사용 하 여 hello 상태 관리 서비스 tooauthenticate에 필요).
4. Windows Server 2008 r 2에서 Windows PowerShell 4.0의 설치에 대 한 자세한 내용은 hello wiki 문서를 참조 하십시오. [여기](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx)합니다.

### <a name="enable-auditing-for-ad-fs"></a>AD FS 감사 사용
> [!NOTE]
> 이 섹션에는 tooAD FS 서버만 적용 됩니다. 없는 toofollow hello 웹 응용 프로그램 프록시 서버에서 다음이 단계입니다.
>

Hello 사용 현황 분석 toogather 기능 및 분석을 위해에서 데이터를 Azure AD Connect Health agent hello hello AD FS 감사 로그의 정보를 hello 필요 합니다. 이러한 로그는 기본적으로 사용하도록 설정되어 있지 않습니다. 프로시저 tooenable AD FS 감사를 수행 하는 사용 하 여 hello 및 toolocate hello AD FS에는 AD FS 서버에서 로그 감사 합니다.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2008-r2"></a>Windows Server 2008 r 2에서 AD FS에 대 한 tooenable 감사
1. 클릭 **시작**, 너무 가리킨**프로그램**, 너무 가리킨**관리 도구**, 클릭 하 고 **로컬 보안 정책**합니다.
2. Toohello 이동 **보안 Settings\Local Policies\User Rights Management** 폴더 보안 감사 생성 두 번 클릭 합니다.
3. Hello에 **로컬 보안 설정** 탭 hello AD FS 2.0 서비스 계정이 목록에 있는지 확인 합니다. 존재 하지 않으면 클릭 **사용자 또는 그룹 추가** toohello 목록 추가 하 고 클릭 **확인**합니다.
4. tooenable 감사 상승 된 권한으로 명령 프롬프트를 열고 및 hello 다음 명령을 실행 합니다.<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code>
5. 로컬 보안 정책을 닫은 다음 hello 관리 스냅인을 엽니다. 관리 스냅인 tooopen hello 클릭 **시작**, 너무 가리킨**프로그램**, 너무 가리킨**관리 도구**, AD를 클릭 한 다음 FS 2.0 관리 합니다.
6. Hello 작업 창에서 페더레이션 서비스 속성 편집을 클릭 합니다.
7. Hello에 **페더레이션 서비스 속성** 대화 상자를 클릭 hello **이벤트** 탭 합니다.
8. 선택 hello **성공 감사** 및 **실패 감사** 확인란 합니다.
9. **확인**을 클릭합니다.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2012-r2"></a>Windows Server 2012 r 2에서 AD FS에 대 한 tooenable 감사
1. 열기 **로컬 보안 정책** 열어 **서버 관리자** hello 시작 화면 또는 hello hello 바탕 화면 작업 표시줄에서 서버 관리자에서 클릭 **도구/로컬 보안 정책**.
2. Toohello 이동 **보안 설정 \ 로컬 정책 \ 사용자 권한 할당** 폴더를 찾아 두 번 클릭 **보안 감사 생성**합니다.
3. Hello에 **로컬 보안 설정** 탭 hello AD FS 서비스 계정이 목록에 있는지 확인 합니다. 존재 하지 않으면 클릭 **사용자 또는 그룹 추가** toohello 목록 추가 하 고 클릭 **확인**합니다.
4. 상승 된 권한으로 명령 프롬프트를 열고 tooenable 감사 및 hello 다음 명령을 실행: ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```합니다.
5. 닫기 **로컬 보안 정책**를 연 다음 hello **AD FS 관리** 스냅인 (서버 관리자에서 도구를 클릭 한 다음 AD FS 관리 선택).
6. Hello 작업 창에서 클릭 **페더레이션 서비스 속성 편집**합니다.
7. Hello 페더레이션 서비스 속성 대화 상자에서 클릭 hello **이벤트** 탭 합니다.
8. 선택 hello **성공 감사 및 실패 감사** 확인란을 선택 하 고 클릭 **확인**합니다.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2016"></a>Windows Server 2016에서 AD FS에 대 한 tooenable 감사
1. 열기 **로컬 보안 정책** 열어 **서버 관리자** hello 시작 화면 또는 hello hello 바탕 화면 작업 표시줄에서 서버 관리자에서 클릭 **도구/로컬 보안 정책**.
2. Toohello 이동 **보안 설정 \ 로컬 정책 \ 사용자 권한 할당** 폴더를 찾아 두 번 클릭 **보안 감사 생성**합니다.
3. Hello에 **로컬 보안 설정** 탭 hello AD FS 서비스 계정이 목록에 있는지 확인 합니다. 존재 하지 않으면 클릭 **사용자 또는 그룹 추가** hello AD FS 서비스 계정 toohello 목록에 추가 하 고 클릭 **확인**합니다.
4. tooenable 감사 상승 된 권한으로 명령 프롬프트를 열고 및 hello 다음 명령을 실행 합니다.<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code>
5. 닫기 **로컬 보안 정책**를 연 다음 hello **AD FS 관리** 스냅인 (서버 관리자에서 도구를 클릭 한 다음 AD FS 관리 선택).
6. Hello 작업 창에서 클릭 **페더레이션 서비스 속성 편집**합니다.
7. Hello 페더레이션 서비스 속성 대화 상자에서 클릭 hello **이벤트** 탭 합니다.
8. 선택 hello **성공 감사 및 실패 감사** 확인란을 선택 하 고 클릭 **확인**합니다. 기본적으로 사용하도록 설정되어 있습니다.
9. PowerShell 창을 열고 다음 명령을 hello를 실행: ```Set-AdfsProperties -AuditLevel Verbose```합니다.

기본적으로 "기본" 감사 수준을 사용하도록 설정되어 있습니다. Hello에 대 한 자세한 [Windows Server 2016에서 AD FS 감사 향상](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)


#### <a name="toolocate-hello-ad-fs-audit-logs"></a>toolocate hello AD FS 감사 로그
1. **이벤트 뷰어**를 엽니다.
2. TooWindows 로그를 이동 하 고 선택 **보안**합니다.
3. 오른쪽 hello, 클릭 **현재 로그 필터링**합니다.
4. 이벤트 소스에서 **AD FS 감사**를 선택합니다.

![AD FS 감사 로그](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> 그룹 정책은 AD FS 감사를 사용하지 않도록 설정할 수 있습니다. AD FS 감사를 사용하지 않도록 설정하면 로그인 활동에 대한 사용 현황 분석을 사용할 수 없습니다. AD FS 감사를 사용하지 않도록 설정하는 그룹 정책이 없는지 확인해야 합니다.
>


## <a name="installing-hello-azure-ad-connect-health-agent-for-sync"></a>동기화 용 hello Azure AD Connect Health agent 설치
동기화 용 hello Azure AD Connect Health agent는 Azure AD Connect의 최신 빌드 hello에에서 자동으로 설치 됩니다. toouse Azure AD Connect 동기화의 toodownload hello 최신 버전의 Azure AD Connect 설치 합니다. Hello 최신 버전을 다운로드할 수 [여기](http://www.microsoft.com/download/details.aspx?id=47594)합니다.

tooverify hello 에이전트 설치가 완료 된 후, 다음 hello 서버의 서비스는 hello를 찾아보십시오. Hello 구성을 완료 실행 이미 합니다. 그렇지 않으면 hello 구성이 완료 될 때까지 중지 합니다.

* Azure AD Connect Health Sync Insights Service
* Azure AD Connect Health Sync Monitoring Service

![동기화에 대한 Azure AD Connect Health 확인](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> Azure AD Connect Health를 사용하려면 Azure AD Premium이 필요합니다. Azure AD Premium이 없으면 hello Azure 포털에에서 없습니다 toocomplete hello 구성 됩니다. 자세한 내용은 참조 hello [요구 사항 페이지](active-directory-aadconnect-health-agent-install.md#requirements)합니다.
>
>

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a>동기화에 대한 Azure AD Connect Health 수동 등록
Hello 동기화 에이전트 등록에 대 한 Azure AD Connect Health에 실패 하면 Azure AD Connect를 성공적으로 설치한 후 다음 PowerShell 명령을 toomanually hello 에이전트를 등록 하는 hello를 사용할 수 있습니다.

> [!IMPORTANT]
> 이 PowerShell 명령을 사용 하는 Azure AD Connect를 설치한 후 hello 에이전트 등록에 실패 하는 경우 필요 합니다.
>
>

hello 다음 PowerShell 명령은 필요만 hello 상태 에이전트 등록에 실패 한 경우 Azure AD Connect의 구성과 성공적으로 설치 된 후에 합니다. hello Azure AD Connect Health 서비스는 hello 에이전트를 성공적으로 등록 한 후 시작 됩니다.

다음 PowerShell 명령을 hello를 사용 하 여 동기화에 대 한 hello Azure AD Connect Health agent를 수동으로 등록할 수 있습니다.

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

hello 명령은 다음 매개 변수를 사용 합니다.

* AttributeFiltering: (기본값)-Azure AD Connect hello 기본 특성 집합을 동기화 하 고 필터링 된 특성을 사용자 지정 된 toouse 되었습니다 $true 설정 합니다. 그렇지 않으면 $false입니다.
* StagingMode: (기본값)-Azure AD Connect 서버 hello hello 서버가 준비 모드, $true에 없는 경우 $false toobe 준비 모드에서 구성 합니다.

사용 해야 인증에 대 한 메시지가 표시 되 면 hello 동일한 전역 관리자 계정 (같은 admin@domain.onmicrosoft.com) Azure AD Connect를 구성 하는 데 사용 하 합니다.

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-ds"></a>Hello AD DS에 대 한 Azure AD Connect Health Agent 설치
toostart hello 에이전트를 설치, 다운로드 한 hello.exe 파일을 두 번 클릭 합니다. Hello 첫 번째 화면에서 설치를 클릭 합니다.

![Azure AD Connect Health 확인](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

Hello 설치가 완료 되 면 지금 구성를 클릭 합니다.

![Azure AD Connect Health 확인](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

명령 프롬프트가 실행된 다음 PowerShell에서 Register-AzureADConnectHealthADDSAgent가 실행됩니다. 입력 정보 요청된 toosign tooAzure에서 계속 진행 하는 경우에 로그인 합니다.

![Azure AD Connect Health 확인](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

로그인한 후 PowerShell이 계속됩니다. 완료 되 면 PowerShell을 닫을 수 있습니다 및 hello 구성이 완료 되었습니다.

이 시점에서 hello 서비스는 hello 에이전트 toomonitor 수 있도록 자동으로 시작 해야 하 고 데이터를 수집 합니다. Hello 이전 섹션에 설명 된 모든 hello 필수 조건을 충족 하지 않은 경우 경고 hello PowerShell 창에 나타납니다. 수 있는지 toocomplete hello [요구 사항](active-directory-aadconnect-health-agent-install.md#requirements) hello 에이전트를 설치 하기 전에. hello 스크린 샷 다음은 이러한 오류의 예입니다.

![AD DS용 Azure AD Connect Health 확인](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

tooverify hello 에이전트 설치가 완료 된 후, 다음 hello 도메인 컨트롤러에서 서비스는 hello를 찾아보십시오.

* Azure AD Connect Health AD DS Insights 서비스
* Azure AD Connect Health AD DS 모니터링 서비스

Hello 구성을 완료 하는 경우 이러한 서비스를 이미 실행 되어야 합니다. 그렇지 않으면 hello 구성이 완료 될 때까지 중지 합니다.

![Azure AD Connect Health 확인](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)


### <a name="agent-registration-using-powershell"></a>PowerShell을 사용한 에이전트 등록
Hello 적절 한 에이전트 setup.exe를 설치한 후 다음 PowerShell 명령을 hello 역할에 따라 hello를 사용 하 여 hello 에이전트 등록 단계를 수행할 수 있습니다. PowerShell 창을 열고 hello 적절 한 명령을 실행 합니다.

```
    Register-AzureADConnectHealthADFSAgent
    Register-AzureADConnectHealthADDSAgent
    Register-AzureADConnectHealthSyncAgent

```

이 명령은 변수로 사용할 수 "Credential" 매개 변수 toocomplete hello 등록을 사용 하는 비 대화형 방식으로 또는 Server Core 컴퓨터.
* hello 자격 증명을 매개 변수로 전달 되는 PowerShell 변수에서 캡처할 수 있습니다.
* 액세스 tooregister hello 에이전트 고 MFA를 사용할 수 없는 모든 Azure AD Id를 제공할 수 있습니다.
* 기본적으로 전역 관리자에 대 한 액세스 권한이 tooperform 에이전트 등록 합니다. 허용할 수 있습니다 다른 권한 있는 id tooperform 덜이 단계입니다. [역할 기반 액세스 제어](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)에 대해 자세히 알아보세요.

```
    $cred = Get-Credential
    Register-AzureADConnectHealthADFSAgent -Credential $cred

```

## <a name="configure-azure-ad-connect-health-agents-toouse-http-proxy"></a>Azure AD Connect Health Agent toouse HTTP 프록시를 구성 합니다.
Azure AD Connect Health Agent toowork HTTP 프록시를 구성할 수 있습니다.

> [!NOTE]
> * "Netsh WinHttp ProxyServerAddress를 설정 하는 데 사용"을 사용 하 여 hello 에이전트가 Microsoft Windows HTTP Services 대신 System.Net toomake 웹 요청을 사용 하는 대로 지원 되지 않습니다.
> * hello 구성 된 Http 프록시 주소는 사용 되는 toopass 통해 암호화 된 Https 메시지입니다.
> * 인증된 프록시(HTTPBasic 사용)는 지원되지 않습니다.
>
>

### <a name="change-health-agent-proxy-configuration"></a>Health Agent 프록시 구성 변경
Hello 옵션 tooconfigure Azure AD Connect Health Agent toouse HTTP 프록시를 수행 해야 합니다.

> [!NOTE]
> 모든 Azure AD Connect Health Agent 서비스를 다시 시작 해야, hello 프록시 설정 toobe 업데이트에 대 한 순서입니다. Hello 다음 명령을 실행 합니다.<br>
> Restart-Service AdHealth*
>
>

#### <a name="import-existing-proxy-settings"></a>기존 프록시 설정 가져오기
##### <a name="import-from-internet-explorer"></a>Internet Explorer에서 가져오기
Internet Explorer HTTP 프록시 설정을 가져올 수 있습니다, 그리고 Azure AD Connect Health Agent hello에서 toobe 사용 합니다. 각 hello Health agent를 실행 하는 hello 서버 hello 다음 PowerShell 명령을 실행 합니다.

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a>WinHTTP에서 가져오기
WinHTTP 프록시 설정을 가져올 수 있습니다, 그리고 Azure AD Connect Health Agent hello에서 toobe 사용 합니다. 각 hello Health agent를 실행 하는 hello 서버 hello 다음 PowerShell 명령을 실행 합니다.

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a>수동으로 프록시 주소 지정
각 hello 다음 PowerShell 명령을 실행 하 여 hello Health Agent를 실행 하는 hello 서버에서 프록시 서버를 수동으로 지정할 수 있습니다.

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

예: *Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress myproxyserver: 443*

* "address"는 DNS 확인 가능 서버 이름 또는 IPv4 주소일 수 있습니다.
* "port"는 생략할 수 있습니다. 생략하면 443이 기본 포트로 선택됩니다.

#### <a name="clear-existing-proxy-configuration"></a>기존 프록시 구성 지우기
Hello 다음 명령을 실행 하 여 hello 기존 프록시 구성을 지울 수 있습니다.

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a>현재 프록시 설정 읽기
다음과 같은 hello 다음 명령을 실행 하 여 hello 현재 구성 된 프록시 설정을 읽을 수 있습니다.

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-tooazure-ad-connect-health-service"></a>테스트 연결 tooAzure AD Connect Health Service
있기 hello Azure AD Connect Health 서비스와 Azure AD Connect Health agent hello toolose 연결을 발생 시키는 문제가 발생할 수 있습니다. 여기에는 네트워크 문제, 권한 문제 또는 기타 다양한 이유가 포함됩니다.

Hello 에이전트는 2 시간 보다 오랫동안 없습니다 toosend 데이터 toohello Azure AD Connect Health 서비스,이 경우 hello 포털에서 경고를 수행 하는 hello로 표시 됩니다: "상태 관리 서비스 데이터 없는 경우 toodate를" Hello 다음 PowerShell 명령을 실행 하 여 영향을 받는 hello Azure AD Connect Health agent 수 tooupload 데이터 toohello Azure AD Connect Health 서비스 인지 확인할 수 있습니다.

    Test-AzureADConnectHealthConnectivity -Role ADFS

hello 역할 매개 변수는 현재 다음 값에는 hello를 사용 합니다.

* ADFS
* 동기화
* ADDS

Hello-ShowResults 플래그를 사용 하 여 hello 명령 tooview에서 로그를 자세히 설명 합니다. 다음 예제는 hello를 사용 합니다.

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> toouse hello 연결 도구를 첫 번째 전체 hello 에이전트 등록을 해야합니다. 에이전트 등록을 hello toocomplete 수 없는 경우 모든 hello가 충족 되는지 확인 [요구 사항](active-directory-aadconnect-health-agent-install.md#requirements) Azure AD Connect Health에 대 한 합니다. 이 연결 테스트는 에이전트를 등록하는 동안 기본적으로 수행됩니다.
>
>

## <a name="related-links"></a>관련 링크
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health 작업](active-directory-aadconnect-health-operations.md)
* [AD FS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adfs.md)
* [동기화에 대한 Azure AD Connect Health 사용](active-directory-aadconnect-health-sync.md)
* [AD DS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health FAQ](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health 버전 내역](active-directory-aadconnect-health-version-history.md)
