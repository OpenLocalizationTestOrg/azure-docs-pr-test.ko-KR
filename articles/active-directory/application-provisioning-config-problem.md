---
title: "Azure AD tooan 갤러리 응용 프로그램 프로 비전 하는 사용자 구성 aaaProblem | Microsoft Docs"
description: "Tootroubleshoot 일반적인 문제 hello Azure AD 응용 프로그램 갤러리에 이미 나열 되어 tooan 응용 프로그램 프로 비전 하는 사용자를 구성할 때 직면 하는 방법"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 19b12be019b05faecef74c6f92a9de03b52a5ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-user-provisioning-tooan-azure-ad-gallery-application"></a>Azure AD tooan 갤러리 응용 프로그램 프로 비전 하는 사용자를 구성 하는 문제

구성 [자동 사용자 프로 비전](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning) 응용 프로그램 (지원) 하는 경우, 특정 한 지침이 자동 프로 비전 하기 위해 열어 tooprepare hello 응용 프로그램 이어야 합니다. 그런 다음 hello Azure 포털 tooconfigure hello 서비스 toosynchronize 사용자 계정 toohello 응용 프로그램을 프로 비전을 사용할 수 있습니다.

Hello 설치 자습서 특정 toosetting 응용 프로그램에 대 한 프로 비전을 검색 하 여 시작 하는 항상 해야 합니다. 그런 다음 이러한 단계 tooconfigure 모두 hello 앱 따르고 Azure AD toocreate hello 프로비저닝 연결 합니다. 응용 프로그램 자습서의 목록에 있습니다 [방법에 대 한 자습서의 목록 tooIntegrate SaaS 앱 Azure Active Directory와](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)합니다.

## <a name="how-toosee-if-provisioning-is-working"></a>Toosee 프로 비전 하는 경우이 작동 하는 방법 

Hello 서비스 구성 되 면 두 위치에서 hello 서비스의 hello 작업에 대 한 정보 대부분을 그릴 수 있습니다.

-   **감사 로그** – hello 프로 비전에 대 한 범위에 있는 사용자가 할당 된 Azure AD에서 쿼리를 포함 하 여 hello 서비스를 구축 하 여 모든 hello 작업이 수행 하는 감사 로그 레코드를 프로 비전 합니다. Hello 시스템 간에 hello 사용자 개체를 비교 합니다. 해당 사용자의 존재 여부 hello에 대 한 hello 대상 응용 프로그램을 쿼리 합니다. 그런 다음 추가, 업데이트 또는 hello 비교 기반 hello 대상 시스템에 사용자 계정을 hello를 사용 하지 않도록 설정 합니다. 감사 로그를 프로 비전 하는 hello hello hello에서 Azure 포털에에서 액세스할 수 있습니다 **Azure Active Directory &gt; 엔터프라이즈 앱 &gt; \[응용 프로그램 이름\] &gt; 감사 로그**탭 합니다. 필터 hello hello 로그온 **계정 프로 비전** 범주 tooonly hello 이러한 앱에 대 한 이벤트를 프로 비전을 참조 하십시오.

-   **프로 비전 상태 –** hello에서 지정된 된 앱을 볼 수 있습니다에 대 한 hello 마지막 프로 비전의 요약 실행할 **Azure Active Directory &gt; 엔터프라이즈 앱 &gt; \[응용 프로그램 이름\] &gt; 프로 비전** 섹션 hello hello 서비스 설정에서 hello 화면 맨 아래에 있습니다. 이 섹션에는 개수 사용자 (및/또는 그룹) 현재 동기화 중인 hello 간의 두 시스템 및 모든 오류가 요약 되어 있습니다. Hello 감사 로그에 오류 정보 수 있습니다. 프로 비전 상태 hello를 채우지 Azure AD 간에 한 번의 전체 초기 동기화 완료 될 때까지 hello 응용 프로그램 및입니다.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>일반적인 문제 영역 tooconsider 프로비저닝

다음 목록은 hello where의 방법이 있는 경우 드릴 수 있는 일반적인 문제 영역 toostart 합니다.

