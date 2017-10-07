---
title: "aaaAssign 사용자 tooa Azure Active Directory에서 사용자 지정 도메인 | Microsoft Docs"
description: "어떻게 toopopulate 사용자 계정으로 Azure Active Directory에서 사용자 지정 도메인입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a>사용자가 사용자 지정 도메인을 tooa 할당
사용자 지정 도메인 tooAzure Active Directory 사용자를 추가한 후에 인증을 시작할 수 있도록이 도메인에 대 한 hello 사용자 계정을 추가 해야 합니다.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. 어떻게 toomanage 도메인 이름 hello Azure AD 관리 센터에서 참조 [Azure Active Directory에서 사용자 지정 도메인 이름을 관리](active-directory-domains-manage-azure-portal.md)합니다.

## <a name="users-synced-from-a-on-premises-directory"></a>온-프레미스 디렉터리에서 동기화된 사용자
이미 설정한 경우 한 연결을 온-프레미스 간의 Active Directory와 Azure Active Directory를 동기화 hello 계정을 채울 수 있습니다. Toosynchronize 온-프레미스 Active Directory와 Azure Active Directory 확인 하려면 어떻게 해야 대 한 자세한 내용은 [Azure Active Directory와 온-프레미스 id 통합](active-directory-aadconnect.md)합니다.

## <a name="users-added-and-managed-in-hello-cloud"></a>사용자 추가 하 고 hello 클라우드에서 관리
기존 사용자 계정에 대 한 toochange hello 도메인:

1. 열기 hello 전역 관리자 또는 사용자 관리자 인 계정을 사용 하 여 Azure 클래식 포털
2. 디렉터리를 엽니다.
3. 선택 hello **사용자** 탭 합니다.
4. Hello 사용자 hello 목록에서 선택 합니다.
5. Hello 사용자에 대 한 hello 도메인을 변경 하 고 다음 선택 **저장**합니다.

또한 이렇게 사용 하 여 [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) 또는 hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)합니다.

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>새 사용자를 만들 때 사용자 지정 도메인 선택
1. 열기 hello 전역 관리자 또는 사용자 관리자 인 계정을 사용 하 여 Azure 클래식 포털
2. 디렉터리를 엽니다.
3. 선택 hello **사용자** 탭 합니다.
4. Hello 명령 모음에서 선택 **추가**합니다.
5. Hello 사용자 이름을 추가 하면 사용자 지정 도메인 hello hello 도메인 목록에서 선택 합니다.
6. **저장**을 선택합니다.

## <a name="next-steps"></a>다음 단계
* [사용자에 대 한 사용자 지정 도메인 이름을 toosimplify hello 로그인 환경을 사용 하 여](active-directory-add-domain.md)
* [사용자 지정 도메인 이름 관리](active-directory-add-manage-domain-names.md)
* [Azure AD에서 도메인 관리 개념 알아보기](active-directory-add-domain-concepts.md)

