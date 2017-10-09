---
title: "Azure IoT Suite aaaCustomize 연결 팩터리 | Microsoft Docs"
description: "Hello의 toocustomize hello 동작 팩터리를 연결 하는 방법에 대 한 설명을 미리 솔루션을 구성 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="2fd70-103">Hello OPC UA는 서버에서 데이터를 표시 팩터리 솔루션에 연결 하는 방법을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="2fd70-103">Customize how hello connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="2fd70-104">소개</span><span class="sxs-lookup"><span data-stu-id="2fd70-104">Introduction</span></span>

<span data-ttu-id="2fd70-105">hello 연결 된 팩터리 솔루션 집계 하 고 hello OPC UA 서버 연결 된 toohello 솔루션의에서 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-105">hello connected factory solution aggregates and displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="2fd70-106">찾아볼 수 있으며 명령을 toohello OPC UA 서버 솔루션에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-106">You can browse and send commands toohello OPC UA servers in your solution.</span></span> <span data-ttu-id="2fd70-107">OPC UA에 대 한 자세한 내용은 참조 hello [팩터리 FAQ 연결](iot-suite-faq-cf.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-107">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="2fd70-108">Hello 솔루션의 집계 된 데이터의 예로 전체 장비 효율성 (OEE) hello 및 hello 팩터리, 선 및 스테이션 수준에서 hello 대시보드에서 볼 수 있는 핵심 성과 지표 (Kpi)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-108">Examples of aggregated data in hello solution include hello Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in hello dashboard at hello factory, line, and station levels.</span></span> <span data-ttu-id="2fd70-109">hello 다음 스크린샷은 hello에 대 한 hello OEE 및 KPI 값 **어셈블리** 스테이션에 **생산 라인 1**, hello에 **뮌헨** 팩터리:</span><span class="sxs-lookup"><span data-stu-id="2fd70-109">hello following screenshot shows hello OEE and KPI values for hello **Assembly** station, on **Production line 1**, in hello **Munich** factory:</span></span>

![Hello 솔루션에서 OEE 및 KPI 값의 예][img-oee-kpi]

<span data-ttu-id="2fd70-111">hello 솔루션 사용 하면 tooview 세부 정보에서 특정 데이터 항목에서 hello 서버 OPC UA 함 *스테이션*합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-111">hello solution enables you tooview detailed information from specific data items from hello OPC UA servers, called *stations*.</span></span> <span data-ttu-id="2fd70-112">hello 다음 스크린샷은 차트가 hello 특정 스테이션에서 제조 된 항목 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="2fd70-112">hello following screenshot shows plots of hello number of manufactured items from a specific station:</span></span>

![제조된 항목 수 그림][img-manufactured-items]

<span data-ttu-id="2fd70-114">Hello 그래프 중 하나를 클릭 하는 경우에 hello 데이터 시간 시계열 Insights (TSI)를 사용 하 여 자세히 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-114">If you click one of hello graphs, you can explore hello data further using Time Series Insights (TSI):</span></span>

![Time Series Insights를 사용하여 데이터 탐색][img-tsi]

<span data-ttu-id="2fd70-116">이 문서에서는 다음을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-116">This article describes:</span></span>

- <span data-ttu-id="2fd70-117">어떻게 hello 데이터 toohello 사용할 수 있는 다양 한 보기를에서 이루어집니다 hello 솔루션.</span><span class="sxs-lookup"><span data-stu-id="2fd70-117">How hello data is made available toohello various views in hello solution.</span></span>
- <span data-ttu-id="2fd70-118">Hello 방식으로 hello 솔루션 사용자 지정할 수 hello 데이터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-118">How you can customize hello way hello solution displays hello data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="2fd70-119">데이터 원본</span><span class="sxs-lookup"><span data-stu-id="2fd70-119">Data sources</span></span>

<span data-ttu-id="2fd70-120">hello 연결 된 팩터리 솔루션 hello OPC UA 연결 된 서버 toohello 솔루션에서에서 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-120">hello connected factory solution displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="2fd70-121">hello 기본 설치는 공장 시뮬레이션을 실행 하는 여러 OPC UA 서버를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-121">hello default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="2fd70-122">사용자 고유의 OPC UA 서버를 추가할 수 있는 [게이트웨이 통해 연결] [ lnk-connect-cf] tooyour 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] tooyour solution.</span></span>

