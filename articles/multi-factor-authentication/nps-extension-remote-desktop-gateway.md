---
title: "Azure MFA NPS 확장명이 데스크톱 게이트웨이 통합 aaaRemote | Microsoft Docs"
description: "이 문서에서는 Microsoft Azure에 대 한 hello 서버 NPS (네트워크 정책) 확장을 사용 하는 Azure MFA를 원격 데스크톱 게이트웨이 인프라 통합 설명 합니다."
services: active-directory
keywords: "Azure MFA, 원격 데스크톱 게이트웨이 통합, Azure Active Directory, 네트워크 정책 서버 확장"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: ae5f6864416582bd82b787005ca787988d23a813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#  <a name="integrate-your-remote-desktop-gateway-infrastructure-using-hello-network-policy-server-nps-extension-and-azure-ad"></a>Hello 정책 서버 NPS (네트워크) 확장 및 Azure AD를 사용 하 여 원격 데스크톱 게이트웨이 인프라 통합

이 문서에서는 Microsoft Azure에 대 한 hello 서버 NPS (네트워크 정책) 확장을 사용 하 여 원격 데스크톱 게이트웨이 인프라와 Azure Multi-factor Authentication (MFA)을 통합 하기 위한 세부 정보. 

Azure를 사용 하 여 고객 toosafeguard 인증 전화 접속 사용자 RADIUS (Remote Service) 클라이언트 인증의 클라우드 기반 Azure에 대 한 서비스 NPS (네트워크 정책) 확장 hello 허용 [Multi-factor Authentication (MFA)](multi-factor-authentication.md)합니다. 이 솔루션은 두 번째 계층을 보안 toouser 로그인 및 트랜잭션에 추가 하는 데 2 단계 인증을 제공 합니다.

이 문서에서는 hello NPS 확장을 사용 하 여 Azure에 대 한 hello NPS 인프라 Azure MFA를 통합 하기 위한 단계별 지침을 제공 합니다. 이렇게 하면 원격 데스크톱 게이트웨이 tooa에 toolog 시도 하는 사용자에 대 한 보안을 확인 합니다. 

hello 네트워크 정책 및 액세스 서비스 (NPS)에서는 조직이 기능 toodo hello 다음 hello:
* 연결할 수 있는 사용자 지정 하 여 hello 관리 및 제어의 네트워크 요청에 대 한 중앙 위치를 정의 연결이 허용 되는지 하루 중 어떤 시간 hello 연결, 기간 및 hello 수준의 보안 클라이언트 tooconnect를 사용 하 고 등 해야 합니다. 이러한 정책은 각 VPN 또는 RD(원격 데스크톱) 게이트웨이 서버에 지정하는 대신 중앙 위치에 한 번만 지정하면 됩니다. RADIUS 프로토콜과 hello hello 중앙 집중식 인증, 권한 부여 및 계정 AAA ()를 제공 합니다. 
* 설정 및 장치 toonetwork 리소스 제한 또는 무제한 액세스를 부여 된 있는지 여부를 결정 하는 네트워크 액세스 보호 (NAP) 클라이언트 상태 정책을 적용 합니다.
* 액세스 too802.1x 지원 무선 액세스 지점 및 이더넷 스위치에 대 한 의미 tooenforce 인증 및 권한 부여를 제공 합니다.    

일반적으로 조직 toosimplify NPS RADIUS ()를 사용 하 고 VPN의 hello 관리를 중앙 집중화 정책이 적용 됩니다. 그러나 대부분의 조직에서는 또한 toosimplify NPS를 사용 하 여 고 RD 데스크톱 연결 권한 부여 정책 RD Cap ()의 hello 관리를 중앙 집중화 합니다. 

조직에서는 Azure MFA tooenhance 보안 NPS 통합할 수 있고 높은 호환성 수준을 제공 합니다. 이렇게 하면 사용자가 원격 데스크톱 게이트웨이 toohello에 2 단계 확인 toolog를 설정 합니다. 에 대 한 액세스 권한이 부여 되는 사용자가 toobe, 해당 컨트롤에 자신의 사용자 이름/암호 조합이 hello 사용자 정보로는 제공 해야 합니다. 이 정보는 신뢰할 수 있어야 하며, 휴대폰 번호, 유선 전화 번호, 모바일 장치 등과 같이 쉽게 복제할 수 없습니다.

Hello Azure에 대 한 NPS 확장의 이전 toohello 가용성, 고객에 대 한 2 단계 인증 tooimplement 입장 통합 NPS 및 Azure MFA 환경 tooconfigure 되었고 hello 온-프레미스 환경에서 별도 MFA 서버를 유지 관리 에 설명 되어 [원격 데스크톱 게이트웨이 및 Azure Multi-factor Authentication 서버 RADIUS를 사용 하 여](multi-factor-authentication-get-started-server-rdg.md)합니다.

