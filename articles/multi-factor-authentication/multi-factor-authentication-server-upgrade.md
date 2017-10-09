---
title: "aaaAzure MFA 서버 업그레이드 | Microsoft Docs"
description: "단계 및 지침 tooupgrade hello Azure Multi-factor Authentication 서버 tooa 최신 버전입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: aaa8d400e0e5f1c6be3a6d22cde6dd893ef4d546
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-toohello-latest-azure-multi-factor-authentication-server"></a>Toohello 업그레이드 최신 Azure Multi-factor Authentication 서버

이 문서에서는 hello를 통해 Azure Multi-factor Authentication (MFA) 서버 v6.0 업그레이드 프로세스 또는 더 높은 합니다. 이전 버전의 hello PhoneFactor Agent tooupgrade, 필요한 경우 너무 참조[업그레이드 hello PhoneFactor Agent tooAzure Multi-factor Authentication 서버](multi-factor-authentication-get-started-server-upgrade.md)합니다.

V6.x 또는 이전 toov7.x에서 업그레이드 하거나 최신 인 경우 모든 구성 요소는.NET 2.0 too.NET 4.5에서에서 변경 합니다. 모든 구성 요소에는 Microsoft Visual C++ 2015 재배포 가능 패키지 업데이트 1 이상이 필요합니다. 이미 설치 되어 있지 않으면 hello MFA 서버 설치 프로그램에서 모두 hello x86 및 x64 버전의 이러한 구성 요소를 설치 합니다. Hello 사용자 포털 및 모바일 앱 웹 서비스에 별도 서버에서 실행 해야 tooinstall 패키지만 해당 구성 요소를 업그레이드 하기 전에. Hello hello에 최신 Microsoft Visual c + + 2015 재배포 가능 패키지 업데이트를 검색할 수 있습니다 [Microsoft 다운로드 센터](https://www.microsoft.com/en-us/download/)합니다. 

## <a name="install-hello-latest-version-of-azure-mfa-server"></a>Hello 최신 버전의 Azure MFA 서버 설치

1. Hello 지침에 따라 [Azure Multi-factor Authentication 서버 다운로드 hello](multi-factor-authentication-get-started-server.md#download-the-azure-multi-factor-authentication-server) tooget hello 최신 버전의 Azure MFA 서버 hello 합니다.
2. 마스터 서버에 MFA C:\Program Files\multi-factor Authentication Server\Data\PhoneFactor.pfdata (되었다고 가정 하면 hello 기본 설치 위치)에 있는 hello와 MFA 서버 데이터 파일의 백업을 만듭니다.
3. 고가용성을 위해 여러 서버를 실행 하는 경우 toohello 서버를 업그레이드 하는 트래픽 전송을 중지 되도록 toohello MFA 서버를 인증 하는 hello 클라이언트 시스템을 변경 합니다. 부하 분산 장치를 사용 하는 경우 MFA 서버 hello 부하 분산 장치에서 제거 업그레이드 hello을 수행한 다음 hello 팜으로 hello 서버를 추가 합니다.
4. 각 MFA 서버 hello 새 설치를 실행 합니다. Hello hello 마스터 여 복제 되는 이전 데이터 파일을 읽을 수 때문에 먼저 하위 서버를 업그레이드 합니다. 

  않아도 toouninstall hello 설치 관리자를 실행 하기 전에 현재 MFA 서버입니다. hello 설치는 적절 한 업그레이드를 수행합니다. hello 설치 경로에서 선택 되었습니다 hello 레지스트리 hello 이전 설치에서 설치 hello에서 동일 하므로 위치 (예: C:\Program Files\multi-factor Authentication Server). 
  
5. 증명된 tooinstall Microsoft Visual c + + 2015 재배포 가능 패키지 업데이트 패키지를 사용 하는 경우에 hello 라는 메시지를 수락 합니다. Hello 패키지의 hello x86 및 x64 버전이 모두 설치 되어 있습니다.
5. Hello 웹 서비스 SDK를 사용 하는 경우 메시지가 표시 되 tooinstall hello 새 웹 서비스 SDK입니다. 새 웹 서비스 SDK hello, 설치할 때 해당 hello 가상 디렉터리 이름이 이전에 설치 하는 hello 가상 디렉터리 (예를 들어 MultiFactorAuthWebServiceSdk)와 일치 하는지 확인 합니다.
6. 모든 하위 서버에서 hello 단계를 반복 합니다. Hello 부하 직원 toobe hello 새 마스터를 다음 업그레이드 hello 이전 마스터 서버 중 하나를 승격 합니다. 

## <a name="upgrade-hello-user-portal"></a>Hello 사용자 포털 업그레이드

1. Hello hello 사용자 포털 설치 위치 (예: C:\inetpub\wwwroot\MultiFactorAuth)의 가상 디렉터리에 있는 hello web.config 파일의 백업을 만듭니다. Toohello 기본 테마 변경 사항, 경우에 hello App_Themes\Default 폴더의 백업을 만듭니다. 더 나은 toocreate hello 기본 폴더의 복사본 되며 toochange hello 기본 테마 보다 새 테마를 만듭니다.
2. 사용자 포털 hello 동일한 서버 hello 다른 MFA 서버 구성 요소 같이 hello hello에서 실행 하는 경우 MFA 서버 설치 tooupdate hello 사용자 포털이 표시 됩니다. Hello 메시지를 확인 하 고 hello 사용자 포털 업데이트를 설치 합니다. 이전에 설치 하는 hello 가상 디렉터리 (예를 들어 MultiFactorAuth) 일치 하는 해당 hello 가상 디렉터리 이름을 확인 합니다.
3. 사용자 포털 hello 자체 서버에 있으면 hello로 hello MultiFactorAuthenticationUserPortalSetup64.msi 파일을 복사 hello MFA 서버 중 하나의 위치를 설치 하 고 hello 사용자 포털 웹 서버에 저장 합니다. Hello 설치 관리자를 실행 합니다. 

  상자가 오류가 발생 하는 경우 "Microsoft Visual c + + 2015 재배포 가능 패키지 업데이트 1 이상이 필요 는"에서 다운로드 및 설치 hello 최신 업데이트 패키지 hello [Microsoft 다운로드 센터](https://www.microsoft.com/download/)합니다. Hello x86 및 x64 버전을 모두 설치 합니다.

4. 소프트웨어를 설치 하는 사용자 포털을 업데이트 하는 hello 후 hello 새 web.config 파일로 1 단계에서 만든 hello web.config 백업을 비교 합니다. Hello 새 web.config에 새 특성이 있으면 hello 가상 디렉터리 toooverwrite hello 새에 백업 하려면 web.config를 복사 합니다. 또 다른 방법은 toocopy/붙여넣기 hello appSettings 값과 hello hello 백업 hello 새 web.config 파일에서 웹 서비스 SDK URL입니다.

여러 서버에서 사용자 포털 hello를 사용 하도록 설정한 경우 모든 속성에 hello 설치를 반복 합니다. 


## <a name="upgrade-hello-mobile-app-web-service"></a>Hello 모바일 앱 웹 서비스를 업그레이드 합니다.

1. 모바일 앱 웹 서비스 설치 위치 (예를 들어 C:\inetpub\wwwroot\app 또는 C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService)의 hello hello 가상 디렉터리에 있는 hello web.config 파일의 백업을 만듭니다.
2. MFA 서버 hello의 위치를 설치 하 고 hello 모바일 응용 프로그램 등록 웹 서버에 저장 하는 hello로 hello MultiFactorAuthenticationMobileAppWebServiceSetup64.msi 파일을 복사 합니다.
3. Hello 설치 관리자를 실행 합니다. 

  Microsoft Visual c + + 2015 재배포 가능 패키지 업데이트 1 이상이 필요한 않음을 나타내는 오류가 발생 하는 경우 다운로드 하 여 hello hello 최신 업데이트 패키지 설치 [Microsoft 다운로드 센터](https://www.microsoft.com/download/)합니다. Hello x86 및 x64 버전을 모두 설치 합니다.

4. 업데이트 하는 hello 모바일 앱 웹 서비스 소프트웨어를 설치한 후 새 web.config 파일로 hello 1 단계에서 백업한 hello web.config 파일을 비교 합니다. 새 특성이 없는 hello 새 web.config에 있는 경우 hello 가상 디렉터리에 다시 저장 된 web.config를 복사 수 있으며 새 hello를 덮어씁니다. 또 다른 방법은 toocopy/붙여넣기 hello appSettings 값과 hello hello 백업 hello 새 web.config 파일에서 웹 서비스 SDK URL입니다.

여러 서버에서 모바일 앱 웹 서비스 hello를 사용 하도록 설정한 경우 모든 속성에 hello 설치를 반복 합니다. 

## <a name="upgrade-hello-ad-fs-adapters"></a>Hello AD FS 어댑터를 업그레이드 합니다.


### <a name="if-mfa-runs-on-different-servers-than-ad-fs"></a>MFA가 AD FS 이외의 다른 서버에서 실행되는 경우

다음 지침은 AD FS 서버와는 별도로 Multi-factor Authentication 서버를 실행하는 경우에만 적용됩니다. 두 서비스에서 실행 하는 경우 동일한 서버 hello,이 섹션을 건너뛰고 toohello 설치 단계를 이동 합니다. 

1. AD FS에서 등록 된 hello MultiFactorAuthenticationAdfsAdapter.config 파일의 복사본을 저장 하거나 다음 PowerShell 명령을 hello를 사용 하 여 hello 구성 내보내기: `Export-AdfsAuthenticationProviderConfigurationData -Name [adapter name] -FilePath [path tooconfig file]`합니다. hello 어댑터 이름은 이전에 설치 하는 hello 버전에 따라 "WindowsAzureMultiFactorAuthentication" 또는 "AzureMfaServerAuthentication" 중 하나입니다.
2. Hello 파일 hello와 MFA 서버 설치 위치 toohello AD FS 서버에서 다음을 복사 합니다.

  - MultiFactorAuthenticationAdfsAdapterSetup64.msi
  - Register-MultiFactorAuthenticationAdfsAdapter.ps1
  - Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
  - MultiFactorAuthenticationAdfsAdapter.config

3. 추가 하 여 hello Register-multifactorauthenticationadfsadapter.ps1 스크립트를 편집 `-ConfigurationFilePath [path]` hello toohello 끝 `Register-AdfsAuthenticationProvider` 명령입니다. 대체 *[경로]* 와 hello 전체 경로 toohello MultiFactorAuthenticationAdfsAdapter.config 파일 또는 hello 구성 파일 단계에서 내보낸 hello 이전 합니다. 

  Hello 이전 구성 파일을 일치 하는 경우 새 MultiFactorAuthenticationAdfsAdapter.config toosee hello에에서 hello 특성을 검사 합니다. 특성이 추가 되거나 hello 새 버전에서 제거 된, 경우 hello 이전 구성 파일 toohello 새에서에서 hello 특성 값을 복사 하거나 hello 이전 구성 파일 toomatch 수정 합니다.

### <a name="install-new-ad-fs-adapters"></a>새 AD FS 어댑터 설치

> [!IMPORTANT] 
> 사용자가이 섹션의 3-8 단계 동안 필요한 tooperform 2 단계 인증 되지 않습니다. AD FS에 구성 된 경우 여러 클러스터를 제거할 수 있습니다, 업그레이드 및 hello의 각 클러스터와 독립적으로 팜 복원 hello 다른 클러스터 tooavoid 가동 중지 시간.

1. Hello 팜에서 일부 AD FS 서버를 제거 합니다. 실행 중인 다른 hello 하는 동안 이러한 서버를 업데이트 합니다.
2. Hello AD FS 팜에서 제거 하는 각 서버에 hello 새 AD FS 어댑터를 설치 합니다. MFA 서버 hello 각 AD FS 서버에 설치 되어, 사용자 환경 admin 님 안녕하세요 MFA 서버를 통해 업데이트할 수 있습니다. 그렇지 않으면 MultiFactorAuthenticationAdfsAdapterSetup64.msi를 실행하여 업데이트합니다. 

  상자가 오류가 발생 하는 경우 "Microsoft Visual c + + 2015 재배포 가능 패키지 업데이트 1 이상이 필요 는"에서 다운로드 및 설치 hello 최신 업데이트 패키지 hello [Microsoft 다운로드 센터](https://www.microsoft.com/download/)합니다. Hello x86 및 x64 버전을 모두 설치 합니다.

3. 너무 이동**AD FS** > **인증 정책** > **전역 다단계 인증 정책 편집**합니다. 선택을 취소 **WindowsAzureMultiFactorAuthentication** 또는 **AzureMFAServerAuthentication** (에 따라 설치 된 hello 현재 버전). 

  이 단계가 완료되면 8단계를 완료할 때까지 이 AD FS 클러스터에서 MFA 서버를 통한 2단계 인증을 사용할 수 없습니다.

4. 등록 취소 hello 이전 버전의 hello Unregister-multifactorauthenticationadfsadapter.ps1 PowerShell 스크립트를 실행 하 여 hello AD FS 어댑터. 해당 hello 확인 *-이름* 매개 변수 ("WindowsAzureMultiFactorAuthentication" 또는 "AzureMFAServerAuthentication")에 3 단계에 표시 된 hello 이름과 일치 합니다. 이 중앙에서 구성 되므로 tooall 서버 hello 동일한 AD FS 클러스터에 적용 됩니다.
5. Hello Register-multifactorauthenticationadfsadapter.ps1 PowerShell 스크립트를 실행 하 여 hello 새 AD FS 어댑터를 등록 합니다. 이 중앙에서 구성 되므로 tooall 서버 hello 동일한 AD FS 클러스터에 적용 됩니다.
6. Hello hello AD FS 팜에서 제거 하는 각 서버에서 AD FS 서비스를 다시 시작 합니다.
7. 제거 hello 팜에서 다른 서버 hello 및 hello 업데이트 서버를 toohello AD FS 팜에 다시 추가 합니다.
8. 너무 이동**AD FS** > **인증 정책** > **전역 다단계 인증 정책 편집**합니다. **AzureMfaServerAuthentication**을 선택합니다.
9. 2 단계 tooupdate hello 서버 hello AD FS 팜에서 들었습니다. 그러나 이제를 반복 하 고 해당 서버의 hello AD FS 서비스를 다시 시작 합니다.
10. Hello AD FS 팜으로 서버를 추가 합니다.

## <a name="next-steps"></a>다음 단계

- [Azure Multi-Factor Authentication 및 타사 VPN을 사용한 고급 시나리오](multi-factor-authentication-advanced-vpn-configurations.md) 예제 보기

- [MFA 서버를 Windows Server Active Directory와 동기화](multi-factor-authentication-get-started-server-dirint.md)

- 응용 프로그램에 대한 [Windows 인증 구성](multi-factor-authentication-get-started-server-windows.md)