<span data-ttu-id="2fd70-123">연결된 된 OPC UA 서버 hello 대시보드에 tooyour 솔루션을 보낼 수 있음을 hello 데이터 항목을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-123">You can browse hello data items that a connected OPC UA server can send tooyour solution in hello dashboard:</span></span>

1. <span data-ttu-id="2fd70-124">Toohello 이동 **OPC UA 서버 선택** 보기:</span><span class="sxs-lookup"><span data-stu-id="2fd70-124">Navigate toohello **Select an OPC UA server** view:</span></span>

    ![탐색 toohello OPC UA 서버 뷰 선택][img-select-server]

1. <span data-ttu-id="2fd70-126">서버를 선택하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="2fd70-127">클릭 **진행** 때 hello 보안 경고가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-127">Click **Proceed** when hello security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2fd70-128">이 경고는만 각 서버에 대해 한 번만 표시 하며 hello 솔루션 대시보드와 hello 서버 간에 트러스트 관계를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-128">This warning only appears once for each server and establishes a trust relationship between hello solution dashboard and hello server.</span></span>

1. <span data-ttu-id="2fd70-129">서버 hello 찾아보기 hello 데이터 항목 toohello 솔루션을 보낼 수 이제 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-129">You can now browse hello data items that hello server can send toohello solution.</span></span> <span data-ttu-id="2fd70-130">Toohello 솔루션 전송 된 항목은 녹색 확인 표시:</span><span class="sxs-lookup"><span data-stu-id="2fd70-130">Items that are being sent toohello solution have a green check mark:</span></span>

    ![게시된 항목][img-published]

1. <span data-ttu-id="2fd70-132">있다면는 *관리자* hello 솔루션을 선택할 수 있습니다 toopublish 데이터 항목 toomake hello에서 사용할 수 있는 공장 솔루션 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-132">If you are an *Administrator* in hello solution, you can choose toopublish a data item toomake it available in hello connected factory solution.</span></span> <span data-ttu-id="2fd70-133">관리자는 데이터 항목의 hello 값을 변경 하 고 hello OPC UA 서버에서에서 메서드를 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-133">As an Administrator, you can also change hello value of data items and call methods in hello OPC UA server.</span></span>

## <a name="map-hello-data"></a><span data-ttu-id="2fd70-134">Hello 데이터 매핑</span><span class="sxs-lookup"><span data-stu-id="2fd70-134">Map hello data</span></span>

<span data-ttu-id="2fd70-135">hello 팩터리 솔루션 지도 연결 하 고 집계 hello 게시 된 데이터 항목 hello OPC UA 서버 toohello에서에서 다양 한 뷰 hello 솔루션에서 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-135">hello connected factory solution maps and aggregates hello published data items from hello OPC UA server toohello various views in hello solution.</span></span> <span data-ttu-id="2fd70-136">hello 연결 된 팩터리 솔루션 배포 tooyour Azure 계정 hello 솔루션을 프로 비전 할 때 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-136">hello connected factory solution deploys tooyour Azure account when you provision hello solution.</span></span> <span data-ttu-id="2fd70-137">JSON 파일에 연결 하는 Visual Studio 팩터리 솔루션 hello이 매핑 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-137">A JSON file in hello Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="2fd70-138">보고 및 hello 연결 된 팩터리 Visual Studio 솔루션에서에서이 JSON 구성 파일을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-138">You can view and modify this JSON configuration file in hello connected factory Visual Studio solution.</span></span> <span data-ttu-id="2fd70-139">변경을 수행한 후 hello 솔루션을 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-139">You can redeploy hello solution after you make a change.</span></span>

<span data-ttu-id="2fd70-140">Hello 구성 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-140">You can use hello configuration file to:</span></span>

