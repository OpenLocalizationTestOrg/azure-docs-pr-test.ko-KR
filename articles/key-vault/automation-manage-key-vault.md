---
title: "Azure 자동화를 사용하여 Azure 주요 자격 증명 모음 관리 | Microsoft Docs"
description: "Azure 자동화 사버시를 사용하여 Azure 주요 자격 증명 모음을 관리하는 방법에 대해 알아봅니다."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: dee39662472fe54776b591977f2b1ecb39d15b00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="fb92d-103">Azure 자동화를 사용하여 Azure 주요 자격 증명 모음 관리</span><span class="sxs-lookup"><span data-stu-id="fb92d-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="fb92d-104">이 가이드에서는 Azure 자동화 서비스 및 이 서비스를 사용하여 Azure 주요 자격 증명 모음에서 키 및 암호 관리를 간소화하는 방법에 대해 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="fb92d-104">This guide will introduce you to the Azure Automation service and how it can be used to simplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="fb92d-105">Azure 자동화 정의</span><span class="sxs-lookup"><span data-stu-id="fb92d-105">What is Azure Automation?</span></span>
<span data-ttu-id="fb92d-106">[Azure 자동화](../automation/automation-intro.md) 는 프로세스 자동화 및 원하는 상태 구성을 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fb92d-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="fb92d-107">Azure 자동화, 수동, 반복되는, 장기 실행 및 오류가 발생하기 쉬운 작업을 사용하면 조직의 안정성, 효율성 및 가치 창출 시간을 개선하도록 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb92d-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="fb92d-108">Azure 자동화는 요구 사항에 맞게 크기가 조정되는 매우 안정적이며 가용성이 높은 워크플로 실행 엔진을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fb92d-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="fb92d-109">Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb92d-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="fb92d-110">Azure 자동화에서 자동으로 실행되도록 클라우드 관리 작업을 이동하여 작업 오버헤드를 줄이고 IT 및 DevOps 직원들이 비즈니스 가치를 추가하는 작업에 집중할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb92d-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="fb92d-111">Azure 자동화를 통해 Azure 주요 자격 증명 모음을 쉽게 관리하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="fb92d-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="fb92d-112">주요 자격 증명 모음은 [AzureRM 주요 자격 증명 모음 cmdlet](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) 및 [Azure 클래식 주요 자격 증명 모음 cmdlet](https://msdn.microsoft.com/library/azure/dn868052.aspx)을 사용하여 Azure 자동화로 관리될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb92d-112">Key Vault can be managed in Azure Automation by using the [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="fb92d-113">클래식 주요 자격 증명 모음 관리를 위한 Azure 모듈은 Azure 자동화에 자동으로 제공되며, 서비스 내에서 많은 주요 자격 증명 모음 관리 작업을 수행할 수 있도록, [AzureRM-KeyVault 모듈](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) 을 Azure 자동화로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb92d-113">The Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import the [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within the service.</span></span> <span data-ttu-id="fb92d-114">Azure 자동화에서 이러한 cmdlet을 다른 Azure 서비스용 cmdlet과 연결하여 Azure 서비스와 타사 시스템 간의 복잡한 작업을 자동화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb92d-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="fb92d-115">Azure 주요 자격 증명 모음 cmdlet을 사용하여 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb92d-115">With the Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="fb92d-116">주요 자격 증명 모음 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="fb92d-116">Create and configure a key vault</span></span>
* <span data-ttu-id="fb92d-117">키 만들기 또는 가져오기</span><span class="sxs-lookup"><span data-stu-id="fb92d-117">Create or import a key</span></span>
* <span data-ttu-id="fb92d-118">암호 만들기 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="fb92d-118">Create or update a secret</span></span>
* <span data-ttu-id="fb92d-119">키 특성 업데이트</span><span class="sxs-lookup"><span data-stu-id="fb92d-119">Update attributes of a key</span></span>
* <span data-ttu-id="fb92d-120">키 또는 암호 가져오기</span><span class="sxs-lookup"><span data-stu-id="fb92d-120">Get a key or secret</span></span>
* <span data-ttu-id="fb92d-121">키 또는 암호 삭제</span><span class="sxs-lookup"><span data-stu-id="fb92d-121">Delete a key or secret</span></span>

<span data-ttu-id="fb92d-122">다음은 PowerShell을 사용하여 주요 자격 증명 모음을 관리하는 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="fb92d-122">Here are some examples of using PowerShell to manage Key Vault:</span></span>  

* [<span data-ttu-id="fb92d-123">Azure 주요 자격 증명 모음 - 단계별</span><span class="sxs-lookup"><span data-stu-id="fb92d-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="fb92d-124">Azure 주요 자격 증명 모음 설정 및 구성</span><span class="sxs-lookup"><span data-stu-id="fb92d-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="fb92d-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fb92d-125">Next steps</span></span>
<span data-ttu-id="fb92d-126">Azure 자동화의 기본 사항과 이를 사용하여 Azure 주요 자격 증명 모음을 관리하는 방법을 알아보았으므로, 이제 다음 링크에 따라 Azure 자동화에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="fb92d-126">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Key Vault, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="fb92d-127">Azure 자동화 [시작 자습서](../automation/automation-first-runbook-graphical.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb92d-127">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="fb92d-128">[Azure 주요 자격 증명 모음 PowerShell 스크립트](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb92d-128">See the [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

