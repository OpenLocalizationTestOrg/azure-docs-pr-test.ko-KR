---
title: "스트림 분석을 사용 하 여는 IoT 솔루션 aaaBuild | Microsoft Docs"
description: "Hello 톨게이트 시나리오의 스트림 분석 IoT 솔루션에 대 한 자습서 시작"
keywords: "iot 솔루션, 창 함수"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e37fc5b56c4ffc4a2d7b820afe0c17631e577ea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a><span data-ttu-id="6cdc3-104">Stream Analytics를 사용하여 IoT 솔루션 빌드</span><span class="sxs-lookup"><span data-stu-id="6cdc3-104">Build an IoT solution by using Stream Analytics</span></span>
## <a name="introduction"></a><span data-ttu-id="6cdc3-105">소개</span><span class="sxs-lookup"><span data-stu-id="6cdc3-105">Introduction</span></span>
<span data-ttu-id="6cdc3-106">이 자습서에서는 살펴보겠습니다 어떻게 toouse Azure 스트림 분석 tooget 데이터에서 실시간 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-106">In this tutorial, you will learn how toouse Azure Stream Analytics tooget real-time insights from your data.</span></span> <span data-ttu-id="6cdc3-107">개발자가 기록 레코드 또는 참조 데이터 tooderive 비즈니스 통찰력 스트림을 클릭 스트림, 로그 및 장치에서 생성 된 이벤트와 같은 데이터를 쉽게 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-107">Developers can easily combine streams of data, such as click-streams, logs, and device-generated events, with historical records or reference data tooderive business insights.</span></span> <span data-ttu-id="6cdc3-108">Microsoft Azure에서 호스팅되는 완전히 관리 되는 실시간 스트림 계산 서비스, Azure 스트림 분석 준비 하 고 분 후에 실행할 기본 제공 복원 력, 낮은 대기 시간 및 확장성 tooget 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-108">As a fully managed, real-time stream computation service that's hosted in Microsoft Azure, Azure Stream Analytics provides built-in resiliency, low latency, and scalability tooget you up and running in minutes.</span></span>

<span data-ttu-id="6cdc3-109">이 자습서를 완료하고 나면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-109">After completing this tutorial, you will be able to:</span></span>

* <span data-ttu-id="6cdc3-110">Hello Azure 스트림 분석 포털 숙지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-110">Familiarize yourself with hello Azure Stream Analytics portal.</span></span>
* <span data-ttu-id="6cdc3-111">스트리밍 작업 구성 및 배포</span><span class="sxs-lookup"><span data-stu-id="6cdc3-111">Configure and deploy a streaming job.</span></span>
* <span data-ttu-id="6cdc3-112">실제 문제를 명확히 하 고 hello 스트림 분석 쿼리 언어를 사용 하 여이 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-112">Articulate real-world problems and solve them by using hello Stream Analytics query language.</span></span>
* <span data-ttu-id="6cdc3-113">안심하고 Stream Analytics를 사용하여 고객에 대한 스트리밍 솔루션 개발</span><span class="sxs-lookup"><span data-stu-id="6cdc3-113">Develop streaming solutions for your customers by using Stream Analytics with confidence.</span></span>
* <span data-ttu-id="6cdc3-114">모니터링 및 로깅 경험 tootroubleshoot 문제 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-114">Use hello monitoring and logging experience tootroubleshoot issues.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cdc3-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6cdc3-115">Prerequisites</span></span>
<span data-ttu-id="6cdc3-116">사용자는 필요 hello 필수 구성 요소 toocomplete 다음이 자습서:</span><span class="sxs-lookup"><span data-stu-id="6cdc3-116">You will need hello following prerequisites toocomplete this tutorial:</span></span>

