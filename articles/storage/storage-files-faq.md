---
title: "Azure File Storage 보안에 대한 FAQ(질문과 대답) | Microsoft Docs"
description: "Azure File Storage에 대해 자주 묻는 질문과 대답(FAQ)을 확인합니다."
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
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: cb2134502a585c4f9772e594f635c10f1841e46f
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a><span data-ttu-id="bc574-103">Azure File Storage 보안에 대한 FAQ(질문과 대답)</span><span class="sxs-lookup"><span data-stu-id="bc574-103">Frequently Asked Questions about Azure File storage</span></span>

## <a name="general"></a><span data-ttu-id="bc574-104">일반</span><span class="sxs-lookup"><span data-stu-id="bc574-104">General</span></span>
* <span data-ttu-id="bc574-105">**Q. Azure File Storage란?**</span><span class="sxs-lookup"><span data-stu-id="bc574-105">**Q. What is Azure File storage?**</span></span>  
   
    <span data-ttu-id="bc574-106">Azure File Storage는 Azure의 분산 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-106">Azure File storage is a distributed file system in Azure.</span></span> <span data-ttu-id="bc574-107">지원되는 Azure Virtual Machine 또는 온-프레미스 컴퓨터에서 저장소를 네이티브 공유로 탑재할 수 있는 SMB 프로토콜 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-107">It provides an SMB protocol interface which allows users to mount the storage as a native share on supported Azure Virtual Machine or on-premises machine.</span></span>

