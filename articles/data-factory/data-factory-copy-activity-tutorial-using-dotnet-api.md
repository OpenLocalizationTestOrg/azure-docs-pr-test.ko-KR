---
title: "자습서: .NET API를 사용하여 복사 작업이 있는 파이프라인 만들기 | Microsoft Docs"
description: "이 자습서에서는 .NET API를 사용하여 복사 작업이 있는 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 30c7cd1ba455d7b1bc93d76e7ee79455bb52aae9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="73214-103">자습서: .NET API를 사용하여 복사 작업이 있는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="73214-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="73214-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="73214-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="73214-105">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="73214-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="73214-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="73214-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="73214-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73214-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="73214-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="73214-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="73214-109">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="73214-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="73214-110">REST API</span><span class="sxs-lookup"><span data-stu-id="73214-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="73214-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="73214-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="73214-112">이 문서에서는 [.NET API](https://portal.azure.com)를 사용하여 Azure Blob Storage에서 Azure SQL Database로 데이터를 복사하는 파이프라인이 있는 데이터 팩터리를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="73214-112">In this article, you learn how to use [.NET API](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="73214-113">Azure Data Factory를 처음 사용하는 경우 이 자습서를 수행하기 전에 [Azure Data Factory 소개](data-factory-introduction.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="73214-114">이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73214-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="73214-115">복사 작업은 지원되는 데이터 저장소에서 지원되는 싱크 데이터 저장소로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="73214-116">원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="73214-117">이 작업은 다양한 데이터 저장소 간에 데이터를 안전하고 안정적이며 확장성 있는 방법으로 복사할 수 있는 전역적으로 사용 가능한 서비스를 통해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="73214-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="73214-118">복사 작업에 대한 자세한 내용은 [데이터 이동 작업](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="73214-119">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="73214-120">한 활동의 출력 데이터 집합을 다른 활동의 입력 데이터 집합으로 설정함으로써 두 활동을 연결하여 활동을 하나씩 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="73214-121">자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="73214-122">Data Factory용 .NET API에 대한 포괄적인 설명서는 [데이터 팩터리 .NET API 참조](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="73214-123">이 자습서에서 데이터 파이프라인은 원본 데이터 저장소의 데이터를 대상 데이터 저장소로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-123">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="73214-124">Azure Data Factory를 사용하여 데이터를 변환하는 방법에 대한 자습서는 [자습서: Hadoop 클러스터를 사용하여 데이터를 변환하도록 파이프라인 빌드](data-factory-build-your-first-pipeline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-124">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73214-125">필수 조건</span><span class="sxs-lookup"><span data-stu-id="73214-125">Prerequisites</span></span>
* <span data-ttu-id="73214-126">[자습서 개요 및 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 를 살펴보고 자습서 개요를 가져와서 **필수 구성 요소** 를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to get an overview of the tutorial and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="73214-127">Visual Studio 2012, 2013 또는 2015</span><span class="sxs-lookup"><span data-stu-id="73214-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="73214-128">[Azure .NET SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="73214-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="73214-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="73214-129">Azure PowerShell.</span></span> <span data-ttu-id="73214-130">[Azure PowerShell을 설치 및 구성하는 방법](../powershell-install-configure.md) 문서의 지침을 수행하여 컴퓨터에 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-130">Follow instructions in [How to install and configure Azure PowerShell](../powershell-install-configure.md) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="73214-131">Azure PowerShell을 사용하여 Azure Active Directory 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73214-131">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="73214-132">Azure Active Directory에서 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="73214-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="73214-133">Azure Active Directory 응용 프로그램을 만든 다음 응용 프로그램의 서비스 주체를 만들고 **데이터 팩터리 참가자** 역할에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-133">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="73214-134">**PowerShell**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="73214-135">다음 명령을 실행하고 Azure 포털에 로그인하는 데 사용할 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-135">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="73214-136">다음 명령을 실행하여 이 계정의 모든 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-136">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="73214-137">다음 명령을 실행하여 사용하려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-137">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="73214-138">**&lt;NameOfAzureSubscription**&gt;을 Azure 구독의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="73214-138">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="73214-139">이 명령의 출력에서 **SubscriptionId** 및 **TenantId**를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="73214-139">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="73214-140">PowerShell에서 다음 명령을 실행하여 **ADFTutorialResourceGroup** 이라는 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73214-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="73214-141">리소스 그룹이 이미 있다면 업데이트(Y)할지 또는 유지(N)할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-141">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="73214-142">다른 리소스 그룹을 사용하는 경우 이 자습서에서 ADFTutorialResourceGroup 대신 해당 리소스 그룹의 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-142">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="73214-143">Azure Active Directory 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73214-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="73214-144">다음과 같은 오류가 발생하면 다른 URL을 지정하고 명령을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-144">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="73214-145">AD 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73214-145">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="73214-146">**데이터 팩터리 참가자** 역할에 서비스 주체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-146">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="73214-147">응용 프로그램 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="73214-147">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="73214-148">출력에서 응용 프로그램 ID(applicationID)를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="73214-148">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="73214-149">이 단계에서 다음과 같은 4가지 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="73214-150">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="73214-150">Tenant ID</span></span>
* <span data-ttu-id="73214-151">구독 ID</span><span class="sxs-lookup"><span data-stu-id="73214-151">Subscription ID</span></span>
* <span data-ttu-id="73214-152">응용 프로그램 UI</span><span class="sxs-lookup"><span data-stu-id="73214-152">Application ID</span></span>
* <span data-ttu-id="73214-153">(첫 번째 명령에 지정된)암호</span><span class="sxs-lookup"><span data-stu-id="73214-153">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="73214-154">연습</span><span class="sxs-lookup"><span data-stu-id="73214-154">Walkthrough</span></span>
1. <span data-ttu-id="73214-155">Visual Studio 2012/2013/2015를 사용하여 C# .NET 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73214-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="73214-156">**Visual Studio** 2012/2013/2015를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="73214-157">**파일**을 클릭하고 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-157">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="73214-158">**템플릿**을 확장하고 **Visual C#**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="73214-159">이 연습에서는 C#을 사용하지만 모든 .NET 언어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="73214-160">오른쪽의 프로젝트 형식 목록에서 **콘솔 응용 프로그램** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-160">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="73214-161">이름에 **DataFactoryAPITestApp** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-161">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="73214-162">**C:\ADFGetStarted**를 [위치]로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-162">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="73214-163">**확인** 을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73214-163">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="73214-164">**도구**를 클릭하고 **NuGet 패키지 관리자**를 가리킨 다음 **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-164">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="73214-165">**패키지 관리자 콘솔**에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-165">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="73214-166">다음 명령을 실행하여 Data Factory 패키지를 설치합니다. `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="73214-166">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="73214-167">Azure Active Directory 패키지를 설치하려면 다음 명령을 실행합니다(코드에서 Active Directory API를 사용함). `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="73214-167">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="73214-168">다음 **appSetttings** 섹션을 **App.config** 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-168">Add the following **appSetttings** section to the **App.config** file.</span></span> <span data-ttu-id="73214-169">이 설정은 도우미 메서드 **GetAuthorizationHeader**에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="73214-169">These settings are used by the helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="73214-170">**&lt;응용 프로그램 ID&gt;**, **&lt;암호&gt;**, **&lt;구독 ID&gt;** 및 **&lt;테넌트 ID&gt;**의 값을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="73214-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating the AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```

5. <span data-ttu-id="73214-171">다음 **using** 문을 프로젝트의 원본 파일(Program.cs)에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-171">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

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

6. <span data-ttu-id="73214-172">**DataPipelineManagementClient** 클래스의 인스턴스를 만드는 다음 코드를 **Main** 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-172">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="73214-173">이 개체를 사용하여 데이터 팩터리, 연결된 서비스, 입력 및 출력 데이터 집합과 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73214-173">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="73214-174">또한 이 개체를 사용하여 런타임 시 데이터 집합의 조각을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-174">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="73214-175">**resourceGroupName** 값을 Azure 리소스 그룹의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="73214-175">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="73214-176">데이터 팩터리 이름(dataFactoryName)을 고유한 이름으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-176">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="73214-177">데이터 팩터리 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-177">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="73214-178">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="73214-179">**데이터 팩터리**를 만드는 다음 코드를 **Main** 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-179">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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

    <span data-ttu-id="73214-180">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="73214-181">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="73214-182">예를 들어 원본에서 대상 데이터 저장소에 데이터를 복사하는 복사 작업 및 입력 데이터를 제품 출력 데이터로 변환하는 Hive 스크립트를 실행하는 HDInsight Hive 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="73214-182">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="73214-183">이 단계에서는 데이터 팩터리 만들기를 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-183">Let's start with creating the data factory in this step.</span></span>
8. <span data-ttu-id="73214-184">**Azure Storage 연결된 서비스**를 만드는 다음 코드를 **Main** 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-184">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="73214-185">**storageaccountname** 및 **accountkey**를 Azure Storage 계정의 이름 및 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="73214-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="73214-186">데이터 팩터리에서 연결된 서비스를 만들어 데이터 저장소를 연결하고 계산 서비스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-186">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="73214-187">이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="73214-188">Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="73214-189">이에 따라 두 개의 연결된 서비스, 즉 AzureStorage와 AzureSqlDatabase 유형의 AzureStorageLinkedService와 AzureSqlLinkedService를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73214-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="73214-190">AzureStorageLinkedService는 Azure 저장소 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-190">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="73214-191">이 저장소 계정은 컨테이너를 만들고 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 데이터를 업로드한 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="73214-191">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="73214-192">**Azure SQL 연결된 서비스**를 만드는 다음 코드를 **Main** 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-192">Add the following code that creates an **Azure SQL linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="73214-193">**servername**, **databasename**, **username** 및 **password**를 Azure SQL Server의 이름, 데이터베이스, 사용자 계정 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="73214-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    <span data-ttu-id="73214-194">AzureSqlLinkedService는 Azure SQL 데이터베이스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-194">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="73214-195">Blob 저장소에서 복사된 데이터는 이 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="73214-195">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="73214-196">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 emp 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-196">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="73214-197">**입력 및 출력 데이터 집합**을 만드는 다음 코드를 **Main** 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-197">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
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

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
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
    
    <span data-ttu-id="73214-198">이전 단계에서는 Azure Storage 계정과 Azure SQL Database를 데이터 팩터리에 연결하는 연결된 서비스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-198">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="73214-199">이 단계에서는 AzureStorageLinkedService 및 AzureSqlLinkedService에서 각각 참조하는 데이터 저장소에 저장된 입력 및 출력 데이터를 나타내는 InputDataset 및 OutputDataset이라는 두 개의 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="73214-200">Azure 저장소 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure 저장소 계정에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-200">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="73214-201">그리고 입력 Blob 데이터 집합(InputDataset)은 입력 데이터가 포함된 컨테이너와 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-201">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="73214-202">마찬가지로 Azure SQL Database 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure SQL 데이터베이스에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-202">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="73214-203">그리고 출력 SQL 테이블 데이터 집합(OututDataset)은 Blob 저장소의 데이터가 복사되는 데이터베이스의 테이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-203">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span>

    <span data-ttu-id="73214-204">이 단계에서는 AzureStorageLinkedService 연결된 서비스에서 나타내는 Azure Storage의 Blob 컨테이너(adftutorial)의 루트 폴더에 있는 Blob 파일(emp.txt)을 가리키는 InputDataset이라는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73214-204">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="73214-205">fileName 값을 지정하지 않거나 건너뛰면 입력 폴더에 있는 모든 Blob의 데이터가 대상에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="73214-205">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="73214-206">이 자습서에서는 fileName 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-206">In this tutorial, you specify a value for the fileName.</span></span>    

    <span data-ttu-id="73214-207">이 단계에서는 **OutputDataset**이라는 출력 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73214-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="73214-208">이 데이터 집합은 **AzureSqlLinkedService**가 나타내는 Azure SQL Database에서 SQL 테이블을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="73214-208">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="73214-209">**파이프라인을 만들고 활성화**하는 다음 코드를 **Main** 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-209">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="73214-210">이 단계에서는 **InputDataset**을 입력으로 사용하고 **OutputDataset**을 출력으로 사용하는 **복사 활동**을 포함한 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73214-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new PipelineCreateOrUpdateParameters()
        {
            Pipeline = new Pipeline()
            {
                Name = PipelineName,
                Properties = new PipelineProperties()
                {
                    Description = "Demo Pipeline for data transfer between blobs",

                    // Initial value for pipeline's active period. With this, you won't need to set slice status
                    Start = PipelineActivePeriodStartTime,
                    End = PipelineActivePeriodEndTime,

                    Activities = new List<Activity>()
                    {
                        new Activity()
                        {
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
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
                    }
                }
            }
        });
    ```

    <span data-ttu-id="73214-211">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-211">Note the following points:</span></span>
   
    - <span data-ttu-id="73214-212">작업 섹션에는 **형식**이 **복사**로 설정된 작업만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-212">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="73214-213">복사 활동에 대한 자세한 내용은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-213">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="73214-214">Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="73214-215">작업에 대한 입력을 **InputDataset**으로 설정하고 작업에 대한 출력을 **OutputDataset**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-215">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="73214-216">**typeProperties** 섹션에서 **BlobSource**를 원본 유형으로 지정하고 **SqlSink**를 싱크 유형으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-216">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="73214-217">복사 활동에서 원본 및 싱크로 지원되는 데이터 저장소의 전체 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-217">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="73214-218">지원되는 특정 데이터 저장소를 원본/싱크로 사용하는 방법을 알아보려면 표에 나와 있는 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-218">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
   
    <span data-ttu-id="73214-219">현재 출력 데이터 집합은 일정을 작동하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="73214-219">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="73214-220">이 자습서에서는 출력 데이터 집합이 한 시간에 한 번씩 조각을 생성하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="73214-220">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="73214-221">이 파이프라인은 하루 24시간 간격, 즉 24시간 동안에 걸친 시작 시간과 종료 시간을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-221">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="73214-222">따라서 24개의 출력 데이터 집합이 파이프라인에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="73214-222">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span>
12. <span data-ttu-id="73214-223">**Main** 메서드에 다음 코드를 추가하여 출력 데이터 집합의 데이터 조각 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="73214-223">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="73214-224">이 샘플에서는 조각만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-224">There is only slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;

    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling the slice status");        
        // wait before the next status check
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

13. <span data-ttu-id="73214-225">데이터 조각의 실행 정보를 가져오는 다음 코드를 **Main** 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-225">Add the following code to get run details for a data slice to the **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");

    // give it a few minutes for the output slice to be ready
    Console.WriteLine("\nGive it a few minutes for the output slice to be ready and press any key.");
    Console.ReadKey();

    var datasliceRunListResponse = client.DataSliceRuns.List(
            resourceGroupName,
            dataFactoryName,
            Dataset_Destination,
            new DataSliceRunListParameters()
            {
                DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
            }
        );

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

    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```

14. <span data-ttu-id="73214-226">**Main** 메서드에서 사용하는 다음 도우미 메서드를 **Program** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-226">Add the following helper method used by the **Main** method to the **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="73214-227">다음 코드를 복사하여 붙여넣을 때 복사된 코드가 Main 메서드와 동일한 수준인지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="73214-227">When you copy and paste the following code, make sure that the copied code is at the same level as the Main method.</span></span>

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

        throw new InvalidOperationException("Failed to acquire token");
    }
    ```

15. <span data-ttu-id="73214-228">솔루션 탐색기에서 프로젝트(DataFactoryAPITestApp)를 확장하고 **참조**를 마우스 오른쪽 단추로 클릭한 다음 **참조 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-228">In the Solution Explorer, expand the project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="73214-229">**System.Configuration** 어셈블리에 대한 확인란을 선택하고</span><span class="sxs-lookup"><span data-stu-id="73214-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="73214-230">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-230">and click **OK**.</span></span>
16. <span data-ttu-id="73214-231">콘솔 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-231">Build the console application.</span></span> <span data-ttu-id="73214-232">메뉴에서 **빌드**를 클릭하고 **솔루션 빌드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-232">Click **Build** on the menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="73214-233">Azure Blob 저장소의 **adftutorial** 컨테이너에 하나 이상의 파일이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-233">Confirm that there is at least one file in the **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="73214-234">그렇지 않은 경우 메모장에서 다음 내용이 포함된 **Emp.txt** 파일을 만들어 adftutorial 컨테이너에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-234">If not, create **Emp.txt** file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="73214-235">메뉴에서 **디버그** -> **디버깅 시작**을 클릭하여 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-235">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="73214-236">**데이터 조각의 실행 정보 가져오기**가 표시되면 몇 분 동안 기다린 다음 **ENTER** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="73214-236">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="73214-237">Azure 포털을 사용하여 데이터 팩터리 **APITutorialFactory** 가 다음 아티팩트로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-237">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
   * <span data-ttu-id="73214-238">연결된 서비스: **LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="73214-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="73214-239">데이터 집합: **InputDataset** 및 **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="73214-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="73214-240">파이프라인: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="73214-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="73214-241">지정된 Azure SQL Database의 **emp** 테이블에서 두 개의 직원 레코드가 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-241">Verify that the two employee records are created in the **emp** table in the specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73214-242">다음 단계</span><span class="sxs-lookup"><span data-stu-id="73214-242">Next steps</span></span>
<span data-ttu-id="73214-243">Data Factory용 .NET API에 대한 포괄적인 설명서는 [데이터 팩터리 .NET API 참조](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="73214-244">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="73214-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="73214-245">다음 표에서는 복사 활동에서 원본 및 싱크로 지원되는 데이터 저장소의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="73214-245">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="73214-246">데이터 저장소간에 데이터를 복사하는 방법에 대해 알아보려면 테이블에서 데이터 저장소에 대한 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="73214-246">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>

