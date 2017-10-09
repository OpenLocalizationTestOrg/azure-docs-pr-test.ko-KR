---
title: "Azure 자동화를 사용 하 여 Azure 클라우드 서비스 aaaManage | Microsoft Docs"
description: "Azure 자동화 서비스 hello 규모에 사용 되는 toomanage Azure 클라우드 서비스를 수 있는 방법에 대해 알아봅니다."
services: cloud-services, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 8e920fb94955466bfec71cc332444f5f0ee497a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="522d1-103">Azure 자동화를 사용하여 Azure 클라우드 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="522d1-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="522d1-104">이 가이드에서는 toohello Azure 자동화 서비스 및 Azure 클라우드 서비스의 관리를 사용 하는 toosimplify 수 있는 방법을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="522d1-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="522d1-105">Azure 자동화 정의</span><span class="sxs-lookup"><span data-stu-id="522d1-105">What is Azure Automation?</span></span>
<span data-ttu-id="522d1-106">[Azure 자동화](https://azure.microsoft.com/services/automation/) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="522d1-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="522d1-107">Azure 자동화를 사용 하 여 장기 실행, 수동, 오류가 발생 하기 쉽고 자주 반복 되는 작업에 자동화 된 tooincrease 안정성, 효율성 및 조직에 대 한 시간 toovalue 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="522d1-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="522d1-108">Azure 자동화는 조직의 규모가 커짐에 toomeet 요구에 맞게 확장 되는 매우 안정적이 고 항상 사용 가능한 워크플로 실행 엔진을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="522d1-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="522d1-109">Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="522d1-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="522d1-110">작동 오버 헤드를 줄이고 확보 IT / DevOps 직원 toofocus 프로그램 클라우드 관리 작업 toobe 이동 하 여 비즈니스 가치를 추가 하는 작업에는 Azure 자동화에 의해 자동으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="522d1-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="522d1-111">Azure 자동화를 통해 Azure 클라우드 서비스 관리 향상</span><span class="sxs-lookup"><span data-stu-id="522d1-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="522d1-112">Hello에서 사용할 수 있는 hello PowerShell cmdlet을 사용 하 여 Azure 자동화에서 azure 클라우드 서비스를 관리할 수 있습니다 [Azure PowerShell 도구](https://msdn.microsoft.com/library/azure/jj156055.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="522d1-112">Azure cloud services can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="522d1-113">Azure 자동화에는 클라우드 서비스 PowerShell cmdlet를 사용할 수 있는 이러한 hello 상자 밖의 hello 서비스 내에서 클라우드 서비스 관리 작업을 모두 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="522d1-113">Azure Automation has these cloud service PowerShell cmdlets available out of hello box, so that you can perform all of your cloud service management tasks within hello service.</span></span> <span data-ttu-id="522d1-114">또한 Azure 서비스 및 제 3 자 시스템에서 다른 Azure 서비스, tooautomate 복잡 한 작업에 대 한 hello cmdlet 통해 Azure 자동화에서 이러한 cmdlet을 페어링할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="522d1-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="522d1-115">Azure 클라우드 서비스를 포함 하는 Azure 자동화 toomanage의 사용 하 여 몇 가지 예제:</span><span class="sxs-lookup"><span data-stu-id="522d1-115">Some example uses of Azure Automation toomanage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="522d1-116">Azure Blob 저장소에서 cscfg 또는 cspkg가 업데이트될 때마다 클라우드 서비스의 연속 배포</span><span class="sxs-lookup"><span data-stu-id="522d1-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="522d1-117">클라우드 서비스 인스턴스를 병렬로 다시 부팅할 때 한 번에 하나의 도메인 업그레이드</span><span class="sxs-lookup"><span data-stu-id="522d1-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="522d1-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="522d1-118">Next Steps</span></span>
<span data-ttu-id="522d1-119">Azure 자동화 및 사용 되는 toomanage Azure 클라우드 서비스 수 있는 방법의 hello 기본 사항 학습 한를 했으므로 이러한 링크 toolearn Azure 자동화에 대 한 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="522d1-119">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure cloud services, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="522d1-120">Azure 자동화 개요</span><span class="sxs-lookup"><span data-stu-id="522d1-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="522d1-121">내 첫 번째 runbook</span><span class="sxs-lookup"><span data-stu-id="522d1-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="522d1-122">Azure 자동화 학습 맵</span><span class="sxs-lookup"><span data-stu-id="522d1-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
