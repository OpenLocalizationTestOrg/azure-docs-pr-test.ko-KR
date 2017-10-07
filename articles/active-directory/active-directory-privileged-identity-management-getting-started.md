---
title: "Azure AD Privileged Identity management 시작 aaaGet | Microsoft Docs"
description: "Toomanage hello Azure Active Directory Privileged Identity Management 응용 프로그램을 Azure 포털에서 id 특권 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: a89205023a8dbcc3649fa732735ca927e64736ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>Azure AD Privileged Identity Management 시작
Azure Active Directory(AD) Privileged Identity Management를 사용하여 조직 내에서 액세스를 관리, 제어 및 모니터링할 수 있습니다. 이 범위는 Azure AD에서 액세스 tooresources 및 Microsoft Intune 또는 Office 365와 같은 다른 Microsoft 온라인 서비스를 포함합니다.

이 문서는 어떻게 tooadd hello Azure AD PIM 앱 tooyour Azure 포털 대시보드에서 알려 줍니다.

## <a name="add-hello-privileged-identity-management-application"></a>Hello Privileged Identity Management 응용 프로그램 추가
Azure AD Privileged Identity Management를 사용 하기 전에 tooadd hello 응용 프로그램 tooyour Azure 포털 대시보드에서 해야 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/) 디렉터리의 전역 관리자입니다.
2. 조직에서 둘 이상의 디렉터리를 경우 hello hello Azure 포털의 상단 오른쪽 모서리에서 사용자 이름을 선택 합니다. PIM toouse 원하는 hello 디렉터리를 선택 합니다.
3. 선택 **더 많은 서비스** 에 대 한 필터 텍스트 상자에 붙여넣습니다 toosearch hello를 사용 하 여 **Azure AD Privileged Identity Management**합니다.
4. 확인 **Pin toodashboard** 클릭 하 고 **만들기**합니다. hello Privileged Identity Management 응용 프로그램을 엽니다.

Hello 디렉터리의 첫 번째 사람 toouse Azure AD Privileged Identity Management를 hello 하는, 하는 경우 자동으로 할당 됩니다 **보안 관리자** 및 **권한 있는 역할 관리자** 역할 hello directory 의미 합니다. 권한 있는 역할 관리자만 사용자의 역할 할당을 관리할 수 있습니다. 또한 toorun hello를 선택할 수 있습니다 [보안 마법사.](active-directory-privileged-identity-management-security-wizard.md) hello 초기 검색 및 할당 경험을 안내 합니다.

## <a name="navigate-tooyour-tasks"></a>Tooyour 작업 탐색
Azure AD Privileged Identity Management 설정 되 고 나면 hello 응용 프로그램을 열 때마다 hello 탐색 블레이드를 표시 합니다. 이 블레이드 tooaccomplish identity 관리 작업을 사용 합니다.

![PIM의 최상위 태스크 - 스크린샷](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* **역할 내** tooa 목록이 tooyou 할당 된 역할을 이동 합니다. 이 섹션은 자격이 있는 모든 역할을 활성화하는 위치입니다.
* **요청 승인(미리 보기)**은 디렉터리에 있는 사용자의 보류 중인 활성화 요청 목록을 표시합니다. [자세한 정보](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* **보류 중인 요청 (미리 보기)** 모든 현재 요청 내용을 toohave tooactivate 표시 됩니다.
* **액세스 검토** 하나 액세스 보류 중인 tooany toocomplete, 해야 하는 사용자가 직접 또는 다른 사용자에 대 한 액세스를 검토 하는 여부를 검토 합니다.
* **Azure AD 디렉터리 역할** 권한 있는 역할 관리자 toomanage 역할 할당, 역할 정품 인증 설정 변경, 시작 액세스 검토 등에 hello 대시보드는 hello '관리' 섹션 아래에 있습니다. 이 대시보드에서 hello 옵션은 모든 사용자가 권한 있는 역할 관리자가 아니면 비활성화 됩니다.

## <a name="next-steps"></a>다음 단계
hello [Azure AD Privileged Identity Management 개요](active-directory-privileged-identity-management-configure.md) 조직에 대 한 관리 액세스를 관리 하는 방법에 대 한 자세한 내용은 포함 됩니다.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
