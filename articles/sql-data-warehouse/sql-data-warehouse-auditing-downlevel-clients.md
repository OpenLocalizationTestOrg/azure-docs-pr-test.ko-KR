---
title: "데이터 감사에 대한 SQL 데이터 웨어하우스 하위 수준 클라이언트 지원 | Microsoft Docs"
description: "데이터 감사에 대한 SQL 데이터 웨어하우스 하위 수준 클라이언트 지원에 대해 알아보기"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: a7ea6141285a0098339f1e071af2592dd4535c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="c24d4-103">SQL Data Warehouse - 감사 및 동적 데이터 마스킹에 대한 하위 수준 클라이언트 지원</span><span class="sxs-lookup"><span data-stu-id="c24d4-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="c24d4-104">[감사](sql-data-warehouse-auditing-overview.md) 는 TDS 리디렉션을 지원하는 SQL 클라이언트와 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c24d4-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="c24d4-105">TDS 7.4를 구현하는 모든 클라이언트는 리디렉션도 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c24d4-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="c24d4-106">이에 대한 예외에는 리디렉션 기능이 완전히 지원되지 않는 JDBC 4.0 및 리디렉션이 구현되지 않은 Node.JS용 Tedious가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c24d4-106">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="c24d4-107">TDS 버전 7.3 이하를 지원하는 "하위 클라이언트"의 경우, 연결 문자열에서 서버 FQDN을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c24d4-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span></span>

<span data-ttu-id="c24d4-108">연결 문자열에서 원래 서버 FQDN: <*서버 이름*>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="c24d4-108">Original server FQDN in the connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="c24d4-109">연결 문자열에서 수정된 서버 FQDN: <*서버 이름*>.database.**secure**.windows.net</span><span class="sxs-lookup"><span data-stu-id="c24d4-109">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="c24d4-110">"하위 클라이언트"의 일부 목록에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c24d4-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="c24d4-111">.NET 4.0 이하</span><span class="sxs-lookup"><span data-stu-id="c24d4-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="c24d4-112">ODBC 10.0 이하</span><span class="sxs-lookup"><span data-stu-id="c24d4-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="c24d4-113">JDBC(JDBC는 TDS 7.4를 지원하지만 TDS 리디렉션 기능은 완전히 지원되지 않음)</span><span class="sxs-lookup"><span data-stu-id="c24d4-113">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="c24d4-114">Tedious(Node.JS용)</span><span class="sxs-lookup"><span data-stu-id="c24d4-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="c24d4-115">**주석:** 위의 서버 FDQN 수정은 각 데이터베이스에서 구성 단계에 대한 요구 없이 SQL 서버 수준 감사 정책의 적용에도 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c24d4-115">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

