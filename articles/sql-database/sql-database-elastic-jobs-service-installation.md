---
title: "aaaInstalling 탄력적 데이터베이스 작업 | Microsoft Docs"
description: "Hello 탄력적 작업 기능을 설치 하는 과정을 안내 합니다."
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
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="e2191-103">탄력적 데이터베이스 작업 설치 개요</span><span class="sxs-lookup"><span data-stu-id="e2191-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="e2191-104">[**탄력적 데이터베이스 작업** ](sql-database-elastic-jobs-overview.md) PowerShell을 통해 설치할 수 있습니다 또는 Azure 클래식 Portal.You를 얻을 수 hello toocreate 액세스 하는 고 hello PowerShell 패키지를 설치 하는 경우에 hello PowerShell API를 사용 하 여 작업을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through hello Azure Classic Portal.You can gain access toocreate and manage jobs using hello PowerShell API only if you install hello PowerShell package.</span></span> <span data-ttu-id="e2191-105">또한 hello PowerShell Api는이 시점에서 hello 포털 보다 훨씬 더 많은 기능 제공.</span><span class="sxs-lookup"><span data-stu-id="e2191-105">Additionally, hello PowerShell APIs provide significantly more functionality than hello portal at this point in time.</span></span>

<span data-ttu-id="e2191-106">이미 설치한 경우 **탄력적 데이터베이스 작업** 기존 hello 포털을 통해 **탄력적 풀**, hello 최신 Powershell 미리 보기 스크립트 tooupgrade 기존 설치를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-106">If you have already installed **Elastic Database jobs** through hello Portal from an existing **elastic pool**, hello latest Powershell preview includes scripts tooupgrade your existing installation.</span></span> <span data-ttu-id="e2191-107">이 뛰어납니다 tooupgrade 설치 toohello 최신 권장 **탄력적 데이터베이스 작업** 순서 tootake 활용을 통해 노출 되는 새로운 기능에 대 한 구성 요소 hello PowerShell Api입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-107">It is highly recommended tooupgrade your installation toohello latest **Elastic Database jobs** components in order tootake advantage of new functionality exposed via hello PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2191-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e2191-108">Prerequisites</span></span>
* <span data-ttu-id="e2191-109">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="e2191-109">An Azure subscription.</span></span> <span data-ttu-id="e2191-110">무료 평가판에 대해서는 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2191-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e2191-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2191-111">Azure PowerShell.</span></span> <span data-ttu-id="e2191-112">Hello를 사용 하 여 hello 최신 버전 설치 [웹 플랫폼 설치 관리자](http://go.microsoft.com/fwlink/p/?linkid=320376)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-112">Install hello latest version using hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="e2191-113">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-113">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="e2191-114">[NuGet 명령줄 유틸리티](https://nuget.org/nuget.exe) 사용 되는 tooinstall hello 탄력적 데이터베이스 작업 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used tooinstall hello Elastic Database jobs package.</span></span> <span data-ttu-id="e2191-115">자세한 내용은 http://docs.nuget.org/docs/start-here/installing-nuget을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2191-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a><span data-ttu-id="e2191-116">다운로드 하 고 hello 탄력적 데이터베이스 작업 PowerShell 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="e2191-116">Download and import hello Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="e2191-117">Microsoft Azure PowerShell 명령 창을 시작 하 고 다운로드 NuGet 명령줄 유틸리티 (nuget.exe) toohello 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-117">Launch Microsoft Azure PowerShell command window and navigate toohello directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="e2191-118">다운로드 및 가져오기 **탄력적 데이터베이스 작업** 다음 명령을 hello로 hello 현재 디렉터리에 패키지:</span><span class="sxs-lookup"><span data-stu-id="e2191-118">Download and import **Elastic Database jobs** package into hello current directory with hello following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="e2191-119">hello **탄력적 데이터베이스 작업** hello 라는 폴더의 로컬 디렉터리에 파일이 배치 됩니다 **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** 여기서 *x.x.xxxx.x* hello 버전 번호를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-119">hello **Elastic Database jobs** files are placed in hello local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects hello version number.</span></span> <span data-ttu-id="e2191-120">hello PowerShell cmdlet (필요한 클라이언트.dll 포함) hello에 살고 있는 **tools\ElasticDatabaseJobs** 하위 디렉터리 및 PowerShell 스크립트 tooinstall hello 업그레이드 및 제거할 수도 hello에  **도구** 하위 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-120">hello PowerShell cmdlets (including required client .dlls) are located in hello **tools\ElasticDatabaseJobs** sub-directory and hello PowerShell scripts tooinstall, upgrade and uninstall also reside in hello **tools** sub-directory.</span></span>
3. <span data-ttu-id="e2191-121">예를 들어 cd 도구를 입력 하 여 hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x 폴더 toohello tools 하위 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-121">Navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="e2191-122">$Home\Documents\WindowsPowerShell\Modules에 hello.\InstallElasticDatabaseJobsCmdlets.ps1 스크립트 toocopy hello ElasticDatabaseJobs 디렉터리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-122">Execute hello .\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="e2191-123">자동으로 가져옵니다 hello 모듈을 사용에 대 한 예:</span><span class="sxs-lookup"><span data-stu-id="e2191-123">This will also automatically import hello module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="e2191-124">Hello 탄력적 데이터베이스 작업 구성 요소를 PowerShell을 사용 하 여 설치</span><span class="sxs-lookup"><span data-stu-id="e2191-124">Install hello Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="e2191-125">Microsoft Azure PowerShell 명령 창을 시작 하 고 hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x 폴더 toohello \tools 하위 디렉터리를 이동: cd \tools 입력</span><span class="sxs-lookup"><span data-stu-id="e2191-125">Launch a Microsoft Azure PowerShell command window and navigate toohello \tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="e2191-126">Hello.\InstallElasticDatabaseJobs.ps1 PowerShell 스크립트를 실행 하 고 요청 된 해당 변수에 대 한 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-126">Execute hello .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="e2191-127">이 스크립트는에 설명 된 hello 구성 요소를 만듭니다 [탄력적 데이터베이스 작업 구성 요소 및 가격](sql-database-elastic-jobs-overview.md#components-and-pricing) tooappropriately hello Azure 클라우드 서비스를 구성 하는 함께 hello 종속 구성 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-127">This script will create hello components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring hello Azure Cloud Service tooappropriately use hello dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="e2191-128">이 명령을 실행하면 **사용자 이름**과 **암호**를 묻는 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="e2191-129">이 Azure 자격 증명 hello 사용자 이름 및 hello 관리자 자격 증명 toocreate hello 새 서버에 대 한 원하는 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-129">This is not your Azure credentials, enter hello user name and password that will be hello administrator credentials you want toocreate for hello new server.</span></span>

