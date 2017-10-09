---
title: "aaaNo 사용자 프로 비전 된 Azure AD tooan 갤러리 응용 프로그램 되는 | Microsoft Docs"
description: "Tootroubleshoot 일반적인 문제에 나타나는 사용자 표시 되지 않는 경우를 처리 하는 방법을 Azure AD는 사용자가 Azure AD에 프로 비전에 대 한 구성한 갤러리 응용 프로그램"
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
ms.date: 05/04/2017
ms.author: asteen
ms.openlocfilehash: 4d9693a202ed657e1de5571b50e5d499bef1bb3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="no-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>사용자를 프로 비전 된 Azure AD tooan 갤러리 응용 프로그램

한 번 자동 프로 비전 하는 등는 hello 앱 자격 증명을 제공 tooAzure AD tooconnect toohello 앱이 올바른지 확인 하는 응용 프로그램에 대해 구성 되어 있습니다. 그런 다음 사용자 및/또는 그룹 프로 비전 된 toohello 앱 이며 hello 작업 다음에 의해 결정 됩니다.

-   사용자 및 그룹은 되는 **할당** toohello 응용 프로그램입니다. 할당에 대 한 자세한 내용은 참조 하십시오. [Azure Active Directory에서 사용자 또는 그룹 tooan 엔터프라이즈 앱 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)합니다.

-   여부 **특성 매핑을** 은 Azure AD toohello 앱에서 구성 하 고 활성화 toosync 유효한 특성입니다. 특성 매핑에 대한 자세한 내용은 [Azure Active Directory에서 SaaS 응용 프로그램에 대한 사용자 프로비전 특성 매핑 사용자 지정](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)을 참조하세요.

-   특정 특성 값을 기반으로 사용자를 필터링하는 **범위 지정 필터**가 있는지 여부. 범위 지정 필터에 대한 자세한 내용은 [범위 지정 필터를 사용한 특성 기반 응용 프로그램 프로비전](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters)을 참조하세요.

사용자가 제공 되는 관찰 하는 경우 Azure AD에서 hello 감사 로그를 참조 한 특정 사용자에 대 한 로그 항목에 대 한 검색 합니다.

감사 로그를 프로 비전 하는 hello hello hello에서 Azure 포털에에서 액세스할 수 있습니다 **Azure Active Directory &gt; 엔터프라이즈 앱 &gt; \[응용 프로그램 이름\] &gt; 감사 로그**탭 합니다. 필터 hello hello 로그온 **계정 프로 비전** 범주 tooonly hello 이러한 앱에 대 한 이벤트를 프로 비전을 참조 하십시오. ID에 따라 hello "일치 하는" hello 특성 매핑을에 구성 된 사용자에 대 한 검색할 수 있습니다. 예를 들어 hello "사용자 계정 이름" 또는 "전자 메일 주소" hello Azure AD 쪽에서 특성을 일치 하는 hello로 구성 했으며 hello 사용자 프로 비전이 아닌 값이 "audrey@contoso.com"입니다. 다음에 대 한 hello 감사 로그를 검색 "audrey@contoso.com" 하 고 검토 한 다음 항목을 반환 합니다.

감사를 프로 비전 하는 hello 모든 hello Azure AD에서 프로 비전, 해당 사용자의 존재 여부 hello에 대 한 hello 대상 응용 프로그램을 쿼리, hello 비교에 대 한 범위에 있는 할당 된 사용자에 대 한 쿼리를 포함 하 여 hello 프로 비전 서비스에 의해 수행 된 작업 레코드를 기록 합니다. hello 시스템 사이 사용자 개체입니다. 그런 다음 추가, 업데이트 또는 hello 비교 기반 hello 대상 시스템에 사용자 계정을 hello를 사용 하지 않도록 설정 합니다.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>일반적인 문제 영역 tooconsider 프로비저닝

다음 목록은 hello where의 방법이 있는 경우 드릴 수 있는 일반적인 문제 영역 toostart 합니다.

