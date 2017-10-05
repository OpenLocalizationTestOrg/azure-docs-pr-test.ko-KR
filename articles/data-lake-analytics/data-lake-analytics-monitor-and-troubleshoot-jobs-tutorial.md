---
title: "Azure Portal을 사용하여 Azure Data Lake Analytics 작업 문제 해결 | Microsoft Docs"
description: "Azure 포털을 사용하여 데이터 레이크 분석 작업의 문제를 해결하는 방법에 대해 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: b9c7453cc0a94f70d0098ed83e5f127832065a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="6ef01-103">Azure 포털을 사용하여 Azure 데이터 레이크 분석 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6ef01-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="6ef01-104">Azure 포털을 사용하여 데이터 레이크 분석 작업의 문제를 해결하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-104">Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="6ef01-105">이 자습서에서는 누락된 원본 파일 문제를 설치하고 Azure 포털을 사용하여 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-105">In this tutorial, you will setup a missing source file problem, and use the Azure Portal to troubleshoot the problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="6ef01-106">데이터 레이크 분석 작업 제출</span><span class="sxs-lookup"><span data-stu-id="6ef01-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="6ef01-107">다음 U-SQL 작업 제출:</span><span class="sxs-lookup"><span data-stu-id="6ef01-107">Submit the following U-SQL job:</span></span>

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   TO "/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="6ef01-108">스크립트에 정의된 원본 파일은 **/Samples/Data/SearchLog.tsv1**이고 여기서는 **/Samples/Data/SearchLog.tsv**입니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-108">The source file defined in the script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-the-job"></a><span data-ttu-id="6ef01-109">작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6ef01-109">Troubleshoot the job</span></span>

<span data-ttu-id="6ef01-110">**모든 작업을 보려면**</span><span class="sxs-lookup"><span data-stu-id="6ef01-110">**To see all the jobs**</span></span>

1. <span data-ttu-id="6ef01-111">Azure 포털의 왼쪽 위 모서리에서 **Microsoft Azure** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-111">From the Azure portal, click **Microsoft Azure** in the upper left corner.</span></span>
2. <span data-ttu-id="6ef01-112">데이터 레이크 분석 계정 이름을 가진 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-112">Click the tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="6ef01-113">**작업 관리** 타일에 작업 요약이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-113">The job summary is shown on the **Job Management** tile.</span></span>

    ![Azure 데이터 레이크 분석 작업 관리](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="6ef01-115">작업 관리에서 작업 상태를 한 눈에 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-115">The job Management gives you a glance of the job status.</span></span> <span data-ttu-id="6ef01-116">실패한 작업이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="6ef01-117">해당 작업을 보려면 **작업 관리** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-117">Click the **Job Management** tile to see the jobs.</span></span> <span data-ttu-id="6ef01-118">작업은 **실행 중**, **대기**, **종료됨**으로 범주화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-118">The jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="6ef01-119">**종료됨** 섹션에 실패한 작업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-119">You shall see your failed job in the **Ended** section.</span></span> <span data-ttu-id="6ef01-120">목록에서 먼저 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-120">It shall be first one in the list.</span></span> <span data-ttu-id="6ef01-121">작업이 많은 경우 **필터** 를 클릭하여 작업을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-121">When you have a lot of jobs, you can click **Filter** to help you to locate jobs.</span></span>

    ![Azure 데이터 레이크 분석 필터 작업](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="6ef01-123">새 블레이드에서 작업 세부 정보를 열려면 목록에서 실패한 작업을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-123">Click the failed job from the list to open the job details in a new blade:</span></span>

    ![Azure 데이터 레이크 분석 실패 작업](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="6ef01-125">**다시 제출** 단추를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-125">Notice the **Resubmit** button.</span></span> <span data-ttu-id="6ef01-126">문제를 해결한 후 해당 작업을 다시 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-126">After you fix the problem, you can resubmit the job.</span></span>
5. <span data-ttu-id="6ef01-127">이전 스크린샷에서 강조 표시된 부분을 클릭하고 오류 세부 정보를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-127">Click highlighted part from the previous screenshot to open the error details.</span></span>  <span data-ttu-id="6ef01-128">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-128">You shall see something like:</span></span>

    ![Azure 데이터 레이크 분석 실패 작업 세부 정보](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="6ef01-130">원본 폴더를 찾을 수 없다고 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-130">It tells you the source folder is not found.</span></span>
6. <span data-ttu-id="6ef01-131">**Duplicate Script**(스크립트 복제)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="6ef01-132">**FROM** 경로를 다음으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-132">Update the **FROM** path to the following:</span></span>

    <span data-ttu-id="6ef01-133">"/Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="6ef01-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="6ef01-134">**작업 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef01-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="6ef01-135">참고 항목</span><span class="sxs-lookup"><span data-stu-id="6ef01-135">See also</span></span>
* [<span data-ttu-id="6ef01-136">Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="6ef01-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="6ef01-137">Azure PowerShell을 사용하여 Azure 데이터 레이크 분석 시작</span><span class="sxs-lookup"><span data-stu-id="6ef01-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="6ef01-138">Visual Studio를 사용하여 Azure 데이터 레이크 분석 및 U-SQL 시작</span><span class="sxs-lookup"><span data-stu-id="6ef01-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="6ef01-139">Azure 포털을 사용하여 Azure 데이터 레이크 분석 관리</span><span class="sxs-lookup"><span data-stu-id="6ef01-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
