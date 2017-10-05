---
title: "Azure Security Center에서 디스크 암호화 적용 | Microsoft Docs"
description: "이 문서에서는 보안 센터 권장 사항 **디스크 암호화 적용**을 구현하는 방법을 보여줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 67cff664f3723b2194ecd1519729cca17069d07f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a><span data-ttu-id="7a929-103">Azure 보안 센터에서 디스크 암호화 적용</span><span class="sxs-lookup"><span data-stu-id="7a929-103">Apply disk encryption in Azure Security Center</span></span>
<span data-ttu-id="7a929-104">Azure Security Center는 암호화되지 않은 Windows 또는 Linux VM 디스크가 있는 경우 Azure Disk Encryption을 사용하여 디스크 암호화를 적용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-104">Azure Security Center recommends that you apply disk encryption if you have Windows or Linux VM disks that are not encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="7a929-105">디스크 암호화를 사용하면 Windows 및 Linux IaaS VM 디스크를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-105">Disk Encryption lets you encrypt your Windows and Linux IaaS VM disks.</span></span>  <span data-ttu-id="7a929-106">VM에서 OS 및 데이터 볼륨에 암호화를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-106">Encryption is recommended for both the OS and data volumes on your VM.</span></span>

<span data-ttu-id="7a929-107">디스크 암호화는 업계 표준인 Windows의 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) 기능과 Linux의 [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-107">Disk Encryption uses the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux.</span></span> <span data-ttu-id="7a929-108">이러한 기능은 데이터를 보호하고 조직의 보안 및 규정 준수 요구 사항을 충족하는 데 도움이 되는 OS 및 데이터 암호화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-108">These features provide OS and data encryption to help protect and safeguard your data and meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="7a929-109">디스크 암호화는 [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/)와 함께 통합되어 주요 자격 증명 모음 구독에서 디스크 암호화 키 및 암호를 제어하고 관리할 수 있도록 하며 VM 디스크의 모든 휴지 상태 데이터가 [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)에서 암호화되도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-109">Disk Encryption is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk encryption keys and secrets in your Key Vault subscription, while ensuring that all data in the VM disks are encrypted at rest in your [Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span></span>

> [!NOTE]
> <span data-ttu-id="7a929-110">Azure 디스크 암호화는 Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2와 같은 Windows Server 운영 체제에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-110">Azure Disk Encryption is supported on the following Windows server operating systems - Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span> <span data-ttu-id="7a929-111">디스크 암호화는 Ubuntu, CentOS, SUSE 및 SLES(SUSE Linux Enterprise Server)와 같은 Linux Server 운영 체제에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-111">Disk encryption is supported on the following Linux server operating systems - Ubuntu, CentOS, SUSE, and SUSE Linux Enterprise Server (SLES).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="7a929-112">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="7a929-112">Implement the recommendation</span></span>
1. <span data-ttu-id="7a929-113">**권장 사항** 블레이드에서 **디스크 암호화 적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-113">In the **Recommendations** blade, select **Apply disk encryption**.</span></span>
2. <span data-ttu-id="7a929-114">**디스크 암호화 적용** 블레이드에서 디스크 암호화가 추천되는 VM의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-114">In the **Apply disk encryption** blade, you see a list of VMs for which Disk Encryption is recommended.</span></span>
3. <span data-ttu-id="7a929-115">지시를 따라서 이러한 VM에 암호화를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-115">Follow the instructions to apply encryption to these VMs.</span></span>

![][1]

<span data-ttu-id="7a929-116">보안 센터에 의해 암호화가 필요하다고 식별된 Azure 가상 컴퓨터를 암호화하려면 다음 단계를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-116">To encrypt Azure Virtual Machines that have been identified by Security Center as needing encryption, we recommend the following steps:</span></span>

* <span data-ttu-id="7a929-117">Azure PowerShell을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-117">Install and configure Azure PowerShell.</span></span> <span data-ttu-id="7a929-118">이렇게 하면 Azure Virtual Machines를 암호화하는 데 필요한 필수 구성 요소를 설정하는 데 필요한 PowerShell 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-118">This enables you to run the PowerShell commands required to set up the prerequisites required to encrypt Azure Virtual Machines.</span></span>
* <span data-ttu-id="7a929-119">Azure 디스크 암호화 필수 구성 요소 Azure PowerShell 스크립트를 가져오고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-119">Obtain and run the Azure Disk Encryption Prerequisites Azure PowerShell script.</span></span>
* <span data-ttu-id="7a929-120">가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="7a929-120">Encrypt your virtual machines.</span></span>

<span data-ttu-id="7a929-121">[Azure Virtual Machine 암호화](security-center-disk-encryption.md)에서 이러한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-121">[Encrypt an Azure Virtual Machine](security-center-disk-encryption.md) walks you through these steps.</span></span>  <span data-ttu-id="7a929-122">이 항목에서는 디스크 암호화를 구성할 클라이언트 컴퓨터로 Windows 10을 사용하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-122">This topic assumes you are using Windows 10 as the client machine from which you configure disk encryption.</span></span>

<span data-ttu-id="7a929-123">Azure Virtual Machines에 대해 사용할 수 있는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-123">There are many approaches that can be used for Azure Virtual Machines.</span></span> <span data-ttu-id="7a929-124">이미 Azure PowerShell 또는 Azure CLI에 대해 잘 알고 있다면 대체 방법을 사용하는 것을 선호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-124">If you are already well-versed in Azure PowerShell or Azure CLI, then you may prefer to use alternate approaches.</span></span> <span data-ttu-id="7a929-125">이러한 대체 방법에 대한 자세한 내용은 [Azure Disk Encryption](../security/azure-security-disk-encryption.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a929-125">To learn about these other approaches, see [Azure disk encryption](../security/azure-security-disk-encryption.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7a929-126">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7a929-126">See also</span></span>
<span data-ttu-id="7a929-127">이 문서에서는 보안 센터 권장 사항 "디스크 암호화 적용"을 구현하는 방법을 보여주었습니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-127">This document showed you how to implement the Security Center recommendation "Apply disk encryption."</span></span> <span data-ttu-id="7a929-128">디스크 암호화에 대해 자세히 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a929-128">To learn more about disk encryption, see the following:</span></span>

* <span data-ttu-id="7a929-129">[Azure 주요 자격 증명으로 암호화 및 키 관리](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (비디오, 36분 39초) -- IaaS VM 및 Azure 주요 자격 증명 모음에 디스크 암호화 관리를 사용하여 데이터를 세이프가드하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="7a929-129">[Encryption and key management with Azure Key Vault](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (video, 36 min 39 sec) -- Learn how to use disk encryption management for IaaS VMs and Azure Key Vault to help protect and safeguard your data.</span></span>
* <span data-ttu-id="7a929-130">[Azure 가상 컴퓨터 암호화](security-center-disk-encryption.md) (문서) -- Azure 가상 컴퓨터를 암호화하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="7a929-130">[Encrypt an Azure Virtual Machine](security-center-disk-encryption.md) (document) -- Learn how to encrypt Azure Virtual Machines.</span></span>
* <span data-ttu-id="7a929-131">[Azure 디스크 암호화](../security/azure-security-disk-encryption.md) (문서) -- Windows 및 Linux VM에 디스크 암호화를 사용하도록 설정하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="7a929-131">[Azure disk encryption](../security/azure-security-disk-encryption.md) (document) -- Learn how to enable disk encryption for Windows and Linux VMs.</span></span>

<span data-ttu-id="7a929-132">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a929-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="7a929-133">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -- 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="7a929-134">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -- Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="7a929-135">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) -- 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="7a929-136">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="7a929-137">[Azure 보안 센터 FAQ](security-center-faq.md) -- 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-137">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="7a929-138">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7a929-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
