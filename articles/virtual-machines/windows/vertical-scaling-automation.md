---
title: "Azure 자동화 toovertically aaaUse Windows 가상 컴퓨터의 크기를 조정 | Microsoft Docs"
description: "세로로 응답 toomonitoring 알림 Azure 자동화에서 Windows 가상 컴퓨터 크기를 조정합니다"
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
ms.openlocfilehash: 24d07f3e2e217668f18676e6d6873be4f9770349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a><span data-ttu-id="2306c-103">Azure Automation을 사용하여 Windows VM 수직 확장</span><span class="sxs-lookup"><span data-stu-id="2306c-103">Vertically scale Windows VMs with Azure Automation</span></span>

<span data-ttu-id="2306c-104">세로 배율는 증가 또는 감소 응답 toohello 작업에서 컴퓨터의 hello 리소스의 hello 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-104">Vertical scaling is hello process of increasing or decreasing hello resources of a machine in response toohello workload.</span></span> <span data-ttu-id="2306c-105">Azure의 hello 가상 컴퓨터의 hello 크기를 변경 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-105">In Azure this can be accomplished by changing hello size of hello Virtual Machine.</span></span> <span data-ttu-id="2306c-106">이 hello 다음 시나리오에에서 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-106">This can help in hello following scenarios</span></span>

* <span data-ttu-id="2306c-107">가상 컴퓨터 hello 자주 사용 하지 않으면, 조정할 수 있습니다 더 작은 크기 tooreduce tooa 아래로 월별 비용</span><span class="sxs-lookup"><span data-stu-id="2306c-107">If hello Virtual Machine is not being used frequently, you can resize it down tooa smaller size tooreduce your monthly costs</span></span>
* <span data-ttu-id="2306c-108">수 hello 가상 컴퓨터는 최대 부하를 보고 하는 경우 크기가 조정 된 tooa 더 큰 크기 tooincrease 용량과 수</span><span class="sxs-lookup"><span data-stu-id="2306c-108">If hello Virtual Machine is seeing a peak load, it can be resized tooa larger size tooincrease its capacity</span></span>

<span data-ttu-id="2306c-109">이 목록은 hello 단계 tooaccomplish에 대 한 hello 개요 아래</span><span class="sxs-lookup"><span data-stu-id="2306c-109">hello outline for hello steps tooaccomplish this is as below</span></span>

1. <span data-ttu-id="2306c-110">Azure 자동화 tooaccess 가상 컴퓨터 설정</span><span class="sxs-lookup"><span data-stu-id="2306c-110">Setup Azure Automation tooaccess your Virtual Machines</span></span>
2. <span data-ttu-id="2306c-111">구독에 hello Azure 자동화 세로 배율 runbook 가져오기</span><span class="sxs-lookup"><span data-stu-id="2306c-111">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="2306c-112">Webhook tooyour runbook 추가</span><span class="sxs-lookup"><span data-stu-id="2306c-112">Add a webhook tooyour runbook</span></span>
4. <span data-ttu-id="2306c-113">경고는 tooyour 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-113">Add an alert tooyour Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="2306c-114">Hello hello 크기 때문에 첫 번째 가상 컴퓨터를 확장할 수 있습니다 hello 크기 제한 될 수 있습니다 hello의 가용성을 toohello 인해 hello 클러스터에 다른 크기 현재 가상 컴퓨터 배포에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-114">Because of hello size of hello first Virtual Machine, hello sizes it can be scaled to, may be limited due toohello availability of hello other sizes in hello cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="2306c-115">Hello이이 경우 처리 하 고 VM 크기 쌍 아래 hello 내로 확장할이 문서에서 사용 하는 자동화 runbook을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-115">In hello published automation runbooks used in this article we take care of this case and only scale within hello below VM size pairs.</span></span> <span data-ttu-id="2306c-116">이 있음을 의미 Standard_D1v2 가상 컴퓨터는 하지 갑자기 수 tooStandard_G5 수직 확장 tooBasic_A0 축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up tooStandard_G5 or scaled down tooBasic_A0.</span></span>
> 
> | <span data-ttu-id="2306c-117">VM 크기 조정 쌍</span><span class="sxs-lookup"><span data-stu-id="2306c-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="2306c-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="2306c-118">Basic_A0</span></span> |<span data-ttu-id="2306c-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="2306c-119">Basic_A4</span></span> |
> | <span data-ttu-id="2306c-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="2306c-120">Standard_A0</span></span> |<span data-ttu-id="2306c-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="2306c-121">Standard_A4</span></span> |
> | <span data-ttu-id="2306c-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="2306c-122">Standard_A5</span></span> |<span data-ttu-id="2306c-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="2306c-123">Standard_A7</span></span> |
> | <span data-ttu-id="2306c-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="2306c-124">Standard_A8</span></span> |<span data-ttu-id="2306c-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="2306c-125">Standard_A9</span></span> |
> | <span data-ttu-id="2306c-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="2306c-126">Standard_A10</span></span> |<span data-ttu-id="2306c-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="2306c-127">Standard_A11</span></span> |
> | <span data-ttu-id="2306c-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="2306c-128">Standard_D1</span></span> |<span data-ttu-id="2306c-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="2306c-129">Standard_D4</span></span> |
> | <span data-ttu-id="2306c-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="2306c-130">Standard_D11</span></span> |<span data-ttu-id="2306c-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="2306c-131">Standard_D14</span></span> |
> | <span data-ttu-id="2306c-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="2306c-132">Standard_DS1</span></span> |<span data-ttu-id="2306c-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="2306c-133">Standard_DS4</span></span> |
> | <span data-ttu-id="2306c-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="2306c-134">Standard_DS11</span></span> |<span data-ttu-id="2306c-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="2306c-135">Standard_DS14</span></span> |
> | <span data-ttu-id="2306c-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="2306c-136">Standard_D1v2</span></span> |<span data-ttu-id="2306c-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="2306c-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="2306c-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="2306c-138">Standard_D11v2</span></span> |<span data-ttu-id="2306c-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="2306c-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="2306c-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="2306c-140">Standard_G1</span></span> |<span data-ttu-id="2306c-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="2306c-141">Standard_G5</span></span> |
> | <span data-ttu-id="2306c-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="2306c-142">Standard_GS1</span></span> |<span data-ttu-id="2306c-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="2306c-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a><span data-ttu-id="2306c-144">Azure 자동화 tooaccess 가상 컴퓨터 설정</span><span class="sxs-lookup"><span data-stu-id="2306c-144">Setup Azure Automation tooaccess your Virtual Machines</span></span>
<span data-ttu-id="2306c-145">hello가 가장 먼저 toodo 필요한 가상 컴퓨터를 사용 하는 runbook tooscale hello 호스팅할 Azure 자동화 계정 만들기.</span><span class="sxs-lookup"><span data-stu-id="2306c-145">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale a Virtual Machine.</span></span> <span data-ttu-id="2306c-146">최근에 hello 자동화 서비스는 hello 서비스 사용자 설치를 위해 자동으로 실행 중인 hello runbook hello 사용자 대신 매우 쉽게 hello "계정으로 실행" 기능을 소개 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-146">Recently hello Automation service introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on hello user's behalf very easy.</span></span> <span data-ttu-id="2306c-147">자세한 내용은 아래 hello 기술 자료 문서에서이 내용을:</span><span class="sxs-lookup"><span data-stu-id="2306c-147">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="2306c-148">Azure 실행 계정으로 Runbook 인증</span><span class="sxs-lookup"><span data-stu-id="2306c-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="2306c-149">구독에 hello Azure 자동화 세로 배율 runbook 가져오기</span><span class="sxs-lookup"><span data-stu-id="2306c-149">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="2306c-150">가상 컴퓨터에 이미 게시 되어 수직 확장에 필요한 hello runbook hello Azure 자동화 Runbook 갤러리입니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-150">hello runbooks that are needed for Vertically Scaling your Virtual Machine are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="2306c-151">Tooimport 해야 구독에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-151">You will need tooimport them into your subscription.</span></span> <span data-ttu-id="2306c-152">다음 문서를 읽음으로써 tooimport runbook hello 하는 방법을 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-152">You can learn how tooimport runbooks by reading hello following article.</span></span>

