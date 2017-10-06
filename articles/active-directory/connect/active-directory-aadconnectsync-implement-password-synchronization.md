---
title: "Azure AD Connect 동기화로 암호 동기화 aaaImplement | Microsoft Docs"
description: "에 대 한 정보를 제공 하 고 암호 동기화의 작동 방법 tooset를 구성 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 05f16c3e-9d23-45dc-afca-3d0fa9dbf501
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: a0401640f2a4d914419ee4446f923bb3a972389d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-password-synchronization-with-azure-ad-connect-sync"></a>Azure AD Connect 동기화를 사용하여 암호 동기화 구현
이 문서에서는 필요한 정보를 toosynchronize 온-프레미스 Active Directory 인스턴스 tooa 클라우드 기반 Azure Active Directory (Azure AD) 인스턴스에서 사용자 암호를 제공 합니다.

## <a name="what-is-password-synchronization"></a>암호 동기화란 무엇입니까?
확률 hello tooa 잊어버린 암호 인해 작업할 수 없도록 차단 되었는지와 관련 된 toohello 수 tooremember의 서로 다른 암호가 필요 합니다. hello 더 이상 암호 tooremember, hello 더 높은 hello 확률 tooforget 하나 필요 합니다. 질문 및 암호 재설정 필요 및 기타 암호 관련 문제에 대 한 호출에는 대부분의 기술 지원팀 리소스 hello 합니다.

암호 동기화는 온-프레미스 Active Directory 인스턴스 tooa 클라우드 기반 Azure AD 인스턴스에서 toosynchronize 사용자 암호를 사용 하는 기능입니다.
Office 365, Microsoft Intune, CRM Online 및 Azure Active Directory 도메인 서비스 (Azure AD DS)와 같은 tooAzure AD 서비스에서이 기능 toosign를 사용 합니다. Toohello 서비스에 로그인 할 hello를 사용 하 여 동일한 암호 toosign tooyour에서 사용 하 여 온-프레미스 Active Directory 인스턴스.

![Azure AD Connect의 정의](./media/active-directory-aadconnectsync-implement-password-synchronization/arch1.png)

사용자는 hello 암호 수를 줄여 toomaintain toojust 하나 있어야 합니다. 암호 동기화를 사용하면 다음을 수행하는 데 도움이 됩니다.

* 사용자의 hello 생산성을 향상 합니다.
* 지원 센터 비용 절감.  

또한 toouse 결정 한 경우 [Active Directory Federation Services (AD FS)와 페더레이션을](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect), AD FS 인프라 실패 하는 경우 필요에 따라 백업으로 암호 동기화를 설정할 수 있습니다.

암호 동기화에는 Azure AD Connect 동기화에 의해 구현 되는 확장 toohello 디렉터리 동기화 기능입니다. 사용자 환경에서 toouse 암호 동기화 해야합니다.

* Azure AD Connect 설치.  
* 온-프레미스 Active Directory 인스턴스 및 Azure Active Directory 인스턴스 간에 디렉터리 동기화 구성.
* 암호 동기화 사용.

자세한 내용은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)을 참조하세요.

> [!NOTE]
> FIPS 및 암호 동기화에 대해 구성된 Azure Active Directory Domain Services에 대한 자세한 내용은 문서 뒷부분에 나오는 "암호 동기화 및 FIPS"를 참조하세요.
>
>

## <a name="how-password-synchronization-works"></a>암호 동기화 작동 방법
hello Active Directory 도메인 서비스는 hello 형태의 hello 실제 사용자 암호의 해시 값 표시에 암호를 저장 합니다. 해시 값은 결과의 단방향 수학적 함수 (hello *해시 알고리즘*). 결과 없으며 메서드 toorevert hello 암호의 단방향 함수 toohello 일반 텍스트 버전입니다. 암호 해시 toosign tooyour 온-프레미스 네트워크를 사용할 수 없습니다.

사용자 암호 해시를 추출 하는 암호를 Azure AD Connect 동기화 toosynchronize hello 온-프레미스 Active Directory 인스턴스에 있습니다. 추가적인 보안 처리가 적용 되기 전에 toohello 암호 해시 동기화 toohello Azure Active Directory 인증 서비스입니다. 암호는 각 사용자 기본별로 동기화되고 시간 순서대로 동기화됩니다.

hello 암호 동기화 프로세스의 hello 실제 데이터 흐름은 DisplayName 또는 전자 메일 주소와 같은 사용자 데이터의 비슷한 toohello 동기화 합니다. 그러나 암호는 다른 특성에 대 한 hello 표준 디렉터리 동기화 기간 보다 더 자주 동기화 됩니다. hello 암호 동기화 프로세스에는 2 분 마다 실행 됩니다. 이 프로세스의 hello 빈도 수정할 수 없습니다. 암호를 동기화 하는 경우 기존 클라우드 암호를 hello 덮어씁니다.

