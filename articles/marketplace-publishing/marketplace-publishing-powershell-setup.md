---
title: "Marketplace에 대한 VM을 만들기 위해 PowerShell 설정 | Microsoft Docs"
description: "Azure PowerShell을 설정하고 선택적 프로세스 흐름으로 사용하여 Azure 마켓플레이스에 배포하고 여기에서 판매할 VM 이미지를 만들기 위한 지침"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: bbcce5093d2bbd5326523063db7d0e565fe4de6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-powershell-to-create-an-offer-for-the-azure-marketplace"></a><span data-ttu-id="5ac0d-103">Azure 마켓플레이스에 대한 제품을 만들기 위한 Azure PowerShell 설정</span><span class="sxs-lookup"><span data-stu-id="5ac0d-103">Set up Azure PowerShell to create an offer for the Azure Marketplace</span></span>
<span data-ttu-id="5ac0d-104">Azure에서 PowerShell을 설정하는 방법에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-104">For detailed information on how to set up PowerShell in Azure, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="5ac0d-105">간단한 방법은 인증 방법을 사용하는 것으로, 인증에 필요한 인증서를 다운로드하고 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-105">A simple approach is to use the certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="5ac0d-106">필요한 인증서를 가져오려면 **Get-AzurePublishSettingsFile** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-106">To obtain the needed certificate, use the **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="5ac0d-107">메시지가 나타나면 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-107">Save the file when you're prompted.</span></span> <span data-ttu-id="5ac0d-108">인증서를 PowerShell 세션으로 가져오려면 **Import-AzurePublishSettingsFile** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-108">To import the certificate into a PowerShell session, use the **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="5ac0d-109">PowerShell 세션에 대한 일반적인 Microsoft Azure 구독 설정을 구성하고 저장하려면 **Set-AzureSubscription** 및 **Select-AzureSubscription** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-109">To configure and store the common Microsoft Azure subscription settings for the PowerShell session, use the **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="5ac0d-110">첫 번째 명령은 기본 저장소 계정을 구독에 연결합니다(일부 VM 프로비저닝 작업에 필요).</span><span class="sxs-lookup"><span data-stu-id="5ac0d-110">The first command associates a default storage account with the subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="5ac0d-111">두 번째 명령은 구독을 현재 구독으로 만듭니다(다른 cmdlet에서 인식).</span><span class="sxs-lookup"><span data-stu-id="5ac0d-111">The second makes the subscription the current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="5ac0d-112">참고 항목</span><span class="sxs-lookup"><span data-stu-id="5ac0d-112">See also</span></span>
* [<span data-ttu-id="5ac0d-113">시작: Azure 마켓플레이스에 제품을 게시하는 방법</span><span class="sxs-lookup"><span data-stu-id="5ac0d-113">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="5ac0d-114">마켓플레이스에 대한 가상 컴퓨터 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="5ac0d-114">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

