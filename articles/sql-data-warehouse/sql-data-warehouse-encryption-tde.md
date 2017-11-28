---
title: "SQL 데이터 웨어하우스 (포털)의 데이터 암호화 aaaTransparent | Microsoft Docs"
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
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="d00bc-103">SQL 데이터 웨어하우스에서 투명한 데이터 암호화(TDE) 시작</span><span class="sxs-lookup"><span data-stu-id="d00bc-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d00bc-104">보안 개요</span><span class="sxs-lookup"><span data-stu-id="d00bc-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="d00bc-105">인증</span><span class="sxs-lookup"><span data-stu-id="d00bc-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="d00bc-106">암호화(포털)</span><span class="sxs-lookup"><span data-stu-id="d00bc-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="d00bc-107">암호화(T-SQL)</span><span class="sxs-lookup"><span data-stu-id="d00bc-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="d00bc-108">필요한 권한</span><span class="sxs-lookup"><span data-stu-id="d00bc-108">Required Permssions</span></span>
<span data-ttu-id="d00bc-109">투명 한 데이터 암호화 (TDE) tooenable 관리자나 hello dbmanager 역할의 멤버 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d00bc-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="d00bc-110">암호화 설정</span><span class="sxs-lookup"><span data-stu-id="d00bc-110">Enabling Encryption</span></span>
<span data-ttu-id="d00bc-111">tooenable SQL 데이터 웨어하우스에 대 한 TDE는 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d00bc-111">tooenable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="d00bc-112">Hello에 열기 hello 데이터베이스 [Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d00bc-112">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="d00bc-113">데이터베이스 블레이드에서 hello hello 클릭 **설정을** 단추</span><span class="sxs-lookup"><span data-stu-id="d00bc-113">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="d00bc-114">선택 hello **투명 한 데이터 암호화** 옵션![][1]</span><span class="sxs-lookup"><span data-stu-id="d00bc-114">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="d00bc-115">선택 hello **에** 설정![][2]</span><span class="sxs-lookup"><span data-stu-id="d00bc-115">Select hello **On** setting ![][2]</span></span>
5. <span data-ttu-id="d00bc-116">**저장** 선택 
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="d00bc-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="d00bc-117">암호화 비활성화</span><span class="sxs-lookup"><span data-stu-id="d00bc-117">Disabling Encryption</span></span>
<span data-ttu-id="d00bc-118">toodisable SQL 데이터 웨어하우스에 대 한 TDE는 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d00bc-118">toodisable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="d00bc-119">Hello에 열기 hello 데이터베이스 [Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d00bc-119">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="d00bc-120">데이터베이스 블레이드에서 hello hello 클릭 **설정을** 단추</span><span class="sxs-lookup"><span data-stu-id="d00bc-120">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="d00bc-121">선택 hello **투명 한 데이터 암호화** 옵션![][1]</span><span class="sxs-lookup"><span data-stu-id="d00bc-121">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="d00bc-122">선택 hello **오프** 설정![][4]</span><span class="sxs-lookup"><span data-stu-id="d00bc-122">Select hello **Off** setting ![][4]</span></span>
5. <span data-ttu-id="d00bc-123">**저장** 선택 
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="d00bc-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="d00bc-124">암호화 DMV</span><span class="sxs-lookup"><span data-stu-id="d00bc-124">Encryption DMVs</span></span>
<span data-ttu-id="d00bc-125">다음 Dmv는 hello로 암호화를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d00bc-125">Encryption can be confirmed with hello following DMVs:</span></span>

* <span data-ttu-id="d00bc-126">[sys.databases]</span><span class="sxs-lookup"><span data-stu-id="d00bc-126">[sys.databases]</span></span>
* <span data-ttu-id="d00bc-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="d00bc-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
