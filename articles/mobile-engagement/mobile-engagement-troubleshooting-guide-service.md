---
title: "aaaAzure Mobile Engagement 문제 해결 가이드-서비스"
description: "Azure Mobile Engagement에 대한 문제 해결 가이드"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="b0468-103">서비스 문제에 대한 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="b0468-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="b0468-104">hello 다음은 Azure Mobile Engagement 실행 하는 방법에 발생할 수 있는 관련 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-104">hello following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="b0468-105">서비스 중단</span><span class="sxs-lookup"><span data-stu-id="b0468-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="b0468-106">문제</span><span class="sxs-lookup"><span data-stu-id="b0468-106">Issue</span></span>
* <span data-ttu-id="b0468-107">Azure Mobile Engagement 서비스 중단 때문일 toobe 나타나는 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-107">Issues that appear toobe caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="b0468-108">원인</span><span class="sxs-lookup"><span data-stu-id="b0468-108">Causes</span></span>
* <span data-ttu-id="b0468-109">Azure Mobile Engagement 서비스 중단 때문일 toobe 표시 하는 문제는 여러 다른 문제로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-109">Issues that appear toobe caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="b0468-110">원래 Azure Mobile Engagement의 구조적 tooall를 표시 하는 격리 된 문제</span><span class="sxs-lookup"><span data-stu-id="b0468-110">Isolated issues that originally appear systemic tooall of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="b0468-111">서버 중단으로 인한 알려진 문제(서버 상태에 항상 표시되지는 않음):</span><span class="sxs-lookup"><span data-stu-id="b0468-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="b0468-112">지연, 대상 지정 오류, 배지 업데이트 문제, 수집, 푸시 작동을 중지 하는 통계 중지 예약, API의 작동을 중지, 새로운 앱 또는 사용자가 만들 수 없습니다, DNS 오류 및 시간 초과 오류 장치에서 hello UI, API 또는 앱에서.</span><span class="sxs-lookup"><span data-stu-id="b0468-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in hello UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="b0468-113">클라우드 종속성 작동 중단 [Azure 서비스 상태](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="b0468-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="b0468-114">PNS(푸시 알림 서비스) 종속성 작동 중단</span><span class="sxs-lookup"><span data-stu-id="b0468-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="b0468-115">앱 스토어 작동 중단</span><span class="sxs-lookup"><span data-stu-id="b0468-115">App Store Outages</span></span>

1) <span data-ttu-id="b0468-116">구조적 hello 문제가 발생 한 경우 tootest toosee hello 동일한 다른 함수를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-116">tootest toosee if hello problem is systemic you can test hello same function from a different</span></span>

* <span data-ttu-id="b0468-117">Azure Mobile Engagement 통합 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="b0468-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="b0468-118">테스트 장치</span><span class="sxs-lookup"><span data-stu-id="b0468-118">Test device</span></span>
* <span data-ttu-id="b0468-119">테스트 장치 OS 버전</span><span class="sxs-lookup"><span data-stu-id="b0468-119">Test device OS version</span></span>
* <span data-ttu-id="b0468-120">캠페인</span><span class="sxs-lookup"><span data-stu-id="b0468-120">Campaign</span></span>
* <span data-ttu-id="b0468-121">관리자 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="b0468-121">Administrator user account</span></span>
* <span data-ttu-id="b0468-122">브라우저(IE, Firefox, Chrome 등)</span><span class="sxs-lookup"><span data-stu-id="b0468-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="b0468-123">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="b0468-123">Computer</span></span>

2) <span data-ttu-id="b0468-124">tootest hello 문제만 영향을 주는 hello UI 또는 hello API의 경우:</span><span class="sxs-lookup"><span data-stu-id="b0468-124">tootest if hello problem only affects hello UI or hello API's:</span></span>

* <span data-ttu-id="b0468-125">동일 두 hello Azure Mobile Engagement UI에서에서 작동 하 고 Azure Mobile Engagement API hello hello를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-125">Test hello same function from both hello Azure Mobile Engagement UI and hello Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="b0468-126">tootest 휴대폰 네트워크와 hello 문제가 발생 한 경우:</span><span class="sxs-lookup"><span data-stu-id="b0468-126">tootest if hello problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="b0468-127">연결 된 toohello 휴대폰 3g 네트워크를 통해 연결 되어 있는 동안 및 WIFI를 통해 인터넷 하는 동안 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-127">Test while connected toohello Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="b0468-128">방화벽에서 차단 하지 않는지 hello Azure Mobile Engagement IP 주소 또는 포트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-128">Confirm that your firewall is not blocking any of hello Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="b0468-129">tootest 장치와 함께 hello 문제가 발생 한 경우:</span><span class="sxs-lookup"><span data-stu-id="b0468-129">tootest if hello problem is with your Device:</span></span>

