---
title: "사용자 지정 도메인 tooAzure AD aaaAdd | Microsoft Docs"
description: "에 대해 설명 어떻게 tooadd Azure Active Directory에서 사용자 지정 도메인입니다."
services: active-directory
author: jeffgilb
manager: femila
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 878cecad364ec47f1c6755d742aaccbce627dc5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-a-custom-domain-name-tooazure-active-directory"></a>빠른 시작: 사용자 지정 도메인 이름을 tooAzure Active Directory를 추가 합니다.

모든 Azure AD 디렉터리의 hello 형태로 하면 초기 도메인 이름에는 *domainname*. 하지만 사용자 회사 도메인 이름 tooAzure AD도 추가할 수 있습니다 onmicrosoft.com. hello 초기 도메인 이름을 변경 하거나 삭제할 수 없습니다. 예를 들어 조직 도메인 사용 되는 이름과 toodo 익스트라넷 및 회사 도메인 이름을 사용 하 여에 로그인 한 사용자는 수는 있습니다. 추가 사용자 지정 도메인 이름을 tooAzure AD 있습니다 tooassign와 같은 친숙 한 tooyour 사용자가 있는 hello 디렉터리의 사용자 이름은 'alice@contoso.com.' 'alice@*<domain name>*.onmicrosoft.com' 대신입니다. hello 프로세스는 간단 합니다.

1. Hello 사용자 지정 도메인 이름 tooyour 디렉터리 추가
2. Hello 도메인 이름 등록자에서 도메인 이름 hello에 대 한 DNS 항목을 추가
3. Hello 사용자 지정 도메인 이름을 Azure AD에서 확인 하십시오.

