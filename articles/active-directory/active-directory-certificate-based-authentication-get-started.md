---
title: "Active Directory 인증서 기반 인증-aaaAzure 시작 | Microsoft Docs"
description: "자세한 내용은 방법 tooconfigure 사용자 환경에서 인증서 기반 인증"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a>Azure Active Directory에서 인증서 기반 인증 시작

인증서 기반 인증을 사용 하려면 Exchange online 계정을 연결할 때 Windows, Android 또는 iOS 장치에 클라이언트 인증서와 함께 Azure Active Directory에 의해 인증 toobe가 있습니다. 

- Microsoft Outlook 및 Microsoft Word와 같은 Office 모바일 응용 프로그램   

- EAS(Exchange ActiveSync) 클라이언트 

Hello 필요 tooenter 사용자 이름 및 암호 조합을 특정 메일 및 모바일 장치에서 Microsoft Office 응용 프로그램에이 기능을 구성을 제거 합니다. 

항목 내용:

- 미국 정부 계획 및 tooconfigure 단계 hello로 하 고 Office 365 Enterprise, Business, 교육, 테 넌 트의 사용자에 대 한 인증서 기반 인증을 이용 제공 합니다. 이 기능은 Office 365 중국, 미국 국방부 및 연방 정부 계획에서 미리 보기 상태로 제공됩니다. 

