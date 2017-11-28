---
title: "Azure 자동화를 사용 하 여 Azure 저장소 aaaManage"
description: "Azure 자동화 서비스 hello 규모에 사용 되는 toomanage Azure 저장소를 수 있는 방법에 대해 알아봅니다."
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: 5edfba1a9ce1f9c81b5bd0889de19099f3d86fc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="247ab-103">Azure 자동화를 사용하여 Azure 저장소 관리</span><span class="sxs-lookup"><span data-stu-id="247ab-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="247ab-104">이 가이드에서는 toohello Azure 자동화 서비스 및 Azure 저장소 blob, 테이블 및 큐의 관리를 사용 하는 toosimplify 수 있는 방법을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="247ab-105">Azure 자동화 정의</span><span class="sxs-lookup"><span data-stu-id="247ab-105">What is Azure Automation?</span></span>
<span data-ttu-id="247ab-106">[Azure 자동화](https://azure.microsoft.com/services/automation/) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="247ab-107">Azure 자동화를 사용 하 여 장기 실행, 수동, 오류가 발생 하기 쉽고 자주 반복 작업 자동화 된 tooincrease 안정성 및 효율성을 높일 수를 업데이트 하 고 조직에 대 한 시간 toovalue 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability and efficiency, and reduce time toovalue for your organization.</span></span>

<span data-ttu-id="247ab-108">Azure 자동화는 조직의 규모가 커짐에 toomeet 요구에 맞게 확장 되는 매우 안정적이 고 항상 사용 가능한 워크플로 실행 엔진을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="247ab-109">Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="247ab-110">작동 오버 헤드를 줄이고 확보 IT / DevOps 직원 toofocus 프로그램 클라우드 관리 작업 toobe 이동 하 여 비즈니스 가치를 추가 하는 작업에는 Azure 자동화에 의해 자동으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="247ab-111">Azure 자동화를 통해 Azure 저장소 관리 향상</span><span class="sxs-lookup"><span data-stu-id="247ab-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="247ab-112">사용할 수 있는 hello PowerShell cmdlet을 사용 하 여 Azure 자동화에서 azure 저장소를 관리할 수 있습니다 [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-112">Azure Storage can be managed in Azure Automation by using hello PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="247ab-113">Azure 자동화에는 이러한 저장소 PowerShell cmdlet을 사용할 수 있는 hello 상자 밖의 모든 blob, 테이블 및 hello 서비스 내에서 큐 관리 작업을 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-113">Azure Automation has these Storage PowerShell cmdlets available out of hello box, so that you can perform all of your blob, table, and queue management tasks within hello service.</span></span> <span data-ttu-id="247ab-114">또한 Azure 서비스 및 제 3 자 시스템에서 다른 Azure 서비스, tooautomate 복잡 한 작업에 대 한 hello cmdlet 통해 Azure 자동화에서 이러한 cmdlet을 페어링할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="247ab-115">hello [Azure 자동화 runbook 갤러리](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) 에 다양 한 제품 팀과 커뮤니티 runbook tooget Azure 저장소, 다른 Azure 서비스 및 제 3 자 시스템 관리를 자동화를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-115">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="247ab-116">Runbook 갤러리에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="247ab-117">자동화 서비스를 사용하여 특정 일 수가 지난 Azure 저장소 Blob 제거</span><span class="sxs-lookup"><span data-stu-id="247ab-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="247ab-118">Azure 저장소에서 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="247ab-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="247ab-119">단일 Azure VM 또는 클라우드 서비스의 모든 VM에 대한 모든 디스크 백업</span><span class="sxs-lookup"><span data-stu-id="247ab-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="247ab-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="247ab-120">Next Steps</span></span>
<span data-ttu-id="247ab-121">Azure 자동화 및 사용 되는 toomanage Azure 저장소 blob, 테이블 및 큐 수 있는 방법의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn Azure 자동화에 대 한 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-121">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Storage blobs, tables, and queues, follow these links toolearn more about Azure Automation.</span></span>

<span data-ttu-id="247ab-122">Hello Azure 자동화 자습서 [만들기 또는 Azure 자동화에서 runbook을 가져와](../../automation/automation-creating-importing-runbook.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="247ab-122">See hello Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../../automation/automation-creating-importing-runbook.md).</span></span>

