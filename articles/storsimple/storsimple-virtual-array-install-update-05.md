---
title: "StorSimple 가상 배열에 업데이트 0.5 설치 | Microsoft Docs"
description: "StorSimple 가상 배열 웹 UI를 사용하여 Azure Portal 및 핫픽스 방법을 사용하는 업데이트를 적용하는 방법을 설명합니다."
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
ms.openlocfilehash: c47da5b90c16e2d5b5709e2a6affc026238b9468
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a><span data-ttu-id="72fce-103">StorSimple 가상 배열에 업데이트 0.5 설치</span><span class="sxs-lookup"><span data-stu-id="72fce-103">Install Update 0.5 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="72fce-104">개요</span><span class="sxs-lookup"><span data-stu-id="72fce-104">Overview</span></span>

<span data-ttu-id="72fce-105">이 문서에서는 로컬 웹 UI 및 Azure Portal을 사용하여 StorSimple 가상 배열에 업데이트 0.5를 설치하는 데 필요한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-105">This article describes the steps required to install Update 0.5 on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="72fce-106">StorSimple 가상 배열을 최신 상태로 유지하려면 소프트웨어 업데이트 또는 핫픽스를 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="72fce-107">업데이트를 적용하기 전에 호스트에서 볼륨 또는 공유를 오프라인으로 전환한 후 장치를 오프라인으로 전환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-107">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="72fce-108">이렇게 하면 데이터 손상 가능성이 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="72fce-109">볼륨 또는 공유가 오프라인 상태가 되면 장치의 수동 백업도 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-109">After the volumes or shares are offline, you should also take a manual backup of the device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="72fce-110">업데이트 0.5는 장치에 있는 소프트웨어 버전 **10.0.10290.0**에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-110">Update 0.5 corresponds to **10.0.10290.0** software version on your device.</span></span> <span data-ttu-id="72fce-111">이 업데이트의 새로운 기능에 대한 자세한 내용은 [업데이트 0.5에 대한 릴리스 정보](storsimple-virtual-array-update-05-release-notes.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-111">For information on what is new in this update, go to [Release notes for Update 0.5](storsimple-virtual-array-update-05-release-notes.md).</span></span>
>
> - <span data-ttu-id="72fce-112">업데이트 0.2 이상을 실행 중인 경우 Azure Portal을 통해 업데이트를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-112">If you are running Update 0.2 or later, we recommend that you install the updates via the Azure portal.</span></span> <span data-ttu-id="72fce-113">업데이트 0.1 또는 GA 소프트웨어 버전을 실행 중인 경우 로컬 웹 UI를 통해 핫픽스 메서드를 사용하여 업데이트 0.5를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-113">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install Update 0.5.</span></span>
>
> - <span data-ttu-id="72fce-114">업데이트 또는 핫픽스를 설치하면 장치가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="72fce-115">StorSimple 가상 배열이 단일 노드 장치인 경우 진행 중인 모든 IO가 중단되고 장치에 가동 중지 시간이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-115">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="72fce-116">Azure 포털 사용</span><span class="sxs-lookup"><span data-stu-id="72fce-116">Use the Azure portal</span></span>

<span data-ttu-id="72fce-117">업데이트 0.2 이상을 실행하는 경우 Azure Portal을 통해 업데이트를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-117">If running Update 0.2 and later, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="72fce-118">포털 절차를 사용하려면 사용자가 업데이트를 스캔, 다운로드한 다음 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-118">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="72fce-119">이 절차를 완료하는 데 약 7분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-119">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="72fce-120">다음 단계를 수행하여 업데이트 또는 핫픽스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-120">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="72fce-121">설치가 완료된 후 StorSimple 장치 관리자 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-121">After the installation is complete, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="72fce-122">**장치**를 선택한 후 방금 업데이트한 장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-122">Select **Devices** and then select and click the device you just updated.</span></span> <span data-ttu-id="72fce-123">**설정 > 관리 > 장치 업데이트**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-123">Go to **Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="72fce-124">표시된 소프트웨어 버전은 **10.0.10290.0**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-124">The displayed software version should be **10.0.10290.0**.</span></span>

## <a name="use-the-local-web-ui"></a><span data-ttu-id="72fce-125">로컬 웹 UI 사용</span><span class="sxs-lookup"><span data-stu-id="72fce-125">Use the local web UI</span></span>

<span data-ttu-id="72fce-126">로컬 웹 UI를 사용하는 경우 다음 두 단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-126">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="72fce-127">업데이트 또는 핫픽스 다운로드</span><span class="sxs-lookup"><span data-stu-id="72fce-127">Download the update or the hotfix</span></span>
* <span data-ttu-id="72fce-128">업데이트 또는 핫픽스 설치</span><span class="sxs-lookup"><span data-stu-id="72fce-128">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="72fce-129">업데이트 또는 핫픽스 다운로드</span><span class="sxs-lookup"><span data-stu-id="72fce-129">Download the update or the hotfix</span></span>

<span data-ttu-id="72fce-130">Microsoft 업데이트 카탈로그에서 소프트웨어 업데이트를 다운로드하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-130">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="72fce-131">업데이트 또는 핫픽스를 다운로드하려면</span><span class="sxs-lookup"><span data-stu-id="72fce-131">To download the update or the hotfix</span></span>

1. <span data-ttu-id="72fce-132">Internet Explorer를 시작하고 [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-132">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="72fce-133">이 컴퓨터에서 Microsoft 업데이트 카탈로그를 처음 사용하는 경우 Microsoft 업데이트 카탈로그 추가 기능을 설치하라는 메시지가 나타나면 **설치** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-133">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="72fce-134">Microsoft 업데이트 카탈로그의 검색 상자에 다운로드하려는 핫픽스의 KB(기술 자료) 번호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-134">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="72fce-135">업데이트 0.5의 경우 **4021576**을 입력하고 **검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-135">Enter **4021576** for Update 0.5, and then click **Search**.</span></span>
   
    <span data-ttu-id="72fce-136">핫픽스 목록(예: **StorSimple 가상 배열 업데이트 0.5**)이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-136">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.5**.</span></span>
   
    ![카탈로그 검색](./media/storsimple-virtual-array-install-update-05/download1.png)

4. <span data-ttu-id="72fce-138">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-138">Click **Download**.</span></span> 

5. <span data-ttu-id="72fce-139">다운로드할 수 있는 2개의 파일 *.msu* 및 *.cab*가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-139">You should see two files to download, a *.msu* and a *.cab* file.</span></span> <span data-ttu-id="72fce-140">이러한 각 파일을 폴더에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-140">Download each of those files to a folder.</span></span> <span data-ttu-id="72fce-141">장치에서 연결할 수 있는 네트워크 공유에 폴더도 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-141">The folder can also be copied to a network share that is reachable from the device.</span></span>

6. <span data-ttu-id="72fce-142">파일이 있는 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-142">Open the folder where the files are located.</span></span>
    <span data-ttu-id="72fce-143">![패키지의 파일](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span><span class="sxs-lookup"><span data-stu-id="72fce-143">![Files in the package](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span></span>

    <span data-ttu-id="72fce-144">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-144">You see:</span></span>
    -  <span data-ttu-id="72fce-145">Microsoft 업데이트 독립 실행형 패키지 파일 `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="72fce-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="72fce-146">이 파일은 장치 소프트웨어를 업데이트하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-146">This file is used to update the device software.</span></span>
    - <span data-ttu-id="72fce-147">Geneva 모니터링 에이전트 패키지 파일 `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="72fce-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="72fce-148">이 파일은 MDS(모니터링 및 진단 서비스) 에이전트를 업데이트하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-148">This file is used to update the Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="72fce-149">cab 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-149">Double-click the cab file.</span></span> <span data-ttu-id="72fce-150">.msi가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-150">A .msi is displayed.</span></span> <span data-ttu-id="72fce-151">파일을 선택하고 마우스 오른쪽 단추로 클릭한 다음 파일 **압축을 풉니다**.</span><span class="sxs-lookup"><span data-stu-id="72fce-151">Select the file, right-click, and then **Extract** the file.</span></span> <span data-ttu-id="72fce-152">_.msi_ 파일을 사용하여 에이전트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-152">You will use the _.msi_ file to update the agent.</span></span>

        ![MDS 에이전트 업데이트 파일 압축 풀기](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="72fce-154">업데이트 또는 핫픽스 설치</span><span class="sxs-lookup"><span data-stu-id="72fce-154">Install the update or the hotfix</span></span>

<span data-ttu-id="72fce-155">업데이트 또는 핫픽스를 설치하기 전에, 업데이트 또는 핫픽스를 호스트의 로컬에 다운로드하거나 네트워크 공유를 통해 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-155">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="72fce-156">GA 또는 업데이트 0.1 소프트웨어 버전을 실행하는 장치에 업데이트를 설치하려면 이 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-156">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="72fce-157">이 절차를 완료하는 데 2분 미만이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-157">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="72fce-158">다음 단계를 수행하여 업데이트 또는 핫픽스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-158">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="72fce-159">업데이트 또는 핫픽스를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="72fce-159">To install the update or the hotfix</span></span>

1. <span data-ttu-id="72fce-160">로컬 웹 UI에서 **유지 관리** > **소프트웨어 업데이트**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-160">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![장치 업데이트](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="72fce-162">**업데이트 파일 경로**에 업데이트 또는 핫픽스의 파일 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-162">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="72fce-163">네트워크 공유에 있는 경우 업데이트 또는 핫픽스 설치 파일로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-163">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="72fce-164">**적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-164">Click **Apply**.</span></span>
   
    ![장치 업데이트](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="72fce-166">경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-166">A warning is displayed.</span></span> <span data-ttu-id="72fce-167">단일 노드 장치인 경우 업데이트가 적용된 후 장치를 다시 시작하고 가동 중지 시간이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-167">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="72fce-168">확인 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-168">Click the check icon.</span></span>
   
   ![장치 업데이트](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="72fce-170">업데이트가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-170">The update starts.</span></span> <span data-ttu-id="72fce-171">장치가 성공적으로 업데이트된 후 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-171">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="72fce-172">이 시간 동안 로컬 UI에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-172">The local UI is not accessible in this duration.</span></span>
   
    ![장치 업데이트](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="72fce-174">다시 시작이 완료된 후 **로그인** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-174">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="72fce-175">로컬 웹 UI에서 장치 소프트웨어가 업데이트되었는지 확인하려면 **유지 관리** > **소프트웨어 업데이트**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-175">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="72fce-176">표시된 소프트웨어 버전은 업데이트 0.5의 경우 **10.0.0.0.0.10290.0** 입니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-176">The displayed software version should be **10.0.0.0.0.10290.0** for Update 0.5.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="72fce-177">로컬 웹 UI 및 Azure Portal에서 약간 다른 방법으로 소프트웨어 버전을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-177">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="72fce-178">예를 들어 같은 버전에 대해 로컬 웹 UI는 **10.0.0.0.0.10290**, Azure Portal은 **10.0.10290.0**을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-178">For example, the local web UI reports **10.0.0.0.0.10290** and the Azure portal reports **10.0.10290.0** for the same version.</span></span>
   
    ![장치 업데이트](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. <span data-ttu-id="72fce-180">다음 단계는 MDS 에이전트를 업데이트하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-180">The next step is to update the MDS agent.</span></span> <span data-ttu-id="72fce-181">**소프트웨어 업데이트** 페이지에는 **업데이트 파일 경로**로 이동한 후 `GenevaMonitoringAgentPackageInstaller.msi` 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-181">In the **Software Update** page, go to the **Update file path** and browse to the `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="72fce-182">2-4단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-182">Repeat steps 2-4.</span></span> <span data-ttu-id="72fce-183">가상 배열이 다시 시작되면 로컬 웹 UI에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-183">After the virtual array restarts, sign into the local web UI.</span></span>

<span data-ttu-id="72fce-184">이제 업데이트가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-184">The update is now complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72fce-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="72fce-185">Next steps</span></span>

<span data-ttu-id="72fce-186">[StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="72fce-186">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

