---
title: "Azure 보안 센터의 저장소 계정에 대 한 aaaEnable 암호화 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 암호화에 대 한 Azure 저장소 계정 * *를 사용 합니다."
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
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="83ed6-103">Azure Security Center에서 Azure Storage 계정에 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="83ed6-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="83ed6-104">Azure Security Center에서는 미사용 데이터에 대한 Azure Storage 서비스 암호화를 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="83ed6-105">저장소 서비스 암호화 (SSE) 검색 하기 전에 hello 데이터 tooAzure 저장소 쓰일 때 hello 데이터를 암호화 및 해독 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-105">Storage Service Encryption (SSE) works by encrypting hello data when it is written tooAzure storage and decrypting hello data before retrieval.</span></span>  <span data-ttu-id="83ed6-106">SSE는 hello Azure Blob 서비스에 대 한 현재 사용할 수 및 블록 blob의 페이지 blob 사용할 수 있으며 추가 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-106">SSE is currently available only for hello Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="83ed6-107">toolearn 더 참조 [미사용 데이터에 대 한 저장소 서비스 암호화](../storage/common/storage-service-encryption.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-107">toolearn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="83ed6-108">암호화를 사용하도록 설정하면 새 데이터만 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="83ed6-109">저장소 계정의 모든 기존 blob은 암호화되지 않은 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="83ed6-110">tooencrypt 기존 blob 참조 hello [저장소 서비스 암호화 FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest)합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-110">tooencrypt existing blobs, see hello [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="83ed6-111">Storage 서비스 암호화는 Resource Manager 저장소 계정에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="83ed6-112">클래식 저장소 계정은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="83ed6-113">클래식 toounderstand hello 및 리소스 관리자 배포 모델 참조 [Azure 배포 모델](../azure-classic-rm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-113">toounderstand hello classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="83ed6-114">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-114">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="83ed6-115">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="83ed6-116">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="83ed6-116">Implement hello recommendation</span></span>
1. <span data-ttu-id="83ed6-117">Hello에 **권장 사항을** 블레이드를 **Azure 저장소 계정에 대 한 암호화를 사용 하도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-117">In hello **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="83ed6-118">![저장소 계정에 암호화 사용][1]</span><span class="sxs-lookup"><span data-stu-id="83ed6-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="83ed6-119">hello **저장소 암호화 사용** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-119">hello **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="83ed6-120">이 블레이드는 hello Azure 저장소 계정의 저장소 암호화를 해제 하는 위치를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-120">This blade lists hello Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="83ed6-121">이 예제에서는 **storageacct1**을 선택해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="83ed6-122">![저장소 암호화 사용][2]</span><span class="sxs-lookup"><span data-stu-id="83ed6-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="83ed6-123">hello **암호화** 블레이드 **storageacct1** 열립니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-123">hello **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="83ed6-124">**사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-124">Select **Enabled**.</span></span>
   <span data-ttu-id="83ed6-125">![암호화 블레이드][3]</span><span class="sxs-lookup"><span data-stu-id="83ed6-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="83ed6-126">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-126">Select **Save**.</span></span>

<span data-ttu-id="83ed6-127">이제 **storageacct1**에 대한 저장소 암호화가 사용하도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="83ed6-128">참고 항목</span><span class="sxs-lookup"><span data-stu-id="83ed6-128">See also</span></span>
<span data-ttu-id="83ed6-129">이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 사항 "Enable 암호화 Azure 저장소 계정에 대 한 합니다."</span><span class="sxs-lookup"><span data-stu-id="83ed6-129">This document showed you how tooimplement hello Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="83ed6-130">Azure 저장소 서비스 암호화에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-130">toolearn more about Azure Storage Service Encryption, see hello following:</span></span>

* [<span data-ttu-id="83ed6-131">휴지 상태의 데이터에 대한 Azure 저장소 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="83ed6-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="83ed6-132">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="83ed6-133">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="83ed6-134">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="83ed6-135">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="83ed6-136">[Azure Security Center에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="83ed6-137">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="83ed6-138">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed6-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
