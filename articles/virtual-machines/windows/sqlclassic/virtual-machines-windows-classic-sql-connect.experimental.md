---
title: "Azure에서 SQL Server 가상 컴퓨터에 연결(클래식) | Microsoft Docs"
description: "Azure의 가상 컴퓨터에서 실행되는 SQL Server에 연결하는 방법을 알아봅니다. 이 항목에서는 클래식 배포 모드를 사용합니다. 시나리오는 네트워킹 구성 및 클라이언트의 위치에 따라 다릅니다."
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
ms.openlocfilehash: 67b328cb754e49fe1dea9d57f74dd31793acd93c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-a-sql-server-virtual-machine-on-azure-classic-deployment"></a><span data-ttu-id="0b182-105">Azure에서 SQL Server 가상 컴퓨터 연결(클래식 배포)</span><span class="sxs-lookup"><span data-stu-id="0b182-105">Connect to a SQL Server Virtual Machine on Azure (Classic Deployment)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b182-106">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="0b182-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="0b182-107">클래식</span><span class="sxs-lookup"><span data-stu-id="0b182-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="0b182-108">개요</span><span class="sxs-lookup"><span data-stu-id="0b182-108">Overview</span></span>
<span data-ttu-id="0b182-109">이 항목에서는 Azure 가상 컴퓨터에서 실행되는 SQL Server 인스턴스에 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-109">This topic describes how to connect to your SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="0b182-110">여기서는 몇 가지 [일반 연결 시나리오](#connection-scenarios)를 다룬 다음 [Azure VM에서 SQL Server 연결을 구성하기 위한 상세 단계](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0b182-111">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0b182-112">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-112">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="0b182-113">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-113">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="0b182-114">Resource Manager VM을 사용하는 경우 [Azure에서 Resource Manager를 사용하여 SQL Server 가상 컴퓨터에 연결](../sql/virtual-machines-windows-sql-connect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b182-114">If you are using Resource Manager VMs, see [Connect to a SQL Server Virtual Machine on Azure using Resource Manager](../sql/virtual-machines-windows-sql-connect.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="0b182-115">연결 시나리오</span><span class="sxs-lookup"><span data-stu-id="0b182-115">Connection scenarios</span></span>
<span data-ttu-id="0b182-116">클라이언트가 가상 컴퓨터를 실행 중인 SQL Server에 연결하는 방법은 클라이언트의 위치 및 컴퓨터/네트워킹 구성에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-116">The way a client connects to SQL Server running on a Virtual Machine differs depending on the location of the client and the machine/networking configuration.</span></span> <span data-ttu-id="0b182-117">이 시나리오에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-117">These scenarios include:</span></span>

* [<span data-ttu-id="0b182-118">동일한 클라우드 서비스의 SQL Server에 연결</span><span class="sxs-lookup"><span data-stu-id="0b182-118">Connect to SQL Server in the same cloud service</span></span>](#connect-to-sql-server-in-the-same-cloud-service)
* [<span data-ttu-id="0b182-119">인터넷을 통해 SQL Server에 연결</span><span class="sxs-lookup"><span data-stu-id="0b182-119">Connect to SQL Server over the internet</span></span>](#connect-to-sql-server-over-the-internet)
* [<span data-ttu-id="0b182-120">동일한 가상 네트워크의 SQL Server에 연결</span><span class="sxs-lookup"><span data-stu-id="0b182-120">Connect to SQL Server in the same virtual network</span></span>](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> <span data-ttu-id="0b182-121">이러한 방법으로 연결하기 전에 [이 문서의 단계에 따라 연결을 구성](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-121">Before you connect with any of these methods, you must follow the [steps in this article to configure connectivity](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>
> 
> 

### <a name="connect-to-sql-server-in-the-same-cloud-service"></a><span data-ttu-id="0b182-122">동일한 클라우드 서비스의 SQL Server에 연결</span><span class="sxs-lookup"><span data-stu-id="0b182-122">Connect to SQL Server in the same cloud service</span></span>
<span data-ttu-id="0b182-123">한 클라우드 서비스에 여러 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-123">Multiple virtual machines can be created in the same cloud service.</span></span> <span data-ttu-id="0b182-124">가상 컴퓨터 시나리오를 이해하려면 [가상 컴퓨터를 가상 네트워크 또는 클라우드 서비스와 연결하는 방법](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b182-124">To understand this virtual machines scenario, see [How to connect virtual machines with a virtual network or cloud service](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service).</span></span> <span data-ttu-id="0b182-125">이 시나리오에서 한 가상 컴퓨터의 클라이언트는 동일한 클라우드 서비스의 다른 가상 컴퓨터에서 실행 중인 SQL Server에 연결하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-125">In this scenario, a client on one virtual machine attempts to connect to SQL Server running on another virtual machine in the same cloud service.</span></span>

<span data-ttu-id="0b182-126">이 시나리오에서는 VM **이름**(포털에 **컴퓨터 이름** 또는 **호스트 이름**으로도 표시됨)을 사용하여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-126">In this scenario, you can connect using the VM **Name** (also shown as **Computer Name** or **hostname** in the portal).</span></span> <span data-ttu-id="0b182-127">이 이름은 VM을 만들 때 제공된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-127">This is the name you provided for the VM during creation.</span></span> <span data-ttu-id="0b182-128">예를 들어 SQL VM 이름을 **mysqlvm**으로 지정하면 동일한 클라우드 서비스의 클라이언트 VM은 다음 연결 문자열을 사용하여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-128">For example, if you named your SQL VM **mysqlvm**, a client VM in the same cloud service could use the following connection string to connect:</span></span>

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-to-sql-server-over-the-internet"></a><span data-ttu-id="0b182-129">인터넷을 통해 SQL Server에 연결 </span><span class="sxs-lookup"><span data-stu-id="0b182-129">Connect to SQL Server over the Internet</span></span>
<span data-ttu-id="0b182-130">인터넷을 통해 SQL Server 데이터베이스 엔진에 연결할 경우 들어오는 TCP 통신에 대해 가상 컴퓨터 끝점을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-130">If you want to connect to your SQL Server database engine from the Internet, you must create a virtual machine endpoint for incoming TCP communication.</span></span> <span data-ttu-id="0b182-131">이 Azure 구성 단계에서는 들어오는 TCP 포트 트래픽을 가상 컴퓨터에 액세스 가능한 TCP 포트로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-131">This Azure configuration step, directs incoming TCP port traffic to a TCP port that is accessible to the virtual machine.</span></span>

<span data-ttu-id="0b182-132">인터넷을 통해 연결하려면 VM의 DNS 이름 및 VM 끝점 포트 번호(이 문서 뒷부분에서 구성)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-132">To connect over the internet, you must use the VM's DNS name and the VM endpoint port number (configured later in this article).</span></span> <span data-ttu-id="0b182-133">DNS 이름을 찾으려면 Azure Portal로 이동하고 **가상 컴퓨터(클래식)** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-133">To find the DNS Name, navigate to the Azure portal, and select **Virtual machines (classic)**.</span></span> <span data-ttu-id="0b182-134">그런 다음 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-134">Then select your virtual machine.</span></span> <span data-ttu-id="0b182-135">**DNS 이름**이 **개요** 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-135">The **DNS name** is shown in the **Overview** section.</span></span>

<span data-ttu-id="0b182-136">예를 들어 이름이 **mysqlvm**, DNS 이름이 **mysqlvm7777.cloudapp.net**이고 VM 끝점이 **57500**인 클래식 가상 컴퓨터를 고려해보세요.</span><span class="sxs-lookup"><span data-stu-id="0b182-136">For example, consider a classic virtual machine named **mysqlvm** with a DNS Name of **mysqlvm7777.cloudapp.net** and a VM endpoint of **57500**.</span></span> <span data-ttu-id="0b182-137">올바르게 구성된 연결이라고 가정할 경우 다음 연결 문자열을 사용하여 인터넷의 어디에서든지 가상 컴퓨터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-137">Assuming properly configured connectivity, the following connection string could be used to access the virtual machine from anywhere on the internet:</span></span>

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

<span data-ttu-id="0b182-138">이 연결 문자열은 인터넷을 통한 클라이언트의 연결이 사용하도록 설정하지만 누구나 SQL Server에 연결할 수 있다는 뜻은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-138">Although this connection string enables connectivity for clients over the internet, this does not imply that anyone can connect to your SQL Server.</span></span> <span data-ttu-id="0b182-139">외부 클라이언트는 정확한 사용자 이름과 암호가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-139">Outside clients have to the correct username and password.</span></span> <span data-ttu-id="0b182-140">보안을 높이기 위해 잘 알려진 포트 1433은 공용 가상 컴퓨터 끝점으로 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-140">For additional security, don't use the well-known port 1433 for the public virtual machine endpoint.</span></span> <span data-ttu-id="0b182-141">또한 가능하다면 끝점에 ACL을 추가하여 트래픽을 허용한 클라이언트로  한정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-141">And if possible, consider adding an ACL on your endpoint to restrict traffic only to the clients you permit.</span></span> <span data-ttu-id="0b182-142">끝점에서 ACL을 사용하는 방법에 대한 지침은 [끝점에 대한 ACL 관리](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b182-142">For instructions on using ACLs with endpoints, see [Manage the ACL on an endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

> [!NOTE]
> <span data-ttu-id="0b182-143">이 방법을 사용하여 SQL Server와 통신하는 경우 Azure 데이터 센터에서 보내는 모든 데이터에는 일반적으로 [아웃바운드 데이터 전송 가격](https://azure.microsoft.com/pricing/details/data-transfers/)이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-143">When you use this technique to communicate with SQL Server, all outgoing data from the Azure datacenter is subject to normal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>
> 
> 

### <a name="connect-to-sql-server-in-the-same-virtual-network"></a><span data-ttu-id="0b182-144">동일한 가상 네트워크의 SQL Server에 연결</span><span class="sxs-lookup"><span data-stu-id="0b182-144">Connect to SQL Server in the same virtual network</span></span>
<span data-ttu-id="0b182-145">[가상 네트워크](../../../virtual-network/virtual-networks-overview.md) 에서는 추가적인 시나리오가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-145">[Virtual Network](../../../virtual-network/virtual-networks-overview.md) enables additional scenarios.</span></span> <span data-ttu-id="0b182-146">VM이 다른 클라우드 서비스에 있더라도 동일한 가상 네트워크의 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-146">You can connect VMs in the same virtual network, even if those VMs exist in different cloud services.</span></span> <span data-ttu-id="0b182-147">또한 [사이트 간 VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)을 통해 온-프레미스 네트워크와 컴퓨터에 VM을 연결하는 하이브리드 아키텍처를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-147">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="0b182-148">가상 네트워크를 사용하면 Azure VM을 도메인에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-148">Virtual networks also enable you to join your Azure VMs to a domain.</span></span> <span data-ttu-id="0b182-149">도메인에 연결하는 것이 SQL Server에 Windows 인증을 사용하는 유일한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-149">Joining to a domain is the only way to use Windows Authentication with SQL Server.</span></span> <span data-ttu-id="0b182-150">다른 연결 시나리오의 경우 사용자 이름과 암호가 있는 SQL 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-150">The other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="0b182-151">도메인 환경과 Windows 인증을 구성하려는 경우 공용 끝점이나 SQL 인증 및 로그인을 구성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-151">If you plan to configure a domain environment and Windows Authentication, you do not need to configure the public endpoint or the SQL Authentication and logins.</span></span> <span data-ttu-id="0b182-152">이 시나리오에서는 연결 문자열에 SQL Server VM 이름을 지정하여 SQL Server에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-152">In this scenario, you can connect to your SQL Server instance by specifying the SQL Server VM name in the connection string.</span></span> <span data-ttu-id="0b182-153">다음 예에서는 Windows 인증도 구성되었고 사용자에게 SQL Server 인스턴스에 대한 액세스 권한이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-153">The following example assumes that Windows Authentication was configured and that the user was granted access to the SQL Server instance.</span></span>

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a><span data-ttu-id="0b182-154">Azure VM에서 SQL Server 연결을 구성하기 위한 단계</span><span class="sxs-lookup"><span data-stu-id="0b182-154">Steps for configuring SQL Server connectivity in an Azure VM</span></span>
<span data-ttu-id="0b182-155">다음 단계는 SQL Server Management Studio (SSMS)를 사용하여 인터넷을 통해 SQL Server 인스턴스에 연결하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-155">The following steps demonstrate how to connect to the SQL Server instance over the internet using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="0b182-156">그러나 동일한 단계는 온-프레미스 및 Azure에서 실행중인 응용 프로그램에 대해 SQL Server 가상 컴퓨터를 액세스할 수 있게 만들도록 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-156">However, the same steps apply to making your SQL Server virtual machine accessible for your applications, running both on-premises and in Azure.</span></span>

<span data-ttu-id="0b182-157">인터넷 또는 다른 VM에서 SQL Server의 인스턴스에 연결하기 전에 먼저 다음 작업을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-157">Before you can connect to the instance of SQL Server from another VM or the internet, you must complete the following tasks:</span></span>

* [<span data-ttu-id="0b182-158">가상 컴퓨터에 대한 TCP 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="0b182-158">Create a TCP endpoint for the virtual machine</span></span>](#create-a-tcp-endpoint-for-the-virtual-machine)
* [<span data-ttu-id="0b182-159">Windows 방화벽에서 TCP 포트 열기</span><span class="sxs-lookup"><span data-stu-id="0b182-159">Open TCP ports in the Windows firewall</span></span>](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [<span data-ttu-id="0b182-160">TCP 프로토콜에서 수신하도록 SQL Server 구성</span><span class="sxs-lookup"><span data-stu-id="0b182-160">Configure SQL Server to listen on the TCP protocol</span></span>](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [<span data-ttu-id="0b182-161">혼합된 모드 인증에 대한 SQL Server 구성</span><span class="sxs-lookup"><span data-stu-id="0b182-161">Configure SQL Server for mixed mode authentication</span></span>](#configure-sql-server-for-mixed-mode-authentication)
* [<span data-ttu-id="0b182-162">SQL Server 인증 로그인 만들기</span><span class="sxs-lookup"><span data-stu-id="0b182-162">Create SQL Server authentication logins</span></span>](#create-sql-server-authentication-logins)
* [<span data-ttu-id="0b182-163">가상 컴퓨터의 DNS 이름 확인</span><span class="sxs-lookup"><span data-stu-id="0b182-163">Determine the DNS name of the virtual machine</span></span>](#determine-the-dns-name-of-the-virtual-machine)
* [<span data-ttu-id="0b182-164">다른 컴퓨터에서 데이터베이스 엔진에 연결</span><span class="sxs-lookup"><span data-stu-id="0b182-164">Connect to the Database Engine from another computer</span></span>](#connect-to-the-database-engine-from-another-computer)

<span data-ttu-id="0b182-165">연결 경로는 다음 다이어그램에 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-165">The connection path is summarized by the following diagram:</span></span>

![SQL Server 가상 컴퓨터에 연결](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect to SQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect to SQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect to SQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a><span data-ttu-id="0b182-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b182-167">Next Steps</span></span>
<span data-ttu-id="0b182-168">고가용성 및 재해 복구를 위해 AlwaysOn 가용성 그룹도 사용하려는 경우 수신기의 구현을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-168">If you are also planning to use AlwaysOn Availability Groups for high availability and disaster recovery, you should consider implementing a listener.</span></span> <span data-ttu-id="0b182-169">데이터베이스 클라이언트는 SQL Server 인스턴스 중 하나에 직접 연결하기 보다는 수신기에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-169">Database clients connect to the listener rather than directly to one of the SQL Server instances.</span></span> <span data-ttu-id="0b182-170">수신기는 가용성 그룹의 주 복제본에 클라이언트를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-170">The listener routes clients to the primary replica in the availability group.</span></span> <span data-ttu-id="0b182-171">자세한 내용은 [Azure에서 AlwaysOn 가용성 그룹에 대한 ILB 수신기 구성](../classic/ps-sql-int-listener.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b182-171">For more information, see [Configure an ILB listener for AlwaysOn Availability Groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="0b182-172">Azure 가상 컴퓨터에서 실행되는 SQL Server에 대한 모든 보안 모범 사례를 반드시 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-172">It is important to review all the security best practices for SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="0b182-173">자세한 내용은 [Azure 가상 컴퓨터의 SQL Server에 대한 보안 고려 사항](../sql/virtual-machines-windows-sql-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b182-173">For more information, see [Security Considerations for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-security.md).</span></span>

<span data-ttu-id="0b182-174">[학습 경로를 탐색](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b182-174">[Explore the Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span></span> 

<span data-ttu-id="0b182-175">Azure VM에서의 SQL Server 실행에 관한 다른 항목은 [Azure 가상 컴퓨터의 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b182-175">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

