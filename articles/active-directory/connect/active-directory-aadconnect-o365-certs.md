---
title: "Office 365 및 Azure AD 사용자에 대 한 aaaCertificate 갱신 | Microsoft Docs"
description: "이 문서에서는 tooOffice 365 사용자가 인증서를 갱신 하는 방법에 대 한 알리는 전자 메일을 tooresolve 발급 하는 방법을 설명 합니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 543b7dc1-ccc9-407f-85a1-a9944c0ba1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b9b309e06949dc5488cd628650be413f366ed347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a>Office 365 및 Azure Active Directory에 대한 페더레이션 인증서 갱신
## <a name="overview"></a>개요
Azure Active Directory (Azure AD)와 Active Directory Federation Services (AD FS) 사이의 성공적인 페더레이션에 대 한 AD FS toosign 보안 토큰 tooAzure AD에서 사용 하는 hello 인증서는 Azure AD에 구성 된 일치 해야 합니다. 불일치는 toobroken 트러스트가 될 수 있습니다. 엑스트라넷에 액세스하기 위해 AD FS 및 웹 응용 프로그램 프록시를 배포하는 경우 Azure AD는 이 정보의 동기화를 유지합니다.

이 문서는 추가 정보 toomanage 토큰 서명 인증서를 제공 하 고 비활성화 hello에 Azure AD와 동기화 유지:

* Hello 웹 응용 프로그램 프록시를 배포 하지 않은 hello 페더레이션 메타 데이터 이므로 hello 엑스트라넷에서 사용할 수 없습니다.
* 토큰 서명 인증서에 대 한 AD FS의 기본 구성은 hello를 사용 하지 않는 합니다.
* 타사 ID 공급자를 사용하는 경우.

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a>토큰 서명 인증서에 대한 AD FS의 기본 구성
hello 토큰 서명 및 인증서의 암호를 해독 하는 토큰은 일반적으로 자체 서명된 된 인증서를 이며 1 년 동안 유효 합니다. 기본적으로 AD FS는 **AutoCertificateRollover**라는 자동 갱신 프로세스를 포함합니다. AD FS 2.0 이상을 사용하는 경우는 인증서가 만료되기 전에 Office 365 및 Azure AD에서 자동으로 인증서를 업데이트합니다.

