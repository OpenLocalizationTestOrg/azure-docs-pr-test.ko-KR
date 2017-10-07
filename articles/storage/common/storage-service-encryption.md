---
title: "미사용 데이터에 대 한 저장소 서비스 암호화 aaaAzure | Microsoft Docs"
description: "사용 하 여 hello Azure 저장소 서비스 암호화 기능 tooencrypt Azure Blob 저장소 서비스 쪽 hello hello 데이터를 저장할 때 및 hello 데이터를 검색할 때 암호를 해독 합니다."
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
ms.openlocfilehash: 4e03c5704071281a798936d41d86456afcfdec77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-service-encryption-for-data-at-rest"></a><span data-ttu-id="d8921-103">휴지 상태의 데이터에 대한 Azure 저장소 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="d8921-103">Azure Storage Service Encryption for Data at Rest</span></span>
<span data-ttu-id="d8921-104">Azure 저장소 서비스 암호화 SSE ()을 미사용 데이터를 사용 하면 조직의 보안 및 규정 준수 약정 데이터 toomeet를 보호 하 고 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-104">Azure Storage Service Encryption (SSE) for Data at Rest helps you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="d8921-105">이 기능을 Azure 저장소는 자동으로 데이터 사전 toopersisting toostorage를 암호화 하 고 이전 tooretrieval 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-105">With this feature, Azure Storage automatically encrypts your data prior toopersisting toostorage and decrypts prior tooretrieval.</span></span> <span data-ttu-id="d8921-106">hello 암호화, 해독 및 키 관리에 완전히 투명 한 toousers 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-106">hello encryption, decryption, and key management are totally transparent toousers.</span></span>

<span data-ttu-id="d8921-107">hello 다음 섹션에서는 자세한 지침을 제공 hello 뿐만 아니라 toouse hello 저장소 서비스 암호화 기능 시나리오 및 사용자 환경을 원하는 하는 방법에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-107">hello following sections provide detailed guidance on how toouse hello Storage Service Encryption features as well as hello supported scenarios and user experiences.</span></span>

## <a name="overview"></a><span data-ttu-id="d8921-108">개요</span><span class="sxs-lookup"><span data-stu-id="d8921-108">Overview</span></span>
<span data-ttu-id="d8921-109">Azure 저장소는 다양 한 개발자를 함께 사용 하는 보안 기능 toobuild 보안 응용 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-109">Azure Storage provides a comprehensive set of security capabilities which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="d8921-110">[클라이언트 쪽 암호화](../storage-client-side-encryption.md), HTTP 또는 SMB 3.0을 사용하여 응용 프로그램과 Azure 간에 전송 중인 데이터의 보안을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-110">Data can be secured in transit between an application and Azure by using [Client-Side Encryption](../storage-client-side-encryption.md), HTTPs, or SMB 3.0.</span></span> <span data-ttu-id="d8921-111">저장소 서비스 암호화는 휴지 상태의 암호화를 제공하며 암호화, 암호 해독, 키 관리를 완전히 투명한 방식으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-111">Storage Service Encryption provides encryption at rest, handling encryption, decryption, and key management in a totally transparent fashion.</span></span> <span data-ttu-id="d8921-112">256 비트를 사용 하 여 모든 데이터는 암호화 [AES 암호화](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), 사용할 수 있는 암호 hello 가장 강력한 블록 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-112">All data is encrypted using 256-bit [AES encryption](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), one of hello strongest block ciphers available.</span></span>

<span data-ttu-id="d8921-113">SSE는 tooAzure 저장소, 작성 하 고 Azure Blob 저장소 및 파일 저장소에 사용할 수 있습니다 때 hello 데이터를 암호화 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-113">SSE works by encrypting hello data when it is written tooAzure Storage, and can be used for Azure Blob Storage and File Storage.</span></span> <span data-ttu-id="d8921-114">Hello 다음에 대 한 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-114">It works for hello following:</span></span>

* <span data-ttu-id="d8921-115">표준 저장소: Blob에 대한 범용 저장소 계정과 File Storage 및 Blob Storage 계정</span><span class="sxs-lookup"><span data-stu-id="d8921-115">Standard Storage: General purpose storage accounts for Blobs and File storage and Blob storage accounts</span></span>
* <span data-ttu-id="d8921-116">Premium Storage</span><span class="sxs-lookup"><span data-stu-id="d8921-116">Premium storage</span></span> 
* <span data-ttu-id="d8921-117">모든 중복 수준(LRS, ZRS, GRS, RA-GRS)</span><span class="sxs-lookup"><span data-stu-id="d8921-117">All redundancy levels (LRS, ZRS, GRS, RA-GRS)</span></span>
* <span data-ttu-id="d8921-118">Azure Resource Manager 저장소 계정(클래식 아님)</span><span class="sxs-lookup"><span data-stu-id="d8921-118">Azure Resource Manager storage accounts (but not classic)</span></span> 
* <span data-ttu-id="d8921-119">모든 지역</span><span class="sxs-lookup"><span data-stu-id="d8921-119">All regions.</span></span>

