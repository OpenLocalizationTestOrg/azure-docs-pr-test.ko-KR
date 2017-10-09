---
title: "Azure Active Directory tooauthenticate 일괄 처리 관리 솔루션 aaaUse | Microsoft Docs"
description: "Azure 리소스 관리자를 사용 하 여 빌드한 응용 프로그램 및 hello 일괄 처리 리소스 공급자는 Azure AD로 인증 합니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a>Active Directory를 사용하여 Batch Management 솔루션 인증

Hello Azure 일괄 처리 관리 서비스를 호출 하는 응용 프로그램으로 인증 [Azure Active Directory] [ aad_about] (Azure AD). Azure AD는 Microsoft의 다중 테넌트 클라우드 기반 디렉터리 및 ID 관리 서비스입니다. Azure 자체가 hello 고객, 서비스 관리자 및 조직 사용자를 인증 하기 위해 Azure AD를 사용 합니다.

hello Batch Management.NET 라이브러리는 일괄 처리 계정, 계정 키, 응용 프로그램 및 응용 프로그램 패키지를 사용 하기 위한 형식을 제공 합니다. hello Batch Management.NET 라이브러리는 Azure 리소스 공급자 클라이언트 이며와 함께 사용 [Azure 리소스 관리자] [ resman_overview] toomanage 이러한 리소스 프로그래밍 방식으로 합니다. Azure AD는 필요한 tooauthenticate 요청 및 모든 Azure 리소스 공급자를 포함 한 클라이언트 hello Batch Management.NET 라이브러리를 통해 [Azure 리소스 관리자][resman_overview]합니다.

이 문서에서는 Azure AD tooauthenticate hello Batch Management.NET 라이브러리를 사용 하는 응용 프로그램에서 사용 하 여 탐색 합니다. Azure AD toouse tooauthenticate 구독 관리자 또는 공동 관리자를 사용 하 여 통합 인증 방법을 보여줍니다. 사용 하 여 hello [AccountManagment] [ acct_mgmt_sample] 샘플 프로젝트를 Azure AD를 사용 하 여 hello Batch Management.NET 라이브러리를 통해 toowalk GitHub에서 사용할 수 있습니다.

hello Batch Management.NET 라이브러리 및 hello AccountManagement 샘플 사용에 대 한 더 toolearn 참조 [일괄 처리 관리 계정 및 할당량.NET 용 hello 일괄 처리 관리 클라이언트 라이브러리와](batch-management-dotnet.md)합니다.

## <a name="register-your-application-with-azure-ad"></a>Azure AD에 응용 프로그램 등록

Azure hello [Active Directory 인증 라이브러리] [ aad_adal] (ADAL)에 응용 프로그램 프로그래밍 인터페이스 tooAzure 사용 하기 위해 AD를 제공 합니다. 응용 프로그램에서 ADAL을 toocall, Azure AD 테 넌 트에 응용 프로그램을 등록 해야 합니다. 응용 프로그램을 등록 하는 경우에 hello Azure AD 테 넌 트 내에 대 한 이름을 포함 하 여 응용 프로그램에 대 한 정보로 Azure AD를 제공 합니다. 그런 다음 azure AD는 응용 프로그램 ID를 제공 합니다. 사용 하는 tooassociate 응용 프로그램 런타임 시 Azure AD와 합니다. hello 응용 프로그램 ID에 대해 자세히 toolearn 참조 [응용 프로그램 및 Azure Active Directory에서 서비스 보안 주체 개체](../active-directory/develop/active-directory-application-objects.md)합니다.

tooregister hello AccountManagement 샘플 응용 프로그램에서에서 다음과 같이 hello hello [응용 프로그램 추가](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) 섹션 [Azure Active Directory와 응용 프로그램 통합] [ aad_integrate]. 지정 **네이티브 클라이언트 응용 프로그램** hello 유형의 응용 프로그램에 대 한 합니다. 업계 hello hello에 대 한 표준 OAuth 2.0 URI **리디렉션 URI** 은 `urn:ietf:wg:oauth:2.0:oob`합니다. 그러나 모든 유효한 URI를 지정할 수 있습니다 (같은 `http://myaccountmanagementsample`) hello에 대 한 **리디렉션 URI**마찬가지로 toobe 실제 끝점이 필요 하지 않습니다:

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

Hello 등록 과정을 완료 되 면 hello 응용 프로그램 ID를 참조 하 고 응용 프로그램에 대해 나열 된 개체 (서비스 주체) ID hello 합니다.  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a>Hello Azure 리소스 관리자 API 액세스 tooyour 응용 프로그램에 부여

다음으로 toodelegate 액세스 tooyour 응용 프로그램 toohello Azure 리소스 관리자 API 필요 합니다. 리소스 관리자 API hello에 대 한 Azure AD hello 식별자가 **Windows Azure 서비스 관리 API**합니다.

