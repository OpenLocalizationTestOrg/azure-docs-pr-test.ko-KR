---
title: "Azure의 SQL Server에 대 한 고려 사항 aaaSecurity | Microsoft Docs"
description: "이 항목에서는 Azure Virtual Machine에서 실행되는 SQL Server 보안에 대한 일반적인 지침을 제공합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a><span data-ttu-id="cb8b9-103">Azure 가상 컴퓨터의 SQL Server에 대한 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="cb8b9-103">Security Considerations for SQL Server in Azure Virtual Machines</span></span>

<span data-ttu-id="cb8b9-104">이 항목에는 Azure 가상 컴퓨터 (VM)에 대 한 보안 액세스 tooSQL 서버 인스턴스를 설정 하는 데 도움이 되는 전반적인 보안 지침이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-104">This topic includes overall security guidelines that help establish secure access tooSQL Server instances in an Azure virtual machine (VM).</span></span>

<span data-ttu-id="cb8b9-105">Azure는 몇 가지 산업 규정 및 표준을 사용할 수 있는 호환 되는 솔루션 toobuild 가상 컴퓨터에서 실행 중인 SQL Server를 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-105">Azure complies with several industry regulations and standards that can enable you toobuild a compliant solution with SQL Server running in a virtual machine.</span></span> <span data-ttu-id="cb8b9-106">Azure 규정 준수에 대한 자세한 내용은 [Azure 보안 센터](https://azure.microsoft.com/support/trust-center/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-106">For information about regulatory compliance with Azure, see [Azure Trust Center](https://azure.microsoft.com/support/trust-center/).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a><span data-ttu-id="cb8b9-107">컨트롤 액세스 toohello SQL VM</span><span class="sxs-lookup"><span data-stu-id="cb8b9-107">Control access toohello SQL VM</span></span>

<span data-ttu-id="cb8b9-108">SQL Server 가상 컴퓨터를 만들면 사용자 액세스 toohello 컴퓨터와 서버 tooSQL 누가 toocarefully을 제어 하는 방법을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-108">When you create your SQL Server virtual machine, consider how toocarefully control who has access toohello machine and tooSQL Server.</span></span> <span data-ttu-id="cb8b9-109">일반적으로 수행 해야 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="cb8b9-109">In general, you should do hello following:</span></span>

- <span data-ttu-id="cb8b9-110">액세스 tooSQL 서버 tooonly hello 응용 프로그램 및 필요로 하는 클라이언트를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-110">Restrict access tooSQL Server tooonly hello applications and clients that need it.</span></span>
- <span data-ttu-id="cb8b9-111">사용자 계정 및 암호를 관리하는 모범 사례를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-111">Follow best practices for managing user accounts and passwords.</span></span>

<span data-ttu-id="cb8b9-112">hello 다음 섹션에 이러한 요소를 고려 제안을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-112">hello following sections provide suggestions on thinking through these points.</span></span>

## <a name="secure-connections"></a><span data-ttu-id="cb8b9-113">보안 연결</span><span class="sxs-lookup"><span data-stu-id="cb8b9-113">Secure connections</span></span>

<span data-ttu-id="cb8b9-114">갤러리 이미지를 사용 하는 SQL Server 가상 컴퓨터를 만들 때 hello **SQL Server 연결** 옵션은 다양 한 hello **(VM) 내부의 로컬**, **개인 (가상 네트워크 내에서)** , 또는 **공개 (인터넷)**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-114">When you create a SQL Server virtual machine with a gallery image, hello **SQL Server Connectivity** option gives you hello choice of **Local (inside VM)**, **Private (within Virtual Network)**, or **Public (Internet)**.</span></span>

![SQL Server 연결](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

<span data-ttu-id="cb8b9-116">Hello 최상의 보안을 위해 사용자의 시나리오에 대 한 hello 가장 제한적인 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-116">For hello best security, choose hello most restrictive option for your scenario.</span></span> <span data-ttu-id="cb8b9-117">예를 들어 SQL Server에 액세스 하는 응용 프로그램을 실행 하는 경우 hello 동일한 VM 다음 **로컬** 는 hello 가장 안전한 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-117">For example, if you are running an application that accesses SQL Server on hello same VM, then **Local** is hello most secure choice.</span></span> <span data-ttu-id="cb8b9-118">다음 액세스 toohello SQL Server를 필요로 하는 Azure 응용 프로그램을 실행 하는 경우 **개인** 통신 tooSQL 서버 hello 지정 내 에서만 보호 [Azure 가상 네트워크](../../../virtual-network/virtual-networks-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-118">If you are running an Azure application that requires access toohello SQL Server, then **Private** secures communication tooSQL Server only within hello specified [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="cb8b9-119">필요한 경우 **공용** (internest) 액세스 toohello SQL Server VM을 확인 한 다음 있는지 toofollow 공격 노출 영역에서이 항목 tooreduce 다른 모범 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-119">If you require **Public** (internest) access toohello SQL Server VM, then make sure toofollow other best practices in this topic tooreduce your attack surface area.</span></span>

<span data-ttu-id="cb8b9-120">hello hello 포털에서 선택 된 옵션 사용 하 여 인바운드 보안 규칙 hello Vm에 [네트워크 보안 그룹](../../../virtual-network/virtual-networks-nsg.md) tooallow (NSG) 또는 네트워크 트래픽 tooyour 가상 컴퓨터를 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-120">hello selected options in hello portal use inbound security rules on hello VMs [Network Security Group](../../../virtual-network/virtual-networks-nsg.md) (NSG) tooallow or deny network traffic tooyour virtual machine.</span></span> <span data-ttu-id="cb8b9-121">수정 하거나 새 인바운드 NSG 규칙 tooallow 트래픽 toohello SQL Server 포트 (기본값 1433)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-121">You can modify or create new inbound NSG rules tooallow traffic toohello SQL Server port (default 1433).</span></span> <span data-ttu-id="cb8b9-122">허용 되는 toocommunicate이이 포트를 통해 특정 IP 주소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-122">You can also specify specific IP addresses that are allowed toocommunicate over this port.</span></span>

![네트워크 보안 그룹 규칙](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

<span data-ttu-id="cb8b9-124">또한 tooNSG 규칙 toorestrict 네트워크 트래픽, hello 가상 컴퓨터에서 Windows 방화벽 hello를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-124">In addition tooNSG rules toorestrict network traffic, you can also use hello Windows Firewall on hello virtual machine.</span></span>

<span data-ttu-id="cb8b9-125">끝점 hello 클래식 배포 모델을 사용 하는 경우 사용 하지 않는 경우 hello 가상 컴퓨터 끝점을 모두 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-125">If you are using endpoints with hello classic deployment model, remove any endpoints on hello virtual machine if you do not use them.</span></span> <span data-ttu-id="cb8b9-126">끝점 Acl을 사용 하 여, 참조 [끝점에서 ACL 관리 hello](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-126">For instructions on using ACLs with endpoints, see [Manage hello ACL on an endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span> <span data-ttu-id="cb8b9-127">이 작업이 hello 리소스 관리자를 사용 하는 Vm에 대 한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-127">This is not necessary for VMs that use hello Resource Manager.</span></span>

<span data-ttu-id="cb8b9-128">마지막으로, Azure 가상 컴퓨터에 SQL Server 데이터베이스 엔진 hello의 hello 인스턴스에 대 한 암호화 된 연결을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-128">Finally, consider enabling encrypted connections for hello instance of hello SQL Server Database Engine in your Azure virtual machine.</span></span> <span data-ttu-id="cb8b9-129">서명된 인증서로 SQL server 인스턴스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-129">Configure SQL server instance with a signed certificate.</span></span> <span data-ttu-id="cb8b9-130">자세한 내용은 참조 [암호화 연결 사용 toohello 데이터베이스 엔진](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) 및 [연결 문자열 구문](https://msdn.microsoft.com/library/ms254500.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-130">For more information, see [Enable Encrypted Connections toohello Database Engine](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) and [Connection String Syntax](https://msdn.microsoft.com/library/ms254500.aspx).</span></span>

## <a name="use-a-non-default-port"></a><span data-ttu-id="cb8b9-131">기본 포트가 아닌 포트 사용</span><span class="sxs-lookup"><span data-stu-id="cb8b9-131">Use a non-default port</span></span>

<span data-ttu-id="cb8b9-132">기본적으로 SQL Server는 잘 알려진 포트 1433에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-132">By default, SQL Server listens on a well-known port, 1433.</span></span> <span data-ttu-id="cb8b9-133">보안 향상된을 위해 SQL Server toolisten에서 1401 같은 기본이 아닌 포트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-133">For increased security, configure SQL Server toolisten on a non-default port, such as 1401.</span></span> <span data-ttu-id="cb8b9-134">Hello Azure 포털에에서는 SQL Server 갤러리 이미지를 프로 비전 하는 경우 hello에서이 포트를 지정할 수 있습니다 **SQL Server 설정을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-134">If you provision a SQL Server gallery image in hello Azure portal, you can specify this port in hello **SQL Server settings** blade.</span></span>

<span data-ttu-id="cb8b9-135">tooconfigure이에서 프로 비전 후 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-135">tooconfigure this after provisioning, you have two options:</span></span>

- <span data-ttu-id="cb8b9-136">리소스 관리자 Vm에 대해 선택할 수 있습니다 **SQL Server 구성** hello VM 개요 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-136">For Resource Manager VMs, you can select **SQL Server configuration** from hello VM overview blade.</span></span> <span data-ttu-id="cb8b9-137">Toochange hello 포트는 옵션 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-137">This provides an option toochange hello port.</span></span>

  ![포털에서 TCP 포트 변경](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- <span data-ttu-id="cb8b9-139">클래식 Vm 또는 포털 hello로 프로 비전 되지 않은 SQL Server Vm에 대 한 VM toohello 원격으로 연결 하 여 hello 포트를 수동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-139">For Classic VMs or for SQL Server VMs that were not provisioned with hello portal, you can manually configure hello port by connecting remotely toohello VM.</span></span> <span data-ttu-id="cb8b9-140">Hello 구성 단계를 참조 하십시오. [서버 tooListen 특정 TCP 포트로 구성](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-140">For hello configuration steps, see [Configure a Server tooListen on a Specific TCP Port](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).</span></span> <span data-ttu-id="cb8b9-141">이 수동 방법을 사용 하는 경우 해당 TCP 포트에서 Windows 방화벽 규칙 tooallow 들어오는 트래픽이 tooadd가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-141">If you use this manual technique, you also need tooadd a Windows Firewall rule tooallow incoming traffic on that TCP port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cb8b9-142">기본이 아닌 포트를 지정 하는 SQL Server 포트가 열려 toopublic 인터넷 연결 하는 경우에 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-142">Specifying a non-default port is a good idea if your SQL Server port is open toopublic internet connections.</span></span>

<span data-ttu-id="cb8b9-143">SQL Server를 기본이 아닌 포트에서 수신 하는 경우에 연결할 때 hello 포트를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-143">When SQL Server is listening on a non-default port, you must specify hello port when you connect.</span></span> <span data-ttu-id="cb8b9-144">예를 들어 hello 서버 IP 주소가 13.55.255.255 고 1401 포트에서 SQL Server가 수신 하는 시나리오를 고려 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-144">For example, consider a scenario where hello server IP address is 13.55.255.255 and SQL Server is listening on port 1401.</span></span> <span data-ttu-id="cb8b9-145">tooconnect tooSQL 서버를 지정 하는 경우 `13.55.255.255,1401` hello 연결 문자열에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-145">tooconnect tooSQL Server, you would specify `13.55.255.255,1401` in hello connection string.</span></span>

## <a name="manage-accounts"></a><span data-ttu-id="cb8b9-146">계정 관리</span><span class="sxs-lookup"><span data-stu-id="cb8b9-146">Manage accounts</span></span>

<span data-ttu-id="cb8b9-147">공격자가 tooeasily 추측 계정 이름이 나 암호를 되기를 원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-147">You don't want attackers tooeasily guess account names or passwords.</span></span> <span data-ttu-id="cb8b9-148">다음 팁 toohelp hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-148">Use hello following tips toohelp:</span></span>

- <span data-ttu-id="cb8b9-149">로컬 관리자 계정의 이름을 **Administrator**가 아닌 다른 이름으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-149">Create a unique local administrator account that is not named **Administrator**.</span></span>

- <span data-ttu-id="cb8b9-150">모든 계정에 복잡하고 강력한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-150">Use complex strong passwords for all your accounts.</span></span> <span data-ttu-id="cb8b9-151">방법에 대 한 자세한 내용은 강력한 암호를 toocreate 참조 [강력한 암호를 만드는](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) 문서.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-151">For more information about how toocreate a strong password, see [Create a strong password](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) article.</span></span>

- <span data-ttu-id="cb8b9-152">기본적으로 Azure는 SQL Server 가상 컴퓨터를 설치하는 동안 Windows 인증을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-152">By default, Azure selects Windows Authentication during SQL Server Virtual Machine setup.</span></span> <span data-ttu-id="cb8b9-153">따라서 hello **SA** 로그인이 해제 되며 설치 프로그램에서 암호를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-153">Therefore, hello **SA** login is disabled and a password is assigned by setup.</span></span> <span data-ttu-id="cb8b9-154">해당 hello 권장 **SA** 로그인 사용 되거나 사용 하도록 설정 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-154">We recommend that hello **SA** login should not be used or enabled.</span></span> <span data-ttu-id="cb8b9-155">SQL 로그인 해야 할 경우 hello 다음 전략 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-155">If you must have a SQL login, use one of hello following strategies:</span></span>

  - <span data-ttu-id="cb8b9-156">**sysadmin** 멤버 자격이 있는 고유한 이름을 가진 SQL 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-156">Create a SQL account with a unique name that has **sysadmin** membership.</span></span> <span data-ttu-id="cb8b9-157">사용 하 여 hello 포털에서 이렇게 하려면 **SQL 인증** 프로 비전 중입니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-157">You can do this from hello portal by enabling **SQL Authentication** during provisioning.</span></span>

    > [!TIP] 
    > <span data-ttu-id="cb8b9-158">프로 비전 하는 동안 SQL 인증을 사용 하지 않도록 하는 경우 너무 hello 인증 모드를 수동으로 변경 해야 하면**SQL Server 및 Windows 인증 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-158">If you do not enable SQL Authentication during provisioning, you must manually change hello authentication mode too**SQL Server and Windows Authentication Mode**.</span></span> <span data-ttu-id="cb8b9-159">자세한 내용은 [서버 인증 모드 변경](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-159">For more information, see [Change Server Authentication Mode](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).</span></span>

  - <span data-ttu-id="cb8b9-160">Hello를 사용 해야 할 경우 **SA** 로그인을 프로 비전 하 고 강력한 새 암호를 할당 한 후 hello 로그인을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-160">If you must use hello **SA** login, enable hello login after provisioning and assign a new strong password.</span></span>

## <a name="follow-on-premises-best-practices"></a><span data-ttu-id="cb8b9-161">온-프레미스 모범 사례 따르기</span><span class="sxs-lookup"><span data-stu-id="cb8b9-161">Follow on-premises best practices</span></span>

<span data-ttu-id="cb8b9-162">검토 하 고 해당 되는 hello 기존의 온-프레미스 보안 방법을 구현 하는 또한 권장 toohello이이 항목에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-162">In addition toohello practices described in this topic, we recommend that you review and implement hello traditional on-premises security practices where applicable.</span></span> <span data-ttu-id="cb8b9-163">자세한 내용은 [SQL Server 설치에 대한 보안 고려 사항](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-163">For more information, see [Security Considerations for a SQL Server Installation](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb8b9-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb8b9-164">Next Steps</span></span>

<span data-ttu-id="cb8b9-165">성능에 대한 모범 사례에도 관심이 있으면 [Azure Virtual Machines의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-165">If you are also interested in best practices around performance, see [Performance Best Practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

<span data-ttu-id="cb8b9-166">다른 항목은 서로 관련 toorunning Azure Vm에서 SQL Server에 대 한 참조 [SQL Server에 대 한 Azure 가상 컴퓨터 개요](virtual-machines-windows-sql-server-iaas-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb8b9-166">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

