---
title: "Windows server에서 AD fs 서버 aaaMFA | Microsoft Docs"
description: "이 문서에서는 Azure Multi-factor Authentication 및 2016 및 Windows Server 2012 r 2에서 AD FS를 사용 하 여 tooget 시작 하는 방법을 설명 합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 57208068-1e55-45b6-840f-fdcd13723074
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/29/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 656785abcc63a020add765a86670b488a3b84b51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-in-windows-server"></a>Windows server에서 AD FS를 사용 하 여 Azure Multi-factor Authentication 서버 toowork 구성
Active Directory Federation Services (AD FS)을 사용 하 고 toosecure 클라우드 또는 온-프레미스 리소스를 사용할 경우 AD FS와 함께 Azure Multi-factor Authentication 서버 toowork를 구성할 수 있습니다. 이 구성은 높은 값의 끝점에 대해 2단계 인증을 트리거합니다.

이 문서에서는 Windows Server 2012 R2 또는 Windows Server 2016에서 AD FS와 함께 Azure Multi-Factor Authentication 서버를 사용하는 방법을 설명합니다. 자세한 내용은 읽는 방법에 대 한 너무[AD fs 2.0 Azure Multi-factor Authentication 서버를 사용 하 여 클라우드 및 온-프레미스 리소스 보호](multi-factor-authentication-get-started-adfs-adfs2.md)합니다.

## <a name="secure-windows-server-ad-fs-with-azure-multi-factor-authentication-server"></a>Azure Multi-Factor Authentication 서버를 사용하여 Windows Server AD FS 보안 유지
Azure Multi-factor Authentication 서버를 설치할 때 다음 옵션 hello 있습니다.

* Hello에 Azure Multi-factor Authentication 서버를 로컬로 설치 AD FS와 동일한 서버
* Hello AD FS 서버에서 로컬로 hello Azure Multi-factor Authentication 어댑터를 설치 하 고 다른 컴퓨터에 Multi-factor Authentication 서버 설치

시작 하기 전에 다음 정보는 hello 고려해 야 합니다.

* AD FS 서버에 대해 필요한 tooinstall Azure Multi-factor Authentication 서버 않습니다. 그러나 AD FS를 실행 하는 Windows Server 2016 또는 Windows Server 2012 r 2에서 AD FS에 대 한 hello Multi-factor Authentication 어댑터를 설치 해야 합니다. 지원 되는 버전 이며 AD FS 페더레이션 서버에서 개별적으로 hello AD FS 어댑터를 설치 하는 경우 다른 컴퓨터에 hello 서버를 설치할 수 있습니다. Hello 참조 프로시저 toolearn 다음 방법을 tooinstall hello 어댑터 별도로 합니다.
* 조직에는 문자 메시지 또는 모바일 앱 확인 방법을 사용 하는, 하는 경우 회사 설정에 정의 된 hello 문자열 자리 표시자를 포함 하는 <$*i o n _*$> 합니다. MFA 서버 v7.1에서 이 자리 표시자를 대체하는 응용 프로그램 이름을 제공할 수 있습니다. V7.0에서 또는 이전 hello AD FS 어댑터를 사용 하 여이 자리 표시자가 자동으로 대체 되지 않습니다. 이러한 이전 버전에 대 한 AD FS 보안을 유지 하면 hello 자리 표시자 hello 적절 한 문자열에서 제거 합니다.
* toosign를 사용 하는 hello 계정에는 Active Directory 서비스에 사용자 권한 toocreate 보안 그룹 있어야 합니다.
* hello Multi-factor Authentication AD FS 어댑터 설치 마법사는 라는 인스턴스의 Active Directory에서 PhoneFactor Admins 보안 그룹을 만듭니다. 다음 페더레이션 서비스 toothis 그룹의 hello AD FS 서비스 계정을 추가 합니다. 도메인 컨트롤러에서 PhoneFactor Admins 그룹이 실제로 생성 되는 hello 및 hello AD FS 서비스 계정을이 그룹의 구성원 인지 확인 합니다. 필요한 경우 수동으로 도메인 컨트롤러에 hello AD FS 서비스 계정 toohello PhoneFactor Admins 그룹을 추가 합니다.
* 에 대해 알아보세요 hello 사용자 포털을 사용 하 여 hello 웹 서비스 SDK를 설치 하는 방법에 대 한 내용은 [Azure Multi-factor Authentication 서버에 대 한 hello 사용자 포털을 배포 합니다.](multi-factor-authentication-get-started-portal.md)

