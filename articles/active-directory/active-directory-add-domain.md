---
title: "aaaAdd 사용자 지정 도메인 이름을 tooAzure Active Directory | Microsoft Docs"
description: "어떻게 tooadd 회사의 도메인 이름을 tooAzure Active Directory를 지정 하 고 어떻게 tooverify hello 도메인 이름입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 35a6e20a-9907-432b-9d36-16b916a5c249
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: eb208138f2633aaecc54f68dc947caf80d856d23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-domain-name-tooazure-active-directory"></a>사용자 지정 도메인 이름을 tooAzure Active Directory를 추가 합니다.
> [!div class="op_single_selector"]
> * [Azure 포털](active-directory-domains-add-azure-portal.md)
> * [Azure 클래식 포털](active-directory-add-domain.md)
> 
> 

하나 이상의 도메인 이름을 toodo 비즈니스 조직에서 사용 하 고 사용자가 회사 도메인 이름을 사용 하 여 tooyour 회사 네트워크에 로그인 했습니다. Azure Active Directory (Azure AD)를 사용 했으므로 사용자 회사 도메인 이름 tooAzure AD도 추가할 수 있습니다. 이렇게 하면 tooassign와 같은 친숙 한 tooyour 사용자가 있는 hello 디렉터리의 사용자 이름은 'alice@contoso.com.' hello 프로세스는 간단 합니다.

1. Hello 사용자 지정 도메인 이름 tooyour 디렉터리 추가
2. Hello 도메인 이름 등록자에서 도메인 이름 hello에 대 한 DNS 항목을 추가
3. Hello 사용자 지정 도메인 이름을 Azure AD에서 확인 하십시오.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. Tooadd hello Azure AD 관리 센터에서 회사 도메인 이름을 확인 하려면 어떻게 해야 하는 것에 대 한 [Azure Active Directory에서 관리자 역할 할당](active-directory-domains-add-azure-portal.md)합니다.

Active Directory Federation Services (AD FS) 또는 회사 네트워크에서 서로 다른 보안 토큰 서비스 (STS)를 함께 사용 하 여 사용자 지정 도메인 이름 toobe tooconfigure 하려는 경우 hello 지침에 따라 [추가 및 구성에 대 한 도메인 Azure Active Directory와 페더레이션](active-directory-add-domain-federated.md)합니다. 사용자 회사 디렉터리 tooAzure AD에서에서 toosynchronize 사용자가 계획 하는 경우에 유용 하 고 [암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md) 요구 사항을 충족 하지 않습니다.

## <a name="add-a-custom-domain-name-tooyour-directory"></a>사용자 지정 도메인 이름을 tooyour 디렉터리 추가
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) 사용자 계정과 Azure AD 디렉터리의 전역 관리자 계정입니다.
2. **Active Directory**디렉터리 열고 hello 선택 **도메인** 탭 합니다.
3. Hello 명령 모음에서 선택 **추가**합니다. Hello 만든 'contoso.com' 같은 사용자 지정 도메인 이름을 입력 합니다. 시키고 tooinclude.com,.net 또는 다른 최상위 확장명 hello "single sign on"에 대 한 hello 확인란 (페더레이션)의 선택을 취소 합니다.
4. **추가**를 선택합니다.
5. Hello 도메인 추가 마법사의 두 번째 페이지 hello hello를 Azure AD에서 조직 hello 사용자 지정 도메인 이름을 소유 하는지 tooverify을 사용 하는 DNS 항목을 가져옵니다.

사용자가 추가한 hello 도메인 이름 했으므로 Azure AD 조직 hello 도메인 이름을 소유 하는지 확인 해야 합니다. Azure AD에서이 확인을 수행 하려면 먼저 hello 도메인 이름에 대 한 hello DNS 영역 파일에는 DNS 항목을 추가 해야 합니다. Hello 도메인 이름에 대 한 도메인 이름 등록 기관에 대 한 hello 웹 사이트에서이 작업을 수행 합니다.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Hello 도메인에 대 한 hello 도메인 이름 등록자에서 hello DNS 항목을 추가 합니다.
사용자 지정 도메인 이름을 Azure AD와 hello 다음 단계 toouse hello 도메인 tooupdate hello DNS 영역 파일입니다. 그러면 Azure AD tooverify 조직이 hello 사용자 지정 도메인 이름을 소유 하 고 있습니다.

1. Hello 도메인에 대 한 toohello 도메인 이름 등록 기관에 로그인 합니다. Tooupdate hello DNS 항목 액세스를 설정 하지 않은 경우에 hello 또는이 액세스 toocomplete 단계 2를 가진 팀 사람과 toolet 완료 되 면 사용자가 알고 있는 요청.
2. 업데이트 hello DNS 영역 파일 hello DNS 항목을 추가 하 여 hello 도메인에 대 한 Azure AD에서 tooyou를 제공 합니다. 이 DNS 항목 Azure AD tooverify hello 도메인의 사용자 소유권을 수 있습니다. DNS 항목 hello 메일 수신 라우팅 서버 또는 웹 호스팅 등의 모든 동작을 변경 되지 않습니다.

