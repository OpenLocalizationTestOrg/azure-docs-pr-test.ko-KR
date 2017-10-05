---
title: "SQL Data Warehouse의 투명한 데이터 암호화(포털) | Microsoft Docs"
description: "SQL Data Warehouse의 TDE(투명한 데이터 암호화)"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: b1db3bdfdfb54bda325c9b971cfcb4dd5efa333a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="b4c47-103">SQL 데이터 웨어하우스에서 투명한 데이터 암호화(TDE) 시작</span><span class="sxs-lookup"><span data-stu-id="b4c47-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4c47-104">보안 개요</span><span class="sxs-lookup"><span data-stu-id="b4c47-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="b4c47-105">인증</span><span class="sxs-lookup"><span data-stu-id="b4c47-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="b4c47-106">암호화(포털)</span><span class="sxs-lookup"><span data-stu-id="b4c47-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="b4c47-107">암호화(T-SQL)</span><span class="sxs-lookup"><span data-stu-id="b4c47-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="b4c47-108">필요한 권한</span><span class="sxs-lookup"><span data-stu-id="b4c47-108">Required Permssions</span></span>
<span data-ttu-id="b4c47-109">TDE(투명한 데이터 암호화)를 사용하려면 관리자 또는 dbmanager 역할의 멤버여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c47-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="b4c47-110">암호화 설정</span><span class="sxs-lookup"><span data-stu-id="b4c47-110">Enabling Encryption</span></span>
<span data-ttu-id="b4c47-111">SQL 데이터 웨어하우스에 대한 TDE를 사용하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="b4c47-111">To enable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="b4c47-112">[Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b4c47-112">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="b4c47-113">데이터베이스 블레이드에서 **설정** 단추 클릭</span><span class="sxs-lookup"><span data-stu-id="b4c47-113">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="b4c47-114">**투명한 데이터 암호화** 옵션 선택 ![][1]</span><span class="sxs-lookup"><span data-stu-id="b4c47-114">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="b4c47-115">**켜기** 설정 선택 ![][2]</span><span class="sxs-lookup"><span data-stu-id="b4c47-115">Select the **On** setting ![][2]</span></span>
5. <span data-ttu-id="b4c47-116">**저장** 선택 
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="b4c47-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="b4c47-117">암호화 비활성화</span><span class="sxs-lookup"><span data-stu-id="b4c47-117">Disabling Encryption</span></span>
<span data-ttu-id="b4c47-118">SQL 데이터 웨어하우스에 대한 TDE를 비활성화하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="b4c47-118">To disable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="b4c47-119">[Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b4c47-119">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="b4c47-120">데이터베이스 블레이드에서 **설정** 단추 클릭</span><span class="sxs-lookup"><span data-stu-id="b4c47-120">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="b4c47-121">**투명한 데이터 암호화** 옵션 선택 ![][1]</span><span class="sxs-lookup"><span data-stu-id="b4c47-121">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="b4c47-122">**끄기** 설정 선택 ![][4]</span><span class="sxs-lookup"><span data-stu-id="b4c47-122">Select the **Off** setting ![][4]</span></span>
5. <span data-ttu-id="b4c47-123">**저장** 선택 
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="b4c47-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="b4c47-124">암호화 DMV</span><span class="sxs-lookup"><span data-stu-id="b4c47-124">Encryption DMVs</span></span>
<span data-ttu-id="b4c47-125">다음 DMV로 암호화를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c47-125">Encryption can be confirmed with the following DMVs:</span></span>

* <span data-ttu-id="b4c47-126">[sys.databases]</span><span class="sxs-lookup"><span data-stu-id="b4c47-126">[sys.databases]</span></span>
* <span data-ttu-id="b4c47-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="b4c47-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
<span data-ttu-id="b4c47-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span><span class="sxs-lookup"><span data-stu-id="b4c47-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span></span>
<span data-ttu-id="b4c47-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span><span class="sxs-lookup"><span data-stu-id="b4c47-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