### <a name="install-azure-multi-factor-authentication-server-locally-on-hello-ad-fs-server"></a>Hello AD FS 서버에서 Azure Multi-factor Authentication 서버를 로컬로 설치
1. AD FS 서버에 Azure Multi-Factor Authentication 서버를 다운로드하여 설치합니다. 설치에 대한 내용은 [Azure Multi-factor Authentication 서버로 시작](multi-factor-authentication-get-started-server.md)을 읽어보세요.
2. Hello Azure Multi-factor Authentication 서버 관리 콘솔에서 클릭 hello **AD FS** 아이콘입니다. Hello 옵션을 선택 **사용자 등록 허용** 및 **있도록 tooselect 메서드**합니다.
3. 원하는 toospecify 조직에 대 한 추가 옵션을 선택 합니다.
4. **AD FS 어댑터 설치**를 클릭합니다.
   
   <center>![클라우드](./media/multi-factor-authentication-get-started-adfs-w2k12/server.png)</center>

5. Hello Active Directory 창이 표시 되는 경우 다음 두 가지 즉. 컴퓨터가 도메인에 가입된 tooa 및 hello AD FS 어댑터와 hello Multi-factor Authentication 서비스 간에 보안 통신에 대 한 hello Active Directory 구성이 완료 되지 않았습니다. 클릭 **다음** tooautomatically이이 구성을 완료 하거나 hello 선택 **자동 Active Directory 구성을 건너뛰고 구성 설정을 수동으로** 확인란 합니다. **다음**을 누릅니다.
6. 로컬 그룹 windows hello 표시 되 면 다음 두 가지 즉. 컴퓨터는 조인 된 tooa 도메인 및 hello AD FS 어댑터와 hello Multi-factor Authentication 서비스 간에 보안 통신에 대 한 hello 로컬 그룹 구성이 완료 되지 않았습니다. 클릭 **다음** tooautomatically이이 구성을 완료 하거나 hello 선택 **자동 로컬 그룹 구성을 건너뛰고 구성 설정을 수동으로** 확인란 합니다. **다음**을 누릅니다.
7. Hello 설치 마법사에서 **다음**합니다. Azure Multi-factor Authentication 서버 hello PhoneFactor Admins 그룹을 만들고 hello AD FS 서비스 계정 toohello PhoneFactor Admins 그룹을 추가 합니다.
   <center>![클라우드](./media/multi-factor-authentication-get-started-adfs-w2k12/adapter.png)</center>
8. Hello에 **설치 관리자 시작** 페이지 **다음**합니다.
9. Hello Multi-factor Authentication AD FS 어댑터 설치 관리자에서 클릭 **다음**합니다.
10. 클릭 **닫기** hello 설치가 완료 되는 경우.
11. Hello 어댑터 설치가 완료 된 후 AD FS와 함께 등록 해야 합니다. Windows PowerShell을 열고 다음 명령을 hello를 실행 합니다.<br>
    `C:\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`
    <center>![클라우드](./media/multi-factor-authentication-get-started-adfs-w2k12/pshell.png)</center>
12. toouse 새로 등록 된 어댑터를 AD FS에서 사용 되는 hello 전역 인증 정책 편집 합니다. Hello AD FS 관리 콘솔에서 toohello 이동 **인증 정책** 노드. Hello에 **multi-factor Authentication** 섹션에서 hello **편집** 다음 toohello 연결 **전역 설정** 섹션. Hello에 **전역 인증 정책 편집** 창에서 **Multi-factor Authentication** 클릭 한 다음 추가 인증 방법으로 **확인**합니다. hello 어댑터는 WindowsAzureMultiFactorAuthentication으로 등록 됩니다. Hello 등록 tootake 효과 대 한 hello AD FS 서비스를 다시 시작 합니다.

<center>![클라우드](./media/multi-factor-authentication-get-started-adfs-w2k12/global.png)</center>

이 시점에서 AD fs를 사용 하는 추가 인증 공급자 toouse Multi-factor Authentication 서버를 toobe 설정 됩니다.

## <a name="install-a-standalone-instance-of-hello-ad-fs-adapter-by-using-hello-web-service-sdk"></a>Hello 웹 서비스 SDK를 사용 하 여 hello AD FS 어댑터의 독립 실행형 인스턴스를 설치 합니다.
1. Multi-factor Authentication 서버를 실행 하는 hello 서버에 hello 웹 서비스 SDK를 설치 합니다.
2. Hello \program에서 파일을 복사 hello 다음-tooinstall hello AD FS 어댑터 하려는 Authentication Server 디렉터리 toohello 서버:
   * MultiFactorAuthenticationAdfsAdapterSetup64.msi
   * Register-MultiFactorAuthenticationAdfsAdapter.ps1
   * Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
   * MultiFactorAuthenticationAdfsAdapter.config