* <span data-ttu-id="b0468-130">장치는 다른 Azure Mobile Engagement 통합 앱 수 tooconnect tooAzure Mobile Engagement를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-130">Test if your Device is able tooconnect tooAzure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="b0468-131">Hello Azure Mobile Engagement UI에서에서 볼 수 있는 휴대폰에서 이벤트, 작업, 및 작동 중단을 생성할 수 있는 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in hello Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="b0468-132">Id입니다. 해당 장치에 따라 hello Azure Mobile Engagement UI tooyour 장치에서 푸시 알림을 보낼 수 있는 경우에 테스트</span><span class="sxs-lookup"><span data-stu-id="b0468-132">Test if you can send push notifications from hello Azure Mobile Engagement UI tooyour device based on its Device ID.</span></span> 

5) <span data-ttu-id="b0468-133">tootest 응용 프로그램과 함께 hello 문제가 발생 한 경우:</span><span class="sxs-lookup"><span data-stu-id="b0468-133">tootest if hello problem is with your App:</span></span>

* <span data-ttu-id="b0468-134">실제 장치 대신 에뮬레이터에서 응용 프로그램을 설치하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="b0468-135">os hello 문제가 발생 한 경우 tootest tooend 사용자 SDK 업그레이드 tooresolve 해야 하는 장치를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-135">tootest if hello problem is with OS upgrades tooend user Devices, which require an SDK upgrade tooresolve:</span></span>

* <span data-ttu-id="b0468-136">다른 버전의 운영 체제 hello와 서로 다른 장치에서 응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-136">Test your application on different devices with different versions of hello OS.</span></span>
* <span data-ttu-id="b0468-137">Hello hello SDK의 최신 버전을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-137">Confirm that you are using hello most recent version of hello SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="b0468-138">연결 및 잘못된 정보 문제</span><span class="sxs-lookup"><span data-stu-id="b0468-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="b0468-139">문제</span><span class="sxs-lookup"><span data-stu-id="b0468-139">Issue</span></span>
* <span data-ttu-id="b0468-140">Azure Mobile Engagement UI hello 하는 문제에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-140">Problems logging into hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="b0468-141">Hello로 Azure Mobile Engagement API의 연결 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-141">Connection errors with hello Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="b0468-142">Hello Device API를 통해 응용 프로그램 정보 태그를 업로드 하는 중에 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-142">Problems uploading App Info Tags via hello Device API.</span></span>
* <span data-ttu-id="b0468-143">Azure Mobile Engagement에서 로그나 내보낸 데이터를 다운로드하는 데 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="b0468-144">Hello Azure Mobile Engagement UI에에서 표시 된 잘못 된 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-144">Incorrect information shown in hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="b0468-145">Azure Mobile Engagement 로그에 잘못된 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="b0468-146">원인</span><span class="sxs-lookup"><span data-stu-id="b0468-146">Causes</span></span>
* <span data-ttu-id="b0468-147">사용자 계정에 충분 한 사용 권한을 tooperform hello 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-147">Confirm your user account has sufficient permissions tooperform hello task.</span></span>
* <span data-ttu-id="b0468-148">Hello 이러한 문제는 격리 된 tooone 컴퓨터 또는 로컬 네트워크를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-148">Confirm that hello problem is not isolated tooone computer or your local network.</span></span>
* <span data-ttu-id="b0468-149">해당 hello Azure Mobile Engagement 서비스에 보고 된 중단 없는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-149">Confirm that that hello Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="b0468-150">앱 정보 태그 파일이 다음 규칙을 모두 따르는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="b0468-151">사용에만 UTF8 문자 세트 hello (hello ANSI 문자 집합이 지원 되지 않음).</span><span class="sxs-lookup"><span data-stu-id="b0468-151">Use only hello UTF8 character set (hello ANSI character set is not supported).</span></span>
  * <span data-ttu-id="b0468-152">쉼표를 사용 하 여 "," hello 구분 기호 문자로 (쉼표에서 서비스 요청 toorequest toochange hello.csv 구분 문자를 열 수 세미콜론 같은 tooanother 문자 "," ";").</span><span class="sxs-lookup"><span data-stu-id="b0468-152">Use a comma "," as hello separator character (you can open a service request toorequest toochange hello .csv separator character from a comma "," tooanother character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="b0468-153">부울 값 "true"와 "false"에 소문자만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="b0468-154">35MB의 hello 최대 파일 크기 보다 작은 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0468-154">Use a file that is smaller than hello maximum file size of 35MB.</span></span>