이제 Azure 용 hello NPS 확장의 가용성을 hello는 온-프레미스 기반 MFA 솔루션 또는 클라우드 기반 MFA 솔루션 toosecure RADIUS 클라이언트 인증 조직 hello 선택 toodeploy를 제공합니다.

## <a name="authentication-flow"></a>인증 흐름

Toobe 부여는 사용자에 대 한 원격 데스크톱 게이트웨이 통해 toonetwork 리소스에 액세스 한 RD 연결 권한 부여 정책 (RD CAP) 및 하나의 RD 리소스 권한 부여 정책 RD RAP ()에 지정 된 hello 조건을 만족 해야 합니다. RD Cap만 사용자가 권한 있는 tooconnect tooRD 게이트웨이 지정 합니다. RD Rap 원격 데스크톱 또는 원격 앱과 같이 hello 네트워크 리소스를 지정 하면 해당 hello 사용자 수 tooconnect toothrough hello RD 게이트웨이 합니다. 

RD 게이트웨이 구성된 toouse RD Cap 저장소를 중앙 정책 일 수 있습니다. RD Rap hello RD 게이트웨이에서 처리 하면서 중앙 정책을 사용할 수 없습니다. RD 게이트웨이 구성 toouse의 예로 RD Cap에 대 한 중앙 정책 저장소는 hello 중앙 정책 저장소로 사용 하는 RADIUS 클라이언트 tooanother NPS 서버가 있습니다.

Azure에 대 한 NPS 확장 hello와 통합 된 hello NPS 및 원격 데스크톱 게이트웨이 hello 정상적으로 인증 흐름은 다음과 같습니다.

1. hello 원격 데스크톱 게이트웨이 서버는 원격 데스크톱 사용자 tooconnect tooa 같은 리소스에 원격 데스크톱 세션에서 인증 요청을 받습니다. 클라이언트 역할을 하는 RADIUS hello 원격 데스크톱 게이트웨이 서버 hello 요청 tooa RADIUS 액세스 요청 메시지를 변환 하 고 hello NPS 확장이 설치 되어 hello 메시지 toohello RADIUS (NPS) 서버에 보냅니다. 
2. hello 사용자 이름 및 Active Directory에서 암호 조합을 확인 하 고 hello 사용자 인증 됩니다.
3. NPS 연결 요청을 hello 및 hello 네트워크 정책을 충족 조건에 지정 된 대로 hello 모든 경우 (예를 들어 시간이 나 그룹 구성원 자격 제한과), NPS 확장 hello Azure MFA를 보조 인증에 대 한 요청을 트리거합니다. 
4. Azure MFA Azure AD와 통신 하 고, hello 사용자의 세부 정보를 검색, hello 사용자 (문자 메시지, 모바일 앱, 및 등)으로 구성 하는 hello 메서드를 사용 하 여 hello 보조 인증을 수행 합니다. 
5. 검색에 성공 hello MFA 챌린지의 Azure MFA hello 결과 toohello NPS 확장을 통신합니다.
6. hello 확장이 설치 되어 hello NPS 서버 hello RD CAP 정책 toohello 원격 데스크톱 게이트웨이 서버에 대 한 RADIUS 액세스 허용 메시지를 보냅니다.
7. hello 사용자의 액세스 권한 toohello hello RD 게이트웨이 통해 네트워크 리소스를 요청 합니다.

## <a name="prerequisites"></a>필수 조건
이 섹션에는 필수 구성 요소 hello Azure MFA 원격 데스크톱 게이트웨이 hello와 통합 하기 전에 필요한 자세히 설명 합니다. 시작 하기 전에 다음 필수 구성 요소가 충족 하는 hello가 있어야 합니다.  

* RDS(원격 데스크톱 서비스) 인프라
* Azure MFA 라이선스
* Windows Server 소프트웨어
* NPS(네트워크 정책 및 액세스 서비스) 역할
* 온-프레미스 AD와 동기화되는 Azure AD 
* Azure Active Directory GUID ID

### <a name="remote-desktop-services-rds-infrastructure"></a>RDS(원격 데스크톱 서비스) 인프라
작동 중인 RDS(원격 데스크톱 서비스) 인프라가 있어야 합니다. Azure에서이 인프라를 신속 하 게 만들 수 있습니다, 그렇지 않은 경우 사용 하 여 hello 다음 빠른 시작 템플릿: [원격 데스크톱 세션 컬렉션 만들기 배포](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment)합니다. 

원하는 경우 toomanually 하나에 따라 hello 단계 toodeploy 신속 하 게 테스트용으로, 온-프레미스 RDS 인프라를 만듭니다. 
**자세한 정보**: [Azure 빠른 시작으로 RDS 배포](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure) 및 [기본 RDS 인프라 배포](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure) 

