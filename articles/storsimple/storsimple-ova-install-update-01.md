---
title: "StorSimple 가상 배열에 업데이트 설치 | Microsoft Docs"
description: "StorSimple 가상 배열 웹 UI를 사용하여 포털 및 핫픽스 방법을 사용하는 업데이트를 적용하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: bccb0d49c1959a690d513961c32d946763385a87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="2d343-103">StorSimple 가상 배열에 업데이트 설치</span><span class="sxs-lookup"><span data-stu-id="2d343-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="2d343-104">개요</span><span class="sxs-lookup"><span data-stu-id="2d343-104">Overview</span></span>
<span data-ttu-id="2d343-105">이 문서에서는 로컬 웹 UI 및 Azure 클래식 포털을 사용하여 StorSimple 가상 배열에 업데이트를 설치하는 데 필요한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure classic portal.</span></span> <span data-ttu-id="2d343-106">StorSimple 가상 배열을 최신 상태로 유지하려면 소프트웨어 업데이트 또는 핫픽스를 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="2d343-107">업데이트 또는 핫픽스를 설치하면 장치가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="2d343-108">StorSimple 가상 배열이 단일 노드 장치인 경우 진행 중인 모든 IO가 중단되고 장치에 가동 중지 시간이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="2d343-109">업데이트를 적용하기 전에 호스트에서 볼륨 또는 공유를 오프라인으로 전환한 후 장치를 오프라인으로 전환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="2d343-110">이렇게 하면 데이터 손상 가능성이 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d343-111">업데이트 0.1 또는 GA 소프트웨어 버전을 실행 중인 경우 로컬 웹 UI를 통해 핫픽스 메서드를 사용하여 업데이트 0.3을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="2d343-112">업데이트 0.2를 실행 중인 경우 Azure 클래식 포털을 통해 업데이트를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span></span>
> 
> 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="2d343-113">로컬 웹 UI 사용</span><span class="sxs-lookup"><span data-stu-id="2d343-113">Use the local web UI</span></span>
<span data-ttu-id="2d343-114">로컬 웹 UI를 사용하는 경우 다음 두 단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="2d343-115">업데이트 또는 핫픽스 다운로드</span><span class="sxs-lookup"><span data-stu-id="2d343-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="2d343-116">업데이트 또는 핫픽스 설치</span><span class="sxs-lookup"><span data-stu-id="2d343-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="2d343-117">업데이트 또는 핫픽스 다운로드</span><span class="sxs-lookup"><span data-stu-id="2d343-117">Download the update or the hotfix</span></span>
<span data-ttu-id="2d343-118">Microsoft 업데이트 카탈로그에서 소프트웨어 업데이트를 다운로드하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="2d343-119">업데이트 또는 핫픽스를 다운로드하려면</span><span class="sxs-lookup"><span data-stu-id="2d343-119">To download the update or the hotfix</span></span>
1. <span data-ttu-id="2d343-120">Internet Explorer를 시작하고 [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="2d343-121">이 컴퓨터에서 Microsoft 업데이트 카탈로그를 처음 사용하는 경우 Microsoft 업데이트 카탈로그 추가 기능을 설치하라는 메시지가 나타나면 **설치** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="2d343-122">Microsoft 업데이트 카탈로그의 검색 상자에 다운로드하려는 핫픽스의 KB(기술 자료) 번호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="2d343-123">업데이트 0.3의 경우 **3182061**을 입력하고 **검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="2d343-124">핫픽스 목록(예: **StorSimple 가상 배열 업데이트 0.3**)이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![카탈로그 검색](./media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="2d343-126">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-126">Click **Add**.</span></span> <span data-ttu-id="2d343-127">업데이트는 장바구니에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-127">The update is added to the basket.</span></span>
5. <span data-ttu-id="2d343-128">**바구니 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="2d343-129">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-129">Click **Download**.</span></span> <span data-ttu-id="2d343-130">다운로드를 표시할 로컬 위치를 지정하거나 **검색** 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="2d343-131">업데이트를 지정된 위치에 다운로드하고 업데이트와 같은 이름의 하위 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="2d343-132">장치에서 연결할 수 있는 네트워크 공유에 폴더도 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-132">The folder can also be copied to a network share that is reachable from the device.</span></span>
7. <span data-ttu-id="2d343-133">복사된 폴더를 열면 Microsoft 업데이트 독립 실행형 패키지 파일 `WindowsTH-KB3011067-x64`가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="2d343-134">이 파일은 업데이트 또는 핫픽스를 설치하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="2d343-135">업데이트 또는 핫픽스 설치</span><span class="sxs-lookup"><span data-stu-id="2d343-135">Install the update or the hotfix</span></span>
<span data-ttu-id="2d343-136">업데이트 또는 핫픽스를 설치하기 전에, 업데이트 또는 핫픽스를 호스트의 로컬에 다운로드하거나 네트워크 공유를 통해 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="2d343-137">GA 또는 업데이트 0.1 소프트웨어 버전을 실행하는 장치에 업데이트를 설치하려면 이 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="2d343-138">이 절차를 완료하는 데 2분 미만이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="2d343-139">다음 단계를 수행하여 업데이트 또는 핫픽스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="2d343-140">업데이트 또는 핫픽스를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="2d343-140">To install the update or the hotfix</span></span>
1. <span data-ttu-id="2d343-141">로컬 웹 UI에서 **유지 관리** > **소프트웨어 업데이트**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![장치 업데이트](./media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="2d343-143">**업데이트 파일 경로**에 업데이트 또는 핫픽스의 파일 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="2d343-144">네트워크 공유에 있는 경우 업데이트 또는 핫픽스 설치 파일로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="2d343-145">**적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-145">Click **Apply**.</span></span>
   
    ![장치 업데이트](./media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="2d343-147">경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-147">A warning is displayed.</span></span> <span data-ttu-id="2d343-148">단일 노드 장치인 경우 업데이트가 적용된 후 장치를 다시 시작하고 가동 중지 시간이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="2d343-149">확인 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-149">Click the check icon.</span></span>
   
   ![장치 업데이트](./media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="2d343-151">업데이트가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-151">The update starts.</span></span> <span data-ttu-id="2d343-152">장치가 성공적으로 업데이트된 후 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="2d343-153">이 시간 동안 로컬 UI에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-153">The local UI is not accessible in this duration.</span></span>
   
    ![장치 업데이트](./media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="2d343-155">다시 시작이 완료된 후 **로그인** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="2d343-156">로컬 웹 UI에서 장치 소프트웨어가 업데이트되었는지 확인하려면 **유지 관리** > **소프트웨어 업데이트**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="2d343-157">표시된 소프트웨어 버전은 업데이트 0.3의 경우 **10.0.0.0.0.10288.0** 입니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2d343-158">로컬 웹 UI 및 Azure 클래식 포털에서 약간 다른 방법으로 소프트웨어 버전을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-158">We report the software versions in a slightly different way in the local web UI and the Azure classic portal.</span></span> <span data-ttu-id="2d343-159">예를 들어 같은 버전에 대해 로컬 웹 UI는 **10.0.0.0.0.10288**, Azure 클래식 포털은 **10.0.10288.0**을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure classic portal reports **10.0.10288.0** for the same version.</span></span> 
   > 
   > 
   
    ![장치 업데이트](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="2d343-161">Azure 클래식 포털 사용</span><span class="sxs-lookup"><span data-stu-id="2d343-161">Use the Azure classic portal</span></span>
<span data-ttu-id="2d343-162">업데이트 0.2를 실행하는 경우 Azure 클래식 포털을 통해 업데이트를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-162">If running Update 0.2, we recommend that you install updates through the Azure classic portal.</span></span> <span data-ttu-id="2d343-163">포털 절차를 사용하려면 사용자가 업데이트를 스캔, 다운로드한 다음 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="2d343-164">이 절차를 완료하는 데 약 7분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="2d343-165">다음 단계를 수행하여 업데이트 또는 핫픽스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="2d343-166">설치가 완료된 후(작업 상태 100%로 표시) **장치 > 유지 관리 > 소프트웨어 업데이트**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-166">After the installation is complete (as indicated by job status at 100 %), go to **Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="2d343-167">표시된 소프트웨어 버전은 10.0.10288.0이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-167">The displayed software version should be 10.0.10288.0.</span></span>

![장치 업데이트](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="2d343-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d343-169">Next steps</span></span>
<span data-ttu-id="2d343-170">[StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2d343-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

