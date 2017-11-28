---
title: "Azure에서 클라우드 저장소 내부/외부로 대량의 데이터 이동 | Microsoft Docs"
description: "Azure Storage 내부/외부로 데이터를 이동하는 다양한 방법에 대한 개요입니다."
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
ms.openlocfilehash: 538a43e549f47709616dd93e7eab9c8cb7d99dc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="moving-data-to-and-from-azure-storage"></a><span data-ttu-id="8fc73-103">Azure 저장소의 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="8fc73-103">Moving data to and from Azure Storage</span></span>
<span data-ttu-id="8fc73-104">온-프레미스 데이터를 Azure 저장소로(또는 그 반대로) 이동하는 여러 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-104">If you want to move on-premises data to Azure Storage (or vice versa), there are a variety of ways to do this.</span></span> <span data-ttu-id="8fc73-105">가장 적합한 방법은 시나리오에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-105">The approach that works best for you will depend on your scenario.</span></span> <span data-ttu-id="8fc73-106">이 문서에서는 다양한 시나리오 그리고 각 시나리오에 적합한 방법을 신속하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-106">This article will provide a quick overview of different scenarios and appropriate offerings for each one.</span></span>

## <a name="building-applications"></a><span data-ttu-id="8fc73-107">응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="8fc73-107">Building Applications</span></span>
<span data-ttu-id="8fc73-108">응용 프로그램을 빌드하는 경우 REST API 또는 Microsoft의 여러 클라이언트 라이브러리 중 하나에 대해 개발하면 Azure 저장소의 데이터를 쉽게 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-108">If you're building an application, developing against the REST API or one of our many client libraries is a great way to move data to and from Azure Storage.</span></span>

<span data-ttu-id="8fc73-109">Azure 저장소는 .NET, iOS, Java, Android, UWP(Universal Windows Platform), Xamarin, C++, Node.JS, PHP, Ruby 및 Python에 대한 풍부한 클라이언트 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-109">Azure Storage provides rich client libraries for .NET, iOS, Java, Android, Universal Windows Platform (UWP), Xamarin, C++, Node.JS, PHP, Ruby, and Python.</span></span> <span data-ttu-id="8fc73-110">이 클라이언트 라이브러리는 재시도 논리, 로깅, 병렬 업로드와 같은 고급 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-110">The client libraries offer advanced capabilities such as retry logic, logging, and parallel uploads.</span></span> <span data-ttu-id="8fc73-111">HTTP/HTTPS 요청이 가능한 모든 언어로 호출할 수 있는 REST API에 대해 바로 개발할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-111">You can also develop directly against the REST API, which can be called by any language that makes HTTP/HTTPS requests.</span></span>

