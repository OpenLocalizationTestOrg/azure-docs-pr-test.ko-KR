---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-하이브리드 identity lifecycle 채택 전략을 결정 | Microsoft Docs"
description: "Hello 하이브리드 identity 관리 작업을 각 수명 주기 단계에 대해 사용할 수 있는 toohello 옵션에 따라 정의할 수 있습니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 420b6046-bd9b-4fce-83b0-72625878ae71
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 86ec0a9896f069bc93e49e06006954848f8e4d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-hybrid-identity-lifecycle-adoption-strategy"></a>하이브리드 ID 수명 주기 채택 전략 결정
이 태스크에서는 프로그램 하이브리드 id 솔루션 toomeet hello 비즈니스 요구 사항에 정의 된에 대 한 id 관리 전략이 hello를 정의 합니다 [하이브리드 identity 관리 작업을 결정](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)합니다.

toodefine hello 하이브리드 identity, 관리 작업을이 단계에서 제시 toohello 종단 간 identity lifecycle에 따라 각 수명 주기 단계에 대해 사용할 수 있는 tooconsider hello 옵션 해야 합니다.

## <a name="access-management-and-provisioning"></a>액세스 관리 및 프로비전
좋은 계정 액세스 관리 솔루션으로 조직 추적할 수 정확 하 게 hello 조직 전체에서 toowhat 정보에 액세스할 수 있는 합니다.

액세스 제어는 중앙 집중화된 단일 지점 프로비전 시스템의 중요한 기능입니다. 중요한 정보를 보호하는 것 이외에도 액세스 제어는 승인되지 않은 권한 부여가 있는 기존 계정을 노출하거나 더 이상 필요하지 않습니다. 사용 되지 않는 계정 toocontrol hello hello 계정을 소유한 hello 사용자에 대 한 신뢰할 수 있는 정보를 프로 비전 시스템 링크 함께 계정 정보. 신뢰할 수 있는 사용자 id 정보는 hello 데이터베이스 및 인적 자원의 디렉터리에 일반적으로 유지 됩니다.

준비 시스템에서 이러한 세부 정보를 제어할 수 있습니다 및 복잡 한 IT 기업의 계정 hello 기관을 정의 하는 매개 변수에서 수백 포함 됩니다. Hello 권한이 있는 원본에서 제공 하는 hello 데이터로 새 사용자를 식별할 수 있습니다. hello 액세스 요청 승인 기능 승인 (또는 거부) 리소스를 프로 비전 하는 hello 프로세스를 시작 합니다.

