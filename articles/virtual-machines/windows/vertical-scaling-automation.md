---
title: "Azure Automation을 사용하여 Windows 가상 컴퓨터를 수직으로 확장 | Microsoft Docs"
description: "Azure Automation을 사용하여 모니터링 경고에 대한 응답으로 Windows 가상 컴퓨터를 수직으로 확장"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ea5169c1a95f00e78ae3f5f177812466eb7a0deb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a><span data-ttu-id="0537c-103">Azure Automation을 사용하여 Windows VM 수직 확장</span><span class="sxs-lookup"><span data-stu-id="0537c-103">Vertically scale Windows VMs with Azure Automation</span></span>

<span data-ttu-id="0537c-104">수직 확장은 워크로드에 응답하여 컴퓨터의 리소스를 늘리거나 줄이는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-104">Vertical scaling is the process of increasing or decreasing the resources of a machine in response to the workload.</span></span> <span data-ttu-id="0537c-105">Azure에서는 가상 컴퓨터의 크기를 변경하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-105">In Azure this can be accomplished by changing the size of the Virtual Machine.</span></span> <span data-ttu-id="0537c-106">이는 다음과 같은 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-106">This can help in the following scenarios</span></span>

* <span data-ttu-id="0537c-107">가상 컴퓨터가 자주 사용되지 않는 경우 크기를 줄여 월별 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-107">If the Virtual Machine is not being used frequently, you can resize it down to a smaller size to reduce your monthly costs</span></span>
* <span data-ttu-id="0537c-108">가상 컴퓨터에서 최대 부하가 발생하는 경우 크기를 늘려 용량을 증가시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-108">If the Virtual Machine is seeing a peak load, it can be resized to a larger size to increase its capacity</span></span>

<span data-ttu-id="0537c-109">이 작업을 수행하는 개략적인 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-109">The outline for the steps to accomplish this is as below</span></span>

1. <span data-ttu-id="0537c-110">가상 컴퓨터에 액세스하도록 Azure 자동화 설정</span><span class="sxs-lookup"><span data-stu-id="0537c-110">Setup Azure Automation to access your Virtual Machines</span></span>
2. <span data-ttu-id="0537c-111">구독으로 Azure 자동화 수직 확장 runbook 가져오기</span><span class="sxs-lookup"><span data-stu-id="0537c-111">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="0537c-112">Runbook에 Webhook 추가</span><span class="sxs-lookup"><span data-stu-id="0537c-112">Add a webhook to your runbook</span></span>
4. <span data-ttu-id="0537c-113">가상 컴퓨터에 경고 추가</span><span class="sxs-lookup"><span data-stu-id="0537c-113">Add an alert to your Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="0537c-114">첫 번째 가상 컴퓨터의 크기로 인해 확장할 수 있는 크기가 제한될 수 있습니다. 이는 현재 가상 컴퓨터가 배포된 클러스터에서 다른 크기의 가용성 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-114">Because of the size of the first Virtual Machine, the sizes it can be scaled to, may be limited due to the availability of the other sizes in the cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="0537c-115">이 문서에서 사용된 게시된 자동화 runbook에서는 이 점을 염두에 두고 VM 크기 쌍 이내에서만 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-115">In the published automation runbooks used in this article we take care of this case and only scale within the below VM size pairs.</span></span> <span data-ttu-id="0537c-116">따라서 Standard_D1v2 가상 컴퓨터가 갑자기 Standard_G5로 확장되거나 Basic_A0으로 축소되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up to Standard_G5 or scaled down to Basic_A0.</span></span>
> 
> | <span data-ttu-id="0537c-117">VM 크기 조정 쌍</span><span class="sxs-lookup"><span data-stu-id="0537c-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="0537c-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="0537c-118">Basic_A0</span></span> |<span data-ttu-id="0537c-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="0537c-119">Basic_A4</span></span> |
> | <span data-ttu-id="0537c-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="0537c-120">Standard_A0</span></span> |<span data-ttu-id="0537c-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="0537c-121">Standard_A4</span></span> |
> | <span data-ttu-id="0537c-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="0537c-122">Standard_A5</span></span> |<span data-ttu-id="0537c-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="0537c-123">Standard_A7</span></span> |
> | <span data-ttu-id="0537c-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="0537c-124">Standard_A8</span></span> |<span data-ttu-id="0537c-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="0537c-125">Standard_A9</span></span> |
> | <span data-ttu-id="0537c-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="0537c-126">Standard_A10</span></span> |<span data-ttu-id="0537c-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="0537c-127">Standard_A11</span></span> |
> | <span data-ttu-id="0537c-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="0537c-128">Standard_D1</span></span> |<span data-ttu-id="0537c-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="0537c-129">Standard_D4</span></span> |
> | <span data-ttu-id="0537c-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="0537c-130">Standard_D11</span></span> |<span data-ttu-id="0537c-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="0537c-131">Standard_D14</span></span> |
> | <span data-ttu-id="0537c-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="0537c-132">Standard_DS1</span></span> |<span data-ttu-id="0537c-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="0537c-133">Standard_DS4</span></span> |
> | <span data-ttu-id="0537c-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="0537c-134">Standard_DS11</span></span> |<span data-ttu-id="0537c-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="0537c-135">Standard_DS14</span></span> |
> | <span data-ttu-id="0537c-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="0537c-136">Standard_D1v2</span></span> |<span data-ttu-id="0537c-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="0537c-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="0537c-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="0537c-138">Standard_D11v2</span></span> |<span data-ttu-id="0537c-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="0537c-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="0537c-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="0537c-140">Standard_G1</span></span> |<span data-ttu-id="0537c-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="0537c-141">Standard_G5</span></span> |
> | <span data-ttu-id="0537c-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="0537c-142">Standard_GS1</span></span> |<span data-ttu-id="0537c-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="0537c-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-to-access-your-virtual-machines"></a><span data-ttu-id="0537c-144">가상 컴퓨터에 액세스하도록 Azure 자동화 설정</span><span class="sxs-lookup"><span data-stu-id="0537c-144">Setup Azure Automation to access your Virtual Machines</span></span>
<span data-ttu-id="0537c-145">가장 먼저 해야 할 일은 가상 컴퓨터의 규모를 조정하는 데 사용하는 Runbook을 호스트할 Azure 자동화 계정을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-145">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale a Virtual Machine.</span></span> <span data-ttu-id="0537c-146">최근 자동화 서비스에서는 사용자 대신 Runbook을 자동으로 매우 쉽게 실행하기 위한 서비스 주체를 설정하는 "실행 계정" 기능을 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-146">Recently the Automation service introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on the user's behalf very easy.</span></span> <span data-ttu-id="0537c-147">이에 대한 자세한 내용은 아래 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0537c-147">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="0537c-148">Azure 실행 계정으로 Runbook 인증</span><span class="sxs-lookup"><span data-stu-id="0537c-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-the-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="0537c-149">구독으로 Azure 자동화 수직 확장 runbook 가져오기</span><span class="sxs-lookup"><span data-stu-id="0537c-149">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="0537c-150">가상 컴퓨터의 수직 확장에 필요한 runbook은 Azure 자동화 Runbook 갤러리에 이미 게시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-150">The runbooks that are needed for Vertically Scaling your Virtual Machine are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="0537c-151">이를 구독으로 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-151">You will need to import them into your subscription.</span></span> <span data-ttu-id="0537c-152">runbook을 가져오는 방법은 다음 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-152">You can learn how to import runbooks by reading the following article.</span></span>

