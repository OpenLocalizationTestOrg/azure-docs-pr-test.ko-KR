---
title: "데이터 레이크 Tools for Visual Studio에서에서 꼭 짓 점 실행 보기 aaaUse hello | Microsoft Docs"
description: "어떻게 toouse hello 꼭 짓 점 실행 보기 tooexam Data Lake 분석 작업에 알아봅니다."
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
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="0043e-103">데이터 레이크 도구에서 꼭 짓 점 실행 보기 hello를 사용 하 여 Visual Studio에 대 한</span><span class="sxs-lookup"><span data-stu-id="0043e-103">Use hello Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="0043e-104">어떻게 toouse hello 꼭 짓 점 실행 보기 tooexam Data Lake 분석 작업에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-104">Learn how toouse hello Vertex Execution View tooexam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0043e-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0043e-105">Prerequisites</span></span>

<span data-ttu-id="0043e-106">데이터 레이크 도구를 사용 하 여 Visual Studio toodevelop U-SQL 스크립트에 대 한 기본 지식이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-106">You need basic knowledge of using Data Lake Tools for Visual Studio toodevelop U-SQL script.</span></span>  <span data-ttu-id="0043e-107">[자습서: Visual Studio용 Data Lake Tools를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0043e-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-hello-vertex-execution-view"></a><span data-ttu-id="0043e-108">Hello 꼭 짓 점 실행 보기를 열려면</span><span class="sxs-lookup"><span data-stu-id="0043e-108">Open hello Vertex Execution View</span></span>
<span data-ttu-id="0043e-109">Data Lake Tools for Visual Studio에서 U-SQL 작업을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="0043e-110">클릭 **꼭 짓 점 실행 보기** hello 하단 왼쪽된 모서리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-110">Click **Vertex Execution View** in hello bottom left corner.</span></span> <span data-ttu-id="0043e-111">먼저 증명된 tooload 프로필 일 수 있습니다 및 네트워크 연결에 따라 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-111">You may be prompted tooload profiles first and it can take some time depending on your network connectivity.</span></span>

![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="0043e-113">Vertex Execution View 이해</span><span class="sxs-lookup"><span data-stu-id="0043e-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="0043e-114">hello 꼭 짓 점 실행 보기는 세 가지 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-114">hello Vertex Execution View has three parts:</span></span>

![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="0043e-116">hello **꼭 짓 점 선택기** hello 왼쪽된 있습니다 (예: 상위 10 개 데이터 읽기, 또는 단계에서 선택할) 기능을 통해 꼭 짓 점을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-116">hello **Vertex selector** on hello left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="0043e-117">Hello 가장 일반적으로 사용 되는 필터 중 하나는 toosee hello **요주의 경로에 꼭 짓 점을**합니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-117">One of hello most commonly-used filters is toosee hello **vertices on critical path**.</span></span> <span data-ttu-id="0043e-118">hello **요주의 경로** hello 가장 긴 체인이 U-SQL 작업의 꼭 짓 점입니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-118">hello **Critical path** is hello longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="0043e-119">이해 hello에 대 한 중요 한 경로 꼭 짓 점은 hello 오랜 시간이 소요 확인 하 여 작업을 최적화 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-119">Understanding hello critical path is useful for optimizing your jobs by checking which vertex takes hello longest time.</span></span>
  
![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="0043e-121">hello 위쪽 가운데 창에 표시 hello **실행의 모든 hello 꼭 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-121">hello top center pane shows hello **running status of all hello vertices**.</span></span>
  
![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="0043e-123">각 꼭 짓에 대 한 정보를 표시 하는 hello 아래쪽 가운데 창:</span><span class="sxs-lookup"><span data-stu-id="0043e-123">hello bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="0043e-124">프로세스 이름: hello 꼭 짓 점 인스턴스의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-124">Process Name: hello name of hello vertex instance.</span></span> <span data-ttu-id="0043e-125">StageName|VertexName|VertexRunInstance의 다른 부분들로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="0043e-126">Hello SV7_Split [62].v1 꼭 짓 점 hello 두 번째 실행 중인 인스턴스 (.v1, 색인은 0부터 시작)를 의미 하는 예를 들어 꼭 짓 점 숫자 62 단계 SV7_Split의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-126">For example, hello SV7_Split[62].v1 vertex stands for hello second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="0043e-127">총 데이터 읽기/쓰기: hello 데이터가이 꼭지점에서 읽기/쓰기 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-127">Total Data Read/Written: hello data was read/written by this vertex.</span></span>
* <span data-ttu-id="0043e-128">상태/종료 상태: 최종 상태 hello 꼭 짓 점 종료 되 면 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-128">State/Exit Status: hello final status when hello vertex is ended.</span></span>
* <span data-ttu-id="0043e-129">종료 코드/오류 유형: hello 오류 hello 꼭 짓 점 실패 했을 때입니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-129">Exit Code/Failure Type: hello error when hello vertex failed.</span></span>
* <span data-ttu-id="0043e-130">생성 이유: 이유 hello 꼭지점을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-130">Creation Reason: Why hello vertex was created.</span></span>
* <span data-ttu-id="0043e-131">자원과 tooprocess 데이터 toostay hello 큐에 대 한 hello 꼭 짓 점 toowait 걸린 리소스 대기 시간/프로세스 대기 시간/PN 큐 대기 시간: hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-131">Resource Latency/Process Latency/PN Queue Latency: hello time taken for hello vertex toowait for resources, tooprocess data, and toostay in hello queue.</span></span>
* <span data-ttu-id="0043e-132">프로세스/작성자 GUID: GUID hello 현재 실행 중인 꼭 짓 점 또는 작성자입니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-132">Process/Creator GUID: GUID for hello current running vertex or its creator.</span></span>
* <span data-ttu-id="0043e-133">버전: 꼭지점을 실행 하는 hello의 hello N 번째 인스턴스 (hello 시스템을 예약할 수는 꼭 짓 점의 새 인스턴스 중복 등 여러 가지 이유로 인해, 예를 들어 장애 조치 계산에 대 한.)</span><span class="sxs-lookup"><span data-stu-id="0043e-133">Version: hello N-th instance of hello running vertex (hello system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="0043e-134">버전이 만들어진 시간.</span><span class="sxs-lookup"><span data-stu-id="0043e-134">Version Created Time.</span></span>
* <span data-ttu-id="0043e-135">프로세스 만들기 시작 시간, 프로세스/대기 시간/프로세스 시작 시간, 프로세스/완료 시간: hello 꼭 짓 점 프로세스가 생성 시작 될 때 hello 꼭 짓 점 프로세스가 시작 되 tooqueue; 특정 꼭 짓 점 프로세스 시작; 때 hello hello 특정 꼭 짓 점 완료 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when hello vertex process starts creation; when hello vertex process starts tooqueue; when hello certain vertex process starts; when hello certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0043e-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0043e-136">Next steps</span></span>
* <span data-ttu-id="0043e-137">toolog 진단 정보 참조 [Azure Data Lake 분석에 대 한 진단 로그에 액세스](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="0043e-137">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="0043e-138">toosee 복잡 한 쿼리를 참조 [분석 웹 사이트 Azure 데이터 레이크 분석을 사용 하 여 로그](data-lake-analytics-analyze-weblogs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0043e-138">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="0043e-139">tooview 작업 세부 정보 참조 [사용 하 여 작업 브라우저와 Azure 데이터 레이크 분석 작업에 대 한 작업 보기](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="0043e-139">tooview job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
