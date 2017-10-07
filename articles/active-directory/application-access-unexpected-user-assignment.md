---
title: "aaaHow tooAssign 사용자 tooapplications | Microsoft Docs"
description: "사용자가 테 넌 트에 tooan 응용 프로그램 가져오기 할당 하는 방법을 이해합니다"
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
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a>어떻게 tooassign 사용자 tooapplications

이 문서가 도움이 toounderstand 방법을 사용자가 테 넌 트에 응용 프로그램 tooan 할당 합니다.

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a>어떻게 사용자가 할당 않았는지 Azure AD에서 응용 프로그램 tooan?

사용자 tooaccess 응용 프로그램에 대 한 처음 할당 해야 어떤 방식으로든에서 tooit 합니다. 할당 수 수행한 관리자, 비즈니스 대리자 또는 경우에 따라서는 hello 사용자 자체. 아래 사용자도 tooapplications 할당 수 hello 방법에 설명 합니다.

1.  관리자가 [은 사용자를 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) 직접 toohello 응용 프로그램

2.  관리자 [그룹 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) 해당 hello 사용자가 toohello 응용 프로그램의 구성원 포함:

  * 온-프레미스에서 동기화된 그룹

  * Hello 클라우드에서 만든 정적 보안 그룹

  * A [동적 보안 그룹](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) hello 클라우드에서 만든

  * Hello 클라우드에서 만든는 Office 365 그룹

  * hello [모든 사용자에 게](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) 그룹

3.  관리자를 사용 하면 [셀프 서비스 응용 프로그램 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) hello를 사용 하 여 응용 프로그램 사용자 tooadd tooallow [응용 프로그램 액세스 패널로](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **앱 추가** 기능**비즈니스 승인 없이**

4.  관리자를 사용 하면 [셀프 서비스 응용 프로그램 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) hello를 사용 하 여 응용 프로그램 사용자 tooadd tooallow [응용 프로그램 액세스 패널로](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **앱 추가** 기능을 사용 하지만 w **선택한 비즈니스 승인자 집합에서 i 번째 사전 승인**

5.  관리자를 사용 하면 [셀프 서비스 그룹 관리](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow 사용자 toojoin 응용 프로그램은 너무 할당 그룹**비즈니스 승인 없이**

6.  관리자를 사용 하면 [셀프 서비스 그룹 관리](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow 사용자 toojoin 하지만 응용 프로그램에 할당 된 그룹 **선택된 된 비즈니스 승인자 집합의 사전 승인으로**

7.  관리자 할당 첫 번째 파티 응용 프로그램에 대 한 직접 라이선스 tooa 사용자 같은 [Microsoft Office 365](http://products.office.com/)

8.  Hello 사용자 라이선스 tooa 그룹 멤버인 tooa 첫 번째 파티와 응용 프로그램의 같은 프로그램 관리자 할당 [Microsoft Office 365](http://products.office.com/)

9.  [관리자가 tooan 응용 프로그램을 승인](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe 모든 사용자가 사용 하 고 toohello 응용 프로그램에서 사용자가 로그인 한 다음

10. 사용자 [tooan 응용 프로그램 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toohello 응용 프로그램에 로그인 하면 자체

## <a name="next-steps"></a>다음 단계
[Azure Active Directory로 응용 프로그램 관리](active-directory-enable-sso-scenario.md)
