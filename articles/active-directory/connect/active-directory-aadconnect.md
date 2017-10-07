---
title: "Active Directory와 Azure Active Directory 연결 | Microsoft Docs"
description: "Azure AD Connect는 온-프레미스 디렉터리와 Azure Active Directory를 통합니다. 이렇게 하면 tooprovide Office 365, Azure 및 SaaS 응용 프로그램에 대 한 일반 id를 Azure AD와 통합 되어 있습니다."
keywords: "소개 tooAzure AD Connect, Azure AD Connect 개요, Azure AD Connect 설치 active directory 란"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e49f2af4b67e9ed3ad093888541da7c82af0e052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-on-premises-directories-with-azure-active-directory"></a>Azure Active Directory와 온-프레미스 디렉터리 통합
Azure AD Connect는 온-프레미스 디렉터리와 Azure Active Directory를 통합니다. 이렇게 하면 tooprovide Office 365, Azure 및 SaaS 응용 프로그램에 대 한 사용자에 대 한 일반 id를 Azure AD와 통합 되어 있습니다. 이 항목에서는 hello 계획, 배포 및 작업 단계를 통해 안내 합니다. 링크 toohello 항목 관련된 toothis 영역의 컬렉션입니다.

> [!IMPORTANT]
> [Azure AD Connect 가장 좋은 방법은 tooconnect Azure AD와 온-프레미스 디렉터리 hello는 및 Office 365 합니다. 이것이 좋은 시간 tooupgrade tooAzure Windows Azure Active Directory 동기화 (DirSync) 또는 Azure AD Sync에서 AD 연결 이러한 도구는 이제 사용 되지 않으며 2017 년 4 월 13에 대 한 지원의 끝에 도달 합니다.](active-directory-aadconnect-dirsync-deprecated.md)
> 
> 

![Azure AD Connect의 정의](media/active-directory-aadconnect/arch.png)

## <a name="why-use-azure-ad-connect"></a>Azure AD Connect를 사용하는 이유
Azure AD와 온-프레미스 디렉터리를 통합하면 온-프레미스 및 클라우드 리소스 모두에 액세스하기 위한 일반적인 ID를 제공하므로 사용자가 더 생산성을 높일 수 있습니다. 사용자 및 조직 hello 다음을 활용을 사용할 수 있습니다.

* 사용자가 단일 id tooaccess 온-프레미스 응용 프로그램을 사용할 수 있으며 클라우드 Office 365와 같은 서비스.
* 동기화 및 로그인에 대 한 간편한 배포 환경을 도구 tooprovide을 단일.
* 시나리오에 대 한 hello 최신 기능을 제공합니다. Azure AD Connect는 DirSync 및 Azure AD Sync와 같은 이전 버전의 ID 통합 도구를 대체합니다. 자세한 내용은 [하이브리드 ID 디렉터리 통합 도구 비교](../active-directory-hybrid-identity-design-considerations-tools-comparison.md)를 참조하세요.

### <a name="how-azure-ad-connect-works"></a>Azure AD Connect 작동 방법
세 가지 기본 구성 요소 구성 된 azure Active Directory Connect: hello 동기화 서비스, hello 선택적 Active Directory Federation Services 구성 요소 및 hello 모니터링 구성 요소 라는 [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md) .

<center>![Azure AD Connect 스택](./media/active-directory-aadconnect-how-it-works/AADConnectStack2.png)
</center>

* 동기화 - 이 구성 요소는 사용자, 그룹 및 기타 개체 생성을 담당합니다. 온-프레미스 사용자 및 그룹에 대 한 id 정보에는 hello 클라우드 일치 하는 확인할 책임이 이기도 합니다.
* -AD FS 페더레이션은 Azure AD Connect의 선택적 부분 및 온-프레미스를 사용 하는 하이브리드 환경 사용된 tooconfigure 수 AD FS 인프라입니다. 도메인 가입 SSO, 스마트 카드 또는 타사 MFA 및 AD 로그인 정책 적용 등 조직 tooaddress 복잡 한 배포를 사용할 수 있습니다.
* 상태 모니터링-Azure AD Connect Health에서 강력한 모니터링을 제공 하 고이 활동 hello Azure 포털 tooview에서에서 중앙 위치를 제공할 수 있습니다. 자세한 내용은 [Azure Active Directory Connect Health](../connect-health/active-directory-aadconnect-health.md)를 참조하세요.

