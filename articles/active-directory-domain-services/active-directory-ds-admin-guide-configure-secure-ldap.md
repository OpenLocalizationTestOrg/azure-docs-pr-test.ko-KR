---
title: "Azure AD 도메인 서비스에서 LDAP (LDAPS) Secure aaaConfigure | Microsoft Docs"
description: "Azure AD 도메인 서비스 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Azure AD Domain Services 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성
이 문서에서는 Azure AD 도메인 서비스 관리되는 도메인에 대해 LDAPS(Secure Lightweight Directory Access Protocol)를 사용하도록 설정하는 방법을 보여 줍니다. 보안 LDAP는 'SSL(Secure Sockets Layer)/TLS(Transport Layer Security)를 통한 LDAP(Lightweight Directory Access Protocol)'라고도 합니다.

## <a name="before-you-begin"></a>시작하기 전에
이 문서에 나열 된 tooperform hello 작업 해야 합니다.

1. 유효한 **Azure 구독**.
2. **Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.
3. **Azure AD 도메인 서비스** hello Azure AD 디렉터리를 설정 해야 합니다. 그렇게 하지 않은 경우에 따라 hello에 설명 된 모든 hello 작업 [시작 가이드](active-directory-ds-getting-started.md)합니다.
4. A **인증서 사용 toobe tooenable 보안 LDAP**합니다.

   * **권장** - 신뢰할 수 있는 공용 인증 기관에서 인증서를 가져옵니다. 이 구성 옵션은 더 안전합니다.
   * 또는 선택할 수도 있습니다 너무[자체 서명 된 인증서를 만들](#task-1---obtain-a-certificate-for-secure-ldap) 이 문서의 뒷부분에 나와 있는 것 처럼 합니다.

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a>보안 LDAP 인증서 hello에 대 한 요구 사항
보안 LDAP를 사용 하기 전에 지침을 준수 하는 hello 당 유효한 인증서를 획득 합니다. Tooenable 시도 하면 오류가 발생 잘못/잘못 된 인증서로 관리 되는 도메인에 대 한 보안 LDAP 합니다.

1. **신뢰할 수 있는 발급자** -hello 인증서 보안 LDAP를 사용 하 여 toohello 관리 되는 도메인을 연결 하는 컴퓨터에서 신뢰할 수 없는 기관에서 발급 되어야 합니다. 이 기관은 이러한 컴퓨터에서 신뢰할 수 있는 공용 인증 기관일 수 있습니다.
2. **수명** -hello 인증서에 대해 유효 해야 합니다. 적어도 다음 3-6 개월 hello 합니다. 관리 되는 도메인 보안 LDAP 액세스 tooyour hello 인증서 만료 되 면 중단 되었습니다.
3. **주체 이름** -hello hello 인증서 주체 이름이 와일드 카드는 관리 되는 도메인 이어야 합니다. 예를 들어 도메인 이름이 'contoso100.com' 이면 hello 인증서의 주체 이름 이어야 합니다 ' *. contoso100.com'. Hello DNS 이름 (주체 대체 이름) toothis 와일드 카드 이름을 설정 합니다.
4. **키 사용** -hello 인증서를 구성 해야 다음 hello를 사용 하는-디지털 서명 및 키 암호화 합니다.
5. **인증서 용도** -hello 인증서를 SSL 서버 인증에 유효 해야 합니다.

> [!NOTE]
> **엔터프라이즈 인증 기관:** Azure AD Domain Services는 조직의 엔터프라이즈 인증 기관에서 발급한 보안 LDAP 인증서를 사용하도록 지원하지 않습니다. 이 제한은 hello 서비스 엔터프라이즈 루트 인증 기관으로 CA를 신뢰 하지 않기 때문입니다. 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a>작업 1 - 보안 LDAP를 위한 인증서 가져오기
첫 번째 작업 hello 보안 LDAP 액세스 toohello 관리 되는 도메인에 사용 되는 인증서를 받을 포함 됩니다. 다음 두 가지 옵션을 사용할 수 있습니다.

* 인증 기관에서 인증서를 받습니다. hello 기관 공용 인증 기관 될 수 있습니다.
* 자체 서명된 인증서를 만듭니다.

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a>옵션 A(권장) - 인증 기관에서 보안 LDAP 인증서를 가져옵니다.
조직이 공용 인증 기관에서 인증서를 입수 하는 경우 해당 공용 인증 기관에서 tooobtain hello 보안 LDAP 인증서가 필요 합니다.

설명한 모든 hello 요구 사항을 충족 하는지 확인 인증서를 요청할 때 [hello 보안 LDAP 인증서에 대 한 요구 사항을](#requirements-for-the-secure-ldap-certificate)합니다.

> [!NOTE]
> 보안 LDAP를 사용 하 여 tooconnect toohello 관리 되는 도메인을 필요로 하는 클라이언트 컴퓨터는 hello hello 보안 LDAP 인증서 발급자를 신뢰 해야 합니다.
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a>옵션 B - 보안 LDAP에 대한 자체 서명된 인증서 만들기
공용 인증 기관에서 인증서를 toouse 않으려는 경우 선택할 수 있습니다 toocreate 자체 서명 된 인증서 보안 LDAP에 대 한 합니다.

**PowerShell을 사용하여 자체 서명된 인증서 만들기**

Windows 컴퓨터에서으로 새 PowerShell 창을 열고 **관리자** 형식 hello toocreate 새 자체 서명 된 인증서를 명령에 따라 합니다.

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

앞 예제는 hello, 바꿉니다 '*. contoso100.com' 관리 되는 도메인의 hello DNS 도메인 이름으로 합니다. 'Contoso100.onmicrosoft.com' 이라는 관리 되는 도메인을 만든 경우 대체 하는 예를 들어 '*. contoso100.com' 스크립트를 위에 hello에 ' *. contoso100.onmicrosoft.com').

![Azure AD 디렉터리 선택](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

hello 새로 만든 자체 서명 된 인증서는 hello 로컬 컴퓨터 인증서 저장소에 배치 됩니다.


## <a name="next-step"></a>다음 단계
[작업 2-hello 보안 LDAP 인증서 tooa 내보냅니다. PFX 파일](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
