---
title: "Azure Key Vault의 고객 관리 키를 사용하는 Azure Storage 서비스 암호화 | Microsoft Docs"
description: "Azure Storage 서비스 암호화 기능을 사용하여 데이터를 저장할 때 서비스 쪽에서 Azure Blob Storage를 암호화하고 고객 관리 키를 사용하여 데이터를 검색할 때 암호 해독합니다."
services: storage
documentationcenter: .net
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: lakasa
ms.openlocfilehash: b596cf1a98a9c6f42c3bbee9cc27608549e2b5ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a><span data-ttu-id="8f0c8-103">Azure Key Vault의 고객 관리 키를 사용하는 Storage 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="8f0c8-103">Storage Service Encryption using customer managed keys in Azure Key Vault</span></span>

<span data-ttu-id="8f0c8-104">Microsoft Azure는 고객 조직의 보안 및 규정 준수 약정에 맞게 데이터를 보호하도록 지원하는 데 최선을 다하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-104">Microsoft Azure is strongly committed to helping you protect and safeguard your data to meet your organizational security and compliance commitments.</span></span>  <span data-ttu-id="8f0c8-105">미사용 데이터를 보호할 수 있는 한 가지 방법은 자동으로 데이터를 저장소에 쓸 때 암호화하고 데이터를 검색할 때 암호 해독하는 SSE(저장소 서비스 암호화)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-105">One way you can protect your data at rest is to use Storage Service Encryption (SSE), which automatically encrypts your data when writing it to storage, and decrypts your data when retrieving it.</span></span> <span data-ttu-id="8f0c8-106">암호화 및 암호 해독은 자동으로 적용되며 완전히 투명하고, 사용 가능한 가장 강력한 블록 암호 중 하나인 256비트 [AES 암호화](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-106">The encryption and decryption is automatic and completely transparent and uses 256-bit [AES encryption](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), one of the strongest block ciphers available.</span></span>

<span data-ttu-id="8f0c8-107">SSE를 사용하는 Microsoft 관리 암호화 키를 사용하거나 사용자 고유의 암호화 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-107">You can use Microsoft-managed encryption keys with SSE or you can use your own encryption keys.</span></span> <span data-ttu-id="8f0c8-108">이 문서에서는 사용자 고유의 암호화 키 사용 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-108">This article will talk about the latter.</span></span> <span data-ttu-id="8f0c8-109">Microsoft 관리 키 사용 또는 일반적인 SSE에 대한 자세한 내용은 [미사용 데이터에 대한 저장소 서비스 암호화](storage-service-encryption.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-109">For more information about using Microsoft-managed keys, or about SSE in general, please see [Storage Service Encryption for Data at Rest](storage-service-encryption.md).</span></span>

<span data-ttu-id="8f0c8-110">사용자 고유의 암호화 키 사용 기능을 제공하기 위해 Blob 저장소에 대한 SSE가 AKV(Azure Key Vault)와 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-110">To provide the ability to use your own encryption keys, SSE for Blob storage is integrated with Azure Key Vault (AKV).</span></span> <span data-ttu-id="8f0c8-111">사용자 고유의 암호화 키를 만들고 AKV에 저장할 수도 있고 AKV의 API를 사용하여 암호화 키를 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-111">You can create your own encryption keys and store them in AKV, or you can use AKV’s APIs to generate encryption keys.</span></span> <span data-ttu-id="8f0c8-112">AKV를 사용하면 키를 관리하고 제어할 수 있을 뿐만 아니라 키 사용을 감사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-112">Not only does AKV allow you to manage and control your keys, it also enables you to audit your key usage.</span></span> 

<span data-ttu-id="8f0c8-113">사용자 고유의 키를 만드는 이유</span><span class="sxs-lookup"><span data-stu-id="8f0c8-113">Why would you want to create your own keys?</span></span> <span data-ttu-id="8f0c8-114">액세스 제어를 만들고, 회전하고, 사용하지 않도록 설정하고, 정의하는 기능과 데이터 보호에 사용되는 암호화 키를 감사하는 기능을 비롯하여 뛰어난 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-114">It gives you more flexibility, including the ability to create, rotate, disable, and define access controls, and to audit the encryption keys used to protect your data.</span></span>

## <a name="sse-with-customer-managed-keys-preview"></a><span data-ttu-id="8f0c8-115">고객 관리 키를 사용하는 SSE 미리 보기</span><span class="sxs-lookup"><span data-stu-id="8f0c8-115">SSE with customer managed keys preview</span></span>

<span data-ttu-id="8f0c8-116">이 기능은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-116">This feature is currently in preview.</span></span> <span data-ttu-id="8f0c8-117">이 기능을 사용하려면 새 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-117">To use this feature, you need to create a new storage account.</span></span> <span data-ttu-id="8f0c8-118">새 키 자격 증명 모음 및 키를 만들 수도 있고 기존 키 자격 증명 모음 및 키를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-118">You can either create a new key vault and key or you can use an existing key vault and key.</span></span> <span data-ttu-id="8f0c8-119">저장소 계정 및 키 자격 증명 모음은 동일한 지역에 있어야 하지만 서로 다른 구독에 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-119">The storage account and the key vault must be in the same region, but they can be in different subscriptions.</span></span>

<span data-ttu-id="8f0c8-120">미리 보기에 참여하려면 [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-120">To participate in the preview please contact [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com).</span></span> <span data-ttu-id="8f0c8-121">미리 보기에 참여할 특별 링크를 제공해 드립니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-121">We will provide a special link to participate in the preview.</span></span>

<span data-ttu-id="8f0c8-122">자세히 알아보려면 [FAQ](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-122">To learn more, please refer to the [FAQ](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8f0c8-123">이 문서의 단계를 수행하기 전에 미리 보기에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-123">You must sign up for the preview prior to following the steps in this article.</span></span> <span data-ttu-id="8f0c8-124">미리 보기 액세스 권한이 없는 경우 포털에서 이 기능을 사용하도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-124">Without preview access, you will not be able to enable this feature in the portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8f0c8-125">시작하기</span><span class="sxs-lookup"><span data-stu-id="8f0c8-125">Getting Started</span></span>
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a><span data-ttu-id="8f0c8-126">1단계: [새 저장소 계정 만들기](storage-create-storage-account.md)</span><span class="sxs-lookup"><span data-stu-id="8f0c8-126">Step 1: [Create a new storage account](storage-create-storage-account.md)</span></span>

## <a name="step-2-enable-encryption"></a><span data-ttu-id="8f0c8-127">2단계: 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="8f0c8-127">Step 2: Enable encryption</span></span>
<span data-ttu-id="8f0c8-128">[Azure Portal](https://portal.azure.com)을 사용하여 저장소 계정에 대해 SSE를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-128">You can enable SSE for the storage account using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8f0c8-129">저장소 계정의 설정 블레이드에서 아래 그림에 표시된 것처럼 Blob 서비스 섹션을 찾은 후 [암호화]를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-129">On the Settings blade for the storage account, look for the Blob Service section as shown in figure below and click Encryption.</span></span>

<span data-ttu-id="8f0c8-130">![암호화 옵션을 보여 주는 포털 스크린샷](./media/storage-service-encryption/image1.png)
</span><span class="sxs-lookup"><span data-stu-id="8f0c8-130">![Portal Screenshot showing Encryption option](./media/storage-service-encryption/image1.png)
</span></span><br/><span data-ttu-id="8f0c8-131">*Blob 서비스에 대해 SSE 사용*</span><span class="sxs-lookup"><span data-stu-id="8f0c8-131">*Enable SSE for Blob Service*</span></span>

<span data-ttu-id="8f0c8-132">저장소 계정에 대해 저장소 서비스 암호화를 프로그래밍 방식으로 사용 또는 사용하지 않으려면 [Azure Storage Resource Provider REST API](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), [.NET용 Storage Resource Provider 클라이언트 라이브러리](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0) 또는 [Azure CLI](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli)를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-132">If you want to programmatically enable or disable the Storage Service Encryption on a storage account, you can use the [Azure Storage Resource Provider REST API](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), the [Storage Resource Provider Client Library for .NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), or the [Azure CLI](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).</span></span>

<span data-ttu-id="8f0c8-133">이 화면에서 "use your own key"(사용자 고유 키 사용) 확인란이 표시되지 않는 경우 미리 보기가 승인되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-133">On this screen, if you can’t see the “use your own key” checkbox, you have not been approved for the preview.</span></span> <span data-ttu-id="8f0c8-134">[ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com)으로 메일을 보내 승인을 요청해 주세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-134">Please send an e-mail to [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) and request approval.</span></span>

![암호화 미리 보기를 보여 주는 포털 스크린샷](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

<span data-ttu-id="8f0c8-136">기본적으로 SSE는 Microsoft 관리 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-136">By default, SSE will use Microsoft managed keys.</span></span> <span data-ttu-id="8f0c8-137">사용자 고유의 키를 사용하려면 해당 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-137">To use your own keys, check the box.</span></span> <span data-ttu-id="8f0c8-138">그런 다음 키 URI를 지정하거나 선택기에서 키 및 Key Vault를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-138">Then you can either specify your key URI, or select a key and Key Vault from the picker.</span></span>

## <a name="step-3-select-your-key"></a><span data-ttu-id="8f0c8-139">3단계: 키 선택</span><span class="sxs-lookup"><span data-stu-id="8f0c8-139">Step 3: Select your key</span></span>

![암호화 사용자 고유의 키 사용 옵션을 보여 주는 포털 스크린샷](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![키 URI 입력을 사용하는 암호화 옵션을 보여 주는 포털 스크린샷](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

<span data-ttu-id="8f0c8-142">저장소 계정에 Key Vault에 대한 액세스 권한이 없는 경우 Azure Powershell을 통해 다음 명령을 실행하여 필요한 Key Vault에 대한 액세스 권한을 저장소 계정에 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-142">If the storage account does not have access to the Key Vault, you can run the following command using Azure Powershell to grant access to the storage accounts to the required key vault.</span></span>

![Key Vault에 대해 거부된 액세스를 보여 주는 포털 스크린샷](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

<span data-ttu-id="8f0c8-144">또한 Azure Portal에서 Azure Key Vault로 이동하여 저장소 계정에 액세스 권한을 부여하는 방법으로 Azure Portal을 통해 액세스 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-144">You can also grant access via the Azure portal by going to the Azure Key Vault in the Azure portal and granting access to the storage account.</span></span>

## <a name="step-4-copy-data-to-storage-account"></a><span data-ttu-id="8f0c8-145">4단계: 저장소 계정에 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="8f0c8-145">Step 4: Copy data to storage account</span></span>
<span data-ttu-id="8f0c8-146">새 저장소 계정으로 데이터를 전송하여 암호화되도록 하려면 [3단계의 미사용 데이터에 대한 저장소 서비스 암호화에서 시작](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-146">If you would like to transfer data into your new storage account so that it’s encrypted, please refer to [Step 3 of Getting Started in Storage Service Encryption for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).</span></span>

## <a name="step-5-query-the-status-of-the-encrypted-data"></a><span data-ttu-id="8f0c8-147">5단계: 암호화된 데이터 상태 쿼리</span><span class="sxs-lookup"><span data-stu-id="8f0c8-147">Step 5: Query the status of the encrypted data</span></span>
<span data-ttu-id="8f0c8-148">암호화된 데이터 상태를 쿼리하려면 [4단계의 미사용 데이터에 대한 저장소 서비스 암호화에서 시작](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-148">To query the status of the encrypted data please refer to [Step 4 of Getting Started in Storage Service Encryption for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).</span></span>

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a><span data-ttu-id="8f0c8-149">미사용 데이터에 대한 저장소 서비스 암호화에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="8f0c8-149">Frequently asked questions about Storage Service Encryption for Data at Rest</span></span>
<span data-ttu-id="8f0c8-150">**Q: Premium Storage를 사용 중입니다. 고객 관리 키를 사용하는 SSE를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8f0c8-150">**Q: I'm using Premium storage; can I use SSE with customer managed keys?**</span></span>

<span data-ttu-id="8f0c8-151">A: 예, Standard storage 및 Premium Storage 모두에서 Microsoft 관리 키 및 고객 관리 키를 사용하는 SSE가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-151">A: Yes, SSE with Microsoft-managed  and customer managed keys is supported on both Standard storage and Premium storage.</span></span> 

<span data-ttu-id="8f0c8-152">**Q: Azure PowerShell 및 Azure CLI를 사용하여 고객 관리 키를 사용하는 SSE로 새 저장소 계정을 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8f0c8-152">**Q: Can I create new storage accounts with SSE with customer managed keys enabled using Azure PowerShell and Azure CLI?**</span></span>

<span data-ttu-id="8f0c8-153">A: 예.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-153">A: Yes.</span></span>

<span data-ttu-id="8f0c8-154">**Q: 고객 관리 키를 사용하는 SSE를 사용하는 경우 Azure Storage 비용은 얼마나 늘어나나요?**</span><span class="sxs-lookup"><span data-stu-id="8f0c8-154">**Q: How much more does Azure Storage cost if SSE with customer managed keys is enabled?**</span></span>

<span data-ttu-id="8f0c8-155">A: Azure Key Vault 사용과 연관된 비용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-155">A: There is a cost associated for using Azure Key Vault.</span></span> <span data-ttu-id="8f0c8-156">자세한 내용은 [Key Vault 가격](https://azure.microsoft.com/en-us/pricing/details/key-vault/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-156">For more details visit [Key Vault Pricing](https://azure.microsoft.com/en-us/pricing/details/key-vault/).</span></span> <span data-ttu-id="8f0c8-157">SSE 사용에 따른 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-157">There is no additional cost for using SSE.</span></span>

<span data-ttu-id="8f0c8-158">**Q: 암호화 키에 대한 액세스를 해지할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8f0c8-158">**Q: Can I revoke access to the encryption keys?**</span></span>

<span data-ttu-id="8f0c8-159">A: 예, 언제든 액세스를 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-159">A: Yes, you can revoke access at any time.</span></span> <span data-ttu-id="8f0c8-160">키에 대한 액세스를 취소하는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-160">There are several ways to revoke access to your keys.</span></span> <span data-ttu-id="8f0c8-161">자세한 내용은 [Azure Key Vault PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) 및 [Azure Key Vault CLI](https://docs.microsoft.com/en-us/cli/azure/keyvault)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-161">Please refer to [Azure Key Vault PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) and [Azure Key Vault CLI](https://docs.microsoft.com/en-us/cli/azure/keyvault) for more details.</span></span> <span data-ttu-id="8f0c8-162">액세스를 취소하면 Azure Storage에서 계정 암호화 키에 액세스할 수 없으므로 저장소 계정의 모든 Blob에 대한 액세스가 효과적으로 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-162">Revoking access will effectively block access to all blobs in the storage account as the Account Encryption Key is inaccessible by Azure Storage.</span></span>

<span data-ttu-id="8f0c8-163">**Q: 저장소 계정 및 키를 다른 지역에 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8f0c8-163">**Q: Can I create a storage account and key in different region?**</span></span>

<span data-ttu-id="8f0c8-164">A: 아니요, 저장소 계정 및 Key Vault/키는 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-164">A: No, the storage account and key vault/key need to be in the same region.</span></span> 

<span data-ttu-id="8f0c8-165">**Q: 저장소 계정을 만들면서 고객 관리 키를 사용하는 SSE를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8f0c8-165">**Q: Can I enable SSE with customer managed keys while creating the storage account?**</span></span>

<span data-ttu-id="8f0c8-166">A: 아니요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-166">A: No.</span></span> <span data-ttu-id="8f0c8-167">저장소 계정을 만들면서 SSE를 사용하는 경우 Microsoft 관리 키만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-167">When you enable SSE while creating the storage account, you can only use Microsoft managed keys.</span></span> <span data-ttu-id="8f0c8-168">고객 관리 키를 사용하려면 저장소 계정 속성을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-168">If you would like to use customer managed keys you will need to update the storage account properties.</span></span> <span data-ttu-id="8f0c8-169">REST 또는 저장소 클라이언트 라이브러리 중 하나를 사용하여 프로그래밍 방식으로 저장소 계정을 업데이트하거나 계정을 만든 후 Azure Portal을 사용하여 저장소 계정 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-169">You can use REST or one of the storage client libraries to programmatically update your storage account, or update the storage account properties using the Azure Portal after creating the account.</span></span>

<span data-ttu-id="8f0c8-170">**Q: 고객 관리 키를 사용하는 SSE를 사용하면서 암호화를 사용하지 않을 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8f0c8-170">**Q: Can I disable encryption while using SSE with customer managed keys?**</span></span>

<span data-ttu-id="8f0c8-171">A: 아니요, 고객 관리 키를 사용하는 SSE를 사용하면서 암호화를 사용하지 않을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-171">A: No, you cannot disable encryption while using SSE with customer managed keys.</span></span> <span data-ttu-id="8f0c8-172">암호화를 사용하지 않으려면 Microsoft 관리 키를 사용하도록 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-172">To disable encryption, you will need to switch to using Microsoft managed keys.</span></span> <span data-ttu-id="8f0c8-173">이 작업은 Azure Portal 또는 PowerShell을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-173">You can do this using either the Azure portal or PowerShell.</span></span>

<span data-ttu-id="8f0c8-174">**Q: 새 저장소 계정을 만들 때 기본적으로 SSE가 사용되도록 설정되어 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8f0c8-174">**Q: Is SSE enabled by default when I create a new storage account?**</span></span>

<span data-ttu-id="8f0c8-175">A: SSE는 기본적으로 사용되지 않습니다. Azure 포털로 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-175">A: SSE is not enabled by default; you can use the Azure portal to enable it.</span></span> <span data-ttu-id="8f0c8-176">또한 프로그래밍 방식으로 저장소 리소스 공급자 REST API를 사용하여 이 기능을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-176">You can also programmatically enable this feature using the Storage Resource Provider REST API.</span></span> 

<span data-ttu-id="8f0c8-177">**Q: 내 저장소 계정에서 암호화를 사용할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="8f0c8-177">**Q: I can't enable encryption on my storage account.**</span></span>

<span data-ttu-id="8f0c8-178">A: Resource Manager 저장소 계정인가요?</span><span class="sxs-lookup"><span data-stu-id="8f0c8-178">A: Is it a Resource Manager storage account?</span></span> <span data-ttu-id="8f0c8-179">클래식 저장소 계정은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-179">Classic storage accounts are not supported.</span></span> <span data-ttu-id="8f0c8-180">고객 관리 키를 사용하는 SSE는 새로 만든 리소스 관리자 저장소 계정에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-180">SSE with customer managed keys can also be enabled only on newly created Resource Manager storage accounts.</span></span>

<span data-ttu-id="8f0c8-181">**Q: 고객 관리 키를 사용하는 SSE는 특정 지역에서만 허용되나요?**</span><span class="sxs-lookup"><span data-stu-id="8f0c8-181">**Q: Is SSE with customer managed keys only permitted in specific regions?**</span></span>

<span data-ttu-id="8f0c8-182">A: 이 미리 보기의 경우 Blob storage에 대한 SSE는 특정 지역에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-182">A: SSE is available in only certain regions for Blob storage for this Preview.</span></span> <span data-ttu-id="8f0c8-183">미리 보기에 대한 세부 정보와 가용성을 확인하려면 [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com)으로 메일을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-183">Please email [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) to check for availability and details on preview.</span></span> 

<span data-ttu-id="8f0c8-184">**Q: 문제가 있거나 피드백을 제공하고 싶은 경우 어떻게 연락하나요?**</span><span class="sxs-lookup"><span data-stu-id="8f0c8-184">**Q: How do I contact someone if I have any issues or want to provide feedback?**</span></span>

<span data-ttu-id="8f0c8-185">A: 저장소 서비스 암호화에 대한 문제는 [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) 으로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-185">A: Please contact [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) for any issues related to Storage Service Encryption.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8f0c8-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f0c8-186">Next steps</span></span>

*   <span data-ttu-id="8f0c8-187">개발자가 보안 응용 프로그램을 빌드하는 데 도움이 되는 포괄적인 보안 기능 집합에 대한 자세한 내용은 [Storage 보안 가이드](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-187">For more information on the comprehensive set of security capabilities that help developers build secure applications, please see the [Storage Security Guide](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).</span></span>
*   <span data-ttu-id="8f0c8-188">Azure Key Vault에 대한 개요는 [Azure Key Vault란](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)?을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-188">For overview information about Azure Key Vault, see [What is Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)?</span></span>
*   <span data-ttu-id="8f0c8-189">Azure Key Vault 시작 방법은 [Azure Key Vault 시작](../key-vault/key-vault-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f0c8-189">For getting started on Azure Key Vault, see [Getting Started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
