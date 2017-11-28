---
title: "LOB 응용 프로그램 테스트 환경 | Microsoft Docs"
description: "IT 전문가 또는 개발 테스트용 하이브리드 클라우드에 웹 기반 LOB(기간 업무) 응용 프로그램을 설치하는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 8e9a380458bfede80ed0fc1ee7e62b0caec09501
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="a3ae3-103">테스트용 하이브리드 클라우드에 웹 기반 LOB 응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="a3ae3-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="a3ae3-104">이 항목에서는 Microsoft Azure에서 호스트되는 웹 기반 LOB(기간 업무) 응용 프로그램을 테스트하기 위한 시뮬레이션된 하이브리드 클라우드 환경을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="a3ae3-105">다음은 결과 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-105">Here is the resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="a3ae3-106">이 구성은 다음과 같이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-106">This configuration consists of:</span></span>

* <span data-ttu-id="a3ae3-107">Azure에서 호스팅되는 시뮬레이션된 온-프레미스 네트워크(TestLab VNet)</span><span class="sxs-lookup"><span data-stu-id="a3ae3-107">A simulated on-premises network hosted in Azure (the TestLab VNet).</span></span>
* <span data-ttu-id="a3ae3-108">Azure에서 호스트되는 크로스-프레미스 가상 네트워크(TestVNET)</span><span class="sxs-lookup"><span data-stu-id="a3ae3-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="a3ae3-109">VNet 간 VPN 연결</span><span class="sxs-lookup"><span data-stu-id="a3ae3-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="a3ae3-110">TestVNET 가상 네트워크의 웹 기반 LOB(기간 업무) 서버, SQL Server 및 보조 도메인 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="a3ae3-110">A web-based LOB server, SQL server, and secondary domain controller in the TestVNET virtual network.</span></span>

<span data-ttu-id="a3ae3-111">이 구성은 다음 작업을 수행할 수 있는 기초 및 일반적인 시작 지점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="a3ae3-112">Azure에서 SQL Server 2014 데이터베이스 백 엔드를 사용하여 IIS(인터넷 정보 서비스)에서 호스트되는 LOB 응용 프로그램 개발 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a3ae3-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="a3ae3-113">이 시뮬레이션된 하이브리드 클라우드 기반 IT 워크로드의 테스트 수행</span><span class="sxs-lookup"><span data-stu-id="a3ae3-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="a3ae3-114">이 하이브리드 클라우드 테스트 환경을 설정하는 세 가지 주요 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-114">There are three major phases to setting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="a3ae3-115">시뮬레이션된 하이브리드 클라우드 환경 설정</span><span class="sxs-lookup"><span data-stu-id="a3ae3-115">Set up the simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="a3ae3-116">SQL Server 컴퓨터(SQL1) 구성</span><span class="sxs-lookup"><span data-stu-id="a3ae3-116">Configure the SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="a3ae3-117">LOB 서버(LOB1) 구성</span><span class="sxs-lookup"><span data-stu-id="a3ae3-117">Configure the LOB server (LOB1).</span></span>

