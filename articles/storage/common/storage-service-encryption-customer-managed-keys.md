---
title: "저장소 서비스 암호화 aaaAzure 관리 되는 Azure 키 자격 증명 모음의 키 고객을 사용 하 여 | Microsoft Docs"
description: "사용 하 여 hello Azure 저장소 서비스 암호화 기능 tooencrypt Azure Blob 저장소 서비스 쪽 hello hello 데이터를 저장할 때 및 관리 되는 키 고객을 사용 하 여 hello 데이터를 검색할 때 암호를 해독 합니다."
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
ms.openlocfilehash: eb2e0ad27df40e61f9c08b9db7ca7a7568adad9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a><span data-ttu-id="bfefb-103">Azure Key Vault의 고객 관리 키를 사용하는 Storage 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="bfefb-103">Storage Service Encryption using customer managed keys in Azure Key Vault</span></span>

<span data-ttu-id="bfefb-104">Microsoft Azure는 커밋된 toohelping 보호 하 고 조직의 보안 및 규정 준수 약정 데이터 toomeet를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-104">Microsoft Azure is committed toohelping you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span>  <span data-ttu-id="bfefb-105">미사용 데이터를 보호할 수는 한 가지 방법은 toouse 저장소 서비스 암호화 SSE ()를 자동으로 toostorage를 작성할 때 데이터를 암호화 하 고 가져올 때는 데이터를 해독 하는 경우</span><span class="sxs-lookup"><span data-stu-id="bfefb-105">One way you can protect your data at rest is toouse Storage Service Encryption (SSE), which automatically encrypts your data when writing it toostorage, and decrypts your data when retrieving it.</span></span> <span data-ttu-id="bfefb-106">hello 암호화 및 암호 해독 자동 완전히 투명 하 고, 256 비트를 사용 하 여 [AES 암호화](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), 사용할 수 있는 암호 hello 가장 강력한 블록 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-106">hello encryption and decryption is automatic, completely transparent, and uses 256-bit [AES encryption](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), one of hello strongest block ciphers available.</span></span>

