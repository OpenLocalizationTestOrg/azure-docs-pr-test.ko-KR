---
title: "aaaConnect tooa (클래식) Azure에서 SQL Server 가상 컴퓨터 | Microsoft Docs"
description: "자세한 내용은 방법 tooconnect tooSQL 서버 Azure에서 가상 컴퓨터에서 실행 합니다. 이 항목에서는 hello 클래식 배포 모델을 사용 합니다. hello 시나리오 hello 네트워킹 구성 및 hello 클라이언트의 hello 위치에 따라 다릅니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 4fff3936ad0bcfd3a56855a8436991e19b92522b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a><span data-ttu-id="bf4d8-105">Tooa (클래식 배포) Azure에서 SQL Server 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-105">Connect tooa SQL Server Virtual Machine on Azure (Classic Deployment)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf4d8-106">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="bf4d8-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="bf4d8-107">클래식</span><span class="sxs-lookup"><span data-stu-id="bf4d8-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="bf4d8-108">개요</span><span class="sxs-lookup"><span data-stu-id="bf4d8-108">Overview</span></span>
<span data-ttu-id="bf4d8-109">이 항목에서는 tooconnect tooyour SQL Server 인스턴스는 Azure 가상 컴퓨터에서 실행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-109">This topic describes how tooconnect tooyour SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="bf4d8-110">여기서는 몇 가지 [일반 연결 시나리오](#connection-scenarios)를 다룬 다음 [Azure VM에서 SQL Server 연결을 구성하기 위한 상세 단계](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="bf4d8-111">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bf4d8-112">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-112">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="bf4d8-113">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="bf4d8-114">리소스 관리자 Vm을 사용 하는 경우 참조 [tooa 리소스 관리자를 사용 하 여 Azure에서 SQL Server 가상 컴퓨터를 연결](../sql/virtual-machines-windows-sql-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-114">If you are using Resource Manager VMs, see [Connect tooa SQL Server Virtual Machine on Azure using Resource Manager](../sql/virtual-machines-windows-sql-connect.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="bf4d8-115">연결 시나리오</span><span class="sxs-lookup"><span data-stu-id="bf4d8-115">Connection scenarios</span></span>
<span data-ttu-id="bf4d8-116">hello 방식으로 클라이언트 tooSQL hello 클라이언트와 hello 컴퓨터/네트워킹 구성의 hello 위치에 따라 달라 집니다 가상 컴퓨터에서 실행 중인 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-116">hello way a client connects tooSQL Server running on a Virtual Machine differs depending on hello location of hello client and hello machine/networking configuration.</span></span> <span data-ttu-id="bf4d8-117">이 시나리오에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-117">These scenarios include:</span></span>

* [<span data-ttu-id="bf4d8-118">연결 tooSQL 서버 hello에 동일한 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="bf4d8-118">Connect tooSQL Server in hello same cloud service</span></span>](#connect-to-sql-server-in-the-same-cloud-service)
* [<span data-ttu-id="bf4d8-119">TooSQL 서버 hello 통해 연결 인터넷</span><span class="sxs-lookup"><span data-stu-id="bf4d8-119">Connect tooSQL Server over hello internet</span></span>](#connect-to-sql-server-over-the-internet)
* [<span data-ttu-id="bf4d8-120">연결 tooSQL 서버 hello에 동일한 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="bf4d8-120">Connect tooSQL Server in hello same virtual network</span></span>](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> <span data-ttu-id="bf4d8-121">이러한 메서드를 사용 하 여 연결 하기 전에 hello 따라야 [이 문서 tooconfigure 연결의 단계를](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-121">Before you connect with any of these methods, you must follow hello [steps in this article tooconfigure connectivity](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a><span data-ttu-id="bf4d8-122">연결 tooSQL 서버 hello에 동일한 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="bf4d8-122">Connect tooSQL Server in hello same cloud service</span></span>
<span data-ttu-id="bf4d8-123">여러 가상 컴퓨터에서에서 만들 수 있습니다 hello 동일한 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-123">Multiple virtual machines can be created in hello same cloud service.</span></span> <span data-ttu-id="bf4d8-124">toounderstand이 가상 컴퓨터 시나리오에서는 참조 [어떻게 tooconnect 가상 컴퓨터 가상 네트워크 또는 클라우드 서비스와](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-124">toounderstand this virtual machines scenario, see [How tooconnect virtual machines with a virtual network or cloud service](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service).</span></span> <span data-ttu-id="bf4d8-125">이 시나리오는 하나의 가상 컴퓨터에서 실행 중인 tooconnect tooSQL 서버 시도 하면 hello에 다른 가상 컴퓨터에서 동일한 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-125">This scenario is when a client on one virtual machine attempts tooconnect tooSQL Server running on another virtual machine in hello same cloud service.</span></span>

<span data-ttu-id="bf4d8-126">이 시나리오에서는 연결할 수 있습니다 VM hello를 사용 하 여 **이름** (표시 **컴퓨터 이름** 또는 **호스트 이름** hello 포털에서).</span><span class="sxs-lookup"><span data-stu-id="bf4d8-126">In this scenario, you can connect using hello VM **Name** (also shown as **Computer Name** or **hostname** in hello portal).</span></span> <span data-ttu-id="bf4d8-127">만드는 동안 hello VM에 대해 제공한 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-127">This is hello name you provided for hello VM during creation.</span></span> <span data-ttu-id="bf4d8-128">예를 들어, SQL VM의 이름을 **mysqlvm**, hello 동일한 클라우드 서비스를 사용할 수 있는 클라이언트 VM 다음 연결 문자열 tooconnect hello:</span><span class="sxs-lookup"><span data-stu-id="bf4d8-128">For example, if you named your SQL VM **mysqlvm**, a client VM in hello same cloud service could use hello following connection string tooconnect:</span></span>

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a><span data-ttu-id="bf4d8-129">TooSQL 서버 hello 인터넷을 통해 연결</span><span class="sxs-lookup"><span data-stu-id="bf4d8-129">Connect tooSQL Server over hello Internet</span></span>
<span data-ttu-id="bf4d8-130">원하는 tooconnect tooyour SQL Server 데이터베이스 엔진 hello 인터넷에서에서 들어오는 TCP 통신에 대 한 가상 컴퓨터 끝점을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-130">If you want tooconnect tooyour SQL Server database engine from hello Internet, you must create a virtual machine endpoint for incoming TCP communication.</span></span> <span data-ttu-id="bf4d8-131">이 Azure 구성 단계에서는 들어오는 TCP 포트 트래픽을 tooa TCP 포트를 액세스할 수 있는 toohello 가상 컴퓨터가 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-131">This Azure configuration step, directs incoming TCP port traffic tooa TCP port that is accessible toohello virtual machine.</span></span>

<span data-ttu-id="bf4d8-132">통해 tooconnect hello 인터넷 hello VM의 DNS 이름 및 hello VM 끝점 포트 번호 (이 문서의 뒷부분에 나오는 구성)를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-132">tooconnect over hello internet, you must use hello VM's DNS name and hello VM endpoint port number (configured later in this article).</span></span> <span data-ttu-id="bf4d8-133">toofind hello DNS 이름 toohello Azure 포털에서 선택한 탐색 **가상 컴퓨터 (클래식)**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-133">toofind hello DNS Name, navigate toohello Azure portal, and select **Virtual machines (classic)**.</span></span> <span data-ttu-id="bf4d8-134">그런 다음 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-134">Then select your virtual machine.</span></span> <span data-ttu-id="bf4d8-135">hello **DNS 이름** hello에 보여집니다 **개요** 섹션.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-135">hello **DNS name** is shown in hello **Overview** section.</span></span>

<span data-ttu-id="bf4d8-136">예를 들어 이름이 **mysqlvm**, DNS 이름이 **mysqlvm7777.cloudapp.net**이고 VM 끝점이 **57500**인 클래식 가상 컴퓨터를 고려해보세요.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-136">For example, consider a classic virtual machine named **mysqlvm** with a DNS Name of **mysqlvm7777.cloudapp.net** and a VM endpoint of **57500**.</span></span> <span data-ttu-id="bf4d8-137">올바르게 구성 된 연결을 가정할 hello 연결 문자열 뒤에 있을 수 어디에서 나 사용된 tooaccess hello 가상 컴퓨터 인터넷 hello:</span><span class="sxs-lookup"><span data-stu-id="bf4d8-137">Assuming properly configured connectivity, hello following connection string could be used tooaccess hello virtual machine from anywhere on hello internet:</span></span>

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

<span data-ttu-id="bf4d8-138">통해 클라이언트에 대 한 연결을 통해이 있지만 인터넷 hello, 것은 아닙니다 모든 사용자가 SQL Server tooyour 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-138">Although this enables connectivity for clients over hello internet, this does not imply that anyone can connect tooyour SQL Server.</span></span> <span data-ttu-id="bf4d8-139">클라이언트 외부 toohello 올바른 사용자 이름 및 암호가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-139">Outside clients have toohello correct username and password.</span></span> <span data-ttu-id="bf4d8-140">추가 보안을 위해 hello 공용 가상 컴퓨터 끝점에 대 한 hello 잘 알려진 포트 1433 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-140">For additional security, don't use hello well-known port 1433 for hello public virtual machine endpoint.</span></span> <span data-ttu-id="bf4d8-141">및 가능한 경우 허용할 끝점 toorestrict 트래픽만 toohello 클라이언트에는 ACL을 추가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-141">And if possible, consider adding an ACL on your endpoint toorestrict traffic only toohello clients you permit.</span></span> <span data-ttu-id="bf4d8-142">끝점 Acl을 사용 하 여, 참조 [끝점에서 ACL 관리 hello](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-142">For instructions on using ACLs with endpoints, see [Manage hello ACL on an endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

> [!NOTE]
> <span data-ttu-id="bf4d8-143">이 SQL Server와 함께이 기술을 toocommunicate를 사용할 때 모든 보내는 데이터를 hello Azure 데이터 센터 toonote 주체 toonormal 중요 [아웃 바운드 데이터 전송에 대 한 가격](https://azure.microsoft.com/pricing/details/data-transfers/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-143">It is important toonote that when you use this technique toocommunicate with SQL Server, all outgoing data from hello Azure datacenter is subject toonormal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a><span data-ttu-id="bf4d8-144">연결 tooSQL 서버 hello에 동일한 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="bf4d8-144">Connect tooSQL Server in hello same virtual network</span></span>
<span data-ttu-id="bf4d8-145">[가상 네트워크](../../../virtual-network/virtual-networks-overview.md) 에서는 추가적인 시나리오가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-145">[Virtual Network](../../../virtual-network/virtual-networks-overview.md) enables additional scenarios.</span></span> <span data-ttu-id="bf4d8-146">Hello 서로 다른 클라우드 서비스에 있는 동일한 가상 네트워크에서 이러한 경우에 Vm의에서 Vm에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-146">You can connect VMs in hello same virtual network, even if those VMs exist in different cloud services.</span></span> <span data-ttu-id="bf4d8-147">또한 [사이트 간 VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)을 통해 온-프레미스 네트워크와 컴퓨터에 VM을 연결하는 하이브리드 아키텍처를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-147">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="bf4d8-148">가상 네트워크는 또한 toojoin 하면 Azure Vm tooa 도메인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-148">Virtual networks also enables you toojoin your Azure VMs tooa domain.</span></span> <span data-ttu-id="bf4d8-149">이 hello 유일한 방법은 toouse Windows 인증 tooSQL 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-149">This is hello only way toouse Windows Authentication tooSQL Server.</span></span> <span data-ttu-id="bf4d8-150">hello 다른 연결 시나리오의 SQL 인증을 요구할 사용자 이름 및 암호.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-150">hello other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="bf4d8-151">Tooconfigure 도메인 환경 및 Windows 인증 하려는 경우에이 문서 tooconfigure hello 공용 끝점 또는 hello SQL 인증 로그인의 toouse hello 단계를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-151">If you are going tooconfigure a domain environment and Windows Authentication, you do not need toouse hello steps in this article tooconfigure hello public endpoint or hello SQL Authentication and logins.</span></span> <span data-ttu-id="bf4d8-152">이 시나리오에서는 hello 연결 문자열에 hello SQL Server VM 이름을 지정 하 여 tooyour SQL Server 인스턴스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-152">In this scenario, you can connect tooyour SQL Server instance by specifying hello SQL Server VM name in hello connection string.</span></span> <span data-ttu-id="bf4d8-153">다음 예에서는 hello Windows 인증도 구성 되어 있고 해당 hello 사용자 액세스 toohello SQL Server 인스턴스에 부여 받았는지 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-153">hello following example assumes that Windows Authentication has also been configured and that hello user has been granted access toohello SQL Server instance.</span></span>

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a><span data-ttu-id="bf4d8-154">Azure VM에서 SQL Server 연결을 구성하기 위한 단계</span><span class="sxs-lookup"><span data-stu-id="bf4d8-154">Steps for configuring SQL Server connectivity in an Azure VM</span></span>
<span data-ttu-id="bf4d8-155">단계를 수행 하는 hello tooconnect toohello SQL Server 인스턴스를 통해 SQL Server Management Studio (SSMS)를 사용 하 여 인터넷 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-155">hello following steps demonstrate how tooconnect toohello SQL Server instance over hello internet using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="bf4d8-156">그러나 hello 동일한 단계 적용 toomaking Azure 및 온-프레미스를 실행 중인 응용 프로그램에 액세스할 수 있는 SQL Server 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-156">However, hello same steps apply toomaking your SQL Server virtual machine accessible for your applications, running both on-premises and in Azure.</span></span>

<span data-ttu-id="bf4d8-157">다른 VM에서 SQL Server 인스턴스의 toohello 연결 하거나 인터넷 hello 하려면, 먼저 다음 hello 섹션에 설명 된 대로 작업을 수행 하는 hello를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-157">Before you can connect toohello instance of SQL Server from another VM or hello internet, you must complete hello following tasks as described in hello sections that follow:</span></span>

* [<span data-ttu-id="bf4d8-158">Hello 가상 컴퓨터에 대 한 TCP 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="bf4d8-158">Create a TCP endpoint for hello virtual machine</span></span>](#create-a-tcp-endpoint-for-the-virtual-machine)
* [<span data-ttu-id="bf4d8-159">Hello Windows 방화벽에서 TCP 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-159">Open TCP ports in hello Windows firewall</span></span>](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [<span data-ttu-id="bf4d8-160">SQL Server toolisten hello TCP 프로토콜에서 구성</span><span class="sxs-lookup"><span data-stu-id="bf4d8-160">Configure SQL Server toolisten on hello TCP protocol</span></span>](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [<span data-ttu-id="bf4d8-161">혼합된 모드 인증에 대한 SQL Server 구성</span><span class="sxs-lookup"><span data-stu-id="bf4d8-161">Configure SQL Server for mixed mode authentication</span></span>](#configure-sql-server-for-mixed-mode-authentication)
* [<span data-ttu-id="bf4d8-162">SQL Server 인증 로그인 만들기</span><span class="sxs-lookup"><span data-stu-id="bf4d8-162">Create SQL Server authentication logins</span></span>](#create-sql-server-authentication-logins)
* [<span data-ttu-id="bf4d8-163">Hello 가상 컴퓨터의 DNS 이름을 hello 결정</span><span class="sxs-lookup"><span data-stu-id="bf4d8-163">Determine hello DNS name of hello virtual machine</span></span>](#determine-the-dns-name-of-the-virtual-machine)
* [<span data-ttu-id="bf4d8-164">다른 컴퓨터에서 toohello 데이터베이스 엔진 연결</span><span class="sxs-lookup"><span data-stu-id="bf4d8-164">Connect toohello Database Engine from another computer</span></span>](#connect-to-the-database-engine-from-another-computer)

<span data-ttu-id="bf4d8-165">hello 연결 경로 hello 다이어그램을 다음으로 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-165">hello connection path is summarized by hello following diagram:</span></span>

![Tooa SQL Server 가상 컴퓨터 연결](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a><span data-ttu-id="bf4d8-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bf4d8-167">Next Steps</span></span>
<span data-ttu-id="bf4d8-168">고가용성 및 재해 복구를 위한 toouse AlwaysOn 가용성 그룹에도 계획 하는 경우 수신기를 구현 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-168">If you are also planning toouse AlwaysOn Availability Groups for high availability and disaster recovery, you should consider implementing a listener.</span></span> <span data-ttu-id="bf4d8-169">데이터베이스 클라이언트 toohello 수신기 하지 않고 직접 tooone hello SQL Server 인스턴스를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-169">Database clients connect toohello listener rather than directly tooone of hello SQL Server instances.</span></span> <span data-ttu-id="bf4d8-170">hello 수신기 경로 클라이언트 toohello 기본 hello 가용성 그룹의 복제본입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-170">hello listener routes clients toohello primary replica in hello availability group.</span></span> <span data-ttu-id="bf4d8-171">자세한 내용은 [Azure에서 AlwaysOn 가용성 그룹에 대한 ILB 수신기 구성](../classic/ps-sql-int-listener.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-171">For more information, see [Configure an ILB listener for AlwaysOn Availability Groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="bf4d8-172">모든 hello 보안 모범 사례는 Azure 가상 컴퓨터에서 실행 되는 SQL Server에 대 한 중요 한 tooreview 이며</span><span class="sxs-lookup"><span data-stu-id="bf4d8-172">It is important tooreview all of hello security best practices for SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="bf4d8-173">자세한 내용은 [Azure Virtual Machines의 SQL Server에 대한 보안 고려 사항](../sql/virtual-machines-windows-sql-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-173">For more information, see [Security Considerations for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-security.md).</span></span>

<span data-ttu-id="bf4d8-174">[Hello 학습 경로 탐색](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) Azure 가상 컴퓨터에 SQL Server에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-174">[Explore hello Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span></span> 

<span data-ttu-id="bf4d8-175">다른 항목은 서로 관련 toorunning Azure Vm에서 SQL Server에 대 한 참조 [Azure 가상 컴퓨터에 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d8-175">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

