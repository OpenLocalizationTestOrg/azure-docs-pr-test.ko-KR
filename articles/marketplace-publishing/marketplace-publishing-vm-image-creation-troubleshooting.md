---
title: "VHD를 만드는 동안 일반적인 문제 해결 방법 | Microsoft Docs"
description: "VHD 만드는 동안 문제를 해결하는 일반적인 질문 및 문제에 대답합니다."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c4e88a9fbb15dd90d619b159ae1065dfacc1907f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-common-issues-encountered-during-vhd-creation"></a><span data-ttu-id="3b683-103">VHD를 만드는 동안 발생하는 일반적인 문제 해결 방법</span><span class="sxs-lookup"><span data-stu-id="3b683-103">How to troubleshoot common issues encountered during VHD creation</span></span>
<span data-ttu-id="3b683-104">이 문서는 가상 컴퓨터 솔루션을 게시하거나 관리하는 동안 문제가 발생하거나 관련된 일반적인 질문이 있는 Azure Marketplace 게시자 및/또는 공동 관리자를 돕기 위해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b683-104">This article is provided to help an Azure Marketplace publisher and/or co-administrator that may experience an issue or have common questions while publishing or managing their virtual machine solution(s).</span></span>

1. <span data-ttu-id="3b683-105">호스트의 이름을 변경하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3b683-105">How do I change the name of the host?</span></span>
   
    <span data-ttu-id="3b683-106">VM이 만들어지면 사용자는 호스트의 이름을 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b683-106">Once VM is created, users can’t update the name of the host.</span></span>
2. <span data-ttu-id="3b683-107">원격 데스크톱 서비스 또는 해당 로그인 암호를 다시 설정하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3b683-107">How to reset the Remote Desktop service or its login password?</span></span>
   
   * [<span data-ttu-id="3b683-108">Windows VM에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="3b683-108">Reference for Windows VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [<span data-ttu-id="3b683-109">Linux VM에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="3b683-109">Reference for Linux VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. <span data-ttu-id="3b683-110">새 SSH 인증서를 생성하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3b683-110">How to generate new ssh certificates?</span></span>
   
   <span data-ttu-id="3b683-111">[https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/) 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b683-111">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span></span>
4. <span data-ttu-id="3b683-112">열린 VPN 인증서를 구성하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3b683-112">How to configure an open VPN certificate?</span></span>
   
   <span data-ttu-id="3b683-113">[https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/) 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b683-113">Please refer to the link: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span></span>
5. <span data-ttu-id="3b683-114">Microsoft Azure 가상 컴퓨터 환경(infrastructure-as-a-service)에서 Microsoft 서버 소프트웨어를 실행하기 위한 지원 정책은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="3b683-114">What is the support policy for running Microsoft server software in the Microsoft Azure virtual machine environment (infrastructure-as-a-service)?</span></span>
   
   <span data-ttu-id="3b683-115">[https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672) 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b683-115">Please refer to the link: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
6. <span data-ttu-id="3b683-116">가상 컴퓨터는 고유 식별자를 가지고 있나요?</span><span class="sxs-lookup"><span data-stu-id="3b683-116">Do Virtual Machines have any unique identifier?</span></span>
   
   <span data-ttu-id="3b683-117">Azure는 모든 VM에 Azure VM 고유 ID를 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="3b683-117">Azure encodes Azure VM Unique ID in every VM.</span></span> <span data-ttu-id="3b683-118">이 블로그 및 문서에서 세부 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b683-118">See details in this blog and documentation.</span></span>
7. <span data-ttu-id="3b683-119">VM에서 시작 태스크에 있는 사용자 지정 스크립트 확장을 어떻게 관리할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="3b683-119">In a VM how can I manage the custom script extension in the startup task?</span></span>
   
   <span data-ttu-id="3b683-120">[https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/) 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b683-120">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span></span>
8. <span data-ttu-id="3b683-121">Premium Storage에 업로드된 VHD를 사용하여 Azure Portal에서 VM을 만들려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3b683-121">How to create a VM from the Azure portal using the VHD that is uploaded to premium storage?</span></span>
   
   <span data-ttu-id="3b683-122">이 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b683-122">We do not support this feature yet.</span></span>
9. <span data-ttu-id="3b683-123">32비트 앱은 Azure Marketplace에서 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="3b683-123">Is a 32-bit app supported in the Azure Marketplace?</span></span>
   
   <span data-ttu-id="3b683-124">지원 정책에 대한 자세한 내용은 [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672) 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b683-124">Please refer to the link for details on the support policy: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
10. <span data-ttu-id="3b683-125">내 VHD에서 이미지를 만들려고 할 때마다 PowerShell에서 "리소스인 이미지 리포지토리로 VHD를 이미 등록했습니다." 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b683-125">Every time I am trying to create an image from my VHDs, I get the error “.VHD is already registered with image repository as the resource” in PowerShell.</span></span> <span data-ttu-id="3b683-126">이미지를 만들지 않았거나 Azure에서 이 이름을 가진 이미지를 찾지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b683-126">I did not create any image before nor did I find any image with this name in Azure.</span></span> <span data-ttu-id="3b683-127">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3b683-127">How do I resolve this?</span></span>
    
    <span data-ttu-id="3b683-128">이 문제는 일반적으로 사용자가 이 VHD에서 VM을 프로비전하고 해당 VHD에 대한 잠금이 있는 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3b683-128">This usually happen if the user provisioned a VM from this VHD and there is a lock on that VHD.</span></span> <span data-ttu-id="3b683-129">이 VHD에서 할당된 VM이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b683-129">Please check that there is no VM allocated from this VHD.</span></span> <span data-ttu-id="3b683-130">오류가 계속되는 경우 이 링크를 사용하거나 관련된 게시 포털에서 지원 티켓을 제기합니다.(질문 11의 답변에서 세부 정보를 제공).</span><span class="sxs-lookup"><span data-stu-id="3b683-130">If the error still persist , then please raise a support ticket using this link or from the Publishing portal regarding this (details are given in the answer of question 11).</span></span>