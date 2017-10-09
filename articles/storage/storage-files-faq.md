---
title: "Azure 파일 저장소에 대 한 질문과 aaaFrequently | Microsoft Docs"
description: "찾기 toofrequently Azure 파일 저장소에 대 한 질문과 대답을 제공 합니다."
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
ms.openlocfilehash: ecd685b3094f51e998bbf5dd0567a20732757015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a><span data-ttu-id="ecd95-103">Azure File Storage 보안에 대한 FAQ(질문과 대답)</span><span class="sxs-lookup"><span data-stu-id="ecd95-103">Frequently Asked Questions about Azure File storage</span></span>

## <a name="general"></a><span data-ttu-id="ecd95-104">일반</span><span class="sxs-lookup"><span data-stu-id="ecd95-104">General</span></span>
* <span data-ttu-id="ecd95-105">**Q. Azure File Storage란?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-105">**Q. What is Azure File storage?**</span></span>  
   
    <span data-ttu-id="ecd95-106">Azure File Storage는 Azure의 분산 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-106">Azure File storage is a distributed file system in Azure.</span></span> <span data-ttu-id="ecd95-107">지원 되는 Azure 가상 컴퓨터 또는 온-프레미스 컴퓨터에 있는 네이티브 공유로 사용자 toomount hello 저장소 수 있는 SMB 프로토콜 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-107">It provides an SMB protocol interface which allows users toomount hello storage as a native share on supported Azure Virtual Machine or on-premises machine.</span></span>

