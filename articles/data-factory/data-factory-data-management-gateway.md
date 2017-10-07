---
title: "데이터 팩토리에 대 한 관리 게이트웨이 aaaData | Microsoft Docs"
description: "Hello와 온-프레미스 데이터 게이트웨이 toomove 데이터 설정 클라우드입니다. 데이터 toomove Azure Data Factory에서에서 데이터 관리 게이트웨이 사용 합니다."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="60d12-104">데이터 관리 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="60d12-104">Data Management Gateway</span></span>
<span data-ttu-id="60d12-105">hello 데이터 관리 게이트웨이 클라우드 및 온-프레미스 데이터 저장소 간의 온-프레미스 환경 toocopy 데이터에 설치 해야 하는 클라이언트 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-105">hello Data management gateway is a client agent that you must install in your on-premises environment toocopy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="60d12-106">hello 온-프레미스 데이터를 Data Factory에서 지 원하는 저장소 hello에 나열 된 [지원 되는 데이터 원본](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 섹션.</span><span class="sxs-lookup"><span data-stu-id="60d12-106">hello on-premises data stores supported by Data Factory are listed in hello [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="60d12-107">이 문서는 hello에 hello 연습 보완 [온-프레미스와 클라우드 간 데이터 이동 데이터 저장소](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="60d12-107">This article complements hello walkthrough in hello [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="60d12-108">Hello 연습 hello 게이트웨이 toomove 데이터는 온-프레미스 SQL Server 데이터베이스 tooan Azure blob에서 사용 하는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-108">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span> <span data-ttu-id="60d12-109">이 문서는 데이터 관리 게이트웨이 hello에 대 한 깊이 있는 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-109">This article provides detailed in-depth information about hello data management gateway.</span></span> 

<span data-ttu-id="60d12-110">Hello 게이트웨이를 여러 온-프레미스 컴퓨터를 연결 하 여 데이터 관리 게이트웨이 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-110">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="60d12-111">노드에서 동시에 실행할 수 있는 데이터 이동 작업의 수를 늘려 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="60d12-112">이 기능은 단일 노드가 있는 논리 게이트웨이에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="60d12-113">자세한 내용은 [Azure Data Factory에서 데이터 관리 게이트웨이 확장](data-factory-data-management-gateway-high-availability-scalability.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60d12-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="60d12-114">현재, 게이트웨이 데이터 팩터리에서 hello 복사 작업 및 저장된 프로시저 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-114">Currently, gateway supports only hello copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="60d12-115">사용자 지정 활동 tooaccess 온-프레미스 데이터 원본에서 가능한 toouse hello 게이트웨이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-115">It is not possible toouse hello gateway from a custom activity tooaccess on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="60d12-116">개요</span><span class="sxs-lookup"><span data-stu-id="60d12-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="60d12-117">데이터 관리 게이트웨이의 기능</span><span class="sxs-lookup"><span data-stu-id="60d12-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="60d12-118">데이터 관리 게이트웨이 hello를 다음 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-118">Data management gateway provides hello following capabilities:</span></span>

* <span data-ttu-id="60d12-119">모델 온-프레미스 데이터 원본 및 클라우드 데이터 원본 내 같은 데이터 팩터리 hello 및 데이터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-119">Model on-premises data sources and cloud data sources within hello same data factory and move data.</span></span>
* <span data-ttu-id="60d12-120">모니터링 및 hello Data Factory 페이지에서 게이트웨이 상태에 대 한 가시성을 사용한 관리를 위한 유리의 단일 창이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-120">Have a single pane of glass for monitoring and management with visibility into gateway status from hello Data Factory page.</span></span>
* <span data-ttu-id="60d12-121">Tooon 온-프레미스 데이터 원본 액세스를 안전 하 게 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-121">Manage access tooon-premises data sources securely.</span></span>
  * <span data-ttu-id="60d12-122">변경 내용이 없습니다 toocorporate 방화벽이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-122">No changes required toocorporate firewall.</span></span> <span data-ttu-id="60d12-123">게이트웨이 아웃 바운드 HTTP 기반 연결 tooopen 더욱 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-123">Gateway only makes outbound HTTP-based connections tooopen internet.</span></span>
  * <span data-ttu-id="60d12-124">인증서를 사용하여 온-프레미스 데이터 저장소에 대한 자격 증명을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="60d12-125">데이터를 효율적으로 이동-병렬, 복원 력 있는 toointermittent 네트워크 문제 자동 다시 시도 논리와 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-125">Move data efficiently – data is transferred in parallel, resilient toointermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="60d12-126">명령 흐름 및 데이터 흐름</span><span class="sxs-lookup"><span data-stu-id="60d12-126">Command flow and data flow</span></span>
<span data-ttu-id="60d12-127">온-프레미스와 클라우드 간 복사 활동 toocopy 데이터를 사용 하면 온-프레미스 데이터 원본 toocloud에서 그 반대의 게이트웨이 tootransfer 데이터 hello 활동에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-127">When you use a copy activity toocopy data between on-premises and cloud, hello activity uses a gateway tootransfer data from on-premises data source toocloud and vice versa.</span></span>

