---
title: "Azure Active Directory에서 사용자 지정 도메인 이름을 aaaManaging | Microsoft Docs"
description: "Azure Active Directory에서 사용자 지정 도메인에 대한 관리 개념 및 관리 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Azure Active Directory에서 사용자 지정 도메인 이름 관리
도메인 이름은 다음의 일부로 많은 디렉터리 리소스에 대한 중요한 식별자일 수 있습니다.

* 사용자 이름 또는 사용자에 대한 전자 메일 주소
* 그룹에 대 한 hello 주소
* 응용 프로그램에 대 한 hello 앱 ID URI

Azure Active Directory (Azure AD)에 리소스 toobe hello 리소스가 포함 된 hello 디렉터리에 의해 소유 이미 확인 된 도메인 이름을 포함할 수 있습니다. 전역 관리자만 Azure AD에서 도메인 관리 작업을 수행할 수 있습니다.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. 어떻게 toomanage 도메인 이름 hello Azure AD 관리 센터에서 참조 [Azure Active Directory에서 사용자 지정 도메인 이름을 관리](active-directory-domains-manage-azure-portal.md)합니다.

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Azure AD 디렉터리에 대 한 hello 기본 도메인 이름 설정
디렉터리를 만들면 hello 초기 도메인 이름 예: 'contoso.onmicrosoft.com' 디렉터리에 대 한 hello 기본 도메인 이름 이기도 합니다. hello에 새 사용자를 만들 때 hello 주 도메인은 새 사용자에 대 한 기본 도메인 이름을 hello [Azure 클래식 포털](https://manage.windowsazure.com/), 또는 hello Office 365 관리 포털 등 다른 포털입니다. 이 관리자 toocreate 새 포털에서 사용자에 hello에 대 한 hello 프로세스를 간소화합니다.

디렉터리에 대 한 toochange hello 주 도메인 이름:

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) 사용자 계정과 Azure AD 디렉터리의 전역 관리자 계정입니다.
2. 선택 **Active Directory** hello 왼쪽된 탐색 모음에서 합니다.
3. 디렉터리를 엽니다.
4. 선택 hello **도메인** 탭 합니다.
5. 선택 hello **변경 주** hello 명령 모음에서 단추입니다.
6. Hello 도메인을 toobe hello 새 주 도메인 디렉터리를 선택 합니다.

페더레이션 계정이 아닌지 확인 된 사용자 지정 도메인 디렉터리 toobe hello 주 도메인 이름을 변경할 수 있습니다. 디렉터리에 대 한 hello 주 도메인 변경 hello 사용자 이름에 대 한 모든 기존 사용자가 변경 되지 않습니다.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>사용자 지정 도메인 이름을 tooyour Azure AD를 추가 합니다.
Too900 사용자 지정 도메인 이름 tooeach Azure AD 디렉터리를 추가할 수 있습니다. 프로세스를 너무 hello[추가 사용자 지정 도메인 이름을 추가](active-directory-add-domain.md) hello 첫 번째 사용자 지정 도메인 이름에 대 한 동일 hello 됩니다.

## <a name="add-subdomains-of-a-custom-domain"></a>사용자 지정 도메인의 하위 도메인 추가
Tooadd 'europe.contoso.com' tooyour 디렉터리와 같이 세 번째 수준의 도메인 이름, 원하는 경우 먼저 추가 하 고 contoso.com 등의 hello 두 번째 수준 도메인을 확인 합니다. Azure AD에 의해 hello 하위 도메인을 자동으로 확인 됩니다. 방금 추가한 하위 도메인 hello toosee 확인 되 면 디렉터리의 hello 도메인을 나열 하는 hello 브라우저에서 새로 고침 hello 페이지입니다.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>사용자 지정 도메인 이름에 대 한 hello DNS 등록을 변경 하는 경우 어떤 toodo
사용자 지정 도메인 이름에 대 한 hello DNS 등록을 변경 하면 toouse을 사용자 지정 도메인 이름을 Azure AD와 자체의 추가 구성 작업 없이 하 고 중단 없이 계속할 수 있습니다. 사용자 지정 도메인 이름을 사용 하 여 Office 365, Intune 또는 Azure AD에서 사용자 지정 도메인 이름을 사용 하는 다른 서비스와 이러한 서비스에 대해 toohello 문서를 참조 하십시오.

## <a name="delete-a-custom-domain-name"></a>사용자 지정 도메인 이름 삭제
조직에는 더 이상 해당 도메인 이름을 사용 하는 경우 또는 다른 Azure AD와 해당 도메인 이름을 toouse을 필요한 경우 Azure AD에서 사용자 지정 도메인을 삭제할 수 없습니다.

사용자 지정 도메인 이름을 toodelete 먼저 확인 해야 디렉터리에 있는 hello 도메인 이름에 사용할 합니다. 다음의 경우 디렉터리에서 도메인 이름을 삭제할 수 없습니다.

* 모든 사용자에 게 사용자 이름, 전자 메일 주소 또는 hello 도메인 이름을 포함 하는 프록시 주소입니다.
* 모든 그룹에 전자 메일 주소 또는 hello 도메인 이름을 포함 하는 프록시 주소입니다.
* Azure AD의 모든 응용 프로그램 ID URI hello 도메인 이름을 포함 하는 응용 프로그램을 있습니다.

Hello 사용자 지정 도메인 이름을 삭제 하려면 먼저 Azure AD 디렉터리에서 이러한 리소스를 삭제 하거나 변경 해야 합니다.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>PowerShell 또는 Graph API toomanage 도메인 이름 사용
Azure Active Directory의 도메인 이름에 대한 대부분의 관리 작업은 Microsoft PowerShell을 사용하거나 프로그래밍 방식으로 Azure AD Graph API를 사용하여 완료할 수도 있습니다.

* [Azure ad에서 PowerShell toomanage 도메인 이름을 사용 하 여](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Azure ad에서 Graph API toomanage 도메인 이름을 사용 하 여](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>다음 단계
* [Azure AD에서 도메인 이름에 대해 알아보기](active-directory-add-domain-concepts.md)
* [사용자 지정 도메인 이름 관리](active-directory-add-manage-domain-names.md)

