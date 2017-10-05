---
title: "Azure Active Directory에서 사용자 지정 도메인 이름 관리 | Microsoft Docs"
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
ms.openlocfilehash: 5ae19bb370064de96cf466ca09b13d02563d65a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Azure Active Directory에서 사용자 지정 도메인 이름 관리
도메인 이름은 다음의 일부로 많은 디렉터리 리소스에 대한 중요한 식별자일 수 있습니다.

* 사용자 이름 또는 사용자에 대한 전자 메일 주소
* 그룹에 대한 주소
* 응용 프로그램에 대한 앱 ID URI

Azure AD(Azure Active Directory)의 리소스는 리소스를 포함하는 디렉터리가 소유하는 이미 확인된 도메인 이름을 포함할 수 있습니다. 전역 관리자만 Azure AD에서 도메인 관리 작업을 수행할 수 있습니다.

> [!IMPORTANT]
> 이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다. Azure AD 관리 센터에서 도메인 이름을 관리하는 방법은 [Azure Active Directory에서 사용자 지정 도메인 이름 관리](active-directory-domains-manage-azure-portal.md)를 참조하세요.

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a>Azure AD 디렉터리에 대한 주 도메인 이름 설정
디렉터리를 만든 경우 'contoso.onmicrosoft.com'과 같은 초기 도메인 이름은 디렉터리에 대한 주 도메인 이름이기도 합니다. [Azure 클래식 포털](https://manage.windowsazure.com/)또는 Office 365 관리자 포털 등 다른 포털에 새 사용자를 만들 때 주 도메인은 새 사용자에 대한 기본 도메인 이름입니다. 관리자에 대한 프로세스를 간소화하여 포털에 새 사용자를 만듭니다.

디렉터리에 대한 주 도메인 이름을 변경하려면

1. Azure AD 디렉터리의 전역 관리자인 사용자 계정으로 [Azure 클래식 포털](https://manage.windowsazure.com/) 에 로그인합니다.
2. 왼쪽 탐색 모음에서 **Active Directory** 를 선택합니다.
3. 디렉터리를 엽니다.
4. **도메인** 탭을 선택합니다.
5. 명령 모음에서 **기본 변경** 단추를 선택합니다.
6. 디렉터리에 대한 새 주 도메인으로 지정할 도메인을 선택합니다.

페더레이션되지 않은 모든 확인된 사용자 지정 도메인이 되도록 디렉터리에 대한 주 도메인 이름을 변경할 수 있습니다. 디렉터리에 대한 주 도메인을 변경해도 기존 사용자에 대한 사용자 이름은 변경되지 않습니다.

## <a name="add-custom-domain-names-to-your-azure-ad"></a>Azure AD에 사용자 지정 도메인 이름 추가
각 Azure AD 디렉터리에 최대 900개의 사용자 지정 도메인 이름을 추가할 수 있습니다. [추가 사용자 지정 도메인 이름을 추가](active-directory-add-domain.md) 하는 프로세스는 첫 번째 사용자 지정 도메인 이름에 대해 동일합니다.

## <a name="add-subdomains-of-a-custom-domain"></a>사용자 지정 도메인의 하위 도메인 추가
디렉터리에 'europe.contoso.com'과 같은 세 번째 수준 도메인 이름을 추가하려면 먼저 contoso.com과 같은 두 번째 수준 도메인을 추가 및 확인해야 합니다. Azure AD에서 자동으로 하위 도메인을 확인합니다. 방금 추가한 하위 도메인이 확인되었는지 보려면 디렉터리의 도메인을 나열하는 브라우저의 페이지를 새로 고칩니다.

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a>사용자 지정 도메인 이름의 DNS 등록 기관을 변경하는 경우 수행할 작업
사용자 지정 도메인 이름을 위해 DNS 등록 기관을 변경할 경우 추가 구성 작업 및 중단 없이 Azure AD 자체로 사용자 지정 도메인 이름을 계속 사용할 수 있습니다. Office 365, Intune 또는 Azure AD의 사용자 지정 도메인 이름을 사용하는 다른 서비스에서 사용자 지정 도메인 이름을 사용하는 경우 해당 서비스에 대한 설명서를 참조하세요.

## <a name="delete-a-custom-domain-name"></a>사용자 지정 도메인 이름 삭제
조직이 더 이상 해당 도메인 이름을 사용하지 않는 경우 또는 다른 Azure AD와 해당 도메인 이름을 사용해야 하는 경우, Azure AD에서 사용자 지정 도메인 이름을 삭제할 수 있습니다.

사용자 지정 도메인 이름을 삭제하려면 먼저 디렉터리에 도메인 이름을 사용하는 리소스가 없는지 확인해야 합니다. 다음의 경우 디렉터리에서 도메인 이름을 삭제할 수 없습니다.

* 임의 사용자가 도메인 이름을 포함하는 사용자 이름, 메일 주소 또는 프록시 주소 사용
* 임의 그룹이 도메인 이름을 포함하는 메일 주소 또는 프록시 주소 사용
* Azure AD의 임의 응용 프로그램이 도메인 이름을 포함하는 앱 ID URI 사용

사용자 지정 도메인 이름을 삭제하려면 먼저 Azure AD 디렉터리에서 이러한 리소스를 변경 또는 삭제해야 합니다.

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a>PowerShell 또는 Graph API를 사용하여 도메인 이름 관리
Azure Active Directory의 도메인 이름에 대한 대부분의 관리 작업은 Microsoft PowerShell을 사용하거나 프로그래밍 방식으로 Azure AD Graph API를 사용하여 완료할 수도 있습니다.

* [PowerShell을 사용하여 Azure AD에서 도메인 이름 관리](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Graph API를 사용하여 Azure AD에서 도메인 이름 관리](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>다음 단계
* [Azure AD에서 도메인 이름에 대해 알아보기](active-directory-add-domain-concepts.md)
* [사용자 지정 도메인 이름 관리](active-directory-add-manage-domain-names.md)

