---
title: "Azure File Storage 소개 | Microsoft Docs"
description: "Microsoft Cloud에서 네트워크 파일 공유를 제공하는 Azure File Storage 소개"
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 498af5cffb76e026c9a87127cab238f0f23b668a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-file-storage"></a><span data-ttu-id="eafe9-103">Azure File Storage 소개</span><span class="sxs-lookup"><span data-stu-id="eafe9-103">Introduction to Azure File storage</span></span>

<span data-ttu-id="eafe9-104">Azure File Storage는 업계 표준 [SMB(서버 메시지 블록) 프로토콜](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) 및 [CIFS(Common Internet File System)](https://technet.microsoft.com/library/cc939973.aspx)를 사용하여 클라우드에 네트워크 파일 공유를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-104">Azure File storage offers network file shares in the cloud using the industry standard [Server Message Block (SMB) Protocol](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) and [Common Internet File System (CIFS)](https://technet.microsoft.com/library/cc939973.aspx).</span></span> <span data-ttu-id="eafe9-105">Azure 파일 공유는 Windows, macOS, Linux를 실행하는 Azure Virtual Machines 또는 온-프레미스 환경에서 동시에 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-105">Azure File shares can be mounted concurrently by Azure Virtual Machines and on-premises deployments running Windows, macOS, or Linux.</span></span> <span data-ttu-id="eafe9-106">범용 저장소 계정을 사용하여 Azure File Storage, Azure Blob Storage 및 Azure Queue Storage에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-106">A general-purpose storage account gives you access to Azure File storage, Azure Blob storage, and Azure Queue storage.</span></span>

## <a name="videos"></a><span data-ttu-id="eafe9-107">비디오</span><span class="sxs-lookup"><span data-stu-id="eafe9-107">Videos</span></span>
| <span data-ttu-id="eafe9-108">Azure File Storage 소개(27분)</span><span class="sxs-lookup"><span data-stu-id="eafe9-108">Introducing Azure File storage (27m)</span></span> | <span data-ttu-id="eafe9-109">Azure File Storage 자습서(5분)</span><span class="sxs-lookup"><span data-stu-id="eafe9-109">Azure File storage Tutorial (5 minutes)</span></span>  |
|-|-|
| <span data-ttu-id="eafe9-110">[![Azure File Storage 소개 비디오의 동영상 가이드 - 재생하려면 클릭하세요.](./media/storage-files-introduction/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs)</span><span class="sxs-lookup"><span data-stu-id="eafe9-110">[![Screencast of the Introducing Azure File storage video - click to play!](./media/storage-files-introduction/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs)</span></span> | <span data-ttu-id="eafe9-111">[![Azure File Storage 자습서 비디오의 동영상 가이드 - 재생하려면 클릭하세요.](./media/storage-files-introduction/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/)</span><span class="sxs-lookup"><span data-stu-id="eafe9-111">[![Screencast of the Azure File storage Tutorial - click to play!](./media/storage-files-introduction/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/)</span></span> |

## <a name="why-azure-file-storage-is-useful"></a><span data-ttu-id="eafe9-112">Azure File Storage가 유용한 이유</span><span class="sxs-lookup"><span data-stu-id="eafe9-112">Why Azure File storage is useful</span></span>

<span data-ttu-id="eafe9-113">Azure File Storage를 사용하면 온-프레미스 또는 클라우드에서 호스팅되는 Windows Server, Linux 또는 NAS 기반 파일 서버를 OS가 필요 없는 클라우드 파일 공유로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-113">Azure File storage allows you to replace Windows Server, Linux, or NAS-based file servers hosted on-premises or in the cloud with an OS-free cloud file share.</span></span> <span data-ttu-id="eafe9-114">Azure 파일 저장소에는 다음과 같은 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-114">Azure File storage has the following benefits:</span></span>

* <span data-ttu-id="eafe9-115">**공유 액세스** Azure 파일 공유는 산업 표준 SMB 프로토콜을 지원합니다. 즉, 응용 프로그램 호환성에 대한 걱정 없이 온-프레미스 파일 공유를 Azure 파일 공유로 원활하게 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-115">**Shared access** Azure File shares support the industry standard SMB protocol, meaning you can seamlessly replace your on-premises file shares with Azure File shares without worrying about application compatibility.</span></span> <span data-ttu-id="eafe9-116">여러 컴퓨터, 응용 프로그램/인스턴스의 파일 시스템에 액세스할 수 있다는 것은 Azure File Storage의 중요한 장점입니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-116">Being able to access a file share from multiple machines and applications/instances is a significant advantage with Azure File storage.</span></span>

* <span data-ttu-id="eafe9-117">**완전히 관리** 하드웨어 또는 OS를 관리할 필요 없이 Azure 파일 공유를 만들 수 있습니다. 즉, 중요한 보안 업그레이드로 서버 OS를 패치하거나 결함이 있는 하드 디스크를 교체할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-117">**Fully Managed** Azure File shares can be created without the need to manage hardware or an OS, which means you don't have to deal with patching the server OS with critical security upgrades or replacing faulty hard disks.</span></span>

* <span data-ttu-id="eafe9-118">**스크립팅 및 도구** PowerShell cmdlet 및 Azure CLI를 사용하여 Azure 응용 프로그램 관리의 일부로 Azure 파일 공유를 만들고 탑재하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-118">**Scripting and Tooling** PowerShell cmdlets and Azure CLI can be used to create, mount, and manage Azure File shares as part of the administration of Azure applications.</span></span> <span data-ttu-id="eafe9-119">[Azure Portal](https://portal.azure.com) 및 [Azure Storage 탐색기](https://storageexplorer.com)를 사용하여 Azure 파일 공유를 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-119">You can create and manage Azure File shares using the [Azure portal](https://portal.azure.com) and the [Azure Storage Explorer](https://storageexplorer.com).</span></span> 

* <span data-ttu-id="eafe9-120">**복원력** Azure File Storage는 처음부터 항상 사용할 수 있도록 빌드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-120">**Resiliency** Azure File storage has been built from the ground up to be always available.</span></span> <span data-ttu-id="eafe9-121">온-프레미스 파일 공유를 Azure File Storage로 바꾸는 경우 더 이상 로컬 정전 또는 네트워크 문제를 처리하는 데 주의할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-121">Replacing on-premises file shares with Azure File storage means you no longer have to wake up to deal with local power outages or network issues.</span></span> 

* <span data-ttu-id="eafe9-122">**친숙한 프로그래밍** Azure에서 실행 중인 응용 프로그램은 [파일 시스템 I/O API](https://msdn.microsoft.com/library/system.io.file.aspx)를 통해 공유 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-122">**Familiar Programmability** Applications running in Azure can access data on the share via [file system I/O APIs](https://msdn.microsoft.com/library/system.io.file.aspx).</span></span> <span data-ttu-id="eafe9-123">따라서 개발자는 기존의 코드와 기술을 이용하여 기존 응용 프로그램을 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-123">Developers can therefore leverage their existing code and skills to migrate existing applications.</span></span> <span data-ttu-id="eafe9-124">시스템 IO API 외에도 [.NET](/dotnet/api/overview/azure/storage?view=azure-dotnet) 또는 [Azure Storage REST API](/rest/api/storageservices/file-service-rest-api)용 Azure Storage 클라이언트 라이브러리 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-124">In addition to System IO APIs, you can use any of the Azure storage client Libraries, such as the one for [.NET](/dotnet/api/overview/azure/storage?view=azure-dotnet), or the [Azure Storage REST API](/rest/api/storageservices/file-service-rest-api).</span></span>

<span data-ttu-id="eafe9-125">Azure 파일 공유를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-125">Azure File shares can be used to:</span></span>

* <span data-ttu-id="eafe9-126">**온-프레미스 파일 서버 바꾸기** Azure File Storage는 기존의 온-프레미스 파일 서버 또는 NAS 장치에서 파일 공유를 완전히 바꾸는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-126">**Replace on-premises file servers** Azure File storage can be used to completely replace file shares on traditional on-premises file servers or NAS devices.</span></span> <span data-ttu-id="eafe9-127">Windows, macOS 및 Linux와 같이 자주 사용되는 운영 체제는 전세계 어디서나 Azure File 공유를 쉽게 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-127">Popular operating systems such as Windows, macOS, and Linux can easily mount an Azure File share wherever they are in the world.</span></span>

* <span data-ttu-id="eafe9-128">**응용 프로그램 "전환"**</span><span class="sxs-lookup"><span data-stu-id="eafe9-128">**"Lift and Shift" applications**</span></span>

    <span data-ttu-id="eafe9-129">Azure File Storage를 사용하면 온-프레미스 파일 공유를 통해 응용 프로그램의 구성 요소 간에 데이터를 공유하는 클라우드로 응용 프로그램을 손쉽게 "리프트 앤 시프트"할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-129">Azure File storage makes it easy to "lift and shift" applications to the cloud that use on-premises file shares to share data between parts of the application.</span></span> <span data-ttu-id="eafe9-130">이렇게 구현하려면 각 VM을 파일 공유에 연결한 다음 온-프레미스 파일 공유와 마찬가지로 파일을 읽고 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-130">To implement this, each VM connects to the file share and then it can read and write files just like it would against an on-premises file share.</span></span>

* <span data-ttu-id="eafe9-131">**클라우드 개발 간소화**</span><span class="sxs-lookup"><span data-stu-id="eafe9-131">**Simplify Cloud Development**</span></span>
    
    <span data-ttu-id="eafe9-132">Azure File Storage는 새로운 클라우드 개발 프로젝트를 간소화하기 위해 다양한 방법으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-132">Azure File storage can be used in a number of different ways to simplify new cloud development projects.</span></span>
    
    * <span data-ttu-id="eafe9-133">**공유 응용 프로그램 설정**</span><span class="sxs-lookup"><span data-stu-id="eafe9-133">**Shared Application Settings**</span></span>
    
        <span data-ttu-id="eafe9-134">분산 응용 프로그램의 일반적인 패턴은 다양한 가상 컴퓨터에서 액세스할 수 있는 중앙 위치에 구성 파일을 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-134">A common pattern for distributed applications is to have configuration files in a centralized location where they can be accessed from many different VMs.</span></span> <span data-ttu-id="eafe9-135">이제 이러한 구성 파일을 Azure 파일 공유에 저장하고 모든 응용 프로그램 인스턴스에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-135">Such configuration files can now be stored in an Azure File share, and read by all application instances.</span></span> <span data-ttu-id="eafe9-136">또한 이러한 설정은 REST 인터페이스를 통해 관리할 수 있습니다. 이 인터페이스를 사용하면 전 세계에서 구성 파일에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-136">These settings can also be managed via the REST interface, which allows worldwide access to the configuration files.</span></span>

    * <span data-ttu-id="eafe9-137">**진단 공유**</span><span class="sxs-lookup"><span data-stu-id="eafe9-137">**Diagnostic Share**</span></span>
    
        <span data-ttu-id="eafe9-138">Azure 파일 공유는 로그, 메트릭 및 크래시 덤프와 같은 진단 파일을 저장하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-138">An Azure File share can also be used to save diagnostic files like logs, metrics, and crash dumps.</span></span> <span data-ttu-id="eafe9-139">SMB 및 REST 인터페이스 모두를 통해 파일 공유를 사용하도록 설정하면 응용 프로그램에서 진단 데이터를 처리 및 분석하기 위한 다양한 분석 도구를 빌드하거나 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-139">Having file shares available through both the SMB and REST interface allows applications to build or leverage a variety of analysis tools for processing and analyzing the diagnostic data.</span></span>

    * <span data-ttu-id="eafe9-140">**개발/테스트/디버그**</span><span class="sxs-lookup"><span data-stu-id="eafe9-140">**Dev/Test/Debug**</span></span>

        <span data-ttu-id="eafe9-141">개발자 또는 관리자가 클라우드의 VM에서 작업할 때 종종 도구 또는 유틸리티 모음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-141">When developers or administrators are working on VMs in the cloud, they often need a set of tools or utilities.</span></span> <span data-ttu-id="eafe9-142">필요로 하는 각 가상 컴퓨터에 이러한 유틸리티를 설치 및 배포하는 데에는 시간이 많이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-142">Installing and distributing these utilities on each virtual machine where they are needed can be a time consuming exercise.</span></span> <span data-ttu-id="eafe9-143">Azure File Storage를 사용하면 개발자 또는 관리자가 가상 컴퓨터에서 쉽게 연결할 수 있는 파일 공유에 자신이 좋아하는 도구를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-143">With Azure File storage, a developer or administrator can store their favorite tools on a file share, which can be easily connected to from any virtual machine.</span></span>
        
## <a name="how-does-it-work"></a><span data-ttu-id="eafe9-144">작동 원리</span><span class="sxs-lookup"><span data-stu-id="eafe9-144">How does it work?</span></span>

<span data-ttu-id="eafe9-145">Azure 파일 공유 관리는 온-프레미스 파일 공유 관리보다 훨씬 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-145">Managing Azure File shares is much simpler than managing file shares on-premises.</span></span> <span data-ttu-id="eafe9-146">다음 다이어그램에서는 Azure File Storage 관리 구조를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-146">The following diagram illustrates the Azure File storage management constructs:</span></span>

![파일 구조](./media/storage-files-introduction/files-concepts.png)

* <span data-ttu-id="eafe9-148">**저장소 계정** Azure Storage에 대한 모든 액세스는 저장소 계정을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-148">**Storage Account** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="eafe9-149">저장소 계정 용량에 대한 자세한 내용은 [확장성 및 성능 목표](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eafe9-149">See [Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="eafe9-150">**공유** File Storage 공유는 Azure의 SMB 파일 공유입니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-150">**Share** A File Storage share is an SMB file share in Azure.</span></span> <span data-ttu-id="eafe9-151">모든 디렉터리 및 파일을 부모 공유에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-151">All directories and files must be created in a parent share.</span></span> <span data-ttu-id="eafe9-152">계정에 포함할 수 있는 공유 수에는 제한이 없으며, 공유에 저장할 수 있는 파일 수에는 파일 공유의 최대 5TB의 최대 용량까지 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-152">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the 5 TB total capacity of the file share.</span></span>

* <span data-ttu-id="eafe9-153">**디렉터리** 선택적인 디렉터리 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-153">**Directory** An optional hierarchy of directories.</span></span>

* <span data-ttu-id="eafe9-154">**파일** 공유에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-154">**File** A file in the share.</span></span> <span data-ttu-id="eafe9-155">파일 1개의 크기는 최대 1TB일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-155">A file may be up to 1 TB in size.</span></span>

* <span data-ttu-id="eafe9-156">**URL 형식** 다음 URL 형식을 사용하여 파일에 주소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eafe9-156">**URL format** Files are addressable using the following URL format:</span></span>  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```

## <a name="next-steps"></a><span data-ttu-id="eafe9-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eafe9-157">Next steps</span></span>

* [<span data-ttu-id="eafe9-158">Azure 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="eafe9-158">Create Azure File Share</span></span>](storage-how-to-create-file-share.md)
* [<span data-ttu-id="eafe9-159">Windows에 연결 및 탑재</span><span class="sxs-lookup"><span data-stu-id="eafe9-159">Connect and Mount on Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="eafe9-160">Linux에 연결 및 탑재</span><span class="sxs-lookup"><span data-stu-id="eafe9-160">Connect and Mount on Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="eafe9-161">macOS에 연결 및 탑재</span><span class="sxs-lookup"><span data-stu-id="eafe9-161">Connect and Mount on macOS</span></span>](storage-how-to-use-files-mac.md)
* [<span data-ttu-id="eafe9-162">FAQ</span><span class="sxs-lookup"><span data-stu-id="eafe9-162">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="eafe9-163">Windows에서 문제 해결</span><span class="sxs-lookup"><span data-stu-id="eafe9-163">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)   
* [<span data-ttu-id="eafe9-164">Linux에서 문제 해결</span><span class="sxs-lookup"><span data-stu-id="eafe9-164">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   

<!-- Rena I would remove any articles from here that are more than a year old. - Robin-->
### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="eafe9-165">개념 문서 및 비디오</span><span class="sxs-lookup"><span data-stu-id="eafe9-165">Conceptual articles and videos</span></span>
* [<span data-ttu-id="eafe9-166">Azure File Storage: 원활한 Windows 및 Linux용 클라우드 SMB 파일 시스템(영문)</span><span class="sxs-lookup"><span data-stu-id="eafe9-166">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="eafe9-167">Azure File Storage용 도구 지원</span><span class="sxs-lookup"><span data-stu-id="eafe9-167">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="eafe9-168">Microsoft Azure 저장소와 함께 AzCopy를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="eafe9-168">How to use AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="eafe9-169">Azure 저장소에서 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="eafe9-169">Using the Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)

### <a name="blog-posts"></a><span data-ttu-id="eafe9-170">블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="eafe9-170">Blog posts</span></span>
* [<span data-ttu-id="eafe9-171">Azure 파일 저장소 일반적으로 사용 가능(영문)</span><span class="sxs-lookup"><span data-stu-id="eafe9-171">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="eafe9-172">Azure File Storage 내부 구조(영문)</span><span class="sxs-lookup"><span data-stu-id="eafe9-172">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="eafe9-173">Microsoft Azure 파일 서비스 소개</span><span class="sxs-lookup"><span data-stu-id="eafe9-173">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="eafe9-174">Azure 파일로 데이터 마이그레이션(영문)</span><span class="sxs-lookup"><span data-stu-id="eafe9-174">Migrating data to Azure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="eafe9-175">참조</span><span class="sxs-lookup"><span data-stu-id="eafe9-175">Reference</span></span>
* [<span data-ttu-id="eafe9-176">Storage Client Library for .NET 참조</span><span class="sxs-lookup"><span data-stu-id="eafe9-176">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="eafe9-177">파일 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="eafe9-177">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
