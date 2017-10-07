---
title: "aaaAdd 사용자 지정 도메인 이름을 tooAzure Active Directory | Microsoft Docs"
description: "어떻게 tooadd 회사의 도메인 이름을 tooAzure Active Directory를 지정 하 고 어떻게 tooverify hello 도메인 이름입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d97e57c6-578a-4929-8fb8-42e858a711c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 88d5f443cd10b098a9a9ffb3137f5e1ca33b6aad
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

Azure Active Directory (Azure AD)를 사용 하 여 회사 도메인 이름 tooAzure AD도 추가할 수 있습니다. 도메인 이름을 해당 하면 조직 사용 하 여 toodo 비즈니스 및 사용자에 게 회사 도메인 이름을 사용 하 여 로그인 할 수 있습니다. 추가 hello 도메인 이름 tooAzure AD 있습니다 tooassign와 같은 친숙 한 tooyour 사용자가 있는 hello 디렉터리의 사용자 이름은 'alice@contoso.com.' hello 프로세스는 간단 합니다.

1. Hello 사용자 지정 도메인 이름 tooyour 디렉터리 추가
2. Hello 도메인 이름 등록자에서 도메인 이름 hello에 대 한 DNS 항목을 추가
3. Hello 사용자 지정 도메인 이름을 Azure AD에서 확인 하십시오.