3. Hello MultiFactorAuthenticationAdfsAdapterSetup64.msi 설치 파일을 실행 합니다.
4. Hello Multi-factor Authentication AD FS 어댑터 설치 관리자에서 클릭 **다음** toostart hello 설치 합니다.
5. 클릭 **닫기** hello 설치가 완료 되는 경우.

## <a name="edit-hello-multifactorauthenticationadfsadapterconfig-file"></a>Hello MultiFactorAuthenticationAdfsAdapter.config 파일 편집
이러한 단계 tooedit hello MultiFactorAuthenticationAdfsAdapter.config 파일을 수행 합니다.

1. 집합 hello **UseWebServiceSdk** 노드 너무**true**합니다.  
2. 에 대 한 hello 값 설정 **WebServiceSdkUrl** hello Multi-factor Authentication 웹 서비스 SDK의 toohello URL입니다. 예를 들어: *https://contoso.com/&lt;certificatename&gt;/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx*여기서 *certificatename* hello 인증서 이름입니다.  
3. 추가 하 여 hello Register-multifactorauthenticationadfsadapter.ps1 스크립트를 편집 *-ConfigurationFilePath &lt;경로&gt;*  hello toohello 끝 `Register-AdfsAuthenticationProvider` 명령, 여기서  *&lt;경로&gt;*  hello toohello MultiFactorAuthenticationAdfsAdapter.config 파일 전체 경로입니다.

### <a name="configure-hello-web-service-sdk-with-a-username-and-password"></a>사용자 이름 및 암호를 사용 하 여 웹 서비스 SDK hello 구성
Hello 웹 서비스 SDK를 구성 하기 위한 방법은 두 가지가 있습니다. hello 먼저 사용자 이름 및 암호를 클라이언트 인증서를 사용 하는 hello 둘째는. Hello 첫 번째 옵션에 대해 다음이 단계를 수행 하거나 두 번째 hello에 대 한 바로 이동 합니다.  

1. 에 대 한 hello 값 설정 **WebServiceSdkUsername** hello PhoneFactor Admins 보안 그룹의 멤버인 tooan 계정. 사용 하 여 hello &lt;도메인&gt;&#92;&lt; 사용자 이름&gt; 형식입니다.  
2. 에 대 한 hello 값 설정 **WebServiceSdkPassword** toohello 적절 한 계정 암호입니다.

### <a name="configure-hello-web-service-sdk-with-a-client-certificate"></a>클라이언트 인증서를 사용 하 여 웹 서비스 SDK hello 구성
Toouse 사용자 이름 및 암호를 않으려는 경우 클라이언트 인증서를 사용 하는 이러한 단계 tooconfigure hello 웹 서비스 SDK를 따릅니다.