* <span data-ttu-id="bc574-108">**Q. Azure File Storage가 유용한 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-108">**Q. Why is Azure File storage useful?**</span></span>  
   
    <span data-ttu-id="bc574-109">Azure File Storage는 여러 VM 및 플랫폼 간에 공유 데이터 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-109">Azure File storage provides shared data access across multiple VMs and platforms.</span></span> <span data-ttu-id="bc574-110">[Azure File Storage가 유용한 이유](storage-files-introduction.md#why-azure-file-storage-is-useful)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc574-110">Refer to [Why Azure File storage is useful](storage-files-introduction.md#why-azure-file-storage-is-useful).</span></span>

* <span data-ttu-id="bc574-111">**Q. Azure File, Azure Blob 및 Azure Disk는 언제 사용해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-111">**Q. When should I use Azure File vs Azure Blob vs Azure Disk ?**</span></span>  
   
    <span data-ttu-id="bc574-112">Microsoft Azure에서는 클라우드에 데이터를 저장하고 액세스하는 여러 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-112">Microsoft Azure provides several ways to store and access data in the cloud.</span></span>  
   
    <span data-ttu-id="bc574-113">Azure File Storage - 어디서나 저장된 파일에 쉽게 액세스할 수 있는 SMB 인터페이스, 클라이언트 라이브러리 및 REST 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-113">Azure File storage - Provides an SMB interface, client libraries, and a REST interface that allows easy access from anywhere to stored files.</span></span>  
   
    <span data-ttu-id="bc574-114">Azure Blobs - 구조화되지 않은 데이터를 블록 Blob에서 대규모로 저장하고 액세스할 수 있는 클라이언트 라이브러리 및 REST 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-114">Azure Blobs - Provides client libraries and a REST interface that allows unstructured data to be stored and accessed at a massive scale in block blobs.</span></span>  
   
    <span data-ttu-id="bc574-115">Azure Data Disks - 연결된 가상 하드 디스크에서 데이터를 영구적으로 저장하고 액세스할 수 있는 클라이언트 라이브러리 및 REST 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-115">Azure Data Disks - Provides client libraries and a REST interface that allows data to be persistently stored and accessed from an attached virtual hard disk.</span></span>  
   
    <span data-ttu-id="bc574-116">[Azure Blobs, Azure Files 또는 Azure Data Disks를 사용할 시기 결정](storage-decide-blobs-files-disks.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="bc574-116">Learn more on [Deciding when to use Azure Blobs, Azure Files, or Azure Data Disks](storage-decide-blobs-files-disks.md)</span></span>

* <span data-ttu-id="bc574-117">**Q. Azure File Storage로 시작하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-117">**Q. How do I get started using Azure File storage?**</span></span>  
   
    <span data-ttu-id="bc574-118">Azure 파일 공유를 만들어 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-118">You can start by creating an Azure file share.</span></span> <span data-ttu-id="bc574-119">Azure Portal, Azure Storage PowerShell cmdlet, Azure Storage 클라이언트 라이브러리 또는 Azure Storage REST API를 사용하여 Azure 파일 공유를 만들 수 있습니다. 이 자습서에서는 다음 항목에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-119">You can create Azure File shares using Azure Portal, the Azure Storage PowerShell cmdlets, the Azure Storage client libraries, or the Azure Storage REST API.In this tutorial, you will learn:</span></span>

    * [<span data-ttu-id="bc574-120">Azure Portal을 사용하여 Azure 파일 공유를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="bc574-120">Learn how to create Azure File share using the Portal</span></span>](storage-file-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [<span data-ttu-id="bc574-121">Powershell을 사용하여 Azure 파일 공유를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="bc574-121">Learn how to create Azure File share using Powershell</span></span>](storage-file-how-to-create-file-share.md#create-file-share-through-powershell)
    * [<span data-ttu-id="bc574-122">CLI를 사용하여 Azure 파일 공유를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="bc574-122">Learn how to create Azure File share using CLI</span></span>](storage-file-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* <span data-ttu-id="bc574-123">**Q. Azure File Storage는 어떤 복제를 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-123">**Q. What replications are supported by Azure File storage?**</span></span>  
   
    <span data-ttu-id="bc574-124">Azure File Storage는 현재 LRS 또는 GRS만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-124">Azure File storage only supports LRS or GRS right now.</span></span> <span data-ttu-id="bc574-125">우리는 RA-GRS를 지원할 계획이지만 아직 공유할 일정이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-125">We plan to support RA-GRS but there is no timeline to share yet.</span></span>

## <a name="security-authentication-and-access-control"></a><span data-ttu-id="bc574-126">보안, 인증 및 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="bc574-126">Security, Authentication and Access Control</span></span>

* <span data-ttu-id="bc574-127">**Q. Azure File Storage에서 파일에 액세스하는 다른 방법은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-127">**Q. What are different ways to access files in Azure File storage?**</span></span>
    
    <span data-ttu-id="bc574-128">SMB 3.0 프로토콜을 사용하여 로컬 컴퓨터에 파일 공유를 탑재하거나 [저장소 탐색기](http://storageexplorer.com/)와 같은 도구를 사용하여 파일 공유의 파일을 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-128">You can mount the file share on your local machine using SMB 3.0 protocol or use tools like [Storage Explorer](http://storageexplorer.com/) to access files in your file share.</span></span> <span data-ttu-id="bc574-129">응용 프로그램에서 저장소 클라이언트 라이브러리, REST API 또는 Powershell을 사용하여 Azure 파일 공유에서 파일에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-129">From your application, you can use storage client libraries, REST APIs or Powershell to access your files in Azure File share.</span></span>

* <span data-ttu-id="bc574-130">**Q. 웹 브라우저를 통해 특정 파일에 대한 액세스를 제공하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-130">**Q. How can I provide access to a specific file using a web browser?**</span></span>
    
    <span data-ttu-id="bc574-131">SAS를 사용하면 지정된 시간 간격 동안 유효한 특정 권한을 가진 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-131">Using SAS, you can generate tokens with specific permissions that are valid for a specified time interval.</span></span> <span data-ttu-id="bc574-132">예를 들어, 특정 기간 동안 특정 파일에 대해 읽기 전용 액세스 권한이 있는 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-132">For example, you can generate a token with read-only access to a particular file for a specific period of time.</span></span> <span data-ttu-id="bc574-133">이 URL을 소유한 사람은 토큰이 유효한 동안 모든 웹 브라우저에서 파일에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-133">Anyone who possesses this url can access the file directly from any web browser while it is valid.</span></span> <span data-ttu-id="bc574-134">저장소 탐색기 같은 UI에서 SAS 키를 쉽게 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-134">SAS keys can be easily generated from UI like Storage Explorer.</span></span>

* <span data-ttu-id="bc574-135">**Q. 공유 내의 폴더에 대한 읽기 전용 또는 쓰기 전용 권한을 지정할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-135">**Q. Is it possible to specify read-only or write-only permissions on folders within the share?**</span></span>
    
    <span data-ttu-id="bc574-136">SMB를 통해 파일 공유를 마운트하는 경우 이 수준의 사용 권한 제어는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-136">You don't have this level of control over permissions if you mount the file share via SMB.</span></span> <span data-ttu-id="bc574-137">그러나 REST API 또는 클라이언트 라이브러리를 통해 공유 액세스 서명(SAS)를 만들어 이 목적을 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-137">However, you can achieve this by creating a shared access signature (SAS) via the REST API or client libraries.</span></span>  

* <span data-ttu-id="bc574-138">**Q. Azure File Storage에 대한 서버 쪽 암호화를 사용하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-138">**Q. How can I enable Server Side encryption for Azure File storage?**</span></span>

    <span data-ttu-id="bc574-139">Azure File Storage에 대한 [서버 쪽 암호화](storage-service-encryption.md)는 일반적으로 모든 지역과 공용 및 국가별 클라우드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-139">[Server Side Encryption](storage-service-encryption.md) for Azure File storage is generally available in all regions and public and national clouds.</span></span> <span data-ttu-id="bc574-140">[Azure Portal](https://portal.azure.com/), [Microsoft Azure Storage 리소스 공급자 API](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) 또는 [Azure CLI](storage-azure-cli.md)를 사용하여 Azure File Storage에 대한 SSE를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-140">You can enable SSE for Azure File storage using [Azure portal](https://portal.azure.com/),[Microsoft Azure Storage Resource Provider API](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) or [Azure CLI](storage-azure-cli.md).</span></span>
    
    <span data-ttu-id="bc574-141">Azure File Storage에서 SSE를 사용하도록 설정한 후에는 해당 저장소 계정의 파일 저장소에 기록된 모든 새 데이터가 자동으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-141">After enabling SSE on Azure File storage, any new data written to the file storage in that storage account will be automatically encrypted.</span></span> <span data-ttu-id="bc574-142">이 기능은 기존 또는 새 저장소 계정에서 기존 또는 새 공유에 기록된 모든 새로운 데이터에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-142">This feature is available for all new data written to existing or new shares in an existing or new storage account.</span></span> <span data-ttu-id="bc574-143">이 기능을 사용하는 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-143">There is no additional charge for enabling this feature.</span></span> <span data-ttu-id="bc574-144">[Azure File Storage에서 SSE를 사용하도록 설정하는 방법](storage-service-encryption.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="bc574-144">Learn more on [how to enable SSE on Azure File storage](storage-service-encryption.md).</span></span>

* <span data-ttu-id="bc574-145">**Q. Azure File Storage에서 Active Directory 기반 인증을 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-145">**Q. Is Active Directory-based authentication supported by Azure File storage?**</span></span>
   
    <span data-ttu-id="bc574-146">우리는 현재 AD 기반 인증 또는 ACL을 지원하지 않지만 우리의 기능 요청 목록에 해당 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-146">We currently do not support AD-based authentication or ACLs, but do have it in our list of feature requests.</span></span> <span data-ttu-id="bc574-147">현재 Azure 저장소 계정 키는 파일 공유에 대한 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-147">For now, the Azure Storage account keys are used to provide authentication to the file share.</span></span> <span data-ttu-id="bc574-148">REST API 또는 클라이언트 라이브러리를 통해 공유 액세스 서명(SAS)을 사용하여 해결 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-148">We do offer a workaround using shared access signatures (SAS) via the REST API or the client libraries.</span></span> <span data-ttu-id="bc574-149">SAS를 사용하면 지정된 시간 간격 동안 유효한 특정 권한을 가진 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-149">Using SAS, you can generate tokens with specific permissions that are valid for a specified time interval.</span></span> <span data-ttu-id="bc574-150">예를 들어 만료 시간으로 10분이 지정된 파일에 대한 읽기 전용 액세스 권한이 있는 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-150">For example, you can generate a token with read-only access to a given file with 10 minutes expiry.</span></span> <span data-ttu-id="bc574-151">이 토큰이 유효한 동안 이 토큰을 소유한 사람은 해당 10분 동안 해당 파일에 대한 읽기 전용 액세스 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-151">Anyone who possesses this token while it is valid has read-only access to that file for those 10 minutes.</span></span>
   
    <span data-ttu-id="bc574-152">SAS는 REST API 또는 클라이언트 라이브러리를 통해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-152">SAS is only supported via the REST API or client libraries.</span></span> <span data-ttu-id="bc574-153">SMB 프로토콜을 통해 파일 공유를 탑재하면 SAS를 사용하여 해당 콘텐츠에 대한 액세스 권한을 위임할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-153">When you mount the file share via the SMB protocol, you can't use a SAS to delegate access to its contents.</span></span> 
    
* <span data-ttu-id="bc574-154">**Q. Azure File Storage에서 지원되는 데이터 규정 준수 정책이란?**</span><span class="sxs-lookup"><span data-stu-id="bc574-154">**Q. What are the data compliance policies supported for Azure File storage?**</span></span>

   <span data-ttu-id="bc574-155">Azure File Storage는 Azure Storage의 다른 저장소 서비스와 동일한 저장소 아키텍처에 기반하여 실행되며 동일한 데이터 규정 준수 정책을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-155">Azure File Storage runs on top of the same storage architecture as other storage services in Azure Storage and applies the same data compliance policies.</span></span> <span data-ttu-id="bc574-156">Azure Storage 데이터 규정 준수에 대한 자세한 내용은 [Microsoft Azure Data Protection 문서](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409)를 다운로드하여 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-156">More information on Azure Storage data compliance, you can download and refer to [Microsoft Azure Data Protection document](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).</span></span>

## <a name="on-premises-access"></a><span data-ttu-id="bc574-157">온-프레미스 액세스</span><span class="sxs-lookup"><span data-stu-id="bc574-157">On-Premises Access</span></span>

* <span data-ttu-id="bc574-158">**Q. Azure ExpressRoute를 사용하여 온-프레미스 VM에서 Azure File Storage에 연결해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-158">**Q.Do I have to use Azure ExpressRoute to connect to Azure File storage from an on-premises VM?**</span></span>
   
    <span data-ttu-id="bc574-159">아니요.</span><span class="sxs-lookup"><span data-stu-id="bc574-159">No.</span></span> <span data-ttu-id="bc574-160">ExpressRoute가 없더라도 인터넷 액세스를 위해 포트 445(TCP 아웃바운드)를 열어 놓기만 하면 온-프레미스에서 여전히 파일 공유에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-160">If you don't have ExpressRoute, you can still access the file share from on-premises as long as you have port 445 (TCP Outbound) open for Internet access.</span></span> <span data-ttu-id="bc574-161">그러나 원하는 경우 파일 저장소와 함께 ExpressRoute를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-161">However, you can use ExpressRoute with Azure File storage if you like.</span></span>

* <span data-ttu-id="bc574-162">**Q. 내 로컬 컴퓨터에서 Azure 파일 공유를 탑재하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-162">**Q. How can I mount an Azure File share on my local machine?**</span></span> 
    
    <span data-ttu-id="bc574-163">445 포트(TCP 아웃바운드)가 열려 있고 클라이언트(예: Windows 10 또는 Windows Server 2012 사용)에서 SMB 3.0 프로토콜을 지원하는 한 SMB 프로토콜을 통해 파일 공유를 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-163">You can mount the file share via the SMB protocol as long as port 445 (TCP Outbound) is open and your client supports the SMB 3.0 protocol (for example, you're using Windows 10 or Windows Server 2012).</span></span> <span data-ttu-id="bc574-164">로컬 ISP 공급자를 사용하여 포트의 차단을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-164">Please work with your local ISP provider to unblock the port.</span></span> <span data-ttu-id="bc574-165">중간에 [저장소 탐색기](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents)를 사용하여 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-165">In the interim, you can view your files using [Storage Explorer](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).</span></span>


## <a name="billing-and-pricing"></a><span data-ttu-id="bc574-166">가격 및 대금 청구</span><span class="sxs-lookup"><span data-stu-id="bc574-166">Billing and Pricing</span></span>
* <span data-ttu-id="bc574-167">**Q. Azure VM과 파일 공유 사이의 네트워크 트래픽은 구독에 청구되는 외부 대역폭으로 간주되나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-167">**Q. Does the network traffic between an Azure VM and a file share count as external bandwidth that is charged to the subscription?**</span></span>
   
    <span data-ttu-id="bc574-168">파일 공유와 VM이 동일한 Azure 지역에 있으면 이들 간의 트래픽은 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-168">If the file share and VM are in the same Azure region, the traffic between them is free.</span></span> <span data-ttu-id="bc574-169">서로 다른 지역에 있는 경우 이들 간의 트래픽은 외부 대역폭으로 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-169">If they are in different regions, the traffic between them will be charged as external bandwidth.</span></span>

## <a name="backup"></a><span data-ttu-id="bc574-170">백업</span><span class="sxs-lookup"><span data-stu-id="bc574-170">Backup</span></span>

* <span data-ttu-id="bc574-171">**Q. 내 Azure 파일 공유를 백업하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-171">**Q. How do I backup my Azure File Share?**</span></span>
    
    <span data-ttu-id="bc574-172">탑재된 파일 공유를 백업할 수 있는 AzCopy, RoboCopy 또는 타사 백업 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-172">You can use AzCopy, RoboCopy, or a 3rd party backup tool that can backup a mounted file share.</span></span> <span data-ttu-id="bc574-173">가까운 장래에 파일 공유의 스냅숏을 만들 수 있을 것으로 예상합니다. 이 기능을 사용하여 Azure 파일 공유를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-173">We expect to have the ability to take snapshots of File shares in the near future; you will be able to use this feature to backup your Azure File share.</span></span>

## <a name="performance"></a><span data-ttu-id="bc574-174">성능</span><span class="sxs-lookup"><span data-stu-id="bc574-174">Performance</span></span>

* <span data-ttu-id="bc574-175">**Q. Azure File Storage의 크기 제한은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-175">**Q. What are the scale limits of Azure File storage?**</span></span>
    <span data-ttu-id="bc574-176">Azure File Storage의 확장성 및 성능 목표에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc574-176">For information on scalability and performance targets of Azure File storage, see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).</span></span>

* <span data-ttu-id="bc574-177">**Q. Azure File Storage에 파일의 압축을 풀려고 하면 성능이 느려졌습니다. 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-177">**Q. My performance was slow when trying to unzip files into Azure File storage. What should I do?**</span></span>
    
    <span data-ttu-id="bc574-178">많은 파일을 Azure File Storage로 전송하려면 네트워크 전송을 위해 최적화된 도구인 AzCopy(Windows, Linux/Unix 용 미리 보기) 또는 Azure Powershell를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-178">To transfer large numbers of files into Azure File storage, we recommend that you use AzCopy(Windows, Preview for Linux/Unix) or Azure Powershell as these tools have been optimized for network transfer.</span></span>

* <span data-ttu-id="bc574-179">**Q. Azure File Storage의 성능 저하 문제를 해결하기 위해 어떤 패치가 릴리스되었나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-179">**Q. What patches has been released to fix slow-performance issue with Azure File storage?**</span></span>
    
    <span data-ttu-id="bc574-180">Windows 팀은 고객이 Windows 8.1 또는 Windows Server 2012 R2에서 Azure File Storage에 액세스할 때 발생하는 성능 저하 문제를 해결하기 위한 패치를 최근에 출시했습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-180">The Windows team recently released a patch to fix a slow performance issue when the customer accesses Azure File storage from Windows 8.1 or Windows Server 2012 R2.</span></span> <span data-ttu-id="bc574-181">자세한 내용은 관련된 KB 문서인 [Windows 8.1 또는 Server 2012 R2 Azure Files Storage에 액세스할 때 성능 저하](https://support.microsoft.com/kb/3114025)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="bc574-181">For more information, please check out the associated KB article, [Slow performance when you access Azure File storage from Windows 8.1 or Server 2012 R2](https://support.microsoft.com/kb/3114025).</span></span>

## <a name="features-and-interoperability-with-other-services"></a><span data-ttu-id="bc574-182">다른 서비스와의 기능 및 상호 운용성</span><span class="sxs-lookup"><span data-stu-id="bc574-182">Features and Interoperability with other services</span></span>
* <span data-ttu-id="bc574-183">**Q. 장애 조치 클러스터에 대한 "파일 공유 감시"는 Azure File Storage의 사용 사례 중 하나인가요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-183">**Q. Is a "File Share Witness" for a failover cluster one of the use cases for Azure File storage?**</span></span>
   
    <span data-ttu-id="bc574-184">현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-184">This is not currently supported.</span></span>

* <span data-ttu-id="bc574-185">**Q. REST API에 이름 바꾸기 작업이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-185">**Q. Is there a rename operation in the REST API?**</span></span>
   
    <span data-ttu-id="bc574-186">지금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-186">Not at this time.</span></span>

* <span data-ttu-id="bc574-187">**Q. 중첩된 공유, 즉 공유 아래에 공유를 가질 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-187">**Q. Can you have nested shares, in other words, a share under a share?**</span></span>
    
    <span data-ttu-id="bc574-188">아니요.</span><span class="sxs-lookup"><span data-stu-id="bc574-188">No.</span></span> <span data-ttu-id="bc574-189">파일 공유는 마운트할 수 있는 가상 드라이버이므로 포함된 공유는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-189">The file share is the virtual driver that you can mount, so nested shares are not supported.</span></span>

* <span data-ttu-id="bc574-190">**Q. IBM MQ에서 Azure File Storage를 사용하고 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="bc574-190">**Q. Using Azure File storage with IBM MQ**</span></span>
    
    <span data-ttu-id="bc574-191">IBM은 이 서비스로 Azure File Storage를 구성할 때 IBM MQ 고객에게 안내하는 문서를 발표했습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-191">IBM has released a document to guide IBM MQ customers when configuring Azure File storage with their service.</span></span> <span data-ttu-id="bc574-192">자세한 내용은 [Microsoft Azure 파일 서비스와 IBM MQ 다중 인스턴스 큐 관리자를 설치하는 방법](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc574-192">For more information, please check out [How to setup IBM MQ Multi instance queue manager with Microsoft Azure File Service](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="bc574-193">문제 해결</span><span class="sxs-lookup"><span data-stu-id="bc574-193">Troubleshooting</span></span>
* <span data-ttu-id="bc574-194">**Q. Azure File Storage 오류를 어떻게 해결하나요?**</span><span class="sxs-lookup"><span data-stu-id="bc574-194">**Q. How do I troubleshoot Azure File storage errors?**</span></span>
    
    <span data-ttu-id="bc574-195">종단 간 문제 해결 지침에 대해서는 [Azure File Storage 문제 해결 문서](storage-troubleshoot-file-connection-problems.md)를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-195">You can refer to [Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span> 


## <a name="see-also"></a><span data-ttu-id="bc574-196">참고 항목</span><span class="sxs-lookup"><span data-stu-id="bc574-196">See also</span></span>
<span data-ttu-id="bc574-197">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="bc574-197">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="bc574-198">개념 문서 및 비디오</span><span class="sxs-lookup"><span data-stu-id="bc574-198">Conceptual articles and videos</span></span>
* [<span data-ttu-id="bc574-199">Azure File Storage: 원활한 Windows 및 Linux용 클라우드 SMB 파일 시스템(영문)</span><span class="sxs-lookup"><span data-stu-id="bc574-199">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="bc574-200">Linux에서 Azure File Storage 사용 방법</span><span class="sxs-lookup"><span data-stu-id="bc574-200">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="bc574-201">파일 저장소용 도구 지원</span><span class="sxs-lookup"><span data-stu-id="bc574-201">Tooling support for File storage</span></span>
* [<span data-ttu-id="bc574-202">Azure 저장소와 함께 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="bc574-202">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="bc574-203">Microsoft Azure 저장소와 함께 AzCopy를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc574-203">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="bc574-204">Azure 저장소에서 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="bc574-204">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md)
* [<span data-ttu-id="bc574-205">Azure File Storage 문제 해결</span><span class="sxs-lookup"><span data-stu-id="bc574-205">Troubleshooting Azure File storage problems</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="blog-posts"></a><span data-ttu-id="bc574-206">블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="bc574-206">Blog posts</span></span>
* [<span data-ttu-id="bc574-207">Azure 파일 저장소 일반적으로 사용 가능(영문)</span><span class="sxs-lookup"><span data-stu-id="bc574-207">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="bc574-208">Azure File Storage 내부 구조(영문)</span><span class="sxs-lookup"><span data-stu-id="bc574-208">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="bc574-209">Microsoft Azure 파일 서비스 소개</span><span class="sxs-lookup"><span data-stu-id="bc574-209">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="bc574-210">Azure File Storage로 데이터 마이그레이션(영문)</span><span class="sxs-lookup"><span data-stu-id="bc574-210">Migrating data to Azure File storage</span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="bc574-211">참조</span><span class="sxs-lookup"><span data-stu-id="bc574-211">Reference</span></span>
* [<span data-ttu-id="bc574-212">Storage Client Library for .NET 참조</span><span class="sxs-lookup"><span data-stu-id="bc574-212">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="bc574-213">파일 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="bc574-213">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