## <a name="how-do-i-add-a-domain-name"></a>도메인 이름을 추가하려면 어떻게 해야 합니까?
1. Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. 선택 **더 많은 서비스**, 입력 **Azure Active Directory** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.
   
   ![사용자 관리 열기](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Hello에 ***디렉터리 이름*** 블레이드를 **도메인 이름**합니다.
4. Hello에  ***디렉터리 이름* -도메인 이름을** 블레이드, 선택 hello **추가** 명령입니다.
   
   ![Hello 추가 명령을 선택 하면](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Hello에 **도메인 이름** 블레이드에서 hello 상자 만든 'contoso.com' 등의 사용자 지정 도메인의 hello 이름을 입력 한 다음 선택 **도메인 추가**합니다. 있는지 tooinclude hello.com,.net 또는 다른 최상위 확장명 수 있습니다.
6. Hello에 ***domainname*** 블레이드 (즉, hello 블레이드에서 열리면 hello 제목에 새 도메인 이름을 가진) Azure AD에서 조직 hello 사용자 지정 도메인 이름을 소유 하는지 tooverify를 사용 하는 hello DNS 항목 정보를 가져옵니다.
   
   ![DNS 항목 정보 가져오기](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

사용자가 추가한 hello 도메인 이름 했으므로 Azure AD 조직 hello 도메인 이름을 소유 하는지 확인 해야 합니다. Azure AD에서이 확인을 수행 하려면 먼저 hello 도메인 이름에 대 한 hello DNS 영역 파일에는 DNS 항목을 추가 해야 합니다. Hello 도메인 이름에 대 한 도메인 이름 등록 기관에 대 한 hello 웹 사이트에서이 작업을 수행 합니다.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Hello 도메인에 대 한 hello 도메인 이름 등록자에서 hello DNS 항목을 추가 합니다.
사용자 지정 도메인 이름을 Azure AD와 hello 다음 단계 toouse hello 도메인 tooupdate hello DNS 영역 파일입니다. 그러면 Azure AD tooverify 조직이 hello 사용자 지정 도메인 이름을 소유 하 고 있습니다.

1. Hello 도메인에 대 한 toohello 도메인 이름 등록 기관에 로그인 합니다. Tooupdate hello DNS 항목 액세스를 설정 하지 않은 경우에 hello 또는이 액세스 toocomplete 단계 2를 가진 팀 사람과 toolet 완료 되 면 사용자가 알고 있는 요청.
2. 업데이트 hello DNS 영역 파일 hello DNS 항목을 추가 하 여 hello 도메인에 대 한 Azure AD에서 tooyou를 제공 합니다. 이 DNS 항목 Azure AD tooverify hello 도메인의 사용자 소유권을 수 있습니다. DNS 항목 hello 메일 수신 라우팅 서버 또는 웹 호스팅 등의 모든 동작을 변경 되지 않습니다.

도움말 추가 hello DNS 항목을 참조 하세요 [인기 있는 DNS 등록 기관에서 DNS 항목을 추가 하기 위한 지침](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Azure AD와 hello 도메인 이름이 유효한 지 확인
Hello DNS 항목을 추가 했으면 준비 tooverify hello 도메인 이름을 Azure AD와 됩니다.

도메인 이름 hello DNS 레코드가 전파 된 후에 확인할 수 있습니다. 이 전파는 보통 몇 초 밖에 걸리지 않지만 한 시간 이상이 걸릴 경우도 있습니다. 확인 작동 하지 않을 hello 처음으로 나중에 다시 시도 하십시오.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. 선택 **찾아보기**hello 텍스트 상자에 사용자 관리를 입력 한 다음 선택, **Enter**합니다.
   
   ![사용자 관리 열기](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Hello에 **사용자 관리-도메인 이름** 블레이드, tooverify 않겠다고 선택 hello 확인 되지 않은 도메인 이름입니다.
4. Hello에 ***domainname*** 블레이드 (즉, hello 블레이드에서 열리면 hello 제목에 새 도메인 이름을 가진) 선택 **확인** toocomplete hello 확인 합니다.

이제 [사용자 지정 도메인 이름을 포함하는 사용자 이름을 할당](active-directory-users-create-azure-portal.md)할 수 있습니다.

## <a name="troubleshooting"></a>문제 해결
사용자 지정 도메인 이름을 확인할 수 없는 경우, hello 다음을 시도 하십시오. 가장 일반적이 고 최소 공통 toohello 아래로 회사 hello로 시작 합니다.

1. **한 시간을 대기합니다**. DNS 레코드 toopropagate가 있어야만 Azure AD는 hello 도메인을 확인할 수 있습니다. 이 작업은 한 시간 이상 걸릴 수 있습니다.
2. **DNS 레코드를 입력 하는 hello 및 정확한 지 확인**합니다. Hello 도메인에 대 한 도메인 이름 등록 기관 hello에 대 한 hello 웹 사이트에서이 단계를 완료 합니다. Azure AD hello DNS 항목이 있거나 없는 경우 DNS 영역 파일 hello에 있는 hello DNS 항목과 정확 하 게 일치 하지 않으면 Azure AD 제공 했으면 hello 도메인 이름을 확인할 수 없습니다. Hello 도메인 hello 도메인 이름 등록 기관에 대 한 액세스 tooupdate DNS 레코드가 없는 경우 hello 사람 또는이 액세스 권한이 있는 사용자의 조직에서 팀과 hello DNS 항목을 공유 하 고 tooadd hello DNS 항목을 요청 하십시오.
3. **Azure AD에서 다른 디렉터리에서 hello 도메인 이름을 삭제**합니다. 단일 디렉터리에서 도메인 이름을 확인할 수 있습니다. 다른 디렉터리에서 이전에 도메인 이름을 확인한 경우 새 디렉터리에서 확인할 수 있게 되기 전에 삭제해야 합니다. 도메인 이름을 삭제 하는 방법에 대 한 toolearn 읽을 [사용자 지정 도메인 이름을 관리](active-directory-domains-manage-azure-portal.md)합니다.    

## <a name="add-more-custom-domain-names"></a>사용자 지정 도메인 이름 더 추가하기
조직에서 '만든 contoso.com' 및 'contosobank.com'와 같은 여러 사용자 지정 도메인 이름을 사용 하는 경우를 tooa 최대 900 개의 도메인 이름 추가할 수 있습니다. 이 문서 tooadd 각 도메인 이름에서 단계를 동일 hello를 사용 합니다.

## <a name="next-steps"></a>다음 단계
[사용자 지정 도메인 이름 관리](active-directory-domains-manage-azure-portal.md)

