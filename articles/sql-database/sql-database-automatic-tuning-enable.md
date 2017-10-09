---
title: "Azure SQL 데이터베이스에 대 한 튜닝 자동 aaaEnable | Microsoft Docs"
description: "Azure SQL Database에서 쉽게 자동 조정을 사용할 수 있습니다."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="73a39-103">자동 조정 사용</span><span class="sxs-lookup"><span data-stu-id="73a39-103">Enable automatic tuning</span></span>

<span data-ttu-id="73a39-104">Azure SQL 데이터베이스는 지속적으로 쿼리를 모니터링 하 고 hello 작업 워크 로드의 성능 tooimprove을 수행할 수 있음을 식별 하는 자동으로 관리 되는 데이터 서비스.</span><span class="sxs-lookup"><span data-stu-id="73a39-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies hello action that you can perform tooimprove performance of your workload.</span></span> <span data-ttu-id="73a39-105">권장 사항을 검토하고 수동으로 적용하거나 Azure SQL Database에서 정정 작업을 자동으로 적용하도록 할 수 있습니다. 이는 **자동 조정 모드**로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="73a39-106">자동 튜닝 hello 서버 또는 hello 데이터베이스 수준에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-106">Automatic tuning can be enabled at hello server or hello database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="73a39-107">서버에서 자동 조정 사용</span><span class="sxs-lookup"><span data-stu-id="73a39-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="73a39-108">tooenable 자동 튜닝 Azure SQL 데이터베이스 서버에 Azure 포털을 다음 선택에서 toohello 서버를 이동 **자동 튜닝** hello 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-108">tooenable automatic tuning on Azure SQL Database server, navigate toohello server in Azure portal and then select **Automatic tuning** in hello menu.</span></span> <span data-ttu-id="73a39-109">선택 hello 자동 튜닝 옵션 tooenable 한 선택 **적용**:</span><span class="sxs-lookup"><span data-stu-id="73a39-109">Select hello automatic tuning options you want tooenable and select **Apply**:</span></span>

![서버](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="73a39-111">튜닝 옵션 서버에서 자동는 hello 서버에 적용 된 tooall 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-111">Automatic tuning options on server are applied tooall databases on hello server.</span></span> <span data-ttu-id="73a39-112">기본적으로 모든 데이터베이스에서 해당 부모 서버 hello 구성을 상속 하지만 재정의 되 고 개별적으로 각 데이터베이스에 대해 지정 된 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-112">By default, all databases inherit hello configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="73a39-113">데이터베이스에서 자동 조정 구성</span><span class="sxs-lookup"><span data-stu-id="73a39-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="73a39-114">안녕 tooindividually 하면 각 데이터베이스에서 hello 자동 튜닝 구성을 지정 하는 Azure 포털 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-114">hello Azure portal enables you tooindividually specify hello automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="73a39-115">hello 일반적인 권장 구성은 toomanage hello 자동 튜닝 서버 수준에서 너무 hello 같은 구성 설정을 모든 데이터베이스에 대해 자동으로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-115">hello general recommendation is toomanage hello automatic tuning configuration at server level so hello same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="73a39-116">Hello 데이터베이스가 동일한 서버 hello에 다른 사용자는 서로 다른 경우 개별 데이터베이스에 자동 조정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-116">Configure automatic tuning on an individual database if hello database is different that others on hello same server.</span></span>
>

<span data-ttu-id="73a39-117">튜닝 단일 데이터베이스에 자동 tooenable hello Azure 포털에서에서 toohello 데이터베이스 이동 이동한 선택 **자동 튜닝**합니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-117">tooenable automatic tuning on a single database, navigate toohello database in hello Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="73a39-118">Hello 확인란을 선택 하 여 hello 데이터베이스에서 단일 데이터베이스 tooinherit hello 설정을 구성 하거나 데이터베이스에 대 한 hello 구성을 개별적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-118">You can configure a single database tooinherit hello settings from hello database by selecting hello checkbox or you can specify hello configuration for a database individually.</span></span>

![데이터베이스](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="73a39-120">적절한 구성을 선택한 후 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73a39-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="73a39-121">Next steps</span></span>
* <span data-ttu-id="73a39-122">읽기 hello [자동 튜닝 문서](sql-database-automatic-tuning.md) toolearn 자동 조정 및 방법을 파악할 수 성능이 개선 하는 방법에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-122">Read hello [Automatic tuning article](sql-database-automatic-tuning.md) toolearn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="73a39-123">Azure SQL Database 성능 권장 사항에 대한 개요는 [성능 권장 사항](sql-database-advisor.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73a39-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="73a39-124">참조 [Query Performance Insight](sql-database-query-performance.md) toolearn hello 상위 쿼리의 성능에 영향을 확인 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a39-124">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>
