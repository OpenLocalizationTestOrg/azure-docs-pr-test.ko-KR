---
title: "Azure SQL 데이터베이스에 대한 일반적인 연결 문제 해결"
description: "Azure SQL 데이터베이스에 대한 일반적인 연결 오류를 확인 및 해결하는 단계"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: b8abf1285318e491d51aadf90f921103d84ce1a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-connection-issues-to-azure-sql-database"></a><span data-ttu-id="09bcf-103">Azure SQL 데이터베이스에 대한 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="09bcf-103">Troubleshoot connection issues to Azure SQL Database</span></span>
<span data-ttu-id="09bcf-104">Azure SQL 데이터베이스에 대한 연결이 실패하면 [오류 메시지](sql-database-develop-error-messages.md)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-104">When the connection to Azure SQL Database fails, you receive [error messages](sql-database-develop-error-messages.md).</span></span> <span data-ttu-id="09bcf-105">이 문서는 Azure SQL Database 연결 문제를 해결하는 데 도움이 되는 중앙 집중식 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-105">This article is a centralized topic that helps you troubleshoot Azure SQL Database connectivity issues.</span></span> <span data-ttu-id="09bcf-106">여기서는 연결 문제의 [일반적인 원인](#cause)을 소개하고, 문제 식별에 도움이 되는 [문제 해결 도구](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues)를 추천하며, [일시적인 오류](#troubleshoot-transient-errors) 및 [영구적이거나 일시적이지 않은 오류](#troubleshoot-persistent-errors)를 해결하는 문제 해결 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-106">It introduces [the common causes](#cause) of connection issues, recommends [a troubleshooting tool](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) that helps you identity the problem, and provides troubleshooting steps to solve [transient errors](#troubleshoot-transient-errors) and [persistent or non-transient errors](#troubleshoot-persistent-errors).</span></span> 

<span data-ttu-id="09bcf-107">연결 문제가 발생하는 경우 이 문서에 설명된 문제 해결 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-107">If you encounter the connection issues, try the troubleshoot steps that are described in this article.</span></span>
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a><span data-ttu-id="09bcf-108">원인</span><span class="sxs-lookup"><span data-stu-id="09bcf-108">Cause</span></span>
<span data-ttu-id="09bcf-109">연결 문제는 다음 중 하나로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-109">Connection problems may be caused by any of the following:</span></span>

* <span data-ttu-id="09bcf-110">응용 프로그램 디자인 프로세스 동안 모범 사례 및 디자인 지침을 적용하지 못함.</span><span class="sxs-lookup"><span data-stu-id="09bcf-110">Failure to apply best practices and design guidelines during the application design process.</span></span>  <span data-ttu-id="09bcf-111">시작하려면 [SQL 데이터베이스 개발 개요](sql-database-develop-overview.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09bcf-111">See [SQL Database Development Overview](sql-database-develop-overview.md) to get started.</span></span>
* <span data-ttu-id="09bcf-112">Azure SQL 데이터베이스 재구성</span><span class="sxs-lookup"><span data-stu-id="09bcf-112">Azure SQL Database reconfiguration</span></span>
* <span data-ttu-id="09bcf-113">방화벽 설정</span><span class="sxs-lookup"><span data-stu-id="09bcf-113">Firewall settings</span></span>
* <span data-ttu-id="09bcf-114">연결 제한 시간</span><span class="sxs-lookup"><span data-stu-id="09bcf-114">Connection time-out</span></span>
* <span data-ttu-id="09bcf-115">잘못된 로그인 정보</span><span class="sxs-lookup"><span data-stu-id="09bcf-115">Incorrect login information</span></span>
* <span data-ttu-id="09bcf-116">일부 Azure SQL 데이터베이스 리소스에서 최대 한도 도달</span><span class="sxs-lookup"><span data-stu-id="09bcf-116">Maximum limit reached on some Azure SQL Database resources</span></span>

<span data-ttu-id="09bcf-117">일반적으로 Azure SQL 데이터베이스에 대한 연결 문제는 다음과 같이 분류할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-117">Generally, connection issues to Azure SQL Database can be classified as follows:</span></span>

* [<span data-ttu-id="09bcf-118">일시적인 오류(단기 또는 일시적)</span><span class="sxs-lookup"><span data-stu-id="09bcf-118">Transient errors (short-lived or intermittent)</span></span>](#troubleshoot-transient-errors)
* [<span data-ttu-id="09bcf-119">영구적 또는 일시적이지 않은 오류(정기적으로 되풀이되는 오류)</span><span class="sxs-lookup"><span data-stu-id="09bcf-119">Persistent or non-transient errors (errors that regularly recur)</span></span>](#troubleshoot-persistent-errors)

## <a name="try-the-troubleshooter-for-azure-sql-database-connectivity-issues"></a><span data-ttu-id="09bcf-120">Azure SQL 데이터베이스 연결 문제에 대한 문제 해결사 시도</span><span class="sxs-lookup"><span data-stu-id="09bcf-120">Try the troubleshooter for Azure SQL Database connectivity issues</span></span>
<span data-ttu-id="09bcf-121">특정 연결 오류가 발생하면 문제를 빠르게 식별하고 해결하는 데 도움이 되는 [이 도구](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database)를 사용해보세요.</span><span class="sxs-lookup"><span data-stu-id="09bcf-121">If you encounter a specific connection error, try [this tool](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), which will help you quickly identity and resolve your problem.</span></span>

## <a name="troubleshoot-transient-errors"></a><span data-ttu-id="09bcf-122">일시적인 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="09bcf-122">Troubleshoot transient errors</span></span>

<span data-ttu-id="09bcf-123">응용 프로그램이 Azure SQL Database에 연결할 때 다음 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-123">When an application connects to an Azure SQL database, you receive the following error message:</span></span>

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry the connection later. If the problem persists, contact customer support, and provide them the session tracing ID of <z>"
```

> [!NOTE]
> <span data-ttu-id="09bcf-124">이 오류 메시지는 대개 일시적으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-124">This error message is typically transient (short-lived).</span></span>
> 
> 

<span data-ttu-id="09bcf-125">Azure 데이터베이스를 이동하거나 다시 구성하는 중이어서 SQL데이터베이스에 대한 응용 프로그램의 연결이 끊기면 이 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-125">This error occurs when the Azure database is being moved (or reconfigured) and your application loses its connection to the SQL database.</span></span> <span data-ttu-id="09bcf-126">SQL Database 재구성 이벤트는 계획된 이벤트(예: 소프트웨어 업그레이드) 또는 계획되지 않은 이벤트(예: 프로세스 충돌 또는 부하 분산) 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-126">SQL database reconfiguration events occur because of a planned event (for example, a software upgrade) or an unplanned event (for example, a process crash, or load balancing).</span></span> <span data-ttu-id="09bcf-127">대부분의 다시 구성 이벤트는 보통 일시적으로 발생하며 최대 60초 이내에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-127">Most reconfiguration events are generally short-lived and should be completed in less than 60 seconds at most.</span></span> <span data-ttu-id="09bcf-128">그러나 큰 트랜잭션으로 인해 복구가 오래 실행되는 등 이러한 이벤트가 완료되는 데 시간이 더 오래 걸리는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-128">However, these events can occasionally take longer to finish, such as when a large transaction causes a long-running recovery.</span></span>

### <a name="steps-to-resolve-transient-connectivity-issues"></a><span data-ttu-id="09bcf-129">일시적인 연결 문제를 해결하는 단계</span><span class="sxs-lookup"><span data-stu-id="09bcf-129">Steps to resolve transient connectivity issues</span></span>

1. <span data-ttu-id="09bcf-130">[Microsoft Azure 서비스 대시보드](https://azure.microsoft.com/status) 에서 응용 프로그램이 오류를 보고한 시간 동안 발생한 알려진 서비스 중단을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-130">Check the [Microsoft Azure Service Dashboard](https://azure.microsoft.com/status) for any known outages that occurred during the time during which the errors were reported by the application.</span></span>
2. <span data-ttu-id="09bcf-131">Azure SQL Database와 같이 클라우드 서비스에 연결하는 응용 프로그램에서는 주기적으로 다시 구성 이벤트가 발생하므로, 이러한 이벤트를 사용자에게 응용 프로그램 오류로 표시하는 대신 해당 오류를 처리하는 다시 시도 논리를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-131">Applications that connect to a cloud service such as Azure SQL Database should expect periodic reconfiguration events and implement retry logic to handle these errors instead of surfacing these as application errors to users.</span></span> <span data-ttu-id="09bcf-132">자세한 내용과 일반적인 다시 시도 전략을 확인하려면 [일시적인 오류](sql-database-connectivity-issues.md) 섹션과 [SQL Database 개발 개요](sql-database-develop-overview.md)에서 모범 사례 및 설계 지침을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="09bcf-132">Review the [Transient errors](sql-database-connectivity-issues.md) section and the best practices and design guidelines at [SQL Database Development Overview](sql-database-develop-overview.md) for more information and general retry strategies.</span></span> <span data-ttu-id="09bcf-133">그런 다음 세부 사항은 [SQL Database 및 SQL Server에 대한 연결 라이브러리](sql-database-libraries.md) 에서 코드 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09bcf-133">Then, see code samples at [Connection Libraries for SQL Database and SQL Server](sql-database-libraries.md) for specifics.</span></span>
3. <span data-ttu-id="09bcf-134">데이터베이스가 리소스 한계에 도달하면 일시적인 연결 문제가 발생한 것처럼 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-134">As a database approaches its resource limits, it can seem to be a transient connectivity issue.</span></span> <span data-ttu-id="09bcf-135">[성능 문제 해결](sql-database-troubleshoot-performance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09bcf-135">See [Troubleshooting Performance Issues](sql-database-troubleshoot-performance.md).</span></span>
4. <span data-ttu-id="09bcf-136">연결 문제가 계속 발생하거나 응용 프로그램에서 오류가 발생하는 기간이 60초를 초과하는 경우 또는 특정일에 오류가 여러 번 발생하는 경우에는 **Azure 지원** 사이트에서 [지원 받기](https://azure.microsoft.com/support/options) 를 선택하여 Azure 지원 요청을 접수합니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-136">If connectivity problems continue, or if the duration for which your application encounters the error exceeds 60 seconds or if you see multiple occurrences of the error in a given day, file an Azure support request by selecting **Get Support** on the [Azure Support](https://azure.microsoft.com/support/options) site.</span></span>

## <a name="troubleshoot-persistent-errors"></a><span data-ttu-id="09bcf-137">영구 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="09bcf-137">Troubleshoot persistent errors</span></span>
<span data-ttu-id="09bcf-138">응용 프로그램이 Azure SQL 데이터베이스 연결에 계속 실패하는 경우 일반적으로 다음 문제 중 하나를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-138">If the application persistently fails to connect to Azure SQL Database, it usually indicates an issue with one of the following:</span></span>

* <span data-ttu-id="09bcf-139">방화벽 구성.</span><span class="sxs-lookup"><span data-stu-id="09bcf-139">Firewall configuration.</span></span> <span data-ttu-id="09bcf-140">Azure SQL 데이터베이스 또는 클라이언트 쪽 방화벽이 Azure SQL 데이터베이스에 대한 연결을 차단하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-140">The Azure SQL database or client-side firewall is blocking connections to Azure SQL Database.</span></span>
* <span data-ttu-id="09bcf-141">클라이언트 쪽 네트워크 재구성: 예를 들어 새 IP 주소 또는 프록시 서버.</span><span class="sxs-lookup"><span data-stu-id="09bcf-141">Network reconfiguration on the client side: for example, a new IP address or a proxy server.</span></span>
* <span data-ttu-id="09bcf-142">사용자 오류: 예를 들어 연결 문자열에서 서버 이름과 같이 연결 매개 변수를 잘못 입력했습니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-142">User error: for example, mistyped connection parameters, such as the server name in the connection string.</span></span>

### <a name="steps-to-resolve-persistent-connectivity-issues"></a><span data-ttu-id="09bcf-143">영구적인 연결 문제를 해결하는 단계</span><span class="sxs-lookup"><span data-stu-id="09bcf-143">Steps to resolve persistent connectivity issues</span></span>
1. <span data-ttu-id="09bcf-144">클라이언트 IP 주소를 허용하도록 [방화벽 규칙](sql-database-configure-firewall-settings.md) 을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-144">Set up [firewall rules](sql-database-configure-firewall-settings.md) to allow the client IP address.</span></span> <span data-ttu-id="09bcf-145">임시 테스트 목적으로 시작 IP 주소 범위로 0.0.0.0을 사용하고 끝 IP 주소 범위로 255.255.255.255를 사용하여 방화벽 규칙을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-145">For temporary testing purposes, set up a firewall rule using 0.0.0.0 as the starting IP address range and using 255.255.255.255 as the ending IP address range.</span></span> <span data-ttu-id="09bcf-146">이렇게 하면 서버가 모든 IP 주소로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-146">This will open the server to all IP addresses.</span></span> <span data-ttu-id="09bcf-147">이렇게 해서 연결 문제가 해결되면 이 규칙을 제거하고 적절하게 제한된 IP 주소 또는 주소 범위에 대해 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-147">If this resolves your connectivity issue, remove this rule and create a firewall rule for an appropriately limited IP address or address range.</span></span> 
2. <span data-ttu-id="09bcf-148">클라이언트와 인터넷 간의 모든 방화벽에서 포트 1433이 아웃바운드 연결에 대해 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-148">On all firewalls between the client and the Internet, make sure that port 1433 is open for outbound connections.</span></span> <span data-ttu-id="09bcf-149">[SQL Server 액세스를 허용하도록 Windows 방화벽 구성](https://msdn.microsoft.com/library/cc646023.aspx) 및 [포트 및 프로토콜이 필요한 하이브리드 ID](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports)에서 Azure Active Directory 인증을 위해 열어야 하는 추가 포트와 관련된 추가 포인터를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="09bcf-149">Review [Configure the Windows Firewall to Allow SQL Server Access](https://msdn.microsoft.com/library/cc646023.aspx) and [Hybrid Identity Required Ports and Protocols](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) for additional pointers related to additional ports that you need to open for Azure Active Directory authentication.</span></span>
3. <span data-ttu-id="09bcf-150">연결 문자열 및 기타 연결 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-150">Verify your connection string and other connection settings.</span></span> <span data-ttu-id="09bcf-151">[연결 문제 항목](sql-database-connectivity-issues.md#connections-to-azure-sql-database)의 연결 문자열 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09bcf-151">See the Connection String section in the [connectivity issues topic](sql-database-connectivity-issues.md#connections-to-azure-sql-database).</span></span>
4. <span data-ttu-id="09bcf-152">대시보드에서 서비스 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="09bcf-152">Check service health in the dashboard.</span></span> <span data-ttu-id="09bcf-153">지역별 가동 중단이 있다고 생각되는 경우 [가동 중단에서 복구](sql-database-disaster-recovery.md) 를 참조하여 새 지역으로 복구하는 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="09bcf-153">If you think there’s a regional outage, see [Recover from an outage](sql-database-disaster-recovery.md) for steps to recover to a new region.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09bcf-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09bcf-154">Next steps</span></span>
* [<span data-ttu-id="09bcf-155">Azure SQL 데이터베이스 성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="09bcf-155">Troubleshoot Azure SQL Database performance issues</span></span>](sql-database-troubleshoot-performance.md)
* [<span data-ttu-id="09bcf-156">Microsoft Azure 설명서 검색</span><span class="sxs-lookup"><span data-stu-id="09bcf-156">Search the documentation on Microsoft Azure</span></span>](http://azure.microsoft.com/search/documentation/)
* [<span data-ttu-id="09bcf-157">Azure SQL 데이터베이스 서비스에 대한 최신 업데이트 보기</span><span class="sxs-lookup"><span data-stu-id="09bcf-157">View the latest updates to the Azure SQL Database service</span></span>](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a><span data-ttu-id="09bcf-158">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="09bcf-158">Additional resources</span></span>
* [<span data-ttu-id="09bcf-159">SQL 데이터베이스 개발 개요</span><span class="sxs-lookup"><span data-stu-id="09bcf-159">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="09bcf-160">일반적인 일시적 오류 처리 지침</span><span class="sxs-lookup"><span data-stu-id="09bcf-160">General transient fault-handling guidance</span></span>](../best-practices-retry-general.md)
* [<span data-ttu-id="09bcf-161">SQL 데이터베이스 및 SQL Server용 연결 라이브러리</span><span class="sxs-lookup"><span data-stu-id="09bcf-161">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

