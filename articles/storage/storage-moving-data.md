---
title: "많은 양의 데이터를 Azure의 클라우드 저장소를 aaaMoving | Microsoft Docs"
description: "Azure 저장소에서 데이터 tooand 이동에 대 한 hello 다른 방법의 개요."
services: storage
documentationcenter: 
author: JarrettRenshaw
manager: msmets
editor: tysonn
ms.assetid: 5e3947a9-d99b-4108-9d57-3eb67c03e7ba
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jarrettr
ms.openlocfilehash: 8f7105fea7c2d28ba9954898743070d338f46a37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-tooand-from-azure-storage"></a><span data-ttu-id="370ac-103">Azure 저장소에서 데이터 tooand 이동</span><span class="sxs-lookup"><span data-stu-id="370ac-103">Moving data tooand from Azure Storage</span></span>
<span data-ttu-id="370ac-104">Toomove 온-프레미스 데이터 tooAzure 저장 하려는 경우 (또는 그 반대로)는 다양 한 방법으로 toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-104">If you want toomove on-premises data tooAzure Storage (or vice versa), there are a variety of ways toodo this.</span></span> <span data-ttu-id="370ac-105">적합 한 경우 hello 방법은 각 시나리오에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-105">hello approach that works best for you will depend on your scenario.</span></span> <span data-ttu-id="370ac-106">이 문서에서는 다양한 시나리오 그리고 각 시나리오에 적합한 방법을 신속하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-106">This article will provide a quick overview of different scenarios and appropriate offerings for each one.</span></span>

## <a name="building-applications"></a><span data-ttu-id="370ac-107">응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="370ac-107">Building Applications</span></span>
<span data-ttu-id="370ac-108">응용 프로그램을 빌드하는 경우 Azure 저장소에서 훌륭한 방법 toomove 데이터 tooand은 REST API hello 또는 많은 클라이언트 라이브러리 중 하나에 대해 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-108">If you're building an application, developing against hello REST API or one of our many client libraries is a great way toomove data tooand from Azure Storage.</span></span>

<span data-ttu-id="370ac-109">Azure 저장소는 .NET, iOS, Java, Android, UWP(Universal Windows Platform), Xamarin, C++, Node.JS, PHP, Ruby 및 Python에 대한 풍부한 클라이언트 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-109">Azure Storage provides rich client libraries for .NET, iOS, Java, Android, Universal Windows Platform (UWP), Xamarin, C++, Node.JS, PHP, Ruby, and Python.</span></span> <span data-ttu-id="370ac-110">hello 클라이언트 라이브러리에 다시 시도 논리, 로깅 및 병렬 업로드 같은 고급 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-110">hello client libraries offer advanced capabilities such as retry logic, logging, and parallel uploads.</span></span> <span data-ttu-id="370ac-111">Hello HTTP/HTTPS 요청 하는 모든 언어에서 호출 될 수 있는 REST API에 대해 직접 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-111">You can also develop directly against hello REST API, which can be called by any language that makes HTTP/HTTPS requests.</span></span>

