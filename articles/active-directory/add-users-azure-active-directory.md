---
title: "aaaAdd 새 사용자 tooAzure Active Directory | Microsoft Docs"
description: "에 대해 설명 방법을 tooadd Azure Active Directory에 새 사용자입니다."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a>빠른 시작: 새로운 사용자가 tooAzure Active Directory를 추가 합니다.
이 문서는 어떻게 hello Azure Active Directory (Azure AD)에서 조직 내에서 새 사용자 tooadd hello Azure 포털을 사용 하 여 한 번에 또는 온-프레미스 Windows Server AD 사용자를 동기화 하 여 계정 데이터를 설명 합니다. 

## <a name="add-cloud-based-users"></a>클라우드 기반 사용자 추가
1. Toohello 로그인 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. **Azure Active Directory**를 선택한 후 **사용자 및 그룹**을 선택합니다.
3. Hello에 **사용자 및 그룹** 블레이드를 **모든 사용자에 게**를 선택한 후 **새 사용자**합니다.
   ![Hello 추가 명령을 선택 하면](./media/add-users-azure-active-directory/add-user.png)
4. 와 같은 hello 사용자에 대 한 세부 정보를 입력 **이름** 및 **사용자 이름**합니다. hello hello 사용자 이름의 도메인 이름 부분 이어야 합니다. hello 초기 기본 도메인 이름 "[도메인 이름].onmicrosoft.com" 또는 검증 된 페더레이션 되지 않은 [사용자 지정 도메인 이름을](add-custom-domain.md) "contoso.com" 등
5. 복사 또는 다른 방법 참고 hello을 제공할 수 있습니다 toohello 사용자가이 프로세스가 완료 된 후 사용자 암호를 생성 합니다.
6. 필요에 따라 수를 열고 hello에 hello 정보를 채울 **프로필** 블레이드, hello **그룹** 블레이드에서 또는 hello **디렉터리 역할** 블레이드 hello 사용자에 대 한 합니다. 사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.
7. Hello에 **사용자** 블레이드를 **만들기**합니다.
8. Hello 사용자 로그인 할 수 있도록 생성 된 hello 암호 toohello 새 사용자를 안전 하 게 배포 합니다.

> [!TIP]
> 또한 온-프레미스 Windows Server AD에서 사용자 계정 데이터를 동기화할 수도 있습니다. Microsoft의 id 솔루션에는 온-프레미스 및 클라우드 기반 기능을 위치에 관계 없이 tooall 리소스, 인증 및 권한 부여에 대 한 단일 사용자 id를 만드는 걸쳐 있습니다. 하이브리드 ID라고 합니다. [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) toointegrate 사용 하는 하이브리드 id 시나리오에 대 한 Azure Active Directory와 온-프레미스 디렉터리를 수 있습니다. 이렇게 하면 tooprovide Office 365, Azure 및 SaaS 응용 프로그램에 대 한 사용자에 대 한 일반 id를 Azure AD와 통합 되어 있습니다. 

## <a name="delete-users-from-azure-ad"></a>Azure AD에서 사용자 삭제
1. Toohello 로그인 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. **사용자 및 그룹**을 선택합니다.
3. Hello에 **사용자 및 그룹** 블레이드, hello 목록에서 선택 hello 사용자 toodelete 합니다. 
4. Hello 선택한 사용자에 대 한 hello 블레이드에서 선택 **개요**를 선택한 다음 hello 명령 모음에서 **삭제**합니다.
   ![Hello 추가 명령을 선택 하면](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>자세한 정보 
* [외부 사용자 추가](active-directory-users-create-external-azure-portal.md)

* [Azure AD에서 사용자 tooa 역할을 할당 합니다.](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>다음 단계
이 빠른 시작에서 배운 어떻게 tooadd 새 사용자 tooAzure AD Premium입니다. 

Hello hello Azure 포털에서에서 링크 toocreate 새 사용자를 Azure AD에서 다음을 사용할 수 있습니다.

> [!div class="nextstepaction"]
> [사용자가 tooAzure AD 추가](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
