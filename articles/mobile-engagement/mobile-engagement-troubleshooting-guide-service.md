---
title: "Azure Mobile Engagement 문제 해결 가이드 - 서비스"
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
ms.openlocfilehash: f13fd0540b783120014b3a8d4e41f78808c7fade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="6de58-103">서비스 문제에 대한 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="6de58-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="6de58-104">다음은 Azure Mobile Engagement 실행 방법과 관련해서 발생할 수 있는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-104">The following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="6de58-105">서비스 중단</span><span class="sxs-lookup"><span data-stu-id="6de58-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="6de58-106">문제</span><span class="sxs-lookup"><span data-stu-id="6de58-106">Issue</span></span>
* <span data-ttu-id="6de58-107">Azure Mobile Engagement 서비스 중단으로 인해 발생한 것처럼 보이는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-107">Issues that appear to be caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="6de58-108">원인</span><span class="sxs-lookup"><span data-stu-id="6de58-108">Causes</span></span>
* <span data-ttu-id="6de58-109">Azure Mobile Engagement 서비스 중단으로 인해 발생한 것으로 나타나는 문제에는 여러 가지 원인이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-109">Issues that appear to be caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="6de58-110">원래 모든 Azure Mobile Engagement에서 전체적으로 발생하는 것으로 확인된 문제</span><span class="sxs-lookup"><span data-stu-id="6de58-110">Isolated issues that originally appear systemic to all of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="6de58-111">서버 중단으로 인한 알려진 문제(서버 상태에 항상 표시되지는 않음):</span><span class="sxs-lookup"><span data-stu-id="6de58-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="6de58-112">예약 지연, 대상 지정 오류, 배지 업데이트 문제, 통계 수집 중지, 푸시 작동 중지, API 작동 중지, 새 앱이나 사용자 만들기 불가, DNS 오류, 장치의 UI/API/앱 시간 초과 오류</span><span class="sxs-lookup"><span data-stu-id="6de58-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in the UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="6de58-113">클라우드 종속성 작동 중단 [Azure 서비스 상태](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="6de58-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="6de58-114">PNS(푸시 알림 서비스) 종속성 작동 중단</span><span class="sxs-lookup"><span data-stu-id="6de58-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="6de58-115">앱 스토어 작동 중단</span><span class="sxs-lookup"><span data-stu-id="6de58-115">App Store Outages</span></span>

1) <span data-ttu-id="6de58-116">문제가 시스템 전체의 문제인지 테스트하려는 경우 다른 항목에서 같은 기능을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-116">To test to see if the problem is systemic you can test the same function from a different</span></span>

* <span data-ttu-id="6de58-117">Azure Mobile Engagement 통합 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="6de58-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="6de58-118">테스트 장치</span><span class="sxs-lookup"><span data-stu-id="6de58-118">Test device</span></span>
* <span data-ttu-id="6de58-119">테스트 장치 OS 버전</span><span class="sxs-lookup"><span data-stu-id="6de58-119">Test device OS version</span></span>
* <span data-ttu-id="6de58-120">캠페인</span><span class="sxs-lookup"><span data-stu-id="6de58-120">Campaign</span></span>
* <span data-ttu-id="6de58-121">관리자 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="6de58-121">Administrator user account</span></span>
* <span data-ttu-id="6de58-122">브라우저(IE, Firefox, Chrome 등)</span><span class="sxs-lookup"><span data-stu-id="6de58-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="6de58-123">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="6de58-123">Computer</span></span>

2) <span data-ttu-id="6de58-124">문제가 UI 또는 API에만 영향을 주는지 테스트하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-124">To test if the problem only affects the UI or the API's:</span></span>

* <span data-ttu-id="6de58-125">Azure Mobile Engagement UI와 Azure Mobile Engagement API 둘 다에서 동일한 기능을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-125">Test the same function from both the Azure Mobile Engagement UI and the Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="6de58-126">휴대폰 네트워크 관련 문제인지를 테스트하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-126">To test if the problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="6de58-127">WIFI를 통해 인터넷에 연결되어 있는 동안과 3G 휴대폰 네트워크를 통해 인터넷에 연결되어 있는 동안 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-127">Test while connected to the Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="6de58-128">방화벽이 Azure Mobile Engagement IP 주소 또는 포트 차단하고 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-128">Confirm that your firewall is not blocking any of the Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="6de58-129">장치 관련 문제인지를 테스트하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-129">To test if the problem is with your Device:</span></span>