1. Hello 웹 서비스 SDK를 실행 하는 hello 서버에 대 한 인증 기관에서 클라이언트 인증서를 가져옵니다. 너무 방법에 대해 알아봅니다[클라이언트 인증서를 얻은](https://technet.microsoft.com/library/cc770328.aspx)합니다.  
2. 가져오기 hello 클라이언트 인증서 toohello 로컬 컴퓨터 개인 인증서 저장소에 hello 웹 서비스 SDK를 실행 하는 hello 서버입니다. 해당 hello 인증 기관의 공용 인증서가 신뢰할 수 있는 루트 인증서 인증서 저장소에 있는지 확인 합니다.  
3. Hello 클라이언트 인증서 tooa.pfx 파일의 hello 공개 및 개인 키를 내보냅니다.  
4. Hello Base64 형식 tooa.cer 파일에서 공개 키를 내보냅니다.  
5. 서버 관리자에서 해당 hello 웹 서버 (IIS) \Web Server\Security\IIS 클라이언트 인증서 매핑 인증 기능이 설치 된 것을 확인 합니다. 이 설치 되어 있지 않으면 선택 **역할 및 기능 추가** tooadd이이 기능입니다.  
6. IIS 관리자에서 두 번 클릭 **구성 편집기** hello 웹 서비스 SDK 가상 디렉터리를 포함 하는 hello 웹 사이트에 있습니다. Hello 가상 디렉터리가 아닌 중요 tooselect hello 웹 사이트입니다.  
7. Toohello 이동 **system.webServer/security/authentication/iisClientCertificateMappingAuthentication** 섹션.  
8. Set도 활성화**true**합니다.  
9. OneToOneCertificateMappingsEnabled를 너무 설정**true**합니다.  
10. Hello 클릭 **...**  다음 toooneToOneMappings 단추를 선택한 다음 hello 클릭 **추가** 링크 합니다.  
11. 앞에서 내보낸 hello Base64.cer 파일을 엽니다. *-----BEGIN CERTIFICATE-----*, *-----END CERTIFICATE-----* 및 줄바꿈을 제거합니다. Hello 결과 문자열을 복사 합니다.  
12. 집합 인증서 toohello hello 앞 단계에서에서 복사한 문자열입니다.  
13. Set도 활성화**true**합니다.  
14. Hello PhoneFactor Admins 보안 그룹의 구성원 인 사용자 이름 tooan 계정을 설정 합니다. 사용 하 여 hello &lt;도메인&gt;&#92;&lt; 사용자 이름&gt; 형식입니다.  
15. Hello 암호 toohello 적절 한 계정 암호를 설정 하 고 구성 편집기를 닫습니다.  
16. Hello 클릭 **적용** 링크 합니다.  
17. Hello 웹 서비스 SDK 가상 디렉터리를 두 번 클릭 **인증**합니다.  
18. ASP.NET 가장 및 기본 인증을 너무 설정 되어 있는지 확인**Enabled**, 다른 모든 항목이 너무 설정 되 고**비활성화**합니다.  
19. Hello 웹 서비스 SDK 가상 디렉터리를 두 번 클릭 **SSL 설정**합니다.  
20. 클라이언트 인증서를 너무 설정**Accept**, 클릭 하 고 **적용**합니다.  
21. 이전 버전의 toohello 서버 hello AD FS 어댑터를 실행 하는 내보낸 hello.pfx 파일을 복사 합니다.  
22. Hello.pfx 파일 toohello 로컬 컴퓨터 개인 인증서 저장소를 가져옵니다.  
23. 마우스 오른쪽 단추로 클릭 하 고 선택 **개인 키 관리**, 및 다음 grant 읽기 액세스 toohello 계정 toosign toohello AD FS 서비스에서 사용 합니다.  
24. Hello 클라이언트 인증서 및 복사 hello 지문을 hello에서 열고 **세부 정보** 탭 합니다.  
25. Hello MultiFactorAuthenticationAdfsAdapter.config 파일에서 설정 **WebServiceSdkCertificateThumbprint** toohello 문자열 hello 이전 단계에서 복사 합니다.  

마지막으로, tooregister hello 어댑터 hello \program 실행-PowerShell에서 단계 Authentication Server\register-multifactorauthenticationadfsadapter.ps1 스크립트입니다. hello 어댑터는 WindowsAzureMultiFactorAuthentication으로 등록 됩니다. Hello 등록 tootake 효과 대 한 hello AD FS 서비스를 다시 시작 합니다.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>AD FS를 사용하여 Azure AD 리소스 보안 유지
toosecure 클라우드 리소스에 있도록를 설정 클레임 규칙 2 단계 인증을 성공적으로 수행할 때 Active Directory Federation Services hello multipleauthn 클레임을 내보냅니다. 이 클레임 tooAzure AD에 전달 됩니다. 이 프로시저 toowalk hello 단계를 수행 합니다.

1. AD FS 관리를 엽니다.
2. Hello 왼쪽에서 선택 **신뢰 당사자 트러스트**합니다.
3. **Microsoft Office 365 ID 플랫폼**을 마우스 오른쪽 단추로 클릭하고 **클레임 규칙 편집...**을 선택합니다.

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. 발급 변환 규칙에서 **규칙 추가**를 클릭합니다.

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. 변환 클레임 규칙 추가 마법사 hello, 선택 **통과 또는 들어오는 클레임 필터링** 에서 드롭 다운 hello 및 **다음**합니다.

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. 규칙의 이름을 지정합니다.
7. 선택 **인증 방법 참조** 들어오는 hello로 클레임 유형입니다.
8. **모든 클레임 값 통과**를 선택합니다.
    ![변환 클레임 규칙 추가 마법사](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. **마침**을 클릭합니다. Hello AD FS 관리 콘솔을 닫습니다.

## <a name="related-topics"></a>관련된 항목
문제 해결 도움말을 참조 hello [Azure Multi-factor Authentication Faq](multi-factor-authentication-faq.md)
