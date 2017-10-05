---
title: "SQL Database에 대한 1433 이외의 포트 | Microsoft Docs"
description: "ADO.NET에서 Azure SQL Database로 클라이언트 연결이 프록시를 무시하고 데이터베이스와 직접 상호 작용하는 경우가 있습니다. 1433 이외의 포트가 중요해집니다."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: d47ee8c794d1e231507dae6bb4aa88bf19ce6418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="10eb4-104">ADO.NET 4.5에 대한 1433 이외 포트</span><span class="sxs-lookup"><span data-stu-id="10eb4-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="10eb4-105">이 문서에서는 ADO.NET 4.5 이상 버전을 사용하는 클라이언트의 Azure SQL Database 연결 동작에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-105">This topic describes the Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="10eb4-106">연결 아키텍처에 대한 정보는 [Azure SQL Database 연결 아키텍처](sql-database-connectivity-architecture.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10eb4-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="10eb4-107">내부 및 외부</span><span class="sxs-lookup"><span data-stu-id="10eb4-107">Outside vs inside</span></span>
<span data-ttu-id="10eb4-108">Azure SQL Database에 연결하려면 먼저 Azure 클라우드 경계의 *외부* 또는*내부*에서 실행되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-108">For connections to Azure SQL Database, we must first ask whether your client program runs *outside* or *inside* the Azure cloud boundary.</span></span> <span data-ttu-id="10eb4-109">하위 섹션에서는 일반적으로 두 가지 시나리오를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-109">The subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="10eb4-110">*외부:* 클라이언트가 데스크톱 컴퓨터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="10eb4-111">포트 1433은 SQL 데이터베이스 클라이언트 응용 프로그램을 호스팅하는 데스크톱 컴퓨터에서 열어야 하는 유일한 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-111">Port 1433 is the only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="10eb4-112">*내부:* 클라이언트가 Azure에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="10eb4-113">클라이언트가 Azure 클라우드 경계 내부에서 실행되는 경우 SQL 데이터베이스 서버와 상호 작용하기 위해 *직접 경로* 라는 것을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-113">When your client runs inside the Azure cloud boundary, it uses what we can call a *direct route* to interact with the SQL Database server.</span></span> <span data-ttu-id="10eb4-114">연결이 설정된 후 클라이언트와 데이터베이스 사이의 추가 상호작용은 미들웨어 프록시를 관련시키지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-114">After a connection is established, further interactions between the client and database involve no middleware proxy.</span></span>

<span data-ttu-id="10eb4-115">순서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-115">The sequence is as follows:</span></span>

1. <span data-ttu-id="10eb4-116">ADO.NET 4.5 (또는 그 이상)는 Azure 클라우드와 간단한 상호작용을 시작하고, 동적으로 식별된 포트 번호를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-116">ADO.NET 4.5 (or later) initiates a brief interaction with the Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="10eb4-117">동적으로 식별된 포트 번호는 11000-11999 또는 14000-14999 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-117">The dynamically identified port number is in the range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="10eb4-118">그러면 ADO.NET은 미들웨어 없이 직접SQL 데이터베이스로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-118">ADO.NET then connects to the SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="10eb4-119">쿼리는 데이터베이스로 직접 전송되며 결과는 클라이언트에 직접 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-119">Queries are sent directly to the database, and results are returned directly to the client.</span></span>

<span data-ttu-id="10eb4-120">Azure 클라이언트 컴퓨터에 있는 11000-11999 및 14000-14999 범위의 포트가 ADO.NET 4.5와 SQL Database 간의 클라이언트 상호 작용에 사용 가능한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-120">Ensure that the port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="10eb4-121">특히 해당 범위의 포트는 모든 다른 아웃바운드 차단으로부터 자유로워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-121">In particular, ports in the range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="10eb4-122">Azure VM의 **고급 보안이 포함된 Windows 방화벽** 이 포트 설정을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-122">On your Azure VM, the **Windows Firewall with Advanced Security** controls the port settings.</span></span>
  
  * <span data-ttu-id="10eb4-123">[방화벽의 사용자 인터페이스](http://msdn.microsoft.com/library/cc646023.aspx)를 사용하여 **11000-11999**와 유사한 구문의 포트 범위와 함께 **TCP** 프로토콜을 지정하는 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-123">You can use the [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) to add a rule for which you specify the **TCP** protocol along with a port range with the syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="10eb4-124">버전 확인</span><span class="sxs-lookup"><span data-stu-id="10eb4-124">Version clarifications</span></span>
<span data-ttu-id="10eb4-125">이 섹션에서는 제품 버전을 참조하는 모니커를 명확히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-125">This section clarifies the monikers that refer to product versions.</span></span> <span data-ttu-id="10eb4-126">또한 제품 간의 버전 연결을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="10eb4-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="10eb4-127">ADO.NET</span></span>
* <span data-ttu-id="10eb4-128">ADO.NET 4.0은 TDS 7.3 프로토콜을 지원하지만 7.4는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-128">ADO.NET 4.0 supports the TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="10eb4-129">ADO.NET 4.5 이상은 TDS 7.4 프로토콜을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-129">ADO.NET 4.5 and later supports the TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="10eb4-130">관련 링크</span><span class="sxs-lookup"><span data-stu-id="10eb4-130">Related links</span></span>
* <span data-ttu-id="10eb4-131">ADO.NET 4.6은 2015년 7월 20일에 출시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="10eb4-132">.NET 팀의 블로그 알림은 [여기](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx)서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-132">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="10eb4-133">ADO.NET 4.5는 2012년 8월 15일에 출시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="10eb4-134">.NET 팀의 블로그 알림은 [여기](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx)서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-134">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="10eb4-135">ADO.NET 4.5.1에 관한 블로그 게시물은 [여기](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx)서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10eb4-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="10eb4-136">TDS 프로토콜 버전 목록</span><span class="sxs-lookup"><span data-stu-id="10eb4-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="10eb4-137">SQL 데이터베이스 개발 개요</span><span class="sxs-lookup"><span data-stu-id="10eb4-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="10eb4-138">Azure SQL 데이터베이스 방화벽</span><span class="sxs-lookup"><span data-stu-id="10eb4-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="10eb4-139">방법: SQL 데이터베이스에서 방화벽 설정 구성</span><span class="sxs-lookup"><span data-stu-id="10eb4-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

