---
title: "Azure AD 도메인 서비스: 비교 Azure AD 도메인 서비스 tooDIY 도메인 컨트롤러 | Microsoft Docs"
description: "Azure Active Directory 도메인 서비스 tooDIY 도메인 컨트롤러를 비교합니다."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 165249d5-e0e7-4ed1-aa26-91a05a87bdc9
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: maheshu
ms.openlocfilehash: 5e384f6a676e76e4f22ff62d4aeb578bc8481ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodecide-if-azure-ad-domain-services-is-right-for-your-use-case"></a>어떻게 toodecide 경우 Azure AD 도메인 서비스는 적합 한 사용 사례
Azure AD 도메인 서비스와 Azure의 id 인프라를 유지 관리 하는 방법에 대 한 tooworry 필요 없이 Azure 인프라 서비스에서 작업을 배포할 수 있습니다. 이 관리되는 서비스는 고유한 서비스에 배포하고 관리하는 일반적인 Windows Server Active Directory 배포와 다릅니다. hello 서비스 쉽게 toodeploy 이며 자동화 상태 모니터링 및 업데이트 관리를 제공 합니다. 끊임없이 일반적인 배포 시나리오에 대 한 hello 서비스 tooadd 지원을 진화 했습니다.

toodecide 읽기 자료 다음 hello 권장 여부 toouse Azure AD 도메인 서비스:

