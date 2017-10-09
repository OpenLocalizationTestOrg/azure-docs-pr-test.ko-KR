---
title: "Azure 로그 분석을 Surface Hub aaaMonitor | Microsoft Docs"
description: "Surface Hub의 hello Surface Hub 솔루션 tootrack hello 상태를 사용 하 고 사용 되는 방법을 이해 합니다."
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
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a><span data-ttu-id="1400a-103">Surface Hub를 로그 분석 tootrack와 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="1400a-103">Monitor Surface Hubs with Log Analytics tootrack their health</span></span>

![Surface Hub 기호](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="1400a-105">이 문서에서는 Microsoft Operations Management Suite (OMS) hello 사용 하 여 로그 분석 toomonitor Microsoft Surface Hub 장치에서 hello Surface Hub 솔루션을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-105">This article describes how you can use hello Surface Hub solution in Log Analytics toomonitor Microsoft Surface Hub devices with hello Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="1400a-106">로그 분석을 통해 사용 되는 방법을 이해 하는 것은 물론 Surface Hub의 hello 상태를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-106">Log Analytics helps you track hello health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="1400a-107">각 Surface Hub hello Microsoft Monitoring Agent 설치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-107">Each Surface Hub has hello Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="1400a-108">해당 통해 hello 에이전트 Surface Hub tooOMS에서 데이터를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-108">Its through hello agent that you can send data from your Surface Hub tooOMS.</span></span> <span data-ttu-id="1400a-109">로그 파일에서 Surface Hub 및가 읽을 수 있으며 다음 toohello OMS 서비스로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-109">Log files are read from your Surface Hubs and are then are sent toohello OMS service.</span></span> <span data-ttu-id="1400a-110">문제를 오프 라인 상태로 유지 하는 서버 hello 하지 동기화 일정 like 또는 hello 장치 계정이 Skype에 없습니다 toolog 경우 대시보드에 표시 됩니다 OMS에서 hello Surface Hub 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-110">Issues like servers being offline, hello calendar not syncing, or if hello device account is unable toolog into Skype are shown in OMS in hello Surface Hub dashboard.</span></span> <span data-ttu-id="1400a-111">Hello 대시보드에 hello 데이터를 사용 하면 다른 문제가 있는 되 고 잠재적으로 hello 검색 문제에 대 한 수정 내용을 적용 하거나 실행 하지 않는 장치를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-111">By using hello data in hello dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for hello detected issues.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="1400a-112">설치 하 고 hello 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="1400a-112">Installing and configuring hello solution</span></span>
<span data-ttu-id="1400a-113">다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-113">Use hello following information tooinstall and configure hello solution.</span></span> <span data-ttu-id="1400a-114">순서 toomanage에 hello Microsoft 작업 관리 도구 모음 (OMS)에서 Surface Hub를 사용 하 여 준비 해야 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-114">In order toomanage your Surface Hubs from hello Microsoft Operations Management Suite (OMS), you'll need hello following:</span></span>

* <span data-ttu-id="1400a-115">유효한 구독 너무[OMS](http://www.microsoft.com/oms)합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-115">A valid subscription too[OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="1400a-116">[OMS 구독](https://azure.microsoft.com/pricing/details/log-analytics/) 수준 hello 수를 지 원하는 toomonitor 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support hello number of devices you want toomonitor.</span></span> <span data-ttu-id="1400a-117">OMS 가격 책정은 등록하는 장치 수와 처리할 데이터양에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="1400a-118">합니다 tootake이 고려 Surface Hub 배포를 계획 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="1400a-118">You'll want tootake this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="1400a-119">다음으로 추가 OMS 구독 tooyour 기존 Microsoft Azure 구독 하거나 직접 hello OMS 포털을 통해 새 작업 영역 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-119">Next, you will either add an OMS subscription tooyour existing Microsoft Azure subscription or create a new workspace directly through hello OMS portal.</span></span> <span data-ttu-id="1400a-120">이 방법들에 대한 자세한 지침은 [Log Analytics 시작](log-analytics-get-started.md)에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="1400a-121">Hello OMS 구독 설정 되 고 나면는 두 가지 방법으로 tooenroll Surface Hub 장치</span><span class="sxs-lookup"><span data-stu-id="1400a-121">Once hello OMS subscription is set up, there are two ways tooenroll your Surface Hub devices:</span></span>

* <span data-ttu-id="1400a-122">InTune을 통해 자동으로</span><span class="sxs-lookup"><span data-stu-id="1400a-122">Automatically through Intune</span></span>
* <span data-ttu-id="1400a-123">Surface Hub 장치의 **설정**을 통한 수동 등록</span><span class="sxs-lookup"><span data-stu-id="1400a-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="1400a-124">모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="1400a-124">Set up monitoring</span></span>
<span data-ttu-id="1400a-125">OMS의 로그 분석을 사용 하 여 Surface Hub의 hello 상태 및 활동을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-125">You can monitor hello health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="1400a-126">Intune을 사용 하 여 또는 사용 하 여 로컬로 hello Surface Hub OMS에 등록할 수 있습니다 **설정을** hello Surface Hub에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-126">You can enroll hello Surface Hub in OMS by using Intune, or locally by using **Settings** on hello Surface Hub.</span></span>

## <a name="connect-surface-hubs-toooms-through-intune"></a><span data-ttu-id="1400a-127">Intune을 통해 Surface Hub tooOMS 연결</span><span class="sxs-lookup"><span data-stu-id="1400a-127">Connect Surface Hubs tooOMS through Intune</span></span>
<span data-ttu-id="1400a-128">작업 영역 ID와 작업 영역 키 Surface Hub를 관리 하는 hello OMS 작업 영역에 대 한 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-128">You'll need hello workspace ID and workspace key for hello OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="1400a-129">Hello OMS 포털에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-129">You can get those from hello OMS portal.</span></span>

<span data-ttu-id="1400a-130">Intune은 toocentrally 수 있는 Microsoft 제품이 적용 된 tooone 이상의 장치 hello OMS 구성 설정을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-130">Intune is a Microsoft product that allows you toocentrally manage hello OMS configuration settings that are applied tooone or more of your devices.</span></span> <span data-ttu-id="1400a-131">이러한 단계 tooconfigure Intune 통해 장치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-131">Follow these steps tooconfigure your devices through Intune:</span></span>

1. <span data-ttu-id="1400a-132">TooIntune에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-132">Sign in tooIntune.</span></span>
2. <span data-ttu-id="1400a-133">너무 이동**설정** > **연결 된 원본**합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-133">Navigate too**Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="1400a-134">만들거나 hello Surface Hub 템플릿을 기반으로 하는 정책을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-134">Create or edit a policy based on hello Surface Hub template.</span></span>
4. <span data-ttu-id="1400a-135">Hello 정책의 toohello OMS (Azure Operational Insights) 섹션을 이동 하 고 hello 추가 *작업 영역 ID* 및 *작업 영역 키* toohello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-135">Navigate toohello OMS (Azure Operational Insights) section of hello policy, and add hello *Workspace ID* and *Workspace Key* toohello policy.</span></span>
5. <span data-ttu-id="1400a-136">Hello 정책을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-136">Save hello policy.</span></span>
6. <span data-ttu-id="1400a-137">Hello 정책과 hello 적절 한 장치 그룹을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-137">Associate hello policy with hello appropriate group of devices.</span></span>

   ![InTune 정책](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="1400a-139">Intune은 다음 hello OMS 설정 hello 대상 그룹에서 OMS 작업 영역에서이 등록 hello 장치와 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-139">Intune then syncs hello OMS settings with hello devices in hello target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a><span data-ttu-id="1400a-140">Surface Hub tooOMS hello 설정 앱을 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="1400a-140">Connect Surface Hubs tooOMS using hello Settings app</span></span>
<span data-ttu-id="1400a-141">작업 영역 ID와 작업 영역 키 Surface Hub를 관리 하는 hello OMS 작업 영역에 대 한 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-141">You'll need hello workspace ID and workspace key for hello OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="1400a-142">Hello OMS 포털에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-142">You can get those from hello OMS portal.</span></span>

<span data-ttu-id="1400a-143">통해 직접 장치를 등록할 수 Intune toomanage 환경을 사용 하지 않는 경우 **설정을** 각 Surface Hub에:</span><span class="sxs-lookup"><span data-stu-id="1400a-143">If you don't use Intune toomanage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="1400a-144">Surface Hub에서 **설정**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="1400a-145">Hello 대화 상자가 나타나면의 장치 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-145">Enter hello device admin credentials when prompted.</span></span>
3. <span data-ttu-id="1400a-146">클릭 **이 장치**, 아래 hello 및 **모니터링**, 클릭 **OMS 설정 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-146">Click **This device**, and hello under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="1400a-147">**모니터링 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="1400a-148">Hello OMS 설정 대화 상자에 입력 hello **작업 영역 ID** 및 형식 hello **작업 영역 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-148">In hello OMS settings dialog, type hello **Workspace ID** and type hello **Workspace Key**.</span></span>  
   <span data-ttu-id="1400a-149">![설정](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="1400a-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="1400a-150">클릭 **확인** toocomplete hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-150">Click **OK** toocomplete hello configuration.</span></span>

<span data-ttu-id="1400a-151">확인 된 OMS 구성을 성공적으로 hello toohello 장치를 적용 하는 여부를 알려 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-151">A confirmation appears telling you whether or not hello OMS configuration was successfully applied toohello device.</span></span> <span data-ttu-id="1400a-152">에 있는 경우 해당 hello 에이전트 toohello OMS 서비스를 성공적으로 연결 되었다는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-152">If it was, a message appears stating that hello agent successfully connected toohello OMS service.</span></span> <span data-ttu-id="1400a-153">hello 장치 볼 수 있으며, 작업을 수행 하는 데이터 tooOMS를 보내기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-153">hello device then starts sending data tooOMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="1400a-154">Surface Hub 모니터링</span><span class="sxs-lookup"><span data-stu-id="1400a-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="1400a-155">OMS를 통한 Surface Hub 모니터링은 등록된 다른 장치 모니터링과 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="1400a-156">OMS 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-156">Sign in toohello OMS portal.</span></span>
2. <span data-ttu-id="1400a-157">Toohello Surface Hub 솔루션 팩 대시보드를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-157">Navigate toohello Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="1400a-158">장치 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-158">Your device's health is displayed.</span></span>

   ![Surface Hub 대시보드](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="1400a-160">기존 또는 사용자 지정 로그 검색에 기반한 [경고](log-analytics-alerts.md)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="1400a-161">Surface Hub에서 OMS에서 수집 하는 hello 데이터 hello를 사용 하 여, 문제 및 장치에 대해 정의 하는 hello 조건에는 경고에 대 한 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-161">Using hello data hello OMS collects from your Surface Hubs, you can search for issues and alert on hello conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1400a-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1400a-162">Next steps</span></span>
* <span data-ttu-id="1400a-163">사용 하 여 [로그 분석 검색 로그인](log-analytics-log-searches.md) tooview Surface Hub 데이터를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Surface Hub data.</span></span>
* <span data-ttu-id="1400a-164">만들 [경고](log-analytics-alerts.md) toonotify Surface Hub 문제가 발생 하는 경우 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400a-164">Create [alerts](log-analytics-alerts.md) toonotify you when issues occur with your Surface Hubs.</span></span>
