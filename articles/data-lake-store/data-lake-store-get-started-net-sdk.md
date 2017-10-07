---
title: "aaaUse hello.NET SDK toodevelop 응용 프로그램에서 Azure 데이터 레이크 저장소 | Microsoft Docs"
description: "Azure 데이터 레이크 저장소.NET SDK toocreate 데이터 레이크 저장소 계정을 사용 하 고 hello 데이터 레이크 저장소의에서 기본 작업 수행"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="fc028-103">.NET SDK를 사용하여 Azure 데이터 레이크 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="fc028-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fc028-104">포털</span><span class="sxs-lookup"><span data-stu-id="fc028-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="fc028-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc028-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="fc028-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="fc028-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="fc028-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="fc028-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="fc028-108">REST API</span><span class="sxs-lookup"><span data-stu-id="fc028-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="fc028-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fc028-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="fc028-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fc028-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="fc028-111">Python</span><span class="sxs-lookup"><span data-stu-id="fc028-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="fc028-112">자세한 내용은 방법 toouse hello [Azure 데이터 레이크 저장소.NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform와 같은 기본 작업 폴더를 만들어 업로드 한 데이터 파일 등을 다운로드 합니다. Data Lake에 대한 자세한 내용은 [Azure Data Lake Store](data-lake-store-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc028-112">Learn how toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc028-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fc028-113">Prerequisites</span></span>
* <span data-ttu-id="fc028-114">**Visual Studio 2013, 2015 또는 2017**.</span><span class="sxs-lookup"><span data-stu-id="fc028-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="fc028-115">Visual Studio 2015 업데이트 2를 사용 하는 hello 지침은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-115">hello instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="fc028-116">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="fc028-116">**An Azure subscription**.</span></span> <span data-ttu-id="fc028-117">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc028-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="fc028-118">**Azure Data Lake Store 계정**.</span><span class="sxs-lookup"><span data-stu-id="fc028-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="fc028-119">방법에 대 한 계정에는 toocreate 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="fc028-119">For instructions on how toocreate an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="fc028-120">**Azure Active Directory 응용 프로그램을 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="fc028-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="fc028-121">Azure AD와 hello Azure AD 응용 프로그램 tooauthenticate hello Data Lake 저장소 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-121">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="fc028-122">없는 Azure AD와 다양 한 접근 방법 tooauthenticate 않는 **최종 사용자 인증** 또는 **서비스 간 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-122">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="fc028-123">지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="fc028-124">.NET 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="fc028-124">Create a .NET application</span></span>
1. <span data-ttu-id="fc028-125">Visual Studio를 열고 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="fc028-126">Hello에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-126">From hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="fc028-127">**새 프로젝트**입력 하거나 다음 값에는 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-127">From **New Project**, type or select hello following values:</span></span>

   | <span data-ttu-id="fc028-128">속성</span><span class="sxs-lookup"><span data-stu-id="fc028-128">Property</span></span> | <span data-ttu-id="fc028-129">값</span><span class="sxs-lookup"><span data-stu-id="fc028-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="fc028-130">Category</span><span class="sxs-lookup"><span data-stu-id="fc028-130">Category</span></span> |<span data-ttu-id="fc028-131">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="fc028-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="fc028-132">Template</span><span class="sxs-lookup"><span data-stu-id="fc028-132">Template</span></span> |<span data-ttu-id="fc028-133">콘솔 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fc028-133">Console Application</span></span> |
   | <span data-ttu-id="fc028-134">이름</span><span class="sxs-lookup"><span data-stu-id="fc028-134">Name</span></span> |<span data-ttu-id="fc028-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="fc028-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="fc028-136">클릭 **확인** toocreate hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="fc028-136">Click **OK** toocreate hello project.</span></span>
5. <span data-ttu-id="fc028-137">Hello Nuget 패키지 tooyour 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-137">Add hello Nuget packages tooyour project.</span></span>

   1. <span data-ttu-id="fc028-138">Hello 솔루션 탐색기에서에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-138">Right-click hello project name in hello Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="fc028-139">Hello에 **Nuget 패키지 관리자** 탭에서 다음 사항을 확인 **패키지 소스** 너무 설정**nuget.org** 있는지 **시험판 포함** 확인란 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-139">In hello **Nuget Package Manager** tab, make sure that **Package source** is set too**nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="fc028-140">검색 하 고 hello 다음 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-140">Search for and install hello following NuGet packages:</span></span>

      * <span data-ttu-id="fc028-141">`Microsoft.Azure.Management.DataLake.Store` - 이 자습서에서는 v2.1.3-미리 보기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="fc028-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - 이 자습서는 v2.2.12를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="fc028-143">![Nuget 원본 추가](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "새 Azure Data Lake 계정 만들기")</span><span class="sxs-lookup"><span data-stu-id="fc028-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="fc028-144">닫기 hello **Nuget 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-144">Close hello **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="fc028-145">열기 **Program.cs**, hello 기존 코드를 삭제 하 고 hello 문을 tooadd 참조 toonamespaces 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-145">Open **Program.cs**, delete hello existing code, and then include hello following statements tooadd references toonamespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="fc028-146">아래와 같이 hello 변수를 선언 하 고 데이터 레이크 저장소 이름 및 이미 존재 하는 hello 리소스 그룹 이름에 대 한 hello 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-146">Declare hello variables as shown below, and provide hello values for Data Lake Store name and hello resource group name that already exist.</span></span> <span data-ttu-id="fc028-147">여기에서 제공한 로컬 경로 파일 이름을 hello hello 컴퓨터에 있어야 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-147">Also, make sure hello local path and file name you provide here must exist on hello computer.</span></span> <span data-ttu-id="fc028-148">Hello 코드 조각 hello 네임 스페이스 선언 후 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-148">Add hello following code snippet after hello namespace declarations.</span></span>

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="fc028-149">Hello 문서의 섹션 남은 hello, 어떻게 toouse hello 인증, 파일 업로드 등의 사용 가능한.NET 메서드 tooperform 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-149">In hello remaining sections of hello article, you can see how toouse hello available .NET methods tooperform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="fc028-150">인증</span><span class="sxs-lookup"><span data-stu-id="fc028-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="fc028-151">최종 사용자 인증을 사용하는 경우(이 자습서에 권장됨)</span><span class="sxs-lookup"><span data-stu-id="fc028-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="fc028-152">이 사용 하 여 기존 Azure AD 네이티브 응용 프로그램 tooauthenticate 응용 프로그램 **대화형으로**, 어떤 의미 됩니다 메시지가 tooenter Azure 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-152">Use this with an existing Azure AD native application tooauthenticate your application **interactively**, which means you will be prompted tooenter your Azure credentials.</span></span>

<span data-ttu-id="fc028-153">경우 사용 편의성에 대 한 아래 hello 조각 클라이언트 ID와 리디렉션 Azure 구독과 작동 하는 URI에 대 한 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-153">For ease of use, hello snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="fc028-154">이 자습서를 더 빨리 완료할 toohelp,이 방법을 사용 하면 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-154">toohelp you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="fc028-155">아래 hello 조각 제공 hello 값 테 넌 트 id</span><span class="sxs-lookup"><span data-stu-id="fc028-155">In hello snippet below, just provide hello value for your tenant ID.</span></span> <span data-ttu-id="fc028-156">제공 하는 hello 지침을 사용 하 여 검색할 수 있습니다 [Active Directory 응용 프로그램을 만들](data-lake-store-end-user-authenticate-using-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-156">You can retrieve it using hello instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="fc028-157">위의이 조각에 대 한 작업 tooknow 몇:</span><span class="sxs-lookup"><span data-stu-id="fc028-157">A couple of things tooknow about this snippet above:</span></span>

* <span data-ttu-id="fc028-158">hello 자습서를 더 빨리 완료 toohelp,이 코드 조각을 사용 하 여 Azure AD는 기본적으로 모든 Azure 구독에 대해 사용할 수 있는 도메인 및 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-158">toohelp you complete hello tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="fc028-159">따라서 **이 코드 조각을 응용 프로그램에서 있는 그대로 사용**할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="fc028-160">그러나 toouse 자신의 Azure AD 도메인을 선택 하 여 응용 프로그램 클라이언트 ID는 Azure AD 네이티브 응용 프로그램을 만들어야 하 고 사용 하 여 hello Azure AD 테 넌 트 ID, 클라이언트 ID 및 리디렉션 URI hello 응용 프로그램에 대 한 다음 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-160">However, if you do want toouse your own Azure AD domain and application client ID, you must create an Azure AD native application and then use hello Azure AD tenant ID, client ID, and redirect URI for hello application you created.</span></span> <span data-ttu-id="fc028-161">지침은 [Data Lake Store를 사용하여 최종 사용자 인증을 위한 Active Directory 응용 프로그램 만들기](data-lake-store-end-user-authenticate-using-active-directory.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc028-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="fc028-162">클라이언트 암호로 서비스 간 인증을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="fc028-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="fc028-163">다음 코드 조각 hello tooauthenticate 사용 되는 응용 프로그램 수 **비 대화형**/ hello 클라이언트 암호를 사용 하 여 응용 프로그램 / 서비스 주체에 대 한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-163">hello following snippet can be used tooauthenticate your application **non-interactively**, using hello client secret / key for an application / service principal.</span></span> <span data-ttu-id="fc028-164">기존 Azure AD "Web App" 응용 프로그램과 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="fc028-165">Toocreate hello Azure AD 웹 응용 프로그램 및 클라이언트 ID와 클라이언트 암호가 hello 조각 아래에 필요한 tooretrieve hello 하는 방법을 참조 하는 방법에 대 한 지침은 [데이터로 서비스 간 인증에 대 한 Active Directory 응용 프로그램 만들기 레이크 저장소](data-lake-store-authenticate-using-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-165">For instructions on how toocreate hello Azure AD web application and how tooretrieve hello client ID and client secret required in hello snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="fc028-166">인증서로 서비스 간 인증을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="fc028-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="fc028-167">세 번째 옵션을 hello 처럼 다음 코드 조각 수 tooauthenticate 사용 되는 응용 프로그램 **비 대화형**hello 인증서를 사용 하 여 Azure Active Directory 응용 프로그램 / 서비스 보안 주체, 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-167">As a third option, hello following snippet can be used tooauthenticate your application **non-interactively**, using hello certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="fc028-168">이것은 [인증서에서 기존 Azure AD 응용 프로그램](../azure-resource-manager/resource-group-authenticate-service-principal.md)과 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="fc028-169">클라이언트 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="fc028-169">Create client objects</span></span>
<span data-ttu-id="fc028-170">hello 다음 조각에서는 hello 데이터 레이크 저장소 계정 및 파일 시스템 사용 되는 클라이언트 개체 tooissue toohello 서비스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-170">hello following snippet creates hello Data Lake Store account and filesystem client objects, which are used tooissue requests toohello service.</span></span>

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="fc028-171">구독 내 모든 Data Lake Store 계정 나열</span><span class="sxs-lookup"><span data-stu-id="fc028-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="fc028-172">hello 다음 코드 조각에서는 특정된 Azure 구독 내에서 모든 데이터 레이크 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="fc028-172">hello following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within hello subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a><span data-ttu-id="fc028-173">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="fc028-173">Create a directory</span></span>
<span data-ttu-id="fc028-174">다음 조각과 hello는 `CreateDirectory` 메서드 toocreate 데이터 레이크 저장소 계정 내에서 디렉터리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-174">hello following snippet shows a `CreateDirectory` method that you can use toocreate a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="fc028-175">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="fc028-175">Upload a file</span></span>
<span data-ttu-id="fc028-176">다음 조각과 hello는 `UploadFile` tooupload를 사용할 수 있는 메서드 tooa 데이터 레이크 저장소 계정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-176">hello following snippet shows an `UploadFile` method that you can use tooupload files tooa Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="fc028-177">hello SDK 재귀 업로드 및 다운로드는 로컬 파일 경로와 데이터 레이크 저장소 파일 경로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-177">hello SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="fc028-178">파일 또는 디렉터리 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="fc028-178">Get file or directory info</span></span>
<span data-ttu-id="fc028-179">다음 조각과 hello는 `GetItemInfo` 메서드 데이터 레이크 저장소의 파일 또는 디렉터리를 사용할 수 있는 방법에 대 한 tooretrieve 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-179">hello following snippet shows a `GetItemInfo` method that you can use tooretrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="fc028-180">파일 또는 디렉터리 나열</span><span class="sxs-lookup"><span data-stu-id="fc028-180">List file or directories</span></span>
<span data-ttu-id="fc028-181">다음 조각과 hello는 `ListItem` toolist hello 파일 및 디렉터리 데이터 레이크 저장소 계정에서 사용할 수 있는 메서드.</span><span class="sxs-lookup"><span data-stu-id="fc028-181">hello following snippet shows a `ListItem` method that can use toolist hello file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="fc028-182">파일 연결</span><span class="sxs-lookup"><span data-stu-id="fc028-182">Concatenate files</span></span>
<span data-ttu-id="fc028-183">다음 조각과 hello는 `ConcatenateFiles` 메서드 tooconcatenate 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-183">hello following snippet shows a `ConcatenateFiles` method that you use tooconcatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a><span data-ttu-id="fc028-184">Tooa 파일 추가</span><span class="sxs-lookup"><span data-stu-id="fc028-184">Append tooa file</span></span>
<span data-ttu-id="fc028-185">다음 조각과 hello는 `AppendToFile` 를 사용 하면 데이터 레이크 저장소 계정에 이미 저장 된 데이터 tooa 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc028-185">hello following snippet shows a `AppendToFile` method that you use append data tooa file already stored in a Data Lake Store account.</span></span>

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="fc028-186">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="fc028-186">Download a file</span></span>
<span data-ttu-id="fc028-187">다음 조각과 hello는 `DownloadFile` toodownload 데이터 레이크 저장소 계정에서 파일을 사용 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="fc028-187">hello following snippet shows a `DownloadFile` method that you use toodownload a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="fc028-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fc028-188">Next steps</span></span>
* [<span data-ttu-id="fc028-189">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="fc028-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="fc028-190">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="fc028-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="fc028-191">데이터 레이크 저장소와 함께 Azure HDInsight 사용</span><span class="sxs-lookup"><span data-stu-id="fc028-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="fc028-192">Data Lake Store .NET SDK 참조</span><span class="sxs-lookup"><span data-stu-id="fc028-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="fc028-193">Data Lake Store REST 참조</span><span class="sxs-lookup"><span data-stu-id="fc028-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