- <span data-ttu-id="2fd70-141">Hello 기존 시뮬레이션 된 팩터리, 생산 라인 및 스테이션을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-141">Edit hello existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="2fd70-142">Toohello 솔루션을 연결 하는 실제 OPC UA 서버에서 데이터를 매핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="2fd70-142">Map data from real OPC UA servers that you connect toohello solution.</span></span>

<span data-ttu-id="2fd70-143">tooclone hello의 복사본을 공장 Visual Studio 솔루션을 사용 하 여 hello 다음 git 명령을 연결:</span><span class="sxs-lookup"><span data-stu-id="2fd70-143">tooclone a copy of hello connected factory Visual Studio solution, use hello following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="2fd70-144">hello 파일 **ContosoTopologyDescription.json** hello hello OPC UA 서버 데이터에서에서 매핑 hello 연결 된 팩터리 솔루션 대시보드에 항목 toohello 뷰를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-144">hello file **ContosoTopologyDescription.json** defines hello mapping from hello OPC UA server data items toohello views in hello connected factory solution dashboard.</span></span> <span data-ttu-id="2fd70-145">Hello에서이 구성 파일을 찾을 수 있습니다 **Contoso\Topology** 폴더 hello에 **WebApp** hello Visual Studio 솔루션에서에서 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="2fd70-145">You can find this configuration file in hello **Contoso\Topology** folder in hello **WebApp** project in hello Visual Studio solution.</span></span>

<span data-ttu-id="2fd70-146">hello JSON 파일의 내용은 hello 팩터리, 생산 라인 및 스테이션 노드 계층으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-146">hello content of hello JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="2fd70-147">이 계층 구조는 hello 연결 된 팩터리 대시보드에 hello 탐색 계층 구조를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-147">This hierarchy defines hello navigation hierarchy in hello connected factory dashboard.</span></span> <span data-ttu-id="2fd70-148">Hello 계층의 각 노드에서 값 hello 대시보드에 표시 되는 hello 정보를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-148">Values at each node of hello hierarchy determine hello information displayed in hello dashboard.</span></span> <span data-ttu-id="2fd70-149">예를 들어 hello JSON 파일에는 hello를 다음 뮌헨 팩터리 hello에 대 한 값에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-149">For example, hello JSON file contains hello following values for hello Munich factory:</span></span>

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

<span data-ttu-id="2fd70-150">hello 이름, 설명 및 위치 hello 대시보드에서이 보기에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-150">hello name, description, and location appear on this view in hello dashboard:</span></span>

![Hello 대시보드에 뮌헨 데이터][img-munich]

<span data-ttu-id="2fd70-152">각 공장, 생산 라인 및 스테이션에는 이미지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="2fd70-153">Hello에서 이러한 JPEG 파일을 찾을 수 있습니다 **Content\img** 폴더 hello에 **WebApp** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="2fd70-153">You can find these JPEG files in hello **Content\img** folder in hello **WebApp** project.</span></span> <span data-ttu-id="2fd70-154">이러한 이미지 파일 hello 연결 된 팩터리 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-154">These image files display in hello connected factory dashboard.</span></span>

<span data-ttu-id="2fd70-155">각 스테이션 hello OPC UA에서에서 데이터 항목의 매핑 hello를 정의 하는 몇 가지 자세한 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-155">Each station includes several detailed properties that define hello mapping from hello OPC UA data items.</span></span> <span data-ttu-id="2fd70-156">이러한 속성은 hello 다음 섹션에에서 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-156">These properties are described in hello following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="2fd70-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="2fd70-157">OpcUri</span></span>

<span data-ttu-id="2fd70-158">hello **OpcUri** 는 hello OPC UA 응용 프로그램 URI hello OPC UA 서버를 고유 하 게 식별 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-158">hello **OpcUri** value is hello OPC UA Application URI that uniquely identifies hello OPC UA server.</span></span> <span data-ttu-id="2fd70-159">예를 들어 hello **OpcUri** hello 어셈블리 스테이션 뮌헨에 생산 라인 1에서 다음과 같은 hello에 대 한 값: **urn: scada2194:ua:munich:productionline0:assemblystation**합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-159">For example, hello **OpcUri** value for hello assembly station on production line 1 in Munich looks like hello following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="2fd70-160">Uri의 연결 된 hello OPC UA 서버 hello hello 솔루션 대시보드에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-160">You can view hello URIs of hello connected OPC UA servers in hello solution dashboard:</span></span>