| 수명 주기 관리 단계 | 온-프레미스 | 클라우드 | 하이브리드 |
| --- | --- | --- | --- |
| 계정 관리 및 프로비전 |Hello Active Directory® 도메인 서비스 (AD DS) 서버 역할을 사용 하 여 사용자 및 리소스 관리에 대 한 확장 가능 하 고 안전 하며 관리 하기 쉬운 인프라를 만들고 Microsoft® Exchange Server와 같은 디렉터리 사용 응용 프로그램에 대 한 지원을 제공 합니다. <br><br> [ID 관리자를 통해 AD DS의 그룹을 프로비전할 수 있습니다.](https://technet.microsoft.com/library/ff686261.aspx) <br>[AD DS의 사용자를 프로비전할 수 있습니다.](https://technet.microsoft.com/library/ff686263.aspx) <br><br> 관리자는 보안을 위해 액세스 제어 toomanage 사용자 액세스 tooshared 리소스를 사용할 수 있습니다. Active Directory 액세스 제어 설정 서로 다른 수준의 액세스 또는 사용 권한, tooobjects 하 여 hello 개체 수준에서 관리 됩니다. 모든 권한, 쓰기, 읽기, 액세스 제한 등입니다. Active directory의 액세스 제어는 어떻게 다른 사용자가 Active Directory 개체를 사용할 수 있는지 정의합니다. 기본적으로 Active Directory 개체에 대 한 가장 안전한 설정이 toohello 설정 됩니다. |사용자에 게 toocreate 계정이 Microsoft 클라우드 서비스에 액세스 하는 모든 사용자에 대 한 합니다. 사용자 계정을 변경할 수도 있으며 더 이상 필요하지 않은 계정은 삭제할 수 있습니다. 기본적으로 사용자에게는 관리자 권한이 없지만 선택적으로 할당할 수 있습니다. 자세한 내용은 [Azure AD에서 사용자 관리](active-directory-create-users.md)를 참조하세요. <br><br> Azure Active Directory within hello 기능 toomanage 액세스 tooresources은 hello 주요 기능 중 하나입니다. 이러한 리소스는 hello 디렉터리나 SaaS 응용 프로그램, Azure 서비스 및 SharePoint 사이트 또는 온-프레미스와 같은 외부 toohello 디렉터리에 있는 리소스에 대 한 역할을 통해 권한 toomanage 개체 hello 경우 처럼 hello 디렉터리의 일부가 될 수 있습니다. 리소스입니다. <br><br> Hello에 센터의 Azure Active Directory의 액세스 관리 솔루션은 hello 보안 그룹입니다. hello 리소스 소유자 (또는 hello 디렉터리의 관리자에 게) 그룹 tooprovide 특정는 액세스 오른쪽 toohello 리소스 자신이 소유한 할당할 수 있습니다. hello 그룹의 구성원 hello hello 액세스가 제공 됩니다 및 hello 리소스 소유자는 그룹 toosomeone 부서 관리자 또는 기술 지원팀 관리자 같은 다른 – hello 오른쪽 toomanage hello 멤버 목록에 위임할 수 있습니다.<br> <br> hello 관리 그룹에 Azure AD 항목 그룹을 통해 액세스를 관리 하에 자세한 정보를 제공 합니다. |Active Directory id 동기화 및 페더레이션 통해 hello 클라우드로 확장 |

## <a name="role-based-access-control"></a>역할 기반 액세스 제어
역할을 사용 하 여 역할 기반 액세스 제어 (RBAC) 및 테스트 정책 tooevaluate 프로 비전 및 비즈니스 프로세스 및 toousers 액세스 권한을 부여 하는 것에 대 한 규칙을 적용 합니다. 관리자 키 프로 비전 정책을 만들고 사용자 tooroles 할당 하 고 이러한 역할에 대 한 자격 tooresources의 집합을 정의 하는 합니다. RBAC는 hello id 관리 솔루션 toouse 소프트웨어 기반 프로세스를 확장 하 고 hello 프로 비전 프로세스에서에서 사용자 수동 상호 작용을 줄입니다.
Azure AD의 RBAC hello 회사 toorestrict hello 양을 개인 액세스 tooAzure 관리 포털에 그 후 작업을 수행할 수 있는 작업 수 있습니다. RBAC toocontrol 액세스 toohello 포털을 사용 하 여 액세스 관리를 수행 하는 hello를 사용 하 여 IT 관리자는 다음 ca 대리인 액세스 가까워지면:

* **그룹 기반 역할 할당**: 로컬 Active Directory에서 대 한 액세스 동기화 할 수 있는 tooAzure AD 그룹을 할당할 수 있습니다. 이렇게 하면 도구 및 그룹 관리 하기 위한 프로세스에서 조직 변경한 tooleverage hello 기존 투자 있습니다. 또한 Azure AD Premium의 hello 위임 된 그룹 관리 기능을 사용할 수 있습니다.
* **Azure에서 역할에 기본 제공 활용**: 세 가지 역할을 사용할 수 있습니다-사용자 및 그룹 권한 toodo hello 작업만 toodo 업무 필요한 한지 소유자, 참가자 및 독자 tooensure 합니다.
* **세부적인 액세스 tooresources**: 역할 toousers 및 특정 구독, 리소스 그룹 또는 웹 사이트 또는 데이터베이스와 같은 개별 Azure 리소스 그룹을 할당할 수 있습니다. 이러한 방식으로 필요한 tooall hello 리소스에 액세스 하 고 toomanage 필요 하지 않은 액세스 tooresources 없는 사용자가을 확인할 수 있습니다.

## <a name="provisioning-and-other-customization-options"></a>프로비전 및 기타 사용자 지정 옵션
팀에서 얼마나 많은 toocustomize hello id 솔루션 비즈니스 계획 및 요구 사항 toodecide 사용할 수입니다. 예를 들어 대기업은 증분 방식으로 여러 지역에 걸쳐 널리 사용되는 응용 프로그램의 프로비전에 대해 시간 표시 막대에 기반하는 워크플로 및 사용자 지정 어댑터에 관한 단계적인 롤아웃 계획이 필요할 수 있습니다. 다른 사용자 지정 계획에 대 한 테스트에 성공 하는 전체 조직 전체에서 사용자를 프로 비전 하는 두 개 이상의 응용 프로그램 toobe 제공할 수 있습니다. 사용자 응용 프로그램 상호 작용을 사용자 지정할 수 있습니다, 그리고 및 리소스를 프로 비전에 대 한 절차 변경 된 tooaccommodate 자동화 된 프로 비전 수 있습니다.

Tooremove 서비스 또는 구성 요소를 프로 비전 해제할 수 있습니다. 예를 들어 계정 프로 비전 해제 hello 계정 리소스에서 삭제 됨을 의미 합니다.

리소스 프로 비전의 hello 하이브리드 모델 요청 및 역할 기반 접근 방식을 모두 Azure AD에 의해 지원 되며 결합 합니다. 직원 또는 관리 되는 시스템의 하위 집합, 비즈니스 역할 기반 할당을 사용 하 여 tooautomate 액세스를 원할 수 있습니다. 또한 비즈니스가 다른 모든 액세스 요청 또는 요청 기반 모델을 통한 예외를 처리할 수 있습니다. 일부 비즈니스는 수동 할당부터 시작하여 나중에 완벽하게 역할 기반 배포를 목표로 하는 하이브리드 모델로 발전할 수 있습니다.

다른 회사를 할 때 비현실적 비즈니스 이유 tooachieve 전체 역할 기반 프로 비전 및 혼합 접근 방식 대상에 대 한 목표를 필요에 맞게으로. 다른 회사를 여전히 수도 프로비저닝 요청 기반 만족 해 및 하지 tooinvest 노력 toodefine 있으며 역할을 기준으로, 자동화 된 프로 비전 정책을 관리 합니다.

## <a name="license-management"></a>라이선스 관리
Azure AD에서 그룹 기반의 라이선스 관리 사용자 tooa 보안 그룹에 할당 하는 관리자가 수행할 수 있습니다 및 Azure AD를 자동으로 할당 라이선스 hello 그룹의 tooall hello 구성원입니다. 사용자 추가, 이후에 hello 그룹에서 제거 되거나, 경우 라이선스는 자동으로 할당 / 제거할 적절 하 게 합니다.

온-프레미스 AD에서 동기화하고 또는 Azure AD에서 관리한 그룹을 사용할 수 있습니다. Azure AD premium 셀프 서비스 그룹 관리 쌍이 라이선스 할당 toohello 적절 한 의사 결정권자 쉽게 위임할 수 있습니다. 라이선스 충돌 및 누락  위치 데이터와 같은 문제는 자동으로 분류될 수 있습니다.

## <a name="self-regulating-user-administration"></a>자동 조절 사용자 관리
조직의 모든 내부 조직 tooprovision 리소스를 시작할 때 hello 자체적으로 조절 사용자 관리 기능을 구현 합니다. 조직의 경계를 넘어 hello 장점 및 프로 비전 하는 사용자의 이점을 극대화할 수 있습니다. 이 환경에서 사용자의 상태 변경은 조직의 경계 및 지역을 넘어 액세스에 자동으로 반영됩니다. 프로 비전 비용을 줄일 수 있으며 hello 액세스 및 승인 프로세스를 간소화할 수 있습니다. hello 구현을 인식 hello 잠재력을 조직에서 종단 간 액세스 관리에 대 한 역할 기반 액세스 제어를 구현 합니다. 사용자 프로비전의 관리에 대한 자동화된 절차를 통해 관리 비용을 줄일 수 있습니다. 보안 정책을 자동으로 적용하여 보안을 향상하고 대형 사용자 모집단에 대한 사용자 수명 주기 관리 및 리소스 프로비전을 효율적으로 중앙 집중화시킬 수 있습니다.

> [!NOTE]
> 자세한 내용은 셀프 서비스 응용 프로그램 액세스 관리를 위해 Azure AD 설정을 참조하세요.
> 
> 

라이선스 기반(자격 기반) Azure AD 서비스는 Azure AD 디렉터리/서비스 테넌트에서 구독을 활성화하면 작동됩니다. Hello 구독 옵션이 활성화 되 면 hello 서비스 기능을 디렉터리/서비스 관리자에 의해 관리 하 고 사용이 허가 된 사용자가 사용할 수 있습니다. 자세한 내용은 Azure AD 라이선스 작업을 수행하는 방법을 참조하세요.
다른 타사 공급 업체와 통합

Azure Active Directory에 단일 로그인을 제공 하 고 SaaS 응용 프로그램 및 온-프레미스 웹 응용 프로그램의 응용 프로그램 액세스 보안 toothousands 강화 합니다. 자세한 목록은 지원 되는 SaaS 응용 프로그램에 대 한 Azure Active Directory 응용 프로그램 갤러리를 Azure Active Directory 페더레이션 호환성 목록 참조: tooimplement 사용된 될 수 있는 타사 id 공급자 single sign on

## <a name="define-synchronization-management"></a>동기화 관리 정의
Azure AD와 온-프레미스 디렉터리를 통합하면 온-프레미스 및 클라우드 리소스 모두에 액세스하기 위한 일반적인 ID를 제공하므로 사용자가 더 생산성을 높일 수 있습니다. 이러한 통합 된 사용자와 조직에서는 활용할 수 hello 다음:

* 조직에서는 온-프레미스 또는 클라우드 기반 서비스 Windows Server Active Directory를 활용 하 고 다음 tooAzure Active Directory를 연결에서 일반적인 하이브리드 id 가진 사용자가 제공할 수 있습니다.
* 관리자는 응용 프로그램 리소스, 장치 및 사용자 ID, 네트워크 위치, 다단계 인증 등을 기반으로 조건부 액세스를 제공할 수 있습니다.
* 사용자가 Azure AD tooOffice 365, Intune, SaaS 응용 프로그램 및 타사 응용 프로그램에서에서 계정을 통해 일반적인 id를 활용할 수 있습니다.
* 개발자가 응용 프로그램 빌드할 수 hello 일반적인 id 모델을 활용 하는 클라우드 기반 응용 프로그램에 대 한 Active Directory 온-프레미스 또는 Azure에 응용 프로그램 통합

hello 다음 그림에는 identity 동기화 프로세스를 간략하게의 예입니다.

![](./media/hybrid-id-design-considerations/identitysync.png)

ID 동기화 프로세스

다음 테이블 toocompare hello 동기화 옵션 검토 hello:

| 동기화 관리 옵션 | 장점 | 단점 |
| --- | --- | --- |
| 동기화 기반(DirSync 또는 AADConnect를 통해) |온-프레미스 및 클라우드에서 동기화된 사용자 및 그룹  <br>  **정책 제어**: hello 관리자 hello 기능 toomanage 암호 정책, 워크스테이션, 제한 사항, 잠금 컨트롤을 제공 하며, Active Directory를 통해 그리고 tooperform 추가 하지 않고도 더 계정 정책을 설정할 수 있습니다 hello 클라우드에서 작업 합니다.  <br>  **액세스 제어**: hello 서비스 온라인 서버 중 하나 또는 모두를 통해 회사 환경에서 hello 통해 액세스할 수 있도록 액세스 toohello 클라우드 서비스를 제한할 수 있습니다. <br>  지원 전화 감소: 가능성이 더 낮아집니다 tooforget는 게 더 적은 암호 tooremember 있으면 해당 합니다. <br>  보안: 사용자 id와 정보가 hello 서버와의 single sign-on을 사용 하는 서비스의 모든 마스터 때문에 보호 되 고 온-프레미스를 제어 합니다. <br>  강력한 인증 지원: hello 클라우드 서비스와 강력한 인증 (2 단계 인증이 라고도 함)를 사용할 수 있습니다. 그러나 강력한 인증을 사용하는 경우 Single Sign-On을 사용해야 합니다. | |
| 페더레이션 기반(AD FS를 통해) |보안 토큰 서비스(STS)에서 사용 가능. Microsoft 클라우드 서비스와는 STS tooprovide single sign-on 액세스를 구성한 경우 온-프레미스 STS 및 Azure AD 테 넌 트를 지정 하는 hello 페더레이션된 도메인 간의 페더레이션된 트러스트를 만들어야 합니다. <br> 최종 사용자가 자격 증명 tooobtain 액세스 toomultiple 리소스 집합이 동일한 toouse hello 허용 <br>최종 사용자가 없는 toomaintain 여러 자격 증명 집합입니다. 아직 hello 사용자가 tooprovide의 hello 참여 리소스, 하나의 자신의 자격 증명 tooeach B2B 및 B2C 시나리오를 지원 합니다. |전용 온-프레미스 AD FS 서버의 배포 및 유지 관리에 대한 전문 직원이 필요합니다. Toouse AD FS STS에 대 한 계획 하는 경우 강력한 인증 hello 사용 제한 사항이 있습니다. 자세한 내용은 [AD FS 2.0에 대한 고급 옵션 구성](http://go.microsoft.com/fwlink/?linkid=235649)을 참조하세요. |

> [!NOTE]
> 자세한 내용은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)을 참조하세요.
> 
> 

## <a name="see-also"></a>참고 항목
[설계 고려 사항 개요](active-directory-hybrid-identity-design-considerations-overview.md)

