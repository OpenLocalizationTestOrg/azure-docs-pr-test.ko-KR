---
title: "Azure Active Directory의 aaaDedicated 그룹 | Microsoft Docs"
description: "전용된 그룹의 Azure Active Directory를 사용한 작업 방식 및 작성된 방법의 개요입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Azure Active Directory의 전용 그룹
Azure Active Directory (Azure AD)에 hello 전용된 그룹 기능은 자동으로 만들고 미리 정의 된 Azure AD 그룹에 대 한 멤버 자격을 채웁니다. 전용된 그룹의 구성원을 추가할 수 없습니다 또는 Azure 클래식 포털에서 Windows PowerShell cmdlet을 환영 제거를 사용 하 여 또는 프로그래밍 방식으로 합니다.

> [!NOTE]
> 전용 그룹에는 할당된 Azure AD Premium 라이선스가 필요합니다.
>
> * hello 규칙 그룹에서 관리 하는 hello 관리자
> * hello로 선택 되는 모든 사용자 규칙 toobe hello 그룹의 구성원
>
>

**전용 tooenable 그룹**

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 한 다음 조직의 디렉터리를 엽니다.
2. 선택 hello **그룹** 탭을 선택한 tooedit 연 다음 hello 그룹입니다.
3. 선택 hello **구성** 탭을 클릭 한 다음 설정 **전용 그룹 사용** 너무**예**합니다.

전용 그룹 사용 전환 hello 너무 설정 되 고 나면**예**를 추가로 설정할 수 있습니다 hello 디렉터리 tooautomatically hello 설정 하 여 hello 모든 사용자에 게 전용된 그룹을 만들 **"모든 사용자" 그룹** 너무 전환**예**합니다. 그런 다음도 이름을 편집할 수 있습니다 hello 전용 그룹 hello에 입력 하 여 **"모든 사용자"에 대 한 표시 이름을 그룹** 필드입니다.

hello 모든 사용자 그룹을 사용할 수 있습니다 tooassign hello 디렉터리에 동일한 tooall hello 사용자 사용 권한입니다. 예를 들어 hello 모든 사용자에 게 전용된 그룹 toothis 응용 프로그램에 대 한 액세스를 할당 하 여 모든 사용자에 게 디렉터리 액세스 tooa SaaS 응용 프로그램에에서 부여할 수 있습니다.

게스트 및 외부 사용자를 포함 하 여 hello 디렉터리에 모든 사용자를 포함 하는 전용 hello 모든 사용자 그룹입니다. 그룹이 필요한 외부 사용자를 제외 하는 경우 hello 다음과 같은 특성 기반 동적 규칙 그룹을 만들면이 수행할 수 있습니다.

                (user.userPrincipalName -notContains "#EXT#@")

모든 게스트 제외 된 그룹에 대 한 hello 다음과 같은 규칙을 사용 합니다.

                (user.userType -ne "Guest")

방법에 대 한 toolearn toocreate *고급* 규칙 (여러 비교를 포함할 수 있는 규칙) 동적 그룹 멤버 자격에 대 한 참조 [toocreate 특성을 사용 하 여 고급 규칙](active-directory-accessmanagement-groups-with-advanced-rules.md)합니다.

### <a name="next-steps"></a>다음 단계
이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.

* [Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리](active-directory-manage-groups.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [Azure Active Directory란?](active-directory-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
