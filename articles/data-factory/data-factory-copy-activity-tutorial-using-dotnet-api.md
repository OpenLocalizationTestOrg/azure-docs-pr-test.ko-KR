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
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="3ebba-103">자습서: .NET API를 사용하여 복사 작업이 있는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="3ebba-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ebba-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="3ebba-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="3ebba-105">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="3ebba-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="3ebba-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="3ebba-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="3ebba-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3ebba-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="3ebba-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ebba-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="3ebba-109">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="3ebba-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="3ebba-110">REST API</span><span class="sxs-lookup"><span data-stu-id="3ebba-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="3ebba-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="3ebba-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="3ebba-112">이 문서에서는 설명 어떻게 toouse [.NET API](https://portal.azure.com) toocreate 데이터 팩터리 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 파이프라인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-112">In this article, you learn how toouse [.NET API](https://portal.azure.com) toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="3ebba-113">새 tooAzure 데이터 팩터리 인 경우 hello 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 이 자습서를 수행 하기 전에 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="3ebba-114">이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="3ebba-115">hello 복사 작업 지원 되는 데이터 저장소 tooa 싱크를 지원 되는 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="3ebba-116">원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ebba-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="3ebba-117">hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="3ebba-118">Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="3ebba-119">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="3ebba-120">및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="3ebba-121">자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ebba-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="3ebba-122">Data Factory용 .NET API에 대한 포괄적인 설명서는 [데이터 팩터리 .NET API 참조](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ebba-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="3ebba-123">이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-123">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="3ebba-124">방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: 빌드 Hadoop 클러스터를 사용 하 여 파이프라인 tootransform 데이터](data-factory-build-your-first-pipeline.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-124">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ebba-125">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3ebba-125">Prerequisites</span></span>
* <span data-ttu-id="3ebba-126">통해 이동 [자습서 개요 및 필수](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget hello 자습서 및 전체 hello 개요 **필수 구성 요소** 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget an overview of hello tutorial and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="3ebba-127">Visual Studio 2012, 2013 또는 2015</span><span class="sxs-lookup"><span data-stu-id="3ebba-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="3ebba-128">[Azure .NET SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="3ebba-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="3ebba-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ebba-129">Azure PowerShell.</span></span> <span data-ttu-id="3ebba-130">지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고](../powershell-install-configure.md) 컴퓨터에 Azure PowerShell tooinstall 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-130">Follow instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="3ebba-131">Azure PowerShell toocreate Azure Active Directory 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-131">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="3ebba-132">Azure Active Directory에서 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="3ebba-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="3ebba-133">Azure Active Directory 응용 프로그램을 만들고 hello 응용 프로그램에 대 한 서비스 사용자를 만들, toohello 할당 **데이터 팩터리 참가자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-133">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="3ebba-134">**PowerShell**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="3ebba-135">Hello 다음 명령을 실행 하 고 hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="3ebba-136">이 계정에 대 한 모든 hello 구독 hello 명령 tooview 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-136">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="3ebba-137">다음 명령 tooselect hello 피드에 있는 toowork hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="3ebba-138">대체  **&lt;NameOfAzureSubscription** &gt; hello 이름의 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="3ebba-138">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="3ebba-139">기록해 두고 **SubscriptionId** 및 **TenantId** hello이이 명령의 출력에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-139">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="3ebba-140">라는 Azure 리소스 그룹 만들기 **ADFTutorialResourceGroup** hello 다음 hello PowerShell에서에서 명령을 실행 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="3ebba-141">Hello 리소스 그룹이 이미 있는 경우, 지정 여부 tooupdate 것 (Y) 하거나 (N)로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-141">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="3ebba-142">다른 리소스 그룹을 사용 하는 경우이 자습서의 ADFTutorialResourceGroup 대신 리소스 그룹의 toouse hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-142">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="3ebba-143">Azure Active Directory 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="3ebba-144">Hello 다음 오류가 발생 하는 경우 다른 URL을 지정 하 고 hello 명령을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-144">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="3ebba-145">Hello AD 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-145">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="3ebba-146">서비스 보안 주체 toohello 추가 **데이터 팩터리 참가자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-146">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="3ebba-147">Hello 응용 프로그램 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-147">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="3ebba-148">Hello hello 출력에서 응용 프로그램 ID (applicationID) 아래로 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-148">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="3ebba-149">이 단계에서 다음과 같은 4가지 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="3ebba-150">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="3ebba-150">Tenant ID</span></span>
* <span data-ttu-id="3ebba-151">구독 ID</span><span class="sxs-lookup"><span data-stu-id="3ebba-151">Subscription ID</span></span>
* <span data-ttu-id="3ebba-152">응용 프로그램 UI</span><span class="sxs-lookup"><span data-stu-id="3ebba-152">Application ID</span></span>
* <span data-ttu-id="3ebba-153">암호 (hello 첫 번째 명령에 지정 됨)</span><span class="sxs-lookup"><span data-stu-id="3ebba-153">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="3ebba-154">연습</span><span class="sxs-lookup"><span data-stu-id="3ebba-154">Walkthrough</span></span>
1. <span data-ttu-id="3ebba-155">Visual Studio 2012/2013/2015를 사용하여 C# .NET 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="3ebba-156">**Visual Studio** 2012/2013/2015를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="3ebba-157">클릭 **파일**, 너무 가리킨**새로**를 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-157">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="3ebba-158">**템플릿**을 확장하고 **Visual C#**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="3ebba-159">이 연습에서는 C#을 사용하지만 모든 .NET 언어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="3ebba-160">선택 **콘솔 응용 프로그램** hello hello 오른쪽에 프로젝트 형식 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-160">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="3ebba-161">입력 **DataFactoryAPITestApp** hello 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-161">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="3ebba-162">선택 **C:\ADFGetStarted** hello 위치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-162">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="3ebba-163">클릭 **확인** toocreate hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="3ebba-163">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="3ebba-164">클릭 **도구**, 너무 가리킨**NuGet 패키지 관리자**를 클릭 하 고 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-164">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="3ebba-165">Hello에 **패키지 관리자 콘솔**, 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-165">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="3ebba-166">다음 명령 tooinstall Data Factory 패키지 hello를 실행 합니다.`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="3ebba-166">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="3ebba-167">Hello 명령 tooinstall Azure Active Directory 패키지 (Active Directory API 코드에서 사용 hello) 다음을 실행 합니다.`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="3ebba-167">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="3ebba-168">Hello 다음 추가 **appSetttings** 섹션 toohello **App.config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-168">Add hello following **appSetttings** section toohello **App.config** file.</span></span> <span data-ttu-id="3ebba-169">이러한 설정은 hello 도우미 메서드에서 사용 됩니다: **GetAuthorizationHeader**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-169">These settings are used by hello helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="3ebba-170">**&lt;응용 프로그램 ID&gt;**, **&lt;암호&gt;**, **&lt;구독 ID&gt;** 및 **&lt;테넌트 ID&gt;**의 값을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="3ebba-171">Hello 다음 추가 **를 사용 하 여** hello 프로젝트에서 문 toohello 소스 파일 (Program.cs).</span><span class="sxs-lookup"><span data-stu-id="3ebba-171">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

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

6. <span data-ttu-id="3ebba-172">인스턴스를 만드는 코드 다음 hello 추가 **DataPipelineManagementClient** 클래스 toohello **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3ebba-172">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="3ebba-173">이 개체 toocreate을 사용 하 여 데이터 팩터리, 연결된 된 서비스, 입력 및 출력 데이터 집합 및 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="3ebba-173">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="3ebba-174">또한 런타임에 데이터 집합의 개체 toomonitor 조각을이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-174">You also use this object toomonitor slices of a dataset at runtime.</span></span>

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
   > <span data-ttu-id="3ebba-175">Hello 값의 대체 **resourceGroupName** hello Azure 리소스 그룹 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-175">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="3ebba-176">Hello 데이터 팩터리 () toobe 고유의 이름을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-176">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="3ebba-177">Hello 데이터 팩터리의 이름을 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-177">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="3ebba-178">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ebba-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="3ebba-179">추가 코드를 만드는 다음 hello는 **데이터 팩터리의** toohello **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3ebba-179">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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

    <span data-ttu-id="3ebba-180">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="3ebba-181">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="3ebba-182">예를 들어 원본 tooa 대상 데이터 저장소와 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform에서 복사 작업 toocopy 데이터 데이터 tooproduct 출력 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-182">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="3ebba-183">이 단계에서는 hello 데이터 팩터리를 만드는 것부터 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-183">Let's start with creating hello data factory in this step.</span></span>
8. <span data-ttu-id="3ebba-184">추가 코드를 만드는 다음 hello는 **Azure 저장소 연결 된 서비스** toohello **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3ebba-184">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3ebba-185">**storageaccountname** 및 **accountkey**를 Azure Storage 계정의 이름 및 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="3ebba-186">데이터 팩터리 toolink 데이터 저장 및 계산 toohello 데이터 팩터리 서비스에에서 연결 된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-186">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="3ebba-187">이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="3ebba-188">Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="3ebba-189">이에 따라 두 개의 연결된 서비스, 즉 AzureStorage와 AzureSqlDatabase 유형의 AzureStorageLinkedService와 AzureSqlLinkedService를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="3ebba-190">AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-190">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="3ebba-191">이 저장소 계정은 hello 하나 컨테이너를 생성 하 고 hello 데이터의 일부로 업로드 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-191">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="3ebba-192">추가 코드를 만드는 다음 hello는 **Azure SQL 연결 된 서비스** toohello **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3ebba-192">Add hello following code that creates an **Azure SQL linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3ebba-193">**servername**, **databasename**, **username** 및 **password**를 Azure SQL Server의 이름, 데이터베이스, 사용자 계정 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

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

    <span data-ttu-id="3ebba-194">AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-194">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="3ebba-195">hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-195">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="3ebba-196">이 데이터베이스에 hello emp 테이블의 일부분으로 만든 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-196">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="3ebba-197">추가 코드를 만드는 다음 hello **입력 및 출력 데이터 집합** toohello **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3ebba-197">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

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
    
    <span data-ttu-id="3ebba-198">Hello 이전 단계에서 Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리에 연결 된 서비스 toolink을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-198">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="3ebba-199">이 단계에서는 InputDataset 및 입력을 나타내는 OutputDataset 각각 AzureStorageLinkedService 및 AzureSqlLinkedService에서 참조 하는 hello 데이터 저장소에 저장 되어 있는 출력 데이터 라는 두 개의 데이터 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="3ebba-200">hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-200">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="3ebba-201">고 hello 입력된 blob 데이터 집합 (InputDataset) hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-201">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="3ebba-202">마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-202">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="3ebba-203">및 hello 출력 SQL 테이블의 데이터 집합 (OututDataset) hello blob 저장소에서 데이터를 복사 하는 hello 데이터베이스 toowhich hello에 hello 테이블을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-203">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

    <span data-ttu-id="3ebba-204">이 단계에서는 hello hello AzureStorageLinkedService 연결 된 서비스를 나타내는 Azure 저장소에서에서 blob 컨테이너 (adftutorial)의 hello 루트 폴더에 tooa blob 파일 (emp.txt)를 가리키는 InputDataset 라는 데이터 집합이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-204">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="3ebba-205">하지 hello 파일 이름에 대 한 값을 지정 (하거나 건너뛸 수), 데이터 hello 입력된 폴더의 모든 blob에서 됩니다 복사한 toohello 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-205">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="3ebba-206">이 자습서에서는 hello 파일 이름에 대 한 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-206">In this tutorial, you specify a value for hello fileName.</span></span>    

    <span data-ttu-id="3ebba-207">이 단계에서는 **OutputDataset**이라는 출력 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="3ebba-208">이 데이터 집합으로 표시 하는 hello Azure SQL 데이터베이스의 tooa SQL 테이블 점은 **AzureSqlLinkedService**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-208">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="3ebba-209">Hello 다음 코드를 추가 **가 만들어지고 활성화 파이프라인** toohello **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3ebba-209">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="3ebba-210">이 단계에서는 **InputDataset**을 입력으로 사용하고 **OutputDataset**을 출력으로 사용하는 **복사 활동**을 포함한 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

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

                    // Initial value for pipeline's active period. With this, you won't need tooset slice status
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

    <span data-ttu-id="3ebba-211">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="3ebba-211">Note hello following points:</span></span>
   
    - <span data-ttu-id="3ebba-212">Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-212">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="3ebba-213">Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-213">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="3ebba-214">Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="3ebba-215">Hello 활동 너무 설정 되어 입력**InputDataset** 및 hello 활동 너무 설정 되어 출력**OutputDataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-215">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="3ebba-216">Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-216">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="3ebba-217">원본 및 싱크도 hello 복사 작업에서 지 원하는 데이터 저장소의 전체 목록은 참조 하십시오. [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-217">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="3ebba-218">소스/싱크도 toouse 지원 되는 특정 데이터를 저장 하는 방법 toolearn hello 표에 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-218">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
   
    <span data-ttu-id="3ebba-219">현재 출력 데이터 집합은 어떤 드라이브 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-219">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="3ebba-220">이 자습서에서는 출력 데이터 집합은 구성 된 tooproduce 조각을 두 번는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-220">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="3ebba-221">hello 파이프라인 시작 시간과 종료 시간이 되는 24 시간 이상 떨어져 1 일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-221">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="3ebba-222">따라서 출력 데이터 집합의 24 조각은 hello 파이프라인에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-222">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span>
12. <span data-ttu-id="3ebba-223">다음 코드 toohello hello 추가 **Main** hello의 데이터 조각 방법 tooget hello 상태 출력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-223">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="3ebba-224">이 샘플에서는 조각만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="3ebba-225">다음 코드 tooget 실행 세부 정보에 대 한 데이터 조각 toohello hello 추가 **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3ebba-225">Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

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

    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```

14. <span data-ttu-id="3ebba-226">Hello hello에서 사용 하는 도우미 메서드를 다음 추가 **Main** 메서드 toohello **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-226">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3ebba-227">복사한 코드 다음 hello 붙여 넣는 경우 해야 해당 hello 복사한 코드는 동일한 수준으로 hello Main 메서드에 hello에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-227">When you copy and paste hello following code, make sure that hello copied code is at hello same level as hello Main method.</span></span>

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

15. <span data-ttu-id="3ebba-228">솔루션 탐색기 hello, hello 프로젝트 (DataFactoryAPITestApp) 확장 하 고, 마우스 오른쪽 단추로 클릭 **참조**를 클릭 하 고 **참조 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-228">In hello Solution Explorer, expand hello project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="3ebba-229">**System.Configuration** 어셈블리에 대한 확인란을 선택하고</span><span class="sxs-lookup"><span data-stu-id="3ebba-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="3ebba-230">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-230">and click **OK**.</span></span>
16. <span data-ttu-id="3ebba-231">Hello 콘솔 응용 프로그램을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="3ebba-231">Build hello console application.</span></span> <span data-ttu-id="3ebba-232">클릭 **빌드** hello 메뉴에 **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-232">Click **Build** on hello menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="3ebba-233">Hello에 파일을 하나 이상 있는지 확인 **adftutorial** Azure blob 저장소의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-233">Confirm that there is at least one file in hello **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="3ebba-234">그렇지 않은 경우 만들 **Emp.txt** 콘텐츠를 다음 hello로 메모장에서 파일을 toohello adftutorial 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-234">If not, create **Emp.txt** file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="3ebba-235">클릭 하 여 hello 샘플을 실행 **디버그** -> **디버깅 시작** hello 메뉴.</span><span class="sxs-lookup"><span data-stu-id="3ebba-235">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="3ebba-236">Hello 표시 되 면 **데이터 조각에 대 한 세부 정보 실행**, 몇 분 및 키를 눌러 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-236">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="3ebba-237">사용 하 여 hello Azure 포털 tooverify hello 데이터 팩터리에서 **APITutorialFactory** hello 다음 아티팩트를 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-237">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
   * <span data-ttu-id="3ebba-238">연결된 서비스: **LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="3ebba-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="3ebba-239">데이터 집합: **InputDataset** 및 **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="3ebba-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="3ebba-240">파이프라인: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="3ebba-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="3ebba-241">Hello에 hello 두 직원 레코드가 만들어졌는지 확인 **emp** hello 표에 Azure SQL 데이터베이스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-241">Verify that hello two employee records are created in hello **emp** table in hello specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ebba-242">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3ebba-242">Next steps</span></span>
<span data-ttu-id="3ebba-243">Data Factory용 .NET API에 대한 포괄적인 설명서는 [데이터 팩터리 .NET API 참조](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ebba-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="3ebba-244">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="3ebba-245">hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록:</span><span class="sxs-lookup"><span data-stu-id="3ebba-245">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="3ebba-246">toolearn toocopy 데이터는 데이터를 저장 하는 방법에 대 한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ebba-246">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>

