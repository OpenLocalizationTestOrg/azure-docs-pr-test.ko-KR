---
title: "Azure Active Directory 장치 등록을 사용 하 여 온-프레미스 조건부 액세스를 aaaSetting | Microsoft Docs"
description: "단계별 가이드 tooenabling 조건부 액세스 tooon 온-프레미스 응용 프로그램 Windows Server 2012 r 2에서 Active Directory Federation Services (AD FS)을 사용 하 여 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6ae9df8b-31fe-4d72-9181-cf50cfebbf05
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 808e3b96873102aebae667153f588dcdb205e884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-on-premises-conditional-access-by-using-azure-active-directory-device-registration"></a>Azure Active Directory 장치 등록을 사용하여 온-프레미스 조건부 액세스 설정
사용자가 tooworkplace 조인 자신의 개인 장치 toohello Azure Active Directory (Azure AD) 장치 등록 서비스를 필요로 하는 경우 알려진된 tooyour 조직으로 자신의 장치를 표시할 수 있습니다. 다음은 Windows Server 2012 r 2에서 Active Directory Federation Services (AD FS)을 사용 하 여 조건부 액세스 tooon 온-프레미스 응용 프로그램을 사용 하기 위한 단계별 가이드는입니다.

> [!NOTE]
> Azure Active Directory 장치 등록 서비스 조건부 액세스 정책에 등록된 장치를 사용하는 경우 Office 365 라이선스 또는 Azure AD Premium 라이선스가 필요합니다. 여기에는 온-프레미스 리소스에서 AD FS에 의해 적용되는 정책이 포함됩니다.
> 
> 온-프레미스 리소스에 대 한 조건부 액세스 시나리오 hello에 대 한 자세한 내용은 참조 [SSO 및 원활한 두 번째 단계 인증을 위해 모든 장치에서 tooworkplace를 회사 응용 프로그램 전반](https://technet.microsoft.com/library/dn280945.aspx)합니다.

이러한 기능은 Azure Active Directory Premium 라이선스를 구매 하는 사용 가능한 toocustomers에 설명 합니다.

## <a name="supported-devices"></a>지원되는 장치
* Windows 7 도메인 가입 장치
* Windows 8.1 개인 및 도메인 가입 장치
* iOS 6 이상 hello Safari 브라우저에 대 한
* Android 4.0 이상, 삼성 GS3 이상 휴대폰, 삼성 갤럭시 노트 2 이상 태블릿

## <a name="scenario-prerequisites"></a>시나리오 필수 조건
* 구독 tooOffice 365 또는 Azure Active Directory Premium
* Azure Active Directory 테넌트
* Windows Server Active Directory(Windows Server 2008 이상)
* Windows Server 2012 R2에서 업데이트된 스키마
* Azure Active Directory Premium에 대한 라이선스
* Windows Server 2012 R2 Federation Services를 SSO tooAzure AD에 대 한 구성
* Windows Server 2012 R2 웹 응용 프로그램 프록시 
* Azure AD Connect(Microsoft Azure Active Directory Connect)[(Azure AD Connect 다운로드)](http://www.microsoft.com/en-us/download/details.aspx?id=47594)
* 확인된 도메인

## <a name="known-issues-in-this-release"></a>이 릴리스의 알려진 문제
* 장치 기반 조건부 액세스 정책에는 장치 개체 쓰기 저장 tooActive Azure Active Directory에서 디렉터리를 요구합니다. 장치 개체 toobe tooActive 디렉터리에 다시 기록에 대 한 toothree 시간이 걸릴 수 있습니다.
* iOS 7 장치는 항상 클라이언트 인증서 인증 하는 동안 hello 사용자 tooselect 인증서를 확인 합니다.
* iOS 8.3 이전의 iOS 8 버전 중 일부는 작동하지 않습니다.

## <a name="scenario-assumptions"></a>시나리오의 가정
이 시나리오에서는 Azure AD 테넌트와 온-프레미스 Active Directory로 구성된 하이브리드 환경이 있다고 가정합니다. 이러한 테넌트는 Azure AD Connect, 확인된 도메인 및 SSO용 AD FS를 사용하여 연결되어야 합니다. 다음 검사 목록 toohelp toohello 요구 사항에 따라 환경을 구성 하는 hello를 사용 합니다.

## <a name="checklist-prerequisites-for-conditional-access-scenario"></a>검사 목록: 조건부 액세스 시나리오를 위한 필수 조건
Azure AD 테넌트를 온-프레미스 Active Directory 인스턴스와 연결합니다.

## <a name="configure-azure-active-directory-device-registration-service"></a>Azure Active Directory 장치 등록 서비스 구성
이 가이드 toodeploy 사용 하 고 조직에 대 한 hello Azure Active Directory 장치 등록 서비스를 구성 합니다.

이 가이드에서는 Windows Server Active Directory를 구성 했으면 tooMicrosoft Azure Active Directory 구독을 가정 합니다. 앞에서 설명한 hello 필수 구성 요소를 참조 하십시오.

toodeploy hello Azure Active Directory와 Azure Active Directory 장치 등록 서비스 테 넌 트, hello 순서 대로 검사 목록 다음의 전체 hello 작업. 참조 링크가 개념 항목 tooa, 경우 반환 toothis 검사 목록 이후에 hello 남은 작업을 진행할 수 있도록 합니다. 일부 작업 hello 단계 완료 되었는지 여부를 확인 하는 데 도움이 되는 시나리오 유효성 검사 단계를 포함 합니다.

## <a name="part-1-enable-azure-active-directory-device-registration"></a>1부: Azure Active Directory 장치 등록 사용
Hello 검사 목록 tooenable의 hello 단계를 수행 하 고 hello Azure Active Directory 장치 등록 서비스를 구성 합니다.

| 작업 | 참조 | 
| --- | --- |
| Azure Active Directory 테 넌 트 tooallow 장치 toojoin hello 회사에서 장치 등록을 사용 합니다. 기본적으로 Azure Multi-factor Authentication hello 서비스에 대 한 사용 되지 않습니다. 그러나 장치를 등록할 때는 Multi-Factor Authentication을 사용하는 것이 좋습니다. Active Directory 등록 서비스에서 Multi-Factor Authentication을 사용하도록 설정하기 전에 먼저 AD FS가 Multi-Factor Authentication 공급자에 대해 구성되어 있는지 확인합니다. |[Azure Active Directory 장치 등록 사용](active-directory-device-registration-get-started.md)| 
|장치에서 잘 알려진 DNS 레코드를 찾아 Azure Active Directory 장치 등록 서비스를 검색합니다. 장치에서 Azure Active Directory 장치 등록 서비스를 검색할 수 있도록 회사 DNS를 구성합니다. |[Azure Active Directory 장치 등록 검색 구성](active-directory-device-registration-get-started.md)| 


## <a name="part-2-deploy-and-configure-windows-server-2012-r2-active-directory-federation-services-and-set-up-a-federation-relationship-with-azure-ad"></a>2부: Windows Server 2012 R2 Active Directory Federation Services를 배포 및 구성하고 Azure AD와의 페더레이션 관계를 설정합니다.

| 작업 | 참조 |
| --- | --- |
| Hello Windows Server 2012 R2 스키마 확장으로 Active Directory 도메인 서비스를 배포 합니다. 않아도 tooupgrade 도메인 컨트롤러 tooWindows Server 2012 r 2 중 하나입니다. hello 스키마 업그레이드는 hello 유일한 요구 사항은입니다. |[Active Directory Domain Services 스키마 업그레이드](#upgrade-your-active-directory-domain-services-schema) |
| 장치에서 잘 알려진 DNS 레코드를 찾아 Azure Active Directory 장치 등록 서비스를 검색합니다. 장치에서 Azure Active Directory 장치 등록 서비스를 검색할 수 있도록 회사 DNS를 구성합니다. |[Active Directory 지원 장치 준비](#prepare-your-active-directory-to-support-devices) |

## <a name="part-3-enable-device-writeback-in-azure-ad"></a>3부: Azure AD에서 장치 쓰기 저장 사용
| 작업 | 참조 |
| --- | --- |
| "Azure AD Connect에서 장치 쓰기 저장 사용"의 2부를 완료합니다. 완료 한 후, toothis 가이드를 반환 합니다. |[Azure AD Connect에서 장치 쓰기 저장 사용](#upgrade-your-active-directory-domain-services-schema) |

## <a name="optional-part-4-enable-multi-factor-authentication"></a>[선택 사항] 4부: Multi-Factor Authentication 사용
구성한 hello 중 Multi-factor Authentication에 대 한 몇 가지 옵션 하는 것이 좋습니다. Multi-factor Authentication toorequire 참조 [hello Multi-factor Authentication 보안 솔루션을 선택](../multi-factor-authentication/multi-factor-authentication-get-started.md)합니다. 각 솔루션에 대 한 설명을 포함 하며 toohelp 선택한 hello 솔루션을 구성을 연결 합니다.

## <a name="part-5-verification"></a>5부: 확인
hello 배포 완료, 되며 몇 가지 시나리오를 체험할 수 있습니다. 다음 tooexperiment hello 서비스와 연결 하 고 해당 기능에 익숙해지면 hello를 사용 합니다.

| 작업 | 참조 |
| --- | --- |
| Azure Active Directory 장치 등록 서비스를 사용 하 여 일부 장치 tooyour 작업 공간을 가입 합니다. iOS, Windows 및 Android 장치를 연결할 수 있습니다. |[Azure Active Directory 장치 등록 서비스를 사용 하 여 장치 tooyour 작업 공간 가입](#join-devices-to-your-workplace-using-azure-active-directory-device-registration) |
| 보고를 사용 하도록 설정 하거나 hello 관리자 포털을 사용 하 여 등록 된 장치를 사용 하지 않도록 설정 합니다. 이 태스크에서는 hello 관리자 포털을 사용 하 여 일부 등록 된 장치를 확인 합니다. |[Azure Active Directory 장치 등록 서비스 개요](active-directory-device-registration-get-started.md) |
| 장치 개체가 Azure Active Directory tooWindows Active Directory 서버에서에서 다시 기록 되며 확인 합니다. |[등록 된 장치 쓰기 저장 tooActive 디렉터리를 확인 하십시오.](#verify-registered-devices-are-written-back-to-active-directory) |
| 이제 사용자가 장치를 등록할 수 있으므로 등록된 장치만 허용하도록 AD FS에서 응용 프로그램 액세스 정책을 만들 수 있습니다. 이 작업에서는 응용 프로그램 액세스 규칙과 사용자 지정 액세스 거부 메시지를 만듭니다. |[응용 프로그램 액세스 정책 및 사용자 지정 액세스 거부 메시지 만들기](#create-an-application-access-policy-and-custom-access-denied-message) |

## <a name="integrate-azure-active-directory-with-on-premises-active-directory"></a>온-프레미스 Active Directory와 Azure Active Directory 통합
이 단계에서는 Azure AD Connect를 사용하여 Azure AD 테넌트와 온-프레미스 Active Directory를 통합할 수 있습니다. Hello 단계 hello Azure 클래식 포털에서에서 사용할 수 있지만이 섹션에 나열 된 특별 지침 메모를 확인 합니다.

1. Azure AD에 있는 전역 관리자 계정을 사용 하 여 Azure 클래식 포털 toohello에 로그인 합니다.
2. Hello 왼쪽된 창에서 선택 **Active Directory**합니다.
3. Hello에 **디렉터리** 탭에서 디렉터리를 선택 합니다.
4. 선택 hello **디렉터리 통합** 탭 합니다.
5. Hello에서 **배포 및 관리** 섹션 1-3 toointegrate 온-프레미스 디렉터리와 Azure Active Directory 단계를 수행 하십시오.
   
   1. 도메인을 추가합니다.
   2. 설치 하 고 hello 지침을 사용 하 여 Azure AD Connect를 실행 [Azure AD Connect의 사용자 지정 설치](connect/active-directory-aadconnect-get-started-custom.md)합니다.
   3. 디렉터리 동기화를 확인하고 관리합니다. 이 단계에는 SSO(Single Sign-On) 지침이 포함되어 있습니다.
   
   또한 [Azure AD Connect의 사용자 지정 설치](connect/active-directory-aadconnect-get-started-custom.md)에서 설명한 대로 AD FS를 사용하여 페더레이션을 구성합니다.

## <a name="upgrade-your-active-directory-domain-services-schema"></a>Active Directory 도메인 서비스 스키마 업그레이드
> [!NOTE]
> Active Directory 스키마를 업그레이드 한 후에 hello 프로세스를 취소할 수 없습니다. 테스트 환경에서 hello 업그레이드를 먼저 수행 하는 것이 좋습니다.
> 

1. 엔터프라이즈 관리자와 스키마 관리자 권한이 모두 있는 계정으로 tooyour 도메인 컨트롤러에 로그인 합니다.
2. 복사 hello **[media] \support\adprep** Active Directory 도메인 컨트롤러의 디렉터리와 하위 tooone (여기서 **[미디어]** hello 경로 toohello Windows Server 2012 R2 설치 미디어 ).
4. 명령 프롬프트에서 이동 toohello **adprep** 디렉터리 및 실행 **adprep.exe /forestprep**합니다. Hello 화면에 나타나는 지침 toocomplete hello 스키마 업그레이드를 수행 합니다.

## <a name="prepare-your-active-directory-toosupport-devices"></a>Active Directory toosupport 장치 준비
> [!NOTE]
> 이 한 번 실행 해야 하는지 tooprepare Active Directory 포리스트 toosupport 장치입니다. toocomplete이이 절차에서는 엔터프라이즈 관리자 권한을 사용 하 여 서명 해야 하 고 Active Directory 포리스트 hello Windows Server 2012 R2 스키마가 있어야 합니다.
> 


### <a name="prepare-your-active-directory-forest"></a>Active Directory 포리스트 준비
1. 페더레이션 서버에서 Windows PowerShell 명령 창을 열고 **Initialize-ADDeviceRegistration**을 입력합니다. 
2. 에 대 한 메시지가 표시 되 면 **ServiceAccountName**, AD FS에 대 한 hello 서비스 계정으로 선택한 hello 서비스 계정의 hello 이름을 입력 합니다. GMSA 계정인 경우 계정을 입력 하십시오 hello hello **domain\accountname$** 형식입니다. 도메인 계정에 대 한 hello 형식을 사용 하 여 **domain\accountname**합니다.

### <a name="enable-device-authentication-in-ad-fs"></a>AD FS에서 장치 인증 사용
1. 페더레이션 서버에서 hello AD FS 관리 콘솔을 열고 너무 이동**AD FS** > **인증 정책**합니다.
2. Hello에 **동작** 창 선택 **전역 기본 인증 편집**합니다.
3. **장치 인증 사용**을 선택한 다음 **확인**을 선택합니다.
4. 기본적으로 AD FS는 Active Directory에서 사용하지 않은 장치를 정기적으로 제거합니다. Azure에서 장치를 관리할 수 있도록 Azure Active Directory 장치 등록 서비스를 사용하는 경우 이 작업을 비활성화합니다.

### <a name="disable-unused-device-cleanup"></a>사용하지 않은 장치 정리 사용 안 함
페더레이션 서버에서 Windows PowerShell 명령 창을 연 다음 **Set-AdfsDeviceRegistration -MaximumInactiveDays 0**을 입력합니다.

### <a name="prepare-azure-ad-connect-for-device-writeback"></a>장치 쓰기 저장을 위해 Azure AD Connect 준비
'1부 Azure AD Connect 준비'를 완료합니다.

## <a name="join-devices-tooyour-workplace-by-using-azure-active-directory-device-registration-service"></a>Azure Active Directory 장치 등록 서비스를 사용 하 여 장치 tooyour 작업 공간 가입

### <a name="join-an-ios-device-by-using-azure-active-directory-device-registration"></a>Azure Active Directory 장치 등록을 사용하여 iOS 장치 연결
Hello Over-the-Air 프로필 등록 프로세스를 사용 하 여 iOS 장치에 대 한 azure Active Directory 장치 등록 합니다. 이 프로세스는 hello 사용자가 Safari를 사용 하 여 toohello 프로필 등록 URL을 시작 합니다. hello URL 형식은 다음과 같습니다.

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/"yourdomainname"

이 경우 `yourdomainname` hello 도메인 이름이 Azure Active Directory로 구성 합니다. 예를 들어 도메인 이름이 contoso.com 인 경우 hello URL은 다음과 같습니다.

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com

이 URL tooyour 사용자가 여러 가지 방법으로 toocommunicate. 예를 들어 AD FS의 사용자 지정 응용 프로그램 액세스 거부 메시지에 이 URL을 게시하는 것이 좋습니다. Hello 이후 섹션에서는이 정보를 다룹니다 [프로그램 응용 프로그램 액세스 정책 및 사용자 지정 액세스 거부 메시지 만들기](#create-an-application-access-policy-and-custom-access-denied-message)합니다.

### <a name="join-a-windows-81-device-by-using-azure-active-directory-device-registration"></a>Azure Active Directory 장치 등록을 사용하여 Windows 8.1 장치 연결
1. Windows 8.1 장치에서 **PC 설정** > **네트워크** > **작업 공간**을 차례로 선택합니다.
2. 사용자 이름을 UPN 형식(예: **dan@contoso.com**)으로 입력합니다.
3. **연결**을 선택합니다.
4. 메시지가 표시되면 자격 증명으로 로그인합니다. hello 장치가 연결 됩니다.

### <a name="join-a-windows-7-device-by-using-azure-active-directory-device-registration"></a>Azure Active Directory 장치 등록을 사용하여 Windows 7 장치 연결
tooregister Windows 7 도메인 가입 장치 toodeploy hello 장치 등록 소프트웨어 패키지를 해야합니다. hello 소프트웨어 패키지 라고 작업 공간 연결에 대 한 Windows 7 및의 사용 가능한 hello에서 다운로드할 [Microsoft Connect 웹 사이트](https://connect.microsoft.com/site1164)합니다. 

사용할 수 있는 방법을 toouse hello 패키지에 대 한 지침은 [어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 Azure Active Directory를 사용 하 여 장치](active-directory-conditional-access-automatic-device-registration-setup.md)합니다.

## <a name="verify-that-registered-devices-are-written-back-tooactive-directory"></a>등록 된 장치 쓰기 저장 tooActive 디렉터리를 확인 하십시오.
볼 수 있으며 있는지 장치 개체 쓰기 저장 된 Active Directory tooyour LDP.exe 및 ADSI 편집을 사용 하 여 확인 하십시오. 두 가지 hello Active Directory 관리자 도구와 함께 사용할 수 있습니다.

기본적으로 Azure Active Directory에서 쓰기 저장 되는 장치 개체에에서 배치 됩니다 hello 동일한 AD FS 팜과 도메인입니다.

    CN=RegisteredDevices,defaultNamingContext

## <a name="create-an-application-access-policy-and-custom-access-denied-message"></a>응용 프로그램 액세스 정책 및 사용자 지정 액세스 거부 메시지 만들기
Hello 시나리오를 따르는 것이 좋습니다: 응용 프로그램 AD FS에서 신뢰 당사자 트러스트를 만들고 등록 된 장치만 허용 하는 발급 권한 부여 규칙을 구성 합니다. 이제 등록 된 장치만 tooaccess hello 응용 프로그램을 수 있습니다. 

toomake 방법에 대 한 지침을 포함 하는 사용자 지정 액세스 거부 메시지를 구성할 사용자 toogain access toohello 응용 프로그램을 쉽게 것 toojoin 장치입니다. 이제 사용자가 없으므로 자연스럽 게 tooregister 장치 응용 프로그램에 액세스할 수 있습니다.

hello 다음 단계 방법을 보여 줍니다 tooimplement이이 시나리오입니다.

> [!NOTE]
> 이 섹션에서는 AD FS에서 응용 프로그램에 대한 신뢰 당사자 트러스트를 이미 구성했다고 가정합니다.
> 

1. Hello AD FS MMC 도구를 열고 다음 선택 **AD FS** > **트러스트 관계** > **신뢰 당사자 트러스트**합니다.
2. 이 새 액세스 규칙이 적용 되는 hello 응용 프로그램 toowhich를 찾습니다. Hello 응용 프로그램을 마우스 오른쪽 단추로 클릭 한 다음 선택 **클레임 규칙 편집**합니다.
3. 선택 hello **발급 권한 부여 규칙** 탭을 선택한 다음 선택 **규칙 추가**합니다.
4. Hello에서 **클레임 규칙** 서식 파일 드롭 다운 목록에서 **거부 들어오는 클레임에 따라 사용자 허용 또는**합니다. 그런 후 **다음**을 선택합니다.
5. Hello에 **클레임 규칙 이름** 필드를 입력 **등록 된 장치에서 액세스를 허용**합니다.
6. Hello에서 **들어오는 클레임 유형** 드롭 다운 목록 **등록 된 사용자**합니다.
7. Hello에 **들어오는 클레임 값** 필드를 입력 **true**합니다.
8. 선택 hello **이 들어오는 클레임으로 허용 액세스 toousers** 라디오 단추입니다.
9. **마침**을 선택한 다음 **적용**을 선택합니다.
10. 만든 hello 규칙 보다 허용 범위가 넓은 모든 규칙을 제거 합니다. 예를 들어 hello 기본 규칙을 제거 **사용자 액세스 허용 tooall**합니다.

응용 프로그램에 이제 구성 된 tooallow hello 사용자는 등록 하 고 toohello 작업 공간 가입 된 장치에서 제공 하는 경우에 액세스입니다. 자세한 고급 액세스 정책은 [추가 Multi-Factor Authentication을 통해 중요한 응용 프로그램에 대한 위험 관리](https://technet.microsoft.com/library/dn280949.aspx)를 참조하세요.

다음으로 응용 프로그램에 대한 사용자 지정 오류 메시지를 구성합니다. hello 오류 메시지에는 사용자가 hello 응용 프로그램에 액세스 하기 전에 해당 장치 toohello 작업 공간에 연결 해야 알려 줍니다. 사용자 지정 HTML 및 PowerShell을 사용하여 사용자 지정 응용 프로그램 액세스 거부 메시지를 만들 수 있습니다.

페더레이션 서버에서 PowerShell 명령 창을 열고 hello 다음 명령을 입력 합니다. 특정 tooyour 시스템 항목과 hello 명령의 일부를 바꿉니다.

    Set-AdfsRelyingPartyWebContent -Name "relying party trust name" -ErrorPageAuthorizationErrorMessage
이 응용 프로그램에 액세스하려면 먼저 장치를 등록해야 합니다.

**IOS 장치를 사용 하는 경우이 링크 toojoin 장치를 선택**:

    a href='https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/yourdomain.com

이 iOS 장치 tooyour 작업 공간을 가입 시킵니다.

Windows 8.1 장치를 사용하는 경우 **PC 설정**> **네트워크** > **작업 공간**을 차례로 선택하여 장치를 연결할 수 있습니다.

Hello 명령 앞에 **신뢰 당사자 트러스트 이름** hello AD FS에서 응용 프로그램의 신뢰 당사자 트러스트 개체 이름입니다.
및 **yourdomain.com** Azure Active Directory (예: contoso.com)에 구성 된 hello 도메인 이름입니다.
모든 줄 바꿈 (있는 경우) hello HTML에서에서 toohello 전달 하는 콘텐츠 있는지 tooremove 수 **Set-adfsrelyingpartywebcontent** cmdlet.

이제 사용자가 Azure Active Directory 장치 등록 서비스 hello로 등록 되지 않은 장치에서 응용 프로그램에 액세스, 유사한 toohello 스크린 샷 다음 페이지가 표시 됩니다.

![사용자가 자신의 장치를 Azure AD에 등록하지 않은 경우의 오류 스크린샷](./media/active-directory-conditional-access/error-azureDRS-device-not-registered.gif)