Hello Azure 포털에서에서 다음이 단계를 수행 합니다.

1. Hello hello Azure 포털의 왼쪽 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**를 클릭 하 고 **추가**합니다.
2. 응용 프로그램 등록의 hello 목록에서 응용 프로그램의 hello 이름 검색:

    ![응용 프로그램 이름 검색](./media/batch-aad-auth-management/search-app-registration.png)

3. 디스플레이 hello **설정을** 블레이드입니다. Hello에 **API 액세스** 섹션에서 **필요한 권한**합니다.
4. 클릭 **추가** tooadd 새 필수 사용 권한. 
5. 1 단계에서 입력 **Windows Azure 서비스 관리 API**hello 결과 목록에서 해당 API를 선택 하 고 hello 클릭 **선택** 단추입니다.
6. 2 단계에서 선택 hello 확인란 옆 너무**조직 사용자로 Azure 액세스 클래식 배포 모델**, hello를 클릭 하 고 **선택** 단추입니다.
7. Hello 클릭 **수행** 단추입니다.

hello **필요한 권한** 블레이드 tooboth tooyour 응용 프로그램 사용 권한 부여 되었는지를 보여 줍니다. hello ADAL 및 리소스 관리자 Api는 이제 합니다. 먼저 Azure AD에 앱을 등록 하는 경우 권한은 기본적으로 tooADAL 부여 됩니다.

![대리자 사용 권한 toohello Azure 리소스 관리자 API](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a>Azure AD 끝점

tooauthenticate 일괄 처리 관리 솔루션을 Azure AD와 두 개의 잘 알려진 끝점이 필요 합니다.

- hello **Azure AD의 공통 끝점** 통합된 인증의 hello 경우 처럼 특정 테 넌 트가 제공 되지 않으면 인터페이스 수집 일반 자격 증명을 제공 합니다.

    `https://login.microsoftonline.com/common`

- hello **Azure 리소스 관리자 끝점** 사용 되는 tooacquire 요청 toohello 일괄 처리 관리 서비스를 인증 하기 위한 토큰입니다.

    `https://management.core.windows.net/`

hello AccountManagement 샘플 응용 프로그램은 이러한 끝점에 대 한 상수를 정의합니다. 해당 상수를 변경하지 않고 그대로 둡니다.

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a>응용 프로그램 ID 참조 

클라이언트 응용 프로그램 런타임 시 hello 응용 프로그램 ID (또한 참조 tooas hello 클라이언트 ID) tooaccess Azure AD를 사용합니다. Hello Azure 포털에서에서 응용 프로그램을 등록 한 후 등록 된 응용 프로그램에 대 한 Azure AD에서 제공 된 사용자 코드 toouse hello 응용 프로그램 ID를 업데이트 합니다. Hello AccountManagement 샘플 응용 프로그램에서는 hello Azure 포털 toohello 적절 한 상수에서 응용 프로그램 ID를 복사 합니다.

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
또한 hello 리디렉션 hello 등록 프로세스 중에 지정 된 URI를 복사 합니다. 코드에서 지정 된 URI는 hello 리디렉션 hello 리디렉션 URI hello 응용 프로그램 등록 시 입력 한 일치 해야 합니다.

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a>Azure AD 인증 토큰 획득

Hello AccountManagement 샘플 hello Azure AD 테 넌 트에 등록 하 고 원하는 값으로 hello 샘플 소스 코드를 업데이트 후 hello 샘플은 Azure AD를 사용 하 여 준비 tooauthenticate입니다. Hello 샘플을 실행 하면 hello ADAL tooacquire 인증 토큰을 시도 합니다. 이 단계에서 Microsoft 자격 증명을 묻습니다. 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

자격 증명을 제공 hello 샘플 응용 프로그램 인증 tooissue 요청 toohello 일괄 처리 관리 서비스 계속 진행할 수 있습니다. 

## <a name="next-steps"></a>다음 단계

Hello 실행에 대 한 자세한 내용은 [AccountManagement 샘플 응용 프로그램][acct_mgmt_sample], 참조 [일괄 처리 관리 계정 및 할당량for.nethello일괄처리관리클라이언트라이브러리와](batch-management-dotnet.md).

Azure AD에 대해 자세히 toolearn 참조 hello [Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)합니다. ADAL toouse hello에서 사용할 수 있는 방법을 보여 주는 상세한 예제 [Azure 코드 예제](https://azure.microsoft.com/resources/samples/?service=active-directory) 라이브러리입니다.

Azure AD를 사용 하 여 tooauthenticate 일괄 처리 서비스 응용 프로그램 참조 [Active Directory를 사용 하 여 인증 하는 일괄 처리 서비스 솔루션](batch-aad-auth.md)합니다. 


[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory란?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD의 인증 시나리오"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Azure Active Directory와 응용 프로그램 통합"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
