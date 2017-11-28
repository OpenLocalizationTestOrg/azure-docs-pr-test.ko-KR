---
title: "StorSimple 가상 배열에 0.5 업데이트 aaaInstall | Microsoft Docs"
description: "Toouse hello StorSimple 가상 배열 웹 UI tooapply 업데이트를 사용 하 여 Azure 포털 및 핫픽스 메서드 hello 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a><span data-ttu-id="cd240-103">StorSimple 가상 배열에 업데이트 0.5 설치</span><span class="sxs-lookup"><span data-stu-id="cd240-103">Install Update 0.5 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="cd240-104">개요</span><span class="sxs-lookup"><span data-stu-id="cd240-104">Overview</span></span>

<span data-ttu-id="cd240-105">이 문서에서는 hello 로컬 웹 UI 통해 및 hello Azure 포털을 통해 StorSimple 가상 배열에 hello 단계 필요한 tooinstall 0.5 업데이트를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-105">This article describes hello steps required tooinstall Update 0.5 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="cd240-106">필요한 소프트웨어 업데이트 또는 핫픽스 tookeep tooapply StorSimple 가상 배열 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="cd240-107">업데이트를 적용 하기 전에 수행한 hello 볼륨 또는 공유 hello에 오프 라인에서 먼저 호스트 및 다음 장치를 hello 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="cd240-108">이렇게 하면 데이터 손상 가능성이 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="cd240-109">Hello 볼륨 또는 공유가 오프 라인 상태인 후 취해야 수동 hello 장치의 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="cd240-110">업데이트 0.5 너무 해당**10.0.10290.0** 장치에서 소프트웨어 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-110">Update 0.5 corresponds too**10.0.10290.0** software version on your device.</span></span> <span data-ttu-id="cd240-111">이 업데이트의 새로운 기능에 대 한 내용은 이동 너무[0.5 업데이트에 대 한 릴리스 정보](storsimple-virtual-array-update-05-release-notes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-111">For information on what is new in this update, go too[Release notes for Update 0.5](storsimple-virtual-array-update-05-release-notes.md).</span></span>
>
> - <span data-ttu-id="cd240-112">이상 버전에서는 것을 권장 합니다 또는 0.2 업데이트를 실행 하는 경우 hello Azure 포털을 통해 hello 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="cd240-113">업데이트 0.1 또는 GA 소프트웨어 버전을 실행 하는 경우에 hello 로컬 웹 UI tooinstall 0.5 업데이트를 통해 hello 핫픽스 메서드를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.5.</span></span>
>
> - <span data-ttu-id="cd240-114">업데이트 또는 핫픽스를 설치하면 장치가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="cd240-115">주어진는 hello StorSimple 가상 배열은 단일 노드에 장치, 진행 중인 모든 I/O 중단 된와 장치에 가동 중지 시간이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="cd240-116">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="cd240-116">Use hello Azure portal</span></span>

<span data-ttu-id="cd240-117">업데이트를 0.2 이상을 실행 하는 경우에 hello Azure 포털을 통해 업데이트를 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="cd240-118">hello 포털 프로시저 hello 사용자 tooscan 필요 하 고, 다운로드 및 다음 hello 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="cd240-119">이 프로시저는 약 7 분 toocomplete.</span><span class="sxs-lookup"><span data-stu-id="cd240-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="cd240-120">Hello 다음이 수행 단계 tooinstall hello 업데이트나 핫픽스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="cd240-121">Hello 후 설치 완료, 이동 tooyour StorSimple 장치 관리자 서비스는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="cd240-122">선택 **장치** 다음 선택 하 고 방금 업데이트 hello 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="cd240-123">너무 이동**설정 > 관리 > 장치 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="cd240-124">표시 되는 hello 소프트웨어 버전 이어야 합니다 **10.0.10290.0**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-124">hello displayed software version should be **10.0.10290.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="cd240-125">Hello 로컬 웹 UI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="cd240-125">Use hello local web UI</span></span>

<span data-ttu-id="cd240-126">Hello 로컬 웹 UI를 사용 하는 데는 두 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="cd240-127">Hello 업데이트 또는 hello 핫픽스를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="cd240-128">Hello 업데이트 또는 hello 핫픽스 설치</span><span class="sxs-lookup"><span data-stu-id="cd240-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="cd240-129">Hello 업데이트 또는 hello 핫픽스를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="cd240-130">Hello hello Microsoft Update 카탈로그에서에서 단계 toodownload hello 소프트웨어 업데이트를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="cd240-131">toodownload hello 업데이트나 hello 핫픽스</span><span class="sxs-lookup"><span data-stu-id="cd240-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="cd240-132">Internet Explorer를 시작 하 고 탐색 너무[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="cd240-133">Microsoft Update 카탈로그 hello를 사용 하 여이 컴퓨터에 처음으로 이면 클릭 **설치** 때 메시지 표시 tooinstall hello Microsoft Update 카탈로그 추가 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-133">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="cd240-134">Hello 기술 자료 (KB) 번호를 입력 hello Microsoft Update 카탈로그의 hello 검색 상자에 원하는 toodownload hello 핫픽스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="cd240-135">업데이트 0.5의 경우 **4021576**을 입력하고 **검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-135">Enter **4021576** for Update 0.5, and then click **Search**.</span></span>
   
    <span data-ttu-id="cd240-136">hello 핫픽스 목록이 표시 되 면 예를 들어 **StorSimple 가상 배열 업데이트 0.5**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.5**.</span></span>
   
    ![카탈로그 검색](./media/storsimple-virtual-array-install-update-05/download1.png)

4. <span data-ttu-id="cd240-138">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-138">Click **Download**.</span></span> 

5. <span data-ttu-id="cd240-139">두 개의 파일 toodownload 표시 됩니다는 *.msu* 및 *.cab* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-139">You should see two files toodownload, a *.msu* and a *.cab* file.</span></span> <span data-ttu-id="cd240-140">이러한 파일 tooa 폴더의 각를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="cd240-141">hello 폴더 hello 장치에서 연결할 수 있는 tooa 복사한 네트워크 공유 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="cd240-142">Hello 파일이 있는 hello 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="cd240-143">![Hello 패키지의 파일](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span><span class="sxs-lookup"><span data-stu-id="cd240-143">![Files in hello package](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span></span>

    <span data-ttu-id="cd240-144">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-144">You see:</span></span>
    -  <span data-ttu-id="cd240-145">Microsoft 업데이트 독립 실행형 패키지 파일 `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="cd240-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="cd240-146">이 파일은 사용 되는 tooupdate hello 장치 소프트웨어.</span><span class="sxs-lookup"><span data-stu-id="cd240-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="cd240-147">Geneva 모니터링 에이전트 패키지 파일 `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="cd240-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="cd240-148">이 파일은 사용 되는 tooupdate hello 모니터링 및 진단 서비스 (MDS) 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="cd240-149">Hello cab 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-149">Double-click hello cab file.</span></span> <span data-ttu-id="cd240-150">.msi가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-150">A .msi is displayed.</span></span> <span data-ttu-id="cd240-151">선택 hello 파일을 마우스 오른쪽 단추로 클릭 한 다음 **추출** hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="cd240-152">Hello를 사용 하 여 _.msi_ 파일 tooupdate hello 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-152">You will use hello _.msi_ file tooupdate hello agent.</span></span>

        ![MDS 에이전트 업데이트 파일 압축 풀기](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="cd240-154">Hello 업데이트 또는 hello 핫픽스 설치</span><span class="sxs-lookup"><span data-stu-id="cd240-154">Install hello update or hello hotfix</span></span>

<span data-ttu-id="cd240-155">이전 toohello 업데이트 또는 핫픽스 설치 hello 업데이트가 설치 되어 있거나 호스트에서 로컬로 hello 핫픽스 다운로드 하 고 있는지 또는 네트워크 공유를 통해 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-155">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="cd240-156">GA를 실행 하는 장치에이 메서드가 tooinstall 업데이트를 사용 하거나 0.1 소프트웨어 버전으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-156">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="cd240-157">이 프로시저는 2 분 toocomplete 보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-157">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="cd240-158">Hello 다음이 수행 단계 tooinstall hello 업데이트나 핫픽스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-158">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="cd240-159">tooinstall hello 업데이트나 hello 핫픽스</span><span class="sxs-lookup"><span data-stu-id="cd240-159">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="cd240-160">Hello 로컬 웹 UI에서에서 이동 너무**유지 관리** > **소프트웨어 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-160">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![장치 업데이트](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="cd240-162">**업데이트 파일 경로**, hello 업데이트에 대 한 hello 파일 이름을 입력 또는 핫픽스를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-162">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="cd240-163">네트워크 공유에 배치 하는 경우에 toohello 업데이트 또는 핫픽스 설치 파일을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-163">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="cd240-164">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-164">Click **Apply**.</span></span>
   
    ![장치 업데이트](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="cd240-166">경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-166">A warning is displayed.</span></span> <span data-ttu-id="cd240-167">이 지정 된 단일 노드 장치, hello 업데이트를 적용 하 고 hello 장치가 다시 시작 될 동안 가동 중지 후입니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-167">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="cd240-168">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-168">Click hello check icon.</span></span>
   
   ![장치 업데이트](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="cd240-170">hello 업데이트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-170">hello update starts.</span></span> <span data-ttu-id="cd240-171">Hello 장치를 업데이트 한 후 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-171">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="cd240-172">hello 로컬 UI 액세스할 수 없는 경우이 기간 동안</span><span class="sxs-lookup"><span data-stu-id="cd240-172">hello local UI is not accessible in this duration.</span></span>
   
    ![장치 업데이트](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="cd240-174">Toohello 취해집니다 hello를 다시 시작이 완료 된 후 **로그인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="cd240-174">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="cd240-175">hello 장치 소프트웨어 hello 로컬 웹 UI에서에서 업데이트 된 tooverify 너무 이동**유지 관리** > **소프트웨어 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-175">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="cd240-176">표시 되는 hello 소프트웨어 버전 이어야 합니다 **10.0.0.0.0.10290.0** 0.5 업데이트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-176">hello displayed software version should be **10.0.0.0.0.10290.0** for Update 0.5.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cd240-177">Hello 로컬 웹 UI에서에서 약간 다른 방식으로 hello 소프트웨어 버전을 보고 하 고 hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-177">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="cd240-178">예를 들어 로컬 웹 UI 보고서 hello **10.0.0.0.0.10290** Azure 포털 보고서 hello 및 **10.0.10290.0** hello에 대 한 동일한 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-178">For example, hello local web UI reports **10.0.0.0.0.10290** and hello Azure portal reports **10.0.10290.0** for hello same version.</span></span>
   
    ![장치 업데이트](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. <span data-ttu-id="cd240-180">hello 다음 단계는 tooupdate hello MDS 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-180">hello next step is tooupdate hello MDS agent.</span></span> <span data-ttu-id="cd240-181">Hello에 **소프트웨어 업데이트** 페이지에서 이동 toohello **업데이트 파일 경로** toohello 찾아보기 및 `GenevaMonitoringAgentPackageInstaller.msi` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-181">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="cd240-182">2-4단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-182">Repeat steps 2-4.</span></span> <span data-ttu-id="cd240-183">Hello 가상 배열 다시 시작 되 면 hello 로컬 웹 UI에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-183">After hello virtual array restarts, sign into hello local web UI.</span></span>

<span data-ttu-id="cd240-184">hello 업데이트가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-184">hello update is now complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd240-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cd240-185">Next steps</span></span>

<span data-ttu-id="cd240-186">[StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cd240-186">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

