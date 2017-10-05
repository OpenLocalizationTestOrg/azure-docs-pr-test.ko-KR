---
title: "Azure Security Center에서 저장소 계정에 암호화 사용 | Microsoft Docs"
description: "이 문서에서는 Azure Security Center 권장 사항 **Azure Storage 계정에 암호화 사용**을 구현하는 방법을 보여 줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: b7b2e8a12cbab68da9c8fcc348e8e3c543607007
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="b4ffc-103">Azure Security Center에서 Azure Storage 계정에 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="b4ffc-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="b4ffc-104">Azure Security Center에서는 미사용 데이터에 대한 Azure Storage 서비스 암호화를 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="b4ffc-105">SSE(Storage 서비스 암호화)는 Azure Storage에 기록되는 데이터를 암호화하고 검색 전 해당 데이터를 해독하는 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-105">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypting the data before retrieval.</span></span>  <span data-ttu-id="b4ffc-106">SSE는 현재 Azure Blob service에만 사용할 수 있으며 블록 blob, 페이지 blob 및 추가 blob에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-106">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="b4ffc-107">자세한 내용을 알아보려면 [미사용 데이터에 대한 Storage 서비스 암호화](../storage/common/storage-service-encryption.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-107">To learn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="b4ffc-108">암호화를 사용하도록 설정하면 새 데이터만 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="b4ffc-109">저장소 계정의 모든 기존 blob은 암호화되지 않은 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="b4ffc-110">기존 blob을 암호화하려면 [Storage 서비스 암호화 FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-110">To encrypt existing blobs, see the [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="b4ffc-111">Storage 서비스 암호화는 Resource Manager 저장소 계정에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="b4ffc-112">클래식 저장소 계정은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="b4ffc-113">클래식 및 Resource Manager 배포 모델을 이해하려면 [Azure 배포 모델](../azure-classic-rm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-113">To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b4ffc-114">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-114">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="b4ffc-115">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="b4ffc-116">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="b4ffc-116">Implement the recommendation</span></span>
1. <span data-ttu-id="b4ffc-117">**권장 사항** 블레이드에서 **Azure Storage 계정에 암호화 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-117">In the **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="b4ffc-118">![저장소 계정에 암호화 사용][1]</span><span class="sxs-lookup"><span data-stu-id="b4ffc-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="b4ffc-119">**저장소 암호화 사용** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-119">The **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="b4ffc-120">이 블레이드에는 저장소 암호화를 사용하지 않도록 설정된 Azure Storage 계정이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-120">This blade lists the Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="b4ffc-121">이 예제에서는 **storageacct1**을 선택해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="b4ffc-122">![저장소 암호화 사용][2]</span><span class="sxs-lookup"><span data-stu-id="b4ffc-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="b4ffc-123">**storageacct1**에 대한 **암호화** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-123">The **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="b4ffc-124">**사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-124">Select **Enabled**.</span></span>
   <span data-ttu-id="b4ffc-125">![암호화 블레이드][3]</span><span class="sxs-lookup"><span data-stu-id="b4ffc-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="b4ffc-126">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-126">Select **Save**.</span></span>

<span data-ttu-id="b4ffc-127">이제 **storageacct1**에 대한 저장소 암호화가 사용하도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="b4ffc-128">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b4ffc-128">See also</span></span>
<span data-ttu-id="b4ffc-129">이 문서에서는 Security Center 권장 사항 "Azure Storage 계정에 암호화 사용"을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-129">This document showed you how to implement the Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="b4ffc-130">Azure Storage 서비스 암호화에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-130">To learn more about Azure Storage Service Encryption, see the following:</span></span>

* [<span data-ttu-id="b4ffc-131">휴지 상태의 데이터에 대한 Azure 저장소 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="b4ffc-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="b4ffc-132">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="b4ffc-133">[Azure Security Center에서 보안 정책 설정](security-center-policies.md) - Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="b4ffc-134">[Azure Security Center에서 보안 상태 모니터링](security-center-monitoring.md) - Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="b4ffc-135">[Azure Security Center에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) - 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="b4ffc-136">[Azure Security Center에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b4ffc-137">[Azure Security Center FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="b4ffc-138">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ffc-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
