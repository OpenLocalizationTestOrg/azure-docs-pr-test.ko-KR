---
title: "미사용 데이터에 대한 Azure Storage Service Encryption | Microsoft Docs"
description: "Azure 저장소 서비스 암호화 기능을 사용하여 데이터를 저장할 때 서비스 쪽에서 Azure Blob 저장소를 암호화하고 데이터를 검색할 때 암호 해독합니다."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: robinsh
ms.openlocfilehash: bac7b3292f21aa97d02a18dd58f79a4f10485b7d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-service-encryption-for-data-at-rest"></a><span data-ttu-id="0366d-103">휴지 상태의 데이터에 대한 Azure 저장소 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="0366d-103">Azure Storage Service Encryption for Data at Rest</span></span>
<span data-ttu-id="0366d-104">미사용 데이터에 대한 Azure 저장소 서비스 암호화(SSE)를 사용하면 조직의 보안 및 규정 준수 약정에 맞게 데이터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-104">Azure Storage Service Encryption (SSE) for Data at Rest helps you protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="0366d-105">이 기능을 통해 Azure 저장소는 저장소를 유지하기 전에 데이터를 자동으로 암호화하고 검색하기 전에 암호를 해독합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-105">With this feature, Azure Storage automatically encrypts your data prior to persisting to storage and decrypts prior to retrieval.</span></span> <span data-ttu-id="0366d-106">암호화, 암호 해독 및 키 관리는 사용자에게 완전히 투명하게 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-106">The encryption, decryption, and key management are totally transparent to users.</span></span>

<span data-ttu-id="0366d-107">다음 섹션에서는 저장소 서비스 암호화 기능, 지원되는 시나리오 및 사용자 환경을 사용하는 방법에 대한 자세한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-107">The following sections provide detailed guidance on how to use the Storage Service Encryption features as well as the supported scenarios and user experiences.</span></span>

## <a name="overview"></a><span data-ttu-id="0366d-108">개요</span><span class="sxs-lookup"><span data-stu-id="0366d-108">Overview</span></span>
<span data-ttu-id="0366d-109">Azure 저장소는 여러 개발자가 보안 응용 프로그램을 함께 빌드할 수 있도록 하는 포괄적인 보안 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-109">Azure Storage provides a comprehensive set of security capabilities which together enable developers to build secure applications.</span></span> <span data-ttu-id="0366d-110">[클라이언트 쪽 암호화](../storage-client-side-encryption.md), HTTP 또는 SMB 3.0을 사용하여 응용 프로그램과 Azure 간에 전송 중인 데이터의 보안을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-110">Data can be secured in transit between an application and Azure by using [Client-Side Encryption](../storage-client-side-encryption.md), HTTPs, or SMB 3.0.</span></span> <span data-ttu-id="0366d-111">저장소 서비스 암호화는 휴지 상태의 암호화를 제공하며 암호화, 암호 해독, 키 관리를 완전히 투명한 방식으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-111">Storage Service Encryption provides encryption at rest, handling encryption, decryption, and key management in a totally transparent fashion.</span></span> <span data-ttu-id="0366d-112">모든 데이터는 가장 강력한 블록 암호화 중 하나인 256비트 [AES 암호화](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-112">All data is encrypted using 256-bit [AES encryption](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), one of the strongest block ciphers available.</span></span>

<span data-ttu-id="0366d-113">SSE는 데이터를 Azure Storage에 기록할 때 데이터를 암호화하는 방식으로 작동하며 Azure Blob Storage 및 File Storage에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-113">SSE works by encrypting the data when it is written to Azure Storage, and can be used for Azure Blob Storage and File Storage.</span></span> <span data-ttu-id="0366d-114">다음에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-114">It works for the following:</span></span>

* <span data-ttu-id="0366d-115">표준 저장소: Blob에 대한 범용 저장소 계정과 File Storage 및 Blob Storage 계정</span><span class="sxs-lookup"><span data-stu-id="0366d-115">Standard Storage: General purpose storage accounts for Blobs and File storage and Blob storage accounts</span></span>
* <span data-ttu-id="0366d-116">Premium Storage</span><span class="sxs-lookup"><span data-stu-id="0366d-116">Premium storage</span></span> 
* <span data-ttu-id="0366d-117">모든 중복 수준(LRS, ZRS, GRS, RA-GRS)</span><span class="sxs-lookup"><span data-stu-id="0366d-117">All redundancy levels (LRS, ZRS, GRS, RA-GRS)</span></span>
* <span data-ttu-id="0366d-118">Azure Resource Manager 저장소 계정(클래식 아님)</span><span class="sxs-lookup"><span data-stu-id="0366d-118">Azure Resource Manager storage accounts (but not classic)</span></span> 
* <span data-ttu-id="0366d-119">모든 지역</span><span class="sxs-lookup"><span data-stu-id="0366d-119">All regions.</span></span>