<span data-ttu-id="60d12-128">다음은 대 한 높은 수준의 데이터 흐름 hello와 단계 데이터 게이트웨이 사용 하 여 복사에 대 한 요약: ![게이트웨이 사용 하 여 데이터 흐름](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="60d12-128">Here is hello high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="60d12-129">데이터 개발자 hello 중 하나를 사용 하는 Azure 데이터 팩터리에 대 한 한 게이트웨이 만듭니다 [Azure 포털](https://portal.azure.com) 또는 [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-129">Data developer creates a gateway for an Azure Data Factory using either hello [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="60d12-130">데이터 개발자 hello 게이트웨이 지정 하 여 온-프레미스 데이터 저장소에 대 한 연결 된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-130">Data developer creates a linked service for an on-premises data store by specifying hello gateway.</span></span> <span data-ttu-id="60d12-131">연결 된 서비스를 hello 설정, 데이터 개발자 hello 자격 증명 설정 응용 프로그램 toospecify 인증 유형 및 자격 증명 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-131">As part of setting up hello linked service, data developer uses hello Setting Credentials application toospecify authentication types and credentials.</span></span>  <span data-ttu-id="60d12-132">hello 자격 증명 설정 hello 데이터와 통신 하는 응용 프로그램 대화 상자 tootest 연결과 hello 게이트웨이 toosave 자격 증명을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-132">hello Setting Credentials application dialog communicates with hello data store tootest connection and hello gateway toosave credentials.</span></span>
3. <span data-ttu-id="60d12-133">게이트웨이는 hello 클라우드에서 hello 자격 증명을 저장 하기 전에 hello 인증서 (데이터 개발자가 제공) hello 게이트웨이에 연결 된 hello 자격 증명을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-133">Gateway encrypts hello credentials with hello certificate associated with hello gateway (supplied by data developer), before saving hello credentials in hello cloud.</span></span>
4. <span data-ttu-id="60d12-134">데이터 팩터리 서비스는 일정 및 공유 Azure 서비스 버스 큐를 사용 하는 컨트롤 채널을 통해 작업의 관리에 대 한 hello 게이트웨이와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-134">Data Factory service communicates with hello gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="60d12-135">복사 활동 작업 toobe 시작 하면 데이터 팩터리에 자격 증명 정보와 함께 hello 요청을 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-135">When a copy activity job needs toobe kicked off, Data Factory queues hello request along with credential information.</span></span> <span data-ttu-id="60d12-136">게이트웨이는 hello 작업 hello 큐 폴링 후 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-136">Gateway kicks off hello job after polling hello queue.</span></span>
5. <span data-ttu-id="60d12-137">hello 게이트웨이 hello 인증서 동일 하 고 다음 적절 한 인증 유형 및 자격 증명으로 toohello 온-프레미스 데이터 저장소를 연결로 hello 자격 증명을 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-137">hello gateway decrypts hello credentials with hello same certificate and then connects toohello on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="60d12-138">hello 게이트웨이 온-프레미스 저장소 tooa 클라우드 저장소에서 또는 그 반대로 hello 데이터 파이프라인에서 hello 복사 작업은 구성 하는 방법에 따라 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-138">hello gateway copies data from an on-premises store tooa cloud storage, or vice versa depending on how hello Copy Activity is configured in hello data pipeline.</span></span> <span data-ttu-id="60d12-139">이 단계에 대 한 hello 게이트웨이 직접 보안 (HTTPS) 채널을 통해 Azure Blob 저장소와 같은 클라우드 기반 저장소 서비스와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-139">For this step, hello gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="60d12-140">게이트웨이 사용을 위한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="60d12-140">Considerations for using gateway</span></span>
* <span data-ttu-id="60d12-141">데이터 관리 게이트웨이의 단일 인스턴스를 여러 온-프레미스 데이터 소스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="60d12-142">그러나 **단일 게이트웨이 인스턴스에서 동 점된 tooonly 하나의 Azure 데이터 팩터리** 및 다른 데이터 팩터리와 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-142">However, **a single gateway instance is tied tooonly one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="60d12-143">단일 컴퓨터에 **데이터 관리 게이트웨이 인스턴스를 하나만** 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="60d12-144">Tooaccess 온-프레미스 데이터 소스를 필요로 하는 두 개의 데이터 팩터리 있다고 가정해 보겠습니다 tooinstall 게이트웨이 두 온-프레미스 컴퓨터에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-144">Suppose, you have two data factories that need tooaccess on-premises data sources, you need tooinstall gateways on two on-premises computers.</span></span> <span data-ttu-id="60d12-145">즉, 게이트웨이 동 점된 tooa 특정 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="60d12-145">In other words, a gateway is tied tooa specific data factory</span></span>
* <span data-ttu-id="60d12-146">hello **게이트웨이 toobe hello hello 데이터 원본으로 동일한 컴퓨터에 필요 하지 않습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-146">hello **gateway does not need toobe on hello same machine as hello data source**.</span></span> <span data-ttu-id="60d12-147">그러나 게이트웨이 자세히 toohello 데이터 원본이 있으면 hello 게이트웨이 tooconnect toohello 데이터 원본에 대 한 hello 시간을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-147">However, having gateway closer toohello data source reduces hello time for hello gateway tooconnect toohello data source.</span></span> <span data-ttu-id="60d12-148">Hello 해당 호스트 온-프레미스 데이터 원본 하나에서 다른 컴퓨터에 hello 게이트웨이 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-148">We recommend that you install hello gateway on a machine that is different from hello one that hosts on-premises data source.</span></span> <span data-ttu-id="60d12-149">Hello 게이트웨이 및 데이터 소스가 서로 다른 컴퓨터에서을 hello 게이트웨이가 데이터 소스를 사용 하 여 리소스에 대 한 경합 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-149">When hello gateway and data source are on different machines, hello gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="60d12-150">사용할 수 있습니다 **toohello 연결 하는 서로 다른 컴퓨터에서 여러 게이트웨이 동일한 온-프레미스 데이터 원본**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-150">You can have **multiple gateways on different machines connecting toohello same on-premises data source**.</span></span> <span data-ttu-id="60d12-151">예를 들어 두 데이터 팩터리 하지만 hello 모두 hello 데이터 팩터리와 같은 온-프레미스 데이터 원본 등록을 처리 하는 두 게이트웨이 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-151">For example, you may have two gateways serving two data factories but hello same on-premises data source is registered with both hello data factories.</span></span>
* <span data-ttu-id="60d12-152">컴퓨터에 **Power BI** 시나리오를 처리할 게이트웨이가 이미 설치된 경우 **별도의 Azure Data Factory용 게이트웨이**를 다른 컴퓨터에 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="60d12-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="60d12-153">**Express 경로**를 사용할 때도 게이트웨이를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="60d12-154">**Express 경로**를 사용하더라도 데이터 소스는 방화벽으로 보호되는 온-프레미스 데이터 소스로 취급해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="60d12-155">Hello 서비스와 hello 데이터 원본 간의 hello 게이트웨이 tooestablish 연결 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-155">Use hello gateway tooestablish connectivity between hello service and hello data source.</span></span>
* <span data-ttu-id="60d12-156">수행 해야 **hello 게이트웨이 사용 하 여** hello 데이터 저장소에 hello 클라우드 중인 경우에는 **Azure IaaS VM**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-156">You must **use hello gateway** even if hello data store is in hello cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="60d12-157">설치</span><span class="sxs-lookup"><span data-stu-id="60d12-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="60d12-158">필수 조건</span><span class="sxs-lookup"><span data-stu-id="60d12-158">Prerequisites</span></span>
* <span data-ttu-id="60d12-159">지원 되는 hello **운영 체제** 버전은 Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 r 2입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-159">hello supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="60d12-160">설치의 hello 데이터 관리 게이트웨이 도메인 컨트롤러에서 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-160">Installation of hello data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="60d12-161">.NET Framework 4.5.1 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="60d12-162">Windows 7 컴퓨터에 게이트웨이를 설치하는 경우 .NET Framework 4.5 이상을 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="60d12-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="60d12-163">자세한 내용은 [.NET Framework 시스템 요구 사항](https://msdn.microsoft.com/library/8z6watww.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60d12-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="60d12-164">권장 hello **구성** hello 게이트웨이 컴퓨터 2ghz 이상, 4 개 코어, 8GB RAM 및 디스크 80 GB에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-164">hello recommended **configuration** for hello gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="60d12-165">Hello 호스트 컴퓨터 최대 절전 모드로 전환 하는 경우 hello 게이트웨이 toodata 요청 응답 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-165">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span> <span data-ttu-id="60d12-166">따라서 적절 한 구성 **전원 관리 옵션** hello 게이트웨이 설치 하기 전에 hello 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-166">Therefore, configure an appropriate **power plan** on hello computer before installing hello gateway.</span></span> <span data-ttu-id="60d12-167">Hello 컴퓨터가 구성 된 toohibernate 이면 hello 게이트웨이 설치 메시지는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-167">If hello machine is configured toohibernate, hello gateway installation prompts a message.</span></span>
* <span data-ttu-id="60d12-168">Hello 컴퓨터 tooinstall의 관리자 여야 하 고 hello 데이터 관리 게이트웨이 성공적으로 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-168">You must be an administrator on hello machine tooinstall and configure hello data management gateway successfully.</span></span> <span data-ttu-id="60d12-169">추가 사용자 toohello를 추가할 수 있습니다 **데이터 관리 게이트웨이 사용자** 로컬 Windows 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-169">You can add additional users toohello **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="60d12-170">이 그룹의 hello 구성원은 수 toouse hello **데이터 관리 게이트웨이 구성 관리자** 도구 tooconfigure hello 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-170">hello members of this group are able toouse hello **Data Management Gateway Configuration Manager** tool tooconfigure hello gateway.</span></span>

<span data-ttu-id="60d12-171">특정 빈도에 활동을 실행을 발생 복사, hello hello 컴퓨터에서 리소스 사용 (CPU, 메모리) 따르는 hello 같은 최고 및 유휴 시간 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-171">As copy activity runs happen on a specific frequency, hello resource usage (CPU, memory) on hello machine also follows hello same pattern with peak and idle times.</span></span> <span data-ttu-id="60d12-172">리소스 사용률도에 따라 달라 집니다 hello 양의 데이터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-172">Resource utilization also depends heavily on hello amount of data being moved.</span></span> <span data-ttu-id="60d12-173">여러 복사 작업이 진행 중인 경우 사용량이 많은 시간 동안 리소스 사용량이 증가하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="60d12-174">설치 옵션</span><span class="sxs-lookup"><span data-stu-id="60d12-174">Installation options</span></span>
<span data-ttu-id="60d12-175">다음 방법으로 hello에 데이터 관리 게이트웨이 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-175">Data management gateway can be installed in hello following ways:</span></span>

* <span data-ttu-id="60d12-176">Hello에서 MSI 설치 패키지를 다운로드 하 여 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=39717)합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-176">By downloading an MSI setup package from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="60d12-177">hello MSI tooupgrade 사용 되는 기존 데이터 관리 게이트웨이 toohello 최신 버전을 유지 하는 모든 설정 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-177">hello MSI can also be used tooupgrade existing data management gateway toohello latest version, with all settings preserved.</span></span>
* <span data-ttu-id="60d12-178">수동 설치에서 **데이터 게이트웨이 다운로드 및 설치** 링크 또는 빠른 설치에서 **이 컴퓨터에 직접 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="60d12-179">빠른 설치를 사용하는 단계별 지침은 [온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60d12-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="60d12-180">hello 수동 단계 toohello 다운로드 센터를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-180">hello manual step takes you toohello download center.</span></span>  <span data-ttu-id="60d12-181">다운로드 하 고 hello 게이트웨이 다운로드 센터에서 설치에 대 한 hello 지침은 hello 다음 섹션에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-181">hello instructions for downloading and installing hello gateway from download center are in hello next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="60d12-182">설치 모범 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-182">Installation best practices:</span></span>
1. <span data-ttu-id="60d12-183">Hello 컴퓨터는 최대 절전 모드 없음 있도록 hello 게이트웨이에 대 한 hello 호스트 컴퓨터에 전원 관리 옵션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-183">Configure power plan on hello host machine for hello gateway so that hello machine does not hibernate.</span></span> <span data-ttu-id="60d12-184">Hello 호스트 컴퓨터 최대 절전 모드로 전환 하는 경우 hello 게이트웨이 toodata 요청 응답 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-184">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span>
2. <span data-ttu-id="60d12-185">Hello 게이트웨이에 연결 된 hello 인증서를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-185">Back up hello certificate associated with hello gateway.</span></span>

### <a name="install-hello-gateway-from-download-center"></a><span data-ttu-id="60d12-186">다운로드 센터에서 hello 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-186">Install hello gateway from download center</span></span>
1. <span data-ttu-id="60d12-187">너무 이동[Microsoft 데이터 관리 게이트웨이 다운로드 페이지](https://www.microsoft.com/download/details.aspx?id=39717)합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-187">Navigate too[Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="60d12-188">클릭 **다운로드**, 선택 hello 적절 한 버전 (**32 비트** vs. **64비트**)을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-188">Click **Download**, select hello appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="60d12-189">Hello 실행 **MSI** 직접 또는 tooyour 하드 디스크를 저장 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-189">Run hello **MSI** directly or save it tooyour hard disk and run.</span></span>
4. <span data-ttu-id="60d12-190">Hello에 **시작** 페이지에서 한 **언어** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-190">On hello **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="60d12-191">**수락** 클릭 하 고 최종 사용자 사용권 계약을 hello **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-191">**Accept** hello End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="60d12-192">선택 **폴더** tooinstall 게이트웨이 hello 및 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-192">Select **folder** tooinstall hello gateway and click **Next**.</span></span>
7. <span data-ttu-id="60d12-193">Hello에 **준비 tooinstall** 페이지 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-193">On hello **Ready tooinstall** page, click **Install**.</span></span>
8. <span data-ttu-id="60d12-194">클릭 **마침** toocomplete 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-194">Click **Finish** toocomplete installation.</span></span>
9. <span data-ttu-id="60d12-195">Hello Azure 포털에서에서 hello 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-195">Get hello key from hello Azure portal.</span></span> <span data-ttu-id="60d12-196">Hello에 대 한 단계별 지침은 다음 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="60d12-196">See hello next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="60d12-197">Hello에 **레지스터 게이트웨이** 페이지 **데이터 관리 게이트웨이 구성 관리자** 다음 단계 hello 수행 하 여 컴퓨터에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-197">On hello **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do hello following steps:</span></span>
    1. <span data-ttu-id="60d12-198">Hello 텍스트에 hello 키를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-198">Paste hello key in hello text.</span></span>
    2. <span data-ttu-id="60d12-199">필요에 따라 **표시 게이트웨이 키** toosee hello 키 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-199">Optionally, click **Show gateway key** toosee hello key text.</span></span>
    3. <span data-ttu-id="60d12-200">**Register**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="60d12-201">키를 사용하여 게이트웨이 등록</span><span class="sxs-lookup"><span data-stu-id="60d12-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a><span data-ttu-id="60d12-202">Hello 포털에 이미 논리 게이트웨이 만들지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="60d12-202">If you haven't already created a logical gateway in hello portal</span></span>
<span data-ttu-id="60d12-203">toocreate hello에서 hello 포털 및 get hello 키에서 게이트웨이 **구성** 페이지 hello에 연습에서 단계 수행 [온-프레미스와 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="60d12-203">toocreate a gateway in hello portal and get hello key from hello **Configure** page, Follow steps from walkthrough in hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a><span data-ttu-id="60d12-204">Hello 포털에서 hello 논리 게이트웨이 이미 만든 경우</span><span class="sxs-lookup"><span data-stu-id="60d12-204">If you have already created hello logical gateway in hello portal</span></span>
1. <span data-ttu-id="60d12-205">Azure 포털에서 탐색 toohello **Data Factory** 페이지를 클릭 하 여 **연결 된 서비스** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-205">In Azure portal, navigate toohello **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Data Factory 페이지](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="60d12-207">Hello에 **연결 된 서비스** 페이지를 선택 하는 hello 논리 **게이트웨이** hello 포털에서 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-207">In hello **Linked Services** page, select hello logical **gateway** you created in hello portal.</span></span>

    ![논리 게이트웨이](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="60d12-209">Hello에 **데이터 게이트웨이** 페이지 **데이터 게이트웨이 다운로드 및 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-209">In hello **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![다운로드 링크 hello 포털에서](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="60d12-211">Hello에 **구성** 페이지 **다시 만든 후 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-211">In hello **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="60d12-212">신중 하 게 읽은 후 hello 경고 메시지에서 예를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-212">Click Yes on hello warning message after reading it carefully.</span></span>

    ![키 다시 만들기](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="60d12-214">Toohello 키 다음 복사 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-214">Click Copy button next toohello key.</span></span> <span data-ttu-id="60d12-215">hello 키는 복사한 toohello 클립보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-215">hello key is copied toohello clipboard.</span></span>

    ![키 복사](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="60d12-217">시스템 트레이 아이콘/알림</span><span class="sxs-lookup"><span data-stu-id="60d12-217">System tray icons/ notifications</span></span>
<span data-ttu-id="60d12-218">hello 다음 이미지에서는 hello 중 일부 볼 수 있는 트레이 아이콘</span><span class="sxs-lookup"><span data-stu-id="60d12-218">hello following image shows some of hello tray icons that you see.</span></span>

![시스템 트레이 아이콘](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="60d12-220">Hello 시스템 트레이 아이콘/알림 메시지 위로 커서를 이동 하면 팝업 창의 hello 게이트웨이/업데이트 작업의 hello 상태에 대 한 세부 정보 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-220">If you move cursor over hello system tray icon/notification message, you see details about hello state of hello gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="60d12-221">포트 및 방화벽</span><span class="sxs-lookup"><span data-stu-id="60d12-221">Ports and firewall</span></span>
<span data-ttu-id="60d12-222">Tooconsider 해야 하는 두 개의 방화벽이: **회사 방화벽** hello 중앙 라우터 hello 조직에서 실행 되 고 **Windows 방화벽** 여기서 hello 디먼 hello 로컬 컴퓨터에 구성 된 게이트웨이가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-222">There are two firewalls you need tooconsider: **corporate firewall** running on hello central router of hello organization, and **Windows firewall** configured as a daemon on hello local machine where hello gateway is installed.</span></span>  

![방화벽](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="60d12-224">Hello 다음을 구성 해야 회사 방화벽 수준에서 도메인 및 아웃 바운드 포트:</span><span class="sxs-lookup"><span data-stu-id="60d12-224">At corporate firewall level, you need configure hello following domains and outbound ports:</span></span>

| <span data-ttu-id="60d12-225">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="60d12-225">Domain names</span></span> | <span data-ttu-id="60d12-226">포트</span><span class="sxs-lookup"><span data-stu-id="60d12-226">Ports</span></span> | <span data-ttu-id="60d12-227">설명</span><span class="sxs-lookup"><span data-stu-id="60d12-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60d12-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="60d12-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="60d12-229">443, 80</span><span class="sxs-lookup"><span data-stu-id="60d12-229">443, 80</span></span> |<span data-ttu-id="60d12-230">데이터 이동 서비스 백 엔드와 통신에 사용됨</span><span class="sxs-lookup"><span data-stu-id="60d12-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="60d12-231">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="60d12-231">*.core.windows.net</span></span> |<span data-ttu-id="60d12-232">443</span><span class="sxs-lookup"><span data-stu-id="60d12-232">443</span></span> |<span data-ttu-id="60d12-233">Azure Blob를 사용하여 준비된 복사에 사용됨(구성된 경우)</span><span class="sxs-lookup"><span data-stu-id="60d12-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="60d12-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="60d12-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="60d12-235">443</span><span class="sxs-lookup"><span data-stu-id="60d12-235">443</span></span> |<span data-ttu-id="60d12-236">데이터 이동 서비스 백 엔드와 통신에 사용됨</span><span class="sxs-lookup"><span data-stu-id="60d12-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="60d12-237">Windows 방화벽 수준에서 이러한 아웃바운드 포트를 일반적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="60d12-238">그렇지 않은 수 구성 hello 도메인과 포트 그에 따라 게이트웨이 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-238">If not, you can configure hello domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="60d12-239">소스에 따라 toowhitelist 추가 도메인 및 아웃 바운드 포트에 있을 수 있습니다 싱크를 / Windows/회사 방화벽입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-239">Based on your source/ sinks, you may have toowhitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="60d12-240">일부 클라우드 데이터베이스에 대 한 (예: [Azure SQL 데이터베이스](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure 데이터 레이크](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access)등), 해당 방화벽 구성에 게이트웨이 컴퓨터의 IP 주소 toowhitelist 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need toowhitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a><span data-ttu-id="60d12-241">원본 데이터 저장소 tooa 싱크 데이터 저장소에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-241">Copy data from a source data store tooa sink data store</span></span>
<span data-ttu-id="60d12-242">Hello 회사 방화벽을 hello 게이트웨이 컴퓨터에서 Windows 방화벽 hello 방화벽 규칙을 올바르게 사용할 수 있고 자체 hello 데이터 저장소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-242">Ensure that hello firewall rules are enabled properly on hello corporate firewall, Windows firewall on hello gateway machine, and hello data store itself.</span></span> <span data-ttu-id="60d12-243">이러한 규칙을 사용 하면 hello 게이트웨이 tooconnect tooboth 원본 및 싱크를 성공적으로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-243">Enabling these rules allows hello gateway tooconnect tooboth source and sink successfully.</span></span> <span data-ttu-id="60d12-244">Hello 복사 작업에 포함 되는 각 데이터 저장소에 대 한 규칙을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-244">Enable rules for each data store that is involved in hello copy operation.</span></span>

<span data-ttu-id="60d12-245">예를 들어 toocopy에서 **온-프레미스 데이터 저장소 tooan Azure SQL 데이터베이스 싱크 또는 Azure SQL 데이터 웨어하우스 싱크에**, 다음 단계 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="60d12-245">For example, toocopy from **an on-premises data store tooan Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do hello following steps:</span></span>

* <span data-ttu-id="60d12-246">Windows 방화벽 및 회사 방화벽 둘 다에 대해 포트 **1433**에서 아웃바운드 **TCP** 통신을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="60d12-247">Azure SQL server tooadd hello IP 주소 허용 된 IP 주소의 hello 게이트웨이 컴퓨터 toohello 목록 중 hello 방화벽 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-247">Configure hello firewall settings of Azure SQL server tooadd hello IP address of hello gateway machine toohello list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="60d12-248">방화벽이 아웃바운드 포트 1433을 허용하지 않으면 게이트웨이는 Azure SQL에 직접 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="60d12-249">이 경우 사용할 수 있습니다 [준비 복사](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure 데이터베이스 / SQL Azure DW 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="60d12-250">이 시나리오에서는 hello 데이터 이동에 대 한 HTTPS (포트 443)을만 필요할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-250">In this scenario, you would only require HTTPS (port 443) for hello data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="60d12-251">프록시 서버 고려 사항</span><span class="sxs-lookup"><span data-stu-id="60d12-251">Proxy server considerations</span></span>
<span data-ttu-id="60d12-252">회사 네트워크 환경에는 프록시를 사용 하는 경우 서버 tooaccess hello 인터넷, 데이터 관리 게이트웨이 toouse 적절 한 프록시 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-252">If your corporate network environment uses a proxy server tooaccess hello internet, configure data management gateway toouse appropriate proxy settings.</span></span> <span data-ttu-id="60d12-253">Hello 초기 등록 단계 동안 hello 프록시를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-253">You can set hello proxy during hello initial registration phase.</span></span>

![등록 중에 프록시 설정](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="60d12-255">게이트웨이는 hello 프록시 서버 tooconnect toohello 클라우드 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-255">Gateway uses hello proxy server tooconnect toohello cloud service.</span></span> <span data-ttu-id="60d12-256">초기 설치 중에 **변경** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="60d12-257">Hello 참조 **프록시 설정을** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="60d12-257">You see hello **proxy setting** dialog.</span></span>

![구성 관리자를 사용하여 프록시 설정](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="60d12-259">이 대화 상자에는 세 가지 구성 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-259">There are three configuration options:</span></span>

* <span data-ttu-id="60d12-260">**프록시를 사용 하지 마십시오**: 게이트웨이 모든 프록시 tooconnect toocloud 서비스를 명시적으로 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-260">**Do not use proxy**: Gateway does not explicitly use any proxy tooconnect toocloud services.</span></span>
* <span data-ttu-id="60d12-261">**시스템 프록시를 사용 하 여**: 게이트웨이 설정에 구성 된 diahost.exe.config 및 diawp.exe.config hello 프록시를 사용 합니다.  프록시가 diahost.exe.config 및 diawp.exe.config에서 구성 되 면 게이트웨이 프록시를 통과 하지 않고 직접 toocloud 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-261">**Use system proxy**: Gateway uses hello proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span>
* <span data-ttu-id="60d12-262">**사용자 지정 프록시를 사용 하 여**: diahost.exe.config diawp.exe.config 구성을 사용 하는 대신 게이트웨이에 대 한 프록시 설정 toouse hello HTTP 구성입니다.  이 경우 주소 및 포트를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-262">**Use custom proxy**: Configure hello HTTP proxy setting toouse for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="60d12-263">사용자 이름 및 암호는 프록시 인증 설정에 따라 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="60d12-264">모든 설정은 hello 게이트웨이의 hello 자격 증명 인증서로 암호화 되며 hello 게이트웨이 호스트 컴퓨터에 로컬로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-264">All settings are encrypted with hello credential certificate of hello gateway and stored locally on hello gateway host machine.</span></span>

<span data-ttu-id="60d12-265">hello 데이터 관리 게이트웨이 호스트 서비스 다시 자동으로 업데이트 하는 hello 프록시 설정을 저장 한 후 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-265">hello data management gateway Host Service restarts automatically after you save hello updated proxy settings.</span></span>

<span data-ttu-id="60d12-266">게이트웨이 등록 된 후 성공적으로, tooview 원하는 또는 프록시 설정을 업데이트 하는 경우, 데이터 관리 게이트웨이 구성 관리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-266">After gateway has been successfully registered, if you want tooview or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="60d12-267">**데이터 관리 게이트웨이 구성 관리자**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="60d12-268">Toohello 전환 **설정을** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-268">Switch toohello **Settings** tab.</span></span>
3. <span data-ttu-id="60d12-269">클릭 **변경** 링크를 **HTTP 프록시** 섹션 toolaunch hello **HTTP 프록시 설정** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="60d12-269">Click **Change** link in **HTTP Proxy** section toolaunch hello **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="60d12-270">Hello를 클릭 한 후 **다음** 권한 toosave hello 프록시 설정 및 다시 시작 hello 게이트웨이 호스트 서비스에 대해 묻는 경고 대화 상자가 표시 단추를 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-270">After you click hello **Next** button, you see a warning dialog asking for your permission toosave hello proxy setting and restart hello Gateway Host Service.</span></span>

<span data-ttu-id="60d12-271">구성 관리자 도구를 사용하여 HTTP 프록시를 확인하고 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![구성 관리자를 사용하여 프록시 설정](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="60d12-273">NTLM 인증을 사용 하 여 프록시 서버를 설정한 경우 게이트웨이 호스트 서비스가 hello 도메인 계정으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under hello domain account.</span></span> <span data-ttu-id="60d12-274">나중에 도메인 계정 hello에 대 한 hello 암호를 변경 하면 hello 서비스에 대 한 구성 설정을 tooupdate를 기억 하 고 그에 따라 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-274">If you change hello password for hello domain account later, remember tooupdate configuration settings for hello service and restart it accordingly.</span></span> <span data-ttu-id="60d12-275">Toothis 요구 사항, 인해 암호를 요구 하지 있습니다 tooupdate hello 자주 하는 전용된 도메인 계정을 tooaccess hello 프록시 서버를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-275">Due toothis requirement, we suggest you use a dedicated domain account tooaccess hello proxy server that does not require you tooupdate hello password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="60d12-276">프록시 서버 설정 구성</span><span class="sxs-lookup"><span data-stu-id="60d12-276">Configure proxy server settings</span></span>
<span data-ttu-id="60d12-277">선택 하는 경우 **시스템 프록시를 사용 하 여** diahost.exe.config 및 diawp.exe.config에서 설정 하는 hello 프록시를 사용 하 여 게이트웨이 hello HTTP 프록시를 설정 합니다.  프록시가 diahost.exe.config 및 diawp.exe.config에 지정 된 경우 게이트웨이 toocloud 서비스 프록시를 통과 하지 않고 직접 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-277">If you select **Use system proxy** setting for hello HTTP proxy, gateway uses hello proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span> <span data-ttu-id="60d12-278">hello 다음 절차에서는 설명 hello diahost.exe.config 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-278">hello following procedure provides instructions for updating hello diahost.exe.config file.</span></span>  

1. <span data-ttu-id="60d12-279">파일 탐색기에서 C:\Program Files\Microsoft 데이터 관리 Gateway\2.0\Shared\diahost.exe.config tooback의 복사본을 안전 하 게 보호 hello 원본 파일을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback up hello original file.</span></span>
2. <span data-ttu-id="60d12-280">관리자 권한으로 Notepad.exe 실행을 시작하고 텍스트 파일 "C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config"를 엽니다. Hello 코드 다음에 표시 된 대로 system.net에 대 한 hello 기본 태그를 찾을:</span><span class="sxs-lookup"><span data-stu-id="60d12-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find hello default tag for system.net as shown in hello following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="60d12-281">그런 다음 hello 다음 예제에에서 나와 있는 것 처럼 프록시 서버 세부 정보를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-281">You can then add proxy server details as shown in hello following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="60d12-282">추가 속성 scriptLocation 같은 hello 프록시 태그 toospecify 필요한 hello 설정 내에서 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-282">Additional properties are allowed inside hello proxy tag toospecify hello required settings like scriptLocation.</span></span> <span data-ttu-id="60d12-283">너무 참조[프록시 요소 (네트워크 설정)](https://msdn.microsoft.com/library/sa91de1e.aspx) 구문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-283">Refer too[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="60d12-284">Hello 원래 위치로 hello 구성 파일을 저장 한 다음 hello hello 변경 내용을 선택 하는 데이터 관리 게이트웨이 호스트 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-284">Save hello configuration file into hello original location, then restart hello Data Management Gateway Host service, which picks up hello changes.</span></span> <span data-ttu-id="60d12-285">toorestart hello 서비스: hello 또는 hello 제어판에서 서비스 애플릿을 사용 하 여 **데이터 관리 게이트웨이 구성 관리자** > hello 클릭 **서비스 중지** 단추를 클릭 hello **서비스 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-285">toorestart hello service: use services applet from hello control panel, or from hello **Data Management Gateway Configuration Manager** > click hello **Stop Service** button, then click hello **Start Service**.</span></span> <span data-ttu-id="60d12-286">Hello 서비스가 시작 되지 않는 경우 가능성이 편집 된 hello 응용 프로그램 구성 파일에 잘못 된 XML 태그 구문을 추가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-286">If hello service does not start, it is likely that an incorrect XML tag syntax has been added into hello application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60d12-287">Tooupdate를 잊지 마십시오 **둘 다** diahost.exe.config 및 diawp.exe.config 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-287">Do not forget tooupdate **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="60d12-288">또한 toothese 지점 있어야 toomake 귀사의 허용 목록에 Microsoft Azure 인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-288">In addition toothese points, you also need toomake sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="60d12-289">유효한 Microsoft Azure IP 주소의 hello 목록을 hello에서 다운로드할 수 있습니다 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=41653)합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-289">hello list of valid Microsoft Azure IP addresses can be downloaded from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="60d12-290">방화벽 및 프록시 서버 관련 문제 발생 시 나타날 수 있는 증상</span><span class="sxs-lookup"><span data-stu-id="60d12-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="60d12-291">스토리를 다음 오류와 비슷한 toohello 발생 하는 경우 자체 연결 tooData 팩터리 tooauthenticate에서 게이트웨이 차단 하는 hello 방화벽 또는 프록시 서버 구성을 tooimproper 인해 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-291">If you encounter errors similar toohello following ones, it is likely due tooimproper configuration of hello firewall or proxy server, which blocks gateway from connecting tooData Factory tooauthenticate itself.</span></span> <span data-ttu-id="60d12-292">방화벽 및 프록시 서버에 제대로 구성 되어 tooprevious 섹션 tooensure를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="60d12-292">Refer tooprevious section tooensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="60d12-293">Hello 다음 오류가 수신 tooregister hello 게이트웨이 나타난다: "Failed tooregister hello 게이트웨이 키입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-293">When you try tooregister hello gateway, you receive hello following error: "Failed tooregister hello gateway key.</span></span> <span data-ttu-id="60d12-294">Tooregister hello 게이트웨이 키를 다시 시도 하기 전에 연결 된 상태에서 데이터 관리 게이트웨이 hello 및 데이터 관리 게이트웨이 호스트 서비스가 hello 시작됨인지 확인 합니다. "</span><span class="sxs-lookup"><span data-stu-id="60d12-294">Before trying tooregister hello gateway key again, confirm that hello data management gateway is in a connected state and hello Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="60d12-295">구성 관리자를 열 때 상태가 "연결 끊김" 또는 "연결 중"으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="60d12-296">"이벤트 뷰어" 아래에서 Windows 이벤트 로그를 볼 때 > "응용 프로그램 및 서비스 로그" > 다음 오류가 hello와 같은 오류 메시지가 나타나면 "데이터 관리 게이트웨이":`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="60d12-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as hello following error: `Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="60d12-297">자격 증명 암호화용 8050 포트 열기</span><span class="sxs-lookup"><span data-stu-id="60d12-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="60d12-298">hello **자격 증명 설정** 응용 프로그램에서는 hello 인바운드 포트 **8050** toorelay 자격 증명 toohello 게이트웨이 온-프레미스를 설정할 때 서비스 hello Azure 포털에에서 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-298">hello **Setting Credentials** application uses hello inbound port **8050** toorelay credentials toohello gateway when you set up an on-premises linked service in hello Azure portal.</span></span> <span data-ttu-id="60d12-299">게이트웨이 설치 하는 동안 기본적으로 hello 게이트웨이 설치가 열립니다 hello 게이트웨이 컴퓨터에서.</span><span class="sxs-lookup"><span data-stu-id="60d12-299">During gateway setup, by default, hello gateway installation opens it on hello gateway machine.</span></span>

<span data-ttu-id="60d12-300">타사 방화벽을 사용 하는 경우 hello 포트 8050 수동으로 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-300">If you are using a third-party firewall, you can manually open hello port 8050.</span></span> <span data-ttu-id="60d12-301">게이트웨이 설치 하는 동안 방화벽 문제를 실행 하면 hello 방화벽을 구성 하지 않고 명령 tooinstall hello 게이트웨이 따르는 hello를 사용 하 여 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-301">If you run into firewall issue during gateway setup, you can try using hello following command tooinstall hello gateway without configuring hello firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="60d12-302">Hello 포트 8050 hello 게이트웨이 컴퓨터에서 tooopen 하지 않으려는 경우 hello를 사용 하는 메커니즘을 사용 합니다. **자격 증명 설정** tooconfigure 데이터 응용 프로그램 자격 증명을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-302">If you choose not tooopen hello port 8050 on hello gateway machine, use mechanisms other than using hello **Setting Credentials** application tooconfigure data store credentials.</span></span> <span data-ttu-id="60d12-303">예를 들어 [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="60d12-304">데이터 저장소 자격 증명을 설정할 수 있는 방법은 [자격 증명 및 보안 설정](#set-credentials-and-securityy) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60d12-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="60d12-305">업데이트</span><span class="sxs-lookup"><span data-stu-id="60d12-305">Update</span></span>
<span data-ttu-id="60d12-306">기본적으로 최신 버전의 hello 게이트웨이 사용할 수 있는 데이터 관리 게이트웨이가 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-306">By default, data management gateway is automatically updated when a newer version of hello gateway is available.</span></span> <span data-ttu-id="60d12-307">hello 게이트웨이 모든 hello 예약 된 작업은 완료 될 때까지 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-307">hello gateway is not updated until all hello scheduled tasks are done.</span></span> <span data-ttu-id="60d12-308">Hello 업데이트 작업이 완료 될 때까지 hello 게이트웨이에서 더 이상 작업이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-308">No further tasks are processed by hello gateway until hello update operation is completed.</span></span> <span data-ttu-id="60d12-309">Hello 업데이트가 실패 하면 게이트웨이 롤백됩니다 toohello 이전 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-309">If hello update fails, gateway is rolled back toohello old version.</span></span>

<span data-ttu-id="60d12-310">예약 된 hello 업데이트 시간 hello 위치 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-310">You see hello scheduled update time in hello following places:</span></span>

* <span data-ttu-id="60d12-311">hello Azure 포털의에서 hello 게이트웨이 속성 페이지.</span><span class="sxs-lookup"><span data-stu-id="60d12-311">hello gateway properties page in hello Azure portal.</span></span>
* <span data-ttu-id="60d12-312">Hello 데이터 관리 게이트웨이 구성 관리자의 홈 페이지</span><span class="sxs-lookup"><span data-stu-id="60d12-312">Home page of hello Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="60d12-313">시스템 트레이 알림 메시지</span><span class="sxs-lookup"><span data-stu-id="60d12-313">System tray notification message.</span></span>

<span data-ttu-id="60d12-314">hello 데이터 관리 게이트웨이 구성 관리자의 홈 탭 hello 일정을 업데이트 하는 hello를 표시 하 고 hello 마지막 시간 hello 게이트웨이 설치/업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-314">hello Home tab of hello Data Management Gateway Configuration Manager displays hello update schedule and hello last time hello gateway was installed/updated.</span></span>

![업데이트를 예약](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="60d12-316">Hello 업데이트 즉시 설치 또는 hello 게이트웨이 toobe hello 예약 된 시간에 자동으로 업데이트할 때까지 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-316">You can install hello update right away or wait for hello gateway toobe automatically updated at hello scheduled time.</span></span> <span data-ttu-id="60d12-317">다음 이미지에서는 알림 메시지에에서 표시 된 hello 업데이트 단추를 클릭할 수 있는 tooinstall 함께 hello 게이트웨이 구성 관리자 것 바로 hello hello 예를 들어</span><span class="sxs-lookup"><span data-stu-id="60d12-317">For example, hello following image shows you hello notification message shown in hello Gateway Configuration Manager along with hello Update button that you can click tooinstall it immediately.</span></span>

![DMG 구성 관리자에서 업데이트](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="60d12-319">다음 이미지는 hello와 같이 hello 시스템 트레이에서 hello 알림 메시지 형태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-319">hello notification message in hello system tray would look as shown in hello following image:</span></span>

![시스템 트레이 메시지](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="60d12-321">업데이트 작업 (수동 또는 자동) hello 시스템 트레이에서 hello 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-321">You see hello status of update operation (manual or automatic) in hello system tray.</span></span> <span data-ttu-id="60d12-322">너무 링크와 함께 업데이트 되었습니다 그 hello 게이트웨이가 알림 hello에 대 한 메시지 참조 다음에 게이트웨이 구성 관리자를 시작할 때[새 주제 이란](data-factory-gateway-release-notes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-322">When you launch Gateway Configuration Manager next time, you see a message on hello notification bar that hello gateway has been updated along with a link too[what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="toodisableenable-auto-update-feature"></a><span data-ttu-id="60d12-323">자동 업데이트 기능을 toodisable/사용</span><span class="sxs-lookup"><span data-stu-id="60d12-323">toodisable/enable auto-update feature</span></span>
<span data-ttu-id="60d12-324">있습니다 수 사용/사용 안함 hello 자동 업데이트 기능은 hello 다음 단계를 수행 하 여:</span><span class="sxs-lookup"><span data-stu-id="60d12-324">You can disable/enable hello auto-update feature by doing hello following steps:</span></span>

<span data-ttu-id="60d12-325">[단일 노드 게이트웨이의 경우]</span><span class="sxs-lookup"><span data-stu-id="60d12-325">[For single node gateway]</span></span>
1. <span data-ttu-id="60d12-326">Hello 게이트웨이 컴퓨터에서 Windows PowerShell을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-326">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="60d12-327">Toohello C:\Program Files\Microsoft 데이터 관리 Gateway\2.0\PowerShellScript 폴더를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-327">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="60d12-328">다음 명령은 tooturn hello 자동 업데이트 실행된 hello (해제) 해제 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-328">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="60d12-329">다시 tooturn:</span><span class="sxs-lookup"><span data-stu-id="60d12-329">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="60d12-330">[[다중 노드 고가용성 및 확장 가능 게이트웨이(미리 보기)의 경우](data-factory-data-management-gateway-high-availability-scalability.md)]</span><span class="sxs-lookup"><span data-stu-id="60d12-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="60d12-331">Hello 게이트웨이 컴퓨터에서 Windows PowerShell을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-331">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="60d12-332">Toohello C:\Program Files\Microsoft 데이터 관리 Gateway\2.0\PowerShellScript 폴더를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-332">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="60d12-333">다음 명령은 tooturn hello 자동 업데이트 실행된 hello (해제) 해제 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-333">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="60d12-334">고가용성 기능(미리 보기)이 있는 게이트웨이의 경우 추가 AuthKey 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="60d12-335">다시 tooturn:</span><span class="sxs-lookup"><span data-stu-id="60d12-335">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
<span data-ttu-id="60d12-336">Hello 게이트웨이 컴퓨터와에서 다른 컴퓨터에서 hello 포털에 액세스 하는 경우 자격 증명 관리자 응용 프로그램 hello toohello 게이트웨이 컴퓨터에 연결할 수 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-336">If you access hello portal from a machine that is different from hello gateway machine, you must make sure that hello Credentials Manager application can connect toohello gateway machine.</span></span> <span data-ttu-id="60d12-337">Hello 응용 프로그램 hello 게이트웨이 컴퓨터에 연결할 수 없으면, 수 없습니다 하면 hello 데이터 원본과 tootest 연결 toohello 데이터 원본에 대 한 tooset 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-337">If hello application cannot reach hello gateway machine, it does not allow you tooset credentials for hello data source and tootest connection toohello data source.</span></span>  

<span data-ttu-id="60d12-338">Hello를 사용 하는 경우 **자격 증명 설정** 응용 프로그램을 hello 포털 hello 자격 증명 hello에 지정 된 hello 인증서로 암호화 **인증서** hello 탭 **게이트웨이 Configuration Manager** hello 게이트웨이 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-338">When you use hello **Setting Credentials** application, hello portal encrypts hello credentials with hello certificate specified in hello **Certificate** tab of hello **Gateway Configuration Manager** on hello gateway machine.</span></span>

<span data-ttu-id="60d12-339">Hello 자격 증명을 암호화 하기 위한 API 기반 방법을 찾고 hello를 사용할 수 있습니다 [새로 AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-339">If you are looking for an API-based approach for encrypting hello credentials, you can use hello [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt credentials.</span></span> <span data-ttu-id="60d12-340">hello cmdlet hello 인증서 해당 게이트웨이 구성 된 toouse tooencrypt hello 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-340">hello cmdlet uses hello certificate that gateway is configured toouse tooencrypt hello credentials.</span></span> <span data-ttu-id="60d12-341">암호화 된 자격 증명 toohello 추가 **EncryptedCredential** hello의 요소 **connectionString** hello JSON에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-341">You add encrypted credentials toohello **EncryptedCredential** element of hello **connectionString** in hello JSON.</span></span> <span data-ttu-id="60d12-342">JSON hello를 사용 하 여 hello로 [새로 AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet 또는 hello 데이터 팩터리 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-342">You use hello JSON with hello [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in hello Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="60d12-343">데이터 팩터리 편집기를 사용하여 자격 증명을 설정할 수 있는 방법이 한 가지 더 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="60d12-344">연결 된 SQL 서버를 만든 경우 hello 편집기를 사용 하 여 서비스 자격 증명을 일반 텍스트로 입력, hello 자격 증명 hello 데이터 팩터리 서비스를 소유 하는 인증서를 사용 하 여 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-344">If you create a SQL Server linked service by using hello editor and you enter credentials in plain text, hello credentials are encrypted using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="60d12-345">해당 게이트웨이 구성 된 toouse hello 인증서를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-345">It does NOT use hello certificate that gateway is configured toouse.</span></span> <span data-ttu-id="60d12-346">경우에 따라 이 방법은 약간 빠를 수 있는 반면에 안전성이 떨어집니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="60d12-347">따라서 개발/테스트 목적에 대해서만이 방법을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="60d12-348">PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="60d12-348">PowerShell cmdlets</span></span>
<span data-ttu-id="60d12-349">이 섹션에서는 설명 방법을 toocreate 및 Azure PowerShell cmdlet을 사용 하 여 게이트웨이 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-349">This section describes how toocreate and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="60d12-350">**Azure PowerShell**을 관리자 모드로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="60d12-351">실행 하 여 Azure 계정 tooyour 로그인 hello 명령 하 고 Azure 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-351">Log in tooyour Azure account by running hello following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="60d12-352">사용 하 여 hello **새로 AzureRmDataFactoryGateway** cmdlet toocreate 다음과 같이 논리적 게이트웨이:</span><span class="sxs-lookup"><span data-stu-id="60d12-352">Use hello **New-AzureRmDataFactoryGateway** cmdlet toocreate a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="60d12-353">**예제 명령 및 출력**:</span><span class="sxs-lookup"><span data-stu-id="60d12-353">**Example command and output**:</span></span>

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. <span data-ttu-id="60d12-354">Azure PowerShell에서 전환 toohello 폴더: **C:\Program Files\Microsoft 데이터 관리 Gateway\2.0\PowerShellScript\**합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-354">In Azure PowerShell, switch toohello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="60d12-355">실행 **RegisterGateway.ps1** hello 지역 변수 연관 **$Key** 다음 명령을 hello와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-355">Run **RegisterGateway.ps1** associated with hello local variable **$Key** as shown in hello following command.</span></span> <span data-ttu-id="60d12-356">이 스크립트는 이전에 만들 hello 논리 게이트웨이가 설치 된 컴퓨터에 설치 된 hello 클라이언트 에이전트를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-356">This script registers hello client agent installed on your machine with hello logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="60d12-357">Hello IsRegisterOnRemoteMachine 매개 변수를 사용 하 여 원격 컴퓨터에서 hello 게이트웨이 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-357">You can register hello gateway on a remote machine by using hello IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="60d12-358">예제:</span><span class="sxs-lookup"><span data-stu-id="60d12-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="60d12-359">Hello를 사용할 수 있습니다 **Get AzureRmDataFactoryGateway** data factory에는 게이트웨이 cmdlet tooget hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-359">You can use hello **Get-AzureRmDataFactoryGateway** cmdlet tooget hello list of Gateways in your data factory.</span></span> <span data-ttu-id="60d12-360">Hello 때 **상태** 표시 **온라인**, 게이트웨이가 준비 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-360">When hello **Status** shows **online**, it means your gateway is ready toouse.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="60d12-361">Hello를 사용 하 여 게이트웨이 제거할 수 있습니다 **제거 AzureRmDataFactoryGateway** hello를 사용 하 여 게이트웨이에 대 한 cmdlet 및 업데이트 설명 **집합 AzureRmDataFactoryGateway** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="60d12-361">You can remove a gateway using hello **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using hello **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="60d12-362">이러한 cmdlet에 대한 구문 및 기타 세부 정보는 데이터 팩터리 Cmdlet 참조를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60d12-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="60d12-363">PowerShell을 사용하여 게이트웨이 나열</span><span class="sxs-lookup"><span data-stu-id="60d12-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="60d12-364">PowerShell을 사용하여 게이트웨이 제거</span><span class="sxs-lookup"><span data-stu-id="60d12-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="60d12-365">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60d12-365">Next steps</span></span>
* <span data-ttu-id="60d12-366">[온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60d12-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="60d12-367">Hello 연습 hello 게이트웨이 toomove 데이터는 온-프레미스 SQL Server 데이터베이스 tooan Azure blob에서 사용 하는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60d12-367">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span>  
