---
title: "Stretch Database에 대해 투명한 데이터 암호화를 사용하도록 설정 - Azure | Microsoft Docs"
description: "Azure에서 SQL Server Stretch Database에 대해 TDE(투명한 데이터 암호화)를 사용하도록 설정"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: ceb355d2ba872ed5d3886c6dc82ca75b1854db0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="1c1db-103">Azure에서 Stretch Database에 대해 TDE(투명한 데이터 암호화)를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="1c1db-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c1db-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="1c1db-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="1c1db-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="1c1db-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="1c1db-106">TDE(투명한 데이터 암호화)는 응용 프로그램에 대한 변경 요구 없이 데이터베이스, 연결된 백업 및 저장된 트랜잭션 로그 파일에 대한 실시간 암호화 및 암호 해독을 수행하여 악의적인 활동의 위협으로부터 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1db-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="1c1db-107">TDE는 데이터베이스 암호화 키라는 대칭 키를 사용하여 전체 데이터베이스의 저장소를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1db-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="1c1db-108">데이터베이스 암호화 키는 기본 제공 서버 인증서에 의해 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c1db-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="1c1db-109">기본 제공 서버 인증서는 각 Azure 서버에 대해 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1db-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="1c1db-110">Microsoft는 적어도 90일마다 이러한 인증서를 자동으로 회전합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1db-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="1c1db-111">TDE에 대한 일반적인 설명은 [투명한 데이터 암호화(TDE)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c1db-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="1c1db-112">암호화 설정</span><span class="sxs-lookup"><span data-stu-id="1c1db-112">Enabling Encryption</span></span>
<span data-ttu-id="1c1db-113">스트레치 사용 SQL Server 데이터베이스에서 마이그레이션된 데이터를 저장하는 Azure 데이터베이스에 대해 TDE를 사용하도록 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1db-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="1c1db-114">[Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1c1db-114">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="1c1db-115">데이터베이스 블레이드에서 **설정** 단추 클릭</span><span class="sxs-lookup"><span data-stu-id="1c1db-115">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="1c1db-116">**투명한 데이터 암호화** 옵션 선택 ![][1]</span><span class="sxs-lookup"><span data-stu-id="1c1db-116">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="1c1db-117">**켜기** 설정을 선택한 다음 **저장**
   ![][2] 선택</span><span class="sxs-lookup"><span data-stu-id="1c1db-117">Select the **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="1c1db-118">암호화 비활성화</span><span class="sxs-lookup"><span data-stu-id="1c1db-118">Disabling Encryption</span></span>
<span data-ttu-id="1c1db-119">스트레치 사용 SQL Server 데이터베이스에서 마이그레이션된 데이터를 저장하는 Azure 데이터베이스에 대해 TDE를 사용하지 않도록 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1db-119">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="1c1db-120">[Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1c1db-120">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="1c1db-121">데이터베이스 블레이드에서 **설정** 단추 클릭</span><span class="sxs-lookup"><span data-stu-id="1c1db-121">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="1c1db-122">**투명한 데이터 암호화** 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="1c1db-122">Select the **Transparent data encryption** option</span></span>
4. <span data-ttu-id="1c1db-123">**끄기** 설정을 선택한 다음 **저장** 선택</span><span class="sxs-lookup"><span data-stu-id="1c1db-123">Select the **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
<span data-ttu-id="1c1db-124">[투명한 데이터 암호화(TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="1c1db-124">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
