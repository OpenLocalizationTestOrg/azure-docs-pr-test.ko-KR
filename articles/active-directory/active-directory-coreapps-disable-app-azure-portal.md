---
title: "aaaDisable 사용자 로그인에 대 한 Azure Active Directory에서 엔터프라이즈 응용 프로그램에서 | Microsoft Docs"
description: "어떻게 toodisable 엔터프라이즈 응용 프로그램 사용자가 없는 tooit Azure Active Directory에 로그인 수 있도록"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a>Azure Active Directory에서 엔터프라이즈 앱에 대한 사용자 로그인 비활성화
되 쉽게 toodisable 엔터프라이즈 응용 프로그램 사용자가 Azure Active Directory (Azure AD)에 tooit에 로그인 될 수 있습니다. Hello 디렉터리에 대 한 전역 관리자 여야 하며 hello 적절 한 사용 권한을 toomanage hello 엔터프라이즈 앱 있어야 합니다.

## <a name="how-do-i-disable-user-sign-ins"></a>사용자 로그인을 비활성화하려면 어떻게 합니까?
1. Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. 선택 **더 많은 서비스**, 입력 **Azure Active Directory** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.
3. Hello에 **Azure Active Directory** -  ***디렉터리 이름*** 블레이드 (관리 하는 hello 디렉터리에 대 한 즉, Azure AD hello 블레이드) 선택 **엔터프라이즈응용프로그램**.

    ![엔터프라이즈 앱 열기](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. Hello에 **엔터프라이즈 응용 프로그램** 블레이드를 **모든 응용 프로그램**합니다. Hello 앱을 관리할 수 목록을 표시 합니다.
5. Hello에 **엔터프라이즈 응용 프로그램-모든 응용 프로그램** 블레이드에서 응용 프로그램을 선택 합니다.
6. Hello에 ***appname*** 블레이드 (hello hello 제목에 선택 된 응용 프로그램의 hello 이름으로, 즉 hello 블레이드) 선택 **속성**합니다.

    ![모든 응용 프로그램 명령 hello 선택](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. Hello에 ***appname*** - **속성** 블레이드를 **아니요** 에 대 한 **toosign에서 사용자에 대해 활성화?**합니다.
8. 선택 hello **저장** 명령입니다.

## <a name="next-steps"></a>다음 단계
* [내 그룹 모두 보기](active-directory-groups-view-azure-portal.md)
* [사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당](active-directory-coreapps-assign-user-azure-portal.md)
* [엔터프라이즈 앱에서 사용자 또는 그룹 할당 제거](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Hello 이름 변경 또는 엔터프라이즈 응용 프로그램에서의 로고](active-directory-coreapps-change-app-logo-user-azure-portal.md)