## <a name="add-your-custom-domain"></a>사용자 지정 도메인 추가
1. Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. 선택 **더 많은 서비스**, 입력 **Azure Active Directory** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.
   
   ![사용자 관리 열기](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Hello에 ***디렉터리 이름*** 블레이드를 **도메인 이름**합니다.
4. Hello에  ***디렉터리 이름* -도메인 이름을** 블레이드, 선택 hello **추가** 명령입니다.
   
   ![Hello 추가 명령을 선택 하면](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Hello에 **도메인 이름** 블레이드에서 hello 상자 만든 'contoso.com' 등의 사용자 지정 도메인의 hello 이름을 입력 한 다음 선택 **도메인 추가**합니다. 있는지 tooinclude hello.com,.net 또는 다른 최상위 확장명 수 있습니다.
6. Hello에 ***도메인 이름*** hello 제목에 사용자 지정 도메인 이름), (으로 블레이드 hello DNS 항목 정보 toouse tooverify 조직이 hello 사용자 지정 도메인 이름을 소유 하 고 가져옵니다.
   
   ![DNS 항목 정보 가져오기](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

> [!TIP]
> Toofederate 온-프레미스 Windows Server AD와 Azure AD 계획할 경우 tooselect hello 필요한 **내 로컬 Active Directory와 tooconfigure이이 도메인에서 single sign-on에 대 한 계획** hello Azure AD Connect 도구를 실행 하면 확인란 toosynchronize 디렉터리입니다. 또한 tooregister 해야 hello에 온-프레미스 디렉터리와 페더레이션에 대해 선택한 동일한 도메인 이름을 hello **Azure AD 도메인** hello 마법사의 단계입니다. 다음과 같은 hello 마법사에서 어떤 해당 단계를 확인할 수 있습니다 [이러한 지침에 설명 된](./connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation)합니다. Hello Azure AD Connect 도구가 없는 경우 다음을 할 수 있습니다 [여기 다운로드](http://go.microsoft.com/fwlink/?LinkId=615771)합니다.

사용자가 추가한 hello 도메인 이름 했으므로 Azure AD 조직 hello 도메인 이름을 소유 하는지 확인 해야 합니다. Azure AD에서이 확인을 수행 하려면 먼저 hello 도메인 이름에 대 한 hello DNS 영역 파일에는 DNS 항목을 추가 해야 합니다. Hello 도메인 이름에 대 한 도메인 이름 등록 기관에 대 한 hello 웹 사이트에서이 작업을 수행 합니다.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Hello 도메인에 대 한 hello 도메인 이름 등록자에서 hello DNS 항목을 추가 합니다.
사용자 지정 도메인 이름을 Azure AD와 hello 다음 단계 toouse hello 도메인 tooupdate hello DNS 영역 파일입니다. Azure AD 조직 hello 사용자 지정 도메인 이름을 소유 하는지 확인할 수 있습니다.

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
4. Hello에 ***도메인 이름*** 블레이드 (즉, hello 블레이드에서 열리면 hello 제목에 새 도메인 이름을 가진) 선택 **확인** toocomplete hello 확인 합니다.

> [!TIP]
> Too900 사용자 지정 도메인 이름을 추가할 수 있지만 하나만 수 [Azure AD 디렉터리에 대 한 hello 기본 도메인 이름으로 설정](active-directory-domains-manage-azure-portal.md#set-the-primary-domain-name-for-your-azure-ad-directory) 새 계정을 만들 때 기본적으로 사용 합니다.

이제 사용자 지정 도메인 이름을 사용하여 클라우드 기반 사용자 계정을 만들거나 이전에 동기화된 온-프레미스 사용자 계정 정보를 업데이트합니다. 이전에 동기화 된 사용자 계정 도메인 접미사 사용 하 여 정보를 수정할 수도 있습니다 [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) 또는 hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)합니다.

## <a name="troubleshooting"></a>문제 해결
사용자 지정 도메인 이름을 확인할 수 없는 경우, 문제 해결 단계를 수행 하는 hello를 시도해 보십시오.

1. **한 시간을 대기합니다**. DNS 레코드 toopropagate가 있어야만 Azure AD는 hello 도메인을 확인할 수 있습니다. 이 작업은 한 시간 이상 걸릴 수 있습니다.
2. **DNS 레코드를 입력 하는 hello 및 정확한 지 확인**합니다. Hello 도메인에 대 한 도메인 이름 등록 기관 hello에 대 한 hello 웹 사이트에서이 단계를 완료 합니다. Azure AD hello DNS 항목이 있거나 없는 경우 DNS 영역 파일 hello에 있는 hello DNS 항목과 정확 하 게 일치 하지 않으면 Azure AD 제공 했으면 hello 도메인 이름을 확인할 수 없습니다. Hello 도메인 hello 도메인 이름 등록 기관에 대 한 액세스 tooupdate DNS 레코드가 없는 경우 hello 사람 또는이 액세스 권한이 있는 사용자의 조직에서 팀과 hello DNS 항목을 공유 하 고 tooadd hello DNS 항목을 요청 하십시오.
3. **Azure AD에서 다른 디렉터리에서 hello 도메인 이름을 삭제**합니다. 단일 디렉터리에서 도메인 이름을 확인할 수 있습니다. 다른 디렉터리에서 이전에 도메인 이름을 확인한 경우 새 디렉터리에서 확인할 수 있게 되기 전에 삭제해야 합니다. 도메인 이름을 삭제 하는 방법에 대 한 toolearn 읽을 [사용자 지정 도메인 이름을 관리](active-directory-domains-manage-azure-portal.md)합니다.    

## <a name="add-more-custom-domain-names"></a>사용자 지정 도메인 이름 더 추가하기
조직에 '만든 contoso.com'와 'contosobank.com' 같은 둘 이상의 사용자 지정 도메인 이름을 사용 하는 경우 각각에 대해이 문서의 hello 단계를 반복 하 여 더 부분 일치 too900를 추가할 수 있습니다.

### <a name="learn-more"></a>자세한 정보
[Azure AD에서 사용자 지정 도메인 이름의 개념적 개요](active-directory-add-domain-concepts.md)

[사용자 지정 도메인 이름 관리](active-directory-domains-manage-azure-portal.md)


## <a name="next-steps"></a>다음 단계
이 빠른 시작에서 배운 방법을 사용자 지정 도메인 tooAzure AD tooadd 합니다. 

Hello hello Azure 포털에서에서 링크 tooadd 새 사용자 지정 도메인을 Azure AD에서 다음을 사용할 수 있습니다.

> [!div class="nextstepaction"]
> [사용자 지정 도메인 추가](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/QuickStart) 