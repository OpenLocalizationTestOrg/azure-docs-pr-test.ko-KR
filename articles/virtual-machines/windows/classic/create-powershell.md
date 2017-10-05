---
title: "PowerShell로 Windows VM 만들기 | Microsoft Docs"
description: "Azure PowerShell 및 클래식 배포 모델을 사용하여 Windows 가상 컴퓨터를 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 75c6cf17ee269ae169d9f2f748d0985ca07e454e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-the-classic-deployment-model"></a><span data-ttu-id="95e4b-103">PowerShell 및 클래식 배포 모델을 사용하여 Windows 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="95e4b-103">Create a Windows virtual machine with PowerShell and the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95e4b-104">Azure Portal - Windows</span><span class="sxs-lookup"><span data-stu-id="95e4b-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="95e4b-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="95e4b-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="95e4b-106">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="95e4b-107">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="95e4b-108">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="95e4b-109">[Resource Manager 모델을 사용하여 이러한 단계를 수행하는](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-109">Learn how to [perform these steps using the Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="95e4b-110">다음 단계에서는 구성 요소 접근 방식을 사용하여 Windows 기반 Azure 가상 컴퓨터를 만들고 미리 구성하는 Azure PowerShell 명령 집합을 사용자 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-110">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="95e4b-111">이 프로세스를 사용하여 새 Windows 기반 가상 컴퓨터에 대한 명령 집합을 신속하게 만들고 기존 배포를 확장하거나, 사용자 지정 개발/테스트 또는 IT 전문가 환경을 신속하게 빌드하는 여러 명령 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-111">You can use this process to quickly create a command set for a new Windows-based virtual machine and expand an existing deployment or to create multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="95e4b-112">다음 단계에서는 빈 칸 채우기 접근 방식에 따라 Azure PowerShell 명령 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="95e4b-113">이 접근 방식은 PowerShell을 처음 접하거나 성공적인 구성을 위해 지정할 값만 알기를 원하는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-113">This approach can be useful if you are new to PowerShell or you just want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="95e4b-114">고급 PowerShell 사용자는 명령을 가져와 고유한 변수 값("$"로 시작하는 줄)을 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-114">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="95e4b-115">[Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview) 의 지침을 사용하여 로컬 컴퓨터에 Azure PowerShell을 설치합니다(아직 설치하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="95e4b-115">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="95e4b-116">그런 다음 Windows PowerShell 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="95e4b-117">1단계: 사용자 계정 추가</span><span class="sxs-lookup"><span data-stu-id="95e4b-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="95e4b-118">PowerShell 프롬프트에서 **Add-AzureAccount**를 입력하고 **Enter**.</span><span class="sxs-lookup"><span data-stu-id="95e4b-118">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="95e4b-119">Azure 구독과 연관된 메일 주소를 입력하고 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-119">Type in the email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="95e4b-120">계정에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-120">Type in the password for your account.</span></span> 
4. <span data-ttu-id="95e4b-121">**로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="95e4b-122">2단계: 구독 및 저장소 계정 설정</span><span class="sxs-lookup"><span data-stu-id="95e4b-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="95e4b-123">Windows PowerShell 명령 프롬프트에서 다음 명령을 실행하여 Azure 구독 및 저장소 계정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-123">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="95e4b-124">< 및 > 문자를 포함하여 따옴표 안의 모든 항목을 올바른 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-124">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="95e4b-125">**Get-AzureSubscription** 명령의 출력에 표시된 SubscriptionName 속성에서 올바른 구독 이름을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-125">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="95e4b-126">**Select-AzureSubscription** 명령을 실행한 후 **Get-AzureStorageAccount** 명령의 출력에 표시된 Label 속성에서 올바른 저장소 계정 이름을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-126">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-the-imagefamily"></a><span data-ttu-id="95e4b-127">3단계: ImageFamily 확인</span><span class="sxs-lookup"><span data-stu-id="95e4b-127">Step 3: Determine the ImageFamily</span></span>
<span data-ttu-id="95e4b-128">이제 만들려는 Azure 가상 컴퓨터에 해당하는 특정 이미지에 대한 ImageFamily 또는 Label 값을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-128">Next, you need to determine the ImageFamily or Label value for the specific image corresponding to the Azure virtual machine you want to create.</span></span> <span data-ttu-id="95e4b-129">다음 명령을 사용하여 사용 가능한 ImageFamily 값 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-129">You can get the list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="95e4b-130">다음은 Windows 기반 컴퓨터의 ImageFamily 값에 대한 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="95e4b-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="95e4b-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="95e4b-132">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="95e4b-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="95e4b-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="95e4b-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="95e4b-134">Windows Server 2012의 SQL Server 2012 SP1 Enterprise</span><span class="sxs-lookup"><span data-stu-id="95e4b-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="95e4b-135">검색할 이미지를 찾은 경우, 선택한 텍스트 편집기 또는 PowerShell ISE(통합 스크립팅 환경)의 새 인스턴스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-135">If you find the image you are looking for, open a fresh instance of the text editor of your choice or the PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="95e4b-136">새 텍스트 파일 또는 ImageFamily 값을 대체하는 PowerShell ISE에 다음을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-136">Copy the following into the new text file or the PowerShell ISE, substituting the ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="95e4b-137">경우에 따라 ImageFamily 값 대신 Label 속성에 이미지 이름이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-137">In some cases, the image name is in the Label property instead of the ImageFamily value.</span></span> <span data-ttu-id="95e4b-138">ImageFamily 속성을 사용하여 원하는 이미지를 찾지 못한 경우 다음 명령을 사용하여 해당 Label 속성으로 이미지를 나열하세요.</span><span class="sxs-lookup"><span data-stu-id="95e4b-138">If you didn't find the image that you are looking for using the ImageFamily property, list the images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="95e4b-139">이 명령을 사용하여 올바른 이미지를 찾은 경우, 사용자가 선택한 텍스트 편집기 또는 PowerShell ISE의 새 인스턴스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-139">If you find the right image with this command, open a fresh instance of the text editor of your choice or the PowerShell ISE.</span></span> <span data-ttu-id="95e4b-140">새 텍스트 파일 또는 레이블 값을 대체하는 PowerShell ISE에 다음을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-140">Copy the following into the new text file or the PowerShell ISE, substituting the Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="95e4b-141">4단계: 명령 집합 작성</span><span class="sxs-lookup"><span data-stu-id="95e4b-141">Step 4: Build your command set</span></span>
<span data-ttu-id="95e4b-142">아래에서 해당 블록 집합을 새 텍스트 파일 또는 ISE에 복사한 다음 변수 값을 입력하고 < 및 > 문자를 제거하여 나머지 명령 집합을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-142">Build the rest of your command set by copying the appropriate set of blocks below into your new text file or the ISE and then filling in the variable values and removing the < and > characters.</span></span> <span data-ttu-id="95e4b-143">최종 결과의 개념은 이 문서 끝의 두 [예제](#examples) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95e4b-143">See the two [examples](#examples) at the end of this article for an idea of the final result.</span></span>

<span data-ttu-id="95e4b-144">다음 두 명령 블록 중 하나를 선택하여 명령 집합을 시작합니다(필수).</span><span class="sxs-lookup"><span data-stu-id="95e4b-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="95e4b-145">옵션 1: 가상 컴퓨터 이름 및 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="95e4b-146">옵션 2: 이름, 크기 및 가용성 집합 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="95e4b-147">D-, DS- 또는 G-시리즈 가상 컴퓨터에 대한 InstanceSize 값은 [Azure용 가상 컴퓨터 및 클라우드 서비스 크기](https://msdn.microsoft.com/library/azure/dn197896.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95e4b-147">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="95e4b-148">Software Assurance가 적용되는 기업 계약이 체결되어 있고 Windows Server [하이브리드 사용 혜택](https://azure.microsoft.com/pricing/hybrid-use-benefit/)을 활용하려는 경우 **New-AzureVMConfig**에 **-LicenseType** 매개 변수를 추가하고 일반적인 사용 사례에 대해 **Windows_Server** 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-148">If you have an Enterprise Agreement with Software Assurance, and intend to take advantage of the Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter to the **New-AzureVMConfig** cmdlet, passing the value **Windows_Server** for the typical use case.</span></span>  <span data-ttu-id="95e4b-149">업로드한 이미지를 사용하고 있는지 확인합니다. 하이브리드 사용 혜택으로 갤러리의 표준 이미지를 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-149">Be sure you are using an image you have uploaded; you cannot use a standard image from the Gallery with the Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="95e4b-150">독립 실행형 Windows 컴퓨터의 경우, 선택적으로 로컬 관리자 계정 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-150">Optionally, for a standalone Windows computer, specify the local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="95e4b-151">강력한 암호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-151">Choose a strong password.</span></span> <span data-ttu-id="95e4b-152">암호 강도를 확인하려면 [암호 검사기: 강력한 암호 사용](https://www.microsoft.com/security/pc-security/password-checker.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95e4b-152">To check its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="95e4b-153">선택적으로 Windows 컴퓨터를 기존 Active Directory 도메인에 추가하려면 로컬 관리자 계정 및 암호, 도메인, 도메인 계정의 이름 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-153">Optionally, to add the Windows computer to an existing Active Directory domain, specify the local administrator account and password, the domain, and the name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type the name and password of the local administrator account."
    $cred2=Get-Credential –Message "Now type the name (not including the domain) and password of an account that has permission to add the machine to the domain."
    $domaindns="<FQDN of the domain that the machine is joining>"
    $domacctdomain="<domain of the account that has permission to add the machine to the domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="95e4b-154">Windows 기반 가상 컴퓨터에 대한 추가 사전 구성 옵션은 [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig)에서 **Windows** 및 **WindowsDomain** 매개 변수 집합에 대한 구문을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95e4b-154">For additional pre-configuration options for Windows-based virtual machines, see the syntax for the **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="95e4b-155">선택적으로 가상 컴퓨터에 특정 IP 주소(고정 DIP라고 함)를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-155">Optionally, assign the virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="95e4b-156">특정 IP 주소를 사용할 수 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="95e4b-157">선택적으로 Azure 가상 네트워크의 특정 서브넷에 가상 컴퓨터를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-157">Optionally, assign the virtual machine to a specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of the subnet>"

<span data-ttu-id="95e4b-158">선택적으로 가상 컴퓨터에 단일 데이터 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-158">Optionally, add a single data disk to the virtual machine.</span></span>

    $disksize=<size of the disk in GB>
    $disklabel="<the label on the disk>"
    $lun=<Logical Unit Number (LUN) of the disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="95e4b-159">Active Directory 도메인 컨트롤러에 대해 $hcaching을 "None"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-159">For an Active Directory domain controller, set $hcaching to "None".</span></span>

<span data-ttu-id="95e4b-160">선택적으로 외부 트래픽에 대한 기존 부하 분산된 집합에 가상 컴퓨터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-160">Optionally, add the virtual machine to an existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of the internal port>
    $pubport=<port number of the external port>
    $endpointname="<name of the endpoint>"
    $lbsetname="<name of the existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="95e4b-161">마지막으로, 가상 컴퓨터를 만들기 위해 이러한 필수 명령 블록 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-161">Finally, choose one of these required command blocks for creating the virtual machine.</span></span>

<span data-ttu-id="95e4b-162">옵션 1: 기존 클라우드 서비스에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-162">Option 1: Create the virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of the cloud service>" -VMs $vm1

<span data-ttu-id="95e4b-163">클라우드 서비스의 짧은 이름은 Azure Portal의 Cloud Services 목록에 표시된 이름 또는 Azure Portal의 리소스 그룹 목록에 표시된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-163">The short name of the cloud service is the name that appears in the list of Cloud Services in the Azure portal or in the list of Resource Groups in the Azure portal.</span></span>

<span data-ttu-id="95e4b-164">옵션 2: 기존 클라우드 서비스 및 가상 네트워크에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-164">Option 2: Create the virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of the cloud service>"
    $vnetname="<name of the virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="95e4b-165">5단계: 명령 집합 실행</span><span class="sxs-lookup"><span data-stu-id="95e4b-165">Step 5: Run your command set</span></span>
<span data-ttu-id="95e4b-166">텍스트 편집기 또는 PowerShell ISE에서 작성한 Azure PowerShell 명령 집합(4단계의 여러 명령 블록으로 구성)을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-166">Review the Azure PowerShell command set you built in your text editor or the PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="95e4b-167">필요한 모든 변수를 지정하고 해당 변수에 올바른 값이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-167">Ensure that you have specified all the needed variables and that they have the correct values.</span></span> <span data-ttu-id="95e4b-168">또한 < 및 > 문자를 모두 제거했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-168">Also make sure that you have removed all the < and > characters.</span></span>

<span data-ttu-id="95e4b-169">텍스트 편집기를 사용하는 경우 명령 집합을 클립보드로 복사한 다음, 열려 있는 Windows PowerShell 명령 프롬프트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-169">If you are using a text editor, copy the command set to the clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="95e4b-170">그러면 명령 집합이 일련의 PowerShell 명령으로 실행되고 Azure 가상 컴퓨터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-170">This will issue the command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="95e4b-171">또는 PowerShell ISE에서 명령 집합을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-171">Alternately, run the command set in the PowerShell ISE.</span></span>

<span data-ttu-id="95e4b-172">이 가상 컴퓨터 또는 이와 유사한 가상 컴퓨터를 다시 만들려는 경우 다음과 같이 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="95e4b-173">이 명령 집합을 PowerShell 스크립트 파일(*.ps1)로 저장</span><span class="sxs-lookup"><span data-stu-id="95e4b-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="95e4b-174">Azure Portal의 **자동화 계정** 섹션에서 이 명령 집합을 Azure Automation Runbook으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-174">Save this command set as an Azure Automation runbook in the **Automation Accounts** section of the Azure portal.</span></span>

## <span data-ttu-id="95e4b-175"><a id="examples"></a>예제</span><span class="sxs-lookup"><span data-stu-id="95e4b-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="95e4b-176">다음은 위 단계를 사용하여 Azure에서 Windows 기반 Azure 가상 컴퓨터를 만드는 Azure PowerShell 명령 집합을 작성하는 두 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-176">Here are two examples of using the steps above to build Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="95e4b-177">예 1</span><span class="sxs-lookup"><span data-stu-id="95e4b-177">Example 1</span></span>
<span data-ttu-id="95e4b-178">다음과 같은 Active Directory 도메인 컨트롤러용 초기 가상 컴퓨터를 만드는 데 사용할 수 있는 PowerShell 명령 집합이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-178">I need a PowerShell command set to create the initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="95e4b-179">Windows Server 2012 R2 Datacenter 이미지를 사용함</span><span class="sxs-lookup"><span data-stu-id="95e4b-179">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="95e4b-180">이름이 AZDC1임</span><span class="sxs-lookup"><span data-stu-id="95e4b-180">Has the name AZDC1.</span></span>
* <span data-ttu-id="95e4b-181">독립 실행형 컴퓨터임</span><span class="sxs-lookup"><span data-stu-id="95e4b-181">Is a standalone computer.</span></span>
* <span data-ttu-id="95e4b-182">20GB의 추가 데이터 디스크가 있음</span><span class="sxs-lookup"><span data-stu-id="95e4b-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="95e4b-183">고정 IP 주소가 192.168.244.4임</span><span class="sxs-lookup"><span data-stu-id="95e4b-183">Has the static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="95e4b-184">AZDatacenter 가상 네트워크의 BackEnd 서브넷에 있음</span><span class="sxs-lookup"><span data-stu-id="95e4b-184">Is in the BackEnd subnet of the AZDatacenter virtual network.</span></span>
* <span data-ttu-id="95e4b-185">Azure-TailspinToys 클라우드 서비스에 있음</span><span class="sxs-lookup"><span data-stu-id="95e4b-185">Is in the Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="95e4b-186">다음은 이 가상 컴퓨터를 만드는 해당 Azure PowerShell 명령 집합입니다. 각 블록 사이의 빈 줄은 가독성을 위해 추가된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-186">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a><span data-ttu-id="95e4b-187">예 2</span><span class="sxs-lookup"><span data-stu-id="95e4b-187">Example 2</span></span>
<span data-ttu-id="95e4b-188">다음과 같은 LOB(기간 업무) 서버용 가상 컴퓨터를 만드는 데 사용할 수 있는 PowerShell 명령 집합이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-188">I need a PowerShell command set to create a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="95e4b-189">Windows Server 2012 R2 Datacenter 이미지를 사용함</span><span class="sxs-lookup"><span data-stu-id="95e4b-189">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="95e4b-190">이름이 LOB1임</span><span class="sxs-lookup"><span data-stu-id="95e4b-190">Has the name LOB1.</span></span>
* <span data-ttu-id="95e4b-191">corp.contoso.com 도메인의 멤버임</span><span class="sxs-lookup"><span data-stu-id="95e4b-191">Is a member of the corp.contoso.com domain.</span></span>
* <span data-ttu-id="95e4b-192">200GB의 추가 데이터 디스크가 있음</span><span class="sxs-lookup"><span data-stu-id="95e4b-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="95e4b-193">AZDatacenter 가상 네트워크의 FrontEnd 서브넷에 있음</span><span class="sxs-lookup"><span data-stu-id="95e4b-193">Is in the FrontEnd subnet of the AZDatacenter virtual network.</span></span>
* <span data-ttu-id="95e4b-194">Azure-TailspinToys 클라우드 서비스에 있음</span><span class="sxs-lookup"><span data-stu-id="95e4b-194">Is in the Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="95e4b-195">다음은 이 가상 컴퓨터를 만드는 해당 Azure PowerShell 명령 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-195">Here is the corresponding Azure PowerShell command set to create this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type the name and password of the local administrator account."
    $cred2=Get-Credential –Message "Now type the name (not including the domain) and password of an account that has permission to add the machine to the domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a><span data-ttu-id="95e4b-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95e4b-196">Next steps</span></span>
<span data-ttu-id="95e4b-197">127GB보다 큰 OS 디스크가 필요한 경우 [OS 드라이브를 확장](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e4b-197">If you need an OS disk that is larger than 127 GB, you can [expand the OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

