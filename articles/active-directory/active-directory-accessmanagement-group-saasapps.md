---
title: "응용 프로그램 그룹 toomanage 액세스 tooSaaS aaaUsing | Microsoft Docs"
description: "어떻게 Azure Active Directory Premium 또는 Basic tooassign toouse 그룹 Azure Active Directory와 통합 된 tooSaaS 응용 프로그램에 액세스 합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a>그룹 toomanage 액세스 tooSaaS 응용 프로그램을 사용 하 여
Azure Active Directory (Azure AD)를 사용 하 여 Azure AD Premium 또는 Azure AD Basic 라이선스를 그룹 tooassign access tooa SaaS 응용 프로그램을 Azure AD와 통합을 사용할 수 있습니다. 예를 들어 hello 마케팅 부서 toouse 5 개의 서로 다른 SaaS 응용 프로그램에 대 한 tooassign 액세스 하려는 경우 있습니다 hello 마케팅 부서의 hello 사용자가 포함 하는 그룹을 만든 다음 해당 그룹 toothese 5 개 SaaS 응용 프로그램을 hello 마케팅 부서에서 필요합니다. 이러한 방식으로 hello 마케팅 부서의 한 곳에서의 hello 멤버 자격을 관리 하 여 시간을 절약할 수 있습니다. 사용자가 다음 때 할당 됩니다 toohello 응용 프로그램 hello 마케팅 그룹의 구성원으로 추가 되 고 할당 제거는 hello 응용 프로그램에서 hello 마케팅 그룹에서에서 제거 될 때.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. 

Hello Azure AD 응용 프로그램 갤러리 내에서 추가할 수 있는 수많은 응용 프로그램으로이 기능을 사용할 수 있습니다.

**그룹 tooa SaaS 응용 프로그램에 대 한 tooassign 액세스**

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory** hello hello 왼쪽 탐색 모음에 있습니다.
2. 선택 hello **디렉터리** 탭을 연 다음 hello 디렉터리 그룹 tooa SaaS 응용 프로그램에 대 한 액세스 tooassign 원하는 합니다.
3. 선택 hello **응용 프로그램** 탭 합니다. Hello 응용 프로그램 갤러리에서에서 추가 하는 응용 프로그램을 선택 하 고 클릭 hello **사용자 및 그룹** 탭 합니다.
4. Hello에 **사용자 및 그룹** hello 탭 **부터는** 필드 hello 이름을 입력 hello 그룹 toowhich의 tooassign 액세스 한 다음 선택 hello hello 오른쪽 위에 있는 확인 표시 합니다. 그룹의 이름의 tootype hello 첫 번째 부분을 하기만 하면 됩니다.
5. Hello 그룹을 선택 하 고 다음 hello 선택 **할당 액세스 권한** 단추입니다. 선택 **예** hello 확인 메시지가 표시 될 때입니다. 이 이번에 중첩 된 그룹 멤버 자격 그룹 기반 할당 tooapplications에 대 한 지원 되지 않습니다.
6. 직접 또는 그룹 멤버 자격에 따라 toohello 응용 프로그램에 할당 되는 사용자를 확인할 수도 있습니다. toodo이, 변경 hello **드롭다운 '그룹'에서 표시** 너무**' 모든 사용자**합니다. hello 목록 hello 디렉터리 및 여부는 각 사용자가 할당 된 toohello 응용 프로그램에 사용자가 표시 됩니다. hello 할당 된 사용자에 게 할당 toohello 응용 프로그램 직접 (할당 유형이 '직접'으로 표시), 있는지 아니면 그룹 멤버 자격 (할당 유형이 '상속 됨'으로 표시) hello 목록 표시

> [!NOTE]
> Azure AD Premium 또는 Azure AD Basic 사용 하도록 설정한 후에 hello 사용자 및 그룹 탭을 볼 수 있습니다.
>
>

### <a name="next-steps"></a>다음 단계
이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.

* [Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리](active-directory-manage-groups.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [그룹 설정을 구성하는 Azure Active Directory cmdlets](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Azure Active Directory란?](active-directory-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
