---
title: "Azure Marketplace용 가상 컴퓨터 이미지를 만들기 위한 기술 필수 조건 | Microsoft Docs"
description: "가상 컴퓨터 이미지를 만들고 다른 사람이 구입할 수 있도록 Azure 마켓플레이스에 배포하기 위한 요구 사항을 이해합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: af3e2ad623d8d7bfafe676411f9ae3fbee78aab8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="e000a-103">Azure 마켓플레이스용 가상 컴퓨터 이미지를 만들기 위한 기술 필수 조건</span><span class="sxs-lookup"><span data-stu-id="e000a-103">Technical prerequisites for creating a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="e000a-104">시작하기 전에 프로세스를 자세히 읽고 각 단계를 어디에서, 왜 수행하는지를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-104">Read the process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="e000a-105">제품 만들기 프로세스를 시작하기 전에 회사 정보와 기타 데이터를 최대한 많이 준비하고 필요한 도구를 다운로드하고 기술 구성 요소를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning the offer creation process.</span></span> <span data-ttu-id="e000a-106">이 문서를 검토하여 이러한 항목에 대해 명확히 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="e000a-107">필요한 도구 및 응용 프로그램 다운로드</span><span class="sxs-lookup"><span data-stu-id="e000a-107">Download needed tools & applications</span></span>
<span data-ttu-id="e000a-108">프로세스를 시작하기 전에 다음 항목이 준비되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-108">You should have the following items ready before beginning the process:</span></span>

* <span data-ttu-id="e000a-109">대상으로 하는 운영 체제에 따라 [Azure 다운로드](https://azure.microsoft.com/downloads/) 페이지에서 [Azure PowerShell cmdlet](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) 또는 [Linux 명령줄 인터페이스 도구](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-109">Depending on which operating system you are targeting, install the [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from the [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="e000a-110">CodePlex에서 Azure 저장소 탐색기를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="e000a-111">Azure Certified용 인증 테스트 도구를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-111">Download and install the Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="e000a-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span><span class="sxs-lookup"><span data-stu-id="e000a-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="e000a-113">인증 도구를 실행하려면 Windows 기반 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-113">You need a Windows-based computer to run the certification tool.</span></span> <span data-ttu-id="e000a-114">Windows 기반 컴퓨터를 사용할 수 없는 경우 Azure의 Windows 기반 VM을 사용하여 도구를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-114">If you do not have a Windows-based computer available, you can run the tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="e000a-115">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="e000a-115">Platforms supported</span></span>
<span data-ttu-id="e000a-116">Windows 또는 Linux에서 Azure 기반 VM을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="e000a-117">Azure 호환 VHD(가상 하드 디스크) 만들기와 같은 게시 프로세스의 일부 요소에서는 사용 중인 운영 체제에 따라 다른 도구와 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-117">Some elements of the publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="e000a-118">Linux를 사용 중인 경우에는 [가상 컴퓨터 이미지 게시 가이드](marketplace-publishing-vm-image-creation.md)의 “Azure 호환 VHD 만들기(Linux 기반)” 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e000a-118">If you are using Linux, refer to the “Create an Azure-compatible VHD (Linux-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="e000a-119">Windows를 사용 중인 경우에는 [가상 컴퓨터 이미지 게시 가이드](marketplace-publishing-vm-image-creation.md)의 “Azure 호환 VHD 만들기(Windows 기반)” 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e000a-119">If you are using Windows, refer to the “Create an Azure-compatible VHD (Windows-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e000a-120">Windows 기반 컴퓨터에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-120">You need access to a Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="e000a-121">인증 유효성 검사 도구를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-121">Run the certification validation tool.</span></span>
> * <span data-ttu-id="e000a-122">VHD 인증 제출을 위한 VHD 공유 액세스 서명 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-122">Create the VHD shared access signature URL for the VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="e000a-123">VHD 개발</span><span class="sxs-lookup"><span data-stu-id="e000a-123">Develop your VHD</span></span>
<span data-ttu-id="e000a-124">클라우드 또는 온-프레미스에서 VHD를 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-124">You can develop Azure VHDs in the cloud or on-premises:</span></span>

* <span data-ttu-id="e000a-125">클라우드 기반 개발에서는 모든 개발 단계를 Azure에 있는 VHD에서 원격으로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="e000a-126">온-프레미스 개발에서는 VHD를 다운로드하고 온-프레미스 인프라를 사용하여 VHD를 개발해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="e000a-127">이 방법은 가능하지만 권장되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="e000a-128">Windows 또는 SQL용을 온-프레미스로 개발하려면 관련 온-프레미스 라이선스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-128">Note that developing for Windows or SQL on-premises requires you to have the relevant on-premises license keys.</span></span> <span data-ttu-id="e000a-129">VM을 만든 후에는 SQL Server를 포함하거나 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="e000a-130">또한 제품은 SQL Azure 포털에서 승인된 이미지를 기반으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-130">You must also base your offer on an approved SQL image from the Azure portal.</span></span> <span data-ttu-id="e000a-131">온-프레미스로 개발하려는 경우에는 클라우드에서 개발할 때와 다른 몇몇 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e000a-131">If you decide to develop on-premises, you must perform some steps differently than if you were developing in the cloud.</span></span> <span data-ttu-id="e000a-132">관련 정보는 [온-프레미스 VM 이미지 만들기](marketplace-publishing-vm-image-creation-on-premise.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e000a-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
