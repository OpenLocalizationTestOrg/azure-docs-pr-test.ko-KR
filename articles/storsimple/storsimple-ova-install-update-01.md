---
title: "StorSimple 가상 배열에서 aaaInstall 업데이트 | Microsoft Docs"
description: "Hello 포털 및 핫픽스 메서드를 사용 하 여 toouse hello StorSimple 가상 배열 웹 UI tooapply을 업데이트 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="67957-103">StorSimple 가상 배열에 업데이트 설치</span><span class="sxs-lookup"><span data-stu-id="67957-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="67957-104">개요</span><span class="sxs-lookup"><span data-stu-id="67957-104">Overview</span></span>
<span data-ttu-id="67957-105">이 문서에서는 hello 로컬 웹 UI 통해 및 hello Azure 클래식 포털을 통해 StorSimple 가상 배열에 hello 단계 필요한 tooinstall 업데이트를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-105">This article describes hello steps required tooinstall updates on your StorSimple Virtual Array via hello local web UI and via hello Azure classic portal.</span></span> <span data-ttu-id="67957-106">필요한 소프트웨어 업데이트 또는 핫픽스 tookeep tooapply StorSimple 가상 배열 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="67957-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="67957-107">업데이트 또는 핫픽스를 설치하면 장치가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="67957-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="67957-108">주어진는 hello StorSimple 가상 배열은 단일 노드에 장치, 진행 중인 모든 I/O 중단 된와 장치에 가동 중지 시간이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="67957-109">업데이트를 적용 하기 전에 수행한 hello 볼륨 또는 공유 hello에 오프 라인에서 먼저 호스트 및 다음 장치를 hello 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="67957-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="67957-110">이렇게 하면 데이터 손상 가능성이 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="67957-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67957-111">업데이트 0.1 또는 GA 소프트웨어 버전을 실행 하는 경우에 hello 로컬 웹 UI tooinstall 업데이트 0.3 통해 hello 핫픽스 메서드를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="67957-112">0.2 업데이트를 실행 하는 경우에 hello Azure 클래식 포털을 통해 hello 업데이트를 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="67957-112">If you are running Update 0.2, we recommend that you install hello updates via hello Azure classic portal.</span></span>
> 
> 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="67957-113">Hello 로컬 웹 UI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="67957-113">Use hello local web UI</span></span>
<span data-ttu-id="67957-114">Hello 로컬 웹 UI를 사용 하는 데는 두 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67957-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="67957-115">Hello 업데이트 또는 hello 핫픽스를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="67957-116">Hello 업데이트 또는 hello 핫픽스 설치</span><span class="sxs-lookup"><span data-stu-id="67957-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="67957-117">Hello 업데이트 또는 hello 핫픽스를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-117">Download hello update or hello hotfix</span></span>
<span data-ttu-id="67957-118">Hello hello Microsoft Update 카탈로그에서에서 단계 toodownload hello 소프트웨어 업데이트를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="67957-119">toodownload hello 업데이트나 hello 핫픽스</span><span class="sxs-lookup"><span data-stu-id="67957-119">toodownload hello update or hello hotfix</span></span>
1. <span data-ttu-id="67957-120">Internet Explorer를 시작 하 고 탐색 너무[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="67957-121">Microsoft Update 카탈로그 hello를 사용 하 여이 컴퓨터에 처음으로 이면 클릭 **설치** 때 메시지 표시 tooinstall hello Microsoft Update 카탈로그 추가 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="67957-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="67957-122">Hello 기술 자료 (KB) 번호를 입력 hello Microsoft Update 카탈로그의 hello 검색 상자에 원하는 toodownload hello 핫픽스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="67957-123">업데이트 0.3의 경우 **3182061**을 입력하고 **검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="67957-124">hello 핫픽스 목록이 표시 되 면 예를 들어 **StorSimple 가상 배열 업데이트 0.3**합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![카탈로그 검색](./media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="67957-126">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-126">Click **Add**.</span></span> <span data-ttu-id="67957-127">hello 업데이트 toohello 바구니를 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67957-127">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="67957-128">**바구니 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="67957-129">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-129">Click **Download**.</span></span> <span data-ttu-id="67957-130">지정 하거나 **찾아보기** tooa 로컬 위치 hello tooappear 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="67957-131">hello 업데이트는 다운로드 toohello 위치를 지정 하 고 hello 업데이트로 이름과 같은 이름을 hello로 하위 폴더에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="67957-132">hello 폴더 hello 장치에서 연결할 수 있는 tooa 복사한 네트워크 공유 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67957-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
7. <span data-ttu-id="67957-133">폴더를 복사 하는 hello open, Microsoft Update 독립 실행형 패키지 파일이 `WindowsTH-KB3011067-x64`합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="67957-134">이 파일이 사용 되는 tooinstall hello 업데이트나 핫픽스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="67957-135">Hello 업데이트 또는 hello 핫픽스 설치</span><span class="sxs-lookup"><span data-stu-id="67957-135">Install hello update or hello hotfix</span></span>
<span data-ttu-id="67957-136">이전 toohello 업데이트 또는 핫픽스 설치 hello 업데이트가 설치 되어 있거나 호스트에서 로컬로 hello 핫픽스 다운로드 하 고 있는지 또는 네트워크 공유를 통해 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="67957-137">GA를 실행 하는 장치에이 메서드가 tooinstall 업데이트를 사용 하거나 0.1 소프트웨어 버전으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="67957-138">이 프로시저는 2 분 toocomplete 보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="67957-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="67957-139">Hello 다음이 수행 단계 tooinstall hello 업데이트나 핫픽스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="67957-140">tooinstall hello 업데이트나 hello 핫픽스</span><span class="sxs-lookup"><span data-stu-id="67957-140">tooinstall hello update or hello hotfix</span></span>
1. <span data-ttu-id="67957-141">Hello 로컬 웹 UI에서에서 이동 너무**유지 관리** > **소프트웨어 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![장치 업데이트](./media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="67957-143">**업데이트 파일 경로**, hello 업데이트에 대 한 hello 파일 이름을 입력 또는 핫픽스를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="67957-144">네트워크 공유에 배치 하는 경우에 toohello 업데이트 또는 핫픽스 설치 파일을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67957-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="67957-145">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-145">Click **Apply**.</span></span>
   
    ![장치 업데이트](./media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="67957-147">경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67957-147">A warning is displayed.</span></span> <span data-ttu-id="67957-148">이 지정 된 단일 노드 장치, hello 업데이트를 적용 하 고 hello 장치가 다시 시작 될 동안 가동 중지 후입니다.</span><span class="sxs-lookup"><span data-stu-id="67957-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="67957-149">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-149">Click hello check icon.</span></span>
   
   ![장치 업데이트](./media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="67957-151">hello 업데이트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-151">hello update starts.</span></span> <span data-ttu-id="67957-152">Hello 장치를 업데이트 한 후 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67957-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="67957-153">hello 로컬 UI 액세스할 수 없는 경우이 기간 동안</span><span class="sxs-lookup"><span data-stu-id="67957-153">hello local UI is not accessible in this duration.</span></span>
   
    ![장치 업데이트](./media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="67957-155">Toohello 취해집니다 hello를 다시 시작이 완료 된 후 **로그인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="67957-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="67957-156">hello 장치 소프트웨어 hello 로컬 웹 UI에서에서 업데이트 된 tooverify 너무 이동**유지 관리** > **소프트웨어 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="67957-157">표시 되는 hello 소프트웨어 버전 이어야 합니다 **10.0.0.0.0.10288.0** 업데이트 0.3에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-157">hello displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="67957-158">Hello 로컬 웹 UI에서에서 약간 다른 방식으로 hello 소프트웨어 버전을 보고 하 고 hello Azure 클래식 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="67957-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure classic portal.</span></span> <span data-ttu-id="67957-159">예를 들어 로컬 웹 UI 보고서 hello **10.0.0.0.0.10288** Azure 클래식 포털 보고서 hello 및 **10.0.10288.0** hello에 대 한 동일한 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="67957-159">For example, hello local web UI reports **10.0.0.0.0.10288** and hello Azure classic portal reports **10.0.10288.0** for hello same version.</span></span> 
   > 
   > 
   
    ![장치 업데이트](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="67957-161">Hello Azure 클래식 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="67957-161">Use hello Azure classic portal</span></span>
<span data-ttu-id="67957-162">0.2 업데이트를 실행 하는 경우에 hello Azure 클래식 포털을 통해 업데이트를 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="67957-162">If running Update 0.2, we recommend that you install updates through hello Azure classic portal.</span></span> <span data-ttu-id="67957-163">hello 포털 프로시저 hello 사용자 tooscan 필요 하 고, 다운로드 및 다음 hello 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="67957-164">이 프로시저는 약 7 분 toocomplete.</span><span class="sxs-lookup"><span data-stu-id="67957-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="67957-165">Hello 다음이 수행 단계 tooinstall hello 업데이트나 핫픽스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="67957-166">설치 후 hello (작업 상태 100%로 표시 됨) 처럼 완료 되 면 너무 이동**장치 > 유지 관리 > 소프트웨어 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-166">After hello installation is complete (as indicated by job status at 100 %), go too**Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="67957-167">표시 되는 hello 소프트웨어 버전 10.0.10288.0 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67957-167">hello displayed software version should be 10.0.10288.0.</span></span>

![장치 업데이트](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="67957-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="67957-169">Next steps</span></span>
<span data-ttu-id="67957-170">[StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="67957-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

