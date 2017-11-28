---
title: "aaaManage 계산 능력이 Azure SQL 데이터 웨어하우스 (Azure 포털)에서 | Microsoft Docs"
description: "Azure 포털 작업 toomanage 전원을 계산 합니다. DWU를 조정하여 계산 리소스 크기를 조정합니다. 또는 일시 중지 및 재개 자원 toosave 비용을 계산 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="b6e69-105">Azure SQL 데이터 웨어하우스의 계산 능력 관리(Azure 포털)</span><span class="sxs-lookup"><span data-stu-id="b6e69-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b6e69-106">개요</span><span class="sxs-lookup"><span data-stu-id="b6e69-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="b6e69-107">포털</span><span class="sxs-lookup"><span data-stu-id="b6e69-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="b6e69-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6e69-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="b6e69-109">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="b6e69-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="b6e69-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="b6e69-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="b6e69-111">계산 능력 크기 조정</span><span class="sxs-lookup"><span data-stu-id="b6e69-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="b6e69-112">toochange 계산 리소스:</span><span class="sxs-lookup"><span data-stu-id="b6e69-112">toochange compute resources:</span></span>

1. <span data-ttu-id="b6e69-113">열기 hello [Azure 포털][Azure portal]데이터베이스를 열고 클릭 **배율**합니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-113">Open hello [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![크기 조정을 클릭합니다.][1]
2. <span data-ttu-id="b6e69-115">Hello 눈금 블레이드에서 왼쪽 hello 슬라이더를 이동 하거나 toochange hello DWU 설정을 마우스 오른쪽 단추로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-115">In hello Scale blade, move hello slider left or right toochange hello DWU setting.</span></span>

    ![슬라이더를 이동합니다][2]
3. <span data-ttu-id="b6e69-117">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-117">Click **Save**.</span></span> <span data-ttu-id="b6e69-118">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-118">A confirmation message appears.</span></span> <span data-ttu-id="b6e69-119">클릭 **예** tooconfirm 또는 **없습니다** toocancel 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-119">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![저장을 클릭합니다.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="b6e69-121">계산 일시 중지</span><span class="sxs-lookup"><span data-stu-id="b6e69-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="b6e69-122">toopause 데이터베이스:</span><span class="sxs-lookup"><span data-stu-id="b6e69-122">toopause a database:</span></span>

1. <span data-ttu-id="b6e69-123">열기 hello [Azure 포털] [ Azure portal] 하 고 데이터베이스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-123">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="b6e69-124">상태는 해당 hello 확인 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-124">Notice that hello Status is **Online**.</span></span>

    ![온라인 상태][6]
2. <span data-ttu-id="b6e69-126">toosuspend 계산 및 메모리 리소스를 클릭 하 여 **일시 중지**, 확인 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-126">toosuspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="b6e69-127">클릭 **예** tooconfirm 또는 **없습니다** toocancel 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-127">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![일시 중지 확인][7]
3. <span data-ttu-id="b6e69-129">Hello 상태는 SQL 데이터 웨어하우스 hello 데이터베이스를 시작 하는 동안 **일시 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-129">While SQL Data Warehouse is starting hello database, hello status is **Pausing**.</span></span>
4. <span data-ttu-id="b6e69-130">Hello 상태 경우 **Paused**, hello 일시 중지 작업이 수행 되 고 더 이상 dwu로 대 한 청구 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-130">When hello status is **Paused**, hello pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![일시 중지 상태][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="b6e69-132">계산 다시 시작</span><span class="sxs-lookup"><span data-stu-id="b6e69-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="b6e69-133">tooresume 데이터베이스:</span><span class="sxs-lookup"><span data-stu-id="b6e69-133">tooresume a database:</span></span>

1. <span data-ttu-id="b6e69-134">열기 hello [Azure 포털] [ Azure portal] 하 고 데이터베이스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-134">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="b6e69-135">상태는 해당 hello 확인 **Paused**합니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-135">Notice that hello Status is **Paused**.</span></span>

    ![데이터베이스 일시 중지][4]
2. <span data-ttu-id="b6e69-137">tooresume hello 데이터베이스 클릭 **시작**, 확인 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-137">tooresume hello database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="b6e69-138">클릭 **예** tooconfirm 또는 **없습니다** toocancel 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-138">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![다시 시작 확인][5]
3. <span data-ttu-id="b6e69-140">SQL 데이터 웨어하우스 hello 데이터베이스를 시작 하는 동안 hello 상태 "다시 시작 중"입니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-140">While SQL Data Warehouse is starting hello database, hello status is "Resuming".</span></span>
4. <span data-ttu-id="b6e69-141">Hello 상태 경우 **온라인**, hello 데이터베이스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6e69-141">When hello status is **online**, hello database is ready.</span></span>

    ![온라인 상태][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="b6e69-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b6e69-143">Next steps</span></span>
<span data-ttu-id="b6e69-144">자세한 내용은 [관리 개요][Management overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6e69-144">For more information, see [Management overview][Management overview].</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