- [PKI(공개 키 인프라)](https://go.microsoft.com/fwlink/?linkid=841737) 및 [AD FS](connect/active-directory-aadconnectfed-whatis.md)가 이미 구성되어 있다고 가정합니다.    


## <a name="requirements"></a>요구 사항

인증서 기반 인증 tooconfigure hello 다음 사항을 충족 해야 합니다.  

- CBA(인증서 기반 인증)는 최신 인증(ADAL)을 사용하는 브라우저 응용 프로그램 또는 네이티브 클라이언트의 페더레이션 환경에서만 지원됩니다. Exchange Active Sync (EAS) 모두, 페더레이션 및 관리 되는 계정에 대해 사용할 수 있는 EXO에 대 한는 hello 예외가입니다. 

- hello 루트 인증 기관 및 중간 인증 기관을 Azure Active Directory에서 구성 되어야 합니다.  

- 각 인증 기관에는 인터넷 연결 URL을 통해 참조될 수 있는 CRL(인증서 해지 목록)이 있어야 합니다.  

- Azure Active Directory에 해당 인증 기관이 하나 이상 구성되어 있어야 합니다. Hello에 관련된 단계를 확인할 수 있습니다 [hello 인증 기관 구성](#step-2-configure-the-certificate-authorities) 섹션.  

- Exchange ActiveSync 클라이언트에 대 한 클라이언트 인증서 hello hello 사용자 라우팅할 수 있는 전자 메일 hello hello 주체 대체 이름 필드의 RFC822 이름 값 또는 hello 사용자 이름 중 하나를 온라인 Exchange 주소가 있어야 합니다. Azure Active Directory hello 디렉터리의 hello RFC822 값 toohello 프록시 주소 특성을 매핑합니다.  

- 클라이언트 장치에 클라이언트 인증서를 발급 하는 액세스 tooat 중 하나 이상이 인증 기관이 있어야 합니다.  

- 클라이언트 인증용 클라이언트 인증서가 발행 되어 있어야 tooyour 클라이언트입니다.  




## <a name="step-1-select-your-device-platform"></a>1단계: 장치 플랫폼 선택

첫 번째 단계로, 조사 하려는 hello 장치 플랫폼에 대 한 필요 tooreview hello 다음 합니다.

- hello Office 모바일 응용 프로그램 지원 
- hello 특정 구현 요구 사항  

hello 관련 hello 다음 장치 플랫폼에 대 한 정보가 있습니다.

- [Android](active-directory-certificate-based-authentication-android.md)
- [iOS](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a>2 단계: hello 인증 기관 구성 

tooconfigure 각 인증 기관에 대 한 Azure Active Directory에서 인증 기관에 따라 hello를 업로드 합니다. 

* hello 인증서의 공개 부분에 hello *.cer* 형식 
* hello 여기서 hello 인터넷 Url 인증서 해지 목록 (Crl) 상주

인증 기관에 대 한 hello 스키마 모양은 다음과 같습니다. 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

Hello 구성에 대 한 hello를 사용할 수 있습니다 [Azure Active Directory PowerShell 버전 2](/powershell/azure/install-adv2?view=azureadps-2.0):  

1. 관리자 권한으로 Windows PowerShell을 시작합니다. 
2. Hello Azure AD 모듈을 설치 합니다. 버전 tooinstall 필요한 [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) 이상.  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

첫 번째 구성 단계로 테 넌 트와 연결 tooestablish 필요. 연결 tooyour 테 넌 트 존재 하는 즉시 있습니다 수 검토, 추가, 삭제 및 수정 디렉터리에 정의 된 hello 신뢰할 수 있는 인증 기관입니다. 

### <a name="connect"></a>연결

테 넌 트를 사용 하 여 hello와의 연결을 tooestablish [연결-azure Ad](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:

    Connect-AzureAD 


### <a name="retrieve"></a>장치 

hello를 사용 하는 디렉터리에 정의 된 tooretrieve hello 신뢰할 수 있는 인증 기관 [Get AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet. 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a>추가

신뢰할 수 있는 인증 기관 toocreate hello를 사용 하 여 [새로 AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet 및 집합 hello **crlDistributionPoint** 특성 tooa 올바른 값: 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a>제거

신뢰할 수 있는 인증 기관 tooremove hello를 사용 하 여 [제거 AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a>수정

신뢰할 수 있는 인증 기관 toomodify hello를 사용 하 여 [집합 AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a>3단계: 해지 구성

Azure Active Directory 클라이언트 인증서를 toorevoke hello 인증서 해지 목록 (CRL) hello Url에서 인증 기관 정보의 일부로 업로드 하 고 캐시를 인출 합니다. hello 타임 스탬프를 마지막 게시 (**발효일** 속성)에 CRL이 사용 하는 hello tooensure hello CRL 여전히 유효 합니다. hello CRL hello 목록의 일부인 주기적으로 참조 된 toorevoke 액세스 toocertificates입니다.

더 즉각적인 해지 (예: 사용자가 장치를 잃어버린 경우) 필요한 경우 hello 사용자의 권한 부여 토큰 hello 무효화 될 수 있습니다. tooinvalidate hello 권한 부여 토큰으로 설정 hello **StsRefreshTokenValidFrom** Windows PowerShell을 사용 하 여이 특정 사용자에 대 한 필드입니다. Hello를 업데이트 해야 **StsRefreshTokenValidFrom** toorevoke 액세스할 각 사용자에 대 한 필드입니다.

hello 해지 유지 하는 tooensure, hello 설정 해야 **발효일** hello 값을 설정한 후 hello CRL tooa 날짜의 **StsRefreshTokenValidFrom** 문제의 hello 인증서가 확인 하 고 CRL 번호입니다.

업데이트 및 hello 설정 하 여 hello 권한 부여 토큰이 무효화를 위한 단계 개요 hello 프로세스 hello **StsRefreshTokenValidFrom** 필드입니다. 

**tooconfigure 해지 합니다.** 

1. 관리자 자격 증명 toohello MSOL 서비스와 연결 합니다. 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. 사용자에 대 한 hello 현재 StsRefreshTokensValidFrom 값을 검색 합니다. 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. Hello 사용자 같은 toohello 현재 타임 스탬프에 대 한 새 StsRefreshTokensValidFrom 값을 구성 합니다. 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

설정한 hello 날짜 이후 hello에 있어야 합니다. Hello 날짜 이후 hello에 없는 경우 hello **StsRefreshTokensValidFrom** 속성이 설정 되지 않았습니다. Hello 날짜 hello 미래에 있으면 **StsRefreshTokensValidFrom** toohello 현재 시간 (hello 날짜가 아닌 Set-msoluser 명령으로 지정) 설정 되어 있습니다. 


## <a name="step-4-test-your-configuration"></a>4단계: 구성 테스트

### <a name="testing-your-certificate"></a>인증서 테스트

첫 번째 구성 테스트를 시도해 야 toosign에 너무[Outlook Web Access](https://outlook.office365.com) 또는 [SharePoint Online](https://microsoft.sharepoint.com) 를 사용 하 여 **장치에서 브라우저**합니다.

로그인에 성공했으면 다음을 의미합니다.

- hello 사용자 인증서를 프로 비전 된 tooyour 테스트 장치 되었습니다.
- AD FS가 올바르게 구성되었습니다.  


### <a name="testing-office-mobile-applications"></a>Office 모바일 응용 프로그램 테스트

**모바일 Office 응용 프로그램에서 인증서 기반 인증 tootest:** 

1. 테스트 장치에서 Office 모바일 응용 프로그램(예: OneDrive)을 설치합니다.
3. Hello 응용 프로그램을 시작 합니다. 
4. 사용자 이름을 입력 하 고 원하는 toouse hello 사용자 인증서를 선택 합니다. 

정상적으로 로그인되어야 합니다. 

### <a name="testing-exchange-activesync-client-applications"></a>Exchange ActiveSync 클라이언트 응용 프로그램 테스트

인증서 기반 인증 일 경우 hello 클라이언트 인증서를 포함 하는 EAS 프로필을 통해 tooaccess EAS (Exchange ActiveSync) 사용 가능한 toohello 응용 프로그램 이어야 합니다. 

hello EAS 프로필 hello 다음 정보를 포함 해야 합니다.

- 인증에 사용 되는 사용자 인증서 toobe hello 

- hello EAS 끝점 (예를 들어 outlook.office365.com)

EAS 프로필을 구성 하 고 모바일 장치 관리 (MDM) 또는 hello hello 장치에 대 한 EAS 프로필에에서 hello 인증서를 수동으로 배치 하 여 Intune 등의 hello 사용률을 통해 hello 장치에 배치할 수 있습니다.  

### <a name="testing-eas-client-applications-on-android"></a>Android에서 EAS 클라이언트 응용 프로그램 테스트

**tootest 인증서 인증:**  

1. 위의 hello 요구 사항을 충족 하는 hello 응용 프로그램에서 EAS 프로필을 구성 합니다.  
2. Hello 응용 프로그램을 열고 메일 동기화를 확인 합니다. 

