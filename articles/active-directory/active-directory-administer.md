---
title: "aaaHow toouse 활성 Direcory Azure 테 넌 트 디렉터리 개요 | Microsoft Docs"
description: "파악할 수를 같은 Azure AD 테 넌 트와 방법을 toomanage Azure Active Directory를 사용 하 여 Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro;oldportal
ms.openlocfilehash: ddb16d89bf06a3753ed5106bd95162130ad51b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-ad-directory"></a>Azure AD 디렉터리 관리

## <a name="what-is-an-azure-ad-tenant"></a>Azure AD 테넌트란?
Azure AD(Azure Active Directory)에서 테넌트는 조직이 Azure 또는 Office 365와 같은 Microsoft 클라우드 서비스에 등록할 때 수신하는 Azure AD 디렉터리의 전용 인스턴스입니다. 각 Azure AD 디렉터리는 고유하며 다른 Azure AD 디렉터리와 구분됩니다. 기업의 사무실 건물이 마찬가지로 보안 자산 특정 tooonly 조직, Azure AD 디렉터리 서버가 있는 보안 자산만 조직에서 사용 하기 위해 디자인 된 toobe 이기도 합니다. hello Azure AD 아키텍처에서는 사용자와 Azure AD 디렉터리의 관리자가 액세스할 수 없도록 실수로 또는 악의적으로 다른 디렉터리의 데이터 고객 데이터와 id 정보가 격리 됩니다.

![Azure Active Directory 관리](./media/active-directory-administer/aad_portals.png)

## <a name="how-can-i-get-an-azure-ad-directory"></a>Azure AD 디렉터리를 받으려면 어떻게 하나요?
Azure AD hello 핵심 디렉터리 및 id 뒤에 있는 대부분의 Microsoft 클라우드 서비스를 포함 하 여 관리 기능을 제공 합니다.

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

Azure AD 디렉터리는 이러한 Microsoft 클라우드 서비스에 등록하면 제공됩니다. 필요에 따라 추가 디렉터리를 만들 수 있습니다. 예를 들어 첫 번째 디렉터리는 프로덕션 디렉터리로 유지 관리하고 테스트나 준비용으로 다른 디렉터리를 만들 수 있습니다.

### <a name="using-hello-azure-ad-directory-that-comes-with-a-new-azure-subscription"></a>새 Azure 구독와 함께 제공 되는 hello Azure AD 디렉터리를 사용 하 여

첫 번째 서비스에 대 한 다른 Microsoft 서비스에 등록할 때 사용 하는 hello 관리자 계정을 사용 하는 것이 좋습니다. hello 정보를 제공 하는 hello Microsoft 서비스를 사용 하는 toocreate 새로운 Azure에 대 한 등록 처음으로 조직에 대 한 AD 디렉터리 인스턴스. 해당 디렉터리 tooauthenticate를 사용 하는 경우 로그인 시도 tooother Microsoft 서비스를 구독 하면, 사용자 계정, 정책, 설정 또는 온-프레미스 디렉터리 통합 기본 디렉터리에 구성한 기존 hello를 사용할 수 있습니다.

예를 들어, Microsoft Intune 구독에 대 한 최대 로그인 한 다음 추가 온-프레미스 Active Directory를 Azure AD 디렉터리와 동기화 하는 경우 Office 365와 같은 다른 Microsoft 서비스에 등록 하 수 hello를 쉽게 달성 동일한 디렉터리 Microsoft Intune을 사용 해야 하는 통합의 혜택.

Azure AD와 온-프레미스 디렉터리 통합에 대한 자세한 내용은 [Azure AD Connect와 디렉터리 통합](active-directory-aadconnect.md)을 참조하세요.

### <a name="associate-an-existing-azure-ad-directory-with-a-new-azure-subscription"></a>새 Azure 구독과 기존 Azure AD 디렉터리 연결
Hello로 새 Azure 구독을 연결할 수 있습니다 기존 Office 365 또는 Microsoft Intune 구독에 대 한 한 로그인을 인증 하는 동일한 디렉터리입니다. 이 시나리오에 대 한 자세한 내용은 참조 하세요. [의 Azure 구독 tooanother 계정 소유권 이전](../billing/billing-subscription-transfer.md)

### <a name="create-an-azure-ad-directory-by-signing-up-for-a-microsoft-cloud-service-as-an-organization"></a>조직으로 Microsoft 클라우드 서비스에 등록하여 Azure AD 디렉터리 만들기
구독 tooa Microsoft 클라우드 서비스를 아직 없는 경우 링크 toosign 이후의 hello 중 하나를 사용할 수 있습니다. 첫 번째 서비스에 등록하면 Azure AD 디렉터리가 자동으로 만들어집니다.