![OPC UA 서버 URI 보기][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="2fd70-162">시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="2fd70-162">Simulation</span></span>

<span data-ttu-id="2fd70-163">hello에 대 한 정보를 hello **시뮬레이션** 노드는 특정 toohello 기본적으로 프로 비전 되는 OPC UA 서버 hello에서 실행 되는 OPC UA 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-163">hello information in hello **Simulation** node is specific toohello OPC UA simulation that runs in hello OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="2fd70-164">실제 OPC UA 서버에는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="2fd70-165">Kpi1 및 Kpi2</span><span class="sxs-lookup"><span data-stu-id="2fd70-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="2fd70-166">이러한 노드는 hello 스테이션에서 데이터 hello 대시보드에 toohello 두 KPI 값을 제공 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-166">These nodes describe how data from hello station contributes toohello two KPI values in hello dashboard.</span></span> <span data-ttu-id="2fd70-167">기본 배포에서 이러한 KPI 값은 시간당 단위 및 시간당 kWh입니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="2fd70-168">스테이션의 hello 수준에서 KPI 값을 계산 하 고 hello 생산 라인 및 팩터리 수준에서이 집계 하는 hello 솔루션.</span><span class="sxs-lookup"><span data-stu-id="2fd70-168">hello solution calculates KPI vales at hello level of a station and aggregates them at hello production line and factory levels.</span></span>

<span data-ttu-id="2fd70-169">각 KPI에는 최소값, 최대값 및 대상 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="2fd70-170">각 KPI 값 팩터리 솔루션 tooperform 연결 hello에 대 한 경고 작업 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-170">Each KPI value can also define alert actions for hello connected factory solution tooperform.</span></span> <span data-ttu-id="2fd70-171">hello 다음 코드 조각 정의 보여 줍니다 hello KPI hello 어셈블리 스테이션에 대 한 생산 라인 뮌헨에 1에서:</span><span class="sxs-lookup"><span data-stu-id="2fd70-171">hello following snippet shows hello KPI definitions for hello assembly station on production line 1 in Munich:</span></span>

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

<span data-ttu-id="2fd70-172">hello 다음 스크린샷은 hello KPI 데이터 hello 대시보드에.</span><span class="sxs-lookup"><span data-stu-id="2fd70-172">hello following screenshot shows hello KPI data in hello dashboard.</span></span>

![Hello 대시보드에서 KPI 정보][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="2fd70-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="2fd70-174">OpcNodes</span></span>

<span data-ttu-id="2fd70-175">hello **OpcNodes** 노드 식별 hello hello OPC UA 서버에서에서 게시 된 데이터 항목 및 지정 방법을 tooprocess 해당 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-175">hello **OpcNodes** nodes identify hello published data items from hello OPC UA server and specify how tooprocess that data.</span></span>

<span data-ttu-id="2fd70-176">hello **NodeId** 값 식별 hello hello OPC UA 서버에서에서 특정 OPC UA NodeID 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-176">hello **NodeId** value identifies hello specific OPC UA NodeID from hello OPC UA server.</span></span> <span data-ttu-id="2fd70-177">hello hello 어셈블리 스테이션에서 생산 라인 뮌헨에 1의 첫 번째 노드 값이 **ns = 2; i = 385**합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-177">hello first node in hello assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="2fd70-178">A **NodeId** 값 지정 OPC UA 서버 hello 및 hello에서 데이터 항목 tooread hello **심볼 이름** 해당 데이터에 대 한 hello 대시보드에 친숙 한 이름 toouse를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-178">A **NodeId** value specifies hello data item tooread from hello OPC UA server, and hello **SymbolicName** provides a user-friendly name toouse in hello dashboard for that data.</span></span>

<span data-ttu-id="2fd70-179">각 노드에 연결 된 다른 값은 다음 표에 hello에 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-179">Other values associated with each node are summarized in hello following table:</span></span>

| <span data-ttu-id="2fd70-180">값</span><span class="sxs-lookup"><span data-stu-id="2fd70-180">Value</span></span> | <span data-ttu-id="2fd70-181">설명</span><span class="sxs-lookup"><span data-stu-id="2fd70-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2fd70-182">관련성</span><span class="sxs-lookup"><span data-stu-id="2fd70-182">Relevance</span></span>  | <span data-ttu-id="2fd70-183">hello KPI 및 OEE 값이이 데이터에 기여합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-183">hello KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="2fd70-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="2fd70-184">OpCode</span></span>     | <span data-ttu-id="2fd70-185">어떻게 hello 데이터가 집계 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-185">How hello data is aggregated.</span></span> |
| <span data-ttu-id="2fd70-186">Units</span><span class="sxs-lookup"><span data-stu-id="2fd70-186">Units</span></span>      | <span data-ttu-id="2fd70-187">hello 대시보드에 hello 단위 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-187">hello units toouse in hello dashboard.</span></span>  |
| <span data-ttu-id="2fd70-188">Visible</span><span class="sxs-lookup"><span data-stu-id="2fd70-188">Visible</span></span>    | <span data-ttu-id="2fd70-189">여부 toodisplay이 값에 hello 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-189">Whether toodisplay this value in hello dashboard.</span></span> <span data-ttu-id="2fd70-190">일부 값은 계산에 사용되지만 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="2fd70-191">최대</span><span class="sxs-lookup"><span data-stu-id="2fd70-191">Maximum</span></span>    | <span data-ttu-id="2fd70-192">hello 대시보드에 경고를 트리거하는 최대 값 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-192">hello maximum value that triggers an alert in hello dashboard.</span></span> |
| <span data-ttu-id="2fd70-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="2fd70-193">MaximumAlertActions</span></span> | <span data-ttu-id="2fd70-194">응답 tooan 경고에서 작업 tootake 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-194">An action tootake in response tooan alert.</span></span> <span data-ttu-id="2fd70-195">예를 들어, 명령 tooa 스테이션을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-195">For example, send a command tooa station.</span></span> |
| <span data-ttu-id="2fd70-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="2fd70-196">ConstValue</span></span> | <span data-ttu-id="2fd70-197">계산에서 사용되는 상수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-hello-changes"></a><span data-ttu-id="2fd70-198">Hello 변경 내용을 배포합니다</span><span class="sxs-lookup"><span data-stu-id="2fd70-198">Deploy hello changes</span></span>

<span data-ttu-id="2fd70-199">변경 내용을 toohello 만들기 완료 했을 때 **ContosoTopologyDescription.json** 파일을 다시 배포 해야 hello 팩터리 솔루션 tooyour Azure 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-199">When you have finished making changes toohello **ContosoTopologyDescription.json** file, you must redeploy hello connected factory solution tooyour Azure account.</span></span>

<span data-ttu-id="2fd70-200">hello **azure iot-연결-공장** 저장소에 포함 되어는 **build.ps1** PowerShell 스크립트 toorebuild를 사용 하 고 hello 솔루션을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd70-200">hello **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use toorebuild and deploy hello solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fd70-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2fd70-201">Next Steps</span></span>

<span data-ttu-id="2fd70-202">자세한 정보 hello 연결 된 팩터리 미리 구성 된 솔루션에 대 한 다음 문서를 읽는 hello 여:</span><span class="sxs-lookup"><span data-stu-id="2fd70-202">Learn more about hello connected factory preconfigured solution by reading hello following articles:</span></span>

* <span data-ttu-id="2fd70-203">[연결된 공장 미리 구성된 솔루션 연습][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="2fd70-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="2fd70-204">[연결된 공장에 대한 게이트웨이 배포][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="2fd70-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="2fd70-205">[Hello azureiotsuite.com 사이트에 대 한 권한][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="2fd70-205">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="2fd70-206">연결된 팩터리 FAQ</span><span class="sxs-lookup"><span data-stu-id="2fd70-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="2fd70-207">[FAQ][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="2fd70-207">[FAQ][lnk-faq]</span></span>


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md