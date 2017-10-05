---
title: "PowerShell을 사용하여 기본 모드 보고서 서버로 VM 만들기 | Microsoft Docs"
description: "이 항목에서는 Azure 가상 컴퓨터에서 SQL Server Reporting Services 기본 모드 보고서 서버의 배포 및 구성에 대해 설명하고 안내합니다. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 5e5c11251cd316e8161dbe362b300be76927ac01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="60064-103">PowerShell을 사용하여 기본 모드 보고서 서버로 Azure VM 만들기</span><span class="sxs-lookup"><span data-stu-id="60064-103">Use PowerShell to Create an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="60064-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="60064-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="60064-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="60064-107">이 항목에서는 Azure 가상 컴퓨터에서 SQL Server Reporting Services 기본 모드 보고서 서버의 배포 및 구성에 대해 설명하고 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-107">This topic describes and walks you through the deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="60064-108">이 문서의 단계는 가상 컴퓨터 및 Windows PowerShell 스크립트를 만드는 수동 단계를 조합하여 VM에서 Reporting Services를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-108">The steps in this document use a combination of manual steps to create the virtual machine and a Windows PowerShell script to configure Reporting Services on the VM.</span></span> <span data-ttu-id="60064-109">구성 스크립트에는 HTTP 또는 HTTPS에 대해 방화벽 포트를 여는 작업이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-109">The configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="60064-110">보고서 서버에서 **HTTPS**가 필요하지 않은 경우 **2단계를 건너뜁니다**.</span><span class="sxs-lookup"><span data-stu-id="60064-110">If you do not require **HTTPS** on the report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="60064-111">1단계에서 VM을 만든 후 스크립트를 사용하여 보고서 서버 및 HTTP 구성 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-111">After creating the VM in step 1, go to the section Use script to configure the report server and HTTP.</span></span> <span data-ttu-id="60064-112">스크립트를 실행하면 보고서 서버를 사용할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-112">After you run the script, the report server is ready to use.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="60064-113">필수 조건 및 가정</span><span class="sxs-lookup"><span data-stu-id="60064-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="60064-114">**Azure 구독**: Azure 구독에서 사용 가능한 코어 수를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-114">**Azure Subscription**: Verify the number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="60064-115">권장되는 VM 크기인 **A3**을 만드는 경우 **4**개의 사용 가능한 코어가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-115">If you create the recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="60064-116">**A2**의 VM 크기를 사용하는 경우 **2**개의 사용 가능한 코어가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="60064-117">구독의 코어 제한을 확인하려면, Azure 클래식 포털의 왼쪽 창에서 설정을 클릭하고 위쪽 메뉴에서 사용을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-117">To verify the core limit of your subscription, in the Azure classic portal, click SETTINGS in the left pane and then Click USAGE in the top menu.</span></span>
  * <span data-ttu-id="60064-118">코어 할당량을 늘리려면 [Azure 지원](https://azure.microsoft.com/support/options/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-118">To increase the core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="60064-119">VM 크기 정보는 [Azure에 대한 가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="60064-120">**Windows PowerShell 스크립팅**: 이 항목에서는 Windows PowerShell의 기본 작동 지식이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-120">**Windows PowerShell Scripting**: The topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="60064-121">Windows PowerShell을 사용하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-121">For more information about using Windows PowerShell, see the following:</span></span>
  
  * [<span data-ttu-id="60064-122">Windows Server에서 Windows PowerShell 시작</span><span class="sxs-lookup"><span data-stu-id="60064-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="60064-123">Windows PowerShell 시작</span><span class="sxs-lookup"><span data-stu-id="60064-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="60064-124">1단계: Azure 가상 컴퓨터 프로비전</span><span class="sxs-lookup"><span data-stu-id="60064-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="60064-125">Azure 클래식 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-125">Browse to the Azure classic portal.</span></span>
2. <span data-ttu-id="60064-126">왼쪽 창에서 **가상 컴퓨터** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-126">Click **Virtual Machines** in the left pane.</span></span>
   
    ![Microsoft Azure 가상 컴퓨터](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="60064-128">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-128">Click **New**.</span></span>
   
    ![새 단추](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="60064-130">**갤러리에서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-130">Click **From Gallery**.</span></span>
   
    ![갤러리의 새 VM](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="60064-132">**SQL Server 2014 RTM 표준 – Windows Server 2012 R2** 를 클릭한 다음 화살표를 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click the arrow to continue.</span></span>
   
    ![다음](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="60064-134">Reporting Services 데이터 기반 구독 기능이 필요한 경우 **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-134">If you need the Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="60064-135">SQL Server 버전 및 기능 지원에 대한 자세한 내용은 [SQL Server 2012 버전에서 지원하는 기능](https://msdn.microsoft.com/library/cc645993.aspx#Reporting)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-135">For more information on SQL Server editions and feature support, see [Features Supported by the Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="60064-136">**가상 컴퓨터 구성** 페이지에서 다음 필드를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-136">On the **Virtual machine configuration** page, edit the following fields:</span></span>
   
   * <span data-ttu-id="60064-137">**버전 릴리스 날짜**가 둘 이상 있는 경우 가장 최신 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-137">If there is more than one **VERSION RELEASE DATE**, select the most recent version.</span></span>
   * <span data-ttu-id="60064-138">**가상 컴퓨터 이름**: 컴퓨터 이름은 다음 구성 페이지에서 기본 클라우드 서비스 DNS 이름으로도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-138">**Virtual Machine Name**: The machine name is also used on the next configuration page as the default Cloud Service DNS name.</span></span> <span data-ttu-id="60064-139">Azure 서비스에서 DNS 이름은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-139">The DNS name must be unique across the Azure service.</span></span> <span data-ttu-id="60064-140">VM의 용도에 대해 설명하는 컴퓨터 이름을 사용하여 VM을 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-140">Consider configuring the VM with a computer name that describes what the VM is used for.</span></span> <span data-ttu-id="60064-141">예를 들어 ssrsnativecloud입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="60064-142">**계층**: 표준</span><span class="sxs-lookup"><span data-stu-id="60064-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="60064-143">**크기: A3** 은 SQL Server 작업에 권장되는 VM 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-143">**Size:A3** is the recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="60064-144">VM이 보고서 서버로만 사용되는 경우 보고서 서버의 작업이 크지 않는 한 VM 크기는 A2이면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless the report server experiences a large workload.</span></span> <span data-ttu-id="60064-145">VM 가격 책정 정보는 [가상 컴퓨터 가격 책정](https://azure.microsoft.com/pricing/details/virtual-machines/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="60064-146">**새 사용자 이름**: 제공하는 이름은 VM에서 관리자로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="60064-146">**New User Name**: the name you provide is created as an administrator on the VM.</span></span>
   * <span data-ttu-id="60064-147">**새 암호** 및 **확인**.</span><span class="sxs-lookup"><span data-stu-id="60064-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="60064-148">이 암호는 새 관리자 계정에 대해 사용되므로 강력한 암호를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-148">This password is used for the new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="60064-149">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="60064-149">Click **Next**.</span></span> <span data-ttu-id="60064-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="60064-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="60064-151">다음 페이지에서 다음 필드를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-151">On the next page, edit the following fields:</span></span>
   
   * <span data-ttu-id="60064-152">**클라우드 서비스**: **새 클라우드 서비스 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="60064-153">**클라우드 서비스 DNS 이름**: VM과 연결된 클라우드 서비스의 공용 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-153">**Cloud Service DNS Name**: This is the public DNS name of the Cloud Service that is associated with the VM.</span></span> <span data-ttu-id="60064-154">기본 이름은 VM 이름에 입력한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-154">The default name is the name you typed in for the VM name.</span></span> <span data-ttu-id="60064-155">이 항목의 이후 단계에서 신뢰할 수 있는 SSL 인증서를 만들면 DNS 이름이 인증서의 “**발급 대상**” 값에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-155">If in later steps of the topic, you create a trusted SSL certificate and then the DNS name is used for the value of the “**Issued to**” of the certificate.</span></span>
   * <span data-ttu-id="60064-156">**지역/선호도 그룹/가상 네트워크**: 최종 사용자에게 가장 가까운 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-156">**Region/Affinity Group/Virtual Network**: Choose the region closest to your end users.</span></span>
   * <span data-ttu-id="60064-157">**저장소 계정**: 자동으로 생성된 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="60064-158">**가용성 집합**: 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="60064-159">**끝점** **원격 데스크톱** 및 **PowerShell** 끝점을 그대로 유지한 다음 사용자 환경에 따라 HTTP 또는 HTTPS 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-159">**ENDPOINTS** Keep the **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="60064-160">**HTTP**: 기본 공용 포트 및 개인 포트가 **80**입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-160">**HTTP**: The default public and private ports are **80**.</span></span> <span data-ttu-id="60064-161">80 이외의 개인 포트를 사용하는 경우 HTTP 스크립트에서 **$HTTPport = 80** 을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in the http script.</span></span>
     * <span data-ttu-id="60064-162">**HTTPS**: 기본 공용 포트 및 개인 포트가 **443**입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-162">**HTTPS**: The default public and private ports are **443**.</span></span> <span data-ttu-id="60064-163">보안 모범 사례는 개인 포트를 변경하고 개인 포트를 사용하도록 방화벽 및 보고서 서버를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-163">A security best practice is to change the private port and configure your firewall and the report server to use the private port.</span></span> <span data-ttu-id="60064-164">끝점에 대한 자세한 내용은 [가상 컴퓨터로 끝점을 설정하는 방법](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-164">For more information on endpoints, see [How to Set Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="60064-165">443 이외의 포트를 사용하는 경우 HTTPS 스크립트에서 매개 변수 **$HTTPsport = 443** 을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-165">Note that if you use a port other than 443, change the parameter **$HTTPsport = 443** in the HTTPS script.</span></span>
   * <span data-ttu-id="60064-166">다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-166">Click next .</span></span> ![다음](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="60064-168">마법사의 마지막 페이지에서 기본 **VM 에이전트 설치** 를 선택한 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-168">On the last page of the wizard, keep the default **Install the VM agent** selected.</span></span> <span data-ttu-id="60064-169">이 항목의 단계에서 VM 에이전트를 이용하지 않지만 이 VM을 유지하려는 경우 VM 에이전트 및 확장을 사용하면 CM이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-169">The steps in this topic do not utilize the VM agent but if you plan to keep this VM, the VM agent and extensions will allow you to enhance he CM.</span></span>  <span data-ttu-id="60064-170">VM 에이전트에 대한 자세한 내용은 [VM 에이전트 및 확장 – 1부](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-170">For more information on the VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="60064-171">AD 실행을 설치한 기본 확장 중 하나가 VM 데스크톱에서 내부 IP 및 여유 드라이브 공간 같은 시스템 정보를 표시하는 “BGINFO” 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-171">One of the default extensions installed ad running is the “BGINFO” extension that displays on the VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="60064-172">완료를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-172">Click complete .</span></span> ![Ok](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="60064-174">VM의 **상태**는 프로비전 프로세스 중에는 **시작 중(프로비전 중)**으로 표시되다가 VM이 프로비전되고 사용할 준비가 되면 **실행 중**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-174">The **Status** of the VM displays as **Starting (Provisioning)** during the provision process and then displays as **Running** when the VM is provisioned and ready to use.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="60064-175">2단계: 서버 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="60064-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="60064-176">보고서 서버에서 HTTPS가 필요하지 않은 경우 **2단계를 건너뛰고** **스크립트를 사용하여 보고서 서버 및 HTTP 구성** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-176">If you do not require HTTPS on the report server, you can **skip step 2** and go to the section **Use script to configure the report server and HTTP**.</span></span> <span data-ttu-id="60064-177">HTTP 스크립트를 사용하여 신속하게 보고서 서버를 구성하면 보고서 서버를 사용할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-177">Use the HTTP script to quickly configure the report server and the report server will be ready to use.</span></span>

<span data-ttu-id="60064-178">VM에서 HTTPS를 사용하려면 신뢰할 수 있는 SSL 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-178">In order to use HTTPS on the VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="60064-179">시나리오에 따라 다음 두 방법 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-179">Depending on your scenario, you can use one of the following two methods:</span></span>

* <span data-ttu-id="60064-180">CA(인증 기관)에서 발급하고 Microsoft에서 신뢰하는 유효한 SSL 인증서.</span><span class="sxs-lookup"><span data-stu-id="60064-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="60064-181">CA 루트 인증서는 Microsoft 루트 인증서 프로그램을 통해 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-181">The CA root certificates are required to be distributed via the Microsoft Root Certificate Program.</span></span> <span data-ttu-id="60064-182">이 프로그램에 대한 자세한 내용은 [Windows 및 Windows Phone 8 SSL 루트 인증서 프로그램(구성원 CA)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) 및 [Microsoft 루트 인증서 프로그램 소개](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction to The Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="60064-183">자체 서명된 인증서.</span><span class="sxs-lookup"><span data-stu-id="60064-183">A self-signed certificate.</span></span> <span data-ttu-id="60064-184">자체 서명된 인증서는 프로덕션 환경에 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="to-use-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="60064-185">신뢰할 수 있는 CA(인증 기관)에서 만든 인증서를 사용하려면</span><span class="sxs-lookup"><span data-stu-id="60064-185">To use a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="60064-186">**인증 기관에서 웹 사이트에 대한 서버 인증서를 요청합니다**.</span><span class="sxs-lookup"><span data-stu-id="60064-186">**Request a server certificate for the website from a certification authority**.</span></span> 
   
    <span data-ttu-id="60064-187">웹 서버 인증서 마법사를 사용하여 인증 기관에 보내는 인증서 요청 파일(Certreq.txt)을 생성하거나 온라인 인증 기관에 대한 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-187">You can use the Web Server Certificate Wizard either to generate a certificate request file (Certreq.txt) that you send to a certification authority, or to generate a request for an online certification authority.</span></span> <span data-ttu-id="60064-188">예를 들어 Windows Server 2012의 Microsoft 인증서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="60064-189">서버 인증서에서 제공하는 식별 보증 수준에 따라 인증 기관이 요청을 승인하고 인증서 파일을 보내는 데 며칠에서 몇 개월까지 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="60064-189">Depending on the level of identification assurance offered by your server certificate, it is several days to several months for the certification authority to approve your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="60064-190">서버 인증서를 요청하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-190">For more information about requesting a server certificates, see the following:</span></span> 
   
   * <span data-ttu-id="60064-191">[Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx) 사용.</span><span class="sxs-lookup"><span data-stu-id="60064-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="60064-192">Windows Server 2012를 관리하는 보안 도구</span><span class="sxs-lookup"><span data-stu-id="60064-192">Security Tools to Administer Windows Server 2012.</span></span>
     
     [<span data-ttu-id="60064-193">Windows Server 2012를 관리하는 보안 도구</span><span class="sxs-lookup"><span data-stu-id="60064-193">Security Tools to Administer Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="60064-194">신뢰할 수 있는 SSL 인증서의 **발급 대상** 필드는 새 VM에 사용한 **클라우드 서비스 DNS 이름**과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-194">The **issued to** field of the trusted SSL certificate should be the same as the **Cloud Service DNS NAME** you used for the new VM.</span></span>

2. <span data-ttu-id="60064-195">**웹 서버에 서버 인증서를 설치합니다**.</span><span class="sxs-lookup"><span data-stu-id="60064-195">**Install the server certificate on the Web server**.</span></span> <span data-ttu-id="60064-196">이 경우의 웹 서버는 보고서 서버를 호스트하는 VM이고 Reporting Services를 구성할 때 이후 단계에서 웹 사이트가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="60064-196">The Web server in this case is the VM that hosts the report server and the website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="60064-197">인증서 MMC 스냅인을 사용하여 웹 서버에 서버 인증서를 설치하는 방법에 대한 자세한 내용은 [서버 인증서 설치](https://technet.microsoft.com/library/cc740068)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-197">For more information about installing the server certificate on the Web server by using the Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="60064-198">이 항목에 포함된 스크립트를 사용하여 보고서 서버를 구성하려면 스크립트의 매개 변수로 인증서 **지문** 의 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-198">If you want to use the script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="60064-199">인증서 지문을 가져오는 방법에 대한 자세한 내용은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-199">See the next section for details on how to obtain the thumbprint of the certificate.</span></span>
3. <span data-ttu-id="60064-200">보고서 서버에 서버 인증서를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-200">Assign the server certificate to the report server.</span></span> <span data-ttu-id="60064-201">할당은 다음 섹션에서 보고서 서버를 구성할 때 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-201">The assignment is completed in the next section when you configure the report server.</span></span>

### <a name="to-use-the-virtual-machines-self-signed-certificate"></a><span data-ttu-id="60064-202">가상 컴퓨터의 자체 서명된 인증서를 사용하려면</span><span class="sxs-lookup"><span data-stu-id="60064-202">To use the Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="60064-203">VM이 프로비전되었을 때 자체 서명된 인증서가 VM에 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-203">A self-signed certificate was created on the VM when the VM was provisioned.</span></span> <span data-ttu-id="60064-204">인증서 이름은 VM DNS 이름과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-204">The certificate has the same name as the VM DNS name.</span></span> <span data-ttu-id="60064-205">인증서 오류를 방지하려면 VM 자체에서 뿐만 아니라 사이트의 모든 사용자도 인증서를 신뢰해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-205">In order to avoid certificate errors, it is required that the certificate is trusted on the VM itself, and also by all users of the site.</span></span>

1. <span data-ttu-id="60064-206">로컬 VM에서 인증서의 루트 CA를 신뢰하려면 인증서를 **신뢰할 수 있는 루트 인증 기관**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-206">To trust the root CA of the certificate on the Local VM, add the certificate to the **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="60064-207">다음은 필요한 단계에 대한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-207">The following is a summary of the steps required.</span></span> <span data-ttu-id="60064-208">CA를 신뢰하는 방법에 대한 자세한 단계는 [서버 인증서 설치](https://technet.microsoft.com/library/cc740068)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-208">For detailed steps on how to trust the CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="60064-209">Azure 클래식 포털에서 VM을 선택하고 연결을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-209">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="60064-210">브라우저 구성에 따라 VM에 연결하기 위해 .rdp 파일을 저장하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-210">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
      
       ![Azure 가상 컴퓨터에 연결](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="60064-212">VM을 만들 때 구성한 사용자 VM 이름, 사용자 이름 및 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-212">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
      
       <span data-ttu-id="60064-213">예를 들어 다음 이미지에서 VM 이름은 **ssrsnativecloud**이고 사용자 이름은 **testuser**입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-213">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
      
       ![로그인에 VM 이름 포함](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="60064-215">Mmc.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-215">Run mmc.exe.</span></span> <span data-ttu-id="60064-216">자세한 내용은 [방법: MMC 스냅인을 사용하여 인증서 보기](https://msdn.microsoft.com/library/ms788967.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-216">For more information, see [How to: View Certificates with the MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="60064-217">콘솔 응용 프로그램 **파일** 메뉴에서 **인증서** 스냅인을 추가하고 메시지가 표시되면 **컴퓨터 계정**을 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-217">In the console application **File** menu, add the **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="60064-218">관리할 **로컬 컴퓨터**를 선택한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-218">Select **Local Computer** to manage and then click **Finish**.</span></span>
   5. <span data-ttu-id="60064-219">**확인**을 클릭한 다음 **인증서 - 개인** 노드를 확장한 다음 **인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-219">Click **Ok** and then expand the **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="60064-220">인증서 이름은 VM의 DNS 이름을 따서 지정되고 **cloudapp.net**으로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="60064-220">The certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="60064-221">인증서 이름을 마우스 오른쪽 단추로 클릭하고 **복사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-221">Right-click the certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="60064-222">**T신뢰할 수 있는 루트 인증 기관** 노드를 확장한 다음 **인증서**를 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-222">Expand the **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="60064-223">유효성을 검사하려면 **신뢰할 수 있는 루트 인증 기관** 에서 인증서 이름을 두 번 클릭하여 오류가 없는지, 인증서가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-223">To validate, double click on the certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="60064-224">이 항목에 포함된 HTTPS 스크립트를 사용하여 보고서 서버를 구성하려면 스크립트의 매개 변수로 인증서 **지문** 의 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-224">If you want to use the HTTPS script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="60064-225">**지문 값을 가져오려면**다음을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-225">**To get the thumbprint value**, complete the following.</span></span> <span data-ttu-id="60064-226">또한 [스크립트를 사용하여 보고서 서버 및 HTTPS 구성](#use-script-to-configure-the-report-server-and-HTTPS)섹션에 지문을 검색하는 PowerShell 샘플도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-226">There is also a PowerShell sample to retrieve the thumbprint in section [Use script to configure the report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="60064-227">인증서의 이름(예: Ssrsnativecloud.cloudapp.net)을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-227">Double-click the name of the certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="60064-228">**세부 정보** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-228">Click the **Details** tab.</span></span>
      3. <span data-ttu-id="60064-229">왼쪽 창에서 **지문**.</span><span class="sxs-lookup"><span data-stu-id="60064-229">Click **Thumbprint**.</span></span> <span data-ttu-id="60064-230">지문 값이 세부 정보 필드에 표시됩니다. 예를 들어 ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-230">The value of the thumbprint is displayed in the details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="60064-231">지문을 복사하고 나중을 위해 값을 저장하거나 지금 스크립트를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-231">Copy the thumbprint and save the value for later or edit the script now.</span></span>
      5. <span data-ttu-id="60064-232">(*) 스크립트를 실행하기 전에 값 쌍 사이의 공백을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-232">(*) Before you run the script, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="60064-233">예를 들어 앞에서 설명한 지문은 이제 ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-233">For example the thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="60064-234">보고서 서버에 서버 인증서를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-234">Assign the server certificate to the report server.</span></span> <span data-ttu-id="60064-235">할당은 다음 섹션에서 보고서 서버를 구성할 때 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-235">The assignment is completed in the next section when you configure the report server.</span></span>

<span data-ttu-id="60064-236">자체 서명된 SSL 인증서를 사용하는 경우 인증서 이름이 이미 VM의 호스트 이름과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-236">If you are using a self-signed SSL certificate, the name on the certificate already matches the hostname of the VM.</span></span> <span data-ttu-id="60064-237">따라서 컴퓨터의 DNS는 이미 전역으로 등록되어 있으므로 모든 클라이언트에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-237">Therefore, the DNS of the machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-the-report-server"></a><span data-ttu-id="60064-238">3단계: 보고서 서버 구성</span><span class="sxs-lookup"><span data-stu-id="60064-238">Step 3: Configure the Report Server</span></span>
<span data-ttu-id="60064-239">이 섹션에서는 Reporting Services 기본 모드 보고서 서버로 VM을 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-239">This section walks you through configuring the VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="60064-240">다음 방법 중 하나를 사용하여 보고서 서버를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-240">You can use one of the following methods to configure the report server:</span></span>

* <span data-ttu-id="60064-241">스크립트를 사용하여 보고서 서버 구성</span><span class="sxs-lookup"><span data-stu-id="60064-241">Use the script to configure the report server</span></span>
* <span data-ttu-id="60064-242">구성 관리자를 사용하여 보고서 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-242">Use Configuration Manager to Configure the Report Server.</span></span>

<span data-ttu-id="60064-243">자세한 단계는 [가상 컴퓨터에 연결 및 Reporting Services 구성 관리자 시작](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager)섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-243">For more detailed steps, see the section [Connect to the Virtual Machine and Start the Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="60064-244">**인증 참고:** Windows 인증은 권장되는 인증 방법이며 기본 Reporting Services 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-244">**Authentication Note:** Windows authentication is the recommended authentication method and it is the default Reporting Services authentication.</span></span> <span data-ttu-id="60064-245">VM에 구성된 사용자만 Reporting Services에 액세스할 수 있으며 Reporting Services 역할에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-245">Only users that are configured on the VM can access Reporting Services and assigned to Reporting Services roles.</span></span>

### <a name="use-script-to-configure-the-report-server-and-http"></a><span data-ttu-id="60064-246">스크립트를 사용하여 보고서 서버 및 HTTP 구성</span><span class="sxs-lookup"><span data-stu-id="60064-246">Use script to configure the report server and HTTP</span></span>
<span data-ttu-id="60064-247">Windows PowerShell 스크립트를 사용하여 보고서 서버를 구성하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-247">To use the Windows PowerShell script to configure the report server, complete the following steps.</span></span> <span data-ttu-id="60064-248">구성에 HTTPS가 아닌 HTTP가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-248">The configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="60064-249">Azure 클래식 포털에서 VM을 선택하고 연결을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-249">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="60064-250">브라우저 구성에 따라 VM에 연결하기 위해 .rdp 파일을 저장하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-250">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![Azure 가상 컴퓨터에 연결](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="60064-252">VM을 만들 때 구성한 사용자 VM 이름, 사용자 이름 및 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-252">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="60064-253">예를 들어 다음 이미지에서 VM 이름은 **ssrsnativecloud**이고 사용자 이름은 **testuser**입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-253">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![로그인에 VM 이름 포함](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="60064-255">VM에서 관리자 권한으로 **Windows PowerShell ISE** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="60064-255">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="60064-256">PowerShell ISE는 Windows Server 2012에 기본적으로 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-256">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="60064-257">스크립트를 ISE에 붙여넣고 스크립트를 수정한 다음 스크립트를 실행할 수 있도록 표준 Windows PowerShell 창 대신 ISE를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-257">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="60064-258">Windows PowerShell ISE에서 **보기** 메뉴를 클릭한 다음 **스크립트 창 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-258">In Windows PowerShell ISE, click the **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="60064-259">다음 스크립트를 복사하고 Windows PowerShell ISE 스크립트 창으로 스크립트를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-259">Copy the following script, and paste the script into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change the value if you used a different port for the private HTTP endpoint when the VM was created.
   
        ## Set PowerShell execution policy to be able to run scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. <span data-ttu-id="60064-260">HTTP 포트 80 이외의 포트를 사용하여 VM을 만든 경우 매개 변수 $HTTPport = 80을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-260">If you created the VM with an HTTP port other than 80, modify the parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="60064-261">스크립트가 현재 Reporting Services에 대해 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-261">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="60064-262">Reporting Services에 대한 스크립트를 실행하려는 경우 Get-WmiObject 문에서 네임스페이스 경로의 버전 부분을 "v11"로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-262">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
7. <span data-ttu-id="60064-263">스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-263">Run the script.</span></span>

<span data-ttu-id="60064-264">**유효성 검사**: 기본 보고서 서버 기능이 작동하는지 확인하려면 이 항목의 뒷부분에 나오는 [구성 확인](#verify-the-configuration) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-264">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-to-configure-the-report-server-and-https"></a><span data-ttu-id="60064-265">스크립트를 사용하여 보고서 서버 및 HTTPS 구성</span><span class="sxs-lookup"><span data-stu-id="60064-265">Use script to configure the report server and HTTPS</span></span>
<span data-ttu-id="60064-266">Windows PowerShell을 사용하여 보고서 서버를 구성하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-266">To use Windows PowerShell to configure the report server, complete the following steps.</span></span> <span data-ttu-id="60064-267">구성에 HTTP가 아닌 HTTPS가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-267">The configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="60064-268">Azure 클래식 포털에서 VM을 선택하고 연결을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-268">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="60064-269">브라우저 구성에 따라 VM에 연결하기 위해 .rdp 파일을 저장하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-269">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![Azure 가상 컴퓨터에 연결](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="60064-271">VM을 만들 때 구성한 사용자 VM 이름, 사용자 이름 및 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-271">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="60064-272">예를 들어 다음 이미지에서 VM 이름은 **ssrsnativecloud**이고 사용자 이름은 **testuser**입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-272">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![로그인에 VM 이름 포함](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="60064-274">VM에서 관리자 권한으로 **Windows PowerShell ISE** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="60064-274">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="60064-275">PowerShell ISE는 Windows Server 2012에 기본적으로 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-275">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="60064-276">스크립트를 ISE에 붙여넣고 스크립트를 수정한 다음 스크립트를 실행할 수 있도록 표준 Windows PowerShell 창 대신 ISE를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-276">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="60064-277">스크립트를 실행하도록 설정하려면 다음 Windows PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-277">To enable running scripts, run the following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="60064-278">그런 후 다음을 실행하면 정책을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-278">You can then run the following to verify the policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="60064-279">**Windows PowerShell ISE**에서 **보기** 메뉴를 클릭한 다음 **스크립트 창 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-279">In **Windows PowerShell ISE**, click the **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="60064-280">다음 스크립트를 복사하고 Windows PowerShell ISE 스크립트 창에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-280">Copy the following script and paste it into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures the report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when the HTTPS endpoint was created.
   
        # You can run the following command to get (.cloudapp.net certificates) so you can copy the thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # The certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # the certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If the certificate is not a wildcard certificate, comment out the following line, and enable the full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "The script will use $DNSNameAndPort as the DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. <span data-ttu-id="60064-281">스크립트에서 **$certificatehash** 매개 변수를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-281">Modify the **$certificatehash** parameter in the script:</span></span>
   
   * <span data-ttu-id="60064-282">이는 **필수** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-282">This is a **required** parameter.</span></span> <span data-ttu-id="60064-283">이전 단계에서 인증서 값을 저장하지 않은 경우 다음 방법 중 하나를 사용하여 인증서 지문에서 인증서 해시 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-283">If you did not save the certificate value from the previous steps, use one of the following methods to copy the certificate hash value from the certificates thumbprint.:</span></span>
     
       <span data-ttu-id="60064-284">VM에서 Windows PowerShell ISE를 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-284">On the VM, open Windows PowerShell ISE and run the following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="60064-285">출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-285">The output will look similar to the following.</span></span> <span data-ttu-id="60064-286">스크립트가 빈 줄을 반환하면 VM에서 인증서가 구성되지 않은 것입니다. 예를 보려면 [가상 컴퓨터의 자체 서명된 인증서를 사용하려면](#to-use-the-virtual-machines-self-signed-certificate) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-286">If the script returns a blank line, the VM does not have a certificate configured for example, see the section [To use the Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="60064-287">또는</span><span class="sxs-lookup"><span data-stu-id="60064-287">OR</span></span>
   * <span data-ttu-id="60064-288">VM에서 mmc.exe를 실행한 다음 **인증서** 스냅인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-288">On the VM Run mmc.exe and then add the **Certificates** snap-in.</span></span>
   * <span data-ttu-id="60064-289">**신뢰할 수 있는 루트 인증 기관** 노드 아래에서 인증서 이름을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-289">Under the **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="60064-290">VM의 자체 서명된 인증서를 사용하는 경우 인증서 이름은 VM의 DNS 이름을 따서 지정되고 **cloudapp.net**으로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="60064-290">If you are using the self-signed certificate of the VM, the certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="60064-291">**세부 정보** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-291">Click the **Details** tab.</span></span>
   * <span data-ttu-id="60064-292">왼쪽 창에서 **지문**.</span><span class="sxs-lookup"><span data-stu-id="60064-292">Click **Thumbprint**.</span></span> <span data-ttu-id="60064-293">지문 값이 세부 정보 필드에 표시됩니다. 예를 들어 af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-293">The value of the thumbprint is displayed in the details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="60064-294">**스크립트를 실행하기 전에**값 쌍 사이의 공백을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-294">**Before you run the script**, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="60064-295">예를 들어 af1160b64b288d890a8212ff6ba9c3664f319048입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="60064-296">**$httpsport** 매개 변수를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-296">Modify the **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="60064-297">HTTPS 끝점에 포트 443을 사용한 경우 스크립트에서 이 매개 변수를 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-297">If you used port 443 for the HTTPS endpoint, then you do not need to update this parameter in the script.</span></span> <span data-ttu-id="60064-298">그렇지 않은 경우 VM에서 HTTPS 개인 끝점을 구성할 때 선택한 포트 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-298">Otherwise use the port value you selected when you configured the HTTPS private endpoint on the VM.</span></span>
8. <span data-ttu-id="60064-299">**$DNSName** 매개 변수를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-299">Modify the **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="60064-300">스크립트가 와일드카드 인증서 $DNSName= "+"에 대해 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-300">The script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="60064-301">와일드카드 인증서 바인딩에 대해 구성하지 않으려면 $DNSName="+"를 주석으로 처리하고 전체 $DNSNAme 참조인 ##$DNSName="$server.cloudapp.net” 줄을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-301">If you do no want to configure for a wildcard certificate binding, comment out $DNSName="+" and enable the following line, the full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="60064-302">Reporting Services에 대해 가상 컴퓨터의 DNS 이름을 사용하지 않으려는 경우 $DNSName 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-302">Change the $DNSName value if you do not want to use the virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="60064-303">매개 변수를 사용하는 경우 인증서가 이 이름을 사용해야 하며 DNS 서버에서 전역으로 이름을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-303">If you use the parameter, the certificate must also use this name and you register the name globally on a DNS server.</span></span>
9. <span data-ttu-id="60064-304">스크립트가 현재 Reporting Services에 대해 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-304">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="60064-305">Reporting Services에 대한 스크립트를 실행하려는 경우 Get-WmiObject 문에서 네임스페이스 경로의 버전 부분을 "v11"로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-305">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
10. <span data-ttu-id="60064-306">스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-306">Run the script.</span></span>

<span data-ttu-id="60064-307">**유효성 검사**: 기본 보고서 서버 기능이 작동하는지 확인하려면 이 항목의 뒷부분에 나오는 [구성 확인](#verify-the-connection) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-307">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="60064-308">인증서 바인딩을 확인하려면 관리자 권한으로 명령 프롬프트를 연 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-308">To verify the certificate binding open a command prompt with administrative privileges, and then run the following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="60064-309">결과에는 다음이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-309">The result will include the following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-to-configure-the-report-server"></a><span data-ttu-id="60064-310">구성 관리자를 사용하여 보고서 서버 구성</span><span class="sxs-lookup"><span data-stu-id="60064-310">Use Configuration Manager to Configure the Report Server</span></span>
<span data-ttu-id="60064-311">PowerShell 스크립트를 실행하여 보고서 서버를 구성하지 않으려는 경우 이 섹션의 단계를 따라 Reporting Services 기본 모드 구성 관리자를 사용하여 보고서 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-311">If you do not want to run the PowerShell script to configure the report server, follow the steps in this section to use the Reporting Services native mode configuration manager to configure the report server.</span></span>

1. <span data-ttu-id="60064-312">Azure 클래식 포털에서 VM을 선택하고 연결을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-312">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="60064-313">VM을 만들 때 구성한 사용자 이름 및 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-313">Use the user name and password you configured when you created the VM.</span></span>
   
    ![Azure 가상 컴퓨터에 연결](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="60064-315">Windows 업데이트를 실행하고 VM에 대한 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-315">Run Windows update and install updates to the VM.</span></span> <span data-ttu-id="60064-316">VM 재시작이 필요한 경우, VM을 재시작하고 Azure 클래식 포털에서 VM을 재연결합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-316">If a restart of the VM is required, restart the VM and reconnect to the VM from the Azure classic portal.</span></span>
3. <span data-ttu-id="60064-317">VM의 시작 메뉴에서 **Reporting Services**를 입력하고 **Reporting Services 구성 관리자**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="60064-317">From the Start menu on the VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="60064-318">**서버 이름** 및 **보고서 서버 인스턴스**의 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="60064-318">Leave the default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="60064-319">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-319">Click **Connect**.</span></span>
5. <span data-ttu-id="60064-320">왼쪽 창에서 **웹 서비스 URL**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-320">In the left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="60064-321">기본적으로 RS는 IP가 “모두 할당됨"으로 HTTP 포트 80에 대해 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="60064-322">HTTPS를 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="60064-322">To add HTTPS:</span></span>
   
   1. <span data-ttu-id="60064-323">**SSL 인증서**에서: 사용하려는 인증서를 선택합니다. 예를 들어 [VM 이름].cloudapp.net입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-323">In **SSL Certificate**: select the certificate you want to use, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="60064-324">인증서가 나열되지 않은 경우 VM에서 인증서를 설치하고 신뢰하는 방법이 설명된 **2단계: 서버 인증서 만들기** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-324">If no certificates are listed, see the section **Step 2: Create a Server Certificate** for information on how to install and trust the certificate on the VM.</span></span>
   2. <span data-ttu-id="60064-325">**SSL 포트**에서: 443을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="60064-326">VM에 다른 개인 포트를 사용하여 HTTPS 개인 끝점을 구성한 경우 해당 값을 여기에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-326">If you configured the HTTPS private endpoint in the VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="60064-327">**적용** 을 클릭하고 작업이 완료되기를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="60064-327">Click **Apply** and wait for the operation to complete.</span></span>
7. <span data-ttu-id="60064-328">왼쪽 창에서 **데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-328">In the left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="60064-329">**데이터베이스 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="60064-330">**새 보고서 서버 데이터베이스 만들기**를 클릭한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="60064-331">기본 **서버 이름**을 VM 이름으로 그대로 적용하고 기본 **인증 유형**을 **현재 사용자** – **통합된 보안**으로 그대로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-331">Leave the default **Server Name**: as the VM name and leave the default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="60064-332">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="60064-332">Click **Next**.</span></span>
   4. <span data-ttu-id="60064-333">기본 **데이터베이스 이름**을 **ReportServer**로 그대로 적용하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-333">Leave the default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="60064-334">기본 **인증 유형**을 **서비스 자격 증명**으로 그대로 적용하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-334">Leave the default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="60064-335">왼쪽 창에서 **다음** on the **다음** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-335">Click **Next** on the **Summary** page.</span></span>
   7. <span data-ttu-id="60064-336">구성 단계가 완료되면 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-336">When the configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="60064-337">왼쪽 창에서 **보고서 관리자 URL**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-337">In the left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="60064-338">기본 **가상 디렉터리**를 **보고서**로 그대로 적용하고 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-338">Leave the default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="60064-339">**종료** 를 클릭하여 Reporting Services 구성 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-339">Click **Exit** to close the Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="60064-340">4단계: Windows 방화벽 포트 열기</span><span class="sxs-lookup"><span data-stu-id="60064-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="60064-341">스크립트 중 하나를 사용하여 보고서 서버를 구성한 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-341">If you used one of the scripts to configure the report server, you can skip this section.</span></span> <span data-ttu-id="60064-342">스크립트에는 방화벽 포트를 여는 단계가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-342">The script included a step to open the firewall port.</span></span> <span data-ttu-id="60064-343">기본값은 HTTP의 경우 포트 80이고 HTTPS의 경우 포트 443입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-343">The default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="60064-344">가상 컴퓨터의 보고서 관리자 또는 보고서 서버에 원격으로 연결하려면 VM에서 TCP 끝점이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-344">To connect remotely to Report Manager or the Report Server on the virtual machine, a TCP Endpoint is required on the VM.</span></span> <span data-ttu-id="60064-345">이는 VM의 방화벽에서 동일한 포트를 여는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-345">It is required to open the same port in the VM’s firewall.</span></span> <span data-ttu-id="60064-346">VM이 프로비전되었을 때 끝점이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-346">The endpoint was created when the VM was provisioned.</span></span>

<span data-ttu-id="60064-347">이 섹션에서는 방화벽 포트를 여는 방법에 대한 기본 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-347">This section provides basic information on how to open the firewall port.</span></span> <span data-ttu-id="60064-348">자세한 내용은 [보고서 서버 액세스를 위한 방화벽 구성](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="60064-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="60064-349">스크립트를 사용하여 보고서 서버를 구성한 경우 이 섹션을 건너뛰면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-349">If you used the script to configure the report server, you can skip this section.</span></span> <span data-ttu-id="60064-350">스크립트에는 방화벽 포트를 여는 단계가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-350">The script included a step to open the firewall port.</span></span>
> 
> 

<span data-ttu-id="60064-351">HTTPS에 대해 443 이외의 개인 포트를 구성한 경우 다음 스크립트를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-351">If you configured a private port for HTTPS other than 443, modify the following script appropriately.</span></span> <span data-ttu-id="60064-352">Windows 방화벽에서 포트 **443** 을 열려면 다음을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-352">To open port **443** on the Windows Firewall, complete the following:</span></span>

1. <span data-ttu-id="60064-353">관리자 권한으로 Windows PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="60064-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="60064-354">VM에서 HTTPS 끝점을 구성할 때 443 이외의 포트를 사용한 경우 다음 명령에서 포트를 업데이트하고 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-354">If you used a port other than 443 when you configured the HTTPS endpoint on the VM, update the port in the following command and then run the command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="60064-355">명령이 완료되면 **Ok** 가 명령 프롬프트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-355">When the command completes, **Ok** is displayed in the command prompt.</span></span>

<span data-ttu-id="60064-356">포트가 열렸는지 확인하려면 Windows PowerShell 창을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-356">To verify that the port is opened, open a Windows PowerShell window and run the following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-the-configuration"></a><span data-ttu-id="60064-357">구성 확인</span><span class="sxs-lookup"><span data-stu-id="60064-357">Verify the configuration</span></span>
<span data-ttu-id="60064-358">이제 기본 보고서 서버 기능이 작동하는지 확인하려면 관리자 권한으로 브라우저를 열고 다음 보고서 서버 AD 보고서 관리자 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-358">To verify that the basic report server functionality is now working, open your browser with administrative privileges and then browse to the following report server ad report manager URLS:</span></span>

* <span data-ttu-id="60064-359">VM에서 보고서 서버 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-359">On the VM, browse to the report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="60064-360">VM에서 보고서 관리자 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-360">On the VM, browse to the report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="60064-361">로컬 컴퓨터의 VM에서 **원격** 보고서 관리자로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-361">From your local computer, browse to the **remote** report Manager on the VM.</span></span> <span data-ttu-id="60064-362">다음 예제에서 DNS 이름을 적절하게 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-362">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="60064-363">암호를 입력하라는 메시지가 표시되면 VM이 프로비전되었을 때 만든 관리자 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-363">When prompted for a password, use the administrator credentials you created when the VM was provisioned.</span></span> <span data-ttu-id="60064-364">사용자 이름은 [도메인]\[사용자 이름] 형식이며, 여기서 도메인은 VM 컴퓨터 이름입니다. 예를 들어 ssrsnativecloud\testuser입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-364">The user name is in the [Domain]\[user name] format, where the domain is the VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="60064-365">HTTP**S**를 사용하지 않는 경우 URL에서 **s**를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-365">If you are not using HTTP**S**, remove the **s** in the URL.</span></span> <span data-ttu-id="60064-366">VM에서 추가 사용자를 만드는 방법에 대한 자세한 내용은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-366">See the next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="60064-367">로컬 컴퓨터에서 원격 보고서 서버 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-367">From your local computer, browse to the remote report server URL.</span></span> <span data-ttu-id="60064-368">다음 예제에서 DNS 이름을 적절하게 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-368">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="60064-369">HTTPS를 사용하지 않는 경우 URL에서 s를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-369">If you are not using HTTPS, remove the s in the URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="60064-370">사용자 만들기 및 역할 할당</span><span class="sxs-lookup"><span data-stu-id="60064-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="60064-371">보고서 서버를 구성하고 확인한 후 일반적인 관리 작업은 하나 이상의 사용자를 만들고 Reporting Services 역할에 사용자를 할당하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60064-371">After configuring and verifying the report server, a common administrative task is to create one or more users and assign users to Reporting Services roles.</span></span> <span data-ttu-id="60064-372">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-372">For more information, see the following:</span></span>

* [<span data-ttu-id="60064-373">로컬 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="60064-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="60064-374">[보고서 서버에 사용자 액세스 권한 부여(보고서 관리자)](https://msdn.microsoft.com/library/ms156034.aspx)</span><span class="sxs-lookup"><span data-stu-id="60064-374">[Grant User Access to a Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="60064-375">역할 할당 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="60064-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="to-create-and-publish-reports-to-the-azure-virtual-machine"></a><span data-ttu-id="60064-376">보고서를 만들고 Azure 가상 컴퓨터에 게시하려면</span><span class="sxs-lookup"><span data-stu-id="60064-376">To Create and Publish Reports to the Azure Virtual Machine</span></span>
<span data-ttu-id="60064-377">다음 표에는 온-프레미스 컴퓨터의 기존 보고서를 Microsoft Azure 가상 컴퓨터에 호스트된 보고서 서버에 게시하는 데 사용 가능한 일부 옵션이 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-377">The following table summarizes some of the options available to publish existing reports from an on-premises computer to the report server hosted on the Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="60064-378">**RS.exe 스크립트**: RS.exe 스크립트를 사용하여 기존 보고서 서버의 보고서 항목을 Microsoft Azure 가상 컴퓨터에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-378">**RS.exe script**: Use RS.exe script to copy report items from and existing report server to your Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="60064-379">자세한 내용은 [보고서 서버 간 콘텐츠 마이그레이션을 위한 예제 Reporting Services rs.exe 스크립트](https://msdn.microsoft.com/library/dn531017.aspx)의 "기본 모드에서 기본 모드로 – Microsoft Azure 가상 컴퓨터" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-379">For more information, see the section “Native mode to Native Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="60064-380">**보고서 작성기**: 가상 컴퓨터는 Microsoft SQL Server 보고서 작성기의 ClickOnce 버전을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-380">**Report Builder**: The virtual machine includes the click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="60064-381">가상 컴퓨터에서 처음으로 보고서 작성기를 시작하려면:</span><span class="sxs-lookup"><span data-stu-id="60064-381">To start Report builder the first time on the virtual machine:</span></span>
  
  1. <span data-ttu-id="60064-382">관리자 권한으로 브라우저를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="60064-383">가상 컴퓨터에서 보고서 관리자로 이동하고 리본에서 **보고서 작성기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-383">Browse to report manager on the virtual machine and click **Report Builder**  in the ribbon.</span></span>
     
     <span data-ttu-id="60064-384">자세한 내용은 [보고서 작성기 설치, 제거 및 지원](https://technet.microsoft.com/library/dd207038.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="60064-385">**SQL Server Data Tools: VM**: SQL Server 2012를 사용하여 VM을 만든 경우 SQL Server Data Tools가 가상 컴퓨터에 설치되어 있으므로 가상 컴퓨터에서 **보고서 서버 프로젝트** 및 보고서를 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-385">**SQL Server Data Tools: VM**:  If you created the VM with SQL Server 2012, then SQL Server Data Tools is installed on the virtual machine and can be used to create **Report Server Projects** and reports on the virtual machine.</span></span> <span data-ttu-id="60064-386">SQL Server Data Tools는 보고서를 가상 컴퓨터의 보고서 서버에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-386">SQL Server Data Tools can publish the reports to the report server on the virtual machine.</span></span>
  
    <span data-ttu-id="60064-387">SQL Server 2014에서 VM을 만든 경우 SQL Server Data Tools - Visual Studio용 BI를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60064-387">If you created the VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="60064-388">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-388">For more information, see the following:</span></span>
  
  * [<span data-ttu-id="60064-389">Microsoft SQL Server Data Tools - Visual Studio 2013용 비즈니스 인텔리전스</span><span class="sxs-lookup"><span data-stu-id="60064-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="60064-390">Microsoft SQL Server Data Tools - Visual Studio 2012용 비즈니스 인텔리전스</span><span class="sxs-lookup"><span data-stu-id="60064-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="60064-391">SSDT-BI(SQL Server Data Tools 및 SQL Server Business Intelligence)</span><span class="sxs-lookup"><span data-stu-id="60064-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="60064-392">**SQL Server Data Tools: 원격**: 로컬 컴퓨터에서 SQL Server Data Tools로 Reporting Services 보고서가 포함된 Reporting Services 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60064-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="60064-393">웹 서비스 URL에 연결하도록 프로젝트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-393">Configure the project to connect to the web service URL.</span></span>
  
    ![SSRS 프로젝트의 SSDT 프로젝트 속성](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="60064-395">**스크립트 사용**: 스크립트를 사용하여 보고서 서버 콘텐츠를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-395">**Use script**: Use script to copy report server content.</span></span> <span data-ttu-id="60064-396">자세한 내용은 [보고서 서버 간 콘텐츠 마이그레이션을 위한 예제 Reporting Services rs.exe 스크립트](https://msdn.microsoft.com/library/dn531017.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-396">For more information, see [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-the-vm"></a><span data-ttu-id="60064-397">VM을 사용하지 않는 경우 비용 최소화</span><span class="sxs-lookup"><span data-stu-id="60064-397">Minimize cost if you are not using the VM</span></span>
> [!NOTE]
> <span data-ttu-id="60064-398">Azure 가상 컴퓨터를 사용하지 않을 때 요금을 최소화하려면, Azure 클래식 포털에서 VM을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-398">To minimize charges for your Azure Virtual Machines when not in use, shut down the VM from the Azure classic portal.</span></span> <span data-ttu-id="60064-399">VM 내의 Windows 전원 옵션을 사용하여 VM을 종료하면 VM에 대해 동일한 요금이 계속 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="60064-399">If you use the Windows power options inside a VM to shut down the VM, you are still charged the same amount for the VM.</span></span> <span data-ttu-id="60064-400">요금을 줄이려면 Azure 클래식 포털에서 VM을 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60064-400">To reduce charges, you need to shut down the VM in the Azure classic portal.</span></span> <span data-ttu-id="60064-401">VM이 더 이상 필요하지 않은 경우 저장소 요금이 부과되지 않도록 VM 및 연결된 .vhd 파일을 삭제해야 합니다. 자세한 내용은 [가상 컴퓨터 가격 책정 정보](https://azure.microsoft.com/pricing/details/virtual-machines/)의 FAQ 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-401">If you no longer need the VM, remember to delete the VM and the associated .vhd files to avoid storage charges.For more information, see the FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="60064-402">추가 정보</span><span class="sxs-lookup"><span data-stu-id="60064-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="60064-403">리소스</span><span class="sxs-lookup"><span data-stu-id="60064-403">Resources</span></span>
* <span data-ttu-id="60064-404">SQL Server Business Intelligence 및 SharePoint 2013의 단일 서버 배포와 관련된 유사한 내용은 [Windows PowerShell을 사용하여 SQL Server BI 및 SharePoint 2013에서 Azure VM 만들기](https://msdn.microsoft.com/library/azure/dn385843.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-404">For similar content related to a single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell to Create an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="60064-405">SQL Server Business Intelligence 및 SharePoint 2013의 다중 서버 배포와 관련된 유사한 내용은 [Azure 가상 컴퓨터에서 SQL Server Business Intelligence 배포](https://msdn.microsoft.com/library/dn321998.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-405">For similar content related to a multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="60064-406">Azure 가상 컴퓨터에서 SQL Server Business Intelligence 배포와 관련된 일반 정보는 [Azure 가상 컴퓨터에서 SQL Server Business Intelligence](virtual-machines-windows-classic-ps-sql-bi.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-406">For General information related to deployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="60064-407">Azure 계산 요금의 비용에 대한 자세한 내용은 [Azure 가격 책정 계산기](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines)의 가상 컴퓨터 탭을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-407">For more information about the cost of Azure compute charges, see the Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="60064-408">커뮤니티 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="60064-408">Community Content</span></span>
* <span data-ttu-id="60064-409">스크립트를 사용하지 않고 Reporting Services 기본 모드 보고서 서버를 만드는 방법에 대한 단계별 지침은 [Azure 가상 컴퓨터에 SQL Reporting Services 호스트](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60064-409">For step by step instructions on how to create a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-to-other-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="60064-410">Azure VM의 SQL Server에 대한 기타 리소스 링크</span><span class="sxs-lookup"><span data-stu-id="60064-410">Links to other resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="60064-411">Azure 가상 컴퓨터의 SQL Server 개요</span><span class="sxs-lookup"><span data-stu-id="60064-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

