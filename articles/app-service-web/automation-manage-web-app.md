---
title: "Azure 자동화를 사용 하 여 Azure 웹 앱 aaaManage | Microsoft Docs"
description: "Azure 자동화 서비스 hello 사용된 toomanage Azure 웹 앱을 수 있는 방법에 대해 알아봅니다."
services: app-service\web, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: c960a44f-f941-401d-afba-a4bc0f0394eb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte
ms.openlocfilehash: 6d80351a2927f26753cfbaead6e1c0c3c94e86e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="a4468-103">Azure 자동화를 사용하여 Azure 웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="a4468-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="a4468-104">이 가이드에서는 toohello Azure 자동화 서비스 및 Azure 웹 앱의 관리를 사용 하는 toosimplify 수 있는 방법을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4468-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="a4468-105">Azure 자동화 정의</span><span class="sxs-lookup"><span data-stu-id="a4468-105">What is Azure Automation?</span></span>
<span data-ttu-id="a4468-106">[Azure 자동화](../automation/automation-intro.md) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a4468-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="a4468-107">Azure 자동화를 사용 하 여 수동, 반복, 장기 실행 및 오류가 발생 하기 쉬운 작업에 자동화 된 tooincrease 안정성, 효율성 및 조직에 대 한 시간 toovalue 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4468-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="a4468-108">Azure 자동화 요구에 맞게 toomeet 크기가 조정 되는 매우 신뢰할 수 있으며, 항상 사용 가능한 워크플로 실행 엔진을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4468-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="a4468-109">Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4468-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="a4468-110">작동 오버 헤드를 줄이고 확보 IT DevOps 직원 toofocus 프로그램 클라우드 관리 작업 toobe 이동 하 여 비즈니스 가치를 추가 하는 작업에는 Azure 자동화에 의해 자동으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4468-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="a4468-111">어떻게 Azure 자동화가 Azure 웹앱을 관리할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="a4468-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="a4468-112">Hello에서 사용할 수 있는 hello PowerShell cmdlet을 사용 하 여 Azure 자동화에서 웹 앱을 관리할 수 있습니다 [Azure PowerShell 모듈](/powershell/azureps-cmdlets-docs)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4468-112">Web App can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="a4468-113">있습니다 수 [Azure 자동화에서 이러한 웹 응용 프로그램 PowerShell cmdlet을 설치](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/)의 hello 서비스 내에서 웹 앱 관리 작업을 모두 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4468-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within hello service.</span></span> <span data-ttu-id="a4468-114">또한 Azure 서비스 및 제 3 자 시스템에서 다른 Azure 서비스 tooautomate 복잡 한 작업에 대 한 hello cmdlet 통해 Azure 자동화에서 이러한 cmdlet을 페어링할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4468-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="a4468-115">자동화를 사용하여 앱 서비스를 관리하는 몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a4468-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="a4468-116">웹앱을 관리하기 위한 스크립트</span><span class="sxs-lookup"><span data-stu-id="a4468-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="a4468-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4468-117">Next steps</span></span>
<span data-ttu-id="a4468-118">Azure 자동화 및 사용 하는 Azure 웹 앱 toomanage 수 있는 방법의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn Azure 자동화에 대 한 자세한를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4468-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Web App, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="a4468-119">Azure 자동화 hello 참조 [초보자를 위한 자습서](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="a4468-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