<span data-ttu-id="0366d-120">자세히 알아보려면 FAQ를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0366d-120">To learn more, please refer to the FAQ.</span></span>

<span data-ttu-id="0366d-121">저장소 계정에 대한 저장소 서비스 암호화를 사용하거나 사용하지 않도록 설정하려면 [Azure Portal](https://portal.azure.com) 에 로그인한 후 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-121">To enable or disable Storage Service Encryption for a storage account, log into the [Azure portal](https://portal.azure.com) and select a storage account.</span></span> <span data-ttu-id="0366d-122">설정 블레이드에서 이 스크린샷에 표시된 것처럼 Blob 서비스 섹션을 찾은 후 암호화를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-122">On the Settings blade, look for the Blob Service section as shown in this screenshot and click Encryption.</span></span>

<span data-ttu-id="0366d-123">![암호화 옵션을 보여 주는 포털 스크린샷](./media/storage-service-encryption/image1.png)
</span><span class="sxs-lookup"><span data-stu-id="0366d-123">![Portal Screenshot showing Encryption option](./media/storage-service-encryption/image1.png)
</span></span><br/><span data-ttu-id="0366d-124">*그림 1: Blob Service에 SSE 사용(1단계)*</span><span class="sxs-lookup"><span data-stu-id="0366d-124">*Figure 1: Enable SSE for Blob Service (Step1)*</span></span>

<span data-ttu-id="0366d-125">![암호화 옵션을 보여 주는 포털 스크린샷](./media/storage-service-encryption/image3.png)
</span><span class="sxs-lookup"><span data-stu-id="0366d-125">![Portal Screenshot showing Encryption option](./media/storage-service-encryption/image3.png)
</span></span><br/><span data-ttu-id="0366d-126">*그림 2: 파일 서비스에 SSE 사용(1단계)*</span><span class="sxs-lookup"><span data-stu-id="0366d-126">*Figure 2: Enable SSE for File Service (Step1)*</span></span>

<span data-ttu-id="0366d-127">암호화 설정을 클릭하면 저장소 서비스 암호화를 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-127">After you click the Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

<span data-ttu-id="0366d-128">![암호화 속성을 보여 주는 포털 스크린샷](./media/storage-service-encryption/image2.png)
</span><span class="sxs-lookup"><span data-stu-id="0366d-128">![Portal Screenshot showing Encryption properties](./media/storage-service-encryption/image2.png)
</span></span><br/><span data-ttu-id="0366d-129">*그림 3: Blob 및 파일 서비스에 SSE 사용(2단계)*</span><span class="sxs-lookup"><span data-stu-id="0366d-129">*Figure 3: Enable SSE for Blob and File Service (Step2)*</span></span>

## <a name="encryption-scenarios"></a><span data-ttu-id="0366d-130">암호화 시나리오</span><span class="sxs-lookup"><span data-stu-id="0366d-130">Encryption Scenarios</span></span>
<span data-ttu-id="0366d-131">저장소 계정 수준에서 저장소 서비스 암호화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-131">Storage Service Encryption can be enabled at a storage account level.</span></span> <span data-ttu-id="0366d-132">사용하도록 설정하면 고객이 암호화할 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-132">Once enabled, customers will choose which services to encrypt.</span></span> <span data-ttu-id="0366d-133">다음과 같은 고객 시나리오가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-133">It supports the following customer scenarios:</span></span>

* <span data-ttu-id="0366d-134">리소스 관리자 계정의 Blob Storage 및 File Storage 암호화</span><span class="sxs-lookup"><span data-stu-id="0366d-134">Encryption of Blob Storage and File Storage in Resource Manager accounts.</span></span>
* <span data-ttu-id="0366d-135">리소스 관리자 저장소 계정으로 마이그레이션된 후 클래식 저장소 계정의 Blob 및 파일 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="0366d-135">Encryption of Blob and File Service in classic storage accounts once migrated to Resource Manager storage accounts.</span></span>

<span data-ttu-id="0366d-136">SSE에는 다음 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-136">SSE has the following limitations:</span></span>

* <span data-ttu-id="0366d-137">클래식 저장소 계정의 암호화는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-137">Encryption of classic storage accounts is not supported.</span></span>
* <span data-ttu-id="0366d-138">기존 데이터 - SSE만 암호화가 사용된 후 새로 만든 데이터를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-138">Existing Data - SSE only encrypts newly created data after the encryption is enabled.</span></span> <span data-ttu-id="0366d-139">예를 들어 새 Resource Manager 저장소 계정을 만들지만 암호화를 켜지 않는 경우 Blob 또는 보관된 VHD를 해당 저장소 계정으로 업로드한 후 SSE를 켜면 해당 Blob가 재작성되거나 복사되지 않은 경우 Blob가 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-139">If for example you create a new Resource Manager storage account but don't turn on encryption, and then you upload blobs or archived VHDs to that storage account and then turn on SSE, those blobs will not be encrypted unless they are rewritten or copied.</span></span>
* <span data-ttu-id="0366d-140">마켓플레이스 지원 - [Azure 포털](https://portal.azure.com), PowerShell 및 Azure CLI를 사용하여 마켓플레이스에서 만든 VM의 암호화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-140">Marketplace Support - Enable encryption of VMs created from the Marketplace using the [Azure portal](https://portal.azure.com), PowerShell, and Azure CLI.</span></span> <span data-ttu-id="0366d-141">VHD 기본 이미지는 암호화되지 않은 상태로 유지되지만 VM이 작동된 후 작성된 내용은 모두 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-141">The VHD base image will remain unencrypted; however, any writes done after the VM has spun up will be encrypted.</span></span>
* <span data-ttu-id="0366d-142">테이블 및 큐 데이터는 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-142">Table and Queues data will not be encrypted.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0366d-143">시작하기</span><span class="sxs-lookup"><span data-stu-id="0366d-143">Getting Started</span></span>
### <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a><span data-ttu-id="0366d-144">1단계: [새 저장소 계정 만들기](../storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="0366d-144">Step 1: [Create a new storage account](../storage-create-storage-account.md).</span></span>
### <a name="step-2-enable-encryption"></a><span data-ttu-id="0366d-145">2단계: 암호화 사용.</span><span class="sxs-lookup"><span data-stu-id="0366d-145">Step 2: Enable encryption.</span></span>
<span data-ttu-id="0366d-146">[Azure 포털](https://portal.azure.com)을 사용하여 암호화를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-146">You can enable encryption using the [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="0366d-147">저장소 계정에 대해 저장소 서비스 암호화를 프로그래밍 방식으로 사용 또는 사용하지 않으려면 [Azure Storage Resource Provider REST API](https://msdn.microsoft.com/library/azure/mt163683.aspx), [.NET용 Storage Resource Provider 클라이언트 라이브러리](https://msdn.microsoft.com/library/azure/mt131037.aspx), [Azure PowerShell](/powershell/azureps-cmdlets-docs) 또는 [Azure CLI](../storage-azure-cli.md)를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-147">If you want to programmatically enable or disable the Storage Service Encryption on a storage account, you can use the [Azure Storage Resource Provider REST API](https://msdn.microsoft.com/library/azure/mt163683.aspx), the [Storage Resource Provider Client Library for .NET](https://msdn.microsoft.com/library/azure/mt131037.aspx), [Azure PowerShell](/powershell/azureps-cmdlets-docs), or the [Azure CLI](../storage-azure-cli.md).</span></span>
> 
> 

### <a name="step-3-copy-data-to-storage-account"></a><span data-ttu-id="0366d-148">3단계: 저장소 계정에 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="0366d-148">Step 3: Copy data to storage account</span></span>
<span data-ttu-id="0366d-149">Blob service에 SSE를 사용하는 경우 해당 저장소 계정에 기록된 모든 Blob은 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-149">If you enable SSE for the Blob service, any blobs written to that storage account will be encrypted.</span></span> <span data-ttu-id="0366d-150">저장소 계정에 이미 있는 모든 Blob는 다시 작성할 때까지 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-150">Any blobs already located in that storage account will not be encrypted until they are rewritten.</span></span> <span data-ttu-id="0366d-151">한 저장소 계정에서 SSE 암호화된 다른 계정으로 데이터를 복사하거나 SSE를 사용하도록 설정하고 Blob를 한 컨테이너에서 다른 컨테이너로 복사하여 이전 데이터가 암호화되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-151">You can copy the data from one storage account to one with SSE encrypted, or even enable SSE and copy the blobs from one container to another to sure that previous data is encrypted.</span></span> <span data-ttu-id="0366d-152">이렇게 하려면 다음 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-152">You can use any of the following tools to accomplish this.</span></span> <span data-ttu-id="0366d-153">이는 File Storage에도 동일한 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-153">This is the same behavior for File Storage as well.</span></span>

#### <a name="using-azcopy"></a><span data-ttu-id="0366d-154">AzCopy 사용</span><span class="sxs-lookup"><span data-stu-id="0366d-154">Using AzCopy</span></span>
<span data-ttu-id="0366d-155">AzCopy는 간단한 명령과 최적의 성능으로 데이터를 Microsoft Azure Blob, 파일 및 테이블 저장소에(로부터) 복사하도록 디자인된 Windows 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-155">AzCopy is a Windows command-line utility designed for copying data to and from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="0366d-156">한 저장소 계정에서 SSE가 설정된 다른 계정으로 Blob 또는 파일을 복사하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-156">You can use this to copy your blobs or files from one storage account to another one that has SSE enabled.</span></span> 

<span data-ttu-id="0366d-157">자세한 내용은 [AzCopy 명령줄 유틸리티로 데이터 전송](storage-use-azcopy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0366d-157">To learn more, please visit [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

#### <a name="using-smb"></a><span data-ttu-id="0366d-158">SMB 사용</span><span class="sxs-lookup"><span data-stu-id="0366d-158">Using SMB</span></span>
<span data-ttu-id="0366d-159">Azure 파일 저장소는 표준 SMB 프로토콜을 사용하여 클라우드에서 파일 공유를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-159">Azure File storage offers file shares in the cloud using the standard SMB protocol.</span></span> <span data-ttu-id="0366d-160">온-프레미스 또는 Azure의 클라이언트에서 파일 공유를 마운트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-160">You can mount a file share from a client on premises or in Azure.</span></span> <span data-ttu-id="0366d-161">마운트되면 Azure 파일 공유에 파일을 복사하는 데 Robocopy와 같은 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-161">Once mounted, tools such as Robocopy can be used to copy files over to Azure File shares.</span></span> <span data-ttu-id="0366d-162">자세한 내용은 [Windows에서 Azure 파일 공유를 마운트하는 방법](../files/storage-how-to-use-files-windows.md) 및 [Linux에서 Azure 파일 공유를 마운트하는 방법](../storage-how-to-use-files-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0366d-162">For more information, see [how to mount Azure File Share on Windows](../files/storage-how-to-use-files-windows.md) and [how to mount Azure File share on Linux](../storage-how-to-use-files-linux.md).</span></span>


#### <a name="using-the-storage-client-libraries"></a><span data-ttu-id="0366d-163">저장소 클라이언트 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="0366d-163">Using the Storage Client Libraries</span></span>
<span data-ttu-id="0366d-164">.NET, C++, Java, Android, Node.js, PHP, Python 및 Ruby와 같은 다양한 저장소 클라이언트 라이브러리 집합을 사용하여 Blob 저장소 간 또는 저장소 계정 간에 Blob 또는 파일 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-164">You can copy blob or file data to and from blob storage or between storage accounts using our rich set of Storage Client Libraries including .NET, C++, Java, Android, Node.js, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="0366d-165">자세한 내용은 [.NET을 사용하여 Azure Blob 저장소 시작](../blobs/storage-dotnet-how-to-use-blobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0366d-165">To learn more, please visit our [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

#### <a name="using-a-storage-explorer"></a><span data-ttu-id="0366d-166">저장소 탐색기 사용</span><span class="sxs-lookup"><span data-stu-id="0366d-166">Using a Storage Explorer</span></span>
<span data-ttu-id="0366d-167">저장소 탐색기를 사용하여 저장소 계정을 만들고 데이터를 업로드 및 다운로드하며 Blob 콘텐츠를 보고 디렉터리를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-167">You can use a Storage explorer to create storage accounts, upload and download data, view contents of blobs, and navigate through directories.</span></span> <span data-ttu-id="0366d-168">이중 하나를 사용하여 암호화가 설정된 저장소 계정으로 Blob를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-168">You can use one of these to upload blobs to your storage account with encryption enabled.</span></span> <span data-ttu-id="0366d-169">일부 저장소 탐색기에서 기존 Blob 저장소 계정에서 저장소 계정의 다른 컨테이너로 또는 SSE가 설정된 새 저장소 계정으로 데이터를 복사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-169">With some storage explorers, you can also copy data from existing blob storage to a different container in the storage account or a new storage account that has SSE enabled.</span></span>

<span data-ttu-id="0366d-170">자세한 내용은 [Azure 저장소 탐색기](../storage-explorers.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0366d-170">To learn more, please visit [Azure Storage Explorers](../storage-explorers.md).</span></span>

### <a name="step-4-query-the-status-of-the-encrypted-data"></a><span data-ttu-id="0366d-171">4단계: 암호화된 데이터 상태 쿼리</span><span class="sxs-lookup"><span data-stu-id="0366d-171">Step 4: Query the status of the encrypted data</span></span>
<span data-ttu-id="0366d-172">업데이트된 버전의 저장소 클라이언트 라이브러리가 배포되었으며 이를 통해 개체 상태를 쿼리하여 암호화 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-172">An updated version of the Storage Client libraries has been deployed that allows you to query the state of an object to determine if it is encrypted or not.</span></span> <span data-ttu-id="0366d-173">현재 Blob 저장소에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-173">This is currently only available for Blob storage.</span></span> <span data-ttu-id="0366d-174">파일 저장소에 대한 지원은 준비 중입니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-174">Support for File storage is on the roadmap.</span></span> 

<span data-ttu-id="0366d-175">그동안은 [계정 속성 가져오기](https://msdn.microsoft.com/library/azure/mt163553.aspx) 를 호출하여 저장소 계정에 암호화가 사용되었는지 확인하거나 Azure 포털에서 저장소 계정 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-175">In the meantime, you can call [Get Account Properties](https://msdn.microsoft.com/library/azure/mt163553.aspx) to verify that the storage account has encryption enabled or view the storage account properties in the Azure portal.</span></span>

## <a name="encryption-and-decryption-workflow"></a><span data-ttu-id="0366d-176">암호화 및 암호 해독 워크플로</span><span class="sxs-lookup"><span data-stu-id="0366d-176">Encryption and Decryption Workflow</span></span>
<span data-ttu-id="0366d-177">암호화/암호 해독 워크플로에 대한 간단한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-177">Here is a brief description of the encryption/decryption workflow:</span></span>

* <span data-ttu-id="0366d-178">고객이 저장소 계정에 대해 암호화를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-178">The customer enables encryption on the storage account.</span></span>
* <span data-ttu-id="0366d-179">고객이 새 데이터(PUT Blob, PUT 블록, PUT 페이지, PUT 파일 등)를 Blob 또는 파일 저장소에 기록할 경우 모든 기록 내용이 가장 강력한 블록 암호화 중 하나인 256비트 [AES 암호화](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-179">When the customer writes new data (PUT Blob, PUT Block, PUT Page, PUT File etc.) to Blob or File storage; every write is encrypted using 256-bit [AES encryption](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), one of the strongest block ciphers available.</span></span>
* <span data-ttu-id="0366d-180">고객이 데이터(GET Blob 등)에 액세스해야 하는 경우 사용자에게 반환되기 전에 데이터가 자동으로 해독됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-180">When the customer needs to access data (GET Blob, etc.), data is automatically decrypted before returning to the user.</span></span>
* <span data-ttu-id="0366d-181">암호화를 사용하지 않도록 설정하면 새로운 기록 내용은 더 이상 암호화되지 않으며 기존 암호화된 데이터는 사용자가 다시 작성할 때까지 암호화된 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-181">If encryption is disabled, new writes are no longer encrypted and existing encrypted data remains encrypted until rewritten by the user.</span></span> <span data-ttu-id="0366d-182">암호화를 사용하는 동안 Blob 또는 파일 저장소에 기록된 내용이 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-182">While encryption is enabled, writes to Blob or File storage will be encrypted.</span></span> <span data-ttu-id="0366d-183">저장소 계정에 대해 암호화를 사용/사용하지 않는 것으로 사용자 전환하는 것으로 데이터의 상태는 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-183">The state of data does not change with the user toggling between enabling/disabling encryption for the storage account.</span></span>
* <span data-ttu-id="0366d-184">모든 암호화 키는 Microsoft에서 저장, 암호화 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-184">All encryption keys are stored, encrypted, and managed by Microsoft.</span></span>

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a><span data-ttu-id="0366d-185">미사용 데이터에 대한 저장소 서비스 암호화에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="0366d-185">Frequently asked questions about Storage Service Encryption for Data at Rest</span></span>
<span data-ttu-id="0366d-186">**Q: 기존 클래식 저장소 계정이 있습니다. 이 계정에 SSE를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-186">**Q: I have an existing classic storage account. Can I enable SSE on it?**</span></span>

<span data-ttu-id="0366d-187">A: 아니요, SSE는 Resource Manager 저장소 계정에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-187">A: No, SSE is only supported on Resource Manager storage accounts.</span></span>

<span data-ttu-id="0366d-188">**Q: 내 클래식 저장소 계정에서 데이터를 암호화하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-188">**Q: How can I encrypt data in my classic storage account?**</span></span>

<span data-ttu-id="0366d-189">A: 새 Resource Manager 저장소 계정을 만들고 [AzCopy](storage-use-azcopy.md) 를 사용하여 기존 클래식 저장소 계정에서 데이터를 새로 만든 Resource Manager 저장소 계정으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-189">A: You can create a new Resource Manager storage account and copy your data using [AzCopy](storage-use-azcopy.md) from your existing classic storage account to your newly created Resource Manager storage account.</span></span> 

<span data-ttu-id="0366d-190">클래식 저장소 계정을 리소스 관리자 저장소 계정으로 마이그레이션하는 경우 이 작업은 즉각적이며 계정의 유형을 변경하지만 기존 데이터에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-190">If you migrate your classic storage account to a Resource Manager storage account, this operation is instantaneous, it changes the type of your account but does not effect your existing data.</span></span> <span data-ttu-id="0366d-191">새로 기록되는 데이터는 암호화를 사용하도록 설정한 후에만 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-191">Any new data written will be encrypted only after enabling encryption.</span></span> <span data-ttu-id="0366d-192">자세한 내용은 [클래식에서 Resource Manager로 IaaS 리소스의 플랫폼 지원 마이그레이션](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0366d-192">For more information, see [Platform Supported Migration of IaaS Resources from Classic to Resource Manager](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/).</span></span> <span data-ttu-id="0366d-193">이 기능은 Blob 및 파일 서비스에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-193">Please note that this is supported only for Blob and File services.</span></span>

<span data-ttu-id="0366d-194">**Q: 기존의 Resource Manager 저장소 계정이 있습니다. 이 계정에 SSE를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-194">**Q: I have an existing Resource Manager storage account. Can I enable SSE on it?**</span></span>

<span data-ttu-id="0366d-195">A: 예, 하지만 새로 작성한 데이터만 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-195">A: Yes, but only newly written data will be encrypted.</span></span> <span data-ttu-id="0366d-196">돌아가 기존에 있는 데이터를 암호화하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-196">It does not go back and encrypt data that was already present.</span></span> <span data-ttu-id="0366d-197">File Storage 미리 보기에는 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-197">This is not yet supported for the File Storage Preview.</span></span>

<span data-ttu-id="0366d-198">**Q: 기존 Resource Manager 저장소 계정에서 현재 데이터를 암호화하고 싶습니다.**</span><span class="sxs-lookup"><span data-stu-id="0366d-198">**Q: I would like to encrypt the current data in an existing Resource Manager storage account?**</span></span>

<span data-ttu-id="0366d-199">A: Resource Manager 저장소 계정에서 언제든지 SSE를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-199">A: You can enable SSE at any time in a Resource Manager storage account.</span></span> <span data-ttu-id="0366d-200">그러나 이미 있던 데이터는 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-200">However, data that were already present will not be encrypted.</span></span> <span data-ttu-id="0366d-201">기존 데이터를 암호화하려면 다른 이름이나 다른 컨테이너에 복사한 후 암호화되지 않은 버전을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-201">To encrypt existing data, you can copy them to another name or another container and then remove the unencrypted versions.</span></span>

<span data-ttu-id="0366d-202">**Q: 프리미엄 저장소를 사용 중입니다. SSE를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-202">**Q: I'm using Premium storage; can I use SSE?**</span></span>

<span data-ttu-id="0366d-203">A: 예, SSE는 표준 저장소 및 프리미엄 저장소 모두에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-203">A: Yes, SSE is supported on both Standard Storage and Premium Storage.</span></span>  <span data-ttu-id="0366d-204">파일 서비스에 대한 Premium Storage는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-204">Premium Storage is not supported for the File Service.</span></span>

<span data-ttu-id="0366d-205">**Q: 새 저장소 계정을 만들고 SSE를 사용한 경우 이 저장소 계정을 사용하여 새 VM을 만들면 내 VM이 암호화되어 있나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-205">**Q: If I create a new storage account and enable SSE, then create a new VM using that storage account, does that mean my VM is encrypted?**</span></span>

<span data-ttu-id="0366d-206">A: 예.</span><span class="sxs-lookup"><span data-stu-id="0366d-206">A: Yes.</span></span> <span data-ttu-id="0366d-207">새 저장소 계정을 사용하여 만든 모든 디스크는 SSE가 사용된 후 만들어졌다면 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-207">Any disks created that use the new storage account will be encrypted, as long as they are created after SSE is enabled.</span></span> <span data-ttu-id="0366d-208">VM을 Azure 마켓플레이스를 사용하여 만든 경우 VHD 기본 이미지는 암호화되지 않은 상태로 유지되지만 VM이 작동된 후 작성된 내용은 모두 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-208">If the VM was created using Azure Market Place, the VHD base image will remain unencrypted; however, any writes done after the VM has spun up will be encrypted.</span></span>

<span data-ttu-id="0366d-209">**Q: Azure PowerShell 및 Azure CLI를 사용하여 SSE가 사용된 새 저장소 계정을 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-209">**Q: Can I create new storage accounts with SSE enabled using Azure PowerShell and Azure CLI?**</span></span>

<span data-ttu-id="0366d-210">A: 예.</span><span class="sxs-lookup"><span data-stu-id="0366d-210">A: Yes.</span></span>

<span data-ttu-id="0366d-211">**Q: SSE를 사용하는 경우 Azure 저장소 비용은 얼마나 늘어나나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-211">**Q: How much more does Azure Storage cost if SSE is enabled?**</span></span>

<span data-ttu-id="0366d-212">A: 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-212">A: There is no additional cost.</span></span>

<span data-ttu-id="0366d-213">**Q: 암호화 키는 누가 관리하나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-213">**Q: Who manages the encryption keys?**</span></span>

<span data-ttu-id="0366d-214">A: 키는 Microsoft에서 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-214">A: The keys are managed by Microsoft.</span></span>

<span data-ttu-id="0366d-215">**Q: 나만의 암호화 키를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-215">**Q: Can I use my own encryption keys?**</span></span>

<span data-ttu-id="0366d-216">A: 고객이 자신의 고유한 암호화 키를 가져오는 기능을 제공하기 위한 작업 중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-216">A: We are working on providing capabilities for customers to bring their own encryption keys.</span></span>

<span data-ttu-id="0366d-217">**Q: 암호화 키에 대한 액세스를 해지할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-217">**Q: Can I revoke access to the encryption keys?**</span></span>

<span data-ttu-id="0366d-218">A: 현재는 없습니다. 키는 전적으로 Microsoft에서 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-218">A: Not at this time; the keys are fully managed by Microsoft.</span></span>

<span data-ttu-id="0366d-219">**Q: 새 저장소 계정을 만들 때 기본적으로 SSE가 사용되도록 설정되어 있나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-219">**Q: Is SSE enabled by default when I create a new storage account?**</span></span>

<span data-ttu-id="0366d-220">A: SSE는 기본적으로 사용되지 않습니다. Azure 포털로 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-220">A: SSE is not enabled by default; you can use the Azure portal to enable it.</span></span> <span data-ttu-id="0366d-221">또한 프로그래밍 방식으로 저장소 리소스 공급자 REST API를 사용하여 이 기능을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-221">You can also programmatically enable this feature using the Storage Resource Provider REST API.</span></span>

<span data-ttu-id="0366d-222">**Q: Azure Disk Encryption과 어떻게 다른가요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-222">**Q: How is this different from Azure Disk Encryption?**</span></span>

<span data-ttu-id="0366d-223">A: 이 기능은 Azure Blob 저장소에서 데이터를 암호화하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-223">A: This feature is used to encrypt data in Azure Blob storage.</span></span> <span data-ttu-id="0366d-224">Azure 디스크 암호화는 OS 및 IaaS VM에서 데이터 디스크를 암호화하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-224">The Azure Disk Encryption is used to encrypt OS and Data disks in IaaS VMs.</span></span> <span data-ttu-id="0366d-225">자세한 내용은 [저장소 보안 가이드](../storage-security-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0366d-225">For more details, please visit our [Storage Security Guide](../storage-security-guide.md).</span></span>

<span data-ttu-id="0366d-226">**Q: SSE가 사용되도록 설정된 경우 이동하여 디스크에서 Azure 디스크 암호화를 사용하도록 설정하면 어떻게 되나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-226">**Q: What if I enable SSE, and then go in and enable Azure Disk Encryption on the disks?**</span></span>

<span data-ttu-id="0366d-227">A: 이것은 원활하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-227">A: This will work seamlessly.</span></span> <span data-ttu-id="0366d-228">데이터는 두 가지 방법으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-228">Your data will be encrypted by both methods.</span></span>

<span data-ttu-id="0366d-229">**Q: 내 저장소 계정이 지역 중복되어 복제되도록 설정됩니다. SSE를 사용하도록 설정하는 경우 내 중복 복사본도 암호화되나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-229">**Q: My storage account is set up to be replicated geo-redundantly. If I enable SSE, will my redundant copy also be encrypted?**</span></span>

<span data-ttu-id="0366d-230">A: 예, 저장소 계정의 모든 복사본이 암호화되며 로컬 중복 저장소(LRS), 영역 중복 저장소(ZRS), 지역 중복 저장소(GRS), 읽기 액세스 지역 중복 저장소(RA-GRS)의 모든 중복성 옵션이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-230">A: Yes, all copies of the storage account are encrypted, and all redundancy options – Locally Redundant Storage (LRS), Zone-Redundant Storage (ZRS), Geo-Redundant Storage (GRS), and Read Access Geo-Redundant Storage (RA-GRS) – are supported.</span></span>

<span data-ttu-id="0366d-231">**Q: 내 저장소 계정에서 암호화를 사용할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="0366d-231">**Q: I can't enable encryption on my storage account.**</span></span>

<span data-ttu-id="0366d-232">A: Resource Manager 저장소 계정인가요?</span><span class="sxs-lookup"><span data-stu-id="0366d-232">A: Is it a Resource Manager storage account?</span></span> <span data-ttu-id="0366d-233">클래식 저장소 계정은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-233">Classic storage accounts are not supported.</span></span> 

<span data-ttu-id="0366d-234">**Q: SSE는 특정 지역에만 허용되나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-234">**Q: Is SSE only permitted in specific regions?**</span></span>

<span data-ttu-id="0366d-235">A: SSE는 Blob 저장소에 대해 모든 지역에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-235">A: The SSE is available in all regions for Blob storage.</span></span> <span data-ttu-id="0366d-236">파일 저장소에 대한 가용성 섹션을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0366d-236">Please check the Availability Section for File storage.</span></span> 

<span data-ttu-id="0366d-237">**Q: 문제가 있거나 피드백을 제공하고 싶은 경우 어떻게 연락하나요?**</span><span class="sxs-lookup"><span data-stu-id="0366d-237">**Q: How do I contact someone if I have any issues or want to provide feedback?**</span></span>

<span data-ttu-id="0366d-238">A: 저장소 서비스 암호화에 대한 문제는 [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) 으로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="0366d-238">A: Please contact [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) for any issues related to Storage Service Encryption.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0366d-239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0366d-239">Next Steps</span></span>
<span data-ttu-id="0366d-240">Azure 저장소는 여러 개발자가 보안 응용 프로그램을 함께 빌드할 수 있도록 하는 포괄적인 보안 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0366d-240">Azure Storage provides a comprehensive set of security capabilities which together enable developers to build secure applications.</span></span> <span data-ttu-id="0366d-241">자세한 내용은 [저장소 보안 가이드](../storage-security-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0366d-241">For more details, visit the [Storage Security Guide](../storage-security-guide.md).</span></span>