<span data-ttu-id="bfefb-107">SSE를 사용하는 Microsoft 관리 암호화 키를 사용하거나 사용자 고유의 암호화 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-107">You can use Microsoft-managed encryption keys with SSE or you can use your own encryption keys.</span></span> <span data-ttu-id="bfefb-108">후자의 hello에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-108">This article discusses hello latter.</span></span> <span data-ttu-id="bfefb-109">Microsoft 관리 키 사용 또는 일반적인 SSE에 대한 자세한 내용은 [미사용 데이터에 대한 저장소 서비스 암호화](../storage-service-encryption.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfefb-109">For more information about using Microsoft-managed keys, or about SSE in general, see [Storage Service Encryption for Data at Rest](../storage-service-encryption.md).</span></span>

<span data-ttu-id="bfefb-110">tooprovide hello 기능 toouse SSE Blob 저장소에 대 한 직접 암호화 키를 Azure 키 자격 증명 모음 (AKV)와 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-110">tooprovide hello ability toouse your own encryption keys, SSE for Blob storage is integrated with Azure Key Vault (AKV).</span></span> <span data-ttu-id="bfefb-111">직접 암호화 키를 만들고, AKV에 저장할 수 있습니다 또는 AKV의 Api toogenerate 암호화 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-111">You can create your own encryption keys and store them in AKV, or you can use AKV’s APIs toogenerate encryption keys.</span></span> <span data-ttu-id="bfefb-112">뿐만 아니라 않습니다 AKV toomanage를 허용 하거나 키를 제어할도 가능 하면 tooaudit 키 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-112">Not only does AKV allow you toomanage and control your keys, it also enables you tooaudit your key usage.</span></span> 

<span data-ttu-id="bfefb-113">이유는 무엇 일까요 toocreate 고유한 키?</span><span class="sxs-lookup"><span data-stu-id="bfefb-113">Why would you want toocreate your own keys?</span></span> <span data-ttu-id="bfefb-114">더 큰 유연성, toocreate 수 있도록 제공, 회전, 해제 및 액세스 제어를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-114">It gives you more flexibility, allowing you toocreate, rotate, disable, and define access controls.</span></span> <span data-ttu-id="bfefb-115">Tooaudit hello 암호화 키 사용한 tooprotect 데이터 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-115">It also allows you tooaudit hello encryption keys used tooprotect your data.</span></span>

## <a name="sse-with-customer-managed-keys-preview"></a><span data-ttu-id="bfefb-116">고객 관리 키를 사용하는 SSE 미리 보기</span><span class="sxs-lookup"><span data-stu-id="bfefb-116">SSE with customer managed keys preview</span></span>

<span data-ttu-id="bfefb-117">이 기능은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-117">This feature is currently in preview.</span></span> <span data-ttu-id="bfefb-118">이 기능 toouse, toocreate 새 저장소 계정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-118">toouse this feature, you need toocreate a new storage account.</span></span> <span data-ttu-id="bfefb-119">새 키 자격 증명 모음 및 키를 만들 수도 있고 기존 키 자격 증명 모음 및 키를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-119">You can either create a new key vault and key or you can use an existing key vault and key.</span></span> <span data-ttu-id="bfefb-120">hello 저장소 계정 및 키 자격 증명 모음 hello hello에 있어야 동일한 지역의 있지만 서로 다른 구독에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-120">hello storage account and hello key vault must be in hello same region, but they can be in different subscriptions.</span></span>

<span data-ttu-id="bfefb-121">hello, 미리 보기의 연락처 tooparticipate [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com)합니다. 에서는 hello 미리 보기에서 특별 링크 tooparticipate를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-121">tooparticipate in hello preview, contact [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com). We will provide a special link tooparticipate in hello preview.</span></span>

<span data-ttu-id="bfefb-122">toolearn toohello을 더 참조 [FAQ](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest)합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-122">toolearn more, refer toohello [FAQ](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bfefb-123">이 문서의 미리 보기 이전 toofollowing hello 단계 hello에 대 한 가입 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-123">You must sign up for hello preview prior toofollowing hello steps in this article.</span></span> <span data-ttu-id="bfefb-124">미리 보기 액세스 권한이 없는 할 수 없는 수 tooenable hello 포털에서이 기능 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-124">Without preview access, you will not be able tooenable this feature in hello portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="bfefb-125">시작하기</span><span class="sxs-lookup"><span data-stu-id="bfefb-125">Getting Started</span></span>
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a><span data-ttu-id="bfefb-126">1단계: [새 저장소 계정 만들기](../storage-create-storage-account.md)</span><span class="sxs-lookup"><span data-stu-id="bfefb-126">Step 1: [Create a new storage account](../storage-create-storage-account.md)</span></span>

## <a name="step-2-enable-encryption"></a><span data-ttu-id="bfefb-127">2단계: 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="bfefb-127">Step 2: Enable encryption</span></span>
<span data-ttu-id="bfefb-128">Hello를 사용 하 여 hello 저장소 계정에 대 한 SSE를 사용할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-128">You can enable SSE for hello storage account using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bfefb-129">Hello 저장소 계정에 대 한 hello 설정 블레이드에서 다음 그림을 암호화 클릭 hello에 표시 된 대로 Blob 서비스 섹션 hello에 대 한 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-129">On hello Settings blade for hello storage account, look for hello Blob Service section as shown in hello following figure and click Encryption.</span></span>

<span data-ttu-id="bfefb-130">![암호화 옵션을 보여 주는 포털 스크린샷](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)
</span><span class="sxs-lookup"><span data-stu-id="bfefb-130">![Portal Screenshot showing Encryption option](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)
</span></span><br/><span data-ttu-id="bfefb-131">*Blob 서비스에 대해 SSE 사용*</span><span class="sxs-lookup"><span data-stu-id="bfefb-131">*Enable SSE for Blob Service*</span></span>

<span data-ttu-id="bfefb-132">Hello tooprogrammatically 사용 하려면 저장소 계정에서 저장소 서비스 암호화 hello를 사용 하지 않도록 설정 하거나, 사용할 수 있습니다 [Azure 저장소 리소스 공급자 REST API](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), hello [저장소 리소스 공급자 클라이언트 라이브러리 .NET 용](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), 또는 hello [Azure CLI](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-132">If you want tooprogrammatically enable or disable hello Storage Service Encryption on a storage account, you can use hello [Azure Storage Resource Provider REST API](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), hello [Storage Resource Provider Client Library for .NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), or hello [Azure CLI](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).</span></span>

<span data-ttu-id="bfefb-133">이 화면의 hello "your own key 사용" 확인란 표시 되지 않는 경우 하면 승인 되지 않은 hello 미리 보기에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-133">On this screen, if you can’t see hello “use your own key” checkbox, you have not been approved for hello preview.</span></span> <span data-ttu-id="bfefb-134">너무 전자 메일 보내기[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) 승인을 요청 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-134">Send an e-mail too[ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) and request approval.</span></span>

![암호화 미리 보기를 보여 주는 포털 스크린샷](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

<span data-ttu-id="bfefb-136">기본적으로 SSE는 Microsoft 관리 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-136">By default, SSE uses Microsoft managed keys.</span></span> <span data-ttu-id="bfefb-137">toouse 고유한 키 hello 상자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-137">toouse your own keys, check hello box.</span></span> <span data-ttu-id="bfefb-138">그런 다음 키 URI를 지정 하거나 hello 선택에서 키 및 키 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-138">Then you can either specify your key URI, or select a key and Key Vault from hello picker.</span></span>

## <a name="step-3-select-your-key"></a><span data-ttu-id="bfefb-139">3단계: 키 선택</span><span class="sxs-lookup"><span data-stu-id="bfefb-139">Step 3: Select your key</span></span>

![암호화 사용자 고유의 키 사용 옵션을 보여 주는 포털 스크린샷](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![키 URI 입력을 사용하는 암호화 옵션을 보여 주는 포털 스크린샷](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

<span data-ttu-id="bfefb-142">Hello 저장소 계정 액세스 toohello 주요 자격 증명 모음에 없는 경우에 hello 다음을 실행할 수 있습니다 toohello 키 자격 증명 모음 필요한 Azure Powershell toogrant 액세스 toohello 저장소 계정을 사용 하 여 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-142">If hello storage account does not have access toohello Key Vault, you can run hello following command using Azure Powershell toogrant access toohello storage accounts toohello required key vault.</span></span>

![Key Vault에 대해 거부된 액세스를 보여 주는 포털 스크린샷](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

<span data-ttu-id="bfefb-144">또한 hello Azure 포털에서에서 Azure 주요 자격 증명 모음 toohello 액세스 toohello 저장소 계정에 부여 하 여 hello Azure 포털을 통해 액세스를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-144">You can also grant access via hello Azure portal by going toohello Azure Key Vault in hello Azure portal and granting access toohello storage account.</span></span>

## <a name="step-4-copy-data-toostorage-account"></a><span data-ttu-id="bfefb-145">4 단계: 데이터 toostorage 계정 복사</span><span class="sxs-lookup"><span data-stu-id="bfefb-145">Step 4: Copy data toostorage account</span></span>
<span data-ttu-id="bfefb-146">원하는 경우 tootransfer 데이터 새 저장소 계정에 하 게 암호화 되므로, 너무 참조[단계 3의 시작 되지 않는 데이터에 대 한 저장소 서비스 암호화](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-146">If you would like tootransfer data into your new storage account so that it’s encrypted, refer too[Step 3 of Getting Started in Storage Service Encryption for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).</span></span>

## <a name="step-5-query-hello-status-of-hello-encrypted-data"></a><span data-ttu-id="bfefb-147">5 단계: hello hello 상태 쿼리 암호화 된 데이터</span><span class="sxs-lookup"><span data-stu-id="bfefb-147">Step 5: Query hello status of hello encrypted data</span></span>
<span data-ttu-id="bfefb-148">암호화 된 데이터의 hello tooquery hello 상태, 너무 참조[단계 4의 시작 되지 않는 데이터에 대 한 저장소 서비스 암호화](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-148">tooquery hello status of hello encrypted data, refer too[Step 4 of Getting Started in Storage Service Encryption for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).</span></span>

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a><span data-ttu-id="bfefb-149">미사용 데이터에 대한 저장소 서비스 암호화에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="bfefb-149">Frequently asked questions about Storage Service Encryption for Data at Rest</span></span>
<span data-ttu-id="bfefb-150">**Q: Premium Storage를 사용 중입니다. 고객 관리 키를 사용하는 SSE를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="bfefb-150">**Q: I'm using Premium storage; can I use SSE with customer managed keys?**</span></span>

<span data-ttu-id="bfefb-151">A: 예, Standard storage 및 Premium Storage 모두에서 Microsoft 관리 키 및 고객 관리 키를 사용하는 SSE가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-151">A: Yes, SSE with Microsoft-managed  and customer managed keys is supported on both Standard storage and Premium storage.</span></span> 

<span data-ttu-id="bfefb-152">**Q: Azure PowerShell 및 Azure CLI를 사용하여 고객 관리 키를 사용하는 SSE로 새 저장소 계정을 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="bfefb-152">**Q: Can I create new storage accounts with SSE with customer managed keys enabled using Azure PowerShell and Azure CLI?**</span></span>

<span data-ttu-id="bfefb-153">A: 예.</span><span class="sxs-lookup"><span data-stu-id="bfefb-153">A: Yes.</span></span>

<span data-ttu-id="bfefb-154">**Q: 고객 관리 키를 사용하는 SSE를 사용하는 경우 Azure Storage 비용은 얼마나 늘어나나요?**</span><span class="sxs-lookup"><span data-stu-id="bfefb-154">**Q: How much more does Azure Storage cost if SSE with customer managed keys is enabled?**</span></span>

<span data-ttu-id="bfefb-155">A: Azure Key Vault 사용과 연관된 비용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-155">A: There is a cost associated for using Azure Key Vault.</span></span> <span data-ttu-id="bfefb-156">자세한 내용은 [Key Vault 가격](https://azure.microsoft.com/en-us/pricing/details/key-vault/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfefb-156">For more details visit [Key Vault Pricing](https://azure.microsoft.com/en-us/pricing/details/key-vault/).</span></span> <span data-ttu-id="bfefb-157">SSE 사용에 따른 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-157">There is no additional cost for using SSE.</span></span>

<span data-ttu-id="bfefb-158">**Q: 액세스 toohello 암호화 키 취소 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="bfefb-158">**Q: Can I revoke access toohello encryption keys?**</span></span>

<span data-ttu-id="bfefb-159">A: 예, 언제든 액세스를 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-159">A: Yes, you can revoke access at any time.</span></span> <span data-ttu-id="bfefb-160">여러 가지 방법으로 toorevoke 액세스 tooyour 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-160">There are several ways toorevoke access tooyour keys.</span></span> <span data-ttu-id="bfefb-161">너무 참조[Azure 키 자격 증명 모음 PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) 및 [Azure 키 자격 증명 모음 CLI](https://docs.microsoft.com/en-us/cli/azure/keyvault) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-161">Refer too[Azure Key Vault PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) and [Azure Key Vault CLI](https://docs.microsoft.com/en-us/cli/azure/keyvault) for more details.</span></span> <span data-ttu-id="bfefb-162">Hello 계정 암호화 키가 Azure 저장소에서 액세스할 수 없어서 액세스 권한을 취소할 hello 저장소 계정에 대 한 액세스 tooall blob 효과적으로 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-162">Revoking access will effectively block access tooall blobs in hello storage account as hello Account Encryption Key is inaccessible by Azure Storage.</span></span>

<span data-ttu-id="bfefb-163">**Q: 저장소 계정 및 키를 다른 지역에 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="bfefb-163">**Q: Can I create a storage account and key in different region?**</span></span>

<span data-ttu-id="bfefb-164">A: 아니요, hello 저장소 계정 및 키 자격 증명 모음/키 필요 toobe에 hello 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-164">A: No, hello storage account and key vault/key need toobe in hello same region.</span></span> 

<span data-ttu-id="bfefb-165">**Q: 사용할 수 있습니까 SSE 고객 관리 키를 가진 hello 저장소 계정을 만드는 동안?**</span><span class="sxs-lookup"><span data-stu-id="bfefb-165">**Q: Can I enable SSE with customer managed keys while creating hello storage account?**</span></span>

<span data-ttu-id="bfefb-166">A: 아니요.</span><span class="sxs-lookup"><span data-stu-id="bfefb-166">A: No.</span></span> <span data-ttu-id="bfefb-167">SSE hello 저장소 계정을 만드는 동안 설정한 경우에 Microsoft 관리 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-167">When you enable SSE while creating hello storage account, you can only use Microsoft managed keys.</span></span> <span data-ttu-id="bfefb-168">Toouse 고객 관리 키를 선택 하는 경우에 hello 저장소 계정 속성을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-168">If you would like toouse customer managed keys, you must update hello storage account properties.</span></span> <span data-ttu-id="bfefb-169">REST를 사용할 수 있습니다 또는 저장소 계정의 업데이트 hello 저장소 클라이언트 라이브러리 tooprogrammatically 중 하나 또는 hello 계정을 만든 후 hello Azure 포털을 사용 하 여 hello 저장소 계정 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-169">You can use REST or one of hello storage client libraries tooprogrammatically update your storage account, or update hello storage account properties using hello Azure portal after creating hello account.</span></span>

<span data-ttu-id="bfefb-170">**Q: 고객 관리 키를 사용하는 SSE를 사용하면서 암호화를 사용하지 않을 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="bfefb-170">**Q: Can I disable encryption while using SSE with customer managed keys?**</span></span>

<span data-ttu-id="bfefb-171">A: 아니요, 고객 관리 키를 사용하는 SSE를 사용하면서 암호화를 사용하지 않을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-171">A: No, you cannot disable encryption while using SSE with customer managed keys.</span></span> <span data-ttu-id="bfefb-172">toodisable 암호화 toousing Microsoft 관리 키를 전환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-172">toodisable encryption, you must switch toousing Microsoft managed keys.</span></span> <span data-ttu-id="bfefb-173">Hello Azure 포털 또는 PowerShell을 사용 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-173">You can do this using either hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="bfefb-174">**Q: 새 저장소 계정을 만들 때 기본적으로 SSE가 사용되도록 설정되어 있나요?**</span><span class="sxs-lookup"><span data-stu-id="bfefb-174">**Q: Is SSE enabled by default when I create a new storage account?**</span></span>

<span data-ttu-id="bfefb-175">A: SSE 기본적으로 사용 되지 않습니다. Azure 포털 tooenable hello를 사용할 수 있습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-175">A: SSE is not enabled by default; you can use hello Azure portal tooenable it.</span></span> <span data-ttu-id="bfefb-176">또한 프로그래밍 방식으로 hello 저장소 리소스 공급자 REST API를 사용 하 여이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-176">You can also programmatically enable this feature using hello Storage Resource Provider REST API.</span></span> 

<span data-ttu-id="bfefb-177">**Q: 내 저장소 계정에서 암호화를 사용할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="bfefb-177">**Q: I can't enable encryption on my storage account.**</span></span>

<span data-ttu-id="bfefb-178">A: Resource Manager 저장소 계정인가요?</span><span class="sxs-lookup"><span data-stu-id="bfefb-178">A: Is it a Resource Manager storage account?</span></span> <span data-ttu-id="bfefb-179">클래식 저장소 계정은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-179">Classic storage accounts are not supported.</span></span> <span data-ttu-id="bfefb-180">고객 관리 키를 사용하는 SSE는 새로 만든 리소스 관리자 저장소 계정에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-180">SSE with customer managed keys can also be enabled only on newly created Resource Manager storage accounts.</span></span>

<span data-ttu-id="bfefb-181">**Q: 고객 관리 키를 사용하는 SSE는 특정 지역에서만 허용되나요?**</span><span class="sxs-lookup"><span data-stu-id="bfefb-181">**Q: Is SSE with customer managed keys only permitted in specific regions?**</span></span>

<span data-ttu-id="bfefb-182">A: 이 미리 보기의 경우 Blob storage에 대한 SSE는 특정 지역에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-182">A: SSE is available in only certain regions for Blob storage for this Preview.</span></span> <span data-ttu-id="bfefb-183">전자 메일 [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) toocheck 가용성 및 미리 보기에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-183">Email [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) toocheck for availability and details on preview.</span></span> 

<span data-ttu-id="bfefb-184">**Q: 어떻게에 게 문의 합니까 누군가가 tooprovide 피드백 또는 문제가 발생 합니까?**</span><span class="sxs-lookup"><span data-stu-id="bfefb-184">**Q: How do I contact someone if I have any issues or want tooprovide feedback?**</span></span>

<span data-ttu-id="bfefb-185">A: 연락처 [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) tooStorage 서비스 암호화 관련 된 문제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-185">A: Contact [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) for any issues related tooStorage Service Encryption.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bfefb-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bfefb-186">Next steps</span></span>

*   <span data-ttu-id="bfefb-187">Hello 다양 한 보안에 대 한 자세한 내용은 개발자 기능 보안 응용 프로그램 작성, hello 참조 [저장소 보안 가이드](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide)합니다.</span><span class="sxs-lookup"><span data-stu-id="bfefb-187">For more information on hello comprehensive set of security capabilities that help developers build secure applications, see hello [Storage Security Guide](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).</span></span>
*   <span data-ttu-id="bfefb-188">Azure Key Vault에 대한 개요는 [Azure Key Vault란](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)?을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfefb-188">For overview information about Azure Key Vault, see [What is Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)?</span></span>
*   <span data-ttu-id="bfefb-189">Azure Key Vault 시작 방법은 [Azure Key Vault 시작](../../key-vault/key-vault-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfefb-189">For getting started on Azure Key Vault, see [Getting Started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>
