---
title: "aaaAdd 페더레이션된 로그인 tooAzure Active Directory를 설정 하 여 사용자 지정 도메인 이름 | Microsoft Docs"
description: "어떻게 tooadd 회사의 도메인 이름을 Azure Active Directory와 온-프레미스 페더레이션 솔루션 사이 페더레이션 로그인을 tooAzure Active Directory tooset"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 27126c7e-e6d6-4ef3-a4fb-f5f0706e749d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 77f8cc87c27871ac96581360762aaa8d24c0eb8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-your-custom-domain-name-tooazure-active-directory"></a>사용자 지정 도메인 이름을 tooAzure Active Directory를 추가 합니다.
contoso.com의 사용자가 페더레이션 Single Sign-On 환경을 회사 네트워크에서 유지할 수 있도록 'contoso.com'과 같은 사용자 지정 도메인 이름을 구성할 수 있습니다. Active Directory Federation Services (AD FS)을 이미 있는 경우 또는 회사 네트워크에서 실행 하는 다른 페더레이션 서버를 Azure AD toouse을 hello Azure AD Connect 도구를 사용 하 여 사용자 지정 도메인 이름을 구성할 수 있습니다. Azure AD Connect toodeploy 새 AD FS 환경을 사용 하 고 페더레이션된 single sign on tooAzure AD에 대 한 구성 하는 수도 있습니다.

하지 않은 toodeploy AD FS 또는 다른 페더레이션 서버 하지 않을 경우 다음이 지침을 따라: [추가 사용자 지정 도메인 이름을 tooAzure Active Directory](active-directory-add-domain.md)합니다.

## <a name="add-a-custom-domain-name-tooyour-directory"></a>사용자 지정 도메인 이름을 tooyour 디렉터리 추가
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) 사용자 계정과 Azure AD 디렉터리의 전역 관리자 계정입니다.
2. **Active Directory**디렉터리 열고 hello 선택 **도메인** 탭 합니다.
3. Hello 명령 모음에서 선택 **추가**, 만든 'contoso.com' 같은 사용자 지정 도메인의 hello 이름을 입력 합니다. 있는지 tooinclude hello.com,.net 또는 다른 최상위 확장명 수 있습니다.
4. 선택 hello **내 로컬 Active Directory와 tooconfigure이이 도메인에서 single sign-on에 대 한 계획** 확인란을 선택 합니다.
5. **추가**를 선택합니다.