### <a name="renewal-notification-from-hello-office-365-portal-or-an-email"></a>Hello Office 365 포털 또는 전자 메일에서 갱신 알림
> [!NOTE]
> 전자 메일 또는 포털 toorenew 묻는 알림을 받은 경우 사무실에 대 한 인증서 참조 [관리 tootoken 서명 인증서 변경](#managecerts) toocheck tootake 조치가 필요 합니다. Microsoft는 아무런 작업도 수행할 필요가 있는 경우에 전송 되는 인증서 갱신을 위해 toonotifications 시킬 수 있는 가능한 문제를 알고 있습니다.
>
>

Azure AD toomonitor hello 페더레이션 메타 데이터 및 업데이트 hello 토큰 서명 인증서를이 메타 데이터에 표시 된 대로 시도 합니다. 30 일 hello hello 토큰 서명 인증서가 만료 되기 전에 Azure AD hello 페더레이션 메타 데이터를 폴링하여 새 인증서를 사용할 수 있으면 확인 합니다.

* 성공적으로 hello 페더레이션 메타 데이터를 폴링할 하 고 hello 새 인증서를 검색할 수, 하는 경우 전자 메일 알림 또는 hello Office 365 포털에 경고 없음 toohello 사용자를 실행 됩니다.
* Hello 새 토큰 서명 인증서를 검색할 수 없는 경우 하거나 자동 인증서 롤오버를 사용 하지 않는 또는 hello 페더레이션 메타 데이터에 연결할 수 없기 때문에 Azure AD에서 발행 전자 메일 알림 및 hello Office 365 포털에 경고 합니다.

![Office 365 포털 알림](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> Tooensure 비즈니스 연속성을 AD FS를 사용 하는 경우에 서버 hello 알려진된 문제에 대 한 인증 실패가 발생 하지 않도록 있도록 업데이트 수행 되었는지 확인 하십시오. 이는 갱신 및 향후 갱신 기간에 대해 알려진 AD FS 프록시 서버 문제를 완화합니다.
>
> 서버 2012 R2 - [Windows Server 2014년 5월 롤업](http://support.microsoft.com/kb/2955164)
>
> Server 2008 R2 및 2012 - [Windows Server 2008 또는 Windows 2012 R2 SP1에서 프록시를 통한 인증 실패](http://support.microsoft.com/kb/3094446)
>
>

## Hello 인증서 업데이트 toobe 경우 확인<a name="managecerts"></a>
### <a name="step-1-check-hello-autocertificaterollover-state"></a>1 단계: hello AutoCertificateRollover 상태를 확인 합니다.
AD FS 서버에서 PowerShell을 엽니다. Hello AutoCertificateRollover 값 tooTrue 설정 되어 있는지 확인 합니다.

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
>AD FS 2.0을 사용하는 경우 Add-Pssnapin 먼저 Microsoft.Adfs.Powershell을 실행합니다.

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a>2단계: AD FS와 Azure AD가 동기화되었는지 확인
AD FS 서버의 hello Azure AD PowerShell 프롬프트를 열고 tooAzure AD 연결 합니다.

> [!NOTE]
> Azure AD PowerShell을 [여기](https://technet.microsoft.com/library/jj151815.aspx)에서 다운로드할 수 있습니다.
>
>

    Connect-MsolService

AD FS의에서 hello 인증서 구성 및 Azure AD 트러스트 속성 hello에 대 한 지정 된 도메인을 확인 합니다.

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

모두 hello 지문이 hello 출력 하는 경우 일치 하는 인증서가 Azure AD와 동기화 합니다.

### <a name="step-3-check-if-your-certificate-is-about-tooexpire"></a>3 단계: tooexpire에 대 한 인증서 인지 확인
Get-msolfederationproperty 또는 Get AdfsCertificate hello 출력에서 하지 이후"."에서 hello 날짜에 대 한 확인 Hello 날짜가 30 일 이내 자리를 비울 이면 작업을 수행 해야 합니다.

| AutoCertificateRollover | Azure AD와 동기화된 인증서 | 페더레이션 메타데이터는 공개적으로 액세스할 수 있습니다. | 유효성 검사 | 동작 |
|:---:|:---:|:---:|:---:|:---:|
| 예 |예 |예 |- |어떤 조치도 필요하지 않습니다. [자동으로 토큰 서명 인증서 갱신](#autorenew)을 참조하세요. |
| 예 |아니요 |- |15일 이내 |즉시 갱신합니다. [수동으로 토큰 서명 인증서 갱신](#manualrenew)을 참조하세요. |
| 아니요 |- |- |30일 이내 |즉시 갱신합니다. [수동으로 토큰 서명 인증서 갱신](#manualrenew)을 참조하세요. |

\[-] 중요하지 않습니다.

## Hello 토큰 서명 인증서를 자동으로 갱신 (권장)<a name="autorenew"></a>
필요 없음 tooperform는 수동으로 설치 hello 다음 모두 해당 하는 경우:

* Hello 엑스트라넷에서 액세스 toohello 페더레이션 메타 데이터를 사용할 수 있는 웹 응용 프로그램 프록시를 배포 했습니다.
* AD FS hello 기본 구성 (AutoCertificateRollover 사용)를 사용 하는 합니다.

다음 인증서 hello tooconfirm 검사 hello는 자동으로 업데이트할 수 있습니다.

**1. hello AD FS 속성 AutoCertificateRollover tooTrue 설정 되어야 합니다.** 이 새 토큰 서명 및 토큰 암호 해독 인증서 만료 된 hello 이전 하기 전에 AD FS 자동으로 생성 됩니다 나타냅니다.

**2. hello AD FS 페더레이션 메타 데이터는 공개적으로 액세스할 수 있습니다.** Toohello 이동 하 여 페더레이션 메타 데이터에 공개적으로 액세스할 수 있는지 확인 하십시오 (hello 회사 네트워크)에서 공용 인터넷 hello URL에는 컴퓨터에서 나오는에:

https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml

여기서 `(your_FS_name) `fs.contoso.com과 같이 조직을 사용 하는 hello 페더레이션 서비스 호스트 이름으로 대체 됩니다.  두 tooverify 수 있다면 이러한 설정에 성공적으로 없는 toodo 다른 항목이 있습니다.  

예: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

## Hello 토큰 서명 인증서를 수동으로 갱신<a name="manualrenew"></a>
선택할 수 있습니다 toorenew hello 토큰 서명 인증서 수동으로. 예를 들어 hello 다음과 같은 시나리오에 더 적합할 수 수동 갱신 합니다.

* 토큰 서명 인증서는 자체 서명된 인증서가 아닙니다. hello 가장 일반적인 이유는 조직의 AD FS 인증서는 조직의 인증 기관에서 등록을 관리 합니다.
* 네트워크 보안에는 hello 페더레이션 메타 데이터 toobe 공개적으로 사용할 수 없도록 합니다.

이러한 시나리오에서는 hello 토큰 서명 인증서를 업데이트할 때마다도 업데이트 해야 Office 365 도메인 Update-msolfederateddomain hello PowerShell 명령을 사용 하 여 합니다.

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a>1단계: AD FS에 새 토큰 서명 인증서가 있는지 확인
**기본이 아닌 구성**

AD FS의 기본 구성이 사용 하는 경우 (여기서 **AutoCertificateRollover** 너무 설정**False**), 사용자 지정 인증서 (자체 서명 되지 않았습니다)을 사용할 것입니다. 어떻게 toorenew hello AD FS 토큰 서명 인증서에 대 한 자세한 내용은 참조 [자체 서명 인증서를 AD FS를 사용 하지 않는 고객에 대 한 지침](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert)합니다.

**페더레이션 메타데이터를 공개적으로 사용할 수 없습니다.**

경우에 다른 손을 hello **AutoCertificateRollover** 너무 설정 되어**True**, 페더레이션 메타 데이터를 공개적으로 액세스할 수 없는 경우, 먼저 새 토큰 서명 인증서 AD에서 생성 하 고 있는지 확인 하지만 FS 합니다. 새 토큰 서명 인증서 라인 hello 단계를 수행 하 여 확인 합니다.

1. Toohello 기본 AD FS 서버에 로그온 했는지 확인 합니다.
2. PowerShell 명령 창을 열고 다음 명령을 hello를 실행 하 여 AD FS에서 hello 현재 서명 인증서를 확인 합니다.

    PS C:\>Get-ADFSCertificate –CertificateType token-signing

   > [!NOTE]
   > AD FS 2.0을 사용하는 경우 Add-Pssnapin Microsoft.Adfs.Powershell을 먼저 실행해야 합니다.
   >
   >
3. 나열 된 모든 인증서에 hello 명령 출력을 살펴봅니다. AD FS가 새 인증서를 생성 하는 경우에 hello 출력에 두 개의 인증서 표시 됩니다: 어떤 hello에 대 한 **IsPrimary** 값은 **True** 및 hello **NotAfter** 날짜는 개와 5 일 내 **IsPrimary** 은 **False** 및 **NotAfter** hello 나중에 1 년에 대 한 것입니다.
4. 만 인증서 1 개를 참조 하 고 hello **NotAfter** 날짜 5 일 이내는 toogenerate 새 인증서를 사용 해야 합니다.
5. 새 인증서를 toogenerate hello 다음 PowerShell 명령 프롬프트에서 명령을 실행: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`합니다.
6. 다음 명령을 다시 hello를 실행 하 여 hello 업데이트 확인: PS c:\>Get ADFSCertificate – CertificateType 토큰 서명

이제 두 개의 인증서 표시 됩니다, 그 중 하나에 **NotAfter** hello 미래에 어떤 hello에 대 한 약 1 년의 날짜 **IsPrimary** 값은 **False**합니다.

### <a name="step-2-update-hello-new-token-signing-certificates-for-hello-office-365-trust"></a>2 단계: hello 새 토큰 서명 인증서 hello Office 365 신뢰에 대 한 업데이트
Hello 새 토큰 서명 인증서 toobe 다음과 같이 hello 트러스트에 대 한 사용으로 Office 365를 업데이트 합니다.

1. Hello Microsoft Azure Active Directory 모듈에 대 한 Windows PowerShell을 엽니다.
2. $cred=Get-Credential을 실행합니다. 이 cmdlet에서 자격 증명을 물어보면 클라우드 서비스 관리자 계정 자격 증명을 입력합니다.
3. Connect-MsolService –Credential $cred를 실행합니다. 이 cmdlet toohello 클라우드 서비스를 연결합니다. Hello 도구를 통해 설치 하는 hello 추가 cmdlet을 실행 하기 전에 필요 toohello 클라우드 서비스에 연결 하는 컨텍스트를 만들어야 합니다.
4. AD FS hello 기본 페더레이션 서버가 아닌 컴퓨터에 이러한 명령은 실행 하는 경우 실행 Set-msoladfscontext-컴퓨터 <AD FS primary server>여기서 <AD FS primary server> hello hello 기본 AD FS 서버의 내부 FQDN 이름입니다. 이 cmdlet은 tooAD FS 연결 하는 컨텍스트를 만듭니다.
5. Update-MSOLFederatedDomain –DomainName <domain>을 실행합니다. 이 cmdlet hello 클라우드 서비스에 AD FS의 hello 설정을 업데이트 하 고 hello 2 간의 hello 트러스트 관계를 구성 합니다.

> [!NOTE]
> Hello를 사용 해야 toosupport contoso.com, fabrikam.com 등의 여러 최상위 도메인을 필요한 경우 **SupportMultipleDomain** 모든 cmdlet으로 전환 합니다. 자세한 내용은 [여러 최상위 도메인에 대한 지원](active-directory-aadconnect-multiple-domains.md)을 참조하세요.
>
>

## Azure AD Connect를 사용하여 Azure AD 트러스트 복구 <a name="connectrenew"></a>
Azure AD Connect를 사용 하 여 AD FS 팜 및 Azure AD 트러스트를 구성 하는 경우에 토큰 서명 인증서에 대 한 tootake 조치가 필요한 경우 Azure AD Connect toodetect를 사용할 수 있습니다. Toorenew hello 인증서 해야 할 경우 Azure AD Connect toodo를 지금 사용할 수 있습니다.

자세한 내용은 참조 [hello 신뢰 복구](active-directory-aadconnect-federation-management.md)합니다.
