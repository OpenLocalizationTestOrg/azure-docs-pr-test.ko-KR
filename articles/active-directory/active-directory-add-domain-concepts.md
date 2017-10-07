---
title: "Azure Active Directory에서 사용자 지정 도메인 이름 aaaConceptual 개요 | Microsoft Docs"
description: "Single sign on에 대 한 페더레이션의 포함 하 여 Azure Active directory에 사용자 지정 도메인 이름을 사용 하기 위한 hello 개념적인 프레임 워크에 설명"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fd0c5def-0da2-43af-81bc-76f4cfe86afd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 0a3454ae6b733a8a13a71925df3cc664063f388e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="conceptual-overview-of-custom-domain-names-in-azure-active-directory"></a>Azure Active Directory에서 사용자 지정 도메인 이름의 개념적 개요
도메인 이름은 다음의 일부로 많은 디렉터리 리소스에 대한 중요한 식별자일 수 있습니다.

* 사용자 이름 또는 사용자에 대한 전자 메일 주소
* 그룹에 대 한 hello 주소
* 응용 프로그램에 대 한 hello 앱 ID URI

Azure Active Directory (Azure AD)에 리소스 toobe hello 리소스가 포함 된 hello 디렉터리에 의해 소유 이미 확인 된 도메인 이름을 포함할 수 있습니다. 전역 관리자만 Azure AD에서 도메인 관리 작업을 수행할 수 있습니다.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. 어떻게 toomanage 도메인 이름 hello Azure AD 관리 센터에서 참조 [Azure Active Directory에서 사용자 지정 도메인 이름을 관리](active-directory-domains-manage-azure-portal.md)합니다.

Azure AD의 도메인 이름은 전역적으로 고유합니다. 사용자 지정 도메인 이름은 한 번에 하나의 Azure AD 테넌트에서 사용할 수 있습니다. 한 Azure AD 디렉터리에서 도메인 이름을 확인했다면 다른 Azure AD 디렉터리에서 동일한 도메인 이름을 확인하거나 사용할 수 없습니다.

## <a name="initial-and-custom-domain-names"></a>초기 및 사용자 지정 도메인 이름
Azure AD에서 모든 도메인 이름은 초기 도메인 이름이거나 사용자 지정 도메인 이름입니다.

모든 Azure AD는 hello 양식 contoso.onmicrosoft.com 된 초기 도메인 이름을 함께 제공 됩니다. 이 예에서 "contoso.onmicrosoft.com"이 세 번째 수준 도메인 이름으로 hello 디렉터리를 만들 때, 일반적으로 hello 디렉터리를 만든 admin 님 안녕하세요도 설정 되었습니다. 디렉터리에 대 한 hello 초기 도메인 이름은 변경 하거나 삭제할 수 없습니다. hello 초기 도메인 이름 완벽 하 게 작동 하는 동안는 대상 사용자 지정 도메인 이름의 찾을 때까지 부트스트래핑 메커니즘으로 사용 하는 toobe 주로 확인 합니다.

대부분의 프로덕션 환경에서 디렉터리에 "contoso.com"와 같은 하나 이상의 확인 된 사용자 지정 도메인이 되며 해당 사용자 지정 도메인은 표시 tooend 사용자가 있습니다. 사용자 지정 도메인 이름은 해당 조직이 소유하고 사용하는 도메인 이름입니다. 예를 들면, “contoso.com”은 해당사의 웹 사이트 호스팅 같은 용도로 사용됩니다. 이 도메인 이름은 toosign toohello 회사 네트워크 또는 toosend에 사용 하 고 전자 메일을 검색 하는 hello 사용자 이름의 속해 있기 때문에 친숙 한 tooemployees를입니다.

Azure AD에서 사용할 수 있습니다, 전에 hello 사용자 지정 도메인 이름을 추가 tooyour 디렉터리 여야 및 확인 합니다.

## <a name="verified-and-unverified-domain-names"></a>확인 및 확인되지 않은 도메인 이름
디렉터리에 대 한 hello 초기 도메인 이름은 Azure AD에 의해 확인 된 것에 암시적으로 계산 됩니다. 관리자가 Azure AD는 사용자 지정 도메인 이름을 tooan 추가, 경우에 처음 확인 되지 않은 상태에 있습니다. Azure AD 디렉터리 리소스 toouse 모든 확인 되지 않은 도메인 이름을 허용 하지 않습니다. 이렇게 하면 디렉터리를 하나만 특정 도메인 이름에 사용할 수 있고 해당 도메인 이름을 소유 하 고 실제로 hello 조직 hello 도메인 이름을 사용 하는 합니다.

Azure AD는 hello 도메인 이름에 대 한 hello 도메인 이름 (DNS) 서비스 영역 파일에서 특정 항목을 검색 하 여 도메인 이름의 소유권을 확인 합니다. 도메인 이름의 소유권 tooverify 관리자가 가져옵니다 hello DNS 항목 Azure AD에서 Azure AD는 찾습니다, 그리고 및 hello 도메인 이름에 대 한 해당 항목 toohello DNS 영역 파일을 추가 합니다. 해당 도메인에 대 한 hello 도메인 이름 등록자에서 DNS 영역 파일 hello 유지 됩니다. 도메인에 대 한 hello 문서에 표시 됩니다는 hello 단계 tooverify [사용자 지정 도메인 tooyour Azure AD 디렉터리 추가](active-directory-add-domain.md)합니다.

Hello 도메인 이름에 대 한 DNS 항목 toohello 영역 파일에 추가 웹 호스팅 또는 메일과 같은 다른 도메인 서비스는 영향을 주지 않습니다.

## <a name="federated-and-managed-domain-names"></a>페더레이션 및 관리되는 도메인 이름
Azure AD에서 사용자 지정 도메인 이름이 구성된 toogive 사용자 경험 온-프레미스 Active Directory와 Azure AD 간의 페더레이션된 로그인 일 수 있습니다. Azure AD에서 tooprivileged 리소스 업데이트 페더레이션 용 도메인을 구성 하 고 Windows Server Active Directory tooyour도 합니다. Azure AD Connect에서 또는 PowerShell을 사용하여 페더레이션된 도메인 구성을 완료해야 합니다. 사용자 지정 도메인을 페더레이션 하는 hello Azure 클래식 포털에서에서 초기화할 수 없습니다. [Azure AD Connect 사용 하 여 사용자 로그인에 대 한 AD FS를 구성 하는 방법에 대 한이 비디오 toolearn 시청](http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect)합니다.

경우에 따라 페더레이션되지 않은 도메인을 관리되는 도메인이라고 합니다. Azure AD 디렉터리에 대 한 hello 초기 도메인 관리 되는 도메인으로 암시적으로 계산 됩니다.

## <a name="primary-domain-names"></a>주 도메인 이름
hello 주 도메인 이름이 디렉터리에 대 한 hello 도메인 이름이 hello에 새 사용자를 만들 때 기본값으로 hello hello 사용자 이름의 도메인' hello' 부분에 대 한 미리 선택 되어 있는 [Azure 포털](https://portal.azure.com/), 또는 다른 포털 예: hello Office 365 관리 포털 또는 Microsoft Intune 포털 hello 합니다. 디렉터리에는 하나의 주 도메인 이름만 있을 수 있습니다. 모든 페더레이션 되지 않아서 확인 된 사용자 지정 도메인 또는 toohello 초기 도메인 관리자가 hello 주 도메인 이름 toobe을 변경할 수 있습니다.

## <a name="domain-names-in-azure-ad-and-other-microsoft-online-services"></a>Azure AD 및 기타 Microsoft Online Services에서 도메인 이름
Exchange Online, SharePoint Online 및 Intune과 같은 또 다른 Microsoft Online Services에서 사용할 수 있도록 먼저 Azure AD에서 도메인 이름을 확인해야 합니다. 이러한 다른 서비스는 일반적으로 관리자 tooadd 특정 toohello 서비스는 하나 이상의 DNS 항목이 필요 합니다.

Azure 웹 응용 프로그램 도메인의 고유 메커니즘 tooverify 소유권을 사용합니다. Azure AD에 의존하는 구독의 Azure 웹앱에서 사용하기 위해 이전에 확인한 경우에도 Azure AD에서 사용하기 위해 도메인을 확인해야 합니다. Azure 웹 앱 hello 웹 응용 프로그램을 보호 하는 hello 디렉터리에서 다른 디렉터리에 있는 확인 된 도메인 이름을 사용할 수 있습니다.

## <a name="managing-domain-names"></a>도메인 이름 관리
PowerShell 및 hello Azure 클래식 포털에서에서 도메인 관리 작업을 완료할 수 있습니다. Hello Azure AD Graph API를 사용 하 여 다양 한 작업을 완료할 수 있습니다.

* [사용자 지정 도메인 이름 추가 및 확인](active-directory-add-domain.md)
* [Hello Azure 클래식 포털에서에서 도메인 관리](active-directory-add-manage-domain-names.md)
* [Azure ad에서 PowerShell toomanage 도메인 이름을 사용 하 여](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Azure AD에서 Azure AD Graph API hello toomanage 도메인 이름을 사용 하 여](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