hello hello 암호 동기화 기능을 설정 하면 처음으로 수행 범위에서 모든 사용자의 암호를 hello의 초기 동기화 합니다. 하위 집합만 원하는 toosynchronize 사용자 암호를 명시적으로 정의할 수 없습니다.

온-프레미스 암호를 변경 하면 업데이트 hello 암호가 동기화 됩니다, 가장 자주 몇 분 내에 있습니다.
hello 암호 동기화 기능은 실패 한 동기화 시도 자동으로 다시 시도합니다. 암호 시도 toosynchronize 하는 동안 오류가 발생할 때, 오류가 발생 하면 이벤트 뷰어에 기록 됩니다.

암호를 동기화 hello에 어떠한 영향도 미치지 hello 사용자가 현재 로그인입니다.
현재 클라우드 서비스 세션 tooa 클라우드 서비스에 로그인 하는 동안 발생 하는 동기화 된 암호 변경 하 여 즉시 적용 되지 않습니다. 그러나 클라우드 서비스 hello tooauthenticate 다시를 해야 하는 경우 필요한 tooprovide 새 암호입니다.

사용자는 두 번째 시간 tooauthenticate tooAzure AD tootheir 회사 네트워크에 로그인 하는 했는지 여부에 관계 없이 회사 자격 증명을 입력 해야 합니다. 그러나 이러한 패턴 최소화할 수 있습니다, hello 사용자가 로그인 시 (KMSI) 확인란에서 hello 로그인 유지를 선택 합니다. 이 확인란을 선택하면 짧은 기간 동안 인증을 우회하는 세션 쿠키가 설정됩니다. KMSI 동작을 사용 하도록 설정 또는 hello Azure AD 관리자가 설정을 해제할 수 있습니다.

> [!NOTE]
> 암호 동기화는 hello 개체 유형 Active Directory 사용자에에서 대해서만 지원 됩니다. Hello iNetOrgPerson 개체 유형에 대해 지원 되지 않습니다.

### <a name="detailed-description-of-how-password-synchronization-works"></a>암호 동기화가 작동하는 방법에 대한 자세한 설명
hello 다음 Active Directory와 Azure AD 간의 암호 동기화의 작동 방법을 자세하게 설명 합니다.

![자세한 암호 흐름](./media/active-directory-aadconnectsync-implement-password-synchronization/arch3.png)


