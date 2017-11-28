---
title: "Azure SQL Database에 대한 자동 조정 사용 | Microsoft Docs"
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
ms.openlocfilehash: b391b1f7aa37c5a06fc320ce892534187deb4959
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="1d09c-103">자동 조정 사용</span><span class="sxs-lookup"><span data-stu-id="1d09c-103">Enable automatic tuning</span></span>

<span data-ttu-id="1d09c-104">Azure SQL Database는 지속적으로 쿼리를 모니터링하고 워크로드의 성능 향상을 위해 수행할 수 있는 작업을 식별하는 자동으로 관리되는 데이터 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies the action that you can perform to improve performance of your workload.</span></span> <span data-ttu-id="1d09c-105">권장 사항을 검토하고 수동으로 적용하거나 Azure SQL Database에서 정정 작업을 자동으로 적용하도록 할 수 있습니다. 이는 **자동 조정 모드**로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="1d09c-106">서버 또는 데이터베이스 수준에서 자동 조정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-106">Automatic tuning can be enabled at the server or the database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="1d09c-107">서버에서 자동 조정 사용</span><span class="sxs-lookup"><span data-stu-id="1d09c-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="1d09c-108">Azure SQL Database 서버에서 자동 조정을 사용하려면 Azure Portal에서 서버로 이동한 다음 메뉴에서 **자동 조정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-108">To enable automatic tuning on Azure SQL Database server, navigate to the server in Azure portal and then select **Automatic tuning** in the menu.</span></span> <span data-ttu-id="1d09c-109">사용하려는 자동 조정 옵션을 선택하고 **적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-109">Select the automatic tuning options you want to enable and select **Apply**:</span></span>

![서버](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="1d09c-111">서버의 자동 조정 옵션은 서버의 모든 데이터베이스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-111">Automatic tuning options on server are applied to all databases on the server.</span></span> <span data-ttu-id="1d09c-112">기본적으로 모든 데이터베이스는 부모 서버에서 구성을 상속하지만 이는 각 데이터베이스에 대해 개별적으로 재정의되고 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-112">By default, all databases inherit the configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="1d09c-113">데이터베이스에서 자동 조정 구성</span><span class="sxs-lookup"><span data-stu-id="1d09c-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="1d09c-114">Azure Portal을 통해 각 데이터베이스에서 개별적으로 자동 조정 구성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-114">The Azure portal enables you to individually specify the automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="1d09c-115">동일한 구성 설정을 모든 데이터베이스에 대해 자동으로 적용할 수 있도록 서버 수준에서 자동 조정 구성을 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-115">The general recommendation is to manage the automatic tuning configuration at server level so the same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="1d09c-116">데이터베이스가 동일한 서버에서 서로 다른 경우 개별 데이터베이스에서 자동 조정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-116">Configure automatic tuning on an individual database if the database is different that others on the same server.</span></span>
>

<span data-ttu-id="1d09c-117">단일 데이터베이스에서 자동 조정을 사용하려면 Azure Portal에서 데이터베이스로 이동한 다음 **자동 조정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-117">To enable automatic tuning on a single database, navigate to the database in the Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="1d09c-118">확인란을 선택하여 데이터베이스에서 설정을 상속하도록 단일 데이터베이스를 구성하거나 데이터베이스에 대한 구성을 개별적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-118">You can configure a single database to inherit the settings from the database by selecting the checkbox or you can specify the configuration for a database individually.</span></span>

![데이터베이스](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="1d09c-120">적절한 구성을 선택한 후 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d09c-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d09c-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1d09c-121">Next steps</span></span>
* <span data-ttu-id="1d09c-122">자동 조정 및 성능을 개선할 수 있는 방법에 대한 자세한 내용은 [자동 조정 문서](sql-database-automatic-tuning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d09c-122">Read the [Automatic tuning article](sql-database-automatic-tuning.md) to learn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="1d09c-123">Azure SQL Database 성능 권장 사항에 대한 개요는 [성능 권장 사항](sql-database-advisor.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d09c-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="1d09c-124">상위 쿼리의 성능에 미치는 영향을 알아보려면 [Query Performance Insights](sql-database-query-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d09c-124">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span></span>
