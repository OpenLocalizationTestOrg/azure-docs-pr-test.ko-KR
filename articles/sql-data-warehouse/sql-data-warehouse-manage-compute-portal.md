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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a>Azure SQL 데이터 웨어하우스의 계산 능력 관리(Azure 포털)
> [!div class="op_single_selector"]
> * [개요](sql-data-warehouse-manage-compute-overview.md)
> * [포털](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST (영문)](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a>계산 능력 크기 조정
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange 계산 리소스:

1. 열기 hello [Azure 포털][Azure portal]데이터베이스를 열고 클릭 **배율**합니다.

    ![크기 조정을 클릭합니다.][1]
2. Hello 눈금 블레이드에서 왼쪽 hello 슬라이더를 이동 하거나 toochange hello DWU 설정을 마우스 오른쪽 단추로 합니다.

    ![슬라이더를 이동합니다][2]
3. **Save**를 클릭합니다. 확인 메시지가 표시됩니다. 클릭 **예** tooconfirm 또는 **없습니다** toocancel 합니다.

    ![저장을 클릭합니다.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>계산 일시 중지
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause 데이터베이스:

1. 열기 hello [Azure 포털] [ Azure portal] 하 고 데이터베이스를 엽니다. 상태는 해당 hello 확인 **온라인**합니다.

    ![온라인 상태][6]
2. toosuspend 계산 및 메모리 리소스를 클릭 하 여 **일시 중지**, 확인 메시지가 나타납니다. 클릭 **예** tooconfirm 또는 **없습니다** toocancel 합니다.

    ![일시 중지 확인][7]
3. Hello 상태는 SQL 데이터 웨어하우스 hello 데이터베이스를 시작 하는 동안 **일시 중지**합니다.
4. Hello 상태 경우 **Paused**, hello 일시 중지 작업이 수행 되 고 더 이상 dwu로 대 한 청구 합니다.

    ![일시 중지 상태][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>계산 다시 시작
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume 데이터베이스:

1. 열기 hello [Azure 포털] [ Azure portal] 하 고 데이터베이스를 엽니다. 상태는 해당 hello 확인 **Paused**합니다.

    ![데이터베이스 일시 중지][4]
2. tooresume hello 데이터베이스 클릭 **시작**, 확인 메시지가 나타납니다. 클릭 **예** tooconfirm 또는 **없습니다** toocancel 합니다.

    ![다시 시작 확인][5]
3. SQL 데이터 웨어하우스 hello 데이터베이스를 시작 하는 동안 hello 상태 "다시 시작 중"입니다.
4. Hello 상태 경우 **온라인**, hello 데이터베이스를 준비 합니다.

    ![온라인 상태][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>다음 단계
자세한 내용은 [관리 개요][Management overview]를 참조하세요.

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