* [<span data-ttu-id="0537c-153">Azure 자동화용 Runbook 및 모듈 갤러리</span><span class="sxs-lookup"><span data-stu-id="0537c-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="0537c-154">가져와야 하는 runbook이 아래 이미지에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-154">The runbooks that need to be imported are shown in the image below</span></span>

![Runbook 가져오기](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="0537c-156">Runbook에 Webhook 추가</span><span class="sxs-lookup"><span data-stu-id="0537c-156">Add a webhook to your runbook</span></span>
<span data-ttu-id="0537c-157">Runbook을 가져온 후에는 가상 컴퓨터에서 경고를 통해 트리거될 수 있도록 runbook에 Webhook를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-157">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="0537c-158">Runbook에 대한 Webhook를 만드는 자세한 방법은 여기에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-158">The details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="0537c-159">Azure 자동화 Webhook</span><span class="sxs-lookup"><span data-stu-id="0537c-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="0537c-160">다음 섹션에서 필요하므로 Webhook 대화 상자를 닫기 전에 Webhook를 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0537c-160">Make sure you copy the webhook before closing the webhook dialog as you will need this in the next section.</span></span>

## <a name="add-an-alert-to-your-virtual-machine"></a><span data-ttu-id="0537c-161">가상 컴퓨터에 경고 추가</span><span class="sxs-lookup"><span data-stu-id="0537c-161">Add an alert to your Virtual Machine</span></span>
1. <span data-ttu-id="0537c-162">가상 컴퓨터 설정 선택</span><span class="sxs-lookup"><span data-stu-id="0537c-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="0537c-163">"경고 규칙" 선택</span><span class="sxs-lookup"><span data-stu-id="0537c-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="0537c-164">"경고 추가" 선택</span><span class="sxs-lookup"><span data-stu-id="0537c-164">Select "Add alert"</span></span>
4. <span data-ttu-id="0537c-165">경고를 실행할 메트릭 선택</span><span class="sxs-lookup"><span data-stu-id="0537c-165">Select a metric to fire the alert on</span></span>
5. <span data-ttu-id="0537c-166">충족된 경우 경고를 실행할 조건 선택</span><span class="sxs-lookup"><span data-stu-id="0537c-166">Select a condition, which when fulfilled will cause the alert to fire</span></span>
6. <span data-ttu-id="0537c-167">5단계의 조건을 충족하는</span><span class="sxs-lookup"><span data-stu-id="0537c-167">Select a threshold for the condition in Step 5.</span></span> <span data-ttu-id="0537c-168">임계값 선택</span><span class="sxs-lookup"><span data-stu-id="0537c-168">to be fulfilled</span></span>
7. <span data-ttu-id="0537c-169">모니터링 서비스에서 5단계와 6단계의 조건 및 임계값을 확인할 기간 선택</span><span class="sxs-lookup"><span data-stu-id="0537c-169">Select a period over which the monitoring service will check for the condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="0537c-170">이전 섹션에서 복사한 Webhook에 붙여넣기</span><span class="sxs-lookup"><span data-stu-id="0537c-170">Paste in the webhook you copied from the previous section.</span></span>

![가상 컴퓨터 1에 경고 추가](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![가상 컴퓨터 2에 경고 추가](./media/vertical-scaling-automation/add-alert-webhook-2.png)

