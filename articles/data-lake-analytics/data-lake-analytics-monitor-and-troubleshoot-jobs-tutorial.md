---
title: "Azure 포털을 사용 하 여 aaaTroubleshoot Azure Data Lake 분석 작업 | Microsoft Docs"
description: "어떻게 toouse hello Azure 포털 tootroubleshoot Data Lake 분석 작업에 알아봅니다. "
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
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="afa2e-103">Azure 포털을 사용하여 Azure 데이터 레이크 분석 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="afa2e-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="afa2e-104">어떻게 toouse hello Azure 포털 tootroubleshoot Data Lake 분석 작업에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-104">Learn how toouse hello Azure Portal tootroubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="afa2e-105">이 자습서에서는 누락 된 소스 파일 문제를 설정 및 hello Azure 포털 tootroubleshoot hello 문제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-105">In this tutorial, you will setup a missing source file problem, and use hello Azure Portal tootroubleshoot hello problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="afa2e-106">데이터 레이크 분석 작업 제출</span><span class="sxs-lookup"><span data-stu-id="afa2e-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="afa2e-107">U-SQL 작업을 수행 하는 hello를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-107">Submit hello following U-SQL job:</span></span>

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
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="afa2e-108">hello hello 스크립트에 정의 된 소스 파일은 **/Samples/Data/SearchLog.tsv1**, 여야 함 **/Samples/Data/SearchLog.tsv**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-108">hello source file defined in hello script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-hello-job"></a><span data-ttu-id="afa2e-109">Hello 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="afa2e-109">Troubleshoot hello job</span></span>

<span data-ttu-id="afa2e-110">**toosee 모든 hello 작업**</span><span class="sxs-lookup"><span data-stu-id="afa2e-110">**toosee all hello jobs**</span></span>

1. <span data-ttu-id="afa2e-111">Hello Azure 포털에서에서 클릭 **Microsoft Azure** hello 왼쪽된 위 모퉁이에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-111">From hello Azure portal, click **Microsoft Azure** in hello upper left corner.</span></span>
2. <span data-ttu-id="afa2e-112">Data Lake 분석 계정 이름과 함께 hello 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-112">Click hello tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="afa2e-113">hello에 표시 되는 hello 작업 요약 **작업 관리** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-113">hello job summary is shown on hello **Job Management** tile.</span></span>

    ![Azure 데이터 레이크 분석 작업 관리](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="afa2e-115">hello 작업 관리의 hello 작업 상태 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-115">hello job Management gives you a glance of hello job status.</span></span> <span data-ttu-id="afa2e-116">실패한 작업이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="afa2e-117">Hello 클릭 **작업 관리** toosee hello 작업 바둑판식으로 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-117">Click hello **Job Management** tile toosee hello jobs.</span></span> <span data-ttu-id="afa2e-118">hello 작업으로 분류 됩니다 **실행**, **큐 대기**, 및 **종료 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-118">hello jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="afa2e-119">Hello에 실패 한 작업 표시 **종료 됨** 섹션.</span><span class="sxs-lookup"><span data-stu-id="afa2e-119">You shall see your failed job in hello **Ended** section.</span></span> <span data-ttu-id="afa2e-120">Hello 목록의 첫 번째 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-120">It shall be first one in hello list.</span></span> <span data-ttu-id="afa2e-121">많은 작업을 사용 하는 경우 클릭할 수 있는 **필터** toohelp toolocate 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-121">When you have a lot of jobs, you can click **Filter** toohelp you toolocate jobs.</span></span>

    ![Azure 데이터 레이크 분석 필터 작업](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="afa2e-123">Hello hello 목록 tooopen hello에서에서 작업 세부 정보는 새 블레이드가에서 실패 한 작업을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-123">Click hello failed job from hello list tooopen hello job details in a new blade:</span></span>

    ![Azure 데이터 레이크 분석 실패 작업](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="afa2e-125">공지 hello **다시 전송** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-125">Notice hello **Resubmit** button.</span></span> <span data-ttu-id="afa2e-126">Hello 문제를 해결 한 후에 hello 작업을 다시 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-126">After you fix hello problem, you can resubmit hello job.</span></span>
5. <span data-ttu-id="afa2e-127">Hello 이전 스크린 샷 tooopen hello 오류 정보에서 강조 표시 된 부분을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-127">Click highlighted part from hello previous screenshot tooopen hello error details.</span></span>  <span data-ttu-id="afa2e-128">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-128">You shall see something like:</span></span>

    ![Azure 데이터 레이크 분석 실패 작업 세부 정보](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="afa2e-130">Hello 소스 폴더를 찾지 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-130">It tells you hello source folder is not found.</span></span>
6. <span data-ttu-id="afa2e-131">**Duplicate Script**(스크립트 복제)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="afa2e-132">업데이트 hello **FROM** 경로 toohello 다음:</span><span class="sxs-lookup"><span data-stu-id="afa2e-132">Update hello **FROM** path toohello following:</span></span>

    <span data-ttu-id="afa2e-133">"/Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="afa2e-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="afa2e-134">**작업 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="afa2e-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="afa2e-135">참고 항목</span><span class="sxs-lookup"><span data-stu-id="afa2e-135">See also</span></span>
* [<span data-ttu-id="afa2e-136">Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="afa2e-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="afa2e-137">Azure PowerShell을 사용하여 Azure 데이터 레이크 분석 시작</span><span class="sxs-lookup"><span data-stu-id="afa2e-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="afa2e-138">Visual Studio를 사용하여 Azure 데이터 레이크 분석 및 U-SQL 시작</span><span class="sxs-lookup"><span data-stu-id="afa2e-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="afa2e-139">Azure 포털을 사용하여 Azure 데이터 레이크 분석 관리</span><span class="sxs-lookup"><span data-stu-id="afa2e-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
