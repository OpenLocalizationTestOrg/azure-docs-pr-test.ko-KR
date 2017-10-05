---
title: "탄력적 데이터베이스 작업 설치 | Microsoft Docs"
description: "탄력적 작업 기능의 설치에 대한 단계별 안내"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: e7a2d6dbcefbb31d76257eaf96ccc235d7a29416
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="27506-103">탄력적 데이터베이스 작업 설치 개요</span><span class="sxs-lookup"><span data-stu-id="27506-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="27506-104">[**Elastic Database 작업**](sql-database-elastic-jobs-overview.md)은 Azure 클래식 포털을 통해 설치할 수 있습니다. PowerShell 패키지를 설치한 경우에만 PowerShell API를 사용하여 작업을 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through the Azure Classic Portal.You can gain access to create and manage jobs using the PowerShell API only if you install the PowerShell package.</span></span> <span data-ttu-id="27506-105">또한 PowerShell API는 현재 포털보다 훨씬 더 많은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-105">Additionally, the PowerShell APIs provide significantly more functionality than the portal at this point in time.</span></span>

<span data-ttu-id="27506-106">포털을 통해 기존 **탄력적 풀**에서 **Elastic Database 작업**을 이미 설치한 경우 최신 Powershell 미리 보기에는 기존 설치를 업그레이드하는 스크립트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-106">If you have already installed **Elastic Database jobs** through the Portal from an existing **elastic pool**, the latest Powershell preview includes scripts to upgrade your existing installation.</span></span> <span data-ttu-id="27506-107">PowerShell API를 통해 노출된 새로운 기능을 활용하려면 최신 **탄력적 데이터베이스 작업** 구성 요소로 설치를 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-107">It is highly recommended to upgrade your installation to the latest **Elastic Database jobs** components in order to take advantage of new functionality exposed via the PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27506-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="27506-108">Prerequisites</span></span>
* <span data-ttu-id="27506-109">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="27506-109">An Azure subscription.</span></span> <span data-ttu-id="27506-110">무료 평가판에 대해서는 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27506-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="27506-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27506-111">Azure PowerShell.</span></span> <span data-ttu-id="27506-112">[웹 플랫폼 설치 관리자](http://go.microsoft.com/fwlink/p/?linkid=320376)를 사용하여 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-112">Install the latest version using the [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="27506-113">자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27506-113">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="27506-114">[NuGet 명령줄 유틸리티](https://nuget.org/nuget.exe) 는 탄력적 데이터베이스 작업 패키지를 설치하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used to install the Elastic Database jobs package.</span></span> <span data-ttu-id="27506-115">자세한 내용은 http://docs.nuget.org/docs/start-here/installing-nuget을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27506-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-the-elastic-database-jobs-powershell-package"></a><span data-ttu-id="27506-116">탄력적 데이터베이스 작업 PowerShell 패키지 다운로드 및 가져오기</span><span class="sxs-lookup"><span data-stu-id="27506-116">Download and import the Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="27506-117">Microsoft Azure PowerShell 명령 창을 시작하고 NuGet 명령줄 유틸리티(nuget.exe)를 다운로드한 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-117">Launch Microsoft Azure PowerShell command window and navigate to the directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="27506-118">다음 명령을 사용하여 **탄력적 데이터베이스 작업** 패키지를 현재 디렉터리로 다운로드 및 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27506-118">Download and import **Elastic Database jobs** package into the current directory with the following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="27506-119">**Elastic Database 작업** 파일은 로컬 디렉터리에서 **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x**라는 폴더에 배치됩니다. 여기서 *x.x.xxxx.x*는 버전 번호를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-119">The **Elastic Database jobs** files are placed in the local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects the version number.</span></span> <span data-ttu-id="27506-120">PowerShell cmdlet(필요한 클라이언트 .dll 포함)은 **tools\ElasticDatabaseJobs** 하위 디렉터리에 있고 설치, 업그레이드 및 제거하는 PowerShell 스크립트는 **tools** 하위 디렉터리에도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-120">The PowerShell cmdlets (including required client .dlls) are located in the **tools\ElasticDatabaseJobs** sub-directory and the PowerShell scripts to install, upgrade and uninstall also reside in the **tools** sub-directory.</span></span>
3. <span data-ttu-id="27506-121">cd tools를 입력하여 Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x 폴더 아래의 tools 하위 디렉터리로 이동합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-121">Navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="27506-122">.\InstallElasticDatabaseJobsCmdlets.ps1 스크립트를 실행하여 ElasticDatabaseJobs 디렉터리를 $Home\Documents\WindowsPowerShell\Modules에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-122">Execute the .\InstallElasticDatabaseJobsCmdlets.ps1 script to copy the ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="27506-123">그러면 사용할 모듈도 자동으로 가져옵니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-123">This will also automatically import the module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-the-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="27506-124">PowerShell을 사용하여 탄력적 데이터베이스 작업 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="27506-124">Install the Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="27506-125">Microsoft Azure PowerShell 명령 창을 시작하고 Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x 폴더 아래의 \tools 하위 디렉터리로 이동합니다. cd \tools를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-125">Launch a Microsoft Azure PowerShell command window and navigate to the \tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="27506-126">.\InstallElasticDatabaseJobs.ps1 PowerShell 스크립트를 실행하고 요청된 변수에 대한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-126">Execute the .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="27506-127">이 스크립트는 [탄력적 데이터베이스 작업 구성 요소 및 가격 책정](sql-database-elastic-jobs-overview.md#components-and-pricing) 에 설명된 구성 요소를 만들고 종속 구성 요소를 적절하게 사용하도록 Azure 클라우드 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-127">This script will create the components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring the Azure Cloud Service to appropriately use the dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="27506-128">이 명령을 실행하면 **사용자 이름**과 **암호**를 묻는 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="27506-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="27506-129">이는 Azure 자격 증명이 아니며, 새 서버에 만들려는 관리자 자격 증명이 될 사용자 이름과 암호를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-129">This is not your Azure credentials, enter the user name and password that will be the administrator credentials you want to create for the new server.</span></span>

<span data-ttu-id="27506-130">이 샘플 호출에 제공된 매개 변수를 원하는 설정에 대해 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-130">The parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="27506-131">아래에서는 각 매개 변수의 동작에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-131">The following provides more information on the behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="27506-132">매개 변수</span><span class="sxs-lookup"><span data-stu-id="27506-132">Parameter</span></span></th>
    <th><span data-ttu-id="27506-133">설명</span><span class="sxs-lookup"><span data-stu-id="27506-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="27506-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="27506-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="27506-135">새로 만든 Azure 구성 요소를 포함하기 위해 생성된 Azure 리소스 그룹 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-135">Provides the Azure resource group name created to contain the newly created Azure components.</span></span> <span data-ttu-id="27506-136">이 매개 변수의 기본값은 "__ElasticDatabaseJob"입니다.</span><span class="sxs-lookup"><span data-stu-id="27506-136">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="27506-137">이 값은 변경하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-137">It is not recommended to change this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="27506-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="27506-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="27506-139">새로 만든 Azure 구성 요소에 사용할 Azure 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-139">Provides the Azure location to be used for the newly created Azure components.</span></span> <span data-ttu-id="27506-140">이 매개 변수의 기본값은 미국 중부 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="27506-140">This parameter defaults to the Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="27506-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="27506-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="27506-142">설치할 서비스 작업자 수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-142">Provides the number of service workers to install.</span></span> <span data-ttu-id="27506-143">이 매개 변수의 기본값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="27506-143">This parameter defaults to 1.</span></span> <span data-ttu-id="27506-144">작업자 수를 늘려 서비스를 확장하고 고가용성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-144">A higher number of workers can be used to scale out the service and to provide high availability.</span></span> <span data-ttu-id="27506-145">서비스의 고가용성이 필요한 배포에는 "2"를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-145">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="27506-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="27506-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="27506-147">클라우드 서비스 내에서 사용할 VM 크기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-147">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="27506-148">이 매개 변수의 기본값은 A0입니다.</span><span class="sxs-lookup"><span data-stu-id="27506-148">This parameter defaults to A0.</span></span> <span data-ttu-id="27506-149">작업자 역할이 각각 ExtraSmall/Small/Medium/Large 크기를 사용하도록 하는 매개 변수 값 A0/A1/A2/A3이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-149">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="27506-150">작업자 역할 크기에 대한 자세한 내용은 [Elastic Database 작업 구성 요소 및 가격 책정](sql-database-elastic-jobs-overview.md#components-and-pricing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27506-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="27506-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="27506-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="27506-152">스탠더드 버전에 대한 서비스 수준 목표를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-152">Provides the service level objective for a Standard edition.</span></span> <span data-ttu-id="27506-153">이 매개 변수의 기본값은 S0입니다.</span><span class="sxs-lookup"><span data-stu-id="27506-153">This parameter defaults to S0.</span></span> <span data-ttu-id="27506-154">Azure SQL 데이터베이스가 해당 SLO를 사용하도록 하는 매개 변수 값 S0/S1/S2/S3이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-154">Parameter values of S0/S1/S2/S3 are accepted which cause the Azure SQL Database to use the respective SLO.</span></span> <span data-ttu-id="27506-155">SQL Database SLO에 대한 자세한 내용은 [Elastic Database 작업 구성 요소 및 가격 책정](sql-database-elastic-jobs-overview.md#components-and-pricing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27506-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="27506-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="27506-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="27506-157">새로 만든 Azure SQL 데이터베이스 서버에 대한 관리자 사용자 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-157">Provides the admin user name for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="27506-158">지정되지 않은 경우 자격 증명을 요청하는 PowerShell 자격 증명 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="27506-158">When not specified, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="27506-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="27506-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="27506-160">새로 만든 Azure SQL 데이터베이스 서버에 대한 관리자 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-160">Provides the admin password for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="27506-161">제공되지 않은 경우 자격 증명을 요청하는 PowerShell 자격 증명 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="27506-161">When not provided, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="27506-162">다수의 데이터베이스에 대해 병렬로 실행되는 다수의 작업을 대상으로 하는 시스템의 경우 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2와 같은 매개 변수를 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended to specify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="27506-163">PowerShell을 사용하여 기존 탄력적 데이터베이스 작업 구성 요소 설치 업데이트</span><span class="sxs-lookup"><span data-stu-id="27506-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="27506-164">**탄력적 데이터베이스 작업** 을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="27506-165">이 프로세스를 사용하면 제어 데이터베이스를 삭제하고 다시 만들지 않고도 이후에 서비스 코드를 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-165">This process allows for future upgrades of service code without having to drop and recreate the control database.</span></span> <span data-ttu-id="27506-166">동일한 버전 내에서 이 프로세스를 사용하여 서비스 VM 크기 또는 서버 작업자 수를 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-166">This process can also be used within the same version to modify the service VM size or the server worker count.</span></span>

<span data-ttu-id="27506-167">설치의 VM 크기를 업데이트하려면 매개 변수를 선택한 값으로 업데이트하여 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-167">To update the VM size of an installation, run the following script with parameters updated to the values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="27506-168">매개 변수</span><span class="sxs-lookup"><span data-stu-id="27506-168">Parameter</span></span></th>
  <th><span data-ttu-id="27506-169">설명</span><span class="sxs-lookup"><span data-stu-id="27506-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="27506-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="27506-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="27506-171">탄력적 데이터베이스 작업 구성 요소를 처음 설치할 때 사용한 Azure 리소스 그룹 이름을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-171">Identifies the Azure resource group name used when the Elastic Database job components were initially installed.</span></span> <span data-ttu-id="27506-172">이 매개 변수의 기본값은 "__ElasticDatabaseJob"입니다.</span><span class="sxs-lookup"><span data-stu-id="27506-172">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="27506-173">이 값은 변경하지 않는 것이 좋으므로 이 매개 변수를 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-173">Since it is not recommended to change this value, you shouldn't have to specify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="27506-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="27506-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="27506-175">설치할 서비스 작업자 수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-175">Provides the number of service workers to install.</span></span>  <span data-ttu-id="27506-176">이 매개 변수의 기본값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="27506-176">This parameter defaults to 1.</span></span>  <span data-ttu-id="27506-177">작업자 수를 늘려 서비스를 확장하고 고가용성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-177">A higher number of workers can be used to scale out the service and to provide high availability.</span></span>  <span data-ttu-id="27506-178">서비스의 고가용성이 필요한 배포에는 "2"를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-178">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="27506-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="27506-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="27506-180">클라우드 서비스 내에서 사용할 VM 크기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-180">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="27506-181">이 매개 변수의 기본값은 A0입니다.</span><span class="sxs-lookup"><span data-stu-id="27506-181">This parameter defaults to A0.</span></span> <span data-ttu-id="27506-182">작업자 역할이 각각 ExtraSmall/Small/Medium/Large 크기를 사용하도록 하는 매개 변수 값 A0/A1/A2/A3이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-182">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="27506-183">작업자 역할 크기에 대한 자세한 내용은 [Elastic Database 작업 구성 요소 및 가격 책정](sql-database-elastic-jobs-overview.md#components-and-pricing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27506-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-the-elastic-database-jobs-components-using-the-portal"></a><span data-ttu-id="27506-184">포털을 사용하여 탄력적 데이터베이스 작업 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="27506-184">Install the Elastic Database jobs components using the Portal</span></span>
<span data-ttu-id="27506-185">[탄력적 풀을 만든](sql-database-elastic-pool-manage-portal.md)후에 **Elastic Database 작업** 구성 요소를 설치하여 탄력적 풀에 있는 각 데이터베이스에 대한 관리 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27506-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components to enable execution of administrative tasks against each database in the elastic pool.</span></span> <span data-ttu-id="27506-186">**탄력적 데이터베이스 작업** PowerShell API를 사용하는 경우와 달리 포털 인터페이스는 현재 기존 풀에 대한 실행만으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-186">Unlike when using the **Elastic Database jobs** PowerShell APIs, the portal interface is currently restricted to only executing against an existing pool.</span></span>

<span data-ttu-id="27506-187">**예상 완료 시간:** 10분</span><span class="sxs-lookup"><span data-stu-id="27506-187">**Estimated time to complete:** 10 minutes.</span></span>

1. <span data-ttu-id="27506-188">[Azure Portal](https://portal.azure.com/#)을 통해 탄력적 풀의 대시보드 뷰에서 **작업 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-188">From the dashboard view of the elastic pool via the [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="27506-189">처음으로 작업을 만드는 경우 **미리 보기 약관**을 클릭하여 **Elastic Database 작업**을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-189">If you are creating a job for the first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="27506-190">확인란을 클릭하여 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-190">Accept the terms by clicking the checkbox.</span></span>
4. <span data-ttu-id="27506-191">"서비스 설치" 화면에서 **작업 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-191">In the "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![서비스 설치][1]
5. <span data-ttu-id="27506-193">데이터베이스 관리자의 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-193">Type a user name and password for a database admin.</span></span> <span data-ttu-id="27506-194">설치 과정의 일부로 새 Azure SQL 데이터베이스 서버가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-194">As part of the installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="27506-195">이 새로운 서버 내에 제어 데이터베이스라는 새 데이터베이스가 생성되고 탄력적 데이터베이스 작업에 필요한 메타데이터를 포함하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-195">Within this new server, a new database, known as the control database, is created and used to contain the meta data for Elastic Database jobs.</span></span> <span data-ttu-id="27506-196">여기서 만든 사용자 이름 및 암호는 제어 데이터베이스에 로그인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-196">The user name and password created here are used for the purpose of logging in to the control database.</span></span> <span data-ttu-id="27506-197">풀 내의 데이터베이스에 대한 스크립트 실행에는 별도 자격 증명이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-197">A separate credential is used for script execution against the databases within the pool.</span></span>
   
    ![사용자 이름 및 암호 만들기][2]
6. <span data-ttu-id="27506-199">확인 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-199">Click the OK button.</span></span> <span data-ttu-id="27506-200">몇 분 안에 새 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)에 사용자를 위한 구성 요소가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-200">The components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="27506-201">새 리소스 그룹은 아래 나온 것처럼 시작 보드에 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-201">The new resource group is pinned to the start board, as shown below.</span></span> <span data-ttu-id="27506-202">생성이 완료되면 탄력적 데이터베이스 작업(클라우드 서비스, SQL 데이터베이스, 서비스 버스, 저장소)이 그룹 내에 모두 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-202">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in the group.</span></span>
   
    ![시작 보드 내의 리소스 그룹][3]
7. <span data-ttu-id="27506-204">탄력적 데이터베이스 작업이 설치되는 동안 작업을 만들거나 관리하려고 하면 **자격 증명** 을 제출할 때 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="27506-204">If you attempt to create or manage a job while elastic database jobs is installing, when providing **Credentials** you will see the following message.</span></span>
   
    ![배포가 아직 진행 중입니다.][4]

<span data-ttu-id="27506-206">제거해야 하는 경우 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="27506-206">If uninstallation is required, delete the resource group.</span></span> <span data-ttu-id="27506-207">[탄력적 데이터베이스 작업 구성 요소를 제거하는 방법](sql-database-elastic-jobs-uninstall.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27506-207">See [How to uninstall the Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27506-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="27506-208">Next steps</span></span>
<span data-ttu-id="27506-209">스크립트 실행에 적절한 권한이 있는 자격 증명이 그룹의 각 데이터베이스에 만들어졌는지 확인합니다. 자세한 내용은 [SQL Database 보안](sql-database-manage-logins.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27506-209">Ensure a credential with the appropriate rights for script execution is created on each database in the group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="27506-210">시작하려면 [Elastic Database 작업 만들기 및 관리](sql-database-elastic-jobs-create-and-manage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27506-210">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) to get started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