1. 2 분 마다 hello 암호 동기화 에이전트 hello AD 연결 서버에 저장 된 암호 해시 (hello unicodePwd 특성) 표준 hello 통해 DC에서 요청 [MS DRSR](https://msdn.microsoft.com/library/cc228086.aspx) 사용 되는 toosynchronize 데이터 복제 프로토콜 Dc 간. 디렉터리 변경 내용 복제 및 복제 디렉터리 변경 내용이 모든 AD 사용 권한 (설치에 기본적으로 부여) tooobtain hello 암호 해시 hello 서비스 계정이 있어야 합니다.
2. 키를 사용 하 여 hello DC 암호화 hello MD4 암호 해시를 보내기 전에 [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) 솔트 및 hello RPC 세션 키의 해시입니다. 그런 다음 hello 결과 toohello 암호 동기화 에이전트를 RPC를 통해 보냅니다. hello DC도 hello 솔트 toohello 동기화 에이전트가 사용 하 여 전달 hello DC 복제 프로토콜 hello 에이전트 수 toodecrypt hello 봉투 (envelope) 되도록 합니다.
3.  사용 하 여 hello 암호 동기화 에이전트에 hello 암호화 된 봉투 (envelope)를 만든 후 [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx) 솔트 toogenerate 키 toodecrypt hello 받은 데이터 백 tooits 원래 MD4 형식을 hello 및 합니다. 없습니다 hello 암호 동기화 에이전트에는 액세스 toohello 일반 텍스트 암호. hello m d 5의 암호 동기화 에이전트의 사용은 엄격 하 게 hello DC로 복제 프로토콜 호환성에 대 한 및 온-프레미스 DC hello 사이의 hello 암호 동기화 에이전트에만 사용 됩니다.
4.  hello 암호 동기화 에이전트 u t F-16으로 인코딩된 이진에 다시이 문자열 변환 후 첫 번째 변환 하는 동안 hello 해시 tooa 32 바이트 16 진수 문자열 hello 16 바이트 이진 암호 해시 too64 바이트를 확장 합니다.
5.  hello 암호 동기화 에이전트가 솔트 10 바이트 길이 솔트로 구성 된 추가 하 고, toohello 64 바이트의 이진 toofurther hello 원래 해시 보호 합니다.
6.  hello 암호 동기화 에이전트에서 다음 hello MD4 해시 및 솔트를 결합 하 고 hello로 입력 [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) 함수입니다. hello의 1000 회 반복 [hmac-sha256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) 키 지정된 해시 알고리즘을 사용 합니다. 
7.  hello 암호 동기화 에이전트 hello 결과 32 바이트 해시는, 두 hello 솔트를 연결 (사용 하기 위해 Azure AD 통해), s h a 256 반복 tooit 수가 hello 힙이고 hello 문자열에서 SSL 통해 Azure AD Connect tooAzure 광고를 전송 합니다.</br> 
8.  Hello를 통해 실행 사용자 toosign tooAzure AD에서에서 시도 하 고 해당 암호, hello 암호를 입력 합니다. 동일한 MD4 + 솔트 + PBKDF2 + hmac-sha256 프로세스입니다. Azure AD에 저장 하는 hello 해시 일치 하는 hello 결과 해시 hello 사용자가 hello 올바른 암호를 입력 하 고 인증 됩니다. 

>[!Note] 
>hello 원래 MD4 해시 전송 된 tooAzure AD 않습니다. 대신, hello hello 원래 MD4 해시의 경우 SHA256 해시는 전송 됩니다. 결과적으로, Azure AD에 저장 하는 hello 해시를 가져올 경우 온-프레미스-pass-the-hash 공격에서 사용할 수 없습니다.

### <a name="how-password-synchronization-works-with-azure-active-directory-domain-services"></a>암호 동기화가 Azure Active Directory Domain Services와 작동하는 방식
또한도 사용할 수 있습니다 hello 암호 동기화 기능 toosynchronize 온-프레미스 암호[Azure Active Directory 도메인 서비스](../../active-directory-domain-services/active-directory-ds-overview.md)합니다. 이 시나리오에서는 hello Azure Active Directory 도메인 서비스 인스턴스는 온-프레미스 Active Directory 인스턴스에서 사용할 수 있는 모든 hello 방법 hello 클라우드에서 사용자를 인증합니다. 이 시나리오의 hello 경험은 온-프레미스 환경에서 비슷한 toousing hello Active Directory 마이그레이션 도구 (ADMT)입니다.

### <a name="security-considerations"></a>보안 고려 사항
암호를 동기화 할 때 hello 일반 텍스트 암호 버전이 노출된 toohello 암호 동기화 기능, AD, tooAzure 또는 hello 연결 된 서비스입니다.

사용자 인증에는 Azure AD에 대해 아닌 hello 회사의 Active Directory 인스턴스에 대해 수행이 됩니다. 조직에 hello 프레미스-Azure AD에 저장 하는 s h a 256 암호 데이터는 hello hello 팩트를 고려 하십시오 두면 부분도 암호 데이터에 대 한 질문이 있는 경우 hello 원래 MD4 해시-의 해시는 Active Directory에 저장 된 것 보다 훨씬 더 안전 합니다. 또한이 SHA256 해시를 해독할 수 없거나 때문에 및 수 없습니다 돌아가지 toohello 조직의 Active Directory 환경으로-pass-the-hash 공격에서 유효한 사용자 암호를 제공 합니다.





### <a name="password-policy-considerations"></a>암호 정책 고려 사항
암호 동기화를 사용하여 영향을 받는 두 가지 정책이 있습니다.

* 암호 복잡성 정책
* 암호 만료 정책

#### <a name="password-complexity-policy"></a>암호 복잡성 정책  
암호 동기화를 설정 온-프레미스 Active Directory 인스턴스에서 hello 암호 복잡도 정책이 동기화 된 사용자에 대 한 hello 클라우드에서 복잡도 정책을 재정의 합니다. Hello 유효한 암호의 모든 온-프레미스 Active Directory 인스턴스 tooaccess Azure AD 서비스에서에서 사용할 수 있습니다.

> [!NOTE]
> Hello 클라우드에서 직접 만든 사용자의 암호는 hello 클라우드에 정의 된 주체 toopassword 정책.

#### <a name="password-expiration-policy"></a>암호 만료 정책  
Hello 클라우드 계정 암호를 너무 설정 되어 사용자의 암호 동기화 hello 범위에 있으면*만료 되지 않도록*합니다.

온-프레미스 환경에서 만료 된 동기화 된 암호를 사용 하 여 toosign tooyour 클라우드 서비스에 계속할 수 있습니다. 클라우드 암호를 업데이트할 hello 다음 번 hello 온-프레미스 환경에서 hello 암호를 변경 합니다.

#### <a name="account-expiration"></a>계정 만료
조직 hello 계정 만료 특성을 사용 하 여 사용자 계정 관리의 일환으로, 경우에이 특성은 동기화 된 tooAzure AD 없습니다 주의 해야 합니다. 결과적으로 암호 동기화를 위해 구성된 환경의 만료된 Active Directory 계정은 Azure AD에서 계속 활성 상태입니다. Hello 계정 만료 되 면 워크플로 동작 해야 hello 사용자의 Azure AD 계정을 사용 하지 않도록 설정 하는 PowerShell 스크립트를 트리거하는 것이 좋습니다. 반대로, hello 계정 상태에서 hello Azure AD 인스턴스를 설정 해야 합니다.

### <a name="overwrite-synchronized-passwords"></a>동기화된 암호 덮어쓰기
관리자는 Windows PowerShell을 사용하여 사용자 암호를 수동으로 재설정할 수 있습니다.

이 경우 hello 새 암호 동기화 된 암호를 재정의 하 고 hello 클라우드에 정의 된 모든 암호 정책이 적용된 toohello 새 암호는.

Hello 새 암호를 다시 온-프레미스 암호를 변경한 경우 toohello 클라우드를 동기화 하 고 수동으로 업데이트 하는 hello 암호를 재정의 합니다.

암호의 hello 동기화에 어떠한 영향도 미치지 hello Azure 사용자가 로그인 합니다. 현재 클라우드 서비스 세션 tooa 클라우드 서비스에 로그인 하는 동안 발생 하는 동기화 된 암호 변경 하 여 즉시 적용 되지 않습니다. KMSI는 hello 기간 동안 이러한 차이 확장합니다. 클라우드 서비스 hello tooauthenticate 다시를 해야 하는 경우 새 암호 tooprovide 할 수 있습니다.

### <a name="additional-advantages"></a>추가적인 이점

- 일반적으로 암호 동기화는 페더레이션 서비스 보다 더 간단 tooimplement입니다. 서버를 추가로 필요 하지 않습니다 하 고 항상 사용 가능한 페더레이션 서비스 tooauthenticate 사용자에 대 한 종속성을 제거 합니다. 
- 또한 toofederation에서 암호 동기화를 설정할 수도 있습니다. 페더레이션 서비스에 중단이 발생하는 경우 대체 서비스로 사용될 수 있습니다.












## <a name="enable-password-synchronization"></a>암호 동기화 사용
Hello를 사용 하 여 Azure AD Connect를 설치 하면 **Express 설정을** 암호 동기화 옵션을 자동으로 설정 됩니다. 자세한 내용은 [기본 설정을 사용하여 Azure AD Connect 시작](active-directory-aadconnect-get-started-express.md)을 참조하세요.

Azure AD Connect를 설치 하면 사용자 지정 설정을 사용 하면 암호 동기화는 hello 사용자 로그인 페이지에서 사용할 수 있습니다. 자세한 내용은 [Azure AD Connect의 사용자 지정 설치](active-directory-aadconnect-get-started-custom.md)를 참조하세요.

![암호 동기화를 사용하도록 설정](./media/active-directory-aadconnectsync-implement-password-synchronization/usersignin.png)

### <a name="password-synchronization-and-fips"></a>암호 동기화 및 FIPS
서버에 잠겨 있기 때문 tooFederal FIPS Information Processing Standard ()에 따라, MD5 사용 되지 않습니다.

**암호 동기화에 대 한 MD5 tooenable hello 다음 단계를 수행 합니다.**

1. Too%programfiles%\Azure AD Sync\Bin 이동 합니다.
2. miiserver.exe.config를 엽니다.
3. Hello hello 파일 끝에 toohello configuration/runtime 노드로 이동 하십시오.
4. 노드 다음에 오는 hello를 추가 합니다.`<enforceFIPSPolicy enabled="false"/>`
5. 변경 내용을 저장합니다.

참조용으로 다음 조각처럼 보여야 합니다.

```
    <configuration>
        <runtime>
            <enforceFIPSPolicy enabled="false"/>
        </runtime>
    </configuration>
```

보안 및 FIPS에 대한 자세한 내용은 [AAD 암호 동기화, 암호화 및 FIPS 준수](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/)를 참조하세요.

## <a name="troubleshoot-password-synchronization"></a>암호 동기화 문제 해결
암호 동기화에 문제가 있으면 [암호 동기화 문제 해결](active-directory-aadconnectsync-troubleshoot-password-synchronization.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [Azure AD Connect 동기화: 사용자 지정 동기화 옵션](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