<span data-ttu-id="d8921-120">toolearn을 참조 하십시오 toohello FAQ.</span><span class="sxs-lookup"><span data-stu-id="d8921-120">toolearn more, please refer toohello FAQ.</span></span>

<span data-ttu-id="d8921-121">저장소 계정에 대 한 저장소 서비스 암호화 hello에 로그인 할 tooenable 또는 사용 안 함 [Azure 포털](https://portal.azure.com) 하 고 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-121">tooenable or disable Storage Service Encryption for a storage account, log into hello [Azure portal](https://portal.azure.com) and select a storage account.</span></span> <span data-ttu-id="d8921-122">Hello 설정 블레이드에서이 스크린샷에 표시 된 대로 Blob 서비스 섹션 hello에 대 한 확인 하 고 암호화를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-122">On hello Settings blade, look for hello Blob Service section as shown in this screenshot and click Encryption.</span></span>

<span data-ttu-id="d8921-123">![암호화 옵션을 보여 주는 포털 스크린샷](./media/storage-service-encryption/image1.png)
</span><span class="sxs-lookup"><span data-stu-id="d8921-123">![Portal Screenshot showing Encryption option](./media/storage-service-encryption/image1.png)
</span></span><br/><span data-ttu-id="d8921-124">*그림 1: Blob Service에 SSE 사용(1단계)*</span><span class="sxs-lookup"><span data-stu-id="d8921-124">*Figure 1: Enable SSE for Blob Service (Step1)*</span></span>

<span data-ttu-id="d8921-125">![암호화 옵션을 보여 주는 포털 스크린샷](./media/storage-service-encryption/image3.png)
</span><span class="sxs-lookup"><span data-stu-id="d8921-125">![Portal Screenshot showing Encryption option](./media/storage-service-encryption/image3.png)
</span></span><br/><span data-ttu-id="d8921-126">*그림 2: 파일 서비스에 SSE 사용(1단계)*</span><span class="sxs-lookup"><span data-stu-id="d8921-126">*Figure 2: Enable SSE for File Service (Step1)*</span></span>

<span data-ttu-id="d8921-127">Hello 암호화 설정을 클릭 한 후 사용 하도록 설정 하거나 저장소 서비스 암호화를 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-127">After you click hello Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

<span data-ttu-id="d8921-128">![암호화 속성을 보여 주는 포털 스크린샷](./media/storage-service-encryption/image2.png)
</span><span class="sxs-lookup"><span data-stu-id="d8921-128">![Portal Screenshot showing Encryption properties](./media/storage-service-encryption/image2.png)
</span></span><br/><span data-ttu-id="d8921-129">*그림 3: Blob 및 파일 서비스에 SSE 사용(2단계)*</span><span class="sxs-lookup"><span data-stu-id="d8921-129">*Figure 3: Enable SSE for Blob and File Service (Step2)*</span></span>

## <a name="encryption-scenarios"></a><span data-ttu-id="d8921-130">암호화 시나리오</span><span class="sxs-lookup"><span data-stu-id="d8921-130">Encryption Scenarios</span></span>
<span data-ttu-id="d8921-131">저장소 계정 수준에서 저장소 서비스 암호화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-131">Storage Service Encryption can be enabled at a storage account level.</span></span> <span data-ttu-id="d8921-132">활성화 되 면 어떤 서비스 tooencrypt 고객을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-132">Once enabled, customers will choose which services tooencrypt.</span></span> <span data-ttu-id="d8921-133">Hello 다음 고객 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-133">It supports hello following customer scenarios:</span></span>

* <span data-ttu-id="d8921-134">리소스 관리자 계정의 Blob Storage 및 File Storage 암호화</span><span class="sxs-lookup"><span data-stu-id="d8921-134">Encryption of Blob Storage and File Storage in Resource Manager accounts.</span></span>
* <span data-ttu-id="d8921-135">Blob 및 파일 서비스의에서 암호화 클래식 저장소 계정 한 번 tooResource Manager 저장소 계정 마이그레이션.</span><span class="sxs-lookup"><span data-stu-id="d8921-135">Encryption of Blob and File Service in classic storage accounts once migrated tooResource Manager storage accounts.</span></span>

<span data-ttu-id="d8921-136">SSE 다음과 같은 제한을 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-136">SSE has hello following limitations:</span></span>

* <span data-ttu-id="d8921-137">클래식 저장소 계정의 암호화는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-137">Encryption of classic storage accounts is not supported.</span></span>
* <span data-ttu-id="d8921-138">기존 데이터 요금-SSE hello 암호화가 사용 하도록 설정만 새로 만든된 데이터를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-138">Existing Data - SSE only encrypts newly created data after hello encryption is enabled.</span></span> <span data-ttu-id="d8921-139">예를 들어 새 리소스 관리자 저장소 계정을 만드는 하지만 암호화를 사용 하지 않는 한 blob 또는 보관 된 Vhd toothat 저장소 계정에 업로드 하 고 다음 SSE 설정 하는 다음 경우 다시 작성 하거나 복사 하는 경우가 아니면 해당 blob 암호화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-139">If for example you create a new Resource Manager storage account but don't turn on encryption, and then you upload blobs or archived VHDs toothat storage account and then turn on SSE, those blobs will not be encrypted unless they are rewritten or copied.</span></span>
* <span data-ttu-id="d8921-140">마켓플레이스 지원-Enable Vm의 암호화에서 만든 hello hello를 사용 하 여 마켓플레이스 [Azure 포털](https://portal.azure.com), PowerShell 및 Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-140">Marketplace Support - Enable encryption of VMs created from hello Marketplace using hello [Azure portal](https://portal.azure.com), PowerShell, and Azure CLI.</span></span> <span data-ttu-id="d8921-141">hello VHD에 대 한 기본 이미지; 암호화 되지 않은 상태로 유지 됩니다. 그러나 VM hello가 생성 한 후에 수행 된 쓰기 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-141">hello VHD base image will remain unencrypted; however, any writes done after hello VM has spun up will be encrypted.</span></span>
* <span data-ttu-id="d8921-142">테이블 및 큐 데이터는 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-142">Table and Queues data will not be encrypted.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d8921-143">시작하기</span><span class="sxs-lookup"><span data-stu-id="d8921-143">Getting Started</span></span>
### <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a><span data-ttu-id="d8921-144">1단계: [새 저장소 계정 만들기](../storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d8921-144">Step 1: [Create a new storage account](../storage-create-storage-account.md).</span></span>
### <a name="step-2-enable-encryption"></a><span data-ttu-id="d8921-145">2단계: 암호화 사용.</span><span class="sxs-lookup"><span data-stu-id="d8921-145">Step 2: Enable encryption.</span></span>
<span data-ttu-id="d8921-146">Hello를 사용 하 여 암호화를 사용 하도록 설정할 수 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-146">You can enable encryption using hello [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="d8921-147">Hello tooprogrammatically 사용 하려면 저장소 계정에서 저장소 서비스 암호화 hello를 사용 하지 않도록 설정 하거나, 사용할 수 있습니다 [Azure 저장소 리소스 공급자 REST API](https://msdn.microsoft.com/library/azure/mt163683.aspx), hello [저장소 리소스 공급자 클라이언트 라이브러리 .NET 용](https://msdn.microsoft.com/library/azure/mt131037.aspx), [Azure PowerShell](/powershell/azureps-cmdlets-docs), 또는 hello [Azure CLI](../storage-azure-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-147">If you want tooprogrammatically enable or disable hello Storage Service Encryption on a storage account, you can use hello [Azure Storage Resource Provider REST API](https://msdn.microsoft.com/library/azure/mt163683.aspx), hello [Storage Resource Provider Client Library for .NET](https://msdn.microsoft.com/library/azure/mt131037.aspx), [Azure PowerShell](/powershell/azureps-cmdlets-docs), or hello [Azure CLI](../storage-azure-cli.md).</span></span>
> 
> 

### <a name="step-3-copy-data-toostorage-account"></a><span data-ttu-id="d8921-148">3 단계: 데이터 toostorage 계정 복사</span><span class="sxs-lookup"><span data-stu-id="d8921-148">Step 3: Copy data toostorage account</span></span>
<span data-ttu-id="d8921-149">Hello Blob 서비스에 대 한 SSE를 사용 하면, toothat 저장소 계정 작성 된 모든 blob이 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-149">If you enable SSE for hello Blob service, any blobs written toothat storage account will be encrypted.</span></span> <span data-ttu-id="d8921-150">저장소 계정에 이미 있는 모든 Blob는 다시 작성할 때까지 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-150">Any blobs already located in that storage account will not be encrypted until they are rewritten.</span></span> <span data-ttu-id="d8921-151">암호화, SSE와 한 저장소 계정 tooone에서 hello 데이터를 복사 또는 SSE를에서 이전 데이터 암호화 되어 하나의 컨테이너 tooanother toosure hello blob을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-151">You can copy hello data from one storage account tooone with SSE encrypted, or even enable SSE and copy hello blobs from one container tooanother toosure that previous data is encrypted.</span></span> <span data-ttu-id="d8921-152">사용할 수 있습니다 hello 도구 tooaccomplish 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-152">You can use any of hello following tools tooaccomplish this.</span></span> <span data-ttu-id="d8921-153">파일 저장소에도 동일한 동작을 hello는이 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-153">This is hello same behavior for File Storage as well.</span></span>

#### <a name="using-azcopy"></a><span data-ttu-id="d8921-154">AzCopy 사용</span><span class="sxs-lookup"><span data-stu-id="d8921-154">Using AzCopy</span></span>
<span data-ttu-id="d8921-155">AzCopy는 간단한 명령을 사용 하 여 최적의 성능으로 Microsoft Azure Blob, 파일 및 테이블 저장소에서 데이터 tooand 복사를 위해 설계 된 Windows 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-155">AzCopy is a Windows command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="d8921-156">이 toocopy blob 또는 SSE 사용 하도록 설정 된 하나의 저장소 계정 tooanother에서 파일에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-156">You can use this toocopy your blobs or files from one storage account tooanother one that has SSE enabled.</span></span> 

<span data-ttu-id="d8921-157">toolearn을 방문 하세요 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-157">toolearn more, please visit [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

#### <a name="using-smb"></a><span data-ttu-id="d8921-158">SMB 사용</span><span class="sxs-lookup"><span data-stu-id="d8921-158">Using SMB</span></span>
<span data-ttu-id="d8921-159">Azure 파일 저장소 hello 표준 SMB 프로토콜을 사용 하 여 hello 클라우드에서 파일 공유를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-159">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="d8921-160">온-프레미스 또는 Azure의 클라이언트에서 파일 공유를 마운트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-160">You can mount a file share from a client on premises or in Azure.</span></span> <span data-ttu-id="d8921-161">탑재 면 Robocopy와 같은 도구 tooAzure 파일 공유를 통해 사용된 toocopy 파일 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-161">Once mounted, tools such as Robocopy can be used toocopy files over tooAzure File shares.</span></span> <span data-ttu-id="d8921-162">자세한 내용은 참조 [toomount Azure 파일 공유 어떻게 Windows에서](../files/storage-how-to-use-files-windows.md) 및 [linux toomount Azure 파일을 공유 하는 방법](../storage-how-to-use-files-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-162">For more information, see [how toomount Azure File Share on Windows](../files/storage-how-to-use-files-windows.md) and [how toomount Azure File share on Linux](../storage-how-to-use-files-linux.md).</span></span>


#### <a name="using-hello-storage-client-libraries"></a><span data-ttu-id="d8921-163">Hello 저장소 클라이언트 라이브러리를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d8921-163">Using hello Storage Client Libraries</span></span>
<span data-ttu-id="d8921-164">Blob 저장소에서 또는 다양 한.NET, c + +, Java, Android, Node.js, PHP, Python 및 Ruby를 비롯 한 저장소 클라이언트 라이브러리를 사용 하 여 저장소 계정 간에 blob 또는 파일 데이터 tooand를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-164">You can copy blob or file data tooand from blob storage or between storage accounts using our rich set of Storage Client Libraries including .NET, C++, Java, Android, Node.js, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="d8921-165">toolearn을 방문 하세요 우리의 [.NET을 사용 하 여 Azure Blob 저장소 시작](../blobs/storage-dotnet-how-to-use-blobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-165">toolearn more, please visit our [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

#### <a name="using-a-storage-explorer"></a><span data-ttu-id="d8921-166">저장소 탐색기 사용</span><span class="sxs-lookup"><span data-stu-id="d8921-166">Using a Storage Explorer</span></span>
<span data-ttu-id="d8921-167">하면 저장소 탐색기 toocreate 저장소 계정을 사용 하 여, 업로드 및 데이터 다운로드, blob의 내용을 보는 및 디렉터리를 통해 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-167">You can use a Storage explorer toocreate storage accounts, upload and download data, view contents of blobs, and navigate through directories.</span></span> <span data-ttu-id="d8921-168">암호화가 설정 되어 이러한 tooupload blob tooyour 저장소 계정 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-168">You can use one of these tooupload blobs tooyour storage account with encryption enabled.</span></span> <span data-ttu-id="d8921-169">일부 저장소 탐색기와 SSE를 사용할 수 있는 새 저장소 계정 또는 기존 blob 저장소 tooa 다른 컨테이너에서 hello 저장소 계정에서 데이터를 복사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-169">With some storage explorers, you can also copy data from existing blob storage tooa different container in hello storage account or a new storage account that has SSE enabled.</span></span>

<span data-ttu-id="d8921-170">toolearn을 방문 하세요 [Azure 저장소 탐색기](../storage-explorers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-170">toolearn more, please visit [Azure Storage Explorers](../storage-explorers.md).</span></span>

### <a name="step-4-query-hello-status-of-hello-encrypted-data"></a><span data-ttu-id="d8921-171">4 단계: hello hello 상태 쿼리 암호화 된 데이터</span><span class="sxs-lookup"><span data-stu-id="d8921-171">Step 4: Query hello status of hello encrypted data</span></span>
<span data-ttu-id="d8921-172">수 있는 개체 toodetermine의 tooquery hello 상태 또는 암호화 되어 있으면 업데이트 된 버전의 hello 저장소 클라이언트 라이브러리 배포 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-172">An updated version of hello Storage Client libraries has been deployed that allows you tooquery hello state of an object toodetermine if it is encrypted or not.</span></span> <span data-ttu-id="d8921-173">현재 Blob 저장소에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-173">This is currently only available for Blob storage.</span></span> <span data-ttu-id="d8921-174">파일 저장소에 대 한 지원 hello 로드맵 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-174">Support for File storage is on hello roadmap.</span></span> 

<span data-ttu-id="d8921-175">Hello 그 동안 호출할 수 있습니다 [계정 속성 가져오기](https://msdn.microsoft.com/library/azure/mt163553.aspx) 저장소 계정 hello tooverify에 암호화 사용 또는 hello hello Azure 포털에서에서 저장소 계정 속성 보기.</span><span class="sxs-lookup"><span data-stu-id="d8921-175">In hello meantime, you can call [Get Account Properties](https://msdn.microsoft.com/library/azure/mt163553.aspx) tooverify that hello storage account has encryption enabled or view hello storage account properties in hello Azure portal.</span></span>

## <a name="encryption-and-decryption-workflow"></a><span data-ttu-id="d8921-176">암호화 및 암호 해독 워크플로</span><span class="sxs-lookup"><span data-stu-id="d8921-176">Encryption and Decryption Workflow</span></span>
<span data-ttu-id="d8921-177">암호화/암호 해독 워크플로 hello에 대 한 간단한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-177">Here is a brief description of hello encryption/decryption workflow:</span></span>

* <span data-ttu-id="d8921-178">hello 고객 hello 저장소 계정에서 암호화를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-178">hello customer enables encryption on hello storage account.</span></span>
* <span data-ttu-id="d8921-179">새 데이터 (예: PUT Blob, 배치 블록, PUT Page, 배치 파일 등) tooBlob 또는 파일 저장소; hello 고객 기록 하는 경우 모든 쓰기 256 비트를 사용 하 여 암호화 되어 [AES 암호화](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), 사용할 수 있는 암호 hello 가장 강력한 블록 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-179">When hello customer writes new data (PUT Blob, PUT Block, PUT Page, PUT File etc.) tooBlob or File storage; every write is encrypted using 256-bit [AES encryption](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), one of hello strongest block ciphers available.</span></span>
* <span data-ttu-id="d8921-180">Hello 고객이 tooaccess 데이터 (Blob 가져오기, 등), toohello 사용자를 반환 하기 전에 데이터는 자동으로 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-180">When hello customer needs tooaccess data (GET Blob, etc.), data is automatically decrypted before returning toohello user.</span></span>
* <span data-ttu-id="d8921-181">암호화를 해제 하는 경우 새로운 쓰기는 더 이상 암호화 되며 기존의 암호화 된 데이터 암호화 상태를 유지 hello 사용자가 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-181">If encryption is disabled, new writes are no longer encrypted and existing encrypted data remains encrypted until rewritten by hello user.</span></span> <span data-ttu-id="d8921-182">암호화를 사용 하는 동안 tooBlob 또는 파일 저장소를 암호화할 씁니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-182">While encryption is enabled, writes tooBlob or File storage will be encrypted.</span></span> <span data-ttu-id="d8921-183">hello 저장소 계정에 대 한 암호화를 활성화/비활성화을 전환 하는 hello 사용자와 데이터의 hello 상태 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-183">hello state of data does not change with hello user toggling between enabling/disabling encryption for hello storage account.</span></span>
* <span data-ttu-id="d8921-184">모든 암호화 키는 Microsoft에서 저장, 암호화 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-184">All encryption keys are stored, encrypted, and managed by Microsoft.</span></span>

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a><span data-ttu-id="d8921-185">미사용 데이터에 대한 저장소 서비스 암호화에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="d8921-185">Frequently asked questions about Storage Service Encryption for Data at Rest</span></span>
<span data-ttu-id="d8921-186">**Q: 기존 클래식 저장소 계정이 있습니다. 이 계정에 SSE를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-186">**Q: I have an existing classic storage account. Can I enable SSE on it?**</span></span>

<span data-ttu-id="d8921-187">A: 아니요, SSE는 Resource Manager 저장소 계정에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-187">A: No, SSE is only supported on Resource Manager storage accounts.</span></span>

<span data-ttu-id="d8921-188">**Q: 내 클래식 저장소 계정에서 데이터를 암호화하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-188">**Q: How can I encrypt data in my classic storage account?**</span></span>

<span data-ttu-id="d8921-189">A: 새 저장소 계정 리소스 관리자를 만들고 사용 하 여 데이터를 복사할 수 있습니다 [AzCopy](storage-use-azcopy.md) 기존 클래식 저장소 계정에서 tooyour 새로 만든 저장소 계정 리소스 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-189">A: You can create a new Resource Manager storage account and copy your data using [AzCopy](storage-use-azcopy.md) from your existing classic storage account tooyour newly created Resource Manager storage account.</span></span> 

<span data-ttu-id="d8921-190">클래식 저장소 계정을 tooa 저장소 계정 리소스 관리자를 마이그레이션하는 경우이 작업은 즉각적인를 사용자의 계정 유형을 hello 변경 되지만 기존 데이터는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-190">If you migrate your classic storage account tooa Resource Manager storage account, this operation is instantaneous, it changes hello type of your account but does not effect your existing data.</span></span> <span data-ttu-id="d8921-191">새로 기록되는 데이터는 암호화를 사용하도록 설정한 후에만 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-191">Any new data written will be encrypted only after enabling encryption.</span></span> <span data-ttu-id="d8921-192">자세한 내용은 참조 [플랫폼 지원 마이그레이션의 IaaS에서에서 리소스 관리자 클래식 tooResource](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-192">For more information, see [Platform Supported Migration of IaaS Resources from Classic tooResource Manager](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/).</span></span> <span data-ttu-id="d8921-193">이 기능은 Blob 및 파일 서비스에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-193">Please note that this is supported only for Blob and File services.</span></span>

<span data-ttu-id="d8921-194">**Q: 기존의 Resource Manager 저장소 계정이 있습니다. 이 계정에 SSE를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-194">**Q: I have an existing Resource Manager storage account. Can I enable SSE on it?**</span></span>

<span data-ttu-id="d8921-195">A: 예, 하지만 새로 작성한 데이터만 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-195">A: Yes, but only newly written data will be encrypted.</span></span> <span data-ttu-id="d8921-196">돌아가 기존에 있는 데이터를 암호화하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-196">It does not go back and encrypt data that was already present.</span></span> <span data-ttu-id="d8921-197">이 아직 지원 되지 않습니다 hello 파일 저장소 미리 보기에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-197">This is not yet supported for hello File Storage Preview.</span></span>

<span data-ttu-id="d8921-198">**Q: 기존 저장소 계정 리소스 관리자의에서 현재 데이터 hello를 tooencrypt 겠어요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-198">**Q: I would like tooencrypt hello current data in an existing Resource Manager storage account?**</span></span>

<span data-ttu-id="d8921-199">A: Resource Manager 저장소 계정에서 언제든지 SSE를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-199">A: You can enable SSE at any time in a Resource Manager storage account.</span></span> <span data-ttu-id="d8921-200">그러나 이미 있던 데이터는 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-200">However, data that were already present will not be encrypted.</span></span> <span data-ttu-id="d8921-201">기존 데이터 용량의 tooencrypt tooanother 이름이 나 다른 컨테이너를 복사 하 고 다음 hello 암호화 되지 않은 버전을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-201">tooencrypt existing data, you can copy them tooanother name or another container and then remove hello unencrypted versions.</span></span>

<span data-ttu-id="d8921-202">**Q: 프리미엄 저장소를 사용 중입니다. SSE를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-202">**Q: I'm using Premium storage; can I use SSE?**</span></span>

<span data-ttu-id="d8921-203">A: 예, SSE는 표준 저장소 및 프리미엄 저장소 모두에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-203">A: Yes, SSE is supported on both Standard Storage and Premium Storage.</span></span>  <span data-ttu-id="d8921-204">프리미엄 저장소 hello 파일 서비스에 대 한 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-204">Premium Storage is not supported for hello File Service.</span></span>

<span data-ttu-id="d8921-205">**Q: 새 저장소 계정을 만들고 SSE를 사용한 경우 이 저장소 계정을 사용하여 새 VM을 만들면 내 VM이 암호화되어 있나요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-205">**Q: If I create a new storage account and enable SSE, then create a new VM using that storage account, does that mean my VM is encrypted?**</span></span>

<span data-ttu-id="d8921-206">A: 예.</span><span class="sxs-lookup"><span data-stu-id="d8921-206">A: Yes.</span></span> <span data-ttu-id="d8921-207">SSE 사용 하도록 설정한 후 사용자에 게 만들어질으로 만든 hello 새 저장소 계정을 사용 하는 모든 디스크 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-207">Any disks created that use hello new storage account will be encrypted, as long as they are created after SSE is enabled.</span></span> <span data-ttu-id="d8921-208">VM을 Azure Market Place hello VHD에 대 한 기본 이미지를 사용 하 여 만들어진 hello; 암호화 되지 않은 상태로 유지 되 면 그러나 VM hello가 생성 한 후에 수행 된 쓰기 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-208">If hello VM was created using Azure Market Place, hello VHD base image will remain unencrypted; however, any writes done after hello VM has spun up will be encrypted.</span></span>

<span data-ttu-id="d8921-209">**Q: Azure PowerShell 및 Azure CLI를 사용하여 SSE가 사용된 새 저장소 계정을 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-209">**Q: Can I create new storage accounts with SSE enabled using Azure PowerShell and Azure CLI?**</span></span>

<span data-ttu-id="d8921-210">A: 예.</span><span class="sxs-lookup"><span data-stu-id="d8921-210">A: Yes.</span></span>

<span data-ttu-id="d8921-211">**Q: SSE를 사용하는 경우 Azure 저장소 비용은 얼마나 늘어나나요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-211">**Q: How much more does Azure Storage cost if SSE is enabled?**</span></span>

<span data-ttu-id="d8921-212">A: 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-212">A: There is no additional cost.</span></span>

<span data-ttu-id="d8921-213">**Q: 누구 hello 암호화 키를 관리?**</span><span class="sxs-lookup"><span data-stu-id="d8921-213">**Q: Who manages hello encryption keys?**</span></span>

<span data-ttu-id="d8921-214">A: hello 키 Microsoft에서 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-214">A: hello keys are managed by Microsoft.</span></span>

<span data-ttu-id="d8921-215">**Q: 나만의 암호화 키를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-215">**Q: Can I use my own encryption keys?**</span></span>

<span data-ttu-id="d8921-216">A: 제작 하는 암호화 키가 자신의 고객 toobring에 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-216">A: We are working on providing capabilities for customers toobring their own encryption keys.</span></span>

<span data-ttu-id="d8921-217">**Q: 액세스 toohello 암호화 키 취소 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="d8921-217">**Q: Can I revoke access toohello encryption keys?**</span></span>

<span data-ttu-id="d8921-218">A: 현재는 없습니다. hello 키 Microsoft에서 완전히 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-218">A: Not at this time; hello keys are fully managed by Microsoft.</span></span>

<span data-ttu-id="d8921-219">**Q: 새 저장소 계정을 만들 때 기본적으로 SSE가 사용되도록 설정되어 있나요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-219">**Q: Is SSE enabled by default when I create a new storage account?**</span></span>

<span data-ttu-id="d8921-220">A: SSE 기본적으로 사용 되지 않습니다. Azure 포털 tooenable hello를 사용할 수 있습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-220">A: SSE is not enabled by default; you can use hello Azure portal tooenable it.</span></span> <span data-ttu-id="d8921-221">또한 프로그래밍 방식으로 hello 저장소 리소스 공급자 REST API를 사용 하 여이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-221">You can also programmatically enable this feature using hello Storage Resource Provider REST API.</span></span>

<span data-ttu-id="d8921-222">**Q: Azure Disk Encryption과 어떻게 다른가요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-222">**Q: How is this different from Azure Disk Encryption?**</span></span>

<span data-ttu-id="d8921-223">A:가 기능은 Azure Blob 저장소에 사용 되는 tooencrypt 데이터에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-223">A: This feature is used tooencrypt data in Azure Blob storage.</span></span> <span data-ttu-id="d8921-224">hello Azure 디스크 암호화는 IaaS Vm의 OS 및 데이터 디스크를 사용 하는 tooencrypt 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-224">hello Azure Disk Encryption is used tooencrypt OS and Data disks in IaaS VMs.</span></span> <span data-ttu-id="d8921-225">자세한 내용은 [저장소 보안 가이드](../storage-security-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8921-225">For more details, please visit our [Storage Security Guide](../storage-security-guide.md).</span></span>

<span data-ttu-id="d8921-226">**Q: 어떻게 하면 SSE 및 다음에서 설정 및 hello 디스크에서 Azure 디스크 암호화를 사용 하도록 설정?**</span><span class="sxs-lookup"><span data-stu-id="d8921-226">**Q: What if I enable SSE, and then go in and enable Azure Disk Encryption on hello disks?**</span></span>

<span data-ttu-id="d8921-227">A: 이것은 원활하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-227">A: This will work seamlessly.</span></span> <span data-ttu-id="d8921-228">데이터는 두 가지 방법으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-228">Your data will be encrypted by both methods.</span></span>

<span data-ttu-id="d8921-229">**Q: 내 저장소 계정이 지리적 중복 복제 toobe 설정 되어 있습니다. SSE를 사용하도록 설정하는 경우 내 중복 복사본도 암호화되나요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-229">**Q: My storage account is set up toobe replicated geo-redundantly. If I enable SSE, will my redundant copy also be encrypted?**</span></span>

<span data-ttu-id="d8921-230">A: 예, hello 저장소 계정의 모든 복사본을 암호화 하 고 – 로컬 중복 저장소 (LRS), 영역 중복 저장소 (ZRS), 지역 중복 저장소 (GRS) 및 읽기 액세스 지역 중복 저장소 (RA-GRS) – 모든 중복 옵션이 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-230">A: Yes, all copies of hello storage account are encrypted, and all redundancy options – Locally Redundant Storage (LRS), Zone-Redundant Storage (ZRS), Geo-Redundant Storage (GRS), and Read Access Geo-Redundant Storage (RA-GRS) – are supported.</span></span>

<span data-ttu-id="d8921-231">**Q: 내 저장소 계정에서 암호화를 사용할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="d8921-231">**Q: I can't enable encryption on my storage account.**</span></span>

<span data-ttu-id="d8921-232">A: Resource Manager 저장소 계정인가요?</span><span class="sxs-lookup"><span data-stu-id="d8921-232">A: Is it a Resource Manager storage account?</span></span> <span data-ttu-id="d8921-233">클래식 저장소 계정은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-233">Classic storage accounts are not supported.</span></span> 

<span data-ttu-id="d8921-234">**Q: SSE는 특정 지역에만 허용되나요?**</span><span class="sxs-lookup"><span data-stu-id="d8921-234">**Q: Is SSE only permitted in specific regions?**</span></span>

<span data-ttu-id="d8921-235">A: hello SSE은 Blob 저장소에 대 한 모든 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-235">A: hello SSE is available in all regions for Blob storage.</span></span> <span data-ttu-id="d8921-236">파일 저장소의 가용성 섹션 hello를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d8921-236">Please check hello Availability Section for File storage.</span></span> 

<span data-ttu-id="d8921-237">**Q: 어떻게에 게 문의 합니까 누군가가 tooprovide 피드백 또는 문제가 발생 합니까?**</span><span class="sxs-lookup"><span data-stu-id="d8921-237">**Q: How do I contact someone if I have any issues or want tooprovide feedback?**</span></span>

<span data-ttu-id="d8921-238">A:에 게 문의 하십시오 [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) tooStorage 서비스 암호화 관련 된 문제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-238">A: Please contact [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) for any issues related tooStorage Service Encryption.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8921-239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8921-239">Next Steps</span></span>
<span data-ttu-id="d8921-240">Azure 저장소는 다양 한 개발자를 함께 사용 하는 보안 기능 toobuild 보안 응용 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-240">Azure Storage provides a comprehensive set of security capabilities which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="d8921-241">자세한 내용은 방문 hello [저장소 보안 가이드](../storage-security-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8921-241">For more details, visit hello [Storage Security Guide](../storage-security-guide.md).</span></span>

