---
title: "Excel에서 기계 학습 웹 서비스 aaaConsume | Microsoft Docs"
description: "Excel에서 Azure 기계 학습 웹 서비스 사용"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="ac719-103">Excel에서 Azure 기계 학습 웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="ac719-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="ac719-104">Azure 기계 학습 스튜디오 하면 Excel에서 직접 웹 서비스를 쉽게 toocall hello toowrite 모든 코드가 필요 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-104">Azure Machine Learning Studio makes it easy toocall web services directly from Excel without hello need toowrite any code.</span></span>

<span data-ttu-id="ac719-105">Excel 2013 또는 그 이상의 또는 Excel Online을 사용 하는 경우 Excel hello를 사용 하는 것이 좋습니다 [Excel 추가 기능](machine-learning-excel-add-in-for-web-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use hello Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="ac719-106">단계</span><span class="sxs-lookup"><span data-stu-id="ac719-106">Steps</span></span>
<span data-ttu-id="ac719-107">웹 서비스를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-107">Publish a web service.</span></span> <span data-ttu-id="ac719-108">[이 페이지](machine-learning-walkthrough-5-publish-web-service.md) 설명 어떻게 toodo 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how toodo it.</span></span> <span data-ttu-id="ac719-109">현재 hello Excel 통합 문서 기능을 단일 출력 (즉, 단일 점수 매기기 레이블) 있는 요청/응답 서비스에만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-109">Currently hello Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="ac719-110">웹 서비스를 만든 후 클릭 hello **웹 서비스** hello studio 창의 hello 왼쪽에 섹션 및 다음 Excel에서 웹 서비스 tooconsume hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-110">Once you have a web service, click on hello **WEB SERVICES** section on hello left of hello studio, and then select hello web service tooconsume from Excel.</span></span>

<span data-ttu-id="ac719-111">**기존 웹 서비스**</span><span class="sxs-lookup"><span data-stu-id="ac719-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="ac719-112">Hello에 **대시보드** hello 웹 서비스는 hello에 대 한 행에 대 한 탭 **요청/응답** 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-112">On hello **DASHBOARD** tab for hello web service is a row for hello **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="ac719-113">이 서비스를 단일 출력 있으면 hello 나타나야 **Excel 통합 문서 다운로드** 해당 행에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-113">If this service had a single output, you should see hello **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="ac719-114">**Excel 통합 문서 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="ac719-115">**새 웹 서비스**</span><span class="sxs-lookup"><span data-stu-id="ac719-115">**New Web Service**</span></span>

1. <span data-ttu-id="ac719-116">Hello Azure 기계 학습 웹 서비스 포털에서 선택 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-116">In hello Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="ac719-117">Hello 사용 페이지 hello **웹 서비스 소비 옵션** 섹션에서 hello Excel 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-117">On hello Consume page, in hello **Web service consumption options** section, click hello Excel icon.</span></span>

<span data-ttu-id="ac719-118">**Hello 통합 문서를 사용 하 여**</span><span class="sxs-lookup"><span data-stu-id="ac719-118">**Using hello workbook**</span></span>

1. <span data-ttu-id="ac719-119">통합 문서 열기 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-119">Open hello workbook.</span></span>
2. <span data-ttu-id="ac719-120">보안 경고가 나타납니다. hello 클릭 **편집 사용** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-120">A Security Warning appears; click on hello **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="ac719-121">보안 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-121">A Security Warning appears.</span></span> <span data-ttu-id="ac719-122">Hello 클릭 **콘텐츠 사용** 스프레드시트에 toorun 매크로 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-122">Click on hello **Enable Content** button toorun macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="ac719-123">매크로가 활성화되면 테이블이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="ac719-124">Hello에 대 한 입력으로 필요한 열에 파란색 RR 웹 서비스 또는 **매개 변수**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-124">Columns in blue are required as input into hello RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="ac719-125">Hello RR 서비스의 hello 출력 참고 **PREDICTED VALUES** 녹색으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-125">Note hello output of hello RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="ac719-126">지정된 된 행에 대 한 모든 열 가득 차면 hello 통합 문서 자동으로 hello 점수 매기기 API를 호출 하 고 hello 채 점 된 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-126">When all columns for a given row are filled, hello workbook automatically calls hello scoring API, and displays hello scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="ac719-127">tooscore에 여러 행, 데이터 및 hello 채우기 hello 두 번째 행 값이 생성 되 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-127">tooscore more than one row, fill hello second row with data and hello predicted values are produced.</span></span> <span data-ttu-id="ac719-128">여러 행을 한 번에 붙여 넣을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="ac719-129">예측 hello로 hello Excel 기능 (그래프, 파워 맵, 조건부 서식 지정, 등) 중 하나를 사용할 수 값 toohelp hello 데이터를 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-129">You can use any of hello Excel features (graphs, power map, conditional formatting, etc.) with hello predicted values toohelp visualize hello data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="ac719-130">통합 문서 공유</span><span class="sxs-lookup"><span data-stu-id="ac719-130">Sharing your workbook</span></span>
<span data-ttu-id="ac719-131">Hello 매크로 toowork API 키 hello 스프레드시트의 일부 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-131">For hello macros toowork, your API Key must be part of hello spreadsheet.</span></span> <span data-ttu-id="ac719-132">즉, 엔터티 및 개인 신뢰 에서만 hello 통합 문서를 공유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-132">That means that you should share hello workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="ac719-133">자동 업데이트</span><span class="sxs-lookup"><span data-stu-id="ac719-133">Automatic updates</span></span>
<span data-ttu-id="ac719-134">RRS 호출은 다음 두 가지 상황에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="ac719-135">처음으로 모든 행에 내용이 hello 해당 **매개 변수**</span><span class="sxs-lookup"><span data-stu-id="ac719-135">hello first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="ac719-136">Hello 때마다 **매개 변수** 모든 있던 행의 변경 내용을 해당 **매개 변수** 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac719-136">Any time any of hello **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
