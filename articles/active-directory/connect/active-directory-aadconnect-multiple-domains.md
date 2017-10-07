---
title: "여러 도메인 aaaAzure AD 연결"
description: "이 문서에는 O365 및 Azure AD를 사용하여 여러 최상위 도메인을 설정하고 구성하는 방법이 설명되어 있습니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a>Azure AD로 페더레이션에 대한 여러 도메인 지원
hello 다음 문서는 방법을 제공 toouse 여러 최상위 도메인 및 하위 도메인을 Office 365 또는 Azure AD 도메인을 페더레이션 하는 경우.

## <a name="multiple-top-level-domain-support"></a>여러 최상위 도메인 지원
Azure AD로 여러 최상위 도메인을 페더레이션하려면 하나의 최상위 도메인으로 페더레이션하는 경우 필요하지 않은 몇 가지 추가 구성이 필요합니다.

도메인은 Azure AD와 페더레이션 하는 경우 Azure의 hello 도메인에 여러 속성이 설정 됩니다.  중요한 한가지 속성은 IssuerUri입니다.  이 사용 되는 URI는 토큰 hello hello 도메인으로 Azure AD tooidentify와 연결 됩니다.  hello URI tooresolve tooanything 필요 하지 않습니다 되지만 유효한 URI 여야 합니다.  기본적으로 Azure AD이 값을 설정 toohello hello 페더레이션 서비스 식별자의 온-프레미스에서 AD FS 구성 합니다.

> [!NOTE]
> hello 페더레이션 서비스 식별자는 페더레이션 서비스를 고유 하 게 식별 하는 URI입니다.  hello 페더레이션 서비스는 hello 보안 토큰 서비스와 AD FS에서 작동 하의 인스턴스입니다. 
> 
> 

Hello PowerShell 명령을 사용 하 여 자세한 IssuerUri 수 `Get-MsolDomainFederationSettings -DomainName <your domain>`합니다.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

문제에는 여러 개의 최상위 도메인 tooadd 원하는 경우 발생 합니다.  예를 들어 Azure AD와 온-프레미스 환경 간 페더레이션을 설정했다고 가정합니다.  이 문서의 경우 bmcontoso.com을 사용합니다.  두 번째 최상위 도메인 bmfabrikam.com을 추가했습니다.

![도메인](./media/active-directory-multiple-domains/domains.png)

회원님께 우리의 bmfabrikam.com 도메인 toobe 페더레이션 tooconvert 때에서는 오류가 발생 합니다.  hello 이유는 Azure AD에 hello IssuerUri 속성 toohave hello 같은 둘 이상의 도메인에 대 한 값을 허용 하지 않는 제약 조건이 있습니다.  

