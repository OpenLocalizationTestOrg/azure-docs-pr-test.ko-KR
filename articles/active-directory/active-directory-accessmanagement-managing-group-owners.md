---
title: "그룹을 사용하는 액세스 관리의 다음 단계 | Microsoft Docs"
description: "보안 그룹 관리에 대한 고급 방법과 이러한 그룹을 사용하여 리소스에 대한 액세스를 관리하는 방법입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a>그룹에 대한 소유자 관리
리소스 소유자가 Azure AD 그룹에 리소스에 대한 액세스 권한을 할당하면 그룹의 멤버 자격은 그룹 소유자에 의해 관리됩니다. 실질적으로 리소스 소유자는 사용자를 해당 리소스에 할당할 권한을 그룹 소유자에게 위임합니다.

> [!IMPORTANT]
> 이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다. 

## <a name="assigning-group-ownership"></a>그룹 소유권 할당
**그룹에 소유자를 추가하려면**

1. [Azure 클래식 포털](https://manage.windowsazure.com)에서 **Active Directory**를 선택한 다음 조직의 디렉터리를 엽니다.
2. **그룹** 탭을 선택하고 소유자를 추가할 편집할 그룹을 엽니다.
3. **소유자 추가**를 선택합니다.
4. **소유자 추가** 페이지에서 이 그룹의 소유자로 추가할 사용자를 선택하고 이 이름이 **선택 항목** 창에 추가되었는지 확인합니다.

**그룹에서 소유자를 제거하려면**

1. [Azure 클래식 포털](https://manage.windowsazure.com)에서 **Active Directory**를 선택한 다음 조직의 디렉터리를 엽니다.
2. **그룹** 탭을 선택하고 소유자를 제거할 그룹을 엽니다.
3. **소유자** 탭을 선택합니다.
4. 이 그룹에서 제거할 소유자를 선택한 후 **제거**를 선택합니다.

## <a name="additional-information"></a>추가 정보
이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.

* [Azure Active Directory 그룹을 사용하여 리소스에 대한 액세스 관리](active-directory-manage-groups.md)
* [그룹 설정을 구성하는 Azure Active Directory cmdlet](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [Azure Active Directory란?](active-directory-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
