---
title: "aaaLOB 응용 프로그램 테스트 환경 | Microsoft Docs"
description: "어떻게 toocreate는 웹 기반의 비즈니스 응용 프로그램에는 하이브리드 클라우드 환경에 대 한 자세한 내용은 IT pro 또는 개발 테스트 합니다."
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
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="3ada3-103">테스트용 하이브리드 클라우드에 웹 기반 LOB 응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="3ada3-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="3ada3-104">이 항목에서는 Microsoft Azure에서 호스트되는 웹 기반 LOB(기간 업무) 응용 프로그램을 테스트하기 위한 시뮬레이션된 하이브리드 클라우드 환경을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="3ada3-105">다음은 hello 결과 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="3ada3-106">이 구성은 다음과 같이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-106">This configuration consists of:</span></span>

* <span data-ttu-id="3ada3-107">(테스트 랩 VNet hello) Azure에서 호스팅되는 시뮬레이션 된 온-프레미스 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-107">A simulated on-premises network hosted in Azure (hello TestLab VNet).</span></span>
* <span data-ttu-id="3ada3-108">Azure에서 호스트되는 크로스-프레미스 가상 네트워크(TestVNET)</span><span class="sxs-lookup"><span data-stu-id="3ada3-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="3ada3-109">VNet 간 VPN 연결</span><span class="sxs-lookup"><span data-stu-id="3ada3-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="3ada3-110">웹 기반 LOB 서버, SQL server 및 hello TestVNET 가상 네트워크의 보조 도메인 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-110">A web-based LOB server, SQL server, and secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="3ada3-111">이 구성은 다음 작업을 수행할 수 있는 기초 및 일반적인 시작 지점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="3ada3-112">Azure에서 SQL Server 2014 데이터베이스 백 엔드를 사용하여 IIS(인터넷 정보 서비스)에서 호스트되는 LOB 응용 프로그램 개발 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3ada3-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="3ada3-113">이 시뮬레이션된 하이브리드 클라우드 기반 IT 워크로드의 테스트 수행</span><span class="sxs-lookup"><span data-stu-id="3ada3-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="3ada3-114">이 하이브리드 클라우드 테스트 환경 구축 하는 세 가지 주요 단계 toosetting 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-114">There are three major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="3ada3-115">Hello 시뮬레이션 된 하이브리드 클라우드 환경을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-115">Set up hello simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="3ada3-116">Hello SQL server 컴퓨터 (SQL1)를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-116">Configure hello SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="3ada3-117">Hello LOB 서버 (LOB1)를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-117">Configure hello LOB server (LOB1).</span></span>

