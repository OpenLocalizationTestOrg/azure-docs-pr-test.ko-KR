---
title: "Azure 보안 센터에서 aaaApply 디스크 암호화 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 디스크 암호화 * * 적용 합니다."
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
ms.openlocfilehash: cd803f1120018c5c86da91186eec1e59d425ede7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a><span data-ttu-id="fa3bc-103">Azure 보안 센터에서 디스크 암호화 적용</span><span class="sxs-lookup"><span data-stu-id="fa3bc-103">Apply disk encryption in Azure Security Center</span></span>
<span data-ttu-id="fa3bc-104">Azure Security Center는 암호화되지 않은 Windows 또는 Linux VM 디스크가 있는 경우 Azure Disk Encryption을 사용하여 디스크 암호화를 적용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-104">Azure Security Center recommends that you apply disk encryption if you have Windows or Linux VM disks that are not encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="fa3bc-105">디스크 암호화를 사용하면 Windows 및 Linux IaaS VM 디스크를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-105">Disk Encryption lets you encrypt your Windows and Linux IaaS VM disks.</span></span>  <span data-ttu-id="fa3bc-106">Hello OS와 VM에 데이터 볼륨에 대 한 암호화를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-106">Encryption is recommended for both hello OS and data volumes on your VM.</span></span>