도움말 추가 hello DNS 항목을 참조 하세요 [인기 있는 DNS 등록 기관에서 DNS 항목을 추가 하기 위한 지침](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Azure AD와 hello 도메인 이름이 유효한 지 확인
Hello DNS 항목을 추가 했으면 준비 tooverify hello 도메인 이름을 Azure AD와 됩니다.

Hello 여전히 있는 경우 **도메인 추가** 마법사 열기 선택 **확인** hello hello 마법사의 세 번째 페이지에서. 선택 하는 경우 **확인**, Azure AD은 hello 도메인에 대 한 hello DNS 영역 파일에 hello DNS 항목을 검색 합니다. Azure AD hello DNS 레코드가 전파 된 후에 hello 도메인 이름을 확인할 수 있습니다. 이 전파는 보통 몇 초 밖에 걸리지 않지만 한 시간 이상이 걸릴 경우도 있습니다. 확인 작동 하지 않을 hello 처음으로 나중에 다시 시도 하십시오.

경우 hello **도메인 추가** hello에 hello 도메인을 확인할 수 있습니다, 마법사가 아직 열려 있지 않는 [Azure 클래식 포털](https://manage.windowsazure.com/):

1. Azure AD 디렉터리의 전역 관리자인 사용자 계정으로 로그인합니다.
2. 디렉터리 및 선택 hello 열고 **도메인** 탭 합니다.
3. 선택 hello 도메인 이름을 tooverify 원하고 선택 **확인** hello 명령 모음에서 합니다.
4. 선택 **확인** hello 대화 상자 toocomplete hello 확인에 있습니다.

이제 [사용자 지정 도메인 이름을 포함하는 사용자 이름을 할당](active-directory-add-domain-add-users.md)할 수 있습니다.

## <a name="troubleshooting"></a>문제 해결
사용자 지정 도메인 이름을 확인할 수 없는 경우, hello 다음을 시도 하십시오. 가장 일반적이 고 최소 공통 toohello 아래로 회사 hello로 시작 합니다.

1. **한 시간을 대기합니다**. DNS 레코드 toopropagate가 있어야만 Azure AD는 hello 도메인을 확인할 수 있습니다. 이 작업은 한 시간 이상 걸릴 수 있습니다.
2. **DNS 레코드를 입력 하는 hello 및 정확한 지 확인**합니다. Hello 도메인에 대 한 도메인 이름 등록 기관 hello에 대 한 hello 웹 사이트에서이 단계를 완료 합니다. Azure AD hello DNS 항목이 있거나 없는 경우 DNS 영역 파일 hello에 있는 hello DNS 항목과 정확 하 게 일치 하지 않으면 Azure AD 제공 했으면 hello 도메인 이름을 확인할 수 없습니다. Hello 도메인 hello 도메인 이름 등록 기관에 대 한 액세스 tooupdate DNS 레코드가 없는 경우 hello 사람 또는이 액세스 권한이 있는 사용자의 조직에서 팀과 hello DNS 항목을 공유 하 고 tooadd hello DNS 항목을 요청 하십시오.
3. **Azure AD에서 다른 디렉터리에서 hello 도메인 이름을 삭제**합니다. 단일 디렉터리에서 도메인 이름을 확인할 수 있습니다. 다른 디렉터리에서 이전에 도메인 이름을 확인한 경우 새 디렉터리에서 확인할 수 있게 되기 전에 삭제해야 합니다. 도메인 이름을 삭제 하는 방법에 대 한 toolearn 읽을 [사용자 지정 도메인 이름을 관리](active-directory-add-manage-domain-names.md)합니다.

## <a name="add-more-custom-domain-names"></a>사용자 지정 도메인 이름 더 추가하기
조직에서 '만든 contoso.com' 및 'contosobank.com'와 같은 여러 사용자 지정 도메인 이름을 사용 하는 경우를 tooa 최대 900 개의 도메인 이름 추가할 수 있습니다. 이 문서 tooadd 각 도메인 이름에서 단계를 동일 hello를 사용 합니다.

## <a name="next-steps"></a>다음 단계
* [사용자 지정 도메인 이름을 포함하는 사용자 이름 할당](active-directory-add-domain-add-users.md)
* [사용자 지정 도메인 이름 관리](active-directory-add-manage-domain-names.md)
* [Azure AD에서 도메인 관리 개념 알아보기](active-directory-add-domain-concepts.md)
* [사용자 로그인 시 회사의 브랜딩 표시](active-directory-add-company-branding.md)
* [Azure AD에서 PowerShell toomanage 도메인 이름 사용](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