![페더레이션 오류](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a>SupportMultipleDomain 매개 변수
tooworkaround이 tooadd hello를 사용 하 여 변환을 수행할 수 있는 다른 IssuerUri 필요 `-SupportMultipleDomain` 매개 변수입니다.  이 매개 변수는 cmdlet을 다음 hello로 사용 됩니다.

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

이 매개 변수는 hello 도메인의 hello 이름에 따라이 있도록 IssuerUri hello를 구성 하는 Azure AD를 만듭니다.  Azure AD의 디렉터리에서 고유합니다.  Hello 매개 변수를 사용 하 여 hello PowerShell 명령 toocomplete를 성공적으로 수 있습니다.

![페더레이션 오류](./media/active-directory-multiple-domains/convert.png)

새 bmfabrikam.com 도메인의 hello 설정을 있습니다 보고 hello 다음을 확인할 수 있습니다.

![페더레이션 오류](./media/active-directory-multiple-domains/settings.png)

`-SupportMultipleDomain` hello 바뀌지 않으면 있는 다른 끝점 adfs.bmcontoso.com에서 여전히 toopoint tooour 페더레이션 서비스를 구성 합니다.

또 다른 주의 사항은 `-SupportMultipleDomain` 않습니다는 hello AD FS 시스템에 Azure AD에 대 한 발급 된 토큰에서 적절 한 발급자 값 hello 포함 되도록 보장 됩니다. 이렇게 하기 hello 사용자 UPN hello 도메인 부분을 가져오고이 hello IssuerUri, 즉, https://{upn 접미사의에서 hello 도메인으로 설정 하 여} / adfs/services/신뢰 합니다. 

따라서 인증 tooAzure AD 또는 Office 365 중 hello IssuerUri hello 사용자의 토큰 요소가 사용 되는 toolocate hello 도메인 Azure AD에서 합니다.  일치 하는 항목이 없는 경우 hello 인증이 실패 합니다. 

예를 들어 사용자의 UPN를 bsimon@bmcontoso.com, toohttp://bmcontoso.com/adfs/services/trust hello IssuerUri 요소 hello 토큰 AD FS 문제에 설정 됩니다. Hello Azure AD 구성 일치시킬지 및 인증에 실패 합니다.

hello 다음은이 논리를 구현 하는 hello 사용자 지정된 클레임 규칙:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> 순서 toouse hello-SupportMultipleDomain 새 tooadd 시도할 때 전환 하거나 이미 변환 추가 도메인, toohave 해야 페더레이션된 트러스트 toosupport 설정으로 원래 합니다.  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a>AD FS와 Azure AD 간의 tooupdate hello 신뢰 하는 방법
Toore 해야 AD FS와 Azure AD의 사용자 인스턴스 간의 hello 페더레이션 트러스트를 설정 하지 않았을 경우-이 트러스트를 만들어야 합니다.  되었을 때 원래 hello 없이 설정 때문에 이것이 `-SupportMultipleDomain` 매개 변수를 hello IssuerUri hello 기본 값으로 설정 됩니다.  Hello에서 아래 스크린샷 hello IssuerUri toohttps://adfs.bmcontoso.com/adfs/services/trust 설정 되어 볼 수 있습니다.

이제 hello Azure AD 포털에서 새 도메인을 성공적으로 추가 하 고 다음 tooconvert를 시도 하는 경우 사용 하 여 `Convert-MsolDomaintoFederated -DomainName <your domain>`를 얻을 수 있는 hello 다음 오류가 있습니다.

![페더레이션 오류](./media/active-directory-multiple-domains/trust1.png)

Tooadd hello를 시도 하면 `-SupportMultipleDomain` 스위치 hello 다음 오류가 수신 됩니다.

![페더레이션 오류](./media/active-directory-multiple-domains/trust2.png)

Toorun 할지를 `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` hello에 원래 도메인에서 오류가 발생도 합니다.

![페더레이션 오류](./media/active-directory-multiple-domains/trust3.png)

Tooadd 추가 최상위 도메인 아래 hello 단계를 사용 합니다.  이미 도메인을 추가 하 고 hello를 사용 하지 않은 경우 `-SupportMultipleDomain` 매개 변수 제거 하 고 원래 도메인을 업데이트 하기 위한 hello 단계부터 수행 합니다.  최상위 도메인을 추가 하지 않은 경우 PowerShell의 Azure AD Connect를 사용 하 여 도메인을 추가 하는 단계 hello로 시작할 수 아직.

다음 단계 tooremove hello Microsoft Online 신뢰 hello를 사용 하 고 원래 도메인을 업데이트 합니다.

1. AD FS 페더레이션 서버에서 **AD FS 관리** 
2. Hello 왼쪽의 확장 **트러스트 관계** 및 **신뢰 당사자 트러스트**
3. 오른쪽 hello에서 삭제 hello **Microsoft Office 365 Id 플랫폼** 항목입니다.
   ![Microsoft 온라인 제거](./media/active-directory-multiple-domains/trust4.png)
4. 가 있는 컴퓨터에서 [Azure Active Directory에 대 한 Windows PowerShell 모듈](https://msdn.microsoft.com/library/azure/jj151815.aspx) 설치 hello 다음 실행: `$cred=Get-Credential`합니다.  
5. Hello Azure AD 도메인을 페더레이션 하는 hello 사용자 이름 및 전역 관리자의 암호를 입력 합니다.
6. PowerShell에서 `Connect-MsolService -Credential $cred`
7. PowerShell에서 `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`을(를) 입력합니다.  이 hello 원래 도메인입니다.  따라서 hello를 사용 하 여는 것이 도메인 위에:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`

다음 단계 tooadd hello 새 최상위 도메인 PowerShell을 사용 하 여 hello를 사용 하 여

1. 가 있는 컴퓨터에서 [Azure Active Directory에 대 한 Windows PowerShell 모듈](https://msdn.microsoft.com/library/azure/jj151815.aspx) 설치 hello 다음 실행: `$cred=Get-Credential`합니다.  
2. Hello Azure AD 도메인을 페더레이션 하는 hello 사용자 이름 및 전역 관리자의 암호를 입력 합니다.
3. PowerShell에서 `Connect-MsolService -Credential $cred`
4. PowerShell에서 `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`

다음 단계 tooadd hello 새 최상위 도메인 Azure AD Connect를 사용 하 여 hello를 사용 합니다.

1. 시작 메뉴 또는 hello 바탕 화면에서 Azure AD Connect 시작
2. "추가 Azure AD 도메인 추가" 선택 ![추가 Azure AD 도메인 추가](./media/active-directory-multiple-domains/add1.png)
3. Azure AD 및 Active Directory 자격 증명 입력
4. 페더레이션에 대 한 tooconfigure 원하는 hello 두 번째 도메인을 선택 합니다.
   ![추가 Azure AD 도메인 추가](./media/active-directory-multiple-domains/add2.png)
5. 설치 클릭

### <a name="verify-hello-new-top-level-domain"></a>Hello 새 최상위 도메인 확인
Hello PowerShell 명령을 사용 하 여 `Get-MsolDomainFederationSettings -DomainName <your domain>`볼 수 있습니다 hello IssuerUri를 업데이트 합니다.  hello 아래 스크린샷은 우리의 원래 도메인 http://bmcontoso.com/adfs/services/trust에 업데이트 된 hello 페더레이션 설정

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

새 도메인에서 IssuerUri hello toohttps://bmfabrikam.com/adfs/services/trust 설정 되었는지

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a>하위 도메인에 대한 지원
하위 도메인을 추가 하면 hello 인해 방식으로 Azure AD 처리 도메인, 일부 알림의 hello 상위 hello 설정을 상속 합니다.  즉, 해당 hello IssuerUri toomatch hello 부모 항목입니다.

따라서 예를 들어 bmcontoso.com이 있고 corp.bmcontoso.com을 추가한다고 가정합니다.  즉, 해당 hello IssuerUri corp.bmcontoso.com에서 필요성이 toobe에 대 한 **http://bmcontoso.com/adfs/services/trust 합니다.**  하지만 Azure AD에 대 한 위의 hello 표준 규칙 구현으로 발급자와 토큰을 생성 합니다 **http://corp.bmcontoso.com/adfs/services/trust 합니다.** hello 도메인의 필수 값 일치 하지는 않으며 인증이 실패 합니다.

### <a name="how-tooenable-support-for-sub-domains"></a>하위 도메인에 대 한 tooenable를 지 원하는 방법
이 hello 주위 순서 toowork AD FS 신뢰 당사자 트러스트에 대 한 Microsoft Online toobe 업데이트 해야 합니다.  toodo이 hello 사용자 지정 하는 발급자 값을 생성할 때 모든 하위 도메인에서 hello 사용자의 UPN 접미사를 제거 하는 것을 사용자 지정 클레임 규칙을 구성 해야 합니다. 

hello 클레임 다음이 수행 합니다.

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
hello 정규식의 마지막 번호 hello hello 루트 도메인에 부모 도메인을 설정 합니다. 여기서 bmcontoso.com이 있으므로 2개의 상위 도메인이 필요합니다. 도메인 상위 3 개의 toobe 유지 된 경우 (즉,: corp.bmcontoso.com), hello 수 있었을 세 합니다. Eventualy 범위를 표시할 수 있습니다 하는 경우 일치 하는 hello toomatch hello 최대값인 도메인 수행 항상 합니다. "{" (2, 3} 두 toothree 도메인 일치 합니다 (예:: bmfabrikam.com 및 corp.bmcontoso.com).

다음 단계 tooadd hello 사용자 지정 클레임 toosupport 하위 도메인을 사용 합니다.

1. AD FS 관리 열기
2. Microsoft 온라인 RP trust hello를 마우스 오른쪽 단추로 클릭 하 고 편집 하는 클레임 규칙 선택
3. Hello 세 번째 클레임 규칙을 선택 하 고 대체 ![편집 클레임](./media/active-directory-multiple-domains/sub1.png)
4. Hello 현재 클레임을 바꿉니다.
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![클레임 바꾸기](./media/active-directory-multiple-domains/sub2.png)

5. 확인을 클릭합니다.  적용을 클릭합니다.  확인을 클릭합니다.  AD FS 관리를 닫습니다.

