---
title: "Azure 자동화를 사용 하 여 Vm aaaManage | Microsoft Docs"
description: "Azure 가상 컴퓨터 규모에 hello Azure 자동화 서비스 사용된 toomanage을 수 있는 방법에 대해 알아봅니다."
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: bfe7b3a51b6e82bd7cd5b0a83df7226476ed4f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="abb10-103">Azure 자동화를 사용하여 Azure 가상 컴퓨터 관리</span><span class="sxs-lookup"><span data-stu-id="abb10-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="abb10-104">이 가이드 소개 toohello Azure 자동화 서비스 및 사용할 수 있는 방법을 toosimplify Azure 가상 컴퓨터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="abb10-104">This guide introduces you toohello Azure Automation service and how it can be used toosimplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="abb10-105">Azure 자동화 정의</span><span class="sxs-lookup"><span data-stu-id="abb10-105">What is Azure Automation?</span></span>
<span data-ttu-id="abb10-106">[Azure 자동화](https://azure.microsoft.com/services/automation/) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="abb10-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="abb10-107">Azure 자동화를 사용 하 여 장기 실행, 수동, 오류가 발생 하기 쉽고 자주 반복 되는 작업에 자동화 된 tooincrease 안정성, 효율성 및 조직에 대 한 값으로 시간 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb10-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="abb10-108">Azure 자동화는 조직의 규모가 커짐에 toomeet 요구에 맞게 확장 되는 매우 안정적이 고 항상 사용 가능한 워크플로 실행 엔진을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="abb10-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="abb10-109">Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb10-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="abb10-110">작동 오버 헤드를 절감 하 고 확보 IT 및 DevOps 팀 toofocus 함께 실행 하 여 클라우드 관리 작업 자동으로 Azure 자동화 비즈니스 가치를 추가 하는 작업을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="abb10-110">You can lower operational overhead and free up IT and DevOps staff toofocus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="abb10-111">Azure 자동화를 통해 Azure 가상 컴퓨터 관리 향상</span><span class="sxs-lookup"><span data-stu-id="abb10-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="abb10-112">[Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx)을 사용하여 Azure 자동화에서 가상 컴퓨터를 관리 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb10-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="abb10-113">Azure 자동화의 hello 서비스 내에서 가상 컴퓨터 관리 작업을 모두 수행할 수 있도록 hello Azure PowerShell cmdlet을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="abb10-113">Azure Automation includes hello Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within hello service.</span></span> <span data-ttu-id="abb10-114">Azure 서비스와 타사 시스템에서 다른 Azure 서비스, tooautomate 복잡 한 작업에 대 한 hello cmdlet 통해 Azure 자동화의 hello cmdlet도 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb10-114">You can also pair hello cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abb10-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="abb10-115">Next steps</span></span>
<span data-ttu-id="abb10-116">Hello 기본 사항 학습 한 했으므로 Azure 자동화 및 사용 되는 toomanage 수 있는 방법의 Azure 가상 컴퓨터, 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="abb10-116">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="abb10-117">Azure 자동화 개요</span><span class="sxs-lookup"><span data-stu-id="abb10-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="abb10-118">내 첫 번째 runbook</span><span class="sxs-lookup"><span data-stu-id="abb10-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="abb10-119">Azure 자동화 학습 맵</span><span class="sxs-lookup"><span data-stu-id="abb10-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