### <a name="licenses"></a>라이선스
Azure AD Premium, EMS(Enterprise Mobility plus Security) 또는 MFA 구독을 통해 사용할 수 있는 Azure MFA에 대한 라이선스가 필요합니다. 자세한 내용은 참조 [어떻게 tooget Azure Multi-factor Authentication](multi-factor-authentication-versions-plans.md)합니다. 테스트를 위해 평가판 구독을 사용할 수 있습니다.

### <a name="software"></a>소프트웨어
hello NPS 확장 해야 Windows Server 2008 R2 SP1 이상 hello NPS 역할 서비스가 설치 되어 있는 합니다. Windows Server 2016을 사용 하 여이 섹션의 모든 hello 단계를 수행 했습니다.

### <a name="network-policy-and-access-services-nps-role"></a>NPS(네트워크 정책 및 액세스 서비스) 역할
hello RADIUS 서버 및 클라이언트 기능 뿐만 아니라 네트워크 액세스 정책 상태 관리 서비스 hello NPS 역할 서비스를 제공합니다. 인프라의 두 개 이상의 컴퓨터에이 역할을 설치 해야 합니다: 원격 데스크톱 게이트웨이 및 다른 hello 구성원 서버 또는 도메인 컨트롤러입니다. 기본적으로 hello 역할은 원격 데스크톱 게이트웨이 hello로 구성 하는 hello 컴퓨터에 이미 있습니다.  또한에 설치 해야 hello NPS 역할 이상 도메인 컨트롤러 또는 구성원 서버 등의 다른 컴퓨터에 있습니다.

