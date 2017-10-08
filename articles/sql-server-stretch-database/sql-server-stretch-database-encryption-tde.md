---
title: "스트레치 데이터베이스-Azure에 대 한 투명 한 데이터 암호화 aaaEnable | Microsoft Docs"
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
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="fb1fd-103">Azure에서 Stretch Database에 대해 TDE(투명한 데이터 암호화)를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="fb1fd-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb1fd-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="fb1fd-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="fb1fd-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="fb1fd-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="fb1fd-106">투명 한 데이터 암호화 (TDE)는 변경 내용을 toohello 필요 없이 실시간 암호화 및 hello 데이터베이스, 연결 된 백업 및 트랜잭션 로그 파일에 대 한 암호 해독을 수행 하 여 악의적인 활동의 hello 위협 으로부터 보호 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fb1fd-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="fb1fd-107">TDE 키 호출된 hello 대칭 데이터베이스 암호화 키를 사용 하 여 전체 데이터베이스의 hello 저장소를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb1fd-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="fb1fd-108">hello 데이터베이스 암호화 키는 기본 제공 서버 인증서로 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb1fd-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="fb1fd-109">hello 기본 제공 서버 인증서는 각 Azure 서버에 대해 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb1fd-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="fb1fd-110">Microsoft는 적어도 90일마다 이러한 인증서를 자동으로 회전합니다.</span><span class="sxs-lookup"><span data-stu-id="fb1fd-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="fb1fd-111">TDE에 대한 일반적인 설명은 [투명한 데이터 암호화(TDE)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb1fd-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="fb1fd-112">암호화 설정</span><span class="sxs-lookup"><span data-stu-id="fb1fd-112">Enabling Encryption</span></span>
<span data-ttu-id="fb1fd-113">TDE tooenable hello 스트레치 사용 SQL Server 데이터베이스에서 마이그레이션된 데이터를 저장 하는 Azure 데이터베이스에 대 한 작업을 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb1fd-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="fb1fd-114">Hello에 열기 hello 데이터베이스 [Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="fb1fd-114">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="fb1fd-115">데이터베이스 블레이드에서 hello hello 클릭 **설정을** 단추</span><span class="sxs-lookup"><span data-stu-id="fb1fd-115">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="fb1fd-116">선택 hello **투명 한 데이터 암호화** 옵션![][1]</span><span class="sxs-lookup"><span data-stu-id="fb1fd-116">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="fb1fd-117">선택 hello **에** 설정을 선택한 후 **저장**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="fb1fd-117">Select hello **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="fb1fd-118">암호화 비활성화</span><span class="sxs-lookup"><span data-stu-id="fb1fd-118">Disabling Encryption</span></span>
<span data-ttu-id="fb1fd-119">TDE toodisable hello 스트레치 사용 SQL Server 데이터베이스에서 마이그레이션된 데이터를 저장 하는 Azure 데이터베이스에 대 한 작업을 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb1fd-119">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="fb1fd-120">Hello에 열기 hello 데이터베이스 [Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="fb1fd-120">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="fb1fd-121">데이터베이스 블레이드에서 hello hello 클릭 **설정을** 단추</span><span class="sxs-lookup"><span data-stu-id="fb1fd-121">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="fb1fd-122">선택 hello **투명 한 데이터 암호화** 옵션</span><span class="sxs-lookup"><span data-stu-id="fb1fd-122">Select hello **Transparent data encryption** option</span></span>
4. <span data-ttu-id="fb1fd-123">선택 hello **오프** 설정을 선택한 후 **저장**</span><span class="sxs-lookup"><span data-stu-id="fb1fd-123">Select hello **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
[투명한 데이터 암호화(TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