Hello Azure AD Connect 도구 tooget hello DNS 항목을 실행 하 여 Azure AD tooverify hello 도메인을 사용 합니다. Hello에 hello DNS 항목을 보게 **Azure AD 도메인** hello 마법사의 단계입니다. 다음과 같은 hello 마법사에서 어떤 해당 단계를 확인할 수 있습니다 [이러한 지침에 설명 된](connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation)합니다. Hello Azure AD Connect 도구가 없는 경우 다음을 할 수 있습니다 [여기 다운로드](http://go.microsoft.com/fwlink/?LinkId=615771)합니다.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Hello 도메인에 대 한 hello 도메인 이름 등록자에서 hello DNS 항목을 추가 합니다.
사용자 지정 도메인 이름을 Azure AD와 hello 다음 단계 toouse hello 도메인 tooupdate hello DNS 영역 파일입니다. 그러면 Azure AD tooverify 조직이 hello 사용자 지정 도메인 이름을 소유 하 고 있습니다.

1. 도메인 이름에 대 한 도메인 이름 등록 기관에 대 한 toohello 웹 사이트에 로그인 합니다. 를 설정 하지 않은 액세스 toodo이 hello 개인 이나 팀이 액세스 toocomplete 단계 2를 가진 조직과 toolet 완료 되 면 알고에 게 요청 합니다.
2. 업데이트 hello DNS 영역 파일 hello DNS 항목을 추가 하 여 hello 도메인에 대 한 Azure AD에서 tooyou를 제공 합니다. 이 DNS 항목 Azure AD tooverify hello 도메인의 사용자 소유권을 수 있습니다. DNS 항목 hello 메일 수신 라우팅 서버 또는 웹 호스팅 등의 모든 동작을 변경 되지 않습니다.

이 단계에 대한 도움말은 [널리 사용되는 DNS 등록 기관에서 DNS 항목을 추가하기 위한 지침](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Azure AD와 hello 도메인 이름이 유효한 지 확인
Hello DNS 항목을 추가 했으면 준비 tooverify hello 도메인 이름을 Azure AD와 됩니다.

선택 tooverify hello 도메인 **다음** hello에 **Azure AD 도메인** hello Azure AD Connect 마법사의 단계입니다. Azure AD는 hello 도메인에 대 한 hello DNS 영역 파일에 DNS 항목 hello 찾습니다. Hello DNS 레코드가 전파 되 면만 azure AD hello 도메인 이름을 확인 합니다. 전파는 보통 몇 초 밖에 걸리지 않지만 한 시간 이상이 걸릴 경우도 있습니다. 확인 작동 하지 않을 hello 처음으로 나중에 다시 시도 하십시오.

그런 다음 hello 남은 hello Azure AD Connect 마법사의 단계를 진행 합니다. 그러면 프로그램 Windows Server AD tooAzure AD에서에서 사용자가 동기화 됩니다. 페더레이션에 대해 구성한 hello 도메인의 동기화 된 사용자가 하면 회사 네트워크 tooAzure AD에서에서의 경험이 페더레이션된 single sign-on 수 tooget 됩니다.

## <a name="troubleshooting"></a>문제 해결
사용자 지정 도메인 이름을 확인할 수 없는 경우, hello 다음을 시도 하십시오. 가장 일반적이 고 최소 공통 toohello 아래로 회사 hello로 시작 합니다.

1. **한 시간을 대기합니다**. DNS 레코드 toopropagate가 있어야만 Azure AD는 hello 도메인을 확인할 수 있습니다. 이 작업은 한 시간 이상 걸릴 수 있습니다.
2. **DNS 레코드를 입력 하는 hello 및 정확한 지 확인**합니다. Hello 도메인에 대 한 도메인 이름 등록 기관 hello에 대 한 hello 웹 사이트에서이 단계를 완료 합니다. Azure AD hello DNS 항목이 있거나 없는 경우 DNS 영역 파일 hello에 있는 hello DNS 항목과 정확 하 게 일치 하지 않으면 Azure AD 제공 했으면 hello 도메인 이름을 확인할 수 없습니다. Hello 도메인 hello 도메인 이름 등록 기관에 대 한 액세스 tooupdate DNS 레코드가 없는 경우 hello 사람 또는이 액세스 권한이 있는 사용자의 조직에서 팀과 hello DNS 항목을 공유 하 고 tooadd hello DNS 항목을 요청 하십시오.
3. **Azure AD에서 다른 디렉터리에서 hello 도메인 이름을 삭제**합니다. 단일 디렉터리에서 도메인 이름을 확인할 수 있습니다. 다른 디렉터리에서 이전에 도메인 이름을 확인한 경우 새 디렉터리에서 확인할 수 있게 되기 전에 삭제해야 합니다. 도메인 이름을 삭제 하는 방법에 대 한 toolearn 읽을 [사용자 지정 도메인 이름을 관리](active-directory-add-manage-domain-names.md)합니다.

## <a name="add-more-custom-domain-names"></a>사용자 지정 도메인 이름 더 추가하기
조직에서 '만든 contoso.com' 및 'contosobank.com'와 같은 여러 사용자 지정 도메인 이름을 사용 하는 경우를 tooa 최대 900 개의 도메인 이름 추가할 수 있습니다. 이 문서 tooadd 각 도메인 이름에서 단계를 동일 hello를 사용 합니다.

## <a name="next-steps"></a>다음 단계
* [사용자 지정 도메인 이름 관리](active-directory-add-manage-domain-names.md)
* [Azure AD에서 도메인 관리 개념 알아보기](active-directory-add-domain-concepts.md)
* [사용자 로그인 시 회사의 브랜딩 표시](active-directory-add-company-branding.md)
* [Azure AD에서 PowerShell toomanage 도메인 이름 사용](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