<span data-ttu-id="370ac-112">참조 [Azure Blob 저장소 시작](storage-dotnet-how-to-use-blobs.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-112">See [Get Started with Azure Blob Storage](storage-dotnet-how-to-use-blobs.md) toolearn more.</span></span>

<span data-ttu-id="370ac-113">또한 제공 hello [Azure 저장소 데이터 이동을 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) 는 고성능 데이터 tooand의 Azure에서 복사를 위해 설계 된 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-113">In addition, we also offer hello [Azure Storage Data Movement Library](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) which is a library designed for high-performance copying of data tooand from Azure.</span></span> <span data-ttu-id="370ac-114">Tooour 데이터 이동을 라이브러리를 참조 하십시오 [설명서](https://github.com/Azure/azure-storage-net-data-movement) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-114">Please refer tooour Data Movement Library [documentation](https://github.com/Azure/azure-storage-net-data-movement) toolearn more.</span></span> 

## <a name="quickly-viewinginteracting-with-your-data"></a><span data-ttu-id="370ac-115">신속하게 데이터 보기/상호 작용</span><span class="sxs-lookup"><span data-stu-id="370ac-115">Quickly viewing/interacting with your data</span></span>
<span data-ttu-id="370ac-116">또한 hello 기능 tooupload 않고 쉽게 tooview Azure 저장소 데이터를 원하는 데이터를 다운로드 하는 경우는 것이 좋습니다 Azure 저장소 탐색기를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-116">If you want an easy way tooview your Azure Storage data while also having hello ability tooupload and download your data, then consider using an Azure Storage Explorer.</span></span>

<span data-ttu-id="370ac-117">체크 아웃 목록의 [Azure 저장소 탐색기](storage-explorers.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-117">Check out our list of [Azure Storage Explorers](storage-explorers.md) toolearn more.</span></span>

## <a name="system-administration"></a><span data-ttu-id="370ac-118">시스템 관리</span><span class="sxs-lookup"><span data-stu-id="370ac-118">System Administration</span></span>
<span data-ttu-id="370ac-119">필요 하거나 명령줄 유틸리티 (예: 시스템 관리자)에 더 익숙한 경우에 다음 tooconsider 있습니다에 대 한 몇 가지 옵션은입니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-119">If you require or are more comfortable with a command-line utility (e.g. System Administrators), here are a few options for you tooconsider:</span></span>

### <a name="azcopy"></a><span data-ttu-id="370ac-120">AzCopy</span><span class="sxs-lookup"><span data-stu-id="370ac-120">AzCopy</span></span>
<span data-ttu-id="370ac-121">AzCopy는 고성능 데이터 tooand의 Azure 저장소에서 복사를 위해 설계 된 Windows 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-121">AzCopy is a Windows command-line utility designed for high-performance copying of data tooand from Azure Storage.</span></span> <span data-ttu-id="370ac-122">저장소 계정 내에서 또는 여러 저장소 계정 간에 데이터를 복사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-122">You can also copy data within a storage account, or between different storage accounts.</span></span>

<span data-ttu-id="370ac-123">참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-123">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md) toolearn more.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="370ac-124">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="370ac-124">Azure PowerShell</span></span>
<span data-ttu-id="370ac-125">Azure PowerShell은 Azure의 서비스를 관리하는 cmdlet을 제공하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-125">Azure PowerShell is a module that provides cmdlets for managing services on Azure.</span></span> <span data-ttu-id="370ac-126">시스템 관리를 위해 특별히 설계된 작업 기반 명령줄 셸 및 스크립트 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-126">It's a task-based command-line shell and scripting language designed especially for system administration.</span></span>

<span data-ttu-id="370ac-127">참조 [Azure 저장소와 Azure PowerShell을 사용 하 여](storage-powershell-guide-full.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-127">See [Using Azure PowerShell with Azure Storage](storage-powershell-guide-full.md) toolearn more.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="370ac-128">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="370ac-128">Azure CLI</span></span>
<span data-ttu-id="370ac-129">Azure CLI는 Azure 서비스 작업을 위한 플랫폼 간 오픈 소스 명령 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-129">Azure CLI provides a set of open source, cross-platform commands for working with Azure services.</span></span> <span data-ttu-id="370ac-130">Azure CLI는 Windows, OSX 및 Linux에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-130">Azure CLI is available on Windows, OSX, and Linux.</span></span>

<span data-ttu-id="370ac-131">참조 [hello를 사용 하 여 Azure 저장소와 Azure CLI](storage-azure-cli.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-131">See [Using hello Azure CLI with Azure Storage](storage-azure-cli.md) toolearn more.</span></span>

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a><span data-ttu-id="370ac-132">느린 네트워크를 통해 대량의 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="370ac-132">Moving large amounts of data with a slow network</span></span>
<span data-ttu-id="370ac-133">많은 양의 데이터 이동과 관련 된 hello 가장 큰 해결 과제 중 하나에 hello 전송 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-133">One of hello biggest challenges associated with moving large amounts of data is hello transfer time.</span></span> <span data-ttu-id="370ac-134">네트워크 비용에 대 한 걱정 하거나 코드를 작성 하지 않고도 Azure 저장소에서 tooget 데이터를 원하는 경우 Azure 가져오기/내보내기 적절 한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-134">If you want tooget data to/from Azure Storage without worrying about networks costs or writing code, then Azure Import/Export is an appropriate solution.</span></span>

<span data-ttu-id="370ac-135">참조 [Azure 가져오기/내보내기](storage-import-export-service.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-135">See [Azure Import/Export](storage-import-export-service.md) toolearn more.</span></span>

## <a name="backing-up-your-data"></a><span data-ttu-id="370ac-136">데이터 백업</span><span class="sxs-lookup"><span data-stu-id="370ac-136">Backing up your data</span></span>
<span data-ttu-id="370ac-137">해야 할 경우 단순히 toobackup 사용자 데이터 tooAzure 저장소, Azure 백업은 hello 방식으로 toogo입니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-137">If you simply need toobackup your data tooAzure Storage, Azure Backup is hello way toogo.</span></span> <span data-ttu-id="370ac-138">Azure 백업은 온-프레미스 데이터 및 Azure VM을 백업하는 강력한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-138">This is a powerful solution for backing up on-premises data and Azure VMs.</span></span>

<span data-ttu-id="370ac-139">참조 [Azure 백업](../backup/backup-introduction-to-azure-backup.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-139">See [Azure Backup](../backup/backup-introduction-to-azure-backup.md) toolearn more.</span></span>

## <a name="accessing-your-data-on-premises-and-from-hello-cloud"></a><span data-ttu-id="370ac-140">데이터 온-프레미스에 액세스 하 고 hello 클라우드에서</span><span class="sxs-lookup"><span data-stu-id="370ac-140">Accessing your data on-premises and from hello cloud</span></span>
<span data-ttu-id="370ac-141">데이터 온-프레미스에 액세스 하 고 hello 클라우드에서 솔루션이 필요한 경우 Azure의 하이브리드 클라우드 저장소 솔루션을 StorSimple을 사용 하 여 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-141">If you need a solution for accessing your data on-premises and from hello cloud, then you should consider using Azure's hybrid cloud storage solution, StorSimple.</span></span> <span data-ttu-id="370ac-142">이 솔루션은 자주 사용되는 데이터는 SSD에, 가끔 사용되는 데이터는 HDD에, 비활성/백업/보관 데이터는 Azure 저장소에 지능적으로 저장하는 물리적 StorSimple 장치로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-142">This solution consists of a physical StorSimple device that intelligently stores frequently used data on SSDs, occasionally used data on HDDs, and inactive/backup/archival data on Azure Storage.</span></span>

<span data-ttu-id="370ac-143">참조 [StorSimple](../storsimple/storsimple-overview.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-143">See [StorSimple](../storsimple/storsimple-overview.md) toolearn more.</span></span>

## <a name="recovering-your-data"></a><span data-ttu-id="370ac-144">데이터 복구</span><span class="sxs-lookup"><span data-stu-id="370ac-144">Recovering your data</span></span>
<span data-ttu-id="370ac-145">온-프레미스 작업 부하 및 응용 프로그램, 있는 경우에 재해의 hello 이벤트에서 실행 하 여 비즈니스 toocontinue 수 있는 솔루션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-145">When you have on-premises workloads and applications, you'll need a solution that allows your business toocontinue running in hello event of a disaster.</span></span> <span data-ttu-id="370ac-146">Azure Site Recovery는 가상 컴퓨터 및 실제 서버의 복제, 장애 조치 및 복구를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-146">Azure Site Recovery handles replication, failover, and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="370ac-147">복제 된 데이터는 보조 온사이트 데이터 센터에 대 한 tooeliminate hello 필요성을 허용 하는 Azure 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-147">Replicated data is stored in Azure Storage, allowing you tooeliminate hello need for a secondary on-site datacenter.</span></span>

<span data-ttu-id="370ac-148">참조 [Azure Site Recovery](../site-recovery/site-recovery-overview.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-148">See [Azure Site Recovery](../site-recovery/site-recovery-overview.md) toolearn more.</span></span>
### <a name="moving-data-faq"></a><span data-ttu-id="370ac-149">데이터 이동 FAQ:</span><span class="sxs-lookup"><span data-stu-id="370ac-149">Moving Data FAQ:</span></span>
## <a name="can-i-migrate-vhds-from-one-region-tooanother-without-copying"></a><span data-ttu-id="370ac-150">마이그레이션할 수 Vhd에서 한 영역 tooanother 복사 하지 않고?</span><span class="sxs-lookup"><span data-stu-id="370ac-150">Can I migrate VHDs from one region tooanother without copying?</span></span>
<span data-ttu-id="370ac-151">hello만 방법은 toocopy Vhd 영역 간에 toocopy hello 데이터 각 지역에 저장소 계정 간에입니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-151">hello only way toocopy VHDs between region is toocopy hello data between storage accounts on each region.</span></span> <span data-ttu-id="370ac-152">이 작업에는 AZCopy를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-152">You can use AZCopy for this.</span></span> <span data-ttu-id="370ac-153">더 많은 AzCopy 명령줄 유틸리티 toolearn hello 사용 하 여 전송 데이터를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="370ac-153">See Transfer data with hello AzCopy Command-Line Utility toolearn more.</span></span> <span data-ttu-id="370ac-154">대용량 데이터의 경우 Azure Import/Export를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-154">For very large amounts of data, you can also Azure Import/Export.</span></span> <span data-ttu-id="370ac-155">참조 [Azure 가져오기/내보내기](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="370ac-155">See [Azure Import/Export](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) toolearn more.</span></span>