<span data-ttu-id="3ada3-118">이 워크로드에는 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="3ada3-119">MSDN 또는 Visual Studio 구독이 있는 경우에는 [Visual Studio 구독자를 위한 월간 Azure 크레딧](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ada3-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="3ada3-120">프로덕션 Azure에서 호스팅되는 LOB 응용 프로그램의 예를 들어 참조 hello **업무용 응용 프로그램** 에서 아키텍처 청사진 [Microsoft 소프트웨어 아키텍처 다이어그램 및 청사진](http://msdn.microsoft.com/dn630664)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-120">For an example of a production LOB application hosted in Azure, see hello **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a><span data-ttu-id="3ada3-121">1 단계: hello 시뮬레이션 된 하이브리드 클라우드 환경 설정</span><span class="sxs-lookup"><span data-stu-id="3ada3-121">Phase 1: Set up hello simulated hybrid cloud environment</span></span>
<span data-ttu-id="3ada3-122">Hello 만들기 [시뮬레이션 된 하이브리드 클라우드 테스트 환경](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-122">Create hello [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="3ada3-123">이 테스트 환경을 hello hello APP1 서버 hello Corpnet 서브넷에 있는지에 필요 하지 않으면 때문에 당분간를 종료 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-123">Because this test environment does not require hello presence of hello APP1 server on hello Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="3ada3-124">다음은 현재 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a><span data-ttu-id="3ada3-125">2 단계: 구성 hello SQL server 컴퓨터 (SQL1)</span><span class="sxs-lookup"><span data-stu-id="3ada3-125">Phase 2: Configure hello SQL server computer (SQL1)</span></span>
<span data-ttu-id="3ada3-126">Hello Azure 포털에서에서 필요한 경우 hello DC2 컴퓨터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-126">From hello Azure portal, start hello DC2 computer if needed.</span></span>

<span data-ttu-id="3ada3-127">그런 다음 로컬 컴퓨터의 Azure PowerShell 명령 프롬프트에서 다음 명령을 사용하여 SQL1용 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="3ada3-128">이전 toorunning hello 변수 값 및 제거 hello < 및 > 문자에서 이러한 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-128">Prior toorunning these commands, fill in hello variable values and remove hello < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="3ada3-129">S q l 1의 hello 로컬 관리자 계정을 사용 하 여 Azure 포털 tooconnect tooSQL1 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-129">Use hello Azure portal tooconnect tooSQL1 using hello local administrator account of SQL1.</span></span>

<span data-ttu-id="3ada3-130">Windows 방화벽 규칙 tooallow 기본 연결 테스트 및 SQL Server 트래픽 다음으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-130">Next, configure Windows Firewall rules tooallow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="3ada3-131">SQL1의 관리자 수준 Windows PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="3ada3-132">IP 주소 192.168.0.4에서에서 4 개의 성공 응답 hello ping 명령을 발생 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-132">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="3ada3-133">다음으로 hello 추가 hello 드라이브 문자 f: 새 볼륨으로 s q l 1에서 추가 데이터 디스크.</span><span class="sxs-lookup"><span data-stu-id="3ada3-133">Next, add hello extra data disk on SQL1 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="3ada3-134">Hello 왼쪽된 창에서 서버 관리자의을 클릭 **파일 및 저장소 서비스**, 클릭 하 고 **디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-134">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="3ada3-135">Hello 내용 창의 hello **디스크** 그룹에서 클릭 **2 디스크** (hello로 **파티션** 도**알 수 없는**).</span><span class="sxs-lookup"><span data-stu-id="3ada3-135">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="3ada3-136">**작업**을 클릭한 후 **새 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="3ada3-137">Hello hello 새 볼륨 마법사의 페이지를 시작 하기 전에 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-137">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="3ada3-138">Hello 선택 hello 서버 및 디스크 페이지에서 클릭 **디스크 2**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-138">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="3ada3-139">메시지가 표시되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="3ada3-140">Hello hello 볼륨 페이지의 hello 크기 지정, 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-140">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="3ada3-141">Hello 할당 tooa 드라이브 문자 또는 폴더 페이지를 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-141">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="3ada3-142">Hello 선택 파일 시스템 설정 페이지에서 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-142">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="3ada3-143">선택 확인 페이지 hello 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-143">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="3ada3-144">완료되면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-144">When complete, click **Close**.</span></span>

<span data-ttu-id="3ada3-145">S q l 1 hello Windows PowerShell 명령 프롬프트에서 이러한 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-145">Run these commands at hello Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="3ada3-146">다음에 s q l 1 hello Windows PowerShell 프롬프트에서 다음이 명령 사용 하 여 s q l 1 toohello 회사 Windows Server Active Directory 도메인에 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-146">Next, join SQL1 toohello CORP Windows Server Active Directory domain with these commands at hello Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="3ada3-147">메시지가 나타나면 CORP\User1 hello 계정을 사용 하 여 hello에 대 한 도메인 계정 자격 증명 toosupply **Add-computer** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-147">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="3ada3-148">를 다시 시작한 후 Azure 포털 tooconnect tooSQL1 hello를 사용 하 여 *s q l 1의 hello 로컬 관리자 계정으로*합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-148">After restarting, use hello Azure portal tooconnect tooSQL1 *with hello local administrator account of SQL1*.</span></span>

<span data-ttu-id="3ada3-149">다음으로, 사용자 계정 권한을 새 데이터베이스에 대해 SQL Server 2014 toouse hello f: 드라이브를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-149">Next, configure SQL Server 2014 toouse hello F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="3ada3-150">Hello 시작 화면에서 입력 **SQL Server Management**, 클릭 하 고 **SQL Server 2014 Management Studio**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-150">From hello Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="3ada3-151">**tooServer 연결**, 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-151">In **Connect tooServer**, click **Connect**.</span></span>
3. <span data-ttu-id="3ada3-152">Hello 개체 탐색기 트리 창에서 마우스 오른쪽 단추로 클릭 **SQL1**, 클릭 하 고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-152">In hello Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="3ada3-153">Hello에 **서버 속성** 창 클릭 **데이터베이스 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-153">In hello **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="3ada3-154">Hello 찾을 **데이터베이스 기본 위치** 이러한 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-154">Locate hello **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="3ada3-155">에 대 한 **데이터**, hello 경로 형식의 **f:\Data**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-155">For **Data**, type hello path **f:\Data**.</span></span>
   * <span data-ttu-id="3ada3-156">에 대 한 **로그**, hello 경로 형식의 **f:\Log**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-156">For **Log**, type hello path **f:\Log**.</span></span>
   * <span data-ttu-id="3ada3-157">에 대 한 **백업**, hello 경로 형식의 **f:\Backup**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-157">For **Backup**, type hello path **f:\Backup**.</span></span>
   * <span data-ttu-id="3ada3-158">참고: 새 데이터베이스에서만 이러한 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="3ada3-159">Hello 클릭 **확인** tooclose hello 창.</span><span class="sxs-lookup"><span data-stu-id="3ada3-159">Click hello **OK** tooclose hello window.</span></span>
7. <span data-ttu-id="3ada3-160">Hello에 **개체 탐색기** 트리 창에서 열기 **보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-160">In hello **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="3ada3-161">**로그인**을 마우스 오른쪽 단추로 클릭하고 **새 로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="3ada3-162">**로그인 이름**에 **CORP\User1**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="3ada3-163">Hello에 **서버 역할** 페이지 **sysadmin**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-163">On hello **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="3ada3-164">Microsoft SQL Server Management Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="3ada3-165">다음은 현재 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a><span data-ttu-id="3ada3-166">3 단계: hello LOB 서버 (LOB1)를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-166">Phase 3: Configure hello LOB server (LOB1)</span></span>
<span data-ttu-id="3ada3-167">먼저 로컬 컴퓨터에 hello Azure PowerShell 명령 프롬프트에서 다음이 명령을 사용 하 여 LOB1에 대 한 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-167">First, create a virtual machine for LOB1 with these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="3ada3-168">를 사용 하 여 hello Azure 포털 tooconnect tooLOB1 LOB1의 hello 로컬 관리자 계정의 hello 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-168">Next, use hello Azure portal tooconnect tooLOB1 with hello credentials of hello local administrator account of LOB1.</span></span>

<span data-ttu-id="3ada3-169">다음으로 기본 연결을 테스트 하는 것에 대 한 Windows 방화벽 규칙 tooallow 트래픽을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-169">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="3ada3-170">LOB1의 관리자 수준 Windows PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="3ada3-171">IP 주소 192.168.0.4에서에서 4 개의 성공 응답 hello ping 명령을 발생 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-171">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="3ada3-172">다음으로 hello Windows PowerShell 프롬프트에서 다음이 명령 사용 하 여 LOB1 toohello CORP Active Directory 도메인에 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-172">Next, join LOB1 toohello CORP Active Directory domain with these commands at hello Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="3ada3-173">메시지가 나타나면 CORP\User1 hello 계정을 사용 하 여 hello에 대 한 도메인 계정 자격 증명 toosupply **Add-computer** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-173">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="3ada3-174">를 다시 시작한 후 Azure 포털 tooconnect tooLOB1 hello를 사용 하 여 hello CORP\User1 계정 및 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-174">After restarting, use hello Azure portal tooconnect tooLOB1 with hello CORP\User1 account and password.</span></span>

<span data-ttu-id="3ada3-175">그런 다음 IIS에 대해 LOB1을 구성하고 CLIENT1의 액세스를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="3ada3-176">서버 관리자에서 **역할 및 기능 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="3ada3-177">Hello에 **시작 하기 전에** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-177">On hello **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="3ada3-178">Hello에 **설치 유형 선택** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-178">On hello **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="3ada3-179">Hello에 **대상 서버 선택** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-179">On hello **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="3ada3-180">Hello에 **서버 역할** 페이지 **웹 서버 (IIS)** hello 목록에 **역할**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-180">On hello **Server roles** page, click **Web Server (IIS)** in hello list of **Roles**.</span></span>
6. <span data-ttu-id="3ada3-181">메시지가 나타나면 **기능 추가**를 클릭하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="3ada3-182">Hello에 **기능 선택** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-182">On hello **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="3ada3-183">Hello에 **웹 서버 (IIS)** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-183">On hello **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="3ada3-184">Hello에 **역할 서비스 선택** 페이지 선택 또는 hello LOB 응용 프로그램 테스트에 필요한 hello 서비스에 대 한 확인란의 선택을 취소 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-184">On hello **Select role services** page, select or clear hello check boxes for hello services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="3ada3-185">Hello에 **설치 선택 확인** 페이지 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-185">On hello **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="3ada3-186">구성 요소의 hello 설치가 완료 될 때까지 기다린 후 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-186">Wait until hello installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="3ada3-187">Hello Azure 포털에서에서 hello CORP\User1 계정 자격 증명을 사용 하 여 toohello CLIENT1 컴퓨터를 연결 하 고 Internet Explorer를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-187">From hello Azure portal, connect toohello CLIENT1 computer with hello CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="3ada3-188">Hello 주소 표시줄에 입력 **http://lob1/** 한 다음 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-188">In hello Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="3ada3-189">Hello 기본 IIS 8 웹 페이지 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-189">You should see hello default IIS 8 web page.</span></span>

<span data-ttu-id="3ada3-190">다음은 현재 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="3ada3-191">이 환경은 이제 웹 기반 응용 프로그램 LOB1 및 테스트 하는 기능에 CLIENT1에서 hello Corpnet 서브넷에 대기 중인 toodeploy 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-191">This environment is now ready for you toodeploy your web-based application on LOB1 and test functionality from CLIENT1 on hello Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="3ada3-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3ada3-192">Next step</span></span>
* <span data-ttu-id="3ada3-193">Hello를 사용 하 여 새 가상 컴퓨터를 추가 [Azure 포털](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ada3-193">Add a new virtual machine using hello [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

