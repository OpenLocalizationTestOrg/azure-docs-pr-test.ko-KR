---
title: "Azure 자동화를 사용 하 여 Azure RemoteApp aaaManage | Microsoft Docs"
description: "Azure 자동화 서비스 hello 사용된 toomanage Azure RemoteApp을 수 있는 방법에 대해 알아봅니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: a4cb23e292c797256e971acb3b363b025f140f16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="7c99e-103">Azure 자동화를 사용하여 Azure RemoteApp 관리</span><span class="sxs-lookup"><span data-stu-id="7c99e-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7c99e-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c99e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7c99e-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c99e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7c99e-106">이 가이드에서는 toohello Azure 자동화 서비스 및 Azure RemoteApp의 관리를 사용 하는 toosimplify 수 있는 방법을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c99e-106">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="7c99e-107">Azure 자동화 정의</span><span class="sxs-lookup"><span data-stu-id="7c99e-107">What is Azure Automation?</span></span>
<span data-ttu-id="7c99e-108">[Azure 자동화](../automation/automation-intro.md) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7c99e-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="7c99e-109">Azure 자동화를 사용 하 여 수동, 자주 반복, 장기 실행 및 오류가 발생 하기 쉬운 작업에 자동화 된 tooincrease 안정성, 효율성 및 조직에 대 한 시간 toovalue 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c99e-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="7c99e-110">Azure 자동화 요구에 맞게 toomeet 크기가 조정 되는 매우 신뢰할 수 있으며, 항상 사용 가능한 워크플로 실행 엔진을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c99e-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="7c99e-111">Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c99e-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="7c99e-112">작동 오버 헤드를 줄이고 확보 IT DevOps 직원 toofocus 프로그램 클라우드 관리 작업 toobe 이동 하 여 비즈니스 가치를 추가 하는 작업에는 Azure 자동화에 의해 자동으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c99e-112">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="7c99e-113">Azure 자동화를 통해 Azure RemoteApp 관리 향상</span><span class="sxs-lookup"><span data-stu-id="7c99e-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="7c99e-114">RemoteApp hello에서 사용할 수 있는 hello PowerShell cmdlet을 사용 하 여 Azure 자동화에서 관리할 수 있습니다 [Azure PowerShell 도구](https://msdn.microsoft.com/library/azure/jj156055.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c99e-114">RemoteApp can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="7c99e-115">Azure 자동화에는 사용할 수 있는 RemoteApp PowerShell cmdlet이 hello 상자 밖의 hello 서비스 내에서 RemoteApp 관리 작업을 모두 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c99e-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of hello box, so that you can perform all of your RemoteApp management tasks within hello service.</span></span> <span data-ttu-id="7c99e-116">또한 Azure 서비스 및 제 3 자 시스템에서 다른 Azure 서비스, tooautomate 복잡 한 작업에 대 한 hello cmdlet 통해 Azure 자동화에서 이러한 cmdlet을 페어링할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c99e-116">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c99e-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7c99e-117">Next steps</span></span>
<span data-ttu-id="7c99e-118">Azure 자동화 및 사용 하는 Azure RemoteApp toomanage 수 있는 방법의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn Azure 자동화에 대 한 자세한를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c99e-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure RemoteApp, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="7c99e-119">Azure 자동화 hello 참조 [초보자를 위한 자습서](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="7c99e-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