* <span data-ttu-id="6cdc3-117">최신 버전의 hello [Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="6cdc3-117">hello latest version of [Azure PowerShell](/powershell/azure/overview)</span></span>
* <span data-ttu-id="6cdc3-118">2015, visual Studio 2017 또는 무료 hello [Visual Studio 커뮤니티](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="6cdc3-118">Visual Studio 2017, 2015, or hello free [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)</span></span>
* <span data-ttu-id="6cdc3-119">[Azure 구독](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="6cdc3-119">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* <span data-ttu-id="6cdc3-120">Hello 컴퓨터에서 관리자 권한</span><span class="sxs-lookup"><span data-stu-id="6cdc3-120">Administrative privileges on hello computer</span></span>
* <span data-ttu-id="6cdc3-121">다운로드 [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) hello Microsoft 다운로드 센터에서</span><span class="sxs-lookup"><span data-stu-id="6cdc3-121">Download of [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) from hello Microsoft Download Center</span></span>
* <span data-ttu-id="6cdc3-122">선택 사항: 소스 코드에서 hello TollApp 이벤트 생성기에 대 한 [GitHub](https://aka.ms/azure-stream-analytics-toll-source)</span><span class="sxs-lookup"><span data-stu-id="6cdc3-122">Optional: Source code for hello TollApp event generator in [GitHub](https://aka.ms/azure-stream-analytics-toll-source)</span></span>

## <a name="scenario-introduction-hello-toll"></a><span data-ttu-id="6cdc3-123">시나리오 소개: “Hello, Toll!”</span><span class="sxs-lookup"><span data-stu-id="6cdc3-123">Scenario introduction: “Hello, Toll!”</span></span>
<span data-ttu-id="6cdc3-124">톨게이트 요금소는 일반적인 현상입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-124">A toll station is a common phenomenon.</span></span> <span data-ttu-id="6cdc3-125">볼 수 있는 이러한 여러 고속도로, 브리지 및 터널 hello 전 세계 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-125">You encounter them on many expressways, bridges, and tunnels across hello world.</span></span> <span data-ttu-id="6cdc3-126">각 요금소에는 여러 개의 요금 창구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-126">Each toll station has multiple toll booths.</span></span> <span data-ttu-id="6cdc3-127">수동 부스에서 toopay hello 유료 tooan 수행자를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-127">At manual booths, you stop toopay hello toll tooan attendant.</span></span> <span data-ttu-id="6cdc3-128">자동화 된 부스에서 각 창구 위쪽 센서를 차량을 부착 toohello 차량의 바람막이 hello 요금 소 창구를 전달 하면 RFID 카드를 스캔 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-128">At automated booths, a sensor on top of each booth scans an RFID card that's affixed toohello windshield of your vehicle as you pass hello toll booth.</span></span> <span data-ttu-id="6cdc3-129">이 프로토콜은 차량을 이러한 요금 소를 통해 쉽게 toovisualize hello 통로으로 흥미로운 작업도 수행할 수 있는 이벤트 스트림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-129">It is easy toovisualize hello passage of vehicles through these toll stations as an event stream over which interesting operations can be performed.</span></span>

![요금 창구에 서 있는 자동차 사진](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a><span data-ttu-id="6cdc3-131">들어오는 데이터</span><span class="sxs-lookup"><span data-stu-id="6cdc3-131">Incoming data</span></span>
<span data-ttu-id="6cdc3-132">이 자습서에서는 두 가지 데이터 스트림을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-132">This tutorial works with two streams of data.</span></span> <span data-ttu-id="6cdc3-133">센서 hello 나타내기에 설치 하 고 hello 요금 소 종료 hello 첫 번째 스트림에 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-133">Sensors installed in hello entrance and exit of hello toll stations produce hello first stream.</span></span> <span data-ttu-id="6cdc3-134">hello 두 번째 스트림이 차량 등록 데이터를 가진 정적 조회 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-134">hello second stream is a static lookup dataset that has vehicle registration data.</span></span>

### <a name="entry-data-stream"></a><span data-ttu-id="6cdc3-135">진입 데이터 스트림</span><span class="sxs-lookup"><span data-stu-id="6cdc3-135">Entry data stream</span></span>
<span data-ttu-id="6cdc3-136">hello 입력 데이터 스트림을 요금 소에 들어갈 때 자동차에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-136">hello entry data stream contains information about cars as they enter toll stations.</span></span>

| <span data-ttu-id="6cdc3-137">TollId</span><span class="sxs-lookup"><span data-stu-id="6cdc3-137">TollID</span></span> | <span data-ttu-id="6cdc3-138">EntryTime</span><span class="sxs-lookup"><span data-stu-id="6cdc3-138">EntryTime</span></span> | <span data-ttu-id="6cdc3-139">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="6cdc3-139">LicensePlate</span></span> | <span data-ttu-id="6cdc3-140">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="6cdc3-140">State</span></span> | <span data-ttu-id="6cdc3-141">계정을</span><span class="sxs-lookup"><span data-stu-id="6cdc3-141">Make</span></span> | <span data-ttu-id="6cdc3-142">모델</span><span class="sxs-lookup"><span data-stu-id="6cdc3-142">Model</span></span> | <span data-ttu-id="6cdc3-143">VehicleType</span><span class="sxs-lookup"><span data-stu-id="6cdc3-143">VehicleType</span></span> | <span data-ttu-id="6cdc3-144">VehicleWeight</span><span class="sxs-lookup"><span data-stu-id="6cdc3-144">VehicleWeight</span></span> | <span data-ttu-id="6cdc3-145">Toll</span><span class="sxs-lookup"><span data-stu-id="6cdc3-145">Toll</span></span> | <span data-ttu-id="6cdc3-146">태그</span><span class="sxs-lookup"><span data-stu-id="6cdc3-146">Tag</span></span> |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="6cdc3-147">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-147">1</span></span> |<span data-ttu-id="6cdc3-148">2014-09-10 12:01:00.000</span><span class="sxs-lookup"><span data-stu-id="6cdc3-148">2014-09-10 12:01:00.000</span></span> |<span data-ttu-id="6cdc3-149">JNB 7001</span><span class="sxs-lookup"><span data-stu-id="6cdc3-149">JNB 7001</span></span> |<span data-ttu-id="6cdc3-150">NY</span><span class="sxs-lookup"><span data-stu-id="6cdc3-150">NY</span></span> |<span data-ttu-id="6cdc3-151">Honda</span><span class="sxs-lookup"><span data-stu-id="6cdc3-151">Honda</span></span> |<span data-ttu-id="6cdc3-152">CRV</span><span class="sxs-lookup"><span data-stu-id="6cdc3-152">CRV</span></span> |<span data-ttu-id="6cdc3-153">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-153">1</span></span> |<span data-ttu-id="6cdc3-154">0</span><span class="sxs-lookup"><span data-stu-id="6cdc3-154">0</span></span> |<span data-ttu-id="6cdc3-155">7</span><span class="sxs-lookup"><span data-stu-id="6cdc3-155">7</span></span> | |
| <span data-ttu-id="6cdc3-156">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-156">1</span></span> |<span data-ttu-id="6cdc3-157">2014-09-10 12:02:00.000</span><span class="sxs-lookup"><span data-stu-id="6cdc3-157">2014-09-10 12:02:00.000</span></span> |<span data-ttu-id="6cdc3-158">YXZ 1001</span><span class="sxs-lookup"><span data-stu-id="6cdc3-158">YXZ 1001</span></span> |<span data-ttu-id="6cdc3-159">NY</span><span class="sxs-lookup"><span data-stu-id="6cdc3-159">NY</span></span> |<span data-ttu-id="6cdc3-160">Toyota</span><span class="sxs-lookup"><span data-stu-id="6cdc3-160">Toyota</span></span> |<span data-ttu-id="6cdc3-161">Camry</span><span class="sxs-lookup"><span data-stu-id="6cdc3-161">Camry</span></span> |<span data-ttu-id="6cdc3-162">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-162">1</span></span> |<span data-ttu-id="6cdc3-163">0</span><span class="sxs-lookup"><span data-stu-id="6cdc3-163">0</span></span> |<span data-ttu-id="6cdc3-164">4</span><span class="sxs-lookup"><span data-stu-id="6cdc3-164">4</span></span> |<span data-ttu-id="6cdc3-165">123456789</span><span class="sxs-lookup"><span data-stu-id="6cdc3-165">123456789</span></span> |
| <span data-ttu-id="6cdc3-166">3</span><span class="sxs-lookup"><span data-stu-id="6cdc3-166">3</span></span> |<span data-ttu-id="6cdc3-167">2014-09-10 12:02:00.000</span><span class="sxs-lookup"><span data-stu-id="6cdc3-167">2014-09-10 12:02:00.000</span></span> |<span data-ttu-id="6cdc3-168">ABC 1004</span><span class="sxs-lookup"><span data-stu-id="6cdc3-168">ABC 1004</span></span> |<span data-ttu-id="6cdc3-169">CT</span><span class="sxs-lookup"><span data-stu-id="6cdc3-169">CT</span></span> |<span data-ttu-id="6cdc3-170">Ford</span><span class="sxs-lookup"><span data-stu-id="6cdc3-170">Ford</span></span> |<span data-ttu-id="6cdc3-171">Taurus</span><span class="sxs-lookup"><span data-stu-id="6cdc3-171">Taurus</span></span> |<span data-ttu-id="6cdc3-172">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-172">1</span></span> |<span data-ttu-id="6cdc3-173">0</span><span class="sxs-lookup"><span data-stu-id="6cdc3-173">0</span></span> |<span data-ttu-id="6cdc3-174">5</span><span class="sxs-lookup"><span data-stu-id="6cdc3-174">5</span></span> |<span data-ttu-id="6cdc3-175">456789123</span><span class="sxs-lookup"><span data-stu-id="6cdc3-175">456789123</span></span> |
| <span data-ttu-id="6cdc3-176">2</span><span class="sxs-lookup"><span data-stu-id="6cdc3-176">2</span></span> |<span data-ttu-id="6cdc3-177">2014-09-10 12:03:00.000</span><span class="sxs-lookup"><span data-stu-id="6cdc3-177">2014-09-10 12:03:00.000</span></span> |<span data-ttu-id="6cdc3-178">XYZ 1003</span><span class="sxs-lookup"><span data-stu-id="6cdc3-178">XYZ 1003</span></span> |<span data-ttu-id="6cdc3-179">CT</span><span class="sxs-lookup"><span data-stu-id="6cdc3-179">CT</span></span> |<span data-ttu-id="6cdc3-180">Toyota</span><span class="sxs-lookup"><span data-stu-id="6cdc3-180">Toyota</span></span> |<span data-ttu-id="6cdc3-181">Corolla</span><span class="sxs-lookup"><span data-stu-id="6cdc3-181">Corolla</span></span> |<span data-ttu-id="6cdc3-182">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-182">1</span></span> |<span data-ttu-id="6cdc3-183">0</span><span class="sxs-lookup"><span data-stu-id="6cdc3-183">0</span></span> |<span data-ttu-id="6cdc3-184">4</span><span class="sxs-lookup"><span data-stu-id="6cdc3-184">4</span></span> | |
| <span data-ttu-id="6cdc3-185">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-185">1</span></span> |<span data-ttu-id="6cdc3-186">2014-09-10 12:03:00.000</span><span class="sxs-lookup"><span data-stu-id="6cdc3-186">2014-09-10 12:03:00.000</span></span> |<span data-ttu-id="6cdc3-187">1007 BNJ</span><span class="sxs-lookup"><span data-stu-id="6cdc3-187">BNJ 1007</span></span> |<span data-ttu-id="6cdc3-188">NY</span><span class="sxs-lookup"><span data-stu-id="6cdc3-188">NY</span></span> |<span data-ttu-id="6cdc3-189">Honda</span><span class="sxs-lookup"><span data-stu-id="6cdc3-189">Honda</span></span> |<span data-ttu-id="6cdc3-190">CRV</span><span class="sxs-lookup"><span data-stu-id="6cdc3-190">CRV</span></span> |<span data-ttu-id="6cdc3-191">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-191">1</span></span> |<span data-ttu-id="6cdc3-192">0</span><span class="sxs-lookup"><span data-stu-id="6cdc3-192">0</span></span> |<span data-ttu-id="6cdc3-193">5</span><span class="sxs-lookup"><span data-stu-id="6cdc3-193">5</span></span> |<span data-ttu-id="6cdc3-194">789123456</span><span class="sxs-lookup"><span data-stu-id="6cdc3-194">789123456</span></span> |
| <span data-ttu-id="6cdc3-195">2</span><span class="sxs-lookup"><span data-stu-id="6cdc3-195">2</span></span> |<span data-ttu-id="6cdc3-196">2014-09-10 12:05:00.000</span><span class="sxs-lookup"><span data-stu-id="6cdc3-196">2014-09-10 12:05:00.000</span></span> |<span data-ttu-id="6cdc3-197">CDE 1007</span><span class="sxs-lookup"><span data-stu-id="6cdc3-197">CDE 1007</span></span> |<span data-ttu-id="6cdc3-198">NJ</span><span class="sxs-lookup"><span data-stu-id="6cdc3-198">NJ</span></span> |<span data-ttu-id="6cdc3-199">Toyota</span><span class="sxs-lookup"><span data-stu-id="6cdc3-199">Toyota</span></span> |<span data-ttu-id="6cdc3-200">4x4</span><span class="sxs-lookup"><span data-stu-id="6cdc3-200">4x4</span></span> |<span data-ttu-id="6cdc3-201">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-201">1</span></span> |<span data-ttu-id="6cdc3-202">0</span><span class="sxs-lookup"><span data-stu-id="6cdc3-202">0</span></span> |<span data-ttu-id="6cdc3-203">6</span><span class="sxs-lookup"><span data-stu-id="6cdc3-203">6</span></span> |<span data-ttu-id="6cdc3-204">321987654</span><span class="sxs-lookup"><span data-stu-id="6cdc3-204">321987654</span></span> |

<span data-ttu-id="6cdc3-205">Hello 열에 대 한 간단한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-205">Here is a short description of hello columns:</span></span>

| <span data-ttu-id="6cdc3-206">열</span><span class="sxs-lookup"><span data-stu-id="6cdc3-206">Column</span></span> | <span data-ttu-id="6cdc3-207">설명</span><span class="sxs-lookup"><span data-stu-id="6cdc3-207">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6cdc3-208">TollId</span><span class="sxs-lookup"><span data-stu-id="6cdc3-208">TollID</span></span> |<span data-ttu-id="6cdc3-209">요금 소 창구를 고유 하 게 식별 하는 hello 요금 소 창구 ID</span><span class="sxs-lookup"><span data-stu-id="6cdc3-209">hello toll booth ID that uniquely identifies a toll booth</span></span> |
| <span data-ttu-id="6cdc3-210">EntryTime</span><span class="sxs-lookup"><span data-stu-id="6cdc3-210">EntryTime</span></span> |<span data-ttu-id="6cdc3-211">hello 차량 toohello 요금 소 창구 UTC에서의 항목의 hello 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="6cdc3-211">hello date and time of entry of hello vehicle toohello toll booth in UTC</span></span> |
| <span data-ttu-id="6cdc3-212">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="6cdc3-212">LicensePlate</span></span> |<span data-ttu-id="6cdc3-213">hello 번호판 hello 차량</span><span class="sxs-lookup"><span data-stu-id="6cdc3-213">hello license plate number of hello vehicle</span></span> |
| <span data-ttu-id="6cdc3-214">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="6cdc3-214">State</span></span> |<span data-ttu-id="6cdc3-215">미국의 주 이름</span><span class="sxs-lookup"><span data-stu-id="6cdc3-215">A state in United States</span></span> |
| <span data-ttu-id="6cdc3-216">계정을</span><span class="sxs-lookup"><span data-stu-id="6cdc3-216">Make</span></span> |<span data-ttu-id="6cdc3-217">hello 자동차의 hello 제조업체</span><span class="sxs-lookup"><span data-stu-id="6cdc3-217">hello manufacturer of hello automobile</span></span> |
| <span data-ttu-id="6cdc3-218">모델</span><span class="sxs-lookup"><span data-stu-id="6cdc3-218">Model</span></span> |<span data-ttu-id="6cdc3-219">hello 자동차의 hello 모델 번호</span><span class="sxs-lookup"><span data-stu-id="6cdc3-219">hello model number of hello automobile</span></span> |
| <span data-ttu-id="6cdc3-220">VehicleType</span><span class="sxs-lookup"><span data-stu-id="6cdc3-220">VehicleType</span></span> |<span data-ttu-id="6cdc3-221">여객 차량의 경우 1, 화물 차량의 경우 2</span><span class="sxs-lookup"><span data-stu-id="6cdc3-221">Either 1 for passenger vehicles or 2 for commercial vehicles</span></span> |
| <span data-ttu-id="6cdc3-222">WeightType</span><span class="sxs-lookup"><span data-stu-id="6cdc3-222">WeightType</span></span> |<span data-ttu-id="6cdc3-223">차량 무게(톤), 승용차는 0</span><span class="sxs-lookup"><span data-stu-id="6cdc3-223">Vehicle weight in tons; 0 for passenger vehicles</span></span> |
| <span data-ttu-id="6cdc3-224">Toll</span><span class="sxs-lookup"><span data-stu-id="6cdc3-224">Toll</span></span> |<span data-ttu-id="6cdc3-225">usd로 hello 유료 값</span><span class="sxs-lookup"><span data-stu-id="6cdc3-225">hello toll value in USD</span></span> |
| <span data-ttu-id="6cdc3-226">태그</span><span class="sxs-lookup"><span data-stu-id="6cdc3-226">Tag</span></span> |<span data-ttu-id="6cdc3-227">E-tag 지불; 자동화 하는 hello 자동차에 hello hello 지불 수동으로 수행 된 빈 값</span><span class="sxs-lookup"><span data-stu-id="6cdc3-227">hello e-Tag on hello automobile that automates payment; blank where hello payment was done manually</span></span> |

### <a name="exit-data-stream"></a><span data-ttu-id="6cdc3-228">진출 데이터 스트림</span><span class="sxs-lookup"><span data-stu-id="6cdc3-228">Exit data stream</span></span>
<span data-ttu-id="6cdc3-229">hello 종료 데이터 스트림을 hello 유료 스테이션을 그대로 두고 자동차에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-229">hello exit data stream contains information about cars leaving hello toll station.</span></span>

| <span data-ttu-id="6cdc3-230">**TollId**</span><span class="sxs-lookup"><span data-stu-id="6cdc3-230">**TollId**</span></span> | <span data-ttu-id="6cdc3-231">**ExitTime**</span><span class="sxs-lookup"><span data-stu-id="6cdc3-231">**ExitTime**</span></span> | <span data-ttu-id="6cdc3-232">**LicensePlate**</span><span class="sxs-lookup"><span data-stu-id="6cdc3-232">**LicensePlate**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6cdc3-233">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-233">1</span></span> |<span data-ttu-id="6cdc3-234">2014-09-10T12:03:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="6cdc3-234">2014-09-10T12:03:00.0000000Z</span></span> |<span data-ttu-id="6cdc3-235">JNB 7001</span><span class="sxs-lookup"><span data-stu-id="6cdc3-235">JNB 7001</span></span> |
| <span data-ttu-id="6cdc3-236">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-236">1</span></span> |<span data-ttu-id="6cdc3-237">2014-09-10T12:03:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="6cdc3-237">2014-09-10T12:03:00.0000000Z</span></span> |<span data-ttu-id="6cdc3-238">YXZ 1001</span><span class="sxs-lookup"><span data-stu-id="6cdc3-238">YXZ 1001</span></span> |
| <span data-ttu-id="6cdc3-239">3</span><span class="sxs-lookup"><span data-stu-id="6cdc3-239">3</span></span> |<span data-ttu-id="6cdc3-240">2014-09-10T12:04:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="6cdc3-240">2014-09-10T12:04:00.0000000Z</span></span> |<span data-ttu-id="6cdc3-241">ABC 1004</span><span class="sxs-lookup"><span data-stu-id="6cdc3-241">ABC 1004</span></span> |
| <span data-ttu-id="6cdc3-242">2</span><span class="sxs-lookup"><span data-stu-id="6cdc3-242">2</span></span> |<span data-ttu-id="6cdc3-243">2014-09-10T12:07:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="6cdc3-243">2014-09-10T12:07:00.0000000Z</span></span> |<span data-ttu-id="6cdc3-244">XYZ 1003</span><span class="sxs-lookup"><span data-stu-id="6cdc3-244">XYZ 1003</span></span> |
| <span data-ttu-id="6cdc3-245">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-245">1</span></span> |<span data-ttu-id="6cdc3-246">2014-09-10T12:08:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="6cdc3-246">2014-09-10T12:08:00.0000000Z</span></span> |<span data-ttu-id="6cdc3-247">1007 BNJ</span><span class="sxs-lookup"><span data-stu-id="6cdc3-247">BNJ 1007</span></span> |
| <span data-ttu-id="6cdc3-248">2</span><span class="sxs-lookup"><span data-stu-id="6cdc3-248">2</span></span> |<span data-ttu-id="6cdc3-249">2014-09-10T12:07:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="6cdc3-249">2014-09-10T12:07:00.0000000Z</span></span> |<span data-ttu-id="6cdc3-250">CDE 1007</span><span class="sxs-lookup"><span data-stu-id="6cdc3-250">CDE 1007</span></span> |

<span data-ttu-id="6cdc3-251">Hello 열에 대 한 간단한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-251">Here is a short description of hello columns:</span></span>

| <span data-ttu-id="6cdc3-252">열</span><span class="sxs-lookup"><span data-stu-id="6cdc3-252">Column</span></span> | <span data-ttu-id="6cdc3-253">설명</span><span class="sxs-lookup"><span data-stu-id="6cdc3-253">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6cdc3-254">TollId</span><span class="sxs-lookup"><span data-stu-id="6cdc3-254">TollID</span></span> |<span data-ttu-id="6cdc3-255">요금 소 창구를 고유 하 게 식별 하는 hello 요금 소 창구 ID</span><span class="sxs-lookup"><span data-stu-id="6cdc3-255">hello toll booth ID that uniquely identifies a toll booth</span></span> |
| <span data-ttu-id="6cdc3-256">ExitTime</span><span class="sxs-lookup"><span data-stu-id="6cdc3-256">ExitTime</span></span> |<span data-ttu-id="6cdc3-257">hello 날짜와 시간을 utc로 요금 소 창구 hello 차량 종료</span><span class="sxs-lookup"><span data-stu-id="6cdc3-257">hello date and time of exit of hello vehicle from toll booth in UTC</span></span> |
| <span data-ttu-id="6cdc3-258">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="6cdc3-258">LicensePlate</span></span> |<span data-ttu-id="6cdc3-259">hello 번호판 hello 차량</span><span class="sxs-lookup"><span data-stu-id="6cdc3-259">hello license plate number of hello vehicle</span></span> |

### <a name="commercial-vehicle-registration-data"></a><span data-ttu-id="6cdc3-260">화물 차량 등록 데이터</span><span class="sxs-lookup"><span data-stu-id="6cdc3-260">Commercial vehicle registration data</span></span>
<span data-ttu-id="6cdc3-261">hello 자습서에서는 정적 상용차 등록 데이터베이스 스냅숏을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-261">hello tutorial uses a static snapshot of a commercial vehicle registration database.</span></span>

| <span data-ttu-id="6cdc3-262">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="6cdc3-262">LicensePlate</span></span> | <span data-ttu-id="6cdc3-263">RegistrationId</span><span class="sxs-lookup"><span data-stu-id="6cdc3-263">RegistrationId</span></span> | <span data-ttu-id="6cdc3-264">만료됨</span><span class="sxs-lookup"><span data-stu-id="6cdc3-264">Expired</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6cdc3-265">SVT 6023</span><span class="sxs-lookup"><span data-stu-id="6cdc3-265">SVT 6023</span></span> |<span data-ttu-id="6cdc3-266">285429838</span><span class="sxs-lookup"><span data-stu-id="6cdc3-266">285429838</span></span> |<span data-ttu-id="6cdc3-267">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-267">1</span></span> |
| <span data-ttu-id="6cdc3-268">XLZ 3463</span><span class="sxs-lookup"><span data-stu-id="6cdc3-268">XLZ 3463</span></span> |<span data-ttu-id="6cdc3-269">362715656</span><span class="sxs-lookup"><span data-stu-id="6cdc3-269">362715656</span></span> |<span data-ttu-id="6cdc3-270">0</span><span class="sxs-lookup"><span data-stu-id="6cdc3-270">0</span></span> |
| <span data-ttu-id="6cdc3-271">BAC 1005</span><span class="sxs-lookup"><span data-stu-id="6cdc3-271">BAC 1005</span></span> |<span data-ttu-id="6cdc3-272">876133137</span><span class="sxs-lookup"><span data-stu-id="6cdc3-272">876133137</span></span> |<span data-ttu-id="6cdc3-273">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-273">1</span></span> |
| <span data-ttu-id="6cdc3-274">RIV 8632</span><span class="sxs-lookup"><span data-stu-id="6cdc3-274">RIV 8632</span></span> |<span data-ttu-id="6cdc3-275">992711956</span><span class="sxs-lookup"><span data-stu-id="6cdc3-275">992711956</span></span> |<span data-ttu-id="6cdc3-276">0</span><span class="sxs-lookup"><span data-stu-id="6cdc3-276">0</span></span> |
| <span data-ttu-id="6cdc3-277">SNY 7188</span><span class="sxs-lookup"><span data-stu-id="6cdc3-277">SNY 7188</span></span> |<span data-ttu-id="6cdc3-278">592133890</span><span class="sxs-lookup"><span data-stu-id="6cdc3-278">592133890</span></span> |<span data-ttu-id="6cdc3-279">0</span><span class="sxs-lookup"><span data-stu-id="6cdc3-279">0</span></span> |
| <span data-ttu-id="6cdc3-280">ELH 9896</span><span class="sxs-lookup"><span data-stu-id="6cdc3-280">ELH 9896</span></span> |<span data-ttu-id="6cdc3-281">678427724</span><span class="sxs-lookup"><span data-stu-id="6cdc3-281">678427724</span></span> |<span data-ttu-id="6cdc3-282">1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-282">1</span></span> |

<span data-ttu-id="6cdc3-283">Hello 열에 대 한 간단한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-283">Here is a short description of hello columns:</span></span>

| <span data-ttu-id="6cdc3-284">열</span><span class="sxs-lookup"><span data-stu-id="6cdc3-284">Column</span></span> | <span data-ttu-id="6cdc3-285">설명</span><span class="sxs-lookup"><span data-stu-id="6cdc3-285">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6cdc3-286">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="6cdc3-286">LicensePlate</span></span> |<span data-ttu-id="6cdc3-287">hello 번호판 hello 차량</span><span class="sxs-lookup"><span data-stu-id="6cdc3-287">hello license plate number of hello vehicle</span></span> |
| <span data-ttu-id="6cdc3-288">RegistrationId</span><span class="sxs-lookup"><span data-stu-id="6cdc3-288">RegistrationId</span></span> |<span data-ttu-id="6cdc3-289">hello 차량 등록 ID</span><span class="sxs-lookup"><span data-stu-id="6cdc3-289">hello vehicle's registration ID</span></span> |
| <span data-ttu-id="6cdc3-290">만료됨</span><span class="sxs-lookup"><span data-stu-id="6cdc3-290">Expired</span></span> |<span data-ttu-id="6cdc3-291">hello hello 차량 등록 상태: 0 차량 등록 중인 경우 등록이 만료 되 면 1</span><span class="sxs-lookup"><span data-stu-id="6cdc3-291">hello registration status of hello vehicle: 0 if vehicle registration is active, 1 if registration is expired</span></span> |

## <a name="set-up-hello-environment-for-azure-stream-analytics"></a><span data-ttu-id="6cdc3-292">Azure 스트림 분석에 대 한 hello 환경 설정</span><span class="sxs-lookup"><span data-stu-id="6cdc3-292">Set up hello environment for Azure Stream Analytics</span></span>
<span data-ttu-id="6cdc3-293">toocomplete이이 자습서에서는 Microsoft Azure 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-293">toocomplete this tutorial, you need a Microsoft Azure subscription.</span></span> <span data-ttu-id="6cdc3-294">Microsoft는 Microsoft Azure 서비스에 대한 평가판을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-294">Microsoft offers free trial for Microsoft Azure services.</span></span>

<span data-ttu-id="6cdc3-295">Azure 계정이 없는 경우 [평가판 버전을 요청](http://azure.microsoft.com/pricing/free-trial/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-295">If you do not have an Azure account, you can [request a free trial version](http://azure.microsoft.com/pricing/free-trial/).</span></span>

> [!NOTE]
> <span data-ttu-id="6cdc3-296">무료 평가판에 대해 toosign, 문자 메시지 및 유효한 신용 카드를 받을 수 있는 모바일 장치가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-296">toosign up for a free trial, you need a mobile device that can receive text messages and a valid credit card.</span></span>
> 
> 

<span data-ttu-id="6cdc3-297">Toofollow hello Azure 크레딧 사용에 가장 적합 hello 내릴 수 있도록이 문서의 끝 hello에 hello ""정리 하 여 Azure 계정"섹션에서 단계 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-297">Be sure toofollow hello steps in hello “Clean up your Azure account” section at hello end of this article so that you can make hello best use of your Azure credit.</span></span>

## <a name="provision-azure-resources-required-for-hello-tutorial"></a><span data-ttu-id="6cdc3-298">Hello 자습서에 필요한 Azure 리소스를 프로 비전</span><span class="sxs-lookup"><span data-stu-id="6cdc3-298">Provision Azure resources required for hello tutorial</span></span>
<span data-ttu-id="6cdc3-299">이 자습서에서는 두 개의 이벤트 허브 tooreceive *항목* 및 *종료* 데이터 스트림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-299">This tutorial requires two event hubs tooreceive *entry* and *exit* data streams.</span></span> <span data-ttu-id="6cdc3-300">Azure SQL 데이터베이스의 hello 스트림 분석 작업 hello 결과 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-300">Azure SQL Database outputs hello results of hello Stream Analytics jobs.</span></span> <span data-ttu-id="6cdc3-301">Azure 저장소는 차량 등록에 대한 참조 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-301">Azure Storage stores reference data about vehicle registrations.</span></span>

<span data-ttu-id="6cdc3-302">사용할 수 있습니다 hello Setup.ps1 스크립트 hello TollApp 폴더에 GitHub toocreate에 필요한 모든 리소스.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-302">You can use hello Setup.ps1 script in hello TollApp folder on GitHub toocreate all required resources.</span></span> <span data-ttu-id="6cdc3-303">Hello 관심 있는 시간을 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-303">In hello interest of time, we recommend that you run it.</span></span> <span data-ttu-id="6cdc3-304">어떻게 tooconfigure hello Azure 포털에서에서 이러한 리소스를 참조 하는 방법에 대 한 자세한 toolearn 원하는 경우 toohello "Azure 포털에서 자습서 리소스 구성" 부록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-304">If you would like toolearn more about how tooconfigure these resources in hello Azure portal, refer toohello “Configuring tutorial resources in Azure portal” appendix.</span></span>

<span data-ttu-id="6cdc3-305">다운로드 하 고 hello 지원 저장 [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) 폴더 및 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-305">Download and save hello supporting [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) folder and files.</span></span>

<span data-ttu-id="6cdc3-306">**Microsoft Azure PowerShell** 창을 *관리자 권한으로*엽니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-306">Open a **Microsoft Azure PowerShell** window *as an administrator*.</span></span> <span data-ttu-id="6cdc3-307">Azure PowerShell 아직 없는 경우 hello 지침에 따라 [설치 Azure PowerShell을 구성 하 고](/powershell/azure/overview) tooinstall 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-307">If you do not yet have Azure PowerShell, follow hello instructions in [Install and configure Azure PowerShell](/powershell/azure/overview) tooinstall it.</span></span>

<span data-ttu-id="6cdc3-308">Windows.ps1,.dll 및.exe 파일에 자동으로 차단, 하기 때문에 hello 스크립트를 실행 하기 전에 tooset hello 실행 정책이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-308">Because Windows automatically blocks .ps1, .dll, and .exe files, you need tooset hello execution policy before you run hello script.</span></span> <span data-ttu-id="6cdc3-309">Hello Azure PowerShell 창에서 실행 되 고 있는지 확인 *관리자로 서*합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-309">Make sure hello Azure PowerShell window is running *as an administrator*.</span></span> <span data-ttu-id="6cdc3-310">**Set-ExecutionPolicy unrestricted**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-310">Run **Set-ExecutionPolicy unrestricted**.</span></span> <span data-ttu-id="6cdc3-311">메시지가 표시되면 **Y**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-311">When prompted, type **Y**.</span></span>

![Azure PowerShell 창에서 실행 중인 "Set-executionpolicy unrestricted"의 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

<span data-ttu-id="6cdc3-313">실행 **Get-executionpolicy** toomake hello 명령 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-313">Run **Get-ExecutionPolicy** toomake sure that hello command worked.</span></span>

![Azure PowerShell 창에서 실행 중인 "Get-ExecutionPolicy"의 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

<span data-ttu-id="6cdc3-315">Hello 스크립트 및 응용 프로그램 생성기 있는 toohello 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-315">Go toohello directory that has hello scripts and generator application.</span></span>

!["Cd.\TollApp\TollApp" hello Azure PowerShell 창에서 실행의 스크린 샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

<span data-ttu-id="6cdc3-317">형식 **.\\ Setup.ps1** tooset Azure 계정 만들기 및 필요한 모든 리소스를 구성 및 toogenerate 이벤트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-317">Type **.\\Setup.ps1** tooset up your Azure account, create and configure all required resources, and start toogenerate events.</span></span> <span data-ttu-id="6cdc3-318">hello 스크립트 임의로 선택 영역 toocreate 리소스 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-318">hello script randomly picks up a region toocreate your resources.</span></span> <span data-ttu-id="6cdc3-319">hello를 전달할 수 있습니다, tooexplicitly 지역을 지정 **-위치** hello 다음 예제 에서처럼 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="6cdc3-319">tooexplicitly specify a region, you can pass hello **-location** parameter as in hello following example:</span></span>

<span data-ttu-id="6cdc3-320">**.\\Setup.ps1 -location “Central US”**</span><span class="sxs-lookup"><span data-stu-id="6cdc3-320">**.\\Setup.ps1 -location “Central US”**</span></span>

![Hello Azure 로그인 페이지의 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

<span data-ttu-id="6cdc3-322">hello 스크립트 열립니다 hello **로그인** Microsoft Azure에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-322">hello script opens hello **Sign In** page for Microsoft Azure.</span></span> <span data-ttu-id="6cdc3-323">계정 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-323">Enter your account credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="6cdc3-324">계정에 대 한 액세스 toomultiple 구독이 묻는 tooenter hello 구독 이름을 hello 자습서 toouse 되도록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-324">If your account has access toomultiple subscriptions, you will be asked tooenter hello subscription name that you want toouse for hello tutorial.</span></span>
> 
> 

<span data-ttu-id="6cdc3-325">hello 스크립트에는 몇 분 toorun을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-325">hello script can take several minutes toorun.</span></span> <span data-ttu-id="6cdc3-326">완료 되 면 hello 출력 스크린 샷 다음 hello와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-326">After it finishes, hello output should look like hello following screenshot.</span></span>

![Hello Azure PowerShell 창에서 hello 스크립트의 출력의 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

<span data-ttu-id="6cdc3-328">다음 스크린 샷 유사한 toohello 있는 다른 창도 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-328">You will also see another window that's similar toohello following screenshot.</span></span> <span data-ttu-id="6cdc3-329">이 응용 프로그램 이벤트를 보내는 tooAzure 이벤트 허브 필요한 toorun hello 자습서 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-329">This application is sending events tooAzure Event Hubs, which is required toorun hello tutorial.</span></span> <span data-ttu-id="6cdc3-330">따라서 hello 응용 프로그램을 중지 하거나 마십시오 hello 자습서를 완료 될 때까지이 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-330">So, do not stop hello application or close this window until you finish hello tutorial.</span></span>

!["이벤트 허브 데이터 전송 중" 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

<span data-ttu-id="6cdc3-332">있습니다 수 toosee 리소스에에서 있어야 Azure 포털 이제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-332">You should be able toosee your resources in Azure portal now.</span></span> <span data-ttu-id="6cdc3-333">너무 이동<https://portal.azure.com>, 및 계정 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-333">Go too<https://portal.azure.com>, and sign in with your account credentials.</span></span> <span data-ttu-id="6cdc3-334">일부 기능은 hello 클래식 포털 활용 현재 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-334">Note that currently some functionality utilizes hello classic portal.</span></span> <span data-ttu-id="6cdc3-335">다음 단계가 명확하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-335">These steps will be clearly indicated.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="6cdc3-336">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6cdc3-336">Azure Event Hubs</span></span>
<span data-ttu-id="6cdc3-337">Hello Azure 포털에서에서 클릭 **더 많은 서비스** hello hello 관리 왼쪽된 창 아래쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-337">In hello Azure portal, click **More services** on hello bottom of hello left management pane.</span></span> <span data-ttu-id="6cdc3-338">형식 **이벤트 허브** hello 제공 된 필드와 클릭 **이벤트 허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-338">Type **Event hubs** in hello field provided and click **Event hubs**.</span></span> <span data-ttu-id="6cdc3-339">그러면 새 브라우저 창 toodisplay hello **서비스 버스** hello에 대 한 영역 **클래식 포털**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-339">This launches a new browser window toodisplay hello **SERVICE BUS** area in hello **classic portal**.</span></span> <span data-ttu-id="6cdc3-340">여기서 hello hello Setup.ps1 스크립트에서 만든 이벤트 허브를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-340">Here you can see hello Event Hub created by hello Setup.ps1 script.</span></span>

![서비스 버스](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

<span data-ttu-id="6cdc3-342">Hello로 시작 하는 하나 클릭 *tolldata*합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-342">Click hello one that starts with *tolldata*.</span></span> <span data-ttu-id="6cdc3-343">Hello 클릭 **이벤트 허브** 탭 합니다. 이 네임스페이스에서 만든 *진입*과 *진출*이라는 두 개의 이벤트 허브가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-343">Click hello **EVENT HUBS** tab. You will see two event hubs named *entry* and *exit* created in this namespace.</span></span>

![Hello 클래식 포털의 이벤트 허브 탭](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a><span data-ttu-id="6cdc3-345">Azure 저장소 컨테이너</span><span class="sxs-lookup"><span data-stu-id="6cdc3-345">Azure Storage container</span></span>
1. <span data-ttu-id="6cdc3-346">브라우저 열려 tooAzure 포털에서 toohello 탭을 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-346">Go back toohello tab in your browser open tooAzure portal.</span></span> <span data-ttu-id="6cdc3-347">클릭 **저장소** hello hello 자습서에 사용 되는 hello Azure 포털 toosee hello Azure 저장소 컨테이너의 왼쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-347">Click **STORAGE** on hello left side of hello Azure portal toosee hello Azure Storage container that's used in hello tutorial.</span></span>
   
    ![저장소 메뉴 항목](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. <span data-ttu-id="6cdc3-349">Hello로 시작 하는 하나 클릭 *tolldata*합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-349">Click hello one that start with *tolldata*.</span></span> <span data-ttu-id="6cdc3-350">Hello 클릭 **컨테이너** 탭 toosee hello 만들 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-350">Click hello **CONTAINERS** tab toosee hello created container.</span></span>
   
    ![Hello Azure 포털에서에서 컨테이너 탭](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. <span data-ttu-id="6cdc3-352">Hello 클릭 **tolldata** 컨테이너 toosee hello 차량 등록 데이터를 사용 하는 JSON 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-352">Click hello **tolldata** container toosee hello uploaded JSON file that has vehicle registration data.</span></span>
   
    ![Hello 컨테이너에서 hello registration.json 파일의 스크린 샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a><span data-ttu-id="6cdc3-354">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6cdc3-354">Azure SQL Database</span></span>
1. <span data-ttu-id="6cdc3-355">Azure 포털 toohello hello 브라우저에서 열렸으면 hello 첫 번째 탭에서 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-355">Go back toohello Azure portal on hello first tab that was opened in hello browser.</span></span> <span data-ttu-id="6cdc3-356">클릭 **SQL 데이터베이스** hello hello 자습서에 사용 되 고 클릭 하는 hello Azure 포털 toosee hello SQL 데이터베이스의 왼쪽에 **tolldatadb**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-356">Click **SQL DATABASES** on hello left side of hello Azure portal toosee hello SQL database that will be used in hello tutorial and click **tolldatadb**.</span></span>
   
    ![만든 hello SQL 데이터베이스의 스크린 샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. <span data-ttu-id="6cdc3-358">Hello 포트 번호 없이 복사 hello 서버 이름 (*servername*. 예를 들어 database.windows.net).</span><span class="sxs-lookup"><span data-stu-id="6cdc3-358">Copy hello server name without hello port number (*servername*.database.windows.net, for example).</span></span>
    <span data-ttu-id="6cdc3-359">![만든 hello SQL 데이터베이스 db의 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)</span><span class="sxs-lookup"><span data-stu-id="6cdc3-359">![Screenshot of hello created SQL database db](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)</span></span>

## <a name="connect-toohello-database-from-visual-studio"></a><span data-ttu-id="6cdc3-360">Visual Studio에서 toohello 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="6cdc3-360">Connect toohello database from Visual Studio</span></span>
<span data-ttu-id="6cdc3-361">Visual Studio tooaccess 쿼리 결과 사용 하 여 hello 출력 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-361">Use Visual Studio tooaccess query results in hello output database.</span></span>

<span data-ttu-id="6cdc3-362">Visual Studio에서 toohello SQL 데이터베이스 (hello 대상)을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-362">Connect toohello SQL database (hello destination) from Visual Studio:</span></span>

1. <span data-ttu-id="6cdc3-363">Visual Studio를 열고 클릭 **도구** > **tooDatabase 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-363">Open Visual Studio, and then click **Tools** > **Connect tooDatabase**.</span></span>
2. <span data-ttu-id="6cdc3-364">표시되는 메시지에 따라 **Microsoft SQL Server**를 데이터 원본으로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-364">If asked, click **Microsoft SQL Server** as a data source.</span></span>
   
    ![데이터 원본 변경 대화 상자](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. <span data-ttu-id="6cdc3-366">Hello에 **서버 이름** 필드, hello Azure 포털에서에서 hello 이전 섹션에서 복사한 hello 이름을 붙여 넣습니다 (즉, *servername*. database.windows.net).</span><span class="sxs-lookup"><span data-stu-id="6cdc3-366">In hello **Server name** field, paste hello name that you copied in hello previous section from hello Azure portal (that is, *servername*.database.windows.net).</span></span>
4. <span data-ttu-id="6cdc3-367">**SQL Server 인증 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-367">Click **Use SQL Server Authentication**.</span></span>
5. <span data-ttu-id="6cdc3-368">입력 **tolladmin** hello에 **사용자 이름** 필드 및 **123toll!**</span><span class="sxs-lookup"><span data-stu-id="6cdc3-368">Enter **tolladmin** in hello **User name** field and **123toll!**</span></span> <span data-ttu-id="6cdc3-369">hello에 **암호** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-369">in hello **Password** field.</span></span>
6. <span data-ttu-id="6cdc3-370">클릭 **데이터베이스 이름 선택 또는 입력**를 선택 하 고 **TollDataDB** hello 데이터베이스로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-370">Click **Select or enter a database name**, and select **TollDataDB** as hello database.</span></span>
   
    ![연결 추가 대화 상자](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. <span data-ttu-id="6cdc3-372">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-372">Click **OK**.</span></span>
8. <span data-ttu-id="6cdc3-373">서버 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-373">Open Server Explorer.</span></span>
   
    ![서버 탐색기](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. <span data-ttu-id="6cdc3-375">Hello TollDataDB 데이터베이스에 4 개의 테이블을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-375">See four tables in hello TollDataDB database.</span></span>
   
    ![Hello TollDataDB 데이터베이스의 테이블](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a><span data-ttu-id="6cdc3-377">이벤트 생성기: TollApp 샘플 프로젝트</span><span class="sxs-lookup"><span data-stu-id="6cdc3-377">Event generator: TollApp sample project</span></span>
<span data-ttu-id="6cdc3-378">PowerShell 스크립트 hello hello TollApp 샘플 응용 프로그램을 사용 하 여 toosend 이벤트를 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-378">hello PowerShell script automatically starts toosend events by using hello TollApp sample application program.</span></span> <span data-ttu-id="6cdc3-379">Tooperform 추가 단계가 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-379">You don’t need tooperform any additional steps.</span></span>

<span data-ttu-id="6cdc3-380">그러나 경우에 관심이 있는 구현 정보를 찾을 수 있습니다 hello TollApp 응용 프로그램의 소스 코드 hello GitHub에서 [샘플/TollApp](https://aka.ms/azure-stream-analytics-toll-source)합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-380">However, if you are interested in implementation details, you can find hello source code of hello TollApp application in GitHub [samples/TollApp](https://aka.ms/azure-stream-analytics-toll-source).</span></span>

![Visual Studio에 표시된 샘플 코드의 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="6cdc3-382">Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="6cdc3-382">Create a Stream Analytics job</span></span>
1. <span data-ttu-id="6cdc3-383">Azure 포털 hello 새 스트림 분석 작업 클릭 hello 페이지 toocreate의 hello 왼쪽 위 모서리에 있는 녹색 더하기 기호를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-383">In hello Azure portal, click hello green plus sign in hello top-left corner of hello page toocreate a new Stream Analytics job.</span></span> <span data-ttu-id="6cdc3-384">**인텔리전스+분석**을 선택한 다음 **Stream Analytics 작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-384">Select **Intelligence + Analytics** and then click **Stream Analytics job**.</span></span>
   
    ![새 단추](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. <span data-ttu-id="6cdc3-386">작업 이름을 지정 hello 구독 유효성 검사, 해결 한 다음 hello에서 새 리소스 그룹을 만듭니다는 hello 이벤트 허브 저장소와 동일한 지역 (기본값 hello 스크립트에 대 한 미국 중남부은).</span><span class="sxs-lookup"><span data-stu-id="6cdc3-386">Provide a job name, validate hello subscription is correct and then create a new Resource group in hello same region as hello Event hub storage (default is South Central US for hello script).</span></span>
3. <span data-ttu-id="6cdc3-387">클릭 **Pin toodashboard** 차례로 **만들기** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-387">Click **Pin toodashboard** and then **CREATE** at hello bottom of hello page.</span></span>
   
    ![Stream Analytics 작업 만들기 옵션](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a><span data-ttu-id="6cdc3-389">입력 원본 정의</span><span class="sxs-lookup"><span data-stu-id="6cdc3-389">Define input sources</span></span>
1. <span data-ttu-id="6cdc3-390">hello 작업 만들고 hello 작업 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-390">hello job will create and open hello job page.</span></span> <span data-ttu-id="6cdc3-391">또는 hello 포털 대시보드에서 분석 작업을 생성 하는 hello를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-391">Or you can click hello created analytics job on hello portal dashboard.</span></span>

2. <span data-ttu-id="6cdc3-392">Hello 클릭 **입력** toodefine hello 원본 데이터를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-392">Click hello **INPUTS** tab toodefine hello source data.</span></span>
   
    ![hello 입력 탭](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. <span data-ttu-id="6cdc3-394">**입력 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-394">Click **ADD AN INPUT**.</span></span>
   
    ![hello 추가 입력 옵션](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. <span data-ttu-id="6cdc3-396">**입력 별칭**으로 **EntryStream**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-396">Enter **EntryStream** as **INPUT ALIAS**.</span></span>
5. <span data-ttu-id="6cdc3-397">원본 형식은 **데이터 스트림**입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-397">Source Type is **Data Stream**</span></span>
6. <span data-ttu-id="6cdc3-398">원본은 **Event hub**입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-398">Source is **Event hub**.</span></span>
7. <span data-ttu-id="6cdc3-399">**서비스 버스 네임 스페이스** hello에 TollData 하나 드롭 다운 hello 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-399">**Service bus namespace** should be hello TollData one in hello drop down.</span></span>
8. <span data-ttu-id="6cdc3-400">**이벤트 허브 이름** 설정할지 너무**항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-400">**Event hub name** should be set too**entry**.</span></span>
9. <span data-ttu-id="6cdc3-401">**이벤트 허브 정책 이름*은 **RootManageSharedAccessKey** (기본값 hello).</span><span class="sxs-lookup"><span data-stu-id="6cdc3-401">**Event hub policy name*is **RootManageSharedAccessKey**  (hello default value).</span></span>
10. <span data-ttu-id="6cdc3-402">**이벤트 직렬화 형식**에 대해 **JSON**을, **인코딩**에 대해 **UTF8**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-402">Select **JSON** for **EVENT SERIALIZATION FORMAT** and **UTF8** for **ENCODING**.</span></span>
   
    <span data-ttu-id="6cdc3-403">설정이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-403">Your settings will look like:</span></span>
   
    ![이벤트 허브 설정](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. <span data-ttu-id="6cdc3-405">클릭 **만들기** hello hello 페이지 toofinish hello 마법사 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-405">Click **Create** at hello bottom of hello page toofinish hello wizard.</span></span>
    
    <span data-ttu-id="6cdc3-406">Hello 수행한는 hello 항목 스트림을 만들었으므로 이제 같은 단계 toocreate hello 종료 스트림에 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-406">Now that you've created hello entry stream, you will follow hello same steps toocreate hello exit stream.</span></span> <span data-ttu-id="6cdc3-407">Hello 스크린 샷 뒤에서 같이 있는지 tooenter 값 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-407">Be sure tooenter values as on hello following screenshot.</span></span>
    
    ![Hello 종료 스트림에 대 한 설정](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    <span data-ttu-id="6cdc3-409">다음 두 진입 스트림을 정의했을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-409">You have defined two input streams:</span></span>
    
    ![Hello Azure 포털에에서 입력된 스트림을 정의](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    <span data-ttu-id="6cdc3-411">다음으로, 자동차 대 한 등록 데이터를 포함 하는 hello blob 파일에 대 한 참조 데이터 입력을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-411">Next, you will add reference data input for hello blob file that contains car registration data.</span></span>
11. <span data-ttu-id="6cdc3-412">클릭 **추가**, 한 다음 hello 동일 hello 스트림 입력에 대 한 처리에 선택에 따라 **참조 데이터** 대신 **데이터 스트림을** 및 hello **입력 별칭**  은 **등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-412">Click **ADD**, and then follow hello same process for hello stream inputs but select **REFERENCE DATA** instead of **Data Stream** and hello **Input Alias** is **Registration**.</span></span>

12. <span data-ttu-id="6cdc3-413">**tolldata**로 시작하는 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-413">storage account that starts with **tolldata**.</span></span> <span data-ttu-id="6cdc3-414">hello 컨테이너 이름은 여야 합니다 **tolldata**, 및 hello **경로 패턴** 해야 **registration.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-414">hello container name should be **tolldata**, and hello **PATH PATTERN** should be **registration.json**.</span></span> <span data-ttu-id="6cdc3-415">이 파일 이름은 대/소문자를 구분하므로 **소문자**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-415">This file name is case sensitive and should be **lowercase**.</span></span>
    
    ![블로그 저장소 설정](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. <span data-ttu-id="6cdc3-417">클릭 **만들기** toofinish hello 마법사.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-417">Click **Create** toofinish hello wizard.</span></span>

<span data-ttu-id="6cdc3-418">이제 모든 입력이 정의되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-418">Now all inputs are defined.</span></span>

## <a name="define-output"></a><span data-ttu-id="6cdc3-419">출력 정의</span><span class="sxs-lookup"><span data-stu-id="6cdc3-419">Define output</span></span>
1. <span data-ttu-id="6cdc3-420">Hello 스트림 분석 작업 개요 창에서 선택 **출력**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-420">On hello Stream Analytics job overview pane, select **OUTPUTS**.</span></span>
   
    ![hello 출력 탭 및 옵션 "출력을 추가 합니다."](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. <span data-ttu-id="6cdc3-422">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-422">Click **Add**.</span></span>
3. <span data-ttu-id="6cdc3-423">집합 hello **출력 별칭** too'output' 차례로 **싱크** 너무**SQL 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-423">Set hello **Output alias** too'output' and then **Sink** too**SQL database**.</span></span>
3. <span data-ttu-id="6cdc3-424">Hello hello 문서의 "Visual Studio에서 연결 tooDatabase" 섹션에에서 사용 된 hello 서버 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-424">Select hello server name that was used in hello “Connect tooDatabase from Visual Studio” section of hello article.</span></span> <span data-ttu-id="6cdc3-425">데이터베이스 이름은 hello **TollDataDB**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-425">hello database name is **TollDataDB**.</span></span>
4. <span data-ttu-id="6cdc3-426">입력 **tolladmin** hello에 **USERNAME** 필드 **123toll!**</span><span class="sxs-lookup"><span data-stu-id="6cdc3-426">Enter **tolladmin** in hello **USERNAME** field, **123toll!**</span></span> <span data-ttu-id="6cdc3-427">hello에 **암호** 필드 및 **TollDataRefJoin** hello에 **테이블** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-427">in hello **PASSWORD** field, and **TollDataRefJoin** in hello **TABLE** field.</span></span>
   
    ![SQL Database 설정](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. <span data-ttu-id="6cdc3-429">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-429">Click **Create**.</span></span>

## <a name="azure-stream-analytics-query"></a><span data-ttu-id="6cdc3-430">Azure Stream Analytics 쿼리</span><span class="sxs-lookup"><span data-stu-id="6cdc3-430">Azure Stream analytics query</span></span>
<span data-ttu-id="6cdc3-431">hello **쿼리** 탭 hello 들어오는 데이터를 변환 하는 SQL 쿼리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-431">hello **QUERY** tab contains a SQL query that transforms hello incoming data.</span></span>

![쿼리 추가 toohello 쿼리 탭](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

<span data-ttu-id="6cdc3-433">이 자습서는 tooanswer tooprovide Azure 스트림 분석에에서 사용할 수 있는 tootoll 데이터와 구문 스트림 분석 쿼리 관련 된 여러 가지 비즈니스 질문 관련 응답을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-433">This tutorial attempts tooanswer several business questions that are related tootoll data and constructs Stream Analytics queries that can be used in Azure Stream Analytics tooprovide a relevant answer.</span></span>

<span data-ttu-id="6cdc3-434">첫 번째 스트림 분석 작업을 시작 하기 전에 몇 가지 시나리오와 hello 쿼리 구문을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-434">Before you start your first Stream Analytics job, let’s explore a few scenarios and hello query syntax.</span></span>

## <a name="introduction-tooazure-stream-analytics-query-language"></a><span data-ttu-id="6cdc3-435">소개 tooAzure 스트림 분석 쿼리 언어</span><span class="sxs-lookup"><span data-stu-id="6cdc3-435">Introduction tooAzure Stream Analytics query language</span></span>
- - -
<span data-ttu-id="6cdc3-436">Toocount hello 수가 차량이 요금 소 창구를 입력 해야 하는 경우를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-436">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="6cdc3-437">이벤트의 연속 스트림을 이기 때문에 있는 toodefine는 "기간 시간입니다."</span><span class="sxs-lookup"><span data-stu-id="6cdc3-437">Because this is a continuous stream of events, you have toodefine a “period of time.”</span></span> <span data-ttu-id="6cdc3-438">Hello 질문 toobe "개수 차량 입력 요금 소 창구 3 분 마다?"를 수정 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-438">Let's modify hello question toobe “How many vehicles enter a toll booth every three minutes?”.</span></span> <span data-ttu-id="6cdc3-439">이 일반적으로 참조 된 tooas hello count 텀블 링입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-439">This is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="6cdc3-440">이 질문에 응답 하는 hello Azure 스트림 분석 쿼리를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-440">Let’s look at hello Azure Stream Analytics query that answers this question:</span></span>

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

<span data-ttu-id="6cdc3-441">볼 수 있듯이 Azure 스트림 분석 쿼리 언어는 SQL 유사 하며 추가 하는 몇 가지 확장 toospecify 시간 관련 쿼리의 항목이 hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-441">As you can see, Azure Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="6cdc3-442">자세한 내용은 참고 [시간 관리](https://msdn.microsoft.com/library/azure/mt582045.aspx) 및 [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) MSDN에서 hello 쿼리에 사용 되는 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-442">For more details, read about [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

## <a name="testing-azure-stream-analytics-queries"></a><span data-ttu-id="6cdc3-443">Azure Stream Analytics 쿼리 테스트</span><span class="sxs-lookup"><span data-stu-id="6cdc3-443">Testing Azure Stream Analytics queries</span></span>
<span data-ttu-id="6cdc3-444">이제 첫 번째 Azure 스트림 분석 쿼리를 작성 한 경로 따라 hello에 TollApp 폴더에 있는 예제 데이터 파일을 사용 하 여 시간 tootest입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-444">Now that you have written your first Azure Stream Analytics query, it is time tootest it by using sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="6cdc3-445">**..\\TollApp\\TollApp\\Data**</span><span class="sxs-lookup"><span data-stu-id="6cdc3-445">**..\\TollApp\\TollApp\\Data**</span></span>

<span data-ttu-id="6cdc3-446">이 폴더는 hello를 다음 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-446">This folder contains hello following files:</span></span>

* <span data-ttu-id="6cdc3-447">Entry.json</span><span class="sxs-lookup"><span data-stu-id="6cdc3-447">Entry.json</span></span>
* <span data-ttu-id="6cdc3-448">Exit.json</span><span class="sxs-lookup"><span data-stu-id="6cdc3-448">Exit.json</span></span>
* <span data-ttu-id="6cdc3-449">registration.json</span><span class="sxs-lookup"><span data-stu-id="6cdc3-449">Registration.json</span></span>

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="6cdc3-450">질문 1: 요금 창구에 들어가는 차량 수</span><span class="sxs-lookup"><span data-stu-id="6cdc3-450">Question 1: Number of vehicles entering a toll booth</span></span>
1. <span data-ttu-id="6cdc3-451">Azure 포털 hello 및 이동 tooyour 만든 Azure 스트림 분석 작업을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-451">Open hello Azure portal and go tooyour created Azure Stream Analytics job.</span></span> <span data-ttu-id="6cdc3-452">Hello 클릭 **쿼리** 탭 하 고 hello 이전 섹션에서 쿼리를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-452">Click hello **QUERY** tab and paste query from hello previous section.</span></span>

2. <span data-ttu-id="6cdc3-453">toovalidate 기호 및 선택 샘플 데이터를 클릭 하 여 EntryStream 입력 hello에 hello 데이터 업로드에 대해이 쿼리... hello **파일에서 샘플 데이터 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-453">toovalidate this query against sample data, upload hello data into hello EntryStream input by clicking hello ... symbol and selecting **Upload sample data from file**.</span></span>

    ![Hello Entry.json 파일의 스크린 샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. <span data-ttu-id="6cdc3-455">로컬 컴퓨터와 클릭 선택 hello 파일 (Entry.json) 나타나는 hello 창에서 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-455">In hello pane that appears select hello file (Entry.json) on your local machine and click **OK**.</span></span> <span data-ttu-id="6cdc3-456">hello **테스트** 아이콘 이제 켜려면 되며 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-456">hello **Test** icon will now illuminate and be clickable.</span></span>
   
    ![Hello Entry.json 파일의 스크린 샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. <span data-ttu-id="6cdc3-458">Hello 쿼리의 hello 출력 예상 대로 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-458">Validate that hello output of hello query is as expected:</span></span>
   
    ![Hello 테스트의 결과](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-toopass-through-hello-toll-booth"></a><span data-ttu-id="6cdc3-460">보고서 2 질문: hello 요금 소 창구를 통해 각 자동차 toopass에 대 한 총 시간</span><span class="sxs-lookup"><span data-stu-id="6cdc3-460">Question 2: Report total time for each car toopass through hello toll booth</span></span>
<span data-ttu-id="6cdc3-461">hello 요금 소를 통해 자동차 toopass 하는 데 필요한 평균 시간 hello hello 프로세스 및 hello 고객 경험 tooassess hello 효율성을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-461">hello average time that's required for a car toopass through hello toll helps tooassess hello efficiency of hello process and hello customer experience.</span></span>

<span data-ttu-id="6cdc3-462">toofind hello 총 시간 hello ExitTime 스트림 사용 하 여 toojoin hello EntryTime 스트림이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-462">toofind hello total time, you need toojoin hello EntryTime stream with hello ExitTime stream.</span></span> <span data-ttu-id="6cdc3-463">Hello 스트림을 TollId 및 LicencePlate 열에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-463">You will join hello streams on TollId and LicencePlate columns.</span></span> <span data-ttu-id="6cdc3-464">hello **조인** 연산자는 hello 허용 가능한 시간 차이 hello 가입 이벤트를 설명 하는 임시 여유 toospecify 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-464">hello **JOIN** operator requires you toospecify temporal leeway that describes hello acceptable time difference between hello joined events.</span></span> <span data-ttu-id="6cdc3-465">사용 하 여 **DATEDIFF** 이벤트를 서로 15 분 이내 해야 함을 toospecify 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-465">You will use **DATEDIFF** function toospecify that events should be no more than 15 minutes from each other.</span></span> <span data-ttu-id="6cdc3-466">Hello도 적용 **DATEDIFF** 함수 tooexit 및 항목 toocompute hello 실제 시간을 자동차 hello에서 소비한 시간 스테이션에 전화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-466">You will also apply hello **DATEDIFF** function tooexit and entry times toocompute hello actual time that a car spends in hello toll station.</span></span> <span data-ttu-id="6cdc3-467">Hello 사용의 hello 차이가 **DATEDIFF** 에서 사용 하는 경우는 **선택** 문을 아닌 **조인** 조건.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-467">Note hello difference of hello use of **DATEDIFF** when it's used in a **SELECT** statement rather than a **JOIN** condition.</span></span>

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. <span data-ttu-id="6cdc3-468">tootest 업데이트 hello 쿼리 hello에이 쿼리 **쿼리** hello 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-468">tootest this query, update hello query on hello **QUERY** for hello job.</span></span> <span data-ttu-id="6cdc3-469">Hello 테스트 파일에 대 한 추가 **ExitStream** 마찬가지로 **EntryStream** 위에 입력 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-469">Add hello test file for **ExitStream** just like **EntryStream** was entered above.</span></span>
   
2. <span data-ttu-id="6cdc3-470">**테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-470">Click **Test**.</span></span>

3. <span data-ttu-id="6cdc3-471">Hello 확인란 tootest hello 쿼리 및 뷰 hello 출력을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-471">Select hello check box tootest hello query and view hello output:</span></span>
   
    ![Hello 테스트의 출력](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a><span data-ttu-id="6cdc3-473">질문 3: 등록 기간이 만료된 모든 화물 차량 보고</span><span class="sxs-lookup"><span data-stu-id="6cdc3-473">Question 3: Report all commercial vehicles with expired registration</span></span>
<span data-ttu-id="6cdc3-474">Azure 스트림 분석 데이터 toojoin의 정적 스냅숏 임시 데이터 스트림에 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-474">Azure Stream Analytics can use static snapshots of data toojoin with temporal data streams.</span></span> <span data-ttu-id="6cdc3-475">toodemonstrate이이 기능을 사용 하 여 hello 샘플 질문을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-475">toodemonstrate this capability, use hello following sample question.</span></span>

<span data-ttu-id="6cdc3-476">Hello 소 업체에 상용차 등록 될 검사를 위해 정차할 수 없이 hello 요금 소 창구를 통해 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-476">If a commercial vehicle is registered with hello toll company, it can pass through hello toll booth without being stopped for inspection.</span></span> <span data-ttu-id="6cdc3-477">상용차 등록 조회 테이블 tooidentify 등록 만료 된 모든 상용차를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-477">You will use Commercial Vehicle Registration lookup table tooidentify all commercial vehicles that have expired registrations.</span></span>

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

<span data-ttu-id="6cdc3-478">tootest 참조 데이터를 사용 하 여 쿼리를 이미 수행한 hello 참조 데이터에 대 한 입력된 소스 toodefine를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-478">tootest a query by using reference data, you need toodefine an input source for hello reference data, which you have done already.</span></span>

<span data-ttu-id="6cdc3-479">tootest 붙여넣기 hello 쿼리 hello로이 쿼리에서 **쿼리** 탭을 클릭 **테스트**, 샘플 데이터 및 클릭 hello 두 입력된 소스 및 hello 등록 지정 **테스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-479">tootest this query, paste hello query into hello **QUERY** tab, click **Test**, and specify hello two input sources and hello registration sample data and click **Test**.</span></span>  
   
![Hello 테스트의 출력](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-hello-stream-analytics-job"></a><span data-ttu-id="6cdc3-481">Hello 스트림 분석 작업 시작</span><span class="sxs-lookup"><span data-stu-id="6cdc3-481">Start hello Stream Analytics job</span></span>
<span data-ttu-id="6cdc3-482">이제 시간 toofinish hello 구성 및 시작 hello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-482">Now it's time toofinish hello configuration and start hello job.</span></span> <span data-ttu-id="6cdc3-483">일치 하는 항목 hello hello의 스키마는 출력을 생성 하는 질문 3 자에서 hello 쿼리 저장 **TollDataRefJoin** 출력 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-483">Save hello query from Question 3, which will produce output that matches hello schema of hello **TollDataRefJoin** output table.</span></span>

<span data-ttu-id="6cdc3-484">이동 toohello 작업 **대시보드**를 클릭 하 고 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-484">Go toohello job **DASHBOARD**, and click **START**.</span></span>

![Hello 작업 대시보드에 hello 시작 단추 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

<span data-ttu-id="6cdc3-486">Hello 대화 상자가 열리면 변경 hello **시작 출력** 너무 시간**사용자 지정 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-486">In hello dialog box that opens, change hello **START OUTPUT** time too**CUSTOM TIME**.</span></span> <span data-ttu-id="6cdc3-487">현재 시간 hello 하기 전에 hello 시간 tooone 시간을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-487">Change hello hour tooone hour before hello current time.</span></span> <span data-ttu-id="6cdc3-488">이러한 변경 하면 hello 이벤트 허브의 모든 이벤트 hello 자습서의 hello 시작 부분에서 toogenerate hello 이벤트를 시작한 이후에 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-488">This change ensures that all events from hello event hub are processed since you started toogenerate hello events at hello beginning of hello tutorial.</span></span> <span data-ttu-id="6cdc3-489">이제 hello 클릭 **시작** 단추 toostart hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-489">Now click hello **Start** button toostart hello job.</span></span>

![사용자 지정 시간 선택 항목](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

<span data-ttu-id="6cdc3-491">Hello 작업을 시작 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-491">Starting hello job can take a few minutes.</span></span> <span data-ttu-id="6cdc3-492">스트림 분석에 대 한 최상위 페이지 hello hello 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-492">You can see hello status on hello top-level page for Stream Analytics.</span></span>

![Hello 작업의 hello 상태 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a><span data-ttu-id="6cdc3-494">Visual Studio에서 결과 확인</span><span class="sxs-lookup"><span data-stu-id="6cdc3-494">Check results in Visual Studio</span></span>
1. <span data-ttu-id="6cdc3-495">Visual Studio 서버 탐색기를 열고 hello를 마우스 오른쪽 단추로 클릭 **TollDataRefJoin** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-495">Open Visual Studio Server Explorer, and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="6cdc3-496">클릭 **테이블 데이터 표시** 작업의 toosee hello 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-496">Click **Show Table Data** toosee hello output of your job.</span></span>
   
    ![서버 탐색기의 "테이블 데이터 표시" 선택 항목](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a><span data-ttu-id="6cdc3-498">Azure Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="6cdc3-498">Scale out Azure Stream Analytics jobs</span></span>
<span data-ttu-id="6cdc3-499">Azure 스트림 분석은 설계 된 많은 양의 데이터를 처리할 수 있도록 tooelastically의 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-499">Azure Stream Analytics is designed tooelastically scale so that it can handle a lot of data.</span></span> <span data-ttu-id="6cdc3-500">hello Azure 스트림 분석 쿼리를 사용할 수는 **PARTITION BY** 절 tootell hello 시스템이이 단계는 확장입니다. **PartitionId** hello 입력 (이벤트 허브)의 toomatch hello 파티션 ID를 추가 하는 시스템 hello 특수 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-500">hello Azure Stream Analytics query can use a **PARTITION BY** clause tootell hello system that this step will scale out. **PartitionId** is a special column that hello system adds toomatch hello partition ID of hello input (event hub).</span></span>

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. <span data-ttu-id="6cdc3-501">중지 hello 현재 작업을 hello에 업데이트 hello 쿼리 **쿼리** 탭을 선택한 열려 hello **설정** hello 작업 대시보드에 기어 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-501">Stop hello current job, update hello query in hello **QUERY** tab, and open hello **Settings** gear in hello job dashboard.</span></span> <span data-ttu-id="6cdc3-502">**크기 조정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-502">Click **Scale**.</span></span>
   
    <span data-ttu-id="6cdc3-503">**스트리밍 단위** 정의 hello 양을 작업 hello 계산 능력을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-503">**STREAMING UNITS** define hello amount of compute power that hello job can receive.</span></span>
2. <span data-ttu-id="6cdc3-504">변경 hello 드롭 다운 6에서 1에서입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-504">Change hello drop down from 1 from 6.</span></span>
   
    ![6개의 스트리밍 단위를 선택하는 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. <span data-ttu-id="6cdc3-506">Toohello 이동 **출력** 탭 하 고 hello SQL 테이블의 hello 이름을 너무 변경**TollDataTumblingCountPartitioned**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-506">Go toohello **OUTPUTS** tab and change hello name of hello SQL table too**TollDataTumblingCountPartitioned**.</span></span>

<span data-ttu-id="6cdc3-507">Hello 작업을 시작할 이제 Azure 스트림 분석 더 많은 컴퓨팅 리소스 간에 작업을 분산 하 고 처리량을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-507">If you start hello job now, Azure Stream Analytics can distribute work across more compute resources and achieve better throughput.</span></span> <span data-ttu-id="6cdc3-508">해당 hello TollApp 응용 프로그램 TollId로 분할 하는 이벤트를 보내는 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-508">Please note that hello TollApp application is also sending events partitioned by TollId.</span></span>

## <a name="monitor"></a><span data-ttu-id="6cdc3-509">모니터</span><span class="sxs-lookup"><span data-stu-id="6cdc3-509">Monitor</span></span>
<span data-ttu-id="6cdc3-510">hello **모니터** 영역 작업을 실행 하는 hello에 대 한 통계를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-510">hello **MONITOR** area contains statistics about hello running job.</span></span> <span data-ttu-id="6cdc3-511">구성은 처음으로 필요한 hello에 toouse hello 저장소 계정이 동일한 지역 (이 문서의 나머지 부분 hello와 같은 이름 유료).</span><span class="sxs-lookup"><span data-stu-id="6cdc3-511">First time configuration is needed toouse hello storage account in hello same region (name toll like hello rest of this document).</span></span>   

![모니터링 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

<span data-ttu-id="6cdc3-513">에 액세스할 수 있습니다 **활동 로그** hello 작업 대시보드에서 **설정을** 영역도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-513">You can access **Activity Logs** from hello job dashboard **Settings** area as well.</span></span>


## <a name="conclusion"></a><span data-ttu-id="6cdc3-514">결론</span><span class="sxs-lookup"><span data-stu-id="6cdc3-514">Conclusion</span></span>
<span data-ttu-id="6cdc3-515">이 자습서에서는 Azure 스트림 분석 서비스를 toohello 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-515">This tutorial introduced you toohello Azure Stream Analytics service.</span></span> <span data-ttu-id="6cdc3-516">그 tooconfigure 입력 및 출력을 스트림 분석 작업 hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-516">It demonstrated how tooconfigure inputs and outputs for hello Stream Analytics job.</span></span> <span data-ttu-id="6cdc3-517">Hello 자습서 hello 요금 데이터 시나리오를 사용 하 여 일반적인 유형의 동작 및 해결 방법에서 Azure 스트림 분석에서 간단한 SQL과 비슷한 쿼리를 사용 하 여 데이터의 hello 공간에서 발생 하는 문제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-517">Using hello Toll Data scenario, hello tutorial explained common types of problems that arise in hello space of data in motion and how they can be solved with simple SQL-like queries in Azure Stream Analytics.</span></span> <span data-ttu-id="6cdc3-518">hello 자습서 임시 데이터로 작업 하기 위한 SQL 확장 구문을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-518">hello tutorial described SQL extension constructs for working with temporal data.</span></span> <span data-ttu-id="6cdc3-519">어떻게 toojoin 데이터 스트림, 정적 참조 데이터로 tooenrich hello 데이터 스트림 방법 등에 대해 알아보았습니다 tooscale 쿼리 tooachieve 더 높은 처리량 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-519">It showed how toojoin data streams, how tooenrich hello data stream with static reference data, and how tooscale out a query tooachieve higher throughput.</span></span>

<span data-ttu-id="6cdc3-520">이 자습서가 개요에 해당하는 내용을 잘 소개하고는 있지만 완전하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-520">Although this tutorial provides a good introduction, it is not complete by any means.</span></span> <span data-ttu-id="6cdc3-521">Hello SAQL 언어에서 사용 하 여 더 많은 쿼리 패턴을 찾을 수 있습니다 [일반적인 스트림 분석 사용 패턴에 대 한 예제 쿼리](stream-analytics-stream-analytics-query-patterns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-521">You can find more query patterns using hello SAQL language at [Query examples for common Stream Analytics usage patterns](stream-analytics-stream-analytics-query-patterns.md).</span></span>
<span data-ttu-id="6cdc3-522">Toohello 참조 [온라인 설명서](https://azure.microsoft.com/documentation/services/stream-analytics/) toolearn Azure 스트림 분석에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-522">Refer toohello [online documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) toolearn more about Azure Stream Analytics.</span></span>

## <a name="clean-up-your-azure-account"></a><span data-ttu-id="6cdc3-523">Azure 계정 정리</span><span class="sxs-lookup"><span data-stu-id="6cdc3-523">Clean up your Azure account</span></span>
1. <span data-ttu-id="6cdc3-524">Hello Azure 포털의에서 hello 스트림 분석 작업을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-524">Stop hello Stream Analytics job in hello Azure portal.</span></span>
   
    <span data-ttu-id="6cdc3-525">hello Setup.ps1 스크립트는 두 개의 이벤트 허브 및 SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-525">hello Setup.ps1 script creates two event hubs and a SQL database.</span></span> <span data-ttu-id="6cdc3-526">hello 지침 도움말 hello 자습서의 hello 끝에 리소스를 정리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-526">hello following instructions help you clean up resources at hello end of hello tutorial.</span></span>
2. <span data-ttu-id="6cdc3-527">PowerShell 창에 입력 **.\\ Cleanup.ps1** hello 자습서에 사용 되는 리소스를 삭제 하는 toostart hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-527">In a PowerShell window, type **.\\Cleanup.ps1** toostart hello script that deletes resources used in hello tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6cdc3-528">리소스는 hello 이름으로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-528">Resources are identified by hello name.</span></span> <span data-ttu-id="6cdc3-529">제거를 확인하기 전에 각 항목을 신중하게 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc3-529">Make sure you carefully review each item before confirming removal.</span></span>
   > 
   > 


