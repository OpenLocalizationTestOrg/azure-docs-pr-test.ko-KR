---
title: "SQL 데이터베이스에 대 한 1433 이외의 aaaPorts | Microsoft Docs"
description: "ADO.NET tooAzure SQL 데이터베이스의에서 클라이언트 연결을 때때로 hello 프록시 사용 안 함 및 hello 데이터베이스와 직접 상호 작용 합니다. 1433 이외의 포트가 중요해집니다."
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
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="4a438-104">ADO.NET 4.5에 대한 1433 이외 포트</span><span class="sxs-lookup"><span data-stu-id="4a438-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="4a438-105">이 항목에서는 ADO.NET 4.5 이상 버전을 사용 하는 클라이언트 hello Azure SQL 데이터베이스 연결 동작을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-105">This topic describes hello Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4a438-106">연결 아키텍처에 대한 정보는 [Azure SQL Database 연결 아키텍처](sql-database-connectivity-architecture.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a438-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="4a438-107">내부 및 외부</span><span class="sxs-lookup"><span data-stu-id="4a438-107">Outside vs inside</span></span>
<span data-ttu-id="4a438-108">연결 tooAzure SQL 데이터베이스에 대 한에서는 먼저 요청 해야 클라이언트 프로그램의 실행 여부가 *외부* 또는 *내* hello Azure 클라우드 경계입니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-108">For connections tooAzure SQL Database, we must first ask whether your client program runs *outside* or *inside* hello Azure cloud boundary.</span></span> <span data-ttu-id="4a438-109">hello 하위 섹션에서는 두 가지 일반적인 시나리오를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-109">hello subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="4a438-110">*외부:* 클라이언트가 데스크톱 컴퓨터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="4a438-111">포트 1433는 SQL 데이터베이스 클라이언트 응용 프로그램을 호스트 하는 데스크톱 컴퓨터에 열려 있어야 하는 hello 유일한 포트는입니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-111">Port 1433 is hello only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="4a438-112">*내부:* 클라이언트가 Azure에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="4a438-113">클라이언트 hello Azure 클라우드 경계 내에서 실행을 사용 하 여 주기 수는 *직접 경로* hello SQL 데이터베이스 서버와 toointeract 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-113">When your client runs inside hello Azure cloud boundary, it uses what we can call a *direct route* toointeract with hello SQL Database server.</span></span> <span data-ttu-id="4a438-114">연결이 설정 되 면 hello 클라이언트 데이터베이스와 추가 상호 작용 미들웨어 프록시가 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-114">After a connection is established, further interactions between hello client and database involve no middleware proxy.</span></span>

<span data-ttu-id="4a438-115">hello 시퀀스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-115">hello sequence is as follows:</span></span>

1. <span data-ttu-id="4a438-116">ADO.NET 4.5 (또는 이후 버전) hello Azure 클라우드로 간략 한 상호 작용을 시작 하 고 동적으로 식별 된 포트 번호를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-116">ADO.NET 4.5 (or later) initiates a brief interaction with hello Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="4a438-117">동적으로 식별 된 hello 포트 번호가 11000 11999 또는 14000 14999 hello 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-117">hello dynamically identified port number is in hello range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="4a438-118">ADO.NET 다음 연결 toohello SQL 데이터베이스 서버를 직접 없는 미들웨어 사이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-118">ADO.NET then connects toohello SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="4a438-119">쿼리 직접 toohello 데이터베이스 전송 되 고 결과가 직접 toohello 클라이언트 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-119">Queries are sent directly toohello database, and results are returned directly toohello client.</span></span>

<span data-ttu-id="4a438-120">11000 11999 14000 14999 Azure 클라이언트 컴퓨터의 범위는 SQL 데이터베이스와 ADO.NET 4.5 클라이언트 상호 작용에 사용할 수 있는 남아 hello 포트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-120">Ensure that hello port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="4a438-121">특히 hello 범위의 포트 다른 아웃 바운드 블 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-121">In particular, ports in hello range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="4a438-122">Azure VM에서 hello **고급 보안이 포함 된 Windows 방화벽** 컨트롤 hello 포트 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-122">On your Azure VM, hello **Windows Firewall with Advanced Security** controls hello port settings.</span></span>
  
  * <span data-ttu-id="4a438-123">Hello를 사용할 수 있습니다 [방화벽의 사용자 인터페이스](http://msdn.microsoft.com/library/cc646023.aspx) hello을 지정 하는 규칙 tooadd **TCP** hello 구문 사용 하 여 포트 범위를 함께 프로토콜 같은 **11000 11999**합니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-123">You can use hello [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a rule for which you specify hello **TCP** protocol along with a port range with hello syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="4a438-124">버전 확인</span><span class="sxs-lookup"><span data-stu-id="4a438-124">Version clarifications</span></span>
<span data-ttu-id="4a438-125">이 섹션에 tooproduct 버전을 참조 하는 hello 모니커 명확히 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-125">This section clarifies hello monikers that refer tooproduct versions.</span></span> <span data-ttu-id="4a438-126">또한 제품 간의 버전 연결을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="4a438-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="4a438-127">ADO.NET</span></span>
* <span data-ttu-id="4a438-128">ADO.NET 4.0에서는 hello TDS 7.3 프로토콜 있지만 7.4 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-128">ADO.NET 4.0 supports hello TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="4a438-129">ADO.NET 4.5 이상 hello TDS 7.4 프로토콜을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-129">ADO.NET 4.5 and later supports hello TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="4a438-130">관련 링크</span><span class="sxs-lookup"><span data-stu-id="4a438-130">Related links</span></span>
* <span data-ttu-id="4a438-131">ADO.NET 4.6은 2015년 7월 20일에 출시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="4a438-132">Hello.NET 팀의 블로그 알림을 ´ ï ´ [여기](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-132">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="4a438-133">ADO.NET 4.5는 2012년 8월 15일에 출시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="4a438-134">Hello.NET 팀의 블로그 알림을 ´ ï ´ [여기](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-134">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="4a438-135">ADO.NET 4.5.1에 관한 블로그 게시물은 [여기](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx)서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a438-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="4a438-136">TDS 프로토콜 버전 목록</span><span class="sxs-lookup"><span data-stu-id="4a438-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="4a438-137">SQL 데이터베이스 개발 개요</span><span class="sxs-lookup"><span data-stu-id="4a438-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="4a438-138">Azure SQL 데이터베이스 방화벽</span><span class="sxs-lookup"><span data-stu-id="4a438-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="4a438-139">방법: SQL 데이터베이스에서 방화벽 설정 구성</span><span class="sxs-lookup"><span data-stu-id="4a438-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

