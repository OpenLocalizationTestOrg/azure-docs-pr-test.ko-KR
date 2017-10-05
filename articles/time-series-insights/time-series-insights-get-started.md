---
title: "Azure Time Series Insights 환경 만들기 | Microsoft Docs"
description: "이 자습서에서는 몇 분 안에 Time Series 환경을 만들고, 이벤트 원본에 연결하고, 이벤트 데이터 분석을 준비하는 방법을 배웁니다."
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: eb710795916a2d7beea75a6408a0982fb4dc8750
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-time-series-insights-environment-in-the-azure-portal"></a><span data-ttu-id="45ce7-103">Azure Portal에서 Time Series Insights 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="45ce7-103">Create a new Time Series Insights environment in the Azure portal</span></span>

<span data-ttu-id="45ce7-104">Time Series Insights 환경은 수신 및 저장 기능이 있는 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="45ce7-105">고객은 Azure Portal을 통해 환경에 필요한 용량을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-105">Customers provision environments via the Azure portal with the required capacity.</span></span>

## <a name="steps-to-create-the-environment"></a><span data-ttu-id="45ce7-106">환경을 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="45ce7-106">Steps to create the environment</span></span>

<span data-ttu-id="45ce7-107">다음 단계에 따라 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-107">Follow these steps to create your environment:</span></span>

1.  <span data-ttu-id="45ce7-108">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="45ce7-109">왼쪽 위 모퉁이에서 더하기 기호(“+”)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-109">Click the plus sign (“+”) in the top left corner.</span></span>
3.  <span data-ttu-id="45ce7-110">검색 상자에서 "Time Series Insights"를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-110">Search for “Time Series Insights” in the search box.</span></span>

  ![Time Series Insights 환경 만들기](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="45ce7-112">“Time Series Insights”를 선택하고 “만들기”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Time Series Insights 리소스 그룹 만들기](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="45ce7-114">환경 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-114">Specify environment name.</span></span> <span data-ttu-id="45ce7-115">이 이름은 [time series 탐색기](https://insights.timeseries.azure.com)에서 환경을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-115">This name will represent the environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="45ce7-116">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-116">Select a subscription.</span></span> <span data-ttu-id="45ce7-117">이벤트 원본이 포함된 구독을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-117">Choose one that contains your event source.</span></span> <span data-ttu-id="45ce7-118">Time Series Insights는 같은 구독에 있는 Azure IoT Hub 및 Event Hub 리소스를 자동으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in the same subscription.</span></span>
7.  <span data-ttu-id="45ce7-119">리소스 그룹을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-119">Select or create a resource group.</span></span> <span data-ttu-id="45ce7-120">리소스 그룹은 함께 사용되는 Azure 리소스 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="45ce7-121">호스팅 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-121">Select a hosting location.</span></span> <span data-ttu-id="45ce7-122">데이터 센터 간에 데이터를 이동하지 못하게 하려면 이벤트 원본이 포함된 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-122">To avoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="45ce7-123">가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="45ce7-124">용량을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-124">Select capacity.</span></span> <span data-ttu-id="45ce7-125">환경을 만든 후 환경의 용량을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="45ce7-126">환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-126">Create your environment.</span></span> <span data-ttu-id="45ce7-127">로그인할 때마다 손쉽게 액세스할 수 있도록 환경을 대시보드에 고정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ce7-127">You can also pin your environment to the dashboard for easy access whenever you sign in.</span></span>

  ![Time Series Insights를 만들고 대시보드에 고정](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="45ce7-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="45ce7-129">Next steps</span></span>

* <span data-ttu-id="45ce7-130">[Time Series Insights 포털](https://insights.timeseries.azure.com)에서 환경에 액세스하도록 [데이터 액세스 정책 정의](time-series-insights-data-access.md)</span><span class="sxs-lookup"><span data-stu-id="45ce7-130">[Define data access policies](time-series-insights-data-access.md) to access your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="45ce7-131">이벤트 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="45ce7-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="45ce7-132">이벤트 원본으로 [이벤트 보내기](time-series-insights-send-events.md)</span><span class="sxs-lookup"><span data-stu-id="45ce7-132">[Send events](time-series-insights-send-events.md) to the event source</span></span>
