---
title: "Stream Analytics 작업 시각화 및 문제 해결 | Microsoft Docs"
description: "진단 다이어그램 기능을 사용하여 셀프 서비스 문제 해결을 위해 Stream Analytics 작업 파이프라인을 시각화하는 방법을 알아봅니다."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 18c39a025f750cf5a17c535ab40923b7cafe413d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="03777-103">Stream Analytics 작업 시각화 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="03777-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="03777-104">다른 클라우드 기반 기술과 마찬가지로 Stream Analytics에서도 작업이 예상된 출력(또는 해당 문제에 대한 출력)을 생성하지 않는 이유를 알아내기 위해 문제 해결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="03777-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed to look into why a job does not produce the expected output (or any output for that matter).</span></span> <span data-ttu-id="03777-105">이러한 점을 고려할 때 Stream Analytics은 스트리밍 작업을 시각화하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="03777-105">With this in mind, Stream Analytics provides the capability for visualizing a streaming job.</span></span> <span data-ttu-id="03777-106">이 기능은 모델링 도구만큼 유용하며 업무에 필요한 문서 작성이라는 부수적인 효과도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="03777-106">This is also handy as a modeling tool and has the side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="03777-107">시각화 패널에는 실행되는 쿼리뿐만 아니라 입력 내용과 구성된 모든 출력 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="03777-107">In the visualization panel the inputs are visible as well as the query being executed and then all the outputs configured.</span></span> <span data-ttu-id="03777-108">연결 또는 구성 문제가 좀 더 명확히 드러나며, 구성을 시각적으로 나타내는 것도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03777-108">Connectivity or configuration issues can become more apparent and it can also be helpful to see a visual representation of your configuration.</span></span>

## <a name="using-the-diagnosis-diagram-tool"></a><span data-ttu-id="03777-109">진단 다이어그램 도구 사용</span><span class="sxs-lookup"><span data-stu-id="03777-109">Using the diagnosis diagram tool</span></span>
<span data-ttu-id="03777-110">이 시각화 도우미에 액세스하려면 Stream Analytics 작업의 "설정" 블레이드에서 "진단 다이어그램" 단추를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03777-110">To access this visualizer, simply click on the “Diagnosis diagram” button in the “Settings” blade of the of the Stream Analytics job.</span></span>

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="03777-112">모든 입력 및 출력은 아래와 같이 해당 구성 요소의 현재 상태를 나타내기 위해 색으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="03777-112">Every input and output is color coded to indicate the current state of that component, as shown below.</span></span>

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="03777-114">사용자가 작업 내의 데이터 흐름 패턴을 이해하기 위해 중간 쿼리 단계를 확인하려는 경우 시각화 도구에 쿼리가 구성 요소 단계 및 흐름 시퀀스로 구분되어 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="03777-114">When the user wants to look at intermediate query steps to understand the data flow patterns inside a job, the visualization tool provides a view of the breakdown of the query into its component steps and the flow sequence.</span></span> <span data-ttu-id="03777-115">각 쿼리 단계를 클릭하면 그림과 같이 쿼리 편집 창에 해당 섹션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="03777-115">Clicking on each query step will show the corresponding section in a query editing pane as illustrated.</span></span> 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="03777-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03777-117">Next steps</span></span>
* [<span data-ttu-id="03777-118">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="03777-118">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="03777-119">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="03777-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="03777-120">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="03777-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="03777-121">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="03777-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="03777-122">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="03777-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