* <span data-ttu-id="ecd95-108">**Q. Azure File Storage가 유용한 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-108">**Q. Why is Azure File storage useful?**</span></span>  
   
    <span data-ttu-id="ecd95-109">Azure File Storage는 여러 VM 및 플랫폼 간에 공유 데이터 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-109">Azure File storage provides shared data access across multiple VMs and platforms.</span></span> <span data-ttu-id="ecd95-110">너무 참조[이유 Azure 파일 저장소는 유용](storage-files-introduction.md#why-azure-file-storage-is-useful)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-110">Refer too[Why Azure File storage is useful](storage-files-introduction.md#why-azure-file-storage-is-useful).</span></span>

* <span data-ttu-id="ecd95-111">**Q. Azure File, Azure Blob 및 Azure Disk는 언제 사용해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-111">**Q. When should I use Azure File vs Azure Blob vs Azure Disk ?**</span></span>  
   
    <span data-ttu-id="ecd95-112">Microsoft Azure hello 클라우드에서 toostore 및 액세스 데이터를 여러 가지 방법으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-112">Microsoft Azure provides several ways toostore and access data in hello cloud.</span></span>  
   
    <span data-ttu-id="ecd95-113">Azure 파일 저장소-SMB 인터페이스, 클라이언트 라이브러리 및 toostored 파일 어디에서 든 쉽게 액세스할 수 있도록 REST 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-113">Azure File storage - Provides an SMB interface, client libraries, and a REST interface that allows easy access from anywhere toostored files.</span></span>  
   
    <span data-ttu-id="ecd95-114">Azure Blob-클라이언트 라이브러리 및 구조화 되지 않은 데이터 toobe 저장 하 고 블록 blob에서 대규모로 액세스를 허용 하는 REST 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-114">Azure Blobs - Provides client libraries and a REST interface that allows unstructured data toobe stored and accessed at a massive scale in block blobs.</span></span>  
   
    <span data-ttu-id="ecd95-115">Azure 데이터 디스크-클라이언트 라이브러리 및 데이터 toobe 영구적으로 저장 하 고 연결된 된 가상 하드 디스크에서 액세스를 허용 하는 REST 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-115">Azure Data Disks - Provides client libraries and a REST interface that allows data toobe persistently stored and accessed from an attached virtual hard disk.</span></span>  
   
    <span data-ttu-id="ecd95-116">자세히 알아보세요 [결정 때 toouse Azure Blob, Azure 파일 또는 Azure 데이터 디스크](storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="ecd95-116">Learn more on [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](storage-decide-blobs-files-disks.md)</span></span>

* <span data-ttu-id="ecd95-117">**Q. Azure File Storage로 시작하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-117">**Q. How do I get started using Azure File storage?**</span></span>  
   
    <span data-ttu-id="ecd95-118">Azure 파일 공유를 만들어 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-118">You can start by creating an Azure file share.</span></span> <span data-ttu-id="ecd95-119">Azure 포털 "," hello Azure 저장소 PowerShell cmdlet "," hello Azure 저장소 클라이언트 라이브러리 "또는" hello Azure 저장소 REST API를 사용 하 여 Azure 파일 공유를 만들 수 있습니다. 이 자습서에서는 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-119">You can create Azure File shares using Azure Portal, hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>

    * [<span data-ttu-id="ecd95-120">Hello 포털을 사용 하 여 toocreate Azure 파일을 공유 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="ecd95-120">Learn how toocreate Azure File share using hello Portal</span></span>](storage-file-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [<span data-ttu-id="ecd95-121">Powershell을 사용 하 여 toocreate Azure 파일을 공유 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="ecd95-121">Learn how toocreate Azure File share using Powershell</span></span>](storage-file-how-to-create-file-share.md#create-file-share-through-powershell)
    * [<span data-ttu-id="ecd95-122">CLI를 사용 하 여 toocreate Azure 파일을 공유 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="ecd95-122">Learn how toocreate Azure File share using CLI</span></span>](storage-file-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* <span data-ttu-id="ecd95-123">**Q. Azure File Storage는 어떤 복제를 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-123">**Q. What replications are supported by Azure File storage?**</span></span>  
   
    <span data-ttu-id="ecd95-124">Azure File Storage는 현재 LRS 또는 GRS만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-124">Azure File storage only supports LRS or GRS right now.</span></span> <span data-ttu-id="ecd95-125">RA-GRS toosupport 계획 있지만 아직 타임 라인 tooshare 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-125">We plan toosupport RA-GRS but there is no timeline tooshare yet.</span></span>

## <a name="security-authentication-and-access-control"></a><span data-ttu-id="ecd95-126">보안, 인증 및 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="ecd95-126">Security, Authentication and Access Control</span></span>

* <span data-ttu-id="ecd95-127">**Q. Azure 파일 저장소의 다양 한 방법 tooaccess 파일 이란?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-127">**Q. What are different ways tooaccess files in Azure File storage?**</span></span>
    
    <span data-ttu-id="ecd95-128">SMB 3.0 프로토콜을 사용 하 여 로컬 컴퓨터의 hello 파일 공유를 탑재할 수 또는 사용 하 여 도구와 같은 [저장소 탐색기](http://storageexplorer.com/) 파일 공유의 tooaccess 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-128">You can mount hello file share on your local machine using SMB 3.0 protocol or use tools like [Storage Explorer](http://storageexplorer.com/) tooaccess files in your file share.</span></span> <span data-ttu-id="ecd95-129">응용 프로그램에서 저장소 클라이언트 라이브러리, REST Api 또는 Powershell tooaccess Azure 파일의 파일 공유를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-129">From your application, you can use storage client libraries, REST APIs or Powershell tooaccess your files in Azure File share.</span></span>

* <span data-ttu-id="ecd95-130">**Q. 웹 브라우저를 사용 하 여 액세스 tooa 특정 파일을 제공 하려면 어떻게 해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-130">**Q. How can I provide access tooa specific file using a web browser?**</span></span>
    
    <span data-ttu-id="ecd95-131">SAS를 사용하면 지정된 시간 간격 동안 유효한 특정 권한을 가진 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-131">Using SAS, you can generate tokens with specific permissions that are valid for a specified time interval.</span></span> <span data-ttu-id="ecd95-132">예를 들어 특정 시간 동안에 대 한 읽기 전용 액세스 tooa 특정 파일이 있는 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-132">For example, you can generate a token with read-only access tooa particular file for a specific period of time.</span></span> <span data-ttu-id="ecd95-133">가 유효한 동안 모든 웹 브라우저에서 직접 hello 파일에 액세스할 수 있습니다이 url을 소유한 모든 사용자.</span><span class="sxs-lookup"><span data-stu-id="ecd95-133">Anyone who possesses this url can access hello file directly from any web browser while it is valid.</span></span> <span data-ttu-id="ecd95-134">저장소 탐색기 같은 UI에서 SAS 키를 쉽게 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-134">SAS keys can be easily generated from UI like Storage Explorer.</span></span>

* <span data-ttu-id="ecd95-135">**Q. Hello 공유 내 폴더에 읽기 전용 이거나 쓰기 전용 권한을 가능한 toospecify 입니까?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-135">**Q. Is it possible toospecify read-only or write-only permissions on folders within hello share?**</span></span>
    
    <span data-ttu-id="ecd95-136">SMB 통해 hello 파일 공유를 탑재 하는 경우 사용 권한 보다 이러한 제어 수준은 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-136">You don't have this level of control over permissions if you mount hello file share via SMB.</span></span> <span data-ttu-id="ecd95-137">그러나 hello REST API를 통해 공유 액세스 서명 (SAS) 또는 클라이언트 라이브러리를 만들어이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-137">However, you can achieve this by creating a shared access signature (SAS) via hello REST API or client libraries.</span></span>  

* <span data-ttu-id="ecd95-138">**Q. Azure File Storage에 대한 서버 쪽 암호화를 사용하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-138">**Q. How can I enable Server Side encryption for Azure File storage?**</span></span>

    <span data-ttu-id="ecd95-139">Azure File Storage에 대한 [서버 쪽 암호화](storage-service-encryption.md)는 일반적으로 모든 지역과 공용 및 국가별 클라우드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-139">[Server Side Encryption](storage-service-encryption.md) for Azure File storage is generally available in all regions and public and national clouds.</span></span> <span data-ttu-id="ecd95-140">[Azure Portal](https://portal.azure.com/), [Microsoft Azure Storage 리소스 공급자 API](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) 또는 [Azure CLI](storage-azure-cli.md)를 사용하여 Azure File Storage에 대한 SSE를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-140">You can enable SSE for Azure File storage using [Azure portal](https://portal.azure.com/),[Microsoft Azure Storage Resource Provider API](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) or [Azure CLI](storage-azure-cli.md).</span></span>
    
    <span data-ttu-id="ecd95-141">Azure 파일 저장소에 SSE을 활성화 한 다음 해당 저장소 계정 toohello 파일 저장소로 작성 된 새 데이터도 자동으로 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-141">After enabling SSE on Azure File storage, any new data written toohello file storage in that storage account will be automatically encrypted.</span></span> <span data-ttu-id="ecd95-142">이 기능은 tooexisting 또는 새 공유는 기존 또는 새 저장소 계정에 작성 된 모든 새 데이터에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-142">This feature is available for all new data written tooexisting or new shares in an existing or new storage account.</span></span> <span data-ttu-id="ecd95-143">이 기능을 사용하는 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-143">There is no additional charge for enabling this feature.</span></span> <span data-ttu-id="ecd95-144">자세히 알아보세요 [어떻게 Azure 파일 저장소에 SSE tooenable](storage-service-encryption.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-144">Learn more on [how tooenable SSE on Azure File storage](storage-service-encryption.md).</span></span>

* <span data-ttu-id="ecd95-145">**Q. Azure File Storage에서 Active Directory 기반 인증을 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-145">**Q. Is Active Directory-based authentication supported by Azure File storage?**</span></span>
   
    <span data-ttu-id="ecd95-146">우리는 현재 AD 기반 인증 또는 ACL을 지원하지 않지만 우리의 기능 요청 목록에 해당 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-146">We currently do not support AD-based authentication or ACLs, but do have it in our list of feature requests.</span></span> <span data-ttu-id="ecd95-147">지금은 hello Azure 저장소 계정 키 사용된 tooprovide 인증 toohello 파일 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-147">For now, hello Azure Storage account keys are used tooprovide authentication toohello file share.</span></span> <span data-ttu-id="ecd95-148">공유 액세스 서명 (SAS)를 사용 하 여 hello REST API 또는 hello 클라이언트 라이브러리를 통해 해결 방법이 제공지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-148">We do offer a workaround using shared access signatures (SAS) via hello REST API or hello client libraries.</span></span> <span data-ttu-id="ecd95-149">SAS를 사용하면 지정된 시간 간격 동안 유효한 특정 권한을 가진 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-149">Using SAS, you can generate tokens with specific permissions that are valid for a specified time interval.</span></span> <span data-ttu-id="ecd95-150">예를 들어 10 분 동안 만료 된 파일을 지정 하는 읽기 전용 액세스 tooa와 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-150">For example, you can generate a token with read-only access tooa given file with 10 minutes expiry.</span></span> <span data-ttu-id="ecd95-151">가 유효한 동안이 토큰을 소유한 모든 사용자에 해당 10 분에 대 한 읽기 전용 액세스 toothat 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-151">Anyone who possesses this token while it is valid has read-only access toothat file for those 10 minutes.</span></span>
   
    <span data-ttu-id="ecd95-152">SAS는 hello REST API 또는 클라이언트 라이브러리를 통해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-152">SAS is only supported via hello REST API or client libraries.</span></span> <span data-ttu-id="ecd95-153">Hello SMB 프로토콜을 통해 hello 파일 공유를 탑재할 때 SAS toodelegate 액세스 tooits 콘텐츠를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-153">When you mount hello file share via hello SMB protocol, you can't use a SAS toodelegate access tooits contents.</span></span> 
    
* <span data-ttu-id="ecd95-154">**Q. Azure 파일 저장소에 대 한 지원 hello 데이터 규정 준수 정책 이란?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-154">**Q. What are hello data compliance policies supported for Azure File storage?**</span></span>

   <span data-ttu-id="ecd95-155">Azure 파일 저장소 실행의 맨 위에 다른 저장소에서 Azure 저장소 서비스 및 hello 적용 동일한 저장소 아키텍처를 hello 동일한 데이터 규정 준수 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-155">Azure File Storage runs on top of hello same storage architecture as other storage services in Azure Storage and applies hello same data compliance policies.</span></span> <span data-ttu-id="ecd95-156">Azure 저장소 데이터 규정 준수에 대 한 자세한 내용은 다운로드 하 고 수 너무 참조[Microsoft Azure 데이터 보호 문서](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-156">More information on Azure Storage data compliance, you can download and refer too[Microsoft Azure Data Protection document](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).</span></span>

## <a name="on-premises-access"></a><span data-ttu-id="ecd95-157">온-프레미스 액세스</span><span class="sxs-lookup"><span data-stu-id="ecd95-157">On-Premises Access</span></span>

* <span data-ttu-id="ecd95-158">**Q.Do toouse Azure express 경로 tooconnect tooAzure 파일 저장소는 온-프레미스 VM에서 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-158">**Q.Do I have toouse Azure ExpressRoute tooconnect tooAzure File storage from an on-premises VM?**</span></span>
   
    <span data-ttu-id="ecd95-159">아니요.</span><span class="sxs-lookup"><span data-stu-id="ecd95-159">No.</span></span> <span data-ttu-id="ecd95-160">Express 경로 설정 하지 않은 경우 계속 액세스할 수 있습니다 hello 파일 공유 온-프레미스에서 포트 445 (TCP 아웃 바운드) 인터넷 액세스에 대 한 열기를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-160">If you don't have ExpressRoute, you can still access hello file share from on-premises as long as you have port 445 (TCP Outbound) open for Internet access.</span></span> <span data-ttu-id="ecd95-161">그러나 원하는 경우 파일 저장소와 함께 ExpressRoute를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-161">However, you can use ExpressRoute with Azure File storage if you like.</span></span>

* <span data-ttu-id="ecd95-162">**Q. 내 로컬 컴퓨터에서 Azure 파일 공유를 탑재하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-162">**Q. How can I mount an Azure File share on my local machine?**</span></span> 
    
    <span data-ttu-id="ecd95-163">포트 445 (TCP 아웃 바운드)이 열려 있고 클라이언트 hello SMB 3.0 프로토콜을 지 원하는 hello SMB 프로토콜을 통해 hello 파일 공유를 탑재할 수 있습니다 (예를 들어 사용할 Windows 10 또는 Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="ecd95-163">You can mount hello file share via hello SMB protocol as long as port 445 (TCP Outbound) is open and your client supports hello SMB 3.0 protocol (for example, you're using Windows 10 or Windows Server 2012).</span></span> <span data-ttu-id="ecd95-164">로컬 ISP 공급자 toounblock hello 포트를 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ecd95-164">Please work with your local ISP provider toounblock hello port.</span></span> <span data-ttu-id="ecd95-165">중간 hello에서 사용 하 여 파일을 볼 수 있습니다 [저장소 탐색기](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-165">In hello interim, you can view your files using [Storage Explorer](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).</span></span>


## <a name="billing-and-pricing"></a><span data-ttu-id="ecd95-166">가격 및 대금 청구</span><span class="sxs-lookup"><span data-stu-id="ecd95-166">Billing and Pricing</span></span>
* <span data-ttu-id="ecd95-167">**Q. 가 toohello 구독 청구 되는 외부 대역폭으로 파일 공유 수와 Azure VM 간의 네트워크 트래픽이 hello?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-167">**Q. Does hello network traffic between an Azure VM and a file share count as external bandwidth that is charged toohello subscription?**</span></span>
   
    <span data-ttu-id="ecd95-168">Hello 파일 공유 및 VM에 있으면 hello 같은 Azure 지역 hello 서로 트래픽이 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-168">If hello file share and VM are in hello same Azure region, hello traffic between them is free.</span></span> <span data-ttu-id="ecd95-169">다른 지역에 있으면 둘 사이의 hello 트래픽 외부 대역폭으로 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-169">If they are in different regions, hello traffic between them will be charged as external bandwidth.</span></span>

## <a name="backup"></a><span data-ttu-id="ecd95-170">백업</span><span class="sxs-lookup"><span data-stu-id="ecd95-170">Backup</span></span>

* <span data-ttu-id="ecd95-171">**Q. 내 Azure 파일 공유를 백업하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-171">**Q. How do I backup my Azure File Share?**</span></span>
    
    <span data-ttu-id="ecd95-172">탑재된 파일 공유를 백업할 수 있는 AzCopy, RoboCopy 또는 타사 백업 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-172">You can use AzCopy, RoboCopy, or a 3rd party backup tool that can backup a mounted file share.</span></span> <span data-ttu-id="ecd95-173">Hello 가까운 미래;에서 파일 공유의 toohave hello 기능 tootake 스냅숏을 예상합니다 수 toouse 됩니다.이 기능은 toobackup Azure 파일을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-173">We expect toohave hello ability tootake snapshots of File shares in hello near future; you will be able toouse this feature toobackup your Azure File share.</span></span>

## <a name="performance"></a><span data-ttu-id="ecd95-174">성능</span><span class="sxs-lookup"><span data-stu-id="ecd95-174">Performance</span></span>

* <span data-ttu-id="ecd95-175">**Q. Azure 파일 저장소의 규모 제한을 hello 이란?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-175">**Q. What are hello scale limits of Azure File storage?**</span></span>
    <span data-ttu-id="ecd95-176">Azure File Storage의 확장성 및 성능 목표에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecd95-176">For information on scalability and performance targets of Azure File storage, see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).</span></span>

* <span data-ttu-id="ecd95-177">**Q. Azure 파일 저장소로 toounzip 파일을 동안 내 성능 느린 했습니다. 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-177">**Q. My performance was slow when trying toounzip files into Azure File storage. What should I do?**</span></span>
    
    <span data-ttu-id="ecd95-178">많은 수의 Azure 파일 저장소에 파일 tootransfer, 이러한 도구에 대 한 네트워크 전송을 최적화 하는 대로 AzCopy (Windows, Linux/Unix에 대 한 미리 보기) 또는 Azure Powershell을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-178">tootransfer large numbers of files into Azure File storage, we recommend that you use AzCopy(Windows, Preview for Linux/Unix) or Azure Powershell as these tools have been optimized for network transfer.</span></span>

* <span data-ttu-id="ecd95-179">**Q. 되었습니다 패치 toofix 속도가 느린 성능 문제를 Azure 파일 저장소?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-179">**Q. What patches has been released toofix slow-performance issue with Azure File storage?**</span></span>
    
    <span data-ttu-id="ecd95-180">Windows 팀 hello hello 고객 Windows 8.1 또는 Windows Server 2012 r 2에서 Azure 파일 저장소에 액세스 하는 경우 패치 toofix를 성능 저하 문제 최근에 릴리스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-180">hello Windows team recently released a patch toofix a slow performance issue when hello customer accesses Azure File storage from Windows 8.1 or Windows Server 2012 R2.</span></span> <span data-ttu-id="ecd95-181">자세한 내용은 하십시오 체크 아웃 hello 관련 된 기술 자료 문서 [Windows 8.1 또는 Server 2012 r 2에서 Azure 파일 저장소에 액세스할 때 성능이 저하](https://support.microsoft.com/kb/3114025)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-181">For more information, please check out hello associated KB article, [Slow performance when you access Azure File storage from Windows 8.1 or Server 2012 R2](https://support.microsoft.com/kb/3114025).</span></span>

## <a name="features-and-interoperability-with-other-services"></a><span data-ttu-id="ecd95-182">다른 서비스와의 기능 및 상호 운용성</span><span class="sxs-lookup"><span data-stu-id="ecd95-182">Features and Interoperability with other services</span></span>
* <span data-ttu-id="ecd95-183">**Q. Azure 파일 저장소에 대 한 "파일 공유 감시" hello 중 하나로 장애 조치 클러스터에 대 한 사용 사례는?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-183">**Q. Is a "File Share Witness" for a failover cluster one of hello use cases for Azure File storage?**</span></span>
   
    <span data-ttu-id="ecd95-184">현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-184">This is not currently supported.</span></span>

* <span data-ttu-id="ecd95-185">**Q. Hello REST API에는 이름 바꾸기 작업 거기?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-185">**Q. Is there a rename operation in hello REST API?**</span></span>
   
    <span data-ttu-id="ecd95-186">지금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-186">Not at this time.</span></span>

* <span data-ttu-id="ecd95-187">**Q. 중첩된 공유, 즉 공유 아래에 공유를 가질 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-187">**Q. Can you have nested shares, in other words, a share under a share?**</span></span>
    
    <span data-ttu-id="ecd95-188">아니요.</span><span class="sxs-lookup"><span data-stu-id="ecd95-188">No.</span></span> <span data-ttu-id="ecd95-189">hello 파일 공유를 탑재 하는 가상 드라이버 hello 이므로 중첩된 공유는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-189">hello file share is hello virtual driver that you can mount, so nested shares are not supported.</span></span>

* <span data-ttu-id="ecd95-190">**Q. IBM MQ에서 Azure File Storage를 사용하고 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="ecd95-190">**Q. Using Azure File storage with IBM MQ**</span></span>
    
    <span data-ttu-id="ecd95-191">해당 서비스와 Azure 파일 저장소를 구성할 때 IBM 문서 tooguide IBM MQ 고객을 릴리스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-191">IBM has released a document tooguide IBM MQ customers when configuring Azure File storage with their service.</span></span> <span data-ttu-id="ecd95-192">자세한 내용은 확인 하세요 [어떻게 toosetup IBM MQ 다중 인스턴스 큐 관리자와 Microsoft Azure 파일 서비스](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-192">For more information, please check out [How toosetup IBM MQ Multi instance queue manager with Microsoft Azure File Service](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="ecd95-193">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ecd95-193">Troubleshooting</span></span>
* <span data-ttu-id="ecd95-194">**Q. Azure File Storage 오류를 어떻게 해결하나요?**</span><span class="sxs-lookup"><span data-stu-id="ecd95-194">**Q. How do I troubleshoot Azure File storage errors?**</span></span>
    
    <span data-ttu-id="ecd95-195">너무 참조할 수[Azure 파일 저장소 문제 해결 문서](storage-troubleshoot-file-connection-problems.md) 종단 간 문제 해결 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-195">You can refer too[Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span> 


## <a name="see-also"></a><span data-ttu-id="ecd95-196">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ecd95-196">See also</span></span>
<span data-ttu-id="ecd95-197">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd95-197">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="ecd95-198">개념 문서 및 비디오</span><span class="sxs-lookup"><span data-stu-id="ecd95-198">Conceptual articles and videos</span></span>
* [<span data-ttu-id="ecd95-199">Azure File Storage: 원활한 Windows 및 Linux용 클라우드 SMB 파일 시스템(영문)</span><span class="sxs-lookup"><span data-stu-id="ecd95-199">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="ecd95-200">어떻게 toouse Linux로 Azure 파일 저장소</span><span class="sxs-lookup"><span data-stu-id="ecd95-200">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="ecd95-201">파일 저장소용 도구 지원</span><span class="sxs-lookup"><span data-stu-id="ecd95-201">Tooling support for File storage</span></span>
* [<span data-ttu-id="ecd95-202">Azure 저장소와 함께 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="ecd95-202">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="ecd95-203">어떻게 toouse AzCopy Microsoft Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="ecd95-203">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="ecd95-204">Hello Azure CLI를 사용 하 여 Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="ecd95-204">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md)
* [<span data-ttu-id="ecd95-205">Azure File Storage 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ecd95-205">Troubleshooting Azure File storage problems</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="blog-posts"></a><span data-ttu-id="ecd95-206">블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="ecd95-206">Blog posts</span></span>
* [<span data-ttu-id="ecd95-207">Azure 파일 저장소 일반적으로 사용 가능(영문)</span><span class="sxs-lookup"><span data-stu-id="ecd95-207">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="ecd95-208">Azure File Storage 내부 구조(영문)</span><span class="sxs-lookup"><span data-stu-id="ecd95-208">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="ecd95-209">Microsoft Azure 파일 서비스 소개</span><span class="sxs-lookup"><span data-stu-id="ecd95-209">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="ecd95-210">마이그레이션 데이터 tooAzure 파일 저장소</span><span class="sxs-lookup"><span data-stu-id="ecd95-210">Migrating data tooAzure File storage</span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="ecd95-211">참조</span><span class="sxs-lookup"><span data-stu-id="ecd95-211">Reference</span></span>
* [<span data-ttu-id="ecd95-212">Storage Client Library for .NET 참조</span><span class="sxs-lookup"><span data-stu-id="ecd95-212">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="ecd95-213">파일 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="ecd95-213">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