<span data-ttu-id="e2191-130">이 샘플 호출에서 제공 하는 hello 매개 변수에 원하는 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-130">hello parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="e2191-131">hello 다음 각 매개 변수에의 hello 동작에 더 많은 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-131">hello following provides more information on hello behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="e2191-132">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e2191-132">Parameter</span></span></th>
    <th><span data-ttu-id="e2191-133">설명</span><span class="sxs-lookup"><span data-stu-id="e2191-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="e2191-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="e2191-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="e2191-135">Azure 구성 요소를 새로 만든 toocontain hello 만든 hello Azure 리소스 그룹 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-135">Provides hello Azure resource group name created toocontain hello newly created Azure components.</span></span> <span data-ttu-id="e2191-136">이 매개 변수의 기본값 너무 "__ElasticDatabaseJob"입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-136">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="e2191-137">없으면 toochange이이 값을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-137">It is not recommended toochange this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="e2191-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="e2191-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="e2191-139">Azure 구성 요소를 새로 만든 hello에 사용 되는 hello Azure 위치 toobe를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-139">Provides hello Azure location toobe used for hello newly created Azure components.</span></span> <span data-ttu-id="e2191-140">이 매개 변수 기본값 toohello 중앙 미국 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-140">This parameter defaults toohello Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="e2191-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="e2191-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="e2191-142">서비스 작업 자가 tooinstall hello 수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-142">Provides hello number of service workers tooinstall.</span></span> <span data-ttu-id="e2191-143">이 매개 변수 기본값 too1입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-143">This parameter defaults too1.</span></span> <span data-ttu-id="e2191-144">작업자 수가 높을수록 hello 서비스와 tooprovide 고가용성을 사용 하는 tooscale 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-144">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span> <span data-ttu-id="e2191-145">"2" toouse hello 서비스의 고가용성이 필요한 배포를 위한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-145">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="e2191-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="e2191-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="e2191-147">Hello 클라우드 서비스 내에서 사용에 대 한 hello v M 크기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-147">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="e2191-148">이 매개 변수 기본값 tooA0입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-148">This parameter defaults tooA0.</span></span> <span data-ttu-id="e2191-149">A0/A1/A2/A3의 매개 변수 값은 사용할 수 있는 hello 작업자 역할 toouse ExtraSmall/소규모/보통/큰 크기를 각각.</span><span class="sxs-lookup"><span data-stu-id="e2191-149">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="e2191-150">작업자 역할 크기에 대한 자세한 내용은 [Elastic Database 작업 구성 요소 및 가격 책정](sql-database-elastic-jobs-overview.md#components-and-pricing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2191-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="e2191-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="e2191-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="e2191-152">Standard edition에 대 한 hello 서비스 수준 목표를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-152">Provides hello service level objective for a Standard edition.</span></span> <span data-ttu-id="e2191-153">이 매개 변수 기본값 tooS0입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-153">This parameter defaults tooS0.</span></span> <span data-ttu-id="e2191-154">Hello Azure SQL 데이터베이스 시키는 S0/S1/s 2/s 3의 매개 변수 값 들은 toouse hello 해당 SLO입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-154">Parameter values of S0/S1/S2/S3 are accepted which cause hello Azure SQL Database toouse hello respective SLO.</span></span> <span data-ttu-id="e2191-155">SQL Database SLO에 대한 자세한 내용은 [Elastic Database 작업 구성 요소 및 가격 책정](sql-database-elastic-jobs-overview.md#components-and-pricing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2191-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="e2191-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="e2191-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="e2191-157">새로 만든 Azure SQL 데이터베이스 서버 hello에 대 한 hello 관리자 사용자 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-157">Provides hello admin user name for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="e2191-158">지정 하지 않으면 tooprompt hello 자격 증명에 대 한 PowerShell 자격 증명 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-158">When not specified, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="e2191-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="e2191-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="e2191-160">새로 만든 Azure SQL 데이터베이스 서버 hello에 대 한 hello 관리자 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-160">Provides hello admin password for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="e2191-161">제공 되지 tooprompt hello 자격 증명에 대 한 PowerShell 자격 증명 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-161">When not provided, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="e2191-162">많은 수의 데이터베이스에 대해 동시에 실행 중인 작업 수가 많은 것을 대상으로 하는 시스템에 대 한 것이 좋습니다 toospecify 매개 변수 같은:-ServiceWorkerCount 2-ServiceVmSize a 2-SqlServerDatabaseSlo S2 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended toospecify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="e2191-163">PowerShell을 사용하여 기존 탄력적 데이터베이스 작업 구성 요소 설치 업데이트</span><span class="sxs-lookup"><span data-stu-id="e2191-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="e2191-164">**탄력적 데이터베이스 작업** 을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="e2191-165">이 프로세스는 toodrop 필요 없이 서비스 코드의 향후 업그레이드에 대 한 허용 하 고 hello 제어 데이터베이스를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-165">This process allows for future upgrades of service code without having toodrop and recreate hello control database.</span></span> <span data-ttu-id="e2191-166">Hello 내에서이 프로세스를 사용할 수도 있습니다 동일한 버전 toomodify hello 서비스 VM 크기 또는 hello 서버 작업자 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-166">This process can also be used within hello same version toomodify hello service VM size or hello server worker count.</span></span>

<span data-ttu-id="e2191-167">설치 과정의 tooupdate hello VM 크기, 다음 매개 변수를 사용 하 여 스크립트 실행된 hello 업데이트 선택한 toohello 값.</span><span class="sxs-lookup"><span data-stu-id="e2191-167">tooupdate hello VM size of an installation, run hello following script with parameters updated toohello values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="e2191-168">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e2191-168">Parameter</span></span></th>
  <th><span data-ttu-id="e2191-169">설명</span><span class="sxs-lookup"><span data-stu-id="e2191-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="e2191-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="e2191-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="e2191-171">Hello 탄력적 데이터베이스 작업 구성 요소를 처음으로 설치한 경우 사용 하는 hello Azure 리소스 그룹 이름을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-171">Identifies hello Azure resource group name used when hello Elastic Database job components were initially installed.</span></span> <span data-ttu-id="e2191-172">이 매개 변수의 기본값 너무 "__ElasticDatabaseJob"입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-172">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="e2191-173">이 아니어서 권장 toochange이이 값이 매개이 변수 toospecify 없을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-173">Since it is not recommended toochange this value, you shouldn't have toospecify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="e2191-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="e2191-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="e2191-175">서비스 작업 자가 tooinstall hello 수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-175">Provides hello number of service workers tooinstall.</span></span>  <span data-ttu-id="e2191-176">이 매개 변수 기본값 too1입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-176">This parameter defaults too1.</span></span>  <span data-ttu-id="e2191-177">작업자 수가 높을수록 hello 서비스와 tooprovide 고가용성을 사용 하는 tooscale 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-177">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span>  <span data-ttu-id="e2191-178">"2" toouse hello 서비스의 고가용성이 필요한 배포를 위한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-178">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="e2191-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="e2191-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="e2191-180">Hello 클라우드 서비스 내에서 사용에 대 한 hello v M 크기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-180">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="e2191-181">이 매개 변수 기본값 tooA0입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-181">This parameter defaults tooA0.</span></span> <span data-ttu-id="e2191-182">A0/A1/A2/A3의 매개 변수 값은 사용할 수 있는 hello 작업자 역할 toouse ExtraSmall/소규모/보통/큰 크기를 각각.</span><span class="sxs-lookup"><span data-stu-id="e2191-182">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="e2191-183">작업자 역할 크기에 대한 자세한 내용은 [Elastic Database 작업 구성 요소 및 가격 책정](sql-database-elastic-jobs-overview.md#components-and-pricing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2191-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a><span data-ttu-id="e2191-184">Hello 탄력적 데이터베이스 작업 구성 요소를 hello 포털을 사용 하 여 설치</span><span class="sxs-lookup"><span data-stu-id="e2191-184">Install hello Elastic Database jobs components using hello Portal</span></span>
<span data-ttu-id="e2191-185">설정한 후 [탄력적 풀을 만든](sql-database-elastic-pool-manage-portal.md)를 설치할 수 있습니다 **탄력적 데이터베이스 작업** hello 탄력적인 풀의 각 데이터베이스에 대해 관리 작업의 구성 요소 tooenable 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components tooenable execution of administrative tasks against each database in hello elastic pool.</span></span> <span data-ttu-id="e2191-186">사용 하 여 hello 하는 경우와 달리 **탄력적 데이터베이스 작업** PowerShell Api hello 포털 인터페이스는 현재 제한 tooonly 기존 풀에 대해 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-186">Unlike when using hello **Elastic Database jobs** PowerShell APIs, hello portal interface is currently restricted tooonly executing against an existing pool.</span></span>

<span data-ttu-id="e2191-187">**예상 시간 toocomplete:** 10 분입니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-187">**Estimated time toocomplete:** 10 minutes.</span></span>

1. <span data-ttu-id="e2191-188">Hello 통해 hello 탄력적 풀의 hello 대시보드 보기에서 [Azure 포털](https://portal.azure.com/#) , 클릭 **만들기 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-188">From hello dashboard view of hello elastic pool via hello [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="e2191-189">Hello에 대 한 작업이 처음으로 만드는 경우를 설치 해야 **탄력적 데이터베이스 작업** 클릭 하 여 **미리 보기 약관**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-189">If you are creating a job for hello first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="e2191-190">Hello 용어를 클릭 하 여 hello 확인란을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-190">Accept hello terms by clicking hello checkbox.</span></span>
4. <span data-ttu-id="e2191-191">클릭 "설치 서비스" hello 뷰에서 **작업 자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-191">In hello "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Hello 서비스 설치][1]
5. <span data-ttu-id="e2191-193">데이터베이스 관리자의 사용자 이름과 암호를 입력합니다. 새 Azure SQL 데이터베이스 서버는 hello 설치의 일부로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-193">Type a user name and password for a database admin. As part of hello installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="e2191-194">이 새 서버 내에서 hello 제어 데이터베이스 라고 하는 새 데이터베이스를 만들어지고 탄력적 데이터베이스 작업에 대 한 toocontain hello 메타 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-194">Within this new server, a new database, known as hello control database, is created and used toocontain hello meta data for Elastic Database jobs.</span></span> <span data-ttu-id="e2191-195">hello 사용자 이름 및 암호를 여기서 만든 toohello 제어 데이터베이스에서 로깅 hello 목적을 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-195">hello user name and password created here are used for hello purpose of logging in toohello control database.</span></span> <span data-ttu-id="e2191-196">별도 자격 증명 hello 풀 내의 hello 데이터베이스에 대 한 스크립트 실행에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-196">A separate credential is used for script execution against hello databases within hello pool.</span></span>
   
    ![사용자 이름 및 암호 만들기][2]
6. <span data-ttu-id="e2191-198">Hello 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-198">Click hello OK button.</span></span> <span data-ttu-id="e2191-199">hello 구성 요소가 자동으로 만들어집니다를 새로운 몇 분 안에 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-199">hello components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="e2191-200">hello 새 리소스 그룹이 고정 아래와 같이 toohello 보드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-200">hello new resource group is pinned toohello start board, as shown below.</span></span> <span data-ttu-id="e2191-201">일단 만들어지고, 탄력적 데이터베이스 작업 (클라우드 서비스, SQL 데이터베이스, 서비스 버스 및 저장소)은 모두 hello 그룹에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-201">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in hello group.</span></span>
   
    ![시작 보드 내의 리소스 그룹][3]
7. <span data-ttu-id="e2191-203">Toocreate 또는 제공 하는 경우 탄력적 데이터베이스 작업 설치 되는 동안 작업을 관리 하는 경우 **자격 증명** hello 메시지의 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-203">If you attempt toocreate or manage a job while elastic database jobs is installing, when providing **Credentials** you will see hello following message.</span></span>
   
    ![배포가 아직 진행 중입니다.][4]

<span data-ttu-id="e2191-205">제거에 필요한 경우 hello 리소스 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-205">If uninstallation is required, delete hello resource group.</span></span> <span data-ttu-id="e2191-206">참조 [toouninstall hello 탄력적 데이터베이스 구성 요소를 작업 하는 방법을](sql-database-elastic-jobs-uninstall.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-206">See [How toouninstall hello Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2191-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e2191-207">Next steps</span></span>
<span data-ttu-id="e2191-208">스크립트 실행에 대 한 자세한 내용은 참조 하십시오 hello 그룹의 각 데이터베이스에 만들어집니다. hello 적절 한 권한이 있는 자격 증명 확인 [SQL 데이터베이스를 보호](sql-database-manage-logins.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-208">Ensure a credential with hello appropriate rights for script execution is created on each database in hello group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="e2191-209">참조 [만들고 탄력적 데이터베이스 작업 관리](sql-database-elastic-jobs-create-and-manage.md) tooget 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2191-209">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) tooget started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