* [서비스를 프로 비전 toostart 표시 되지 않습니다.](#provisioning-service-does-not-appear-to-start)
* [사용자가 할당된 경우에도 감사 로그에 사용자가 생략되고 프로비전되지 않았다고 표시됨](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>서비스를 프로 비전 toostart 표시 되지 않습니다.

Hello를 설정한 경우 **프로 비전 상태** toobe **에** hello에 **Azure Active Directory &gt; 엔터프라이즈 앱 &gt; \[응용프로그램이름\] &gt;프로 비전** hello Azure 포털의 섹션입니다. 그러나 다른 상태 세부 정보 페이지에 표시 됩니다 해당 후속 다시 로드 한 후 될 hello 서비스가 실행 되 고 있지만 아직 초기 동기화가 완료 되지 않았습니다. Hello 확인 **감사 로그** toodetermine 위에서 설명한 작업 hello 서비스를 수행 하 고 모든 오류가 있는 경우.

>[!NOTE]
>초기 동기화는 hello Azure AD 디렉터리와 hello 사용자 프로 비전에 대 한 범위에가 수의 hello 크기에 따라 20 분 tooseveral 시간이 걸릴 수 있습니다. Hello 초기 동기화 후 후속 동기화는 경우 더욱 빠릅니다을 hello로 hello 초기 동기화 후 두 시스템의 hello 상태를 나타내는 워터 마크 저장 서비스를 프로 비전 하십시오. 이를 통해 후속 동기화의 성능이 향상됩니다.
>
>

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>사용자가 할당된 경우에도 감사 로그에 사용자가 생략되고 프로비전되지 않았다고 표시됨

사용자는 hello 감사 로그에서 "무시" 됨으로 표시 때 매우 중요 한 tooread hello hello 로그 메시지 toodetermine hello 이유에서 세부 정보를 확장 합니다. 다음은 일반적인 원인과 해결 방법입니다.

-   **범위 지정 필터를 구성한** **는 필터링 hello 사용자 특성 값에 따라**합니다. 범위 지정 필터에 대한 자세한 내용은 <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>를 참조하세요.

-   **hello 사용자는 "없습니다 효율적으로 조직이 권한을 부여 받은"입니다.** 이 특정 오류 메시지가 나타나면 Azure AD에 저장 하는 hello 사용자 할당 레코드에 문제가 있기 때문에 합니다. toofix이 문제를 할당 해제 hello 앱에서 사용자 (또는 그룹) hello 및 다시 다시 할당 합니다. 할당에 대한 자세한 내용은 <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>을 참조하세요.

-   **사용자에게 필요한 특성이 누락되었거나 입력되지 않았습니다.** Tooreview 수 프로 비전을 설정 하는 경우에 중요 한 사항은 tooconsider 및 hello 특성 매핑 및 Azure AD toohello 응용 프로그램에서 어떤 사용자 (또는 그룹) 속성 흐름을 정의 하는 워크플로 구성 합니다. Hello "일치 하는 속성"을 설정 사용된 toouniquely 수 식별 및 사용자/그룹 hello 두 시스템 간에 일치 합니다. 이 중요한 프로세스에 대한 자세한 내용은 [Azure Active Directory에서 SaaS 응용 프로그램에 대한 사용자 프로비전 특성 매핑 사용자 지정](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)을 참조하세요.

  * **특성 그룹에 대 한 매핑을:** hello 프로 비전 일부 응용 프로그램에 대 한 지원 되는 경우 추가 toohello 멤버의 이름과 그룹 세부 정보를 그룹화 합니다. Hello를 사용 하지 않도록 설정 하거나 설정 하 여이 기능을 해제 하거나 설정할 수 있습니다 **매핑** hello에 표시 된 그룹 개체에 대 한 **프로 비전** 탭 합니다. 그룹을 프로 비전을 사용 하는 경우 tooreview hello 특성 매핑을 tooensure를 적절 한 필드 "일치 하는 ID" hello에 사용 되 고 있어야 합니다. 이 사용 가능 hello 표시 이름이 나 메일 별칭)을 hello 그룹 및 해당 멤버를 프로 비전 할 경우 hello 대로 속성을 일치 하는 비어 있거나 없습니다 채워진 그룹에 대 한 Azure AD에서 합니다.

## <a name="next-steps"></a>다음 단계
[Azure AD Connect 동기화: 선언적 프로비전 이해](active-directory-aadconnectsync-understanding-declarative-provisioning.md)

