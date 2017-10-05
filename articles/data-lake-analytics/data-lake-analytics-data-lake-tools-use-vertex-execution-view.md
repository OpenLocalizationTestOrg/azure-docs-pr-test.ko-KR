---
title: "Data Lake Tools for Visual Studio에서 Vertex Execution View 사용 | Microsoft 문서"
description: "Data Lake Analytics 작업을 검사하기 위해 Vertex Execution View를 사용하는 방법을 알아봅니다."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: b788e7bc8ded86ebd49cc0be73e5b4e1bcbeaba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="a4129-103">Visual Studio용 Data Lake Tools의 Vertex Execution View 사용</span><span class="sxs-lookup"><span data-stu-id="a4129-103">Use the Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="a4129-104">Data Lake Analytics 작업을 검사하기 위해 Vertex Execution View를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-104">Learn how to use the Vertex Execution View to exam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4129-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a4129-105">Prerequisites</span></span>

<span data-ttu-id="a4129-106">Data Lake Tools for Visual Studio를 사용한 U-SQL 스크립트 개발에 대한 기본 지식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-106">You need basic knowledge of using Data Lake Tools for Visual Studio to develop U-SQL script.</span></span>  <span data-ttu-id="a4129-107">[자습서: Visual Studio용 Data Lake Tools를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4129-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-the-vertex-execution-view"></a><span data-ttu-id="a4129-108">Vertex Execution View 열기</span><span class="sxs-lookup"><span data-stu-id="a4129-108">Open the Vertex Execution View</span></span>
<span data-ttu-id="a4129-109">Data Lake Tools for Visual Studio에서 U-SQL 작업을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="a4129-110">왼쪽 아래 모서리에서 **Vertex Execution View**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-110">Click **Vertex Execution View** in the bottom left corner.</span></span> <span data-ttu-id="a4129-111">먼저 프로필을 로드하라는 메시지가 나타날 것이며 네트워크 연결 상태에 따라 약간의 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-111">You may be prompted to load profiles first and it can take some time depending on your network connectivity.</span></span>

![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="a4129-113">Vertex Execution View 이해</span><span class="sxs-lookup"><span data-stu-id="a4129-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="a4129-114">Vertex Execution View는 다음 세 가지로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-114">The Vertex Execution View has three parts:</span></span>

![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="a4129-116">왼쪽의 **꼭짓점 선택기**를 통해 기능별로(예: 상위 데이터 10개 읽기, 또는 단계별 선택) 꼭짓점을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-116">The **Vertex selector** on the left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="a4129-117">가장 일반적으로 사용되는 필터 중 하나는 **중요 경로 상의 꼭짓점**을 보는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-117">One of the most commonly-used filters is to see the **vertices on critical path**.</span></span> <span data-ttu-id="a4129-118">**중요 경로**는 U-SQL 작업의 꼭짓점 중에서 가장 긴 체인입니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-118">The **Critical path** is the longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="a4129-119">중요 경로를 이해하는 것은 어떤 꼭짓점이 가장 긴 시간이 걸리는지 확인하여 작업을 최적화하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-119">Understanding the critical path is useful for optimizing your jobs by checking which vertex takes the longest time.</span></span>
  
![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="a4129-121">위쪽 가운데 창은 **모든 꼭짓점의 실행 상태**를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-121">The top center pane shows the **running status of all the vertices**.</span></span>
  
![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="a4129-123">아래쪽 가운데 창은 각 꼭짓점에 대한 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-123">The bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="a4129-124">프로세스 이름: 꼭짓점 인스턴스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-124">Process Name: The name of the vertex instance.</span></span> <span data-ttu-id="a4129-125">StageName|VertexName|VertexRunInstance의 다른 부분들로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="a4129-126">예를 들어, SV7_Split[62].v1 꼭짓점은 Stage SV7_Split에서 Vertex 번호 62번의 두 번째 실행 인스턴스(v1, 인덱스는 0부터 시작됨)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-126">For example, the SV7_Split[62].v1 vertex stands for the second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="a4129-127">총 읽기/쓰기 데이터: 이 꼭짓점에서 읽기/쓰기를 수행한 데이터 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-127">Total Data Read/Written: The data was read/written by this vertex.</span></span>
* <span data-ttu-id="a4129-128">시스템 상태/종료 상태: 꼭짓점이 끝났을 때의 최종 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-128">State/Exit Status: The final status when the vertex is ended.</span></span>
* <span data-ttu-id="a4129-129">종료 코드/오류 유형: 꼭짓점이 실패했을 때의 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-129">Exit Code/Failure Type: The error when the vertex failed.</span></span>
* <span data-ttu-id="a4129-130">생성 이유: 꼭짓점이 만들어진 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-130">Creation Reason: Why the vertex was created.</span></span>
* <span data-ttu-id="a4129-131">리소스 대기 시간/프로세스 대기 시간/PN 큐 대기 시간: 꼭짓점이 리소스를 기다리는 데, 데이터를 처리하는 데, 큐에서 기다리는 데 걸리는 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-131">Resource Latency/Process Latency/PN Queue Latency: the time taken for the vertex to wait for resources, to process data, and to stay in the queue.</span></span>
* <span data-ttu-id="a4129-132">프로세스/작성자 GUID:.현재 실행 중인 꼭짓점 또는 작성자에 대한 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-132">Process/Creator GUID: GUID for the current running vertex or its creator.</span></span>
* <span data-ttu-id="a4129-133">버전: 실행 중인 버전의 N번째 인스턴스(시스템은 장애 조치, 컴퓨터 중복 등과 같은 여러 이유로 꼭짓점의 새 인스턴스 일정을 잡을 수도 있습니다)</span><span class="sxs-lookup"><span data-stu-id="a4129-133">Version: the N-th instance of the running vertex (the system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="a4129-134">버전이 만들어진 시간.</span><span class="sxs-lookup"><span data-stu-id="a4129-134">Version Created Time.</span></span>
* <span data-ttu-id="a4129-135">프로세스 만들기 시작 시간/프로세스 대기 중인 시간/프로세스 시작 시간/프로세스 완료 시간: 꼭짓점 프로세스가 만들기를 시작한 때, 꼭짓점 프로세스가 큐에 대기하기 시작한 때, 특정 꼭짓점 프로세스가 시작한 때, 특정 꼭짓점 프로세스가 완료된 때를 각기 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a4129-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when the vertex process starts creation; when the vertex process starts to queue; when the certain vertex process starts; when the certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4129-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4129-136">Next steps</span></span>
* <span data-ttu-id="a4129-137">진단 정보를 기록하려면 [Azure Data Lake Analytics에 대한 진단 로그에 액세스](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="a4129-137">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="a4129-138">더 복잡한 쿼리를 보려면 [Azure Data Lake Analytics을 사용하여 웹 사이트 로그 분석](data-lake-analytics-analyze-weblogs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4129-138">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="a4129-139">작업 세부 정보를 보려면, [Azure Data lake Analytics 작업에 대한 작업 브라우저 및 작업 보기 사용하기](data-lake-analytics-data-lake-tools-view-jobs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4129-139">To view job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