* [Microsoft Azure](https://account.azure.com/organization)
* [Office 365](http://products.office.com/business/compare-office-365-for-business-plans/)
* [Microsoft Intune](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20)

### <a name="how-toochange-hello-default-directory-for-a-subscription"></a>어떻게 toochange hello 구독에 대 한 기본 디렉터리

1. Toohello 로그인 [Azure 계정 센터](https://account.windowsazure.com/Home/Index) hello hello 구독 tootransfer 구독 소유권의 계정 관리자에 해당 하는 계정을 사용 합니다.
2. 해당 hello 게 사용자에 게 toobe hello 구독 소유자는 hello 대상 디렉터리를 확인 합니다.
3. **구독 이전**을 클릭합니다.
4. Hello 받는 사람을 지정 합니다. hello 받는 사람 전자 메일을 동의 링크를 자동으로 가져옵니다.
5. hello 받는 사람 hello 링크를 클릭 하 고 지불 정보를 입력 하는 등 hello 지침을 따릅니다. Hello 받는 사람에 성공 하면 hello 구독 전송 됩니다. 
6. hello hello 구독의 기본 디렉터리 변경 toohello 디렉터리 사용자 hello 하는 hello 구독 소유권 전송이 성공한 것입니다.

### <a name="manage-hello-default-directory-in-azure"></a>Azure의 hello 기본 디렉터리 관리
Azure에 등록하면 기본 Azure AD 디렉터리가 구독과 연결됩니다. Azure AD를 사용하는 비용이 청구되지 않고 디렉터리는 체험용 리소스입니다. 별도로 사용이 허가되고 로그인 시 회사 브랜딩 및 셀프 서비스 암호 재설정과 같은 추가 기능을 제공하는 Azure AD 서비스에는 비용이 청구됩니다. 소유 하 고 있는 DNS 이름을 사용 하 여 hello 기본값 대신 사용자 지정 도메인을 만들 수도 있습니다 *. onmicrosoft.com 도메인입니다.

## <a name="how-can-i-manage-directory-data"></a>디렉터리 데이터를 관리하는 방법
tooadminister 하나 이상의 Microsoft 클라우드 서비스 구독이 hello를 사용할 수 있습니다 [Azure AD 관리 센터](https://aad.portal.azure.com), Microsoft Intune 계정 포털 hello 또는 hello [Office 365 관리 센터](https://portal.office.com/) toomanage 프로그램 조직의 디렉터리 데이터입니다. 사용할 수도 있습니다 [Azure Active Directory PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/active-directory) Azure AD에 저장 된 데이터 관리 toohelp 합니다.

이러한 포털(또는 cmdlet)에서는 다음을 수행할 수 있습니다.

* 사용자 및 그룹 계정 만들기 및 관리
* 조직의 구독에서 관련 클라우드 서비스 관리
* Azure AD ID 및 인증 서비스와 온-프레미스 통합 설정

hello Azure AD 관리 센터, Office 365 관리 센터, Microsoft Intune 계정 포털 및 Azure AD cmdlet hello 모두에서 읽고 쓰는 tooa 조직의 디렉터리와 연결 된 Azure AD의 단일 공유 인스턴스. 해당 도구는 각각 디렉터리 데이터를 가져오거나 변경하는 프런트 엔드 인터페이스로 작동합니다.

Hello 포털 또는 cmdlet의 이러한 서비스 중 하나의 hello 컨텍스트 내에서 로그인 한 상태 중 하나를 사용 하 여 조직의 데이터를 변경 하면 hello 변경 된 나타납니다 hello에 다른 포털 hello 다음에 로그인 할 때입니다. 이 데이터는 hello Microsoft 클라우드 서비스 toowhich 구독 간에 공유 됩니다.

예를 들어, 사용 하는 경우 Office 365 관리 센터 tooblock hello 로그인에서 사용자 동작 블록 hello tooany 로그인에서 사용자는 다른 서비스 toowhich 조직은 현재 구독. Hello를 보면 hello Microsoft Intune 계정 포털에서 동일한 사용자 계정 표시 해당 hello 사용자가 차단 되었습니다.

## <a name="how-can-i-add-and-manage-multiple-directories"></a>여러 디렉터리를 추가하고 관리하려면 어떻게 하나요?
있습니다 수 [hello Azure 포털에서에서 Azure AD 디렉터리 추가](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory)합니다. Hello 정보를 입력 하 고 선택 **만들기**합니다.

각 디렉터리를 완전히 독립된 리소스로 관리할 수 있습니다. 각 디렉터리는 관리하는 다른 디렉터리와 논리적으로 독립된 완전한 기능을 갖춘 피어이며, 디렉터리 간에는 부모 자식 관계가 없습니다. 디렉터리 간 독립성에는 리소스 독립성, 관리 독립성 및 동기화 독립성이 포함됩니다.

* **리소스 독립성**. 만들거나 특정 디렉터리에서 리소스를 삭제 하는 경우 외부 사용자의 일부 예외가 적용 hello와 다른 디렉터리의 리소스에 영향을 주어에 있습니다. 한 디렉터리에서 사용자 지정 도메인 'contoso.com'을 사용하는 경우 다른 디렉터리에서 사용할 수 없습니다.
* **관리 독립성**.  'Contoso' 디렉터리의 관리자가 아닌 사용자가 테스트 디렉터리 ‘Test’를 만들면 다음과 같이 수행됩니다.
  
  * 'Contoso' 디렉터리의 hello 관리자 's t'의 관리자 구체적으로 부여 이러한 권한이 없는 직접 관리 권한이 toodirectory 'Test' 있어야 합니다. 'Contoso'의 관리자 제어 만든 'Test' hello 사용자 계정을를 통해 액세스 toodirectory 's t'를 제어할 수 있습니다.
    
  * 에 할당 하거나 제거 hello 변경, 특정 디렉터리에서 사용자에 대 한 관리자 역할 있는 관리자 역할에는 영향을 주지 다른 디렉터리에 해당 사용자 있을 수 있습니다.
* **동기화 독립성**. 구성한 각 Azure AD 테 넌 트 하지 독립적으로 tooget 데이터는 단일 인스턴스 hello Azure AD Connect 디렉터리 동기화 도구에서 동기화 합니다.

다른 Azure 리소스와 달리 디렉터리는 Azure 구독의 자식 리소스가 아닙니다. 따라서를 취소 하거나 Azure 구독 tooexpire 허용 하는 경우 hello Office 365 관리 센터와 같은 Azure AD PowerShell, hello Azure Graph API 또는 다른 인터페이스를 사용 하 여 디렉터리 데이터에 계속 액세스할 수 있습니다. Hello 디렉터리와 다른 구독을 연결할 수도 있습니다.

## <a name="how-tooprepare-toodelete-an-azure-ad-directory"></a>어떻게 tooprepare toodelete Azure AD 디렉터리
전역 관리자는 hello 포털에서 Azure AD 디렉터리를 삭제할 수 있습니다. 디렉터리 삭제 되 면 hello 디렉터리에 포함 된 리소스를 모두 삭제 됩니다. 있는지 있습니다 없습니다 필요 hello 디렉터리 삭제 하기 전에 확인 합니다.

> [!NOTE]
> Hello 사용자가 회사 또는 학교 계정으로 로그인 하는 경우 hello 사용자 시도 하면 안 toodelete 홈 디렉터리입니다. 예를 들어 경우 hello 사용자가 로그인으로 joe@contoso.onmicrosoft.com, 해당 사용자는 기본 도메인이 contoso.onmicrosoft.com 있는 hello 디렉터리를 삭제할 수 없습니다.

Azure AD 특정 조건이 충족된 toodelete 디렉터리에 있어야 합니다. 이 부정적인는 디렉터리를 삭제 하면 사용자 또는 사용자 toosign tooOffice 365에서에서 또는 Azure의 리소스에 액세스 하는 hello 기능 등의 응용 프로그램에 영향을 주는 위험을 줄입니다. 예를 들어 구독에 대 한 디렉터리를 실수로 삭제 한 경우 다음 사용자가 액세스할 수 없습니다 hello 해당 구독에 대 한 Azure 리소스입니다.

다음 조건 hello 확인 됩니다.

* hello hello 디렉터리의 사용자만 관리자 여야 합니다. hello 전역 toodelete hello 디렉터리입니다. Hello 디렉터리를 삭제 하려면 먼저 다른 사용자를 삭제 합니다. 온-프레미스에서 사용자를 동기화 면 off, 동기화가 설정 되어 있어야 하 고 hello 사용자를 사용 하 여 hello 클라우드 디렉터리에서 삭제 해야 hello Azure 포털 또는 Azure PowerShell cmdlet. 요구 사항 toodelete 그룹 또는 연락처 hello Office 365 관리 센터에서 추가한 연락처 등 없습니다 있습니다.
* Hello 디렉터리에 응용 프로그램이 있을 수 있습니다. Hello 디렉터리를 삭제 하기 전에 모든 응용 프로그램을 삭제 되어야 합니다.
* 다단계 인증 공급자가 없습니다 연결된 toohello 디렉터리 수 있습니다.
* Hello 디렉터리와 연결 된 Azure AD Premium 또는 Microsoft Azure, Office 365 등의 Microsoft Online Services에 대 한 구독이 없는 수 있습니다. 예를 들어 Azure에서 직접 기본 디렉터리를 만든 경우 Azure 구독에서 인증에 이 디렉터리를 계속 사용하면 이 디렉터리를 삭제할 수 없습니다. 마찬가지로 다른 사용자가 구독을 연결한 경우 디렉터리를 삭제할 수 없습니다. 


## <a name="next-steps"></a>다음 단계
* [Azure AD 포럼](https://social.msdn.microsoft.com/Forums/home?forum=WindowsAzureAD)
* [Azure Multi-Factor Authentication Forum](https://social.msdn.microsoft.com/Forums/home?forum=windowsazureactiveauthentication)
* [Azure 질문에 대한 Stack Overflow](http://stackoverflow.com/questions/tagged/azure)
* [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory)
* [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)