* [서비스를 프로 비전 toostart 표시 되지 않습니다.](#provisioning-service-does-not-appear-to-start)
* [작동 하지 않는 tooapp 자격 증명 때문에 구성을 저장할 수 없습니다.](#can’t-save-configuration-due-to-app-credentials-not-working)
* [사용자가 할당된 경우에도 감사 로그에 사용자가 “생략”되고 프로비전되지 않았다고 표시됨](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>서비스를 프로 비전 toostart 표시 되지 않습니다.

Hello를 설정한 경우 **프로 비전 상태** toobe **에** hello에 **Azure Active Directory &gt; 엔터프라이즈 앱 &gt; \[응용프로그램이름\] &gt;프로 비전** hello Azure 포털의 섹션입니다. 그러나 이후 다시 로드 후 기타 상태 세부 정보가 표시되지 않습니다. Hello 서비스가 실행 되 고 있지만 아직 초기 동기화가 완료 되지 않은 가능성이 높습니다. Hello 확인 **감사 로그** toodetermine 위에서 설명한 작업 hello 서비스를 수행 하 고 모든 오류가 있는 경우.

>[!NOTE]
>초기 동기화는 hello Azure AD 디렉터리와 hello 사용자 프로 비전에 대 한 범위에가 수의 hello 크기에 따라 20 분 tooseveral 시간이 걸릴 수 있습니다. Hello 초기 동기화 후 후속 동기화 서비스를 프로 비전 하는 hello 후속 동기화 성능을 향상 시킬 수 hello 초기 동기화 후 두 시스템의 hello 상태를 나타내는 워터 마크를 저장 하는 대로 속도가 더 빨라지며 합니다.
>
>

## <a name="cant-save-configuration-due-tooapp-credentials-not-working"></a>작동 하지 않는 tooapp 자격 증명 때문에 구성을 저장할 수 없습니다.

프로 비전 toowork 위해 Azure AD 앱에서 제공 하는 API tooconnect tooa 사용자 관리를 허용 하는 유효한 자격 증명이 필요 합니다. 이러한 자격 증명 작동 하지 않습니다는 wat 알 수 없는 경우이 응용 프로그램에서는 앞에서 설명한 설정에 대 한 hello 자습서를 검토 합니다.

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>사용자가 할당된 경우에도 감사 로그에 사용자가 생략되고 프로비전되지 않았다고 표시됨

사용자는 hello 감사 로그에서 "무시" 됨으로 표시 때 매우 중요 한 tooread hello hello 로그 메시지 toodetermine hello 이유에서 세부 정보를 확장 합니다. 다음은 일반적인 원인과 해결 방법입니다.

-   **범위 지정 필터를 구성한** **는 필터링 hello 사용자 특성 값에 따라**합니다. 범위 지정 필터에 대한 자세한 내용은 <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>를 참조하세요.

-   **hello 사용자는 "없습니다 효율적으로 조직이 권한을 부여 받은"입니다.** 이 특정 오류 메시지가 나타나면 Azure AD에 저장 하는 hello 사용자 할당 레코드에 문제가 있기 때문에 합니다. toofix이 문제를 할당 해제 hello 앱에서 사용자 (또는 그룹) hello 및 다시 다시 할당 합니다. 할당에 대한 자세한 내용은 <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>을 참조하세요.

-   **사용자에게 필요한 특성이 누락되었거나 입력되지 않았습니다.** Tooreview 수 프로 비전을 설정 하는 경우에 중요 한 사항은 tooconsider 및 hello 특성 매핑 및 Azure AD toohello 응용 프로그램에서 어떤 사용자 (또는 그룹) 속성 흐름을 정의 하는 워크플로 구성 합니다. Hello "일치 하는 속성"을 설정 사용된 toouniquely 수 식별 및 사용자/그룹 hello 두 시스템 간에 일치 합니다. 이 중요한 프로세스에 대한 자세한 내용은 <https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings>를 참조하세요.

   * **특성 그룹에 대 한 매핑을:** hello 프로 비전 일부 응용 프로그램에 대 한 지원 되는 경우 추가 toohello 멤버의 이름과 그룹 세부 정보를 그룹화 합니다. Hello를 사용 하지 않도록 설정 하거나 설정 하 여이 기능을 해제 하거나 설정할 수 있습니다 **매핑** hello에 표시 된 그룹 개체에 대 한 **프로 비전** 탭 합니다. 그룹을 프로 비전을 사용 하는 경우 tooreview hello 특성 매핑을 tooensure를 적절 한 필드 "일치 하는 ID" hello에 사용 되 고 있어야 합니다. 이 사용 가능 hello 표시 이름이 나 메일 별칭)을 hello 그룹 및 해당 멤버를 프로 비전 할 경우 hello 대로 속성을 일치 하는 비어 있거나 없습니다 채워진 그룹에 대 한 Azure AD에서 합니다.

#<a name="next-steps"></a>다음 단계
[사용자 프로 비전 및 프로 비전 해제 tooSaaS Azure Active Directory와 응용 프로그램 자동화](active-directory-saas-app-provisioning.md)
