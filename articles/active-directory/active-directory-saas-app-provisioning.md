---
title: "aaaAutomated SaaS 응용 프로그램 사용자 프로 비전 Azure AD에서 | Microsoft Docs"
description: "Azure AD tooautomatically 프로 비전을 사용할 수 있는 소개 toohow 프로 비전 해제할 및 지속적으로 여러 타사 SaaS 응용 프로그램에서 사용자 계정을 업데이트 합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 58c5fa2d-bb33-4fba-8742-4441adf2cb62
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: curtand
ms.openlocfilehash: a1f3ecdd513e2b603f8ad9901e9f551b3b982b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-toosaas-applications-with-azure-active-directory"></a>사용자 프로 비전 및 Azure Active Directory와 tooSaaS 응용 프로그램을 프로 비전 해제를 자동화 합니다.
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>SaaS 앱을 위한 자동 사용자 프로비저닝이란?
Azure Active Directory (Azure AD) 사용 하면 tooautomate hello, 유지 관리 작업의 생성 및 제거의 클라우드 사용자 id ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) Dropbox, Salesforce, ServiceNow, 등 응용 프로그램입니다.

**다음은 어떤이 기능을 통해 toodo의 몇 가지 예:**

* 자동으로 새 계정을 만듭니다 hello에 오른쪽 SaaS 앱 새 사용자를 위해 팀에 가입할 때.
* 사람 hello 팀 필연적으로 나갈 때 자동으로 SaaS 응용 프로그램에서 계정을 비활성화 합니다.
* SaaS 앱에 hello id hello 디렉터리의 변화에 따라 toodate 위로 유지 되 확인 합니다.
* 그룹을 지 원하는 tooSaaS 앱 등 비 사용자 개체 프로 비전 합니다.

**자동된 사용자 프로 비전 기능을 수행 하는 hello를 포함 되어 있습니다.**

* Azure AD 간의 기능 toomatch 기존 id hello SaaS 응용 프로그램 및입니다.
* 사용자 지정 옵션 toohelp Azure AD 조직에서 현재 사용 하는 hello SaaS 앱의 현재 구성을 hello 정도입니다.
* 프로비전닝 오류를 전자 메일로 받을 수 있는 선택적 기능.
* 모니터링 및 문제 해결 로그 toohelp 보고 및 활동입니다.

## <a name="why-use-automated-provisioning"></a>자동 프로비저닝을 사용하는 이유
이 기능을 사용하게 되는 일반적인 동기는 다음과 같습니다.

* tooavoid hello 비용, 비효율성을 및 수동 프로세스 배포와 관련 된 사람의 오류입니다.
* toosecure 조직에서 사용자의 id를 즉시 제거 하 여 hello 조직을 떠날 때 SaaS 앱 키입니다.
* tooeasily 특정 SaaS 응용 프로그램에 사용자 수가 경우 대량 가져오기
* tooenjoy hello 편리 하 게 hello에서 실행 하 여 프로 비전 솔루션을 갖추는 것 같은 응용 프로그램 액세스 정책에 대 한 Azure AD Single Sign-on 정의 있습니다.

## <a name="frequently-asked-questions"></a>질문과 대답
**Azure AD 디렉터리 변경 내용이 toohello SaaS 앱을 작성 하는 빈도**

Azure AD 변경 tooten는 5 분 마다 확인합니다. Hello SaaS 앱 여러 오류 (예: 잘못 된 관리자 자격 증명의 대/소문자 hello)를 반환 하는 경우 Azure AD에는 해당 주파수 tooup tooonce hello 오류가 해결 되기 전 까지는 하루 서서히 늦출 됩니다.

**얼마나 오래 걸리는 tooprovision 내 사용자가?**

증분 변경이 tooprovision를 시도 하는 경우를 제외한 거의 즉시 발생 대부분의 디렉터리에 다음 사용자 및 그룹 해야 하는 hello 수에 따라 달라 집니다. 작은 디렉터리는 1 ~ 2분 정도, 중간 규모의 디렉터리는 몇 분 정도, 매우 큰 디렉터리의 경우는 몇 시간까지 걸릴 수 있습니다.

**Hello 현재 프로 비전 작업의 hello 진행률을 추적 하려면 어떻게 해야 합니까?**

디렉터리의 hello 보고서 섹션에서 계정 프로 비전 보고서 hello를 검토할 수 있습니다. 또 다른 옵션 hello 프로 비전 하는 SaaS 응용 프로그램에 대 한 toovisit hello 대시보드 탭 이며 hello hello hello 페이지 아래쪽 근처 "상태를 통합" 섹션에서 찾아봅니다.

**사용자가 tooget 제대로 프로 비전 실패 하는 경우 어떻게 알 수는?**

Hello hello 끝나기 전에 프로 비전 구성 있습니다 되었습니다 오류 프로 비전 하기 위한 옵션 toosubscribe tooemail 알림. Hello 프로 비전 오류 보고서 toosee 있는 사용자를 프로 비전 toobe 실패를 확인할 수 있습니다 및 이유입니다.

**Azure AD hello SaaS 앱 백 toohello 디렉터리에서 변경 내용을 쓸 수 있습니까?**