<span data-ttu-id="fa3bc-107">디스크 암호화 hello 업계 표준을 사용 하 여 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) 창과 hello의 기능 [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-107">Disk Encryption uses hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux.</span></span> <span data-ttu-id="fa3bc-108">이러한 기능은 제공 OS 및 데이터 암호화 toohelp 보호 및 데이터를 보호 하 고 조직의 보안 및 규정 준수 약정을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-108">These features provide OS and data encryption toohelp protect and safeguard your data and meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="fa3bc-109">디스크 암호화와 통합 되어 [Azure 키 자격 증명 모음](https://azure.microsoft.com/documentation/services/key-vault/) toohelp 제어 및 관리 hello 디스크 암호화 키 및 비밀 키 자격 증명 모음 구독에서 프로그램 의helloVM디스크에모든데이터를암호화는확인한후에[ Azure 저장소](https://azure.microsoft.com/documentation/services/storage/)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-109">Disk Encryption is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk encryption keys and secrets in your Key Vault subscription, while ensuring that all data in hello VM disks are encrypted at rest in your [Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span></span>

> [!NOTE]
> <span data-ttu-id="fa3bc-110">Azure 디스크 암호화는 hello 다음 Windows server 운영 체제-Windows Server 2008 R2, Windows Server 2012 및 Windows Server 2012 r 2에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-110">Azure Disk Encryption is supported on hello following Windows server operating systems - Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span> <span data-ttu-id="fa3bc-111">디스크 암호화는 hello 다음 Linux 서버 운영 체제-Ubuntu, CentOS, SUSE, 및 SUSE Linux Enterprise Server (SLES)에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-111">Disk encryption is supported on hello following Linux server operating systems - Ubuntu, CentOS, SUSE, and SUSE Linux Enterprise Server (SLES).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="fa3bc-112">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="fa3bc-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="fa3bc-113">Hello에 **권장 사항을** 블레이드를 **디스크 암호화 적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-113">In hello **Recommendations** blade, select **Apply disk encryption**.</span></span>
2. <span data-ttu-id="fa3bc-114">Hello에 **디스크 암호화 적용** 블레이드에 Vm 디스크 암호화는이 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-114">In hello **Apply disk encryption** blade, you see a list of VMs for which Disk Encryption is recommended.</span></span>
3. <span data-ttu-id="fa3bc-115">Hello 지침 tooapply 암호화 toothese Vm을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-115">Follow hello instructions tooapply encryption toothese VMs.</span></span>

![][1]

<span data-ttu-id="fa3bc-116">보안 센터에서 암호화는 것으로 확인 된 Azure 가상 컴퓨터 tooencrypt 단계를 수행 하는 hello를 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-116">tooencrypt Azure Virtual Machines that have been identified by Security Center as needing encryption, we recommend hello following steps:</span></span>

* <span data-ttu-id="fa3bc-117">Azure PowerShell을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-117">Install and configure Azure PowerShell.</span></span> <span data-ttu-id="fa3bc-118">그러면 toorun hello PowerShell 명령을 필요한 tooset hello 필수 구성 요소 필요 tooencrypt Azure 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-118">This enables you toorun hello PowerShell commands required tooset up hello prerequisites required tooencrypt Azure Virtual Machines.</span></span>
* <span data-ttu-id="fa3bc-119">받으며 hello Azure 디스크 암호화 필수 구성 요소가 Azure PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-119">Obtain and run hello Azure Disk Encryption Prerequisites Azure PowerShell script.</span></span>
* <span data-ttu-id="fa3bc-120">가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="fa3bc-120">Encrypt your virtual machines.</span></span>

<span data-ttu-id="fa3bc-121">[Azure Virtual Machine 암호화](security-center-disk-encryption.md)에서 이러한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-121">[Encrypt an Azure Virtual Machine](security-center-disk-encryption.md) walks you through these steps.</span></span>  <span data-ttu-id="fa3bc-122">이 항목에서는 Windows 10을 사용 하는 디스크 암호화를 구성 하는 hello 클라이언트 컴퓨터로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-122">This topic assumes you are using Windows 10 as hello client machine from which you configure disk encryption.</span></span>

<span data-ttu-id="fa3bc-123">Azure Virtual Machines에 대해 사용할 수 있는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-123">There are many approaches that can be used for Azure Virtual Machines.</span></span> <span data-ttu-id="fa3bc-124">이미 Azure PowerShell 또는 Azure CLI 잘 알고 있다면 toouse 대체 방법을 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-124">If you are already well-versed in Azure PowerShell or Azure CLI, then you may prefer toouse alternate approaches.</span></span> <span data-ttu-id="fa3bc-125">이러한 다른 방법에 대 한 toolearn 참조 [Azure 디스크 암호화](../security/azure-security-disk-encryption.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-125">toolearn about these other approaches, see [Azure disk encryption](../security/azure-security-disk-encryption.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="fa3bc-126">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fa3bc-126">See also</span></span>
<span data-ttu-id="fa3bc-127">이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 사항 "적용 디스크 암호화 합니다."</span><span class="sxs-lookup"><span data-stu-id="fa3bc-127">This document showed you how tooimplement hello Security Center recommendation "Apply disk encryption."</span></span> <span data-ttu-id="fa3bc-128">디스크 암호화에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-128">toolearn more about disk encryption, see hello following:</span></span>

* <span data-ttu-id="fa3bc-129">[Azure 키 자격 증명 암호화 및 키 관리](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (비디오, 36 분 39 초)-IaaS Vm 및 Azure 키 자격 증명 모음 toohelp 보호 하 고 데이터를 보호에 대 한 암호화 관리 toouse 디스크 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-129">[Encryption and key management with Azure Key Vault](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (video, 36 min 39 sec) -- Learn how toouse disk encryption management for IaaS VMs and Azure Key Vault toohelp protect and safeguard your data.</span></span>
* <span data-ttu-id="fa3bc-130">[Azure 가상 컴퓨터를 암호화](security-center-disk-encryption.md) (문서)-자세한 방법을 tooencrypt Azure 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-130">[Encrypt an Azure Virtual Machine](security-center-disk-encryption.md) (document) -- Learn how tooencrypt Azure Virtual Machines.</span></span>
* <span data-ttu-id="fa3bc-131">[Azure 디스크 암호화](../security/azure-security-disk-encryption.md) (문서)-tooenable Windows 및 Linux Vm에 대 한 암호화 디스크 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-131">[Azure disk encryption](../security/azure-security-disk-encryption.md) (document) -- Learn how tooenable disk encryption for Windows and Linux VMs.</span></span>

<span data-ttu-id="fa3bc-132">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="fa3bc-133">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="fa3bc-134">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="fa3bc-135">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="fa3bc-136">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="fa3bc-137">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-137">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="fa3bc-138">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3bc-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
