---
title: "aaaUse Azure Active Directory tooauthenticate Azure 배치 서비스 솔루션 | Microsoft Docs"
description: "일괄 처리는 hello 일괄 처리 서비스에서에서 인증을 위한 Azure AD를 지원합니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a>Active Directory를 사용하여 Batch 서비스 솔루션 인증

Azure Batch는 [Azure Active Directory][aad_about](Azure AD) 인증을 지원합니다. Azure AD는 Microsoft의 다중 테넌트 클라우드 기반 디렉터리 및 ID 관리 서비스입니다. Azure는 고객, 서비스 관리자 및 조직 사용자가 Azure AD tooauthenticate 자체가 사용 합니다.

Azure Batch와 함께 Azure AD 인증을 사용할 때 다음 두 가지 방법 중 하나로 인증할 수 있습니다.

- 사용 하 여 **통합된 인증** tooauthenticate가 hello 응용 프로그램 상호 작용 하는 사용자입니다. 통합된 인증을 사용 하 여 응용 프로그램 사용자의 자격 증명을 수집 하 고 해당 자격 증명 tooauthenticate tooBatch 리소스에 액세스를 사용 합니다.
- 사용 하 여 한 **서비스 사용자** tooauthenticate 무인된 응용 프로그램입니다. 서비스 사용자는 런타임에 리소스에 액세스할 때 순서 toorepresent hello 응용 프로그램에 hello 정책 및 응용 프로그램에 대 한 사용 권한을 정의 합니다.

Azure AD에 대해 자세히 toolearn 참조 hello [Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)합니다.

## <a name="authentication-and-pool-allocation-mode"></a>인증 및 풀 할당 모드

배치 계정을 만들 때 해당 계정에 대해 생성된 풀을 할당해야 하는 위치를 지정할 수 있습니다. 사용자 구독 또는 hello 기본 일괄 처리 서비스 구독에 tooallocate 풀을 선택할 수 있습니다. 사용자가 선택한 해당 계정에 대 한 액세스 tooresources를 인증 하는 방법에 영향을 줍니다.

- **Batch 서비스 구독** - 기본적으로 Batch 풀은 Batch 서비스 구독에 할당됩니다. 이 옵션을 선택 하는 경우를 인증할 수 있습니다 액세스 tooresources 해당 계정에서 사용 하 여 [공유 키](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) 또는 Azure AD와 합니다.
- **사용자 구독** - 지정한 사용자 구독에 tooallocate 일괄 처리 풀을 선택할 수 있습니다. 이 옵션을 선택하는 경우 Azure AD로 인증해야 합니다.

## <a name="endpoints-for-authentication"></a>인증에 대한 끝점

tooinclude 해야 Azure AD와 tooauthenticate 일괄 처리 응용 프로그램 코드에서 잘 알려진 일부 끝점입니다.

### <a name="azure-ad-endpoint"></a>Azure AD 끝점

기본 hello Azure AD 권한 끝점은:

`https://login.microsoftonline.com/`