<span data-ttu-id="8fc73-112">자세한 내용은 [Azure Blob 저장소 시작](storage-dotnet-how-to-use-blobs.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-112">See [Get Started with Azure Blob Storage](storage-dotnet-how-to-use-blobs.md) to learn more.</span></span>

<span data-ttu-id="8fc73-113">또한 Azure 내부/외부로 데이터를 복사할 때 고성능을 보장하도록 설계된 라이브러리인 [Azure Storage 데이터 이동 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) 도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-113">In addition, we also offer the [Azure Storage Data Movement Library](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) which is a library designed for high-performance copying of data to and from Azure.</span></span> <span data-ttu-id="8fc73-114">자세한 내용은 데이터 이동 라이브러리 [설명서](https://github.com/Azure/azure-storage-net-data-movement) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-114">Please refer to our Data Movement Library [documentation](https://github.com/Azure/azure-storage-net-data-movement) to learn more.</span></span> 

## <a name="quickly-viewinginteracting-with-your-data"></a><span data-ttu-id="8fc73-115">신속하게 데이터 보기/상호 작용</span><span class="sxs-lookup"><span data-stu-id="8fc73-115">Quickly viewing/interacting with your data</span></span>
<span data-ttu-id="8fc73-116">간편하게 Azure 저장소 데이터를 살펴보고 데이터를 업로드 및 다운로드할 수 있는 기능을 원하신다면 Azure 저장소 탐색기를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-116">If you want an easy way to view your Azure Storage data while also having the ability to upload and download your data, then consider using an Azure Storage Explorer.</span></span>

<span data-ttu-id="8fc73-117">자세한 내용은 [Azure 저장소 탐색기](storage-explorers.md) 목록을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-117">Check out our list of [Azure Storage Explorers](storage-explorers.md) to learn more.</span></span>

## <a name="system-administration"></a><span data-ttu-id="8fc73-118">시스템 관리</span><span class="sxs-lookup"><span data-stu-id="8fc73-118">System Administration</span></span>
<span data-ttu-id="8fc73-119">시스템 관리자처럼 명령줄 유틸리티가 필요하거나 더 편한 분들은 다음 옵션을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-119">If you require or are more comfortable with a command-line utility (e.g. System Administrators), here are a few options for you to consider:</span></span>

### <a name="azcopy"></a><span data-ttu-id="8fc73-120">AzCopy</span><span class="sxs-lookup"><span data-stu-id="8fc73-120">AzCopy</span></span>
<span data-ttu-id="8fc73-121">AzCopy는 Azure 저장소의 데이터를 고속으로 복사하기 위해 설계된 Windows 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-121">AzCopy is a Windows command-line utility designed for high-performance copying of data to and from Azure Storage.</span></span> <span data-ttu-id="8fc73-122">저장소 계정 내에서 또는 여러 저장소 계정 간에 데이터를 복사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-122">You can also copy data within a storage account, or between different storage accounts.</span></span>

<span data-ttu-id="8fc73-123">자세한 내용은 [AzCopy 명령줄 유틸리티로 데이터 전송](storage-use-azcopy.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-123">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) to learn more.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="8fc73-124">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8fc73-124">Azure PowerShell</span></span>
<span data-ttu-id="8fc73-125">Azure PowerShell은 Azure의 서비스를 관리하는 cmdlet을 제공하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-125">Azure PowerShell is a module that provides cmdlets for managing services on Azure.</span></span> <span data-ttu-id="8fc73-126">시스템 관리를 위해 특별히 설계된 작업 기반 명령줄 셸 및 스크립트 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-126">It's a task-based command-line shell and scripting language designed especially for system administration.</span></span>

<span data-ttu-id="8fc73-127">자세한 내용은 [Azure Storage와 함께 Azure PowerShell 사용](storage-powershell-guide-full.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-127">See [Using Azure PowerShell with Azure Storage](storage-powershell-guide-full.md) to learn more.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="8fc73-128">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8fc73-128">Azure CLI</span></span>
<span data-ttu-id="8fc73-129">Azure CLI는 Azure 서비스 작업을 위한 플랫폼 간 오픈 소스 명령 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-129">Azure CLI provides a set of open source, cross-platform commands for working with Azure services.</span></span> <span data-ttu-id="8fc73-130">Azure CLI는 Windows, OSX 및 Linux에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-130">Azure CLI is available on Windows, OSX, and Linux.</span></span>

<span data-ttu-id="8fc73-131">자세한 내용은 [Azure Storage에서 Azure CLI 사용](storage-azure-cli.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-131">See [Using the Azure CLI with Azure Storage](storage-azure-cli.md) to learn more.</span></span>

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a><span data-ttu-id="8fc73-132">느린 네트워크를 통해 대량의 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="8fc73-132">Moving large amounts of data with a slow network</span></span>
<span data-ttu-id="8fc73-133">대량의 데이터 이동과 관련된 가장 큰 과제 중 하나는 전송 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-133">One of the biggest challenges associated with moving large amounts of data is the transfer time.</span></span> <span data-ttu-id="8fc73-134">네트워크 비용에 대한 걱정 없이 또는 코드 작성 없이 Azure 저장소의/로 데이터를 가져오려면 Azure 가져오기/내보내기가 적절한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-134">If you want to get data to/from Azure Storage without worrying about networks costs or writing code, then Azure Import/Export is an appropriate solution.</span></span>

<span data-ttu-id="8fc73-135">자세한 내용은 [Azure 가져오기/내보내기](storage-import-export-service.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-135">See [Azure Import/Export](storage-import-export-service.md) to learn more.</span></span>

## <a name="backing-up-your-data"></a><span data-ttu-id="8fc73-136">데이터 백업</span><span class="sxs-lookup"><span data-stu-id="8fc73-136">Backing up your data</span></span>
<span data-ttu-id="8fc73-137">Azure 저장소에 데이터를 백업해야 하는 경우 Azure 백업을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-137">If you simply need to backup your data to Azure Storage, Azure Backup is the way to go.</span></span> <span data-ttu-id="8fc73-138">Azure 백업은 온-프레미스 데이터 및 Azure VM을 백업하는 강력한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-138">This is a powerful solution for backing up on-premises data and Azure VMs.</span></span>

<span data-ttu-id="8fc73-139">자세한 내용은 [Azure 백업](../backup/backup-introduction-to-azure-backup.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-139">See [Azure Backup](../backup/backup-introduction-to-azure-backup.md) to learn more.</span></span>

## <a name="accessing-your-data-on-premises-and-from-the-cloud"></a><span data-ttu-id="8fc73-140">온-프레미스 및 클라우드 데이터에 액세스</span><span class="sxs-lookup"><span data-stu-id="8fc73-140">Accessing your data on-premises and from the cloud</span></span>
<span data-ttu-id="8fc73-141">온-프레미스 및 클라우드 데이터에 액세스하기 위한 솔루션이 필요한 경우 Azure의 하이브리드 클라우드 저장소 솔루션인 StorSimple을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-141">If you need a solution for accessing your data on-premises and from the cloud, then you should consider using Azure's hybrid cloud storage solution, StorSimple.</span></span> <span data-ttu-id="8fc73-142">이 솔루션은 자주 사용되는 데이터는 SSD에, 가끔 사용되는 데이터는 HDD에, 비활성/백업/보관 데이터는 Azure 저장소에 지능적으로 저장하는 물리적 StorSimple 장치로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-142">This solution consists of a physical StorSimple device that intelligently stores frequently used data on SSDs, occasionally used data on HDDs, and inactive/backup/archival data on Azure Storage.</span></span>

<span data-ttu-id="8fc73-143">자세한 내용은 [StorSimple](../storsimple/storsimple-overview.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-143">See [StorSimple](../storsimple/storsimple-overview.md) to learn more.</span></span>

## <a name="recovering-your-data"></a><span data-ttu-id="8fc73-144">데이터 복구</span><span class="sxs-lookup"><span data-stu-id="8fc73-144">Recovering your data</span></span>
<span data-ttu-id="8fc73-145">온-프레미스 워크로드 및 응용 프로그램이 있는 경우 재해가 발생하더라도 비즈니스를 계속 실행할 수 있는 솔루션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-145">When you have on-premises workloads and applications, you'll need a solution that allows your business to continue running in the event of a disaster.</span></span> <span data-ttu-id="8fc73-146">Azure Site Recovery는 가상 컴퓨터 및 실제 서버의 복제, 장애 조치 및 복구를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-146">Azure Site Recovery handles replication, failover, and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="8fc73-147">복제된 데이터는 Azure 저장소에 저장되므로 보조 현장 데이터 센터가 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-147">Replicated data is stored in Azure Storage, allowing you to eliminate the need for a secondary on-site datacenter.</span></span>

<span data-ttu-id="8fc73-148">자세한 내용은 [Azure Site Recovery](../site-recovery/site-recovery-overview.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-148">See [Azure Site Recovery](../site-recovery/site-recovery-overview.md) to learn more.</span></span>
### <a name="moving-data-faq"></a><span data-ttu-id="8fc73-149">데이터 이동 FAQ:</span><span class="sxs-lookup"><span data-stu-id="8fc73-149">Moving Data FAQ:</span></span>
## <a name="can-i-migrate-vhds-from-one-region-to-another-without-copying"></a><span data-ttu-id="8fc73-150">VHD를 복사하지 않고 한 지역에서 다른 지역으로 마이그레이션할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8fc73-150">Can I migrate VHDs from one region to another without copying?</span></span>
<span data-ttu-id="8fc73-151">지역 간에 VHD를 복사하는 유일한 방법은 각 지역의 저장소 계정 간에 데이터를 복사하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-151">The only way to copy VHDs between region is to copy the data between storage accounts on each region.</span></span> <span data-ttu-id="8fc73-152">이 작업에는 AZCopy를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-152">You can use AZCopy for this.</span></span> <span data-ttu-id="8fc73-153">자세한 내용은 AzCopy 명령줄 유틸리티로 데이터 전송을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-153">See Transfer data with the AzCopy Command-Line Utility to learn more.</span></span> <span data-ttu-id="8fc73-154">대용량 데이터의 경우 Azure Import/Export를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc73-154">For very large amounts of data, you can also Azure Import/Export.</span></span> <span data-ttu-id="8fc73-155">자세한 내용은 [Azure 가져오기/내보내기](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fc73-155">See [Azure Import/Export](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) to learn more.</span></span>