* [<span data-ttu-id="2306c-153">Azure 자동화용 Runbook 및 모듈 갤러리</span><span class="sxs-lookup"><span data-stu-id="2306c-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="2306c-154">가져온 toobe 해야 하는 hello runbook hello 이미지 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-154">hello runbooks that need toobe imported are shown in hello image below</span></span>

![Runbook 가져오기](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="2306c-156">Webhook tooyour runbook 추가</span><span class="sxs-lookup"><span data-stu-id="2306c-156">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="2306c-157">Hello runbook을 가져온 후 가상 컴퓨터에서 발생 한 경고에 의해 트리거될 수 있으므로 tooadd webhook toohello runbook 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-157">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="2306c-158">Runbook에 대 한는 webhook를 만드는 hello 세부 정보는 여기에 읽을 수합니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-158">hello details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="2306c-159">Azure 자동화 Webhook</span><span class="sxs-lookup"><span data-stu-id="2306c-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="2306c-160">Hello 다음 섹션에서이 필요 하므로 hello webhook 대화 상자를 닫기 전에 hello webhook을 복사 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-160">Make sure you copy hello webhook before closing hello webhook dialog as you will need this in hello next section.</span></span>

## <a name="add-an-alert-tooyour-virtual-machine"></a><span data-ttu-id="2306c-161">경고는 tooyour 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-161">Add an alert tooyour Virtual Machine</span></span>
1. <span data-ttu-id="2306c-162">가상 컴퓨터 설정 선택</span><span class="sxs-lookup"><span data-stu-id="2306c-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="2306c-163">"경고 규칙" 선택</span><span class="sxs-lookup"><span data-stu-id="2306c-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="2306c-164">"경고 추가" 선택</span><span class="sxs-lookup"><span data-stu-id="2306c-164">Select "Add alert"</span></span>
4. <span data-ttu-id="2306c-165">메트릭 toofire hello 경고를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-165">Select a metric toofire hello alert on</span></span>
5. <span data-ttu-id="2306c-166">조건을 선택할 수 있는 경우에 수행 됩니다 hello 경고 toofire 발생</span><span class="sxs-lookup"><span data-stu-id="2306c-166">Select a condition, which when fulfilled will cause hello alert toofire</span></span>
6. <span data-ttu-id="2306c-167">5 단계에서에서 hello 조건에 대 한 임계값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-167">Select a threshold for hello condition in Step 5.</span></span> <span data-ttu-id="2306c-168">fulfilled toobe</span><span class="sxs-lookup"><span data-stu-id="2306c-168">toobe fulfilled</span></span>
7. <span data-ttu-id="2306c-169">5 단계 및 6에서 hello 조건 및 임계값에 대 한 어떤 hello를 통해 모니터링 서비스는 확인 기간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-169">Select a period over which hello monitoring service will check for hello condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="2306c-170">Hello 이전 섹션에서 복사한 hello webhook에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2306c-170">Paste in hello webhook you copied from hello previous section.</span></span>

![경고 tooVirtual 컴퓨터 1 추가](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![경고 tooVirtual 컴퓨터 2 추가](./media/vertical-scaling-automation/add-alert-webhook-2.png)

