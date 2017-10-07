---
title: "AD DS와 Azure AD Connect Health aaaUsing | Microsoft Docs"
description: "이 hello Azure AD Connect Health 페이지에 설명 합니다를 어떻게 toomonitor AD DS 합니다."
services: active-directory
documentationcenter: 
author: arluca
manager: femila
editor: curtand
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e2fb6be65407d02c214dcab385b85d6cb54f48de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a>AD DS와 함께 Azure AD Connect Health 사용
hello 설명서에 Azure AD Connect Health를 특정 toomonitoring Active Directory 도메인 서비스입니다. AD DS의 hello 지원 버전은: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 및 Windows Server 2016 합니다.

Azure AD Connect Health를 사용한 AD FS 모니터링에 대한 자세한 내용은 [AD FS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adfs.md)을 참조하세요. 또한 Azure AD Connect Health와 함께 Azure AD Connect (동기화)를 모니터링하는 방법에 대한 정보는 [동기화를 위해 Azure AD Connect Health 사용](active-directory-aadconnect-health-sync.md)을 참조하세요.

![AD DS용 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a>AD DS용 Azure AD Connect Health에 대한 경고
AD DS에 대 한 Azure AD Connect Health에서 경고 섹션 hello, 관련된 tooyour 도메인 컨트롤러가 활성 및 해결 된 경고 목록을 제공 합니다. 활성 또는 해결 된 경고를 선택 하면 해결 단계를 함께 추가 정보를 사용는 새 블레이드가 열리고 toosupporting 설명서 링크. 각 경고 유형에 tooeach 해당 특정 경고로 영향 받는 hello 도메인 컨트롤러의 상응 하는 하나 이상의 인스턴스를 가질 수 있습니다. Hello 아래 근처의 hello 경고 블레이드, 영향을 받는 도메인 컨트롤러 tooopen 해당 경고 인스턴스에 대 한 자세한 정보는 추가 블레이드를 두 번 수 있습니다.

이 블레이드 내에서 경고에 대 한 전자 메일 알림을 사용 하도록 설정 하 고 보기에 hello 시간 범위를 변경할 수 있습니다. Hello 시간 범위를 확장 하면 toosee 이전 해결 된 경고입니다.

![Azure AD Connect 동기화 오류](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a>도메인 컨트롤러 대시보드
이 대시보드에서는 모니터링 도메인 컨트롤러 각각의 주요 작업 메트릭 및 상태와 함께 사용자 환경의 토폴로지 보기를 제공합니다. 제공 된 hello 메트릭 tooquickly 식별, 추가 조사 해야 할 수도 있는 모든 도메인 컨트롤러. 기본적으로 hello 열의 하위 집합만 표시 됩니다. 그러나 hello 열 명령을 두 번 클릭 하 여 hello 전체 집합이 사용 가능한 열을 찾을 수 있습니다. 가장 중요 한,이 대시보드를 하나의 쉽고 배치 AD DS 환경의 tooview hello 상태 turns hello 열을 선택 합니다.

![도메인 컨트롤러](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

도메인 컨트롤러의 각 도메인 또는 hello 환경 토폴로지를 이해 하는 데 도움이 되는 사이트를 그룹화 할 수 있습니다. 마지막으로, hello 블레이드 헤더를 두 번 클릭 hello 대시보드 tooutilize hello 사용 가능한-화면 공간을 최대화 합니다. 여러 열을 표시하는 경우 크게 볼수록 도움이 됩니다.

## <a name="replication-status-dashboard"></a>복제 상태 대시보드
이 대시보드는 hello 복제 상태 및 복제 토폴로지 모니터링 대상된 도메인 컨트롤러의 보기를 제공합니다. hello 가장 최근 복제 시도의 hello 상태 발견 된 모든 오류에 대 한 유용한 설명서와 함께 나열 됩니다. 그러면 해당 tooopen 정보로는 새 블레이드가 오류와 함께 도메인 컨트롤러와 같은: tootroubleshooting 설명서 링크 및 해결 단계를 권장 하는 hello 오류에 대 한 세부 정보입니다.

![복제 상태](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a>모니터링
이 기능은 각 모니터링 hello 도메인 컨트롤러에서 지속적으로 수집 되는 다양 한 성능 카운터의 추세를 그래픽에 대해 설명 합니다. 도메인 컨트롤러의 성능은 포리스트에 있는 다른 모든 모니터된 도메인 컨트롤러 간에 쉽게 비교될 수 있습니다. 또한 다양한 성능 카운터를 나란히 볼 수 있으며 환경에서 문제를 해결할 때 유용합니다.

![모니터링](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

기본적으로 우리는 미리 선택 되어 4 개의 성능 카운터입니다. 그러나 hello 필터 명령을 클릭 하 고 선택 하거나 원하는 성능 카운터를 선택 취소 하 여 다른을 포함할 수 있습니다. 또한 각 도메인 컨트롤러를 모니터링 하는 hello에 대 한 데이터 요소를 포함 하는 새 블레이드가 성능 카운터를 그래프 tooopen를 두 번 수 있습니다.

## <a name="related-links"></a>관련 링크
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health Agent 설치](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health 작업](active-directory-aadconnect-health-operations.md)
* [AD FS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adfs.md)
* [동기화에 대한 Azure AD Connect Health 사용](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health FAQ](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health 버전 내역](active-directory-aadconnect-health-version-history.md)

