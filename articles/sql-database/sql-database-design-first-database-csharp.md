---
title: "aaaDesign 첫 번째 Azure SQL 데이터베이스-C# | Microsoft Docs"
description: "Toodesign 첫 번째 Azure SQL 데이터베이스 알아보고 tooit ADO.NET을 사용 하 여 C# 프로그램을 사용 하 여 연결 합니다."
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="785c7-103">Azure SQL Database 설계 및 C#과 ADO.NET에 연결</span><span class="sxs-lookup"><span data-stu-id="785c7-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="785c7-104">Azure SQL 데이터베이스는 관계형 데이터베이스-으로-a (DBaaS)의 서비스 hello Microsoft 클라우드 ("Azure").</span><span class="sxs-lookup"><span data-stu-id="785c7-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="785c7-105">이 자습서에서는 Azure 포털 및 Visual studio에 ADO.NET toouse hello 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="785c7-105">In this tutorial, you learn how toouse hello Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="785c7-106">Hello Azure 포털에서에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="785c7-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="785c7-107">Hello Azure 포털에서에서 서버 수준 방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="785c7-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="785c7-108">ADO.NET 및 Visual Studio를 사용 하 여 toohello 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="785c7-108">Connect toohello database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="785c7-109">ADO.NET을 사용하여 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="785c7-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="785c7-110">ADO.NET을 사용하여 데이터 삽입, 업데이트 및 삭제</span><span class="sxs-lookup"><span data-stu-id="785c7-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="785c7-111">ADO.NET 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="785c7-111">Query data ADO.NET</span></span>

<span data-ttu-id="785c7-112">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="785c7-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="785c7-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="785c7-113">Prerequisites</span></span>

<span data-ttu-id="785c7-114">설치된 [Visual Studio Community 2017, Visual Studio Professional 2017 또는 Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="785c7-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="785c7-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="785c7-115">Next steps</span></span>

<span data-ttu-id="785c7-116">이 자습서에서는 기본적인 데이터베이스 작업 같은 데이터베이스와 테이블을 만들 배운, 로드 및 데이터를 쿼리하고 hello 데이터베이스 tooa 이전 지정 시간으로 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="785c7-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="785c7-117">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="785c7-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="785c7-118">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="785c7-118">Create a database</span></span>
> * <span data-ttu-id="785c7-119">방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="785c7-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="785c7-120">사용 하 여 toohello 데이터베이스 연결 [Visual Studio 및 C#](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="785c7-120">Connect toohello database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="785c7-121">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="785c7-121">Create tables</span></span>
> * <span data-ttu-id="785c7-122">데이터 삽입, 업데이트 및 삭제</span><span class="sxs-lookup"><span data-stu-id="785c7-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="785c7-123">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="785c7-123">Query data</span></span>

<span data-ttu-id="785c7-124">데이터 마이그레이션에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="785c7-124">Advance toohello next tutorial toolearn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="785c7-125">SQL Server 데이터베이스 tooAzure SQL 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="785c7-125">Migrate your SQL Server database tooAzure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