대부분의 SaaS 응용 프로그램 프로 비전은 아웃 바운드 전용 이며 따라서 hello 디렉터리 toohello 응용 프로그램에서 사용자가 기록 되 고 hello 응용 프로그램의 변경 내용을 쓸 수 없는 다시 toohello 디렉터리입니다. 그러나에 대 한 [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx), 프로 비전은 인바운드 전용 사용자가 Workday에서 hello 디렉터리로 가져올 하지 않음을 의미와 마찬가지로, hello 디렉터리의 변경 내용을 수행 쓰지 다시 Workday에 있습니다.

**엔지니어링 팀에서 피드백 toohello 보내려면 어떻게 해야 합니까?**

Hello를 통해 문의해 주십시오 [Azure Active Directory 피드백 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/)합니다.

## <a name="how-does-automated-provisioning-work"></a>자동 프로비저닝은 어떻게 수행됩니까?
각 응용 프로그램 공급 업체에서 제공 하는 tooprovisioning 끝점을 연결 하 여 azure AD에 사용자가 tooSaaS 앱 프로 비전 합니다. 이러한 끝점 허용 Azure AD tooprogrammatically 생성, 업데이트 및 사용자를 제거 합니다. 아래 hello의 간략 한 개요를 Azure AD는 tooautomate 프로 비전을 사용 하는 다른 단계는입니다.

1. 응용 프로그램에 대해 hello에 대 한 처음 프로 비전을 사용 하면 작업을 수행 하는 hello 수행 됩니다.
   * Azure AD toomatch hello 디렉터리의 해당 id가 있는 hello SaaS 응용 프로그램에서 기존 사용자를 시도 합니다. 사용자가 일치하는 경우 Single Sign-On에 대해 자동으로 사용하지 *않도록* 설정됩니다. 사용자 toohave 액세스 toohello 응용 프로그램을 위해 명시적으로 할당 해야 toohello 앱 Azure AD에서 직접적으로 또는 그룹 구성원 자격으로 합니다.
   * 어떤 사용자만 할당 해야 toohello 응용 프로그램을 이미 지정한 고 Azure AD에는 해당 사용자에 대 한 기존 계정을 toofind 실패 하면 Azure AD에서는에 새 계정의 hello 응용 프로그램에 제공 합니다.
2. 위에서 설명한 것 처럼 hello 초기 동기화 완료 되 면 되 면 Azure AD는 다음 변경 내용을 hello에 대 일 분 마다 확인:
   * 새 할당 된 사용자가 toohello 응용 프로그램 (직접 또는 그룹 구성원 자격을 통해), 경우 됩니다 hello SaaS 응용 프로그램에서 새 계정을 프로 비전 합니다.
   * 사용자의 액세스 제거 된 경우 hello SaaS 응용 프로그램에서 자신의 계정 사용 안 함으로 표시 됩니다 (사용자가 완전히 삭제 잘못 된 구성의 hello 이벤트에서 데이터 손실 로부터 보호 하).
   * 사용자 toohello 응용 프로그램을 최근에 할당 된 경우 이미 가진 hello SaaS 응용 프로그램에서에서 계정 계정이 사용 되도록 설정으로 표시 됩니다 및 오래 된 비교 toohello 디렉터리 경우 특정 사용자 속성을 업데이트할 수 있습니다.
   * 사용자의 정보 (예: 전화 번호, 사무실 위치 등) hello 디렉터리에 변경 된 경우 해당 정보가 hello SaaS 응용 프로그램에서에서 업데이트도 됩니다.

특성이 Azure AD 간에 매핑되는 방법에 대 한 자세한 내용은 SaaS 응용 프로그램에 hello 문서를 참조 하 고 [특성 매핑 사용자 지정](active-directory-saas-customizing-attribute-mappings.md)합니다.

## <a name="list-of-apps-that-support-automated-user-provisioning"></a>자동 사용자 프로비저닝을 지원하는 앱 목록
Hello Azure AD 응용 프로그램 갤러리에 있는 hello "주요" 앱의 모든 자동화 된 사용자 프로 비전을 지원합니다. [기능 갖춘된 앱의 hello 목록이 여기에서 볼 수 있습니다.](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

응용 프로그램 toosupport 자동된 사용자 프로 비전을 위해 먼저 제공 해야 hello 외부 프로그램 tooautomate hello 생성, 유지 관리, 사용자 및 제거에 대 한 허용 하는 데 필요한 끝점. 따라서 모든 SaaS 앱이 이 기능과 호환되지는 않습니다. 이 지원 않는 응용 프로그램의 경우 hello Azure AD 엔지니어링 팀 다음 수 toobuild 프로비저닝 커넥터 toothose 응용 프로그램, 되며이 작업은 현재 및 잠재 고객의 hello 요구 사항에 따라 우선 순위가 지정 되어 있습니다.

toocontact hello Azure AD 엔지니어링 팀에 추가 응용 프로그램에 대 한 지원을 프로 비전 toorequest 팀, hello 통해 메시지를 보내 주십시오 [Azure Active Directory 피드백 포럼](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning)합니다.

## <a name="related-articles"></a>관련 문서
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [사용자 프로비저닝에 대한 특성 매핑 사용자 지정](active-directory-saas-customizing-attribute-mappings.md)
* [특성 매핑에 대한 식 작성](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [사용자 프로 비전에 대 한 필터 범위 지정](active-directory-saas-scoping-filters.md)
* [SCIM tooenable 자동으로 프로 tooapplications Azure Active Directory에서에서 사용자 및 그룹을 사용 하 여](active-directory-scim-provisioning.md)
* [계정 프로비전 알림](active-directory-saas-account-provisioning-notifications.md)
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱](active-directory-saas-tutorial-list.md)

