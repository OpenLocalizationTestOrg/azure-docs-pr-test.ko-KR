---
title: "Azure.NET SDK를 사용 하 여 자신만 데이터 파이프라인 aaaCreate | Microsoft Docs"
description: "Tooprogrammatically를 만들기, 모니터링 및 데이터 팩터리 SDK를 사용 하 여 Azure 데이터 팩터리를 관리 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="0948b-103">Azure Data Factory .NET SDK를 사용하여 Azure Data Factory 만들기, 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="0948b-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="0948b-104">개요</span><span class="sxs-lookup"><span data-stu-id="0948b-104">Overview</span></span>
<span data-ttu-id="0948b-105">데이터 팩터리 .NET SDK를 사용하여 프로그래밍 방식으로 Azure Data Factory를 만들고, 모니터링하며, 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="0948b-106">이 문서를 만들고 데이터 팩터리를 모니터링 하는 샘플.NET 콘솔 응용 프로그램 toocreate 참고할 수 있는 연습이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-106">This article contains a walkthrough that you can follow toocreate a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="0948b-107">이 문서에서 모든 hello 데이터 팩터리.NET API를 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-107">This article does not cover all hello Data Factory .NET API.</span></span> <span data-ttu-id="0948b-108">데이터 팩터리용 .NET API에 대한 포괄적인 설명서는 [데이터 팩터리 .NET API 참조](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0948b-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0948b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0948b-109">Prerequisites</span></span>
* <span data-ttu-id="0948b-110">Visual Studio 2012, 2013 또는 2015</span><span class="sxs-lookup"><span data-stu-id="0948b-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="0948b-111">[Azure .NET SDK](http://azure.microsoft.com/downloads/)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="0948b-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0948b-112">Azure PowerShell.</span></span> <span data-ttu-id="0948b-113">지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 컴퓨터에 Azure PowerShell tooinstall 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-113">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="0948b-114">Azure PowerShell toocreate Azure Active Directory 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-114">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="0948b-115">Azure Active Directory에서 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="0948b-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="0948b-116">Azure Active Directory 응용 프로그램을 만들고 hello 응용 프로그램에 대 한 서비스 사용자를 만들, toohello 할당 **데이터 팩터리 참가자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-116">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="0948b-117">**PowerShell**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="0948b-118">Hello 다음 명령을 실행 하 고 hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-118">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="0948b-119">이 계정에 대 한 모든 hello 구독 hello 명령 tooview 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-119">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="0948b-120">다음 명령 tooselect hello 피드에 있는 toowork hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-120">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="0948b-121">대체  **&lt;NameOfAzureSubscription** &gt; hello 이름의 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="0948b-121">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="0948b-122">기록해 두고 **SubscriptionId** 및 **TenantId** hello이이 명령의 출력에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-122">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="0948b-123">라는 Azure 리소스 그룹 만들기 **ADFTutorialResourceGroup** hello 다음 hello PowerShell에서에서 명령을 실행 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="0948b-124">Hello 리소스 그룹이 이미 있는 경우, 지정 여부 tooupdate 것 (Y) 하거나 (N)로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-124">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="0948b-125">다른 리소스 그룹을 사용 하는 경우이 자습서의 ADFTutorialResourceGroup 대신 리소스 그룹의 toouse hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-125">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="0948b-126">Azure Active Directory 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="0948b-127">Hello 다음 오류가 발생 하는 경우 다른 URL을 지정 하 고 hello 명령을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-127">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="0948b-128">Hello AD 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-128">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="0948b-129">서비스 보안 주체 toohello 추가 **데이터 팩터리 참가자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-129">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="0948b-130">Hello 응용 프로그램 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-130">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="0948b-131">Hello hello 출력에서 응용 프로그램 ID (applicationID) 아래로 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-131">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="0948b-132">이 단계에서 다음과 같은 4가지 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="0948b-133">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="0948b-133">Tenant ID</span></span>
* <span data-ttu-id="0948b-134">구독 ID</span><span class="sxs-lookup"><span data-stu-id="0948b-134">Subscription ID</span></span>
* <span data-ttu-id="0948b-135">응용 프로그램 UI</span><span class="sxs-lookup"><span data-stu-id="0948b-135">Application ID</span></span>
* <span data-ttu-id="0948b-136">암호 (hello 첫 번째 명령에 지정 됨)</span><span class="sxs-lookup"><span data-stu-id="0948b-136">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="0948b-137">연습</span><span class="sxs-lookup"><span data-stu-id="0948b-137">Walkthrough</span></span>
<span data-ttu-id="0948b-138">Hello 연습 복사 작업을 포함 하는 파이프라인을 사용 하 여 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-138">In hello walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="0948b-139">hello 복사 활동 데이터를 복사 hello에 Azure blob 저장소 tooanother 폴더에 폴더에서 동일한 blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-139">hello copy activity copies data from a folder in your Azure blob storage tooanother folder in hello same blob storage.</span></span> 

<span data-ttu-id="0948b-140">Azure Data Factory에 hello 데이터 이동을 수행 하는 hello 복사 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-140">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="0948b-141">hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-141">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="0948b-142">참조 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업에 대 한 세부 정보에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

1. <span data-ttu-id="0948b-143">Visual Studio 2012/2013/2015를 사용하여 C# .NET 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="0948b-144">**Visual Studio** 2012/2013/2015를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="0948b-145">클릭 **파일**, 너무 가리킨**새로**를 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-145">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="0948b-146">**템플릿**을 확장하고 **Visual C#**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="0948b-147">이 연습에서는 C#을 사용하지만 모든 .NET 언어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="0948b-148">선택 **콘솔 응용 프로그램** hello hello 오른쪽에 프로젝트 형식 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-148">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="0948b-149">입력 **DataFactoryAPITestApp** hello 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-149">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="0948b-150">선택 **C:\ADFGetStarted** hello 위치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-150">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="0948b-151">클릭 **확인** toocreate hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="0948b-151">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="0948b-152">클릭 **도구**, 너무 가리킨**NuGet 패키지 관리자**를 클릭 하 고 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-152">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="0948b-153">Hello에 **패키지 관리자 콘솔**, 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-153">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="0948b-154">다음 명령 tooinstall Data Factory 패키지 hello를 실행 합니다.`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="0948b-154">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="0948b-155">Hello 명령 tooinstall Azure Active Directory 패키지 (Active Directory API 코드에서 사용 hello) 다음을 실행 합니다.`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="0948b-155">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="0948b-156">Hello 내용 바꾸기 **App.config** 콘텐츠를 다음 hello로 hello 프로젝트 파일에에서:</span><span class="sxs-lookup"><span data-stu-id="0948b-156">Replace hello contents of **App.config** file in hello project with hello following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="0948b-157">Hello App.Config 파일에 대 한 값을 업데이트  **&lt;응용 프로그램 ID&gt;**,  **&lt;암호&gt;**,  **&lt; 구독 ID&gt;**, 및  **&lt;테 넌 트 ID&gt;**  고유한 값으로.</span><span class="sxs-lookup"><span data-stu-id="0948b-157">In hello App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="0948b-158">Hello 다음 추가 **를 사용 하 여** 문 toohello **Program.cs** hello 프로젝트 파일에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-158">Add hello following **using** statements toohello **Program.cs** file in hello project.</span></span>

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. <span data-ttu-id="0948b-159">인스턴스를 만드는 코드 다음 hello 추가 **DataPipelineManagementClient** 클래스 toohello **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="0948b-159">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="0948b-160">이 개체 toocreate을 사용 하 여 데이터 팩터리, 연결된 된 서비스, 입력 및 출력 데이터 집합 및 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="0948b-160">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="0948b-161">또한 런타임에 데이터 집합의 개체 toomonitor 조각을이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-161">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="0948b-162">Hello 값의 대체 **resourceGroupName** hello Azure 리소스 그룹 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-162">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span> <span data-ttu-id="0948b-163">Hello를 사용 하 여 리소스 그룹을 만들 수 [새로 AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0948b-163">You can create a resource group using hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="0948b-164">Hello 데이터 팩터리 () toobe 고유의 이름을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-164">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="0948b-165">Hello 데이터 팩터리의 이름을 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-165">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="0948b-166">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0948b-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="0948b-167">추가 코드를 만드는 다음 hello는 **데이터 팩터리의** toohello **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="0948b-167">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. <span data-ttu-id="0948b-168">추가 코드를 만드는 다음 hello는 **Azure 저장소 연결 된 서비스** toohello **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="0948b-168">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0948b-169">**storageaccountname** 및 **accountkey**를 Azure Storage 계정의 이름 및 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. <span data-ttu-id="0948b-170">추가 코드를 만드는 다음 hello **입력 및 출력 데이터 집합** toohello **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="0948b-170">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    <span data-ttu-id="0948b-171">hello **FolderPath** hello 입력된 blob 너무 설정 되어**adftutorial /** 여기서 **adftutorial** hello hello 컨테이너 blob 저장소의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-171">hello **FolderPath** for hello input blob is set too**adftutorial/** where **adftutorial** is hello name of hello container in your blob storage.</span></span> <span data-ttu-id="0948b-172">이 컨테이너 Azure blob 저장소에 없는 경우이 이름을 가진 컨테이너 만들기: **adftutorial** 및 텍스트 파일 toohello 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file toohello container.</span></span>

    <span data-ttu-id="0948b-173">hello FolderPath hello에 대 한 출력 blob로 설정 되어: **adftutorial/apifactoryoutput {Slice} /** 여기서 **조각** 값인지에 따라 동적으로 계산 된 hello **SliceStart**(날짜-시간 각 조각의 시작 합니다.)</span><span class="sxs-lookup"><span data-stu-id="0948b-173">hello FolderPath for hello output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on hello value of **SliceStart** (start date-time of each slice.)</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. <span data-ttu-id="0948b-174">Hello 다음 코드를 추가 **가 만들어지고 활성화 파이프라인** toohello **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="0948b-174">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="0948b-175">이 파이프라인에는 **BlobSource**를 원본으로 사용하고 **BlobSink**를 싱크로 사용하는 **CopyActivity**가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="0948b-176">Azure Data Factory에 hello 데이터 이동을 수행 하는 hello 복사 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-176">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="0948b-177">hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-177">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="0948b-178">참조 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업에 대 한 세부 정보에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. <span data-ttu-id="0948b-179">다음 코드 toohello hello 추가 **Main** hello의 데이터 조각 방법 tooget hello 상태 출력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-179">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="0948b-180">이 샘플에서는 한 개의 조각만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. <span data-ttu-id="0948b-181">**(선택 사항)**  추가 hello 다음 데이터 조각 toohello에 대 한 실행 tooget 세부 정보를 코드 **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="0948b-181">**(optional)** Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="0948b-182">Hello hello에서 사용 하는 도우미 메서드를 다음 추가 **Main** 메서드 toohello **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-182">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span> <span data-ttu-id="0948b-183">이 메서드를 사용 하면 제공할 수 있는 대화 상자를 팝 **사용자 이름** 및 **암호** tooAzure 포털에서 toolog를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use toolog in tooAzure portal.</span></span>

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. <span data-ttu-id="0948b-184">Hello 솔루션 탐색기에서에서 프로젝트 hello 확장: **DataFactoryAPITestApp**를 마우스 오른쪽 단추로 클릭 **참조**를 클릭 하 고 **참조 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-184">In hello Solution Explorer, expand hello project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="0948b-185">`System.Configuration` 어셈블리에 대한 확인란을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="0948b-186">Hello 콘솔 응용 프로그램을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="0948b-186">Build hello console application.</span></span> <span data-ttu-id="0948b-187">클릭 **빌드** hello 메뉴에 **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-187">Click **Build** on hello menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="0948b-188">Azure blob 저장소에 hello adftutorial 컨테이너에 파일을 하나 이상 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-188">Confirm that there is at least one file in hello adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="0948b-189">그렇지 않으면 Emp.txt 파일을 메모장에서에서 다음 hello로 콘텐츠 만들고 toohello adftutorial 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-189">If not, create Emp.txt file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="0948b-190">클릭 하 여 hello 샘플을 실행 **디버그** -> **디버깅 시작** hello 메뉴.</span><span class="sxs-lookup"><span data-stu-id="0948b-190">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="0948b-191">Hello 표시 되 면 **데이터 조각에 대 한 세부 정보 실행**, 몇 분 및 키를 눌러 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-191">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="0948b-192">사용 하 여 hello Azure 포털 tooverify hello 데이터 팩터리에서 **APITutorialFactory** hello 다음 아티팩트를 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-192">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
    * <span data-ttu-id="0948b-193">연결된 서비스: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="0948b-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="0948b-194">데이터 집합: **DatasetBlobSource** 및 **DatasetBlobDestination**</span><span class="sxs-lookup"><span data-stu-id="0948b-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="0948b-195">파이프라인: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="0948b-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="0948b-196">Hello에 출력 파일이 만들어졌는지 확인 **apifactoryoutput** 폴더 hello에 **adftutorial** 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="0948b-196">Verify that an output file is created in hello **apifactoryoutput** folder in hello **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="0948b-197">실패한 데이터 조각 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="0948b-197">Get a list of failed data slices</span></span> 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a><span data-ttu-id="0948b-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0948b-198">Next steps</span></span>
<span data-ttu-id="0948b-199">다음 예제에서는 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는.NET SDK를 사용 하 여 파이프라인 만들기에 대 한 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0948b-199">See hello following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage tooan Azure SQL database:</span></span> 

- [<span data-ttu-id="0948b-200">Blob 저장소 tooSQL 데이터베이스에서에서 파이프라인 toocopy 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="0948b-200">Create a pipeline toocopy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