* Hello 목록이 나타날 [Azure AD 도메인 서비스에서 제공 하는 기능](active-directory-ds-features.md)합니다.
* 일반적인 [Azure AD Domain Services용 배포 시나리오](active-directory-ds-scenarios.md)를 검토합니다.
* 마지막으로, [Azure AD 도메인 서비스 자체 AD tooa 옵션 비교](active-directory-ds-comparison.md#compare-azure-ad-domain-services-to-diy-ad-domain-in-azure)합니다.

## <a name="compare-azure-ad-domain-services-toodiy-ad-domain-in-azure"></a>Azure에서 Azure AD 도메인 서비스 tooDIY AD 도메인을 비교 합니다.
hello 다음 표를 사용 하면 Azure AD 도메인 서비스를 사용 하 여 Azure에서 해당 하는 AD 인프라를 관리 및 중 하나를 결정 합니다.

| **기능** | **Azure AD Domain Services** | **Azure VM의 '직접' AD** |
| --- |:---:|:---:|
| [**관리되는 서비스**](active-directory-ds-comparison.md#managed-service) |**&#x2713;** |**&#x2715;** |
| [**보안 배포**](active-directory-ds-comparison.md#secure-deployments) |**&#x2713;** |관리자는 toosecure hello 배포를 해야합니다. |
| [**DNS 서버**](active-directory-ds-comparison.md#dns-server) |**&#x2713;**(관리되는 서비스) |**&#x2713;** |
| [**Domain or Enterprise administrator privileges**](active-directory-ds-comparison.md#domain-or-enterprise-administrator-privileges) |**&#x2715;** |**&#x2713;** |
| [**도메인 가입**](active-directory-ds-comparison.md#domain-join) |**&#x2713;** |**&#x2713;** |
| [**NTLM 및 Kerberos를 사용하여 도메인 인증**](active-directory-ds-comparison.md#domain-authentication-using-ntlm-and-kerberos) |**&#x2713;** |**&#x2713;** |
| [**Kerberos 제한 위임**](active-directory-ds-comparison.md#kerberos-constrained-delegation)|리소스 기반|리소스 기반 및 계정 기반|
| [**사용자 지정 OU 구조**](active-directory-ds-comparison.md#custom-ou-structure) |**&#x2713;** |**&#x2713;** |
| [**스키마 확장**](active-directory-ds-comparison.md#schema-extensions) |**&#x2715;** |**&#x2713;** |
| [**AD 도메인/포리스트 트러스트**](active-directory-ds-comparison.md#ad-domain-or-forest-trusts) |**&#x2715;** |**&#x2713;** |
| [**LDAP read**](active-directory-ds-comparison.md#ldap-read) |**&#x2713;** |**&#x2713;** |
| [**보안 LDAP(LDAPS)**](active-directory-ds-comparison.md#secure-ldap) |**&#x2713;** |**&#x2713;** |
| [**LDAP write**](active-directory-ds-comparison.md#ldap-write) |**&#x2715;** |**&#x2713;** |
| [**Group Policy**](active-directory-ds-comparison.md#group-policy) |**&#x2713;** |**&#x2713;** |
| [**지리적으로 분산된 배포**](active-directory-ds-comparison.md#geo-dispersed-deployments) |**&#x2715;** |**&#x2713;** |

#### <a name="managed-service"></a>관리되는 서비스
Azure AD Domain Services 도메인은 Microsoft에서 관리합니다. 패치, 업데이트, 백업, 모니터링 및 도메인의 가용성을 보장 하는 방법에 대 한 tooworry를 않아도 됩니다. 이러한 관리 태스크는 Microsoft Azure에서 관리되는 도메인에 대해 서비스로 제공합니다.

#### <a name="secure-deployments"></a>보안 배포
hello 관리 되는 도메인은 안전 하 게 AD 배포에 대 한 Microsoft의 보안 권장 사항 잠겨 있습니다. 이러한 권장 사항은 AD hello 제품 팀의 수십 엔지니어링 및 지원 되는 AD 배포 환경에서에서 형태소 분석 합니다. Tootake 특정 배포 자체 배포에 필요한 배포 단계 toolock 다운/보안 합니다.

#### <a name="dns-server"></a>DNS 서버
Azure AD Domain Services 관리되는 도메인은 관리되는 DNS 서비스를 포함합니다. Hello ' AAD DC Administrators' 그룹의 구성원 hello 관리 되는 도메인에 DNS를 관리할 수 있습니다. 이 그룹의 구성원 hello 관리 되는 도메인에 대 한 DNS 관리에 대 한 모든 권한은 제공 됩니다. 'Hello 원격 서버 관리 도구 (RSAT) 패키지에 포함 된 ' DNS 관리 콘솔 hello를 사용 하 여 DNS 관리를 수행할 수 있습니다.
[자세한 정보](active-directory-ds-admin-guide-administer-dns.md)

#### <a name="domain-or-enterprise-administrator-privileges"></a>도메인 또는 엔터프라이즈 관리자 권한
AAD DS 관리되는 도메인에서는 이러한 상승된 권한이 제공되지 않습니다. 관리자 권한을 요구하는 응용 프로그램은 AAD DS 관리되는 도메인에 대해 배포할 수 없습니다. 관리자 권한의 작은 하위 집합은 ' AAD DC 관리자 '를 호출 하는 hello 위임 된 관리 그룹의 사용 가능한 toomembers입니다. 메뉴, 도구 모음을 이러한 권한을 포함 권한 tooconfigure DNS 그룹 정책을 구성 도메인에 가입 된 컴퓨터 등에서 관리자 권한을 얻게 됩니다.

#### <a name="domain-join"></a>도메인 가입
가상 컴퓨터를 가입할 수 toohello 관리 도메인 비슷한 toohow 컴퓨터 tooan AD 도메인에 가입 합니다.

#### <a name="domain-authentication-using-ntlm-and-kerberos"></a>NTLM 및 Kerberos를 사용하여 도메인 인증
Azure AD 도메인 서비스를 사용 하면 회사 자격 증명 tooauthenticate hello 관리 되는 도메인을 사용할 수 있습니다. 자격 증명은 Azure AD 테넌트와 동기화된 상태로 유지됩니다. 동기화 된 테 넌 트에 대 한 Azure AD Connect 하면 변경 내용을 toocredentials 온-프레미스 AD 동기화 된 tooAzure 됩니다. AD 도메인을 tooset 자체 도메인 설치를 할 수 있습니다 신뢰를 온-프레미스 AD에서 사용자가 회사 자격 증명으로 tooauthenticate 합니다. 또는 tooset AD 복제 tooensure로 사용자 암호 동기화 tooyour Azure 도메인 컨트롤러 가상 컴퓨터를 할 수 있습니다.

#### <a name="kerberos-constrained-delegation"></a>Kerberos 제한 위임
Active Directory Domain Services 관리되는 도메인에서 '도메인 관리자' 권한이 없습니다. 따라서 계정 기반(기존의) Kerberos 제한 위임을 구성할 수 없습니다. 그러나 더 안전한 hello를 구성할 수 있습니다 리소스 기반의 제한 위임 합니다.
[자세한 정보](active-directory-ds-enable-kcd.md)

#### <a name="custom-ou-structure"></a>사용자 지정 OU 구조
Hello ' AAD DC Administrators' 그룹의 구성원 hello 관리 되는 도메인 내에서 사용자 지정 Ou를 만들 수 있습니다. 사용자 지정 Ou를 만드는 사용자가 hello OU 통해 모든 관리 권한이 부여 됩니다.
[자세한 정보](active-directory-ds-admin-guide-create-ou.md)

#### <a name="schema-extensions"></a>스키마 확장
Hello Azure AD 도메인 서비스는 관리 되는 도메인의 기본 스키마를 확장할 수 없습니다. 따라서 확장 tooAD 스키마 (예를 들어 hello 사용자 개체에서 새 특성)에 의존 하는 응용 프로그램 변경 될 수 없습니다 및 tooAAD DS 도메인을 향해 이동 합니다.

#### <a name="ad-domain-or-forest-trusts"></a>AD 도메인 또는 포리스트 트러스트
관리 되는 도메인은 다른 도메인과 트러스트 관계 (인바운드/아웃 바운드)를 구성 된 tooset 일 수 없습니다. 따라서 리소스 포리스트 배포 시나리오는 Azure AD Domain Services를 사용할 수 없습니다. 마찬가지로, 배포 되지 toosynchronize 암호 tooAzure AD 기본 위치는 Azure AD 도메인 서비스를 사용할 수 없습니다.

#### <a name="ldap-read"></a>LDAP 읽기
hello는 도메인 지원 LDAP에 대 한 읽기 작업을 관리합니다. 따라서 LDAP 읽기 hello 관리 되는 도메인에 대해 작업을 수행 하는 응용 프로그램을 배포할 수 있습니다.

#### <a name="secure-ldap"></a>보안 LDAP
Azure AD 도메인 서비스 tooprovide 보안 LDAP 액세스 tooyour 관리를 구성할 수 등을 통해 도메인에 인터넷 hello 합니다.
[자세한 정보](active-directory-ds-admin-guide-configure-secure-ldap.md)

#### <a name="ldap-write"></a>LDAP 쓰기
hello 관리 되는 도메인은 사용자 개체에 대 한 읽기 전용입니다. 따라서 hello 사용자 개체의 특성에 대해 LDAP 쓰기 작업을 수행 하는 응용 프로그램 관리 되는 도메인에서 작동 하지 않습니다. 또한 사용자 암호 hello 관리 되는 도메인 내에서 변경할 수 없습니다. 또 다른 예로의 그룹 멤버 자격 또는 그룹 특성 허용 되지 않는 hello 관리 되는 도메인 내에서 수정할 것입니다. 그러나 변경한 사항이 toouser 특성 또는 (PowerShell/Azure 포털)을 통해 Azure AD에서 암호 또는 온-프레미스 AD에서 동기화 됩니다 toohello AAD DS 도메인을 관리 합니다.

#### <a name="group-policy"></a>그룹 정책
기본 제공 GPO 각 hello "AADDC 컴퓨터"와 "AADDC 사용자" 컨테이너에 대 한 있습니다. 이러한 기본 제공의 Gpo tooconfigure 그룹 정책을 사용자 지정할 수 있습니다. Hello ' AAD DC Administrators' 그룹의 멤버가 사용자 지정 Gpo를 만들 수 있고 tooexisting Ou (사용자 지정 Ou 포함)에 연결 합니다.
[자세한 정보](active-directory-ds-admin-guide-administer-group-policy.md)

#### <a name="geo-dispersed-deployments"></a>지역 분산된 배포
Azure AD Domain Services 관리되는 도메인은 Azure의 단일 가상 네트워크에서 사용할 수 있습니다. Hello 전 세계 여러 Azure 지역에서 사용할 수 있는 도메인 컨트롤러 toobe 해야 하는 시나리오, Azure IaaS Vm에서 도메인 컨트롤러 설정 hello 적절 한 대안이 될 수 있습니다.


## <a name="do-it-yourself-diy-ad-deployment-options"></a>DIY('직접') AD 배포 옵션
Windows Server AD 설치에서 제공 하는 hello 기능 중 일부 필요한 배포 사용 사례를 할 수 있습니다. 이러한 경우 hello 다음 자체 (DIY) 옵션 중 하나를 하세요.

* **독립 실행형 클라우드 도메인:** 도메인 컨트롤러로 구성된 Azure 가상 컴퓨터를 사용하여 독립 실행형 '클라우드 도메인'을 설정할 수 있습니다. 이 인프라는 온-프레미스 AD 환경과 통합되지 않습니다. 이 옵션 '클라우드 자격 증명' toologin/Vm을 관리 hello 클라우드에서 다른 집합이 필요 합니다.
* **리소스 포리스트 배포:** 도메인 컨트롤러로 구성 된 Azure 가상 컴퓨터를 사용 하 여 hello 리소스 포리스트 토폴로지에서 도메인을 설정할 수 있습니다. 다음으로 온-프레미스 AD 환경으로 AD 트러스트 관계를 구성할 수 있습니다. 도메인 가입 컴퓨터 (Azure Vm) toothis 리소스 포리스트 hello 클라우드에서 할 수 있습니다. 사용자 인증 VPN/ExpressRoute 연결 tooyour 온-프레미스 디렉터리 중 하나를 통해 수행 됩니다.
* **온-프레미스 도메인 tooAzure 확장:** VPN/ExpressRoute 연결을 사용 하는 Azure 가상 네트워크 tooyour 온-프레미스 네트워크를 연결할 수 있습니다. 이 설치에서는 Azure Vm toobe 조인된 tooyour 온-프레미스 AD 합니다. 또 다른 방법은 Azure에서 온-프레미스 도메인의 toopromote 복제 도메인 컨트롤러 VM으로입니다. 또한 VPN/ExpressRoute 연결 tooyour 온-프레미스 디렉터리를 통해 tooreplicate를 설정 합니다. 이 배포 모드는 온-프레미스 도메인 tooAzure 효과적으로 확장합니다.

> [!NOTE]
> 배포 사용 사례에 DIY 옵션이 더 적합한지 결정할 수 있습니다. 것이 좋습니다 [의견을 공유](active-directory-ds-contact-us.md) toohelp 도움이 될 기능을 이해 우리 hello 나중에 Azure AD 도메인 서비스를 선택 합니다. 이 피드백 hello 서비스 toobetter 맞게 프로그램 배포 요구 사항 및 사용 사례를 발전시키는 도움이 됩니다.
>
>

게시 한 우리 [배포 Windows Server Active Directory를 Azure 가상 컴퓨터에 대 한 지침이](https://msdn.microsoft.com/library/azure/jj156090.aspx) toohelp 쉽게 DIY 설치 합니다.

## <a name="related-content"></a>관련 콘텐츠
* [기능 - Azure AD Domain Services](active-directory-ds-features.md)
* [배포 시나리오 - Azure AD Domain Services](active-directory-ds-scenarios.md)
* [Azure 가상 컴퓨터에 Windows Server Active Directory를 배포하기 위한 지침](https://msdn.microsoft.com/library/azure/jj156090.aspx)
