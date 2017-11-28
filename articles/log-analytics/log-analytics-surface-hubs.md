---
title: "Azure Log Analytics로 Surface Hub 모니터링 | Microsoft Docs"
description: "Surface Hub 솔루션으로 Surface Hub 상태를 추적하여 Surface Hub가 사용되고 있는 방식을 파악합니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6ecd0d09589fec85c1633f528afc1165c346b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-to-track-their-health"></a><span data-ttu-id="e6955-103">Log Analytics로 Surface Hub를 모니터링하여 상태 추적</span><span class="sxs-lookup"><span data-stu-id="e6955-103">Monitor Surface Hubs with Log Analytics to track their health</span></span>

![Surface Hub 기호](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="e6955-105">이 문서에서는 Log Analytics의 Surface Hub 솔루션을 사용하여 Microsoft OMS(Operations Management Suite)를 통해 Microsoft Surface Hub 장치를 모니터링하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-105">This article describes how you can use the Surface Hub solution in Log Analytics to monitor Microsoft Surface Hub devices with the Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="e6955-106">Log Analytics는 Surface Hub 상태를 추적하여 Surface Hub가 사용되고 있는 방식을 파악하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-106">Log Analytics helps you track the health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="e6955-107">Surface Hub마다 Microsoft Monitoring Agent가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-107">Each Surface Hub has the Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="e6955-108">에이전트를 통해야만 데이터를 Surface Hub에서 OMS로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-108">Its through the agent that you can send data from your Surface Hub to OMS.</span></span> <span data-ttu-id="e6955-109">로그 파일은 먼저 Surface Hub에서 읽은 다음 OMS 서비스로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-109">Log files are read from your Surface Hubs and are then are sent to the OMS service.</span></span> <span data-ttu-id="e6955-110">오프라인 상태에 있는 서버, 동기화되지 않는 일정 또는 Skype에 로그인할 수 없는 장치 계정과 같은 문제들이 OMS의 Surface Hub 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-110">Issues like servers being offline, the calendar not syncing, or if the device account is unable to log into Skype are shown in OMS in the Surface Hub dashboard.</span></span> <span data-ttu-id="e6955-111">대시보드의 데이터를 통해 실행되지 않거나 다른 문제가 있는 장치를 확인하고, 잠재적으로는 발견된 문제에 대한 픽스도 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-111">By using the data in the dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for the detected issues.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="e6955-112">솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="e6955-112">Installing and configuring the solution</span></span>
<span data-ttu-id="e6955-113">다음 정보를 사용하여 솔루션을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-113">Use the following information to install and configure the solution.</span></span> <span data-ttu-id="e6955-114">Microsoft OMS에서 Surface Hub를 관리하는 데 필요한 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-114">In order to manage your Surface Hubs from the Microsoft Operations Management Suite (OMS), you'll need the following:</span></span>

* <span data-ttu-id="e6955-115">[OMS](http://www.microsoft.com/oms)에 유효한 구독</span><span class="sxs-lookup"><span data-stu-id="e6955-115">A valid subscription to [OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="e6955-116">모니터링할 장치의 수를 지원하는 [OMS 구독](https://azure.microsoft.com/pricing/details/log-analytics/) 수준.</span><span class="sxs-lookup"><span data-stu-id="e6955-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support the number of devices you want to monitor.</span></span> <span data-ttu-id="e6955-117">OMS 가격 책정은 등록하는 장치 수와 처리할 데이터양에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="e6955-118">Surface Hub 롤아웃을 계획할 때 이 점을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-118">You'll want to take this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="e6955-119">다음으로 OMS 구독을 기존 Microsoft Azure 구독에 추가하거나 OMS 포털을 통해 직접 새 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-119">Next, you will either add an OMS subscription to your existing Microsoft Azure subscription or create a new workspace directly through the OMS portal.</span></span> <span data-ttu-id="e6955-120">이 방법들에 대한 자세한 지침은 [Log Analytics 시작](log-analytics-get-started.md)에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="e6955-121">일단 OMS 구독을 설정한 후에 Surface Hub 장치를 등록하는 두 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-121">Once the OMS subscription is set up, there are two ways to enroll your Surface Hub devices:</span></span>

* <span data-ttu-id="e6955-122">InTune을 통해 자동으로</span><span class="sxs-lookup"><span data-stu-id="e6955-122">Automatically through Intune</span></span>
* <span data-ttu-id="e6955-123">Surface Hub 장치의 **설정**을 통한 수동 등록</span><span class="sxs-lookup"><span data-stu-id="e6955-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="e6955-124">모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="e6955-124">Set up monitoring</span></span>
<span data-ttu-id="e6955-125">OMS에서 Log Analytics를 사용하여 Surface Hub의 상태와 활동을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-125">You can monitor the health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="e6955-126">InTune을 사용하거나 로컬로 Surface Hub의 **설정**을 사용하여 해당 Surface Hub를 OMS에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-126">You can enroll the Surface Hub in OMS by using Intune, or locally by using **Settings** on the Surface Hub.</span></span>

## <a name="connect-surface-hubs-to-oms-through-intune"></a><span data-ttu-id="e6955-127">InTune 통해 OMS에 Surface Hub 연결</span><span class="sxs-lookup"><span data-stu-id="e6955-127">Connect Surface Hubs to OMS through Intune</span></span>
<span data-ttu-id="e6955-128">Surface Hub를 관리할 OMS 작업 영역에 대한 작업 영역 ID 및 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-128">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="e6955-129">이 ID와 키는 OMS 포털에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-129">You can get those from the OMS portal.</span></span>

<span data-ttu-id="e6955-130">InTune은 하나 이상의 장치에 적용되는 OMS 구성 설정을 중앙에서 관리할 수 있게 하는 Microsoft 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-130">Intune is a Microsoft product that allows you to centrally manage the OMS configuration settings that are applied to one or more of your devices.</span></span> <span data-ttu-id="e6955-131">InTune 통해 장치를 구성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-131">Follow these steps to configure your devices through Intune:</span></span>

1. <span data-ttu-id="e6955-132">InTune에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-132">Sign in to Intune.</span></span>
2. <span data-ttu-id="e6955-133">**설정** > **연결된 원본**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-133">Navigate to **Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="e6955-134">Surface Hub 템플릿을 기반으로 하는 정책을 만들거나 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-134">Create or edit a policy based on the Surface Hub template.</span></span>
4. <span data-ttu-id="e6955-135">정책의 OMS (Azure Operational Insights) 섹션으로 이동한 다음 해당 정책에 *작업 영역 ID* 및 *작업 영역 키*를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-135">Navigate to the OMS (Azure Operational Insights) section of the policy, and add the *Workspace ID* and *Workspace Key* to the policy.</span></span>
5. <span data-ttu-id="e6955-136">해당 정책을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-136">Save the policy.</span></span>
6. <span data-ttu-id="e6955-137">장치가 속한 그룹에 해당 정책을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-137">Associate the policy with the appropriate group of devices.</span></span>

   ![InTune 정책](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="e6955-139">그런 다음 InTune에서 대상 그룹의 장치와 OMS 설정을 동기화하여 OMS 작업 영역에 해당 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-139">Intune then syncs the OMS settings with the devices in the target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-to-oms-using-the-settings-app"></a><span data-ttu-id="e6955-140">설정 앱을 통해 OMS에 Surface Hub 연결</span><span class="sxs-lookup"><span data-stu-id="e6955-140">Connect Surface Hubs to OMS using the Settings app</span></span>
<span data-ttu-id="e6955-141">Surface Hub를 관리할 OMS 작업 영역에 대한 작업 영역 ID 및 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-141">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="e6955-142">이 ID와 키는 OMS 포털에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-142">You can get those from the OMS portal.</span></span>

<span data-ttu-id="e6955-143">사용자 환경을 관리하는 데 InTune을 사용하지 않을 경우 다음과 같이 각 Surface Hub의 **설정**을 통해 수동으로 장치를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-143">If you don't use Intune to manage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="e6955-144">Surface Hub에서 **설정**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="e6955-145">메시지가 표시되면 장치 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-145">Enter the device admin credentials when prompted.</span></span>
3. <span data-ttu-id="e6955-146">**이 장치**를 클릭한 다음 **모니터링** 아래에서 **OMS 설정 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-146">Click **This device**, and the under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="e6955-147">**모니터링 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="e6955-148">OMS 설정 대화 상자에서 **작업 영역 ID**, **작업 영역 키**를 차례로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-148">In the OMS settings dialog, type the **Workspace ID** and type the **Workspace Key**.</span></span>  
   <span data-ttu-id="e6955-149">![설정](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="e6955-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="e6955-150">**확인**을 클릭하여 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-150">Click **OK** to complete the configuration.</span></span>

<span data-ttu-id="e6955-151">장치에 OMS 구성이 성공적으로 적용되었는지 여부를 알리는 확인 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-151">A confirmation appears telling you whether or not the OMS configuration was successfully applied to the device.</span></span> <span data-ttu-id="e6955-152">성공한 경우에는 에이전트가 OMS 서비스에 올바르게 연결되었다고 알리는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-152">If it was, a message appears stating that the agent successfully connected to the OMS service.</span></span> <span data-ttu-id="e6955-153">그러면 해당 장치에서 데이터를 확인하고 작업할 수 있는 OMS로 이 데이터를 보내기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-153">The device then starts sending data to OMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="e6955-154">Surface Hub 모니터링</span><span class="sxs-lookup"><span data-stu-id="e6955-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="e6955-155">OMS를 통한 Surface Hub 모니터링은 등록된 다른 장치 모니터링과 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="e6955-156">OMS 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-156">Sign in to the OMS portal.</span></span>
2. <span data-ttu-id="e6955-157">Surface Hub 솔루션 팩 대시보드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-157">Navigate to the Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="e6955-158">장치 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-158">Your device's health is displayed.</span></span>

   ![Surface Hub 대시보드](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="e6955-160">기존 또는 사용자 지정 로그 검색에 기반한 [경고](log-analytics-alerts.md)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="e6955-161">OMS에서 Surface Hub로부터 수집한 데이터를 사용하면 문제를 검색하여 장치에 정의하는 조건에 대해 경고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6955-161">Using the data the OMS collects from your Surface Hubs, you can search for issues and alert on the conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6955-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6955-162">Next steps</span></span>
* <span data-ttu-id="e6955-163">[Log Analytics에서 로그 검색](log-analytics-log-searches.md)을 통한 자세한 Surface Hub 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="e6955-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Surface Hub data.</span></span>
* <span data-ttu-id="e6955-164">Surface Hub 문제 발생 시 알리는 [경고](log-analytics-alerts.md) 만들기</span><span class="sxs-lookup"><span data-stu-id="e6955-164">Create [alerts](log-analytics-alerts.md) to notify you when issues occur with your Surface Hubs.</span></span>