* <span data-ttu-id="6de58-130">장치에서 다른 Azure Mobile Engagement 통합 응용 프로그램을 사용하여 Azure Mobile Engagement에 연결할 수 있는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-130">Test if your Device is able to connect to Azure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="6de58-131">Azure Mobile Engagement UI에 표시된 휴대폰에서 이벤트, 작업 및 크래시를 생성할 수 있는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in the Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="6de58-132">해당 장치 ID에 따라 Azure Mobile Engagement UI에서 장치로 푸시 알림을 보낼 수 있는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-132">Test if you can send push notifications from the Azure Mobile Engagement UI to your device based on its Device ID.</span></span> 

5) <span data-ttu-id="6de58-133">앱 관련 문제인지를 테스트하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-133">To test if the problem is with your App:</span></span>

* <span data-ttu-id="6de58-134">실제 장치 대신 에뮬레이터에서 응용 프로그램을 설치하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="6de58-135">최종 사용자 장치의 OS 업그레이드 관련 문제인지를 테스트하려면 다음을 수행합니다(문제를 해결하려면 SDK를 업그레이드해야 함).</span><span class="sxs-lookup"><span data-stu-id="6de58-135">To test if the problem is with OS upgrades to end user Devices, which require an SDK upgrade to resolve:</span></span>

* <span data-ttu-id="6de58-136">OS 버전이 서로 다른 여러 장치에서 응용 프로그램을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-136">Test your application on different devices with different versions of the OS.</span></span>
* <span data-ttu-id="6de58-137">최신 버전의 SDK를 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-137">Confirm that you are using the most recent version of the SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="6de58-138">연결 및 잘못된 정보 문제</span><span class="sxs-lookup"><span data-stu-id="6de58-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="6de58-139">문제</span><span class="sxs-lookup"><span data-stu-id="6de58-139">Issue</span></span>
* <span data-ttu-id="6de58-140">Azure Mobile Engagement UI에 로그인하는 데 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-140">Problems logging into the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="6de58-141">Azure Mobile Engagement API에서 연결 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-141">Connection errors with the Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="6de58-142">장치 API를 통해 앱 정보 태그를 업로드하는 데 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-142">Problems uploading App Info Tags via the Device API.</span></span>
* <span data-ttu-id="6de58-143">Azure Mobile Engagement에서 로그나 내보낸 데이터를 다운로드하는 데 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="6de58-144">Azure Mobile Engagement UI에 잘못된 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-144">Incorrect information shown in the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="6de58-145">Azure Mobile Engagement 로그에 잘못된 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="6de58-146">원인</span><span class="sxs-lookup"><span data-stu-id="6de58-146">Causes</span></span>
* <span data-ttu-id="6de58-147">사용자 계정에 작업을 수행할 수 있는 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-147">Confirm your user account has sufficient permissions to perform the task.</span></span>
* <span data-ttu-id="6de58-148">문제가 단일 컴퓨터나 로컬 네트워크에서만 발생하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-148">Confirm that the problem is not isolated to one computer or your local network.</span></span>
* <span data-ttu-id="6de58-149">Azure Mobile Engagement 서비스에서 작동 중단이 보고되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-149">Confirm that that the Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="6de58-150">앱 정보 태그 파일이 다음 규칙을 모두 따르는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="6de58-151">UTF8 문자 집합만 사용합니다. ANSI 문자 집합은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-151">Use only the UTF8 character set (the ANSI character set is not supported).</span></span>
  * <span data-ttu-id="6de58-152">쉼표(",")를 구분 기호 문자로 사용합니다. .csv 구문 기호 문자를 쉼표(",")에서 세미콜론(";") 등의 다른 문자로 변경하도록 요청하는 서비스 요청을 개설할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-152">Use a comma "," as the separator character (you can open a service request to request to change the .csv separator character from a comma "," to another character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="6de58-153">부울 값 "true"와 "false"에 소문자만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="6de58-154">최대 파일 크기인 35MB보다 작은 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6de58-154">Use a file that is smaller than the maximum file size of 35MB.</span></span>

