---
title: "첫 번째 Azure SQL Database 설계 - C# | Microsoft Docs"
description: "첫 번째 Azure SQL Database를 설계하고 ADO.NET을 사용하여 C# 프로그램과 연결하는 방법을 알아봅니다."
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
ms.openlocfilehash: d9731cf5399cce6f103129ccda521f2867bd8da6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="d7cec-103">Azure SQL Database 설계 및 C#과 ADO.NET에 연결</span><span class="sxs-lookup"><span data-stu-id="d7cec-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="d7cec-104">Azure SQL Database는 Microsoft 클라우드("Azure")의 관계형 DBaaS(Database-As-A-Service)입니다.</span><span class="sxs-lookup"><span data-stu-id="d7cec-104">Azure SQL Database is a relational database-as-a service (DBaaS) in the Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="d7cec-105">이 자습서에서는 Visual Studio에서 Azure Portal 및 ADO.NET을 사용하여 다음과 같은 작업을 수행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d7cec-105">In this tutorial, you learn how to use the Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d7cec-106">Azure Portal에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="d7cec-106">Create a database in the Azure portal</span></span>
> * <span data-ttu-id="d7cec-107">Azure Portal에서 서버 수준 방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="d7cec-107">Set up a server-level firewall rule in the Azure portal</span></span>
> * <span data-ttu-id="d7cec-108">ADO.NET 및 Visual Studio를 사용하여 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="d7cec-108">Connect to the database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="d7cec-109">ADO.NET을 사용하여 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="d7cec-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="d7cec-110">ADO.NET을 사용하여 데이터 삽입, 업데이트 및 삭제</span><span class="sxs-lookup"><span data-stu-id="d7cec-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="d7cec-111">ADO.NET 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="d7cec-111">Query data ADO.NET</span></span>

<span data-ttu-id="d7cec-112">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7cec-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7cec-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d7cec-113">Prerequisites</span></span>

<span data-ttu-id="d7cec-114">설치된 [Visual Studio Community 2017, Visual Studio Professional 2017 또는 Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="d7cec-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- The following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- The following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="d7cec-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7cec-115">Next steps</span></span>

<span data-ttu-id="d7cec-116">이 자습서에서는 데이터베이스 및 테이블 만들기, 데이터 로드 및 쿼리, 데이터베이스를 이전 시점으로 복원과 같은 기본적인 데이터베이스 작업에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="d7cec-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore the database to a previous point in time.</span></span> <span data-ttu-id="d7cec-117">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d7cec-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="d7cec-118">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="d7cec-118">Create a database</span></span>
> * <span data-ttu-id="d7cec-119">방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="d7cec-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="d7cec-120">[Visual Studio 및 C#](sql-database-connect-query-dotnet-visual-studio.md)을 사용하여 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="d7cec-120">Connect to the database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="d7cec-121">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="d7cec-121">Create tables</span></span>
> * <span data-ttu-id="d7cec-122">데이터 삽입, 업데이트 및 삭제</span><span class="sxs-lookup"><span data-stu-id="d7cec-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="d7cec-123">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="d7cec-123">Query data</span></span>

<span data-ttu-id="d7cec-124">데이터를 마이그레이션하는 방법에 대해 자세히 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d7cec-124">Advance to the next tutorial to learn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="d7cec-125">SQL Server 데이터베이스를 Azure SQL Database로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d7cec-125">Migrate your SQL Server database to Azure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

