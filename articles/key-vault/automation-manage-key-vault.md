---
title: "Azure 자동화를 사용 하 여 Azure 키 자격 증명 모음 aaaManage | Microsoft Docs"
description: "Azure 자동화 서비스 hello 사용된 toomanage Azure 키 자격 증명 모음을 수 있는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="9a49f-103">Azure 자동화를 사용하여 Azure 주요 자격 증명 모음 관리</span><span class="sxs-lookup"><span data-stu-id="9a49f-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="9a49f-104">이 가이드에서는 Azure 자동화 서비스 toohello 및 사용 되는 toosimplify 관리 키와 Azure 키 자격 증명 모음의 암호의 수 있는 방법을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-104">This guide will introduce you toohello Azure Automation service and how it can be used toosimplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="9a49f-105">Azure 자동화 정의</span><span class="sxs-lookup"><span data-stu-id="9a49f-105">What is Azure Automation?</span></span>
<span data-ttu-id="9a49f-106">[Azure 자동화](../automation/automation-intro.md) 는 프로세스 자동화 및 원하는 상태 구성을 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="9a49f-107">Azure 자동화를 사용 하 여 수동, 반복, 장기 실행 및 오류가 발생 하기 쉬운 작업에 자동화 된 tooincrease 안정성, 효율성 및 조직에 대 한 시간 toovalue 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="9a49f-108">Azure 자동화 요구에 맞게 toomeet 크기가 조정 되는 매우 신뢰할 수 있으며, 항상 사용 가능한 워크플로 실행 엔진을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="9a49f-109">Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="9a49f-110">작동 오버 헤드를 줄이고 확보 IT DevOps 직원 toofocus 프로그램 클라우드 관리 작업 toobe 이동 하 여 비즈니스 가치를 추가 하는 작업에는 Azure 자동화에 의해 자동으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="9a49f-111">Azure 자동화를 통해 Azure 주요 자격 증명 모음을 쉽게 관리하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="9a49f-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="9a49f-112">Hello를 사용 하 여 Azure 자동화에서 주요 자격 증명 모음을 관리할 수 있습니다 [AzureRM 키 자격 증명 모음 cmdlet](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) 및 [Azure 클래식 키 자격 증명 모음 cmdlet](https://msdn.microsoft.com/library/azure/dn868052.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-112">Key Vault can be managed in Azure Automation by using hello [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="9a49f-113">Azure 자동화에서 자동으로 사용할 수 없으면 기존 키 자격 증명 모음 관리 Azure 모듈 hello 및 hello를 가져올 수 있습니다 [AzureRM KeyVault 모듈](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) Azure 자동화로 다양 한 자격 증명 모음 키 관리를 수행할 수 있도록 hello 서비스 내에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-113">hello Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within hello service.</span></span> <span data-ttu-id="9a49f-114">또한 Azure 서비스 및 제 3 자 시스템에서 다른 Azure 서비스, tooautomate 복잡 한 작업에 대 한 hello cmdlet 통해 Azure 자동화에서 이러한 cmdlet을 페어링할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="9a49f-115">Hello Azure 키 자격 증명 모음 cmdlet과 함께 다른 규칙 으로부터 이러한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-115">With hello Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="9a49f-116">주요 자격 증명 모음 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="9a49f-116">Create and configure a key vault</span></span>
* <span data-ttu-id="9a49f-117">키 만들기 또는 가져오기</span><span class="sxs-lookup"><span data-stu-id="9a49f-117">Create or import a key</span></span>
* <span data-ttu-id="9a49f-118">암호 만들기 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="9a49f-118">Create or update a secret</span></span>
* <span data-ttu-id="9a49f-119">키 특성 업데이트</span><span class="sxs-lookup"><span data-stu-id="9a49f-119">Update attributes of a key</span></span>
* <span data-ttu-id="9a49f-120">키 또는 암호 가져오기</span><span class="sxs-lookup"><span data-stu-id="9a49f-120">Get a key or secret</span></span>
* <span data-ttu-id="9a49f-121">키 또는 암호 삭제</span><span class="sxs-lookup"><span data-stu-id="9a49f-121">Delete a key or secret</span></span>

<span data-ttu-id="9a49f-122">다음은 PowerShell toomanage 주요 자격 증명 모음을 사용 하 여 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-122">Here are some examples of using PowerShell toomanage Key Vault:</span></span>  

* [<span data-ttu-id="9a49f-123">Azure 주요 자격 증명 모음 - 단계별</span><span class="sxs-lookup"><span data-stu-id="9a49f-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="9a49f-124">Azure 주요 자격 증명 모음 설정 및 구성</span><span class="sxs-lookup"><span data-stu-id="9a49f-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="9a49f-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9a49f-125">Next steps</span></span>
<span data-ttu-id="9a49f-126">Azure 자동화 및 Azure 키 자격 증명 모음 사용된 toomanage 수 있는 방법의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn Azure 자동화에 대 한 자세한를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-126">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Key Vault, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="9a49f-127">Azure 자동화 hello 참조 [초보자를 위한 자습서](../automation/automation-first-runbook-graphical.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-127">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="9a49f-128">Hello 참조 [Azure 키 자격 증명 모음 PowerShell 스크립트를](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a49f-128">See hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