Azure AD와 tooauthenticate, hello 테 넌 트 ID (디렉터리 ID)와 함께이 끝점을 사용 합니다. hello 테 넌 트 ID를 인증에 대 한 hello Azure AD 테 넌 트 toouse를 식별합니다. tooretrieve hello 테 넌 트 ID에 설명 된 hello 단계에 따라 [hello 테 넌 트 ID를 Azure Active Directory에 대 한 가져오기](#get-the-tenant-id-for-your-active-directory):

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> 서비스 사용자를 사용 하 여 인증 hello 테 넌 트 별 끝점이 필요 합니다. 
> 
> hello 테 넌 트 별 끝점 통합된 인증을 사용 하 여 인증 하는 경우 선택 사항 이지만 권장 됩니다. 그러나 hello Azure AD의 공통 끝점을 사용할 수 있습니다. hello 일반 끝점이 특정 테 넌 트가 제공 되지 않으면 인터페이스 수집 일반 자격 증명을 제공 합니다. hello 공용 끝점을 `https://login.microsoftonline.com/common`합니다.
>
>

Azure AD 끝점에 대한 자세한 내용은 [Azure AD의 인증 시나리오][aad_auth_scenarios]를 참조하세요.

### <a name="batch-resource-endpoint"></a>Batch 리소스 끝점

사용 하 여 hello **Azure 배치 리소스 끝점** tooacquire 인증을 위한 토큰 toohello 일괄 처리 서비스를 요청 합니다.

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a>테넌트에 응용 프로그램 등록

hello tooauthenticate Azure AD를 사용 하 여 첫 번째 단계는 Azure AD 테 넌 트의 응용 프로그램을 등록 합니다. Toocall hello Azure 응용 프로그램을 등록 하면 [Active Directory 인증 라이브러리] [ aad_adal] (ADAL) 사용자 코드에서. ADAL hello 응용 프로그램에서 Azure AD에 인증 하기 위해 API를 제공 합니다. Toouse 통합된 인증 또는 서비스 사용자를 계획 하 고 있는지 여부를 응용 프로그램 등록가 필요 합니다.

응용 프로그램을 등록 하는 경우에 프로그램 응용 프로그램 tooAzure AD에 대 한 정보를 제공 합니다. 그런 다음 azure AD는 응용 프로그램 ID를 제공 합니다. 사용 하는 tooassociate 응용 프로그램 런타임 시 Azure AD와 합니다. hello 응용 프로그램 ID에 대해 자세히 toolearn 참조 [응용 프로그램 및 Azure Active Directory에서 서비스 보안 주체 개체](../active-directory/develop/active-directory-application-objects.md)합니다.

tooregister hello의 hello 단계에 따라 일괄 처리 응용 프로그램 [응용 프로그램 추가](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) 섹션 [Azure Active Directory와 응용 프로그램 통합][aad_integrate]합니다. Hello에 대 한 모든 유효한 URI를 지정할 수는 네이티브 응용 프로그램으로 응용 프로그램을 등록 하는 경우 **리디렉션 URI**합니다. 실제 끝점 toobe가 필요는 없습니다.

응용 프로그램에 등록 한 후 hello 응용 프로그램 ID에 표시 됩니다.

![Azure AD에 Batch 응용 프로그램 등록](./media/batch-aad-auth/app-registration-data-plane.png)

Azure AD에 응용 프로그램을 등록하는 방법에 대한 자세한 내용은 [Azure AD의 인증 시나리오](../active-directory/develop/active-directory-authentication-scenarios.md)를 참조하세요.

## <a name="get-hello-tenant-id-for-your-active-directory"></a>Active Directory에 대 한 hello 테 넌 트 ID 가져오기

hello 테 넌 트 ID 인증 서비스 tooyour 응용 프로그램을 제공 hello Azure AD 테 넌 트를 식별 합니다. tooget hello 테 넌 트 ID, 다음이 단계를 수행 합니다.

1. Hello Azure 포털에서에서 Active Directory를 선택 합니다.
2. **속성**을 클릭합니다.
3. Hello 디렉터리 ID에 대해 제공 된 hello GUID 값 복사 이 값은 테 넌 트 ID hello 라고도

![Hello 디렉터리 ID 복사](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a>통합 인증 사용

통합 인증으로 tooauthenticate toogrant 응용 프로그램 사용 권한 tooconnect toohello 일괄 처리 서비스 API를 해야 합니다. 이 단계에서는 Azure AD와 응용 프로그램 tooauthenticate 호출 toohello 일괄 처리 서비스 API입니다.

한 후 [응용 프로그램 등록](#register-your-application-with-an-azure-ad-tenant), hello toohello 일괄 처리 서비스에 액세스 하는 Azure 포털 toogrant에서에서 다음이 단계를 수행 합니다.

1. Hello hello Azure 포털의 왼쪽 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**합니다.
2. 응용 프로그램 등록의 hello 목록에서 응용 프로그램의 hello 이름 검색:

    ![응용 프로그램 이름 검색](./media/batch-aad-auth/search-app-registration.png)

3. 열기 hello **설정을** 블레이드 응용 프로그램에 대 한 합니다. Hello에 **API 액세스** 섹션에서 **필요한 권한**합니다.
4. Hello에 **필요한 권한** 블레이드에서 hello 클릭 **추가** 단추입니다.
5. 1 단계에서 일괄 처리 API hello에 대 한 검색 합니다. Hello API를 찾을 때까지 이러한 문자열에 대 한 검색:
    1. **MicrosoftAzureBatch**
    2. **Microsoft Azure Batch** - 최신 Azure AD 테넌트에서는 이 이름을 사용할 수도 있습니다.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** hello 일괄 처리 API에 대 한 hello id입니다. 
6. 일괄 처리 API hello를 찾은 후 선택 하 고 hello 클릭 **선택** 단추입니다.
6. 2 단계에서 선택 hello 확인란 옆 너무**Access Azure 일괄 처리 서비스** hello 클릭 **선택** 단추입니다.
7. Hello 클릭 **수행** 단추입니다.

hello **필요한 권한** 블레이드 이제 Azure AD 응용 프로그램에 표시 tooboth ADAL에 액세스 하 고 일괄 처리 서비스 API hello 합니다. 먼저 Azure AD에 앱을 등록 하는 경우 권한은 tooADAL은 자동으로 부여 됩니다.

![API 권한 부여](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a>서비스 주체 사용 

tooauthenticate 무인 모드로 실행 되는 응용 프로그램, 서비스 사용자를 사용 합니다. 응용 프로그램에 등록 한 후에 hello Azure 포털 tooconfigure 서비스 사용자의 다음이 단계를 따르십시오.

1. 응용 프로그램에 대한 비밀 키를 요청합니다.
2. RBAC 역할 tooyour 응용 프로그램을 할당 합니다.

### <a name="request-a-secret-key-for-your-application"></a>응용 프로그램에 대한 비밀 키 요청

응용 프로그램 서비스 사용자를 인증 하는 경우 hello 응용 프로그램 ID 및 비밀 키 tooAzure AD 모두 보냅니다. Toocreate 필요 하 고 사용자 코드에서 비밀 키 toouse hello를 복사 합니다.

Hello Azure 포털에서에서 다음이 단계를 수행 합니다.

1. Hello hello Azure 포털의 왼쪽 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**합니다.
2. 응용 프로그램 등록의 hello 목록에서 응용 프로그램의 hello 이름을 검색 합니다.
3. 디스플레이 hello **설정을** 블레이드입니다. Hello에 **API 액세스** 섹션에서 **키**합니다.
4. 키를 toocreate hello 키에 대 한 설명을 입력 합니다. 하나 또는 두 개의 년의 hello 키에 대 한 기간을 선택 합니다. 
5. Hello 클릭 **저장** toocreate 단추 및 hello 키를 표시 합니다. 수 tooaccess 수 없을 것 처럼 hello 키 값 tooa 안전한 곳을 복사 후 다시 hello 블레이드를 둡니다. 

    ![비밀 키 만들기](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a>RBAC 역할 tooyour 응용 프로그램 할당

서비스 사용자와 tooauthenticate, tooassign RBAC 역할 tooyour 응용 프로그램이 필요합니다. 다음 단계를 수행하세요.

1. Hello Azure 포털에서에서 응용 프로그램에서 사용 하는 일괄 처리 계정 toohello를 탐색 합니다.
2. Hello에 **설정** 선택 hello 일괄 처리 계정에 대 한 블레이드 **액세스 제어 (IAM)**합니다.
3. Hello 클릭 **추가** 단추입니다. 
4. Hello에서 **역할** 드롭다운 목록에서 선택 하거나 hello _참가자_ 또는 _판독기_ 응용 프로그램에 대 한 역할입니다. 이러한 역할에 대 한 자세한 내용은 참조 하십시오. [hello Azure 포털에서에서 역할 기반 액세스 제어를 시작 하려면](../active-directory/role-based-access-control-what-is.md)합니다.  
5. Hello에 **선택** 필드에, 응용 프로그램의 hello 이름을 입력 합니다. Hello 목록에서 응용 프로그램을 선택 하 고 클릭 **저장**합니다.

이제 액세스 제어 설정에서 RBAC 역할이 할당된 응용 프로그램이 표시됩니다. 

![RBAC 역할 tooyour 응용 프로그램 할당](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a>Azure Active Directory에 대 한 hello 테 넌 트 ID 가져오기

hello 테 넌 트 ID 인증 서비스 tooyour 응용 프로그램을 제공 hello Azure AD 테 넌 트를 식별 합니다. tooget hello 테 넌 트 ID, 다음이 단계를 수행 합니다.

1. Hello Azure 포털에서에서 Active Directory를 선택 합니다.
2. **속성**을 클릭합니다.
3. Hello 디렉터리 ID에 대해 제공 된 hello GUID 값 복사 이 값은 테 넌 트 ID hello 라고도

![Hello 디렉터리 ID 복사](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a>코드 예제

이 섹션의 hello 코드 예제에는 통합 인증을 사용 하 여 Azure AD와 tooauthenticate 하는 방법 및 서비스 사용자와 보여 줍니다. 이러한 코드 예제에서는.NET을 사용 하지만 hello 개념은 다른 언어에 대 한 유사 합니다.

> [!NOTE]
> Azure AD 인증 토큰은 1시간 후 만료됩니다. 수명이 긴을 사용 하는 경우 **BatchClient** 개체 토큰을 검색 하는 것이 좋습니다 모든 요청 tooensure에 ADAL에서 항상 유효한 토큰을 저장 해야 합니다. 
>
>
> tooachieve.net에서는이 메서드를 작성 검색 hello Azure AD에서 토큰 및 해당 메서드 tooa 전달 **BatchTokenCredentials** 대리자로 개체입니다. 유효한 토큰을 제공 하는 모든 요청 toohello 일괄 처리 서비스 tooensure hello 대리자 메서드 호출 됩니다. 기본적으로 ADAL은 토큰을 캐시하므로 필요한 경우 Azure AD에서 새 토큰이 검색됩니다. Azure AD의 토큰에 대한 자세한 내용은 [Azure AD의 인증 시나리오][aad_auth_scenarios]를 참조하세요.
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a>코드 예제: Batch .NET에서 Azure AD 통합 인증 사용

일괄 처리.NET, 참조 hello에서에서 통합된 인증으로 tooauthenticate [Azure 일괄 처리.NET](https://www.nuget.org/packages/Azure.Batch/) 패키지 및 hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) 패키지 합니다.

Hello 다음이 포함 `using` 사용자 코드에서 문:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

참조 hello hello를 비롯 하 여 코드에서 Azure AD 끝점 id입니다. 테 넌 트 tooretrieve hello 테 넌 트 ID에 설명 된 hello 단계에 따라 [hello 테 넌 트 ID를 Azure Active Directory에 대 한 가져오기](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

참조 hello 일괄 처리 서비스 리소스 끝점:

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

배치 계정 참조:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

응용 프로그램에 대 한 hello 응용 프로그램 ID (클라이언트 ID)를 지정 합니다. hello 응용 프로그램 ID는 hello Azure 포털에서에서 응용 프로그램 등록에서 제공 됩니다.

```csharp
private const string ClientId = "<application-id>";
```

또한 hello 리디렉션 hello 등록 프로세스 중에 지정 된 URI를 복사 합니다. 코드에서 지정 된 URI는 hello 리디렉션 hello 리디렉션 URI hello 응용 프로그램 등록 시 입력 한 일치 해야 합니다.

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

Azure AD에서 콜백 메서드 tooacquire hello 인증 토큰을 씁니다. hello **GetAuthenticationTokenAsync** 여기에 표시 된 콜백 메서드는 ADAL tooauthenticate hello 응용 프로그램과 상호 작용 하는 사용자를 호출 합니다. hello **AcquireTokenAsync** 메서드 ADAL에서 표시 되는 메시지는 사용자 자격 증명에 대 한 hello 및 hello 응용 프로그램을 한 번 계속 hello 사용자 제공 제공 (없는 경우 자격 증명 캐시 된 이미):

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

생성 된 **BatchTokenCredentials** hello 대리자를 매개 변수로 사용 하는 개체입니다. 이러한 자격 증명 tooopen를 사용 하 여 한 **BatchClient** 개체입니다. 이 사용할 수 **BatchClient** hello 일괄 처리 서비스에 대 한 후속 작업에 대 한 개체:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a>코드 예제: Batch .NET에서 Azure AD 서비스 주체 사용

일괄 처리.NET, 참조 hello에서에서 서비스 사용자와 tooauthenticate [Azure 일괄 처리.NET](https://www.nuget.org/packages/Azure.Batch/) 패키지 및 hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) 패키지 합니다.

Hello 다음이 포함 `using` 사용자 코드에서 문:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

참조 hello hello를 비롯 하 여 코드에서 Azure AD 끝점 id입니다. 테 넌 트 서비스 주체를 사용하는 경우 테넌트별 끝점을 제공해야 합니다. tooretrieve hello 테 넌 트 ID에 설명 된 hello 단계에 따라 [hello 테 넌 트 ID를 Azure Active Directory에 대 한 가져오기](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

참조 hello 일괄 처리 서비스 리소스 끝점:  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

배치 계정 참조:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

응용 프로그램에 대 한 hello 응용 프로그램 ID (클라이언트 ID)를 지정 합니다. hello 응용 프로그램 ID는 hello Azure 포털에서에서 응용 프로그램 등록에서 제공 됩니다.

```csharp
private const string ClientId = "<application-id>";
```

Hello Azure 포털에서에서 복사한 hello 비밀 키를 지정 합니다.

```csharp
private const string ClientKey = "<secret-key>";
```

Azure AD에서 콜백 메서드 tooacquire hello 인증 토큰을 씁니다. hello **GetAuthenticationTokenAsync** 여기 무인된 인증에 대 한 ADAL 호출에 표시 된 콜백 메서드입니다.

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

생성 된 **BatchTokenCredentials** hello 대리자를 매개 변수로 사용 하는 개체입니다. 이러한 자격 증명 tooopen를 사용 하 여 한 **BatchClient** 개체입니다. 그런 다음이 사용할 수 **BatchClient** hello 일괄 처리 서비스에 대 한 후속 작업에 대 한 개체:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a>다음 단계

Azure AD에 대해 자세히 toolearn 참조 hello [Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)합니다. ADAL toouse hello에서 사용할 수 있는 방법을 보여 주는 상세한 예제 [Azure 코드 예제](https://azure.microsoft.com/resources/samples/?service=active-directory) 라이브러리입니다.

서비스 사용자에 대해 자세히 toolearn 참조 [응용 프로그램 및 Azure Active Directory에서 서비스 보안 주체 개체](../active-directory/develop/active-directory-application-objects.md)합니다. 서비스 보안 주체를 사용 하 여 toocreate hello Azure 포털에서 참조 [포털 toocreate Active Directory 응용 프로그램 및 리소스에 액세스할 수 있는 서비스 보안 주체를 사용 하 여](../resource-group-create-service-principal-portal.md)합니다. 또한 PowerShell 또는 Azure CLI를 사용하여 서비스 주체를 만들 수도 있습니다. 

Azure AD를 사용 하 여 tooauthenticate 일괄 처리 관리 응용 프로그램 참조 [Active Directory를 사용 하 여 일괄 처리 관리 인증 솔루션](batch-aad-auth-management.md)합니다. 

[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory란?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD의 인증 시나리오"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Azure Active Directory와 응용 프로그램 통합"
[azure_portal]: http://portal.azure.com
