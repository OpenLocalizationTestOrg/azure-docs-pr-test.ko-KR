---
title: "Azure Active Directory 도메인 서비스: hello Azure AD DC 관리자 그룹 만들기 | Microsoft Docs"
description: "Azure Active Directory 도메인 서비스 hello Azure 클래식 포털을 사용 하 여 사용 하도록 설정"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Azure Active Directory 도메인 서비스 hello Azure 클래식 포털을 사용 하 여 사용 하도록 설정
이 문서에 설명 하 고 hello 구성 작업 tooenable Azure Active Directory 도메인 서비스 (Azure AD DS) Azure Active Directory (Azure AD) 테 넌 트에 대 한 사용자에 게 필요한을 안내 합니다.

> [!NOTE]
> [**(미리 보기) Azure 포털 경험을 새 hello를 대신 사용해 보세요**](active-directory-ds-getting-started.md)합니다. 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a>작업 1: hello Azure AD DC 관리자 그룹 만들기
hello 첫 번째 작업은 Azure AD 테 넌 트의 관리 그룹 toocreate입니다. 이 특수 관리 그룹을 *AAD DC Administrators*라고 합니다. 이 그룹의 구성원은 Azure Active Directory 도메인 서비스에서 관리 하는 도메인 toohello 도메인에 가입 된 컴퓨터에 대 한 관리 권한이 부여 됩니다. 도메인에 가입 된 컴퓨터에서이 그룹은 toohello 관리자 그룹을 추가 합니다. 또한이 그룹의 구성원 원격 데스크톱 tooconnect 원격으로 toodomain에 가입 된 컴퓨터를 사용할 수 있습니다.  

> [!NOTE]
> Azure Active Directory 도메인 서비스를 사용 하 여 만든 hello 관리 되는 도메인에 도메인 관리자 또는 엔터프라이즈 관리자 권한이 없는 합니다. 관리 되는 도메인에 이러한 hello 서비스에서 예약 된 사용 권한과 hello 테 넌 트 내에서 사용할 수 있는 toousers 적용 되지 않습니다. 그러나 만든 hello 특별 한 관리 그룹을 사용할 수 있습니다이 구성 작업 tooperform에서 일부 권한 있는 작업입니다. 이러한 작업 컴퓨터 toohello 도메인 가입, toohello 관리 그룹 도메인에 가입 된 컴퓨터에 속하는 및 그룹 정책 구성에 포함 됩니다.
>

이 구성 작업에 hello 관리 그룹 만들고 directory toohello 그룹의 하나 이상의 사용자를 추가 합니다. Azure Active Directory 도메인 서비스에 대 한 toocreate hello 관리 그룹은 다음 hello 수행:

1. Toohello 이동 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 왼쪽된 창에서 선택 hello **Active Directory** 단추입니다.
3. Hello Azure AD 테 넌 트 (디렉터리) 하려는 tooenable Azure Active Directory 도메인 서비스를 선택 합니다. Azure AD 디렉터리에 한 개의 도메인만 만들 수 있습니다.

    ![Azure AD Directory 선택](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Hello에 **미리 보기 디렉터리** 페이지에서 hello **그룹** 탭 합니다.
5. tooadd 그룹 tooyour Azure AD 테 넌 트, hello hello 창 맨 아래에 hello 작업창에 클릭 **그룹 추가**합니다.

    ![hello 그룹 추가 단추](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. Hello에 **그룹 추가** 대화 상자, 라는 그룹을 만들고 **AAD DC 관리자**를 설정한 **그룹 종류** 너무**보안**합니다.

   > [!WARNING]
   > Azure Active Directory 도메인 서비스에서 관리 하는 도메인 내에서 tooenable 액세스 정확한이 이름을 가진 그룹을 만듭니다.
   >
   >

    ![hello 그룹 추가 대화 상자](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. Hello에 **설명** 하면 다른 사용자는 설명을 입력 합니다 toounderstand이이 그룹에 Azure Active Directory 도메인 서비스 내에서 관리 권한을 부여 하 합니다.
8. Hello 그룹을 만든 후 hello 그룹 이름 tooview 속성을 클릭 합니다.
9. hello hello 창 맨 아래에 hello 그룹의 구성원으로 tooadd 사용자가 클릭 hello **구성원 추가** 단추입니다.

    ![그룹 구성원 단추 추가](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. Hello에 **멤버 추가** 대화 상자에서이 그룹의 구성원 이어야 하 고 hello에 hello 확인 표시 아이콘을 클릭 해야 선택 hello 사용자 하단 오른쪽입니다.

    ![사용자가 tooadministrators 그룹 추가](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a>다음 단계
[작업 2: Azure 가상 네트워크 만들기 또는 선택](active-directory-ds-getting-started-vnet.md)