<span data-ttu-id="a3ae3-118">이 워크로드에는 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="a3ae3-119">MSDN 또는 Visual Studio 구독이 있는 경우에는 [Visual Studio 구독자를 위한 월간 Azure 크레딧](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="a3ae3-120">Azure에서 호스트되는 프로덕션 LOB 응용 프로그램의 예는 **Microsoft 소프트웨어 아키텍처 다이어그램 및 청사진** 에서 [LOB(기간 업무) 응용 프로그램](http://msdn.microsoft.com/dn630664)아키텍처 청사진을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-120">For an example of a production LOB application hosted in Azure, see the **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-the-simulated-hybrid-cloud-environment"></a><span data-ttu-id="a3ae3-121">1단계: 시뮬레이션된 하이브리드 클라우드 환경 설정</span><span class="sxs-lookup"><span data-stu-id="a3ae3-121">Phase 1: Set up the simulated hybrid cloud environment</span></span>
<span data-ttu-id="a3ae3-122">[시뮬레이션된 하이브리드 클라우드 테스트 환경](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-122">Create the [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a3ae3-123">이 테스트 환경에는 APP1 서버가 Corpnet 서브넷에 있을 필요가 없으므로 지금은 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-123">Because this test environment does not require the presence of the APP1 server on the Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="a3ae3-124">다음은 현재 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-the-sql-server-computer-sql1"></a><span data-ttu-id="a3ae3-125">2단계: SQL Server 컴퓨터(SQL1) 구성</span><span class="sxs-lookup"><span data-stu-id="a3ae3-125">Phase 2: Configure the SQL server computer (SQL1)</span></span>
<span data-ttu-id="a3ae3-126">Azure 포털에서 DC2 컴퓨터(필요한 경우)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-126">From the Azure portal, start the DC2 computer if needed.</span></span>

<span data-ttu-id="a3ae3-127">그런 다음 로컬 컴퓨터의 Azure PowerShell 명령 프롬프트에서 다음 명령을 사용하여 SQL1용 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="a3ae3-128">이러한 명령을 실행하기 전에 변수 값을 작성하고 < and > 문자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-128">Prior to running these commands, fill in the variable values and remove the < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<the Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type the name and password of the local administrator account for the SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="a3ae3-129">Azure 포털을 사용하여 SQL1의 로컬 관리자 계정으로 SQL1에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-129">Use the Azure portal to connect to SQL1 using the local administrator account of SQL1.</span></span>

<span data-ttu-id="a3ae3-130">다음으로 기본 연결 테스트 및 SQL Server 트래픽을 허용하도록 Windows 방화벽 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-130">Next, configure Windows Firewall rules to allow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="a3ae3-131">SQL1의 관리자 수준 Windows PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="a3ae3-132">Ping 명령을 실행한 경우 IP 주소 192.168.0.4에서 성공적인 회신 4개가 수신되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-132">The ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="a3ae3-133">다음으로 SQL1에서 추가 데이터 디스크를 드라이브 문자가 F:인 새 볼륨으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-133">Next, add the extra data disk on SQL1 as a new volume with the drive letter F:.</span></span>

1. <span data-ttu-id="a3ae3-134">Server Manager의 왼쪽 창에서 **파일 및 저장소 서비스**를 클릭한 다음 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-134">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="a3ae3-135">내용 창의 **디스크** 그룹에서 **디스크 2**(**파티션**이 **알 수 없음**으로 설정됨)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-135">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span></span>
3. <span data-ttu-id="a3ae3-136">**작업**을 클릭한 후 **새 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="a3ae3-137">새 볼륨 마법사의 시작하기 전에 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-137">On the Before you begin page of the New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="a3ae3-138">서버 및 디스크 선택 페이지에서 **디스크 2**를 클릭하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-138">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="a3ae3-139">메시지가 표시되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="a3ae3-140">볼륨 크기를 선택합니다 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-140">On the Specify the size of the volume page, click **Next**.</span></span>
7. <span data-ttu-id="a3ae3-141">드라이브 문자 또는 폴더에 할당 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-141">On the Assign to a drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="a3ae3-142">파일 시스템 설정 선택 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-142">On the Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="a3ae3-143">선택 확인 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-143">On the Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="a3ae3-144">완료되면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-144">When complete, click **Close**.</span></span>

<span data-ttu-id="a3ae3-145">SQL1의 Windows PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-145">Run these commands at the Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="a3ae3-146">다음으로, SQL1의 Window PowerShell 프롬프트에서 이러한 명령을 사용하여 SQL1을 CORP Windows Server Active Directory 도메인에 가입합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-146">Next, join SQL1 to the CORP Windows Server Active Directory domain with these commands at the Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="a3ae3-147">**Add-Computer** 명령에 대한 도메인 계정 자격 증명을 제공하라는 메시지가 표시되면 CORP\User1 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-147">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span></span>

<span data-ttu-id="a3ae3-148">다시 시작한 후 Azure 포털을 사용하여 *SQL1의 로컬 관리자 계정으로*SQL1에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-148">After restarting, use the Azure portal to connect to SQL1 *with the local administrator account of SQL1*.</span></span>

<span data-ttu-id="a3ae3-149">그런 다음 새 데이터베이스 및 사용자 계정 권한에 F: 드라이브를 사용하도록 SQL Server 2014를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-149">Next, configure SQL Server 2014 to use the F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="a3ae3-150">시작 화면에서 **SQL Server 관리**를 입력하고 **SQL Server 2014 Management Studio**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-150">From the Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="a3ae3-151">**서버에 연결**에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-151">In **Connect to Server**, click **Connect**.</span></span>
3. <span data-ttu-id="a3ae3-152">개체 탐색기 트리 창에서 **SQL1**을 지정한 다음 **속성**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-152">In the Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="a3ae3-153">**서버 속성** 창에서 **데이터베이스 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-153">In the **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="a3ae3-154">**데이터베이스 기본 위치** 를 찾아서 다음 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-154">Locate the **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="a3ae3-155">**데이터**에 경로 **f:\Data**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-155">For **Data**, type the path **f:\Data**.</span></span>
   * <span data-ttu-id="a3ae3-156">**로그**에 경로 **f:\Log**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-156">For **Log**, type the path **f:\Log**.</span></span>
   * <span data-ttu-id="a3ae3-157">**백업**에 경로 **f:\Backup**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-157">For **Backup**, type the path **f:\Backup**.</span></span>
   * <span data-ttu-id="a3ae3-158">참고: 새 데이터베이스에서만 이러한 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="a3ae3-159">**확인** 을 클릭하여 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-159">Click the **OK** to close the window.</span></span>
7. <span data-ttu-id="a3ae3-160">**개체 탐색기** 트리 창에서 **보안**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-160">In the **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="a3ae3-161">**로그인**을 마우스 오른쪽 단추로 클릭하고 **새 로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="a3ae3-162">**로그인 이름**에 **CORP\User1**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="a3ae3-163">**서버 역할** 페이지에서 **sysadmin**을 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-163">On the **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="a3ae3-164">Microsoft SQL Server Management Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="a3ae3-165">다음은 현재 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-the-lob-server-lob1"></a><span data-ttu-id="a3ae3-166">3단계: LOB 서버(LOB1) 구성</span><span class="sxs-lookup"><span data-stu-id="a3ae3-166">Phase 3: Configure the LOB server (LOB1)</span></span>
<span data-ttu-id="a3ae3-167">먼저 로컬 컴퓨터의 Azure PowerShell 명령 프롬프트에서 다음 명령을 사용하여 LOB1용 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-167">First, create a virtual machine for LOB1 with these commands at the Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type the name and password of the local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="a3ae3-168">다음으로, Azure 포털을 사용하여 LOB1의 로컬 관리자 계정의 자격 증명으로 LOB1에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-168">Next, use the Azure portal to connect to LOB1 with the credentials of the local administrator account of LOB1.</span></span>

<span data-ttu-id="a3ae3-169">그런 다음 기본 연결 테스트에 대한 트래픽을 허용하도록 Windows 방화벽 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-169">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span></span> <span data-ttu-id="a3ae3-170">LOB1의 관리자 수준 Windows PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="a3ae3-171">Ping 명령을 실행한 경우 IP 주소 192.168.0.4에서 성공적인 회신 4개가 수신되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-171">The ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="a3ae3-172">다음으로, Window Power Shell 프롬프트에서 이러한 명령을 사용하여 LOB1을 CORP Active Directory 도메인에 가입합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-172">Next, join LOB1 to the CORP Active Directory domain with these commands at the Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="a3ae3-173">**Add-Computer** 명령에 대한 도메인 계정 자격 증명을 제공하라는 메시지가 표시되면 CORP\User1 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-173">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span></span>

<span data-ttu-id="a3ae3-174">다시 시작한 후 Azure 포털을 사용하여 CORP\User1 계정 및 암호로 LOB1에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-174">After restarting, use the Azure portal to connect to LOB1 with the CORP\User1 account and password.</span></span>

<span data-ttu-id="a3ae3-175">그런 다음 IIS에 대해 LOB1을 구성하고 CLIENT1의 액세스를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="a3ae3-176">서버 관리자에서 **역할 및 기능 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="a3ae3-177">**시작하기 전에** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-177">On the **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="a3ae3-178">**설치 유형 선택** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-178">On the **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="a3ae3-179">**대상 서버 선택** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-179">On the **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="a3ae3-180">**서버 역할** 페이지의 **역할** 목록에서 **웹 서버(IIS)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-180">On the **Server roles** page, click **Web Server (IIS)** in the list of **Roles**.</span></span>
6. <span data-ttu-id="a3ae3-181">메시지가 나타나면 **기능 추가**를 클릭하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="a3ae3-182">**기능 선택** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-182">On the **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="a3ae3-183">**웹 서버(IIS)** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-183">On the **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="a3ae3-184">**역할 서비스 선택** 페이지에서 LOB 응용 프로그램을 테스트하는 데 필요한 서비스의 확인란을 선택하거나 선택 취소하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-184">On the **Select role services** page, select or clear the check boxes for the services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="a3ae3-185">**설치 선택 확인** 페이지에서 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-185">On the **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="a3ae3-186">구성 요소 설치가 완료될 때까지 기다렸다가 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-186">Wait until the installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="a3ae3-187">Azure 포털에서 CORP\User1 계정 자격 증명으로 CLIENT1 컴퓨터에 연결한 다음 Internet Explorer를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-187">From the Azure portal, connect to the CLIENT1 computer with the CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="a3ae3-188">주소 표시줄에 **http://lob1/**을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-188">In the Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="a3ae3-189">기본 IIS 8 웹 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-189">You should see the default IIS 8 web page.</span></span>

<span data-ttu-id="a3ae3-190">다음은 현재 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="a3ae3-191">이제 이 환경은 LOB1의 웹 기반 응용 프로그램을 배포하고 Corpnet 서브넷의 CLIENT1에서 기능을 테스트할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-191">This environment is now ready for you to deploy your web-based application on LOB1 and test functionality from CLIENT1 on the Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="a3ae3-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a3ae3-192">Next step</span></span>
* <span data-ttu-id="a3ae3-193">[Azure Portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 사용하여 새 가상 컴퓨터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ae3-193">Add a new virtual machine using the [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