## <a name="install-azure-ad-connect"></a>Azure AD Connect 설치
Azure AD Connect에 대 한 hello 다운로드에서 찾을 수 있습니다 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=615771)합니다.

| 해결 방법 | 시나리오 |
| --- | --- |
| 시작하기 전에 - [하드웨어 및 필수 구성 요소](active-directory-aadconnect-prerequisites.md) |<li>단계 toocomplete tooinstall Azure AD Connect를 시작 하기 전에</li> |
| [Express 설정](active-directory-aadconnect-get-started-express.md) |<li>단일 포리스트 AD 다음이 있는 경우 hello가 좋습니다 toouse 옵션.</li> <li>동일한 hello를 사용 하 여 사용자 로그인 암호 동기화를 사용 하 여 암호입니다.</li> |
| [사용자 지정된 설정](active-directory-aadconnect-get-started-custom.md) |<li>여러 포리스트가 있는 경우 사용됩니다. 다양한 온-프레미스 [토폴로지](active-directory-aadconnect-topologies.md)를 지원합니다.</li> <li>페더레이션의 ADFS와 같은 로그인 옵션을 사용자 지정하거나 타사 ID 공급자를 사용합니다.</li> <li>필터링 및 쓰기 저장과 같은 동기화 기능을 사용자 지정합니다.</li> |
| [DirSync에서 업그레이드](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>기존 DirSync 서버를 이미 실행 중인 경우 사용됩니다.</li> |
| [Azure AD Sync 또는 Azure AD Connect에서 업그레이드](active-directory-aadconnect-upgrade-previous-version.md) |<li>기본 설정에 따라 여러 가지 방법이 있습니다.</li> |

[설치 후](active-directory-aadconnect-whats-next.md) 예상 대로 작동 되 고 toohello 사용자 라이선스 할당을 확인 해야 합니다.

### <a name="next-steps-tooinstall-azure-ad-connect"></a>Azure AD Connect tooInstall 다음 단계
|항목 |링크|  
| --- | --- |
|Azure AD Connect 다운로드 | [Azure AD Connect 다운로드](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Express 설정을 사용하여 설치 | [Azure AD Connect의 빠른 설치](./active-directory-aadconnect-get-started-express.md)|
|사용자 지정 설정을 사용하여 설치 | [Azure AD Connect의 사용자 지정 설치](./active-directory-aadconnect-get-started-custom.md)|
|DirSync에서 업그레이드 | [Azure AD Sync 도구(DirSync)에서 업그레이드](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|설치 후 | [Hello 설치 되었는지 확인 하 고 라이선스 할당](active-directory-aadconnect-whats-next.md)|

### <a name="learn-more-about-install-azure-ad-connect"></a>Azure AD Connect 설치에 대해 자세히 알아봅니다.
에 대 한 tooprepare 시겠습니까 [operational](active-directory-aadconnectsync-operations.md) 문제입니다. 쉽게 수 해당 하는 독자를 통해 없을 경우 하므로 toohave 대기 서버를 할 수 있습니다는 [재해](active-directory-aadconnectsync-operations.md#disaster-recovery)합니다. 에 대 한 계획 해야 toomake 자주 구성 변경 하려는 경우는 [준비 모드](active-directory-aadconnectsync-operations.md#staging-mode) 서버입니다.

|항목 |링크|  
| --- | --- |
|지원되는 토폴로지 | [Azure AD Connect에 대한 토폴로지](active-directory-aadconnect-topologies.md)|
|설계 개념 | [Azure AD Connect 설계 개념](active-directory-aadconnect-design-concepts.md)|
|설치에 사용되는 계정 | [Azure AD Connect 자격 증명 및 사용 권한에 대한 자세한 정보](./active-directory-aadconnect-accounts-permissions.md)|
|운영 계획 | [Azure AD Connect Sync: 운영 작업 및 고려 사항](active-directory-aadconnectsync-operations.md)|
|사용자 로그인 옵션 | [Azure AD Connect 사용자 로그인 옵션](active-directory-aadconnect-user-signin.md)|

## <a name="configure-sync-features"></a>동기화 기능 구성
Azure AD Connect는 필요에 따라 기본적으로 키거나 사용할 수 있는 몇 가지 기능이 함께 제공됩니다. 일부 기능은 특정한 시나리오 및 토폴로지에 추가적인 구성이 필요한 경우도 있습니다.

[필터링](active-directory-aadconnectsync-configure-filtering.md) 어느 개체가 toolimit tooAzure AD 동기화 원할 때 사용 됩니다. 기본적으로 모든 사용자, 연락처, 그룹 및 Windows 10 컴퓨터는 동기화됩니다. Hello 도메인, Ou 또는 특성 기반 필터링을 변경할 수 있습니다.

[암호 동기화](active-directory-aadconnectsync-implement-password-synchronization.md) Active Directory tooAzure AD에서에서 hello 암호 해시 동기화 합니다. hello 최종 사용자는 hello 같은 암호를 온-프레미스와만 hello 클라우드에서 관리에 한 위치에서 사용할 수 있습니다. Hello 기관으로 온-프레미스 Active Directory를 사용 하므로 사용자 고유의 암호 정책을 사용할 수도 있습니다.

[암호 쓰기 저장](../active-directory-passwords-getting-started.md) 사용자 toochange 허용 하 고 hello 클라우드에서 암호를 재설정할 및 프로그램 온-프레미스 암호 정책이 적용 됩니다.

[장치 쓰기 저장](active-directory-aadconnect-feature-device-writeback.md) 조건부 액세스에 사용할 수 있도록 tooon 온-프레미스 Active Directory 다시 작성 하는 Azure AD toobe에 등록 된 장치를 허용 합니다.

hello [실수로 삭제 금지](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) 기본적으로 설정 하 고 hello에서 많은 삭제를 클라우드 디렉터리를 보호 하는 기능 동시 합니다. 기본적으로 실행 당 삭제 500회를 허용합니다. 조직의 규모에 따라서 이 설정을 변경할 수 있습니다.

[자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md) 은 기본 설정 설치를 위한 기본값으로 사용 가능 하 고 Azure AD Connect에는 항상 hello 최신 릴리스로 toodate를 되도록 합니다.

### <a name="next-steps-tooconfigure-sync-features"></a>다음 단계 tooconfigure sync 화 기능
|항목 |링크|  
| --- | --- |
|필터링 구성 | [Azure AD Connect 동기화 구성 필터링](active-directory-aadconnectsync-configure-filtering.md)|
|암호 동기화 | [Azure AD Connect 동기화: 암호 동기화 구현](active-directory-aadconnectsync-implement-password-synchronization.md)|
|비밀번호 쓰기 저장 | [암호 관리 시작](../active-directory-passwords-getting-started.md)|
|장치 쓰기 저장 | [Azure AD Connect에서 장치 쓰기 저장 사용](active-directory-aadconnect-feature-device-writeback.md)|
|실수로 인한 삭제 방지 | [Azure AD Connect 동기화: 실수로 인한 삭제 방지](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)|
|자동 업그레이드 | [Azure AD Connect: 자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md)|

## <a name="customize-azure-ad-connect-sync"></a>Azure AD Connect 동기화 사용자 지정
Azure AD Connect 동기화 의도 한 toowork 대부분의 고객 및 토폴로지를 기본 구성으로 제공 됩니다. 하지만 항상 hello 기본 구성이 작동 하지 않습니다 있으며 조정 해야 합니다. 이 섹션 및 연결 된 항목에 문서화 된 대로 지원된 toomake 변경 되기.

Toostart toounderstand hello 기본 사항 및 hello에 설명 된 대로 사용 되는 용어 hello 전에 하지 동기화 토폴로지를 사용한 적이 있으면 [기술 개념](active-directory-aadconnectsync-technical-concepts.md)합니다. Azure AD Connect가 miis 2003, ILM2007와 FIM2010 hello 발전 합니다. 일부가 동일하지만 많은 부분이 변경되었습니다.

hello [기본 구성](active-directory-aadconnectsync-understanding-default-configuration.md) hello 구성에 둘 이상의 포리스트에 있을 수 있다고 가정 합니다. 이러한 토폴로지에서 사용자 개체는 다른 포리스트에 연락처로 표시될 수 있습니다. hello 사용자는 다른 리소스 포리스트에 연결된 된 사서함을 있을 수 있습니다. 에 설명 된 hello 기본 구성의 hello 동작 [사용자 및 연락처](active-directory-aadconnectsync-understanding-users-and-contacts.md)합니다.

동기화 hello 구성 모델 라고 [선언적 프로비저닝이](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)합니다. hello 고급 특성 흐름 사용 하는 [함수](active-directory-aadconnectsync-functions-reference.md) tooexpress 특성 변환 합니다. 참조할 수 있으며 hello 전체 구성을 검사 도구를 사용 하 여 Azure AD Connect와 함께 제공 되 있습니다. Toomake 구성을 변경 해야 할 경우 hello를 따르고 있는지 확인 [모범 사례](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) tooadopt 새 릴리스를 보다 쉽게 되기 때문입니다.

### <a name="next-steps-toocustomize-azure-ad-connect-sync"></a>다음 toocustomize Azure AD Connect 동기화 단계
|항목 |링크|  
| --- | --- |
|모든 Azure AD Connect Sync 문서 | [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md)|
|기술 개념 | [Azure AD Connect Sync: 기술 개념](active-directory-aadconnectsync-technical-concepts.md)|
|Hello 기본 구성 이해 | [Azure AD Connect 동기화: hello 기본 구성 이해](active-directory-aadconnectsync-understanding-default-configuration.md)|
|사용자 및 연락처 이해 | [Azure AD Connect Sync: 사용자 및 연락처 이해](active-directory-aadconnectsync-understanding-users-and-contacts.md)|
|선언적 프로비전 | [Azure AD Connect Sync: 선언적 프로비전 식 이해](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)|
|Hello 기본 구성 변경 | [Hello 기본 구성 변경에 대 한 모범 사례](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)|

## <a name="configure-federation-features"></a>페더레이션 기능 구성
Ad FS 구성된 toosupport 수 [여러 도메인](active-directory-aadconnect-multiple-domains.md)합니다. 예를 들어 여러 최상위 도메인 페더레이션 toouse 사용 해야 할 수 있습니다.

ADFS 서버에서 구성 된 tooautomatically Azure AD에서 인증서를 업데이트 하지 않았습니다 또는 ADFS 아닌 솔루션을 사용 하는 경우 다음 알려 너무 있으면[인증서 업데이트](active-directory-aadconnect-o365-certs.md)합니다.

### <a name="next-steps-tooconfigure-federation-features"></a>다음 단계 tooconfigure 페더레이션 기능
|항목 |링크|  
| --- | --- |
|모든 AD FS 문서 | [Azure AD Connect 및 페더레이션](active-directory-aadconnectfed-whatis.md)|
|ADFS에 하위 도메인 구성 | [Azure AD로 페더레이션에 대한 여러 도메인 지원](active-directory-aadconnect-multiple-domains.md)|
|AD FS 팜 관리 | [Azure AD Connect를 사용한 AD FS 관리 및 사용자 지정](active-directory-aadconnect-federation-management.md)|
|페더레이션 인증서를 수동으로 업데이트 | [Office 365 및 Azure AD에 대한 페더레이션 인증서 갱신](active-directory-aadconnect-o365-certs.md)|

## <a name="more-information-and-references"></a>자세한 내용 및 참조
|항목 |링크|  
| --- | --- |
|버전 기록 | [버전 기록](active-directory-aadconnect-version-history.md)|
|DirSync, Azure ADSync 및 Azure AD Connect 비교 | [디렉터리 통합 도구 비교](../active-directory-hybrid-identity-design-considerations-tools-comparison.md)|
|Azure AD의 비 ADFS 호환성 목록 | [Azure AD 페더레이션 호환성 목록](active-directory-aadconnect-federation-compatibility.md)|
|SAML 2.0 Idp 구성|[Single Sign-On에 SAML 2.0 IdP(ID 공급자) 사용](active-directory-aadconnect-federation-saml-idp.md)|
|동기화된 특성 | [동기화된 특성](active-directory-aadconnectsync-attributes-synchronized.md)|
|Azure AD Connect Health를 사용하여 모니터링 | [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md)|
|질문과 대답 | [Azure AD Connect FAQ](active-directory-aadconnect-faq.md)|

**추가 리소스**

온-프레미스 디렉터리 toohello 클라우드 확장에서 2015 프레젠테이션을 칼럼 합니다.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3862/player]
> 
> 