Hello NPS 역할 설치에 대 한 내용은 Windows Server 2012 또는 이전 서비스, 참조 [NAP 상태 정책 서버 설치](https://technet.microsoft.com/library/dd296890.aspx)합니다. NPS 포함 하 여 hello 권장 tooinstall NPS 도메인 컨트롤러에 대 한 모범 사례에 대 한 설명을 참조 하십시오. [NPS에 대 한 유용한](https://technet.microsoft.com/library/cc771746)합니다.

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>온-프레미스 Active Directory와 동기화되는 Azure Active Directory 
toouse hello NPS 확장 온-프레미스 사용자를 Azure AD와 동기화 하 고 MFA에 대해 사용 하도록 설정 해야 합니다. 이 섹션에서는 온-프레미스 사용자가 AD Connect를 사용하여 Azure AD와 동기화된다고 가정합니다. Azure AD 연결에 대한 자세한 내용은 [Azure Active Directory와 온-프레미스 디렉터리 통합](../active-directory/connect/active-directory-aadconnect.md)을 참조하세요. 

### <a name="azure-active-directory-guid-id"></a>Azure Active Directory GUID ID
NPS tooinstall tooknow hello hello Azure AD의 GUID 필요합니다. Hello hello Azure AD의 GUID 찾기에 대 한 지침 아래에 나와 있습니다.

## <a name="configure-multi-factor-authentication"></a>Multi-Factor Authentication 구성 
이 섹션에서는 원격 데스크톱 게이트웨이 hello로 Azure MFA를 통합 하기 위한 지침을 제공 합니다. 관리자로 서 사용자는 자신의 multi-factor 장치 또는 응용 프로그램에 직접 등록할 수 전에 hello Azure MFA 서비스를 구성 해야 합니다.

Hello 단계에 따라 [hello 클라우드에서 Azure Multi-factor Authentication 시작](multi-factor-authentication-get-started-cloud.md) Azure AD 사용자에 대 한 MFA tooenable 합니다. 

### <a name="configure-accounts-for-two-step-verification"></a>2단계 인증에 대한 계정 구성
계정이 활성화 된 MFA에 로그인 할 수 없습니다 tooresources 적용 hello MFA 정책까지 hello 두 번째 인증 단계 2 단계 인증을 사용 하 여 인증에 대 한 신뢰할 수 있는 장치 toouse를 구성 했습니다.

Hello 단계에 따라 [무엇 Azure Multi-factor Authentication을 의미 합니까 내?](./end-user/multi-factor-authentication-end-user.md) toounderstand 제대로 MFA에 대 한 사용자 계정으로 장치를 구성 하 고 있습니다.

## <a name="install-and-configure-nps-extension"></a>NPS 확장 설치 및 구성
이 섹션에서는 원격 데스크톱 게이트웨이 hello로 클라이언트 인증을 위해 RDS 인프라 toouse Azure MFA를 구성 하기 위한 지침을 제공 합니다.

### <a name="acquire-azure-active-directory-guid-id"></a>Azure Active Directory GUID ID 얻기

Hello NPS 확장의 hello 구성의 일환으로, Azure AD 테 넌 트에 대 한 toosupply 관리자 자격 증명와 hello Azure AD ID가 필요 있습니다. 단계를 수행 하는 hello 알려주는 tooget hello 테 넌 트 id입니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 테 넌 트 hello Azure의 hello 전역 관리자로 합니다.
2. 왼쪽 탐색 hello, 선택 hello **Azure Active Directory** 아이콘입니다.
3. **속성**을 선택합니다.
4. Hello 디렉터리 ID 옆에 있는 hello 속성 블레이드 클릭 hello **복사** toocopy hello ID tooclipboard 아래와 같이 아이콘을 합니다.

 ![properties](./media/nps-extension-remote-desktop-gateway/image1.png)

### <a name="install-hello-nps-extension"></a>Hello NPS 확장 설치
Hello NPS 확장 hello 네트워크 정책 및 액세스 서비스 (NPS) 역할이 설치 되어 있는 서버에 설치 합니다. 이 설계에 대 한 hello RADIUS 서버로 작동합니다. 

>[!Important]
> 원격 데스크톱 게이트웨이 서버의 hello NPS 확장을 설치 하지 않으면 확인 해야 합니다.
> 

1. Hello 다운로드 [NPS 확장](https://aka.ms/npsmfa)합니다. 
2. Hello 설치 프로그램 실행 파일 (NpsExtnForAzureMfaInstaller.exe) toohello NPS 서버에 복사 합니다.
3. Hello NPS 서버에서 두 번 클릭 **NpsExtnForAzureMfaInstaller.exe**합니다. 메시지가 표시되면 **실행**을 클릭합니다.
4. NPS 확장 Azure MFA 대화 상자에 대 한 hello, hello 소프트웨어 사용 조건 검토 확인 **toohello 사용 약관 동의**를 클릭 하 고 **설치**합니다.
 
  ![Azure MFA 설치](./media/nps-extension-remote-desktop-gateway/image2.png)

5. Azure MFA 대화 상자에 대 한 hello NPS 확장에서에서 닫기를 클릭 합니다. 

  ![Azure MFA용 NPS 확장](./media/nps-extension-remote-desktop-gateway/image3.png)

### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>PowerShell 스크립트를 사용 하 여 hello NPS 확장으로 사용 하기 위해 인증서 구성
다음으로 hello NPS 확장 tooensure 보안 통신 및 보증에서 사용 하기 위해 tooconfigure 인증서가 필요 합니다. hello NPS 구성 요소에는 NPS와 함께 사용 하기 위해 자체 서명 된 인증서를 구성 하는 Windows PowerShell 스크립트를 포함 합니다. 

hello 스크립트 hello 다음 작업을 수행 합니다.

* 자체 서명된 인증서 만들기
* Azure AD에서 사용자 인증서 tooservice의 공개 키를 연결합니다.
* 저장소 hello hello 로컬 컴퓨터 저장소에서 인증서
* Toohello 인증서의 개인 키 toohello 네트워크 사용자 액세스 부여
* 네트워크 정책 서버 서비스 다시 시작

자체 인증서 toouse 하려는 경우 Azure AD에서 tooassociate hello 공용 인증서 toohello 서비스 원칙의 필요 하 고 등입니다.

toouse hello 스크립트는 Azure AD 관리자 자격 증명에 hello 확장을 제공 하 고 앞에서 복사한 Azure AD 테 넌 트 ID hello 합니다. Hello NPS 확장 설치 위치는 각 NPS 서버에서 hello 스크립트를 실행 합니다. 그런 다음 않습니다 다음 hello:

1. 관리 Windows PowerShell 프롬프트를 엽니다.
2. Hello PowerShell 프롬프트에서 입력 **cd 'c:\Program Files\Microsoft\AzureMfa\Config'**, 누릅니다 **ENTER**합니다.
3. _.\AzureMfsNpsExtnConfigSetup.ps1_을 입력하고 **Enter** 키를 누릅니다. hello 스크립트 hello Azure Active Directory PowerShell 모듈 설치 된 경우 toosee를 확인 합니다. 설치 되어 있지 않으면 hello 스크립트 hello 모듈을 설치 합니다.

  ![Azure AD PowerShell](./media/nps-extension-remote-desktop-gateway/image4.png)
  
4. Hello PowerShell 모듈의 hello 설치를 확인 하는 hello 스크립트, 후 hello Azure Active Directory PowerShell 모듈 대화 상자가 표시 됩니다. Hello 대화 상자에서 Azure AD 관리자 자격 증명 및 암호를 입력 하 고 클릭 **로그인**합니다.

  ![Powershell 계정 열기](./media/nps-extension-remote-desktop-gateway/image5.png)

5. 대화 상자가 나타나면 toohello 클립보드를 앞에서 복사한 hello 테 넌 트 ID를 붙여 넣고 키를 눌러 **ENTER**합니다.

  ![테넌트 ID 입력](./media/nps-extension-remote-desktop-gateway/image6.png)

6. hello 스크립트 자체 서명 된 인증서를 만들고 다른 구성 변경 작업을 수행 합니다. 아래에 표시 된 hello 이미지와 같이 hello 출력 해야 합니다.

  ![자체 서명된 인증서](./media/nps-extension-remote-desktop-gateway/image7.png)

## <a name="configure-nps-components-on-remote-desktop-gateway"></a>원격 데스크톱 게이트웨이에서 NPS 구성 요소 구성
이 섹션에서는 hello 원격 데스크톱 게이트웨이 연결 권한 부여 정책 및 기타 RADIUS 설정을 구성합니다.

hello 인증 흐름에 RADIUS 메시지 hello 원격 데스크톱 게이트웨이 및 hello NPS 서버 hello NPS 서버를 설치한 간에 교환 될 필요 합니다. 즉, hello NPS 확장이 설치 되어 있는 원격 데스크톱 게이트웨이 및 hello 모두 NPS 서버의 RADIUS 클라이언트 설정을 구성 해야 합니다. 

### <a name="configure-remote-desktop-gateway-connection-authorization-policies-toouse-central-store"></a>원격 데스크톱 게이트웨이 연결 권한 부여 정책 toouse 중앙 저장소를 구성 합니다.
원격 데스크톱 연결 권한 부여 정책 (RD Cap)에 연결 tooa 원격 데스크톱 게이트웨이 서버에 대 한 hello 요구 사항을 지정 합니다. RD CAP는 로컬로(기본값) 저장하거나 NPS를 실행하는 중앙 RD CAP 저장소에 저장할 수 있습니다. RDS와 Azure mfa tooconfigure 통합, 중앙 저장소의 toospecify hello 사용을 해야합니다.

1. Hello RD 게이트웨이 서버에서 엽니다 **서버 관리자**합니다. 
2. Hello 메뉴를 클릭 **도구**, 너무 가리킨**원격 데스크톱 서비스**, 클릭 하 고 **원격 데스크톱 게이트웨이 관리자**합니다.

  ![원격 데스크톱 서비스](./media/nps-extension-remote-desktop-gateway/image8.png)

3. RD 게이트웨이 관리자 hello 단추로 클릭 하 고  **\[서버 이름\] (Local)**를 클릭 하 고 **속성**합니다.

  ![서버 이름](./media/nps-extension-remote-desktop-gateway/image9.png)

4. Hello 속성 대화 상자에서 선택 hello **RD CAP** 저장소 탭 합니다.
5. Hello RD CAP 저장소 탭에서 선택 **NPS를 실행 하는 중앙 서버**합니다. 
6. Hello에 **NPS를 실행 하는 hello 서버에 대 한 이름 또는 IP 주소를 입력** 필드 이름을 입력 합니다 hello IP 주소 또는 서버 hello 서버 hello NPS 확장을 설치 하는 위치입니다.

  ![이름 또는 IP 주소 입력](./media/nps-extension-remote-desktop-gateway/image10.png)
  
7. **추가**를 클릭합니다.
8. Hello에 **공유 암호** 대화 상자에서 공유 암호를 입력 한 다음 클릭 **확인**합니다. 이 공유 암호 기록 hello 레코드를 안전 하 게 저장 및 확인 합니다.

 >[!NOTE]
 >공유 암호는 hello RADIUS 서버와 클라이언트 간의 tooestablish 신뢰 합니다. 길고 복잡한 암호를 만드세요.
 >

 ![공유 비밀](./media/nps-extension-remote-desktop-gateway/image11.png)

9. 클릭 **확인** tooclose hello 대화 상자.

### <a name="configure-radius-timeout-value-on-remote-desktop-gateway-nps"></a>원격 데스크톱 게이트웨이 NPS에서 RADIUS 시간 제한 값 구성
tooensure 있습니다 toovalidate 사용자의 자격 증명을 시간, 2 단계 인증을 수행 하 고, 응답을 수신 되어 tooRADIUS 메시지 응답, 필요한 tooadjust hello RADIUS 제한 시간 값입니다.

1. Hello RD 게이트웨이 서버에서 서버 관리자에서 **도구**, 클릭 하 고 **네트워크 정책 서버**합니다. 
2. Hello에 **NPS (로컬)** 콘솔에서 **RADIUS 클라이언트 및 서버**를 선택 하 고 **원격 RADIUS 서버**합니다.

 ![원격 RADIUS 서버](./media/nps-extension-remote-desktop-gateway/image12.png)

3. Hello 세부 정보 창에서 두 번 클릭 **TS 게이트웨이 서버 그룹**합니다.

 >[!NOTE]
 >NPS 정책에 대 한 hello 중앙 서버를 구성할 때이 RADIUS 서버 그룹을 만들었습니다. RD 게이트웨이 hello hello 그룹에서 1 보다 큰 경우 RADIUS 메시지 toothis 서버 또는 서버 그룹에 전달 합니다.
 >

4. Hello에 **TS 게이트웨이 서버 그룹 속성** 대화 상자, 선택 hello IP 주소 또는 toostore RD Cap를 구성한 NPS 서버 hello 및 클릭 한 다음 이름을 **편집**합니다. 

 ![TS 게이트웨이 서버 그룹](./media/nps-extension-remote-desktop-gateway/image13.png)

5. Hello에 **RADIUS 서버 편집** 대화 상자, 선택 hello **부하 분산** 탭 합니다.
6. Hello에 **부하 분산** hello 탭 **시간 (초) 요청이 것으로 간주 되기 전에 응답 없이 삭제** 필드, 30-60 초 사이 tooa 값 3에서 hello 기본값을 변경 합니다.
7. Hello에 **서버가 사용할 수 없는 상태로 표시 된 경우 요청 사이의 시간 (초)** 필드 같으면 tooor hello 이전 단계에서 지정한 hello 값 보다 큰은 30 초 tooa 값의 hello 기본 값을 변경 하세요.

 ![Radius 서버 편집](./media/nps-extension-remote-desktop-gateway/image14.png)

8.  Tooclose hello 대화 상자에 시간 2 확인을 클릭 합니다.

### <a name="verify-connection-request-policies"></a>연결 요청 정책 확인 
기본적으로 hello RD 게이트웨이 toouse 연결 권한 부여 정책에 대 한 중앙 정책 저장소를 구성 하는 경우 hello RD 게이트웨이 구성 된 tooforward CAP 요청 toohello NPS 서버는 합니다. hello Azure MFA 확장명이 hello NPS 서버 설치 프로세스 hello RADIUS 액세스 요청 합니다. 단계를 수행 하는 hello 정책 tooverify hello 기본 연결을 요청 하는 방법을 보여 줍니다. 

1. RD 게이트웨이 hello hello NPS (로컬) 콘솔에서 확장 **정책**를 선택 하 고 **연결 요청 정책**합니다.
2. **연결 요청 정책**을 마우스 오른쪽 단추로 클릭하고 **TS 게이트웨이 권한 부여 정책**을 두 번 클릭합니다.
3. Hello에 **TS 게이트웨이 권한 부여 정책 속성** 대화 상자를 클릭 hello **설정을** 탭 합니다.
4. **설정** 탭의 [연결 요청 전달]에서 **인증**을 클릭합니다. RADIUS 클라이언트는 인증에 대 한 구성 된 tooforward 요청입니다.

 ![인증 설정](./media/nps-extension-remote-desktop-gateway/image15.png)
 
5. **취소**를 클릭합니다. 

## <a name="configure-nps-on-hello-server-where-hello-nps-extension-is-installed"></a>Hello NPS 확장이 설치 되어 있는 hello 서버의 NPS를 구성 합니다.
hello NPS 서버 hello NPS 확장 hello NPS 서버에 원격 데스크톱 게이트웨이 hello 사용 하 여 설치 된 요구 toobe 수 tooexchange RADIUS 메시지입니다. 이 메시지를 교환 tooenable, hello NPS 확장 서비스를 설치한 hello 서버의 tooconfigure hello NPS 구성 요소가 필요 합니다. 

### <a name="register-server-in-active-directory"></a>Active Directory에 서버 등록
이 시나리오에서 제대로 toofunction, NPS 서버 hello toobe Active Directory에 등록 해야 합니다.

1. **서버 관리자**를 엽니다.
2. [서버 관리자]에서 **도구**를 클릭한 다음 **네트워크 정책 서버**를 클릭합니다. 
3. Hello 네트워크 정책 서버 콘솔에서 마우스 오른쪽 단추로 클릭 **NPS (로컬)**, 클릭 하 고 **Active Directory에 등록 서버**합니다. 
4. **확인**을 두 번 클릭합니다.

 ![AD에 서버 등록](./media/nps-extension-remote-desktop-gateway/image16.png)

5. Hello 콘솔을 hello 다음 절차에 대 한 열어 둡니다.

### <a name="create-and-configure-radius-client"></a>RADIUS 클라이언트 만들기 및 구성 
원격 데스크톱 게이트웨이 hello toobe RADIUS 클라이언트 toohello NPS 서버를 구성 해야 합니다. 

1. Hello에 hello NPS 확장이 설치 되어 hello NPS 서버 **NPS (로컬)** 콘솔 마우스 오른쪽 단추로 클릭 **RADIUS 클라이언트** 클릭 **새로**합니다.

 ![새 RADIUS 클라이언트](./media/nps-extension-remote-desktop-gateway/image17.png)

2. Hello에 **새 RADIUS 클라이언트** 대화 상자를 같은 친숙 한 이름을 제공 _게이트웨이_, hello hello 원격 데스크톱 게이트웨이 서버의 DNS 이름 또는 IP 주소 및 합니다. 
3. Hello에 **공유 암호** 및 hello **공유 암호 확인** 필드 입력 hello 이전에 사용한 동일한 암호입니다.

 ![이름 및 주소](./media/nps-extension-remote-desktop-gateway/image18.png)

4. 클릭 **확인** tooclose hello 새 RADIUS 클라이언트 대화 상자.

### <a name="configure-network-policy"></a>네트워크 정책 구성
Azure MFA 확장 hello로 회수 hello NPS 서버는 hello 연결 권한 부여 정책 (CAP)에 대 한 hello 지정 된 중앙 정책 저장소입니다. 따라서 hello NPS 서버 tooauthorize 유효한 연결 요청에 CAP tooimplement을 해야합니다.  

1. Hello NPS (로컬) 콘솔에서 확장 **정책**를 클릭 하 고 **네트워크 정책**합니다.
2. 마우스 오른쪽 단추로 클릭 **연결 tooother 액세스 서버**를 클릭 하 고 **정책 중복**합니다. 

 ![중복된 정책](./media/nps-extension-remote-desktop-gateway/image19.png)

3. 마우스 오른쪽 단추로 클릭 **연결 복사본 tooother 액세스 서버**를 클릭 하 고 **속성**합니다.

 ![네트워크 속성](./media/nps-extension-remote-desktop-gateway/image20.png)

4. Hello에 **연결 복사본 tooother 액세스 서버** 대화 상자, 정책 이름에 적합 한 이름 같은 입력 **RDG_CAP**합니다. **정책 사용**을 선택하고 **액세스 허용**을 선택합니다. 필요에 따라 네트워크 액세스 형식에서 **원격 데스크톱 게이트웨이**를 선택하거나 **지정되지 않음**으로 그대로 둘 수 있습니다.

 ![연결 복사본](./media/nps-extension-remote-desktop-gateway/image21.png)

5.  Hello 클릭 **제약 조건을** 탭을 확인 **인증 방법을 협상 하지 않고 허용 클라이언트 tooconnect**합니다.

 ![클라이언트가 허용 tooconnect](./media/nps-extension-remote-desktop-gateway/image22.png)

6. 필요에 따라 hello 클릭 **조건** 탭 및 hello 연결 toobe 권한이, 예를 들어 특정 Windows 그룹 멤버 자격에 대해 충족 해야 하는 조건을 추가 합니다.

 ![조건](./media/nps-extension-remote-desktop-gateway/image23.png)

7. **확인**을 클릭합니다. 입력 정보 요청된 tooview hello 해당 하는 도움말 항목을 클릭 하 여 **아니요**합니다.
8. 액세스 부여 하는 것이 고 hello hello 정책을 사용 하는 hello 목록 위쪽에 새 정책 인지 확인 합니다.

 ![네트워크 정책](./media/nps-extension-remote-desktop-gateway/image24.png)

## <a name="verify-configuration"></a>구성 확인
tooverify hello 구성 해야 toolog 원격 데스크톱 게이트웨이 hello에 적합 한 RDP 클라이언트를 사용 합니다. 있는지 toouse 연결 권한 부여 정책에서 허용 하 고 Azure MFA에 대해 사용 하도록 설정 하는 계정 이어야 합니다. 

Hello 이미지 아래에 표시를 사용 하 여 hello **원격 데스크톱 웹 액세스** 페이지.

![원격 데스크톱 웹 액세스](./media/nps-extension-remote-desktop-gateway/image25.png)

기본 인증을 위해 자격 증명 입력을 시 hello 원격 데스크톱 연결 대화 상자 아래와 같이 원격 연결을 초기화 하는 상태가 표시 됩니다. 

Azure MFA에서 이전에 구성한 hello 보조 인증 방법으로 성공적으로 인증 하는 경우 연결 된 toohello 리소스입니다. 그러나 hello 보조 인증 실패할 경우 tooresource 액세스를 거부 됩니다. 

![원격 연결 시작](./media/nps-extension-remote-desktop-gateway/image26.png)

Hello 인증자 아래 hello 예제에서 Windows phone에서 앱 인증이 사용 되는 tooprovide hello 보조 합니다.

![계정](./media/nps-extension-remote-desktop-gateway/image27.png)

Hello 보조 인증 방법을 사용 하 여 인증 성공적으로 면 hello 원격 데스크톱 게이트웨이 정상적으로 로그인 해야 합니다. 그러나 필요한 toouse 신뢰할 수 있는 장치에서 모바일 앱을 사용 하 여 보조 인증 방법 이므로, hello 로그인 프로세스는 그렇지 않은 경우 복구할 때 보다 더 안전 합니다.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>성공적인 로그온 이벤트에 대한 이벤트 뷰어 로그 보기
tooview hello 성공적인 로그인 이벤트 hello Windows 이벤트 뷰어 로그에서 다음 Windows PowerShell 명령 tooquery hello Windows 터미널 서비스 및 Windows 보안 로그 hello를 발급할 수 있습니다.

tooquery 성공적인 로그인 이벤트 hello 게이트웨이 작업 로그에서 _(이벤트 뷰어 \ 응용 프로그램 및 서비스 Logs\Microsoft\Windows\TerminalServices Gateway\Operational_, hello 다음 명령을 사용 하 여:

* _Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '300'} | FL 
* 이 명령은 hello 사용자 리소스 권한 부여 정책 요구 사항을 RD RAP ()을 충족 하 고 액세스 권한이 부여 되었습니다 표시 하는 Windows 이벤트를 표시 합니다.

![이벤트 뷰어 보기](./media/nps-extension-remote-desktop-gateway/image28.png)

* _Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '200'} | FL
* 이 명령은 사용자 연결 권한 부여 정책 요구 사항을 충족 하는 경우를 보여 주는 hello 이벤트를 표시 합니다.

![연결 권한 부여](./media/nps-extension-remote-desktop-gateway/image29.png)

또한 이 로그를 보고 300 및 200 이벤트 ID에서 필터링할 수도 있습니다. tooquery 성공 로그온 이벤트 hello 보안 이벤트 뷰어 로그에서 다음 명령을 hello를 사용 합니다.

* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL 
* 이 명령은 실행할 수 중앙 NPS hello 또는 RD 게이트웨이 서버를 환영 합니다. 

![성공적인 로그온 이벤트](./media/nps-extension-remote-desktop-gateway/image30.png)

아래와 같이 hello 보안 로그 또는 네트워크 정책 및 액세스 서비스 사용자 지정 보기 hello도 볼 수 있습니다.

![네트워크 정책 및 액세스 서비스](./media/nps-extension-remote-desktop-gateway/image31.png)

Azure MFA에 대 한 hello NPS 확장을 설치한 hello 서버에서 찾을 수 있습니다 이벤트 뷰어 응용 프로그램 로그에서 특정 toohello 확장 _응용 프로그램 및 서비스 Logs\Microsoft\AzureMfa_합니다. 

![이벤트 뷰어 응용 프로그램 로그](./media/nps-extension-remote-desktop-gateway/image32.png)

## <a name="troubleshoot-guide"></a>문제 해결 가이드

Hello 구성이 예상 대로 작동 하지 않는 경우 첫 번째 위치 toostart tootroubleshoot hello 경우 사용자 hello tooverify가 구성 된 toouse Azure MFA. Hello 사용자 toohello 연결 [Azure 포털](https://portal.azure.com)합니다. 사용자가 보조 인증을 요청받았고 성공적으로 인증할 수 있으면 Azure MFA의 잘못된 구성을 제거할 수 있습니다.

Azure MFA hello 사용자에 대해 작동 하 고 hello 관련 이벤트 로그를 검토 해야 합니다. 여기에 hello 이전 섹션에서 설명 하는 hello 보안 이벤트, 운영, 게이트웨이 및 Azure MFA 로그 포함 됩니다. 

다음은 실패한 로그온 이벤트(6273 이벤트 ID)를 보여 주는 보안 로그의 출력 예입니다.

![실패한 로그온 이벤트](./media/nps-extension-remote-desktop-gateway/image33.png)

다음은 hello AzureMFA 로그에서 관련된 이벤트입니다.

![Azure MFA 로그](./media/nps-extension-remote-desktop-gateway/image34.png)

tooperform 고급 옵션을 참조 하 여 hello NPS 데이터베이스 형식 로그 파일 hello NPS 서비스를 설치한 문제를 해결 합니다. 이러한 로그 파일은 _%SystemRoot%\System32\Logs_ 폴더에 쉼표로 구분된 텍스트 파일로 만들어집니다. 

이러한 로그 파일에 대한 자세한 내용은 [NPS 데이터베이스 형식 로그 파일 해석(영문)](https://technet.microsoft.com/library/cc771748.aspx)을 참조하세요. 이러한 로그 파일의 hello 항목 스프레드시트나 데이터베이스 가져오지 않고 어려운 toointerpret 될 수 있습니다. 여러 IAS 파서를 찾을 수 있습니다 온라인 tooassist 로그 파일을 hello 해석에 있습니다. 

hello 아래 이미지 출력을 보여 hello 하나의 같은 다운로드 가능한 [셰어웨어 응용 프로그램](http://www.deepsoftware.com/iasviewer)합니다. 

![셰어웨어 앱](./media/nps-extension-remote-desktop-gateway/image35.png)

마지막으로 추가적인 문제 해결 옵션을 위해 [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)와 같은 프로토콜 분석기를 사용할 수 있습니다. 

hello Microsoft 메시지 분석기에서 아래 이미지 표시 hello 사용자 이름을 포함 하는 RADIUS 프로토콜을 필터링 하는 네트워크 트래픽을 **Contoso\AliceC**합니다.

![Microsoft Message Analyzer](./media/nps-extension-remote-desktop-gateway/image36.png)

## <a name="next-steps"></a>다음 단계
[어떻게 tooget Azure Multi-factor Authentication](multi-factor-authentication-versions-plans.md)

[RADIUS를 사용한 원격 데스크톱 게이트웨이 및 Azure Multi-Factor Authentication 서버](multi-factor-authentication-get-started-server-rdg.md)

[Azure Active Directory와 온-프레미스 디렉터리 통합](../active-directory/connect/active-directory-aadconnect.md)
