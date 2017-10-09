---
title: "PowerShell 사용 하 여 Windows VM aaaCreate | Microsoft Docs"
description: "Azure PowerShell을 hello 클래식 배포 모델을 사용 하 여 Windows 가상 컴퓨터를 만듭니다."
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
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a><span data-ttu-id="3ffc2-103">PowerShell 및 hello 클래식 배포 모델에서 Windows 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="3ffc2-103">Create a Windows virtual machine with PowerShell and hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ffc2-104">Azure Portal - Windows</span><span class="sxs-lookup"><span data-stu-id="3ffc2-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="3ffc2-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="3ffc2-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="3ffc2-106">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3ffc2-107">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3ffc2-108">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="3ffc2-109">너무 방법에 대해 알아봅니다[hello 리소스 관리자 모델을 사용 하 여 이러한 단계를 수행](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-109">Learn how too[perform these steps using hello Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="3ffc2-110">이러한 단계에 만들고 빌딩 블록 방법을 사용 하 여 Windows 기반 Azure 가상 컴퓨터를 미리 구성 하는 toocustomize 집합의 Azure PowerShell 명령 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-110">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="3ffc2-111">이 프로세스를 사용 하는 사용자 지정 개발/테스트 또는 IT 전문가 환경 구축 toocreate 여러 명령은 신속 하 게 하는 설정 또는 tooquickly 새 Windows 기반 가상 컴퓨터에 대 한 명령 집합을 만들고 기존 배포를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-111">You can use this process tooquickly create a command set for a new Windows-based virtual machine and expand an existing deployment or toocreate multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="3ffc2-112">다음 단계에서는 빈 칸 채우기 접근 방식에 따라 Azure PowerShell 명령 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="3ffc2-113">이 방법은 새 tooPowerShell 또는 방금 tooknow 어떤 값 toospecify에 대해 원하는 구성이 성공적으로 완료 하는 경우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-113">This approach can be useful if you are new tooPowerShell or you just want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="3ffc2-114">고급 PowerShell 사용자 수 hello 명령을 수행 하 고 hello 변수 ("$"로 시작 하 고 hello 선)에 대 한 고유한 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-114">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="3ffc2-115">아직 수행 하지 않은 경우의 지침에 hello를 사용 하 여 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 로컬 컴퓨터에 Azure PowerShell tooinstall 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-115">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="3ffc2-116">그런 다음 Windows PowerShell 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="3ffc2-117">1단계: 사용자 계정 추가</span><span class="sxs-lookup"><span data-stu-id="3ffc2-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="3ffc2-118">Hello PowerShell 프롬프트에서 입력 **Add-azureaccount** 클릭 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-118">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="3ffc2-119">Azure 구독에 연결 된 hello 전자 메일 주소에 입력 하 고 클릭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="3ffc2-120">Hello 계정의 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="3ffc2-121">**로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="3ffc2-122">2단계: 구독 및 저장소 계정 설정</span><span class="sxs-lookup"><span data-stu-id="3ffc2-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="3ffc2-123">Hello Windows PowerShell 명령 프롬프트에서 다음이 명령을 실행 하 여 Azure 구독 및 저장소 계정을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-123">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="3ffc2-124">Hello < 및 > 문자를 포함 하는 hello 따옴표 안의 hello 올바른 이름으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-124">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="3ffc2-125">Hello 올바른 구독 이름을 hello hello의 hello 출력의 SubscriptionName 속성에서에서 가져올 수 있습니다 **Get-azuresubscription** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-125">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="3ffc2-126">Hello hello의 hello 출력의 Label 속성에서에서 hello 올바른 저장소 계정 이름을 가져올 수 있습니다 **Get AzureStorageAccount** hello를 실행 한 후 명령을 **Select-azuresubscription** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-126">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-hello-imagefamily"></a><span data-ttu-id="3ffc2-127">3 단계: hello ImageFamily 확인</span><span class="sxs-lookup"><span data-stu-id="3ffc2-127">Step 3: Determine hello ImageFamily</span></span>
<span data-ttu-id="3ffc2-128">다음으로, 해야 toodetermine hello ImageFamily 또는 레이블 값 hello 특정 이미지 해당 toohello toocreate를 원하는 Azure 가상 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-128">Next, you need toodetermine hello ImageFamily or Label value for hello specific image corresponding toohello Azure virtual machine you want toocreate.</span></span> <span data-ttu-id="3ffc2-129">이 명령 사용 하 여 사용 가능한 ImageFamily 값 hello 목록을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-129">You can get hello list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="3ffc2-130">다음은 Windows 기반 컴퓨터의 ImageFamily 값에 대한 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="3ffc2-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="3ffc2-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="3ffc2-132">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="3ffc2-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="3ffc2-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="3ffc2-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="3ffc2-134">Windows Server 2012의 SQL Server 2012 SP1 Enterprise</span><span class="sxs-lookup"><span data-stu-id="3ffc2-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="3ffc2-135">원하는 hello 이미지를 찾을 경우 choice 또는 hello PowerShell 스크립팅 환경을 ISE (통합)의 hello 텍스트 편집기의 새 인스턴스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-135">If you find hello image you are looking for, open a fresh instance of hello text editor of your choice or hello PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="3ffc2-136">Hello 새 텍스트 파일 또는 hello hello ImageFamily 값으로 대체 되는 PowerShell ISE에 hello 다음을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-136">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="3ffc2-137">경우에 따라 hello 이미지 이름이 hello hello ImageFamily 값 대신 Label 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-137">In some cases, hello image name is in hello Label property instead of hello ImageFamily value.</span></span> <span data-ttu-id="3ffc2-138">Hello ImageFamily 속성을 사용 하 여 원하는 hello 이미지를 찾지 못한 경우이 명령 사용 하 여 해당 레이블 속성에 의해 hello 이미지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-138">If you didn't find hello image that you are looking for using hello ImageFamily property, list hello images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="3ffc2-139">이 명령 사용 하 여 hello 오른쪽 이미지를 찾을 경우 choice 또는 hello PowerShell ISE의 hello 텍스트 편집기의 새 인스턴스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-139">If you find hello right image with this command, open a fresh instance of hello text editor of your choice or hello PowerShell ISE.</span></span> <span data-ttu-id="3ffc2-140">Hello 새 텍스트 파일 또는 hello hello 레이블 값으로 대체 되는 PowerShell ISE에 hello 다음을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-140">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="3ffc2-141">4단계: 명령 집합 작성</span><span class="sxs-lookup"><span data-stu-id="3ffc2-141">Step 4: Build your command set</span></span>
<span data-ttu-id="3ffc2-142">새 텍스트 파일 또는 ISE hello 및 다음 hello 변수 값 채우기 및 hello < 및 > 문자를 제거 합니다. 아래 블록의 hello 적절 한 집합을 복사 하 여 설정 명령 hello 나머지를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-142">Build hello rest of your command set by copying hello appropriate set of blocks below into your new text file or hello ISE and then filling in hello variable values and removing hello < and > characters.</span></span> <span data-ttu-id="3ffc2-143">Hello 두 참조 [예제](#examples) hello 최종 결과의 개념에 대 한이 문서의 hello 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-143">See hello two [examples](#examples) at hello end of this article for an idea of hello final result.</span></span>

<span data-ttu-id="3ffc2-144">다음 두 명령 블록 중 하나를 선택하여 명령 집합을 시작합니다(필수).</span><span class="sxs-lookup"><span data-stu-id="3ffc2-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="3ffc2-145">옵션 1: 가상 컴퓨터 이름 및 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="3ffc2-146">옵션 2: 이름, 크기 및 가용성 집합 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="3ffc2-147">D, DS 또는 G 시리즈 가상 컴퓨터에 대 한 hello InstanceSize 값, 참조 [가상 컴퓨터와 Azure 클라우드 서비스 크기](https://msdn.microsoft.com/library/azure/dn197896.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-147">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="3ffc2-148">Software Assurance와 함께 기업 계약 하 고 Windows 서버 hello tootake 활용 하려는 경우 [하이브리드 사용 혜택](https://azure.microsoft.com/pricing/hybrid-use-benefit/), 추가 된 **-LicenseType** 매개 변수 toohello  **New-azurevmconfig** hello 값을 전달 cmdlet **Windows_Server** 일반적인 hello에 대 한 사용 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-148">If you have an Enterprise Agreement with Software Assurance, and intend tootake advantage of hello Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter toohello **New-AzureVMConfig** cmdlet, passing hello value **Windows_Server** for hello typical use case.</span></span>  <span data-ttu-id="3ffc2-149">업로드 한; 이미지를 사용 하는 확인 hello 혜택을 사용 하는 하이브리드로 hello 갤러리에서에서 독립 실행형 이미지를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-149">Be sure you are using an image you have uploaded; you cannot use a standard image from hello Gallery with hello Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="3ffc2-150">필요에 따라 독립 실행형 Windows 컴퓨터에 대 한 hello 로컬 관리자 계정 및 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-150">Optionally, for a standalone Windows computer, specify hello local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="3ffc2-151">강력한 암호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-151">Choose a strong password.</span></span> <span data-ttu-id="3ffc2-152">toocheck의 강도 참조 [암호 검사기: 강력한 암호를 사용 하 여](https://www.microsoft.com/security/pc-security/password-checker.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-152">toocheck its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="3ffc2-153">필요에 따라 Windows 컴퓨터 tooan 기존 Active Directory 도메인을 tooadd hello hello 로컬 관리자 계정 및 암호, hello 도메인 및 hello 이름 및 도메인 계정의 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-153">Optionally, tooadd hello Windows computer tooan existing Active Directory domain, specify hello local administrator account and password, hello domain, and hello name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="3ffc2-154">Windows 기반 가상 컴퓨터에 대 한 추가 사전 구성 옵션에 대 한 hello에 대 한 hello 구문을 참조 **Windows** 및 **WindowsDomain** 매개 변수 집합에 [ 추가 AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-154">For additional pre-configuration options for Windows-based virtual machines, see hello syntax for hello **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="3ffc2-155">필요에 따라 hello 가상 컴퓨터를 고정 DIP를 라고 특정 IP 주소를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-155">Optionally, assign hello virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="3ffc2-156">특정 IP 주소를 사용할 수 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="3ffc2-157">필요에 따라 Azure 가상 네트워크의 hello 가상 컴퓨터 tooa 특정 서브넷을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-157">Optionally, assign hello virtual machine tooa specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

<span data-ttu-id="3ffc2-158">필요에 따라 단일 데이터 디스크 toohello 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-158">Optionally, add a single data disk toohello virtual machine.</span></span>

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="3ffc2-159">Active Directory 도메인 컨트롤러 설정 $hcaching 너무 "None"입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-159">For an Active Directory domain controller, set $hcaching too"None".</span></span>

<span data-ttu-id="3ffc2-160">Hello 가상 컴퓨터 tooan 기존 부하 분산 된 집합 외부 트래픽에 대해 필요에 따라 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-160">Optionally, add hello virtual machine tooan existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="3ffc2-161">마지막으로, 이러한 필수 명령 블록 hello 가상 컴퓨터를 만드는 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-161">Finally, choose one of these required command blocks for creating hello virtual machine.</span></span>

<span data-ttu-id="3ffc2-162">옵션 1: 기존 클라우드 서비스에 hello 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-162">Option 1: Create hello virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

<span data-ttu-id="3ffc2-163">hello hello 클라우드 서비스의 짧은 이름에는 클라우드 서비스의 hello Azure 포털 또는 hello Azure 포털에서에서 리소스 그룹의 hello 목록 hello 목록에 표시 된 hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-163">hello short name of hello cloud service is hello name that appears in hello list of Cloud Services in hello Azure portal or in hello list of Resource Groups in hello Azure portal.</span></span>

<span data-ttu-id="3ffc2-164">옵션 2: 기존 클라우드 서비스 및 가상 네트워크에 hello 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-164">Option 2: Create hello virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="3ffc2-165">5단계: 명령 집합 실행</span><span class="sxs-lookup"><span data-stu-id="3ffc2-165">Step 5: Run your command set</span></span>
<span data-ttu-id="3ffc2-166">텍스트 편집기에서 빌드한 hello Azure PowerShell 명령 집합을 검토 하거나 PowerShell ISE 명령 4 단계에서 여러 개의 블록으로 구성 된 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-166">Review hello Azure PowerShell command set you built in your text editor or hello PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="3ffc2-167">모든 필요한 hello 변수를 지정 하 고 hello 올바른 값을 가진 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-167">Ensure that you have specified all hello needed variables and that they have hello correct values.</span></span> <span data-ttu-id="3ffc2-168">또한 모든 hello < 및 > 문자를 제거 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-168">Also make sure that you have removed all hello < and > characters.</span></span>

<span data-ttu-id="3ffc2-169">텍스트 편집기를 사용 하는 경우 복사 hello 명령은 toohello 클립보드를 설정 하 고 열린 Windows PowerShell 명령 프롬프트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-169">If you are using a text editor, copy hello command set toohello clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="3ffc2-170">이에서는 일련의 PowerShell 명령으로 hello 명령 집합을 발급 하 고 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-170">This will issue hello command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="3ffc2-171">또는 hello PowerShell ISE에서에서 설정 하는 hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-171">Alternately, run hello command set in hello PowerShell ISE.</span></span>

<span data-ttu-id="3ffc2-172">이 가상 컴퓨터 또는 이와 유사한 가상 컴퓨터를 다시 만들려는 경우 다음과 같이 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="3ffc2-173">이 명령 집합을 PowerShell 스크립트 파일(*.ps1)로 저장</span><span class="sxs-lookup"><span data-stu-id="3ffc2-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="3ffc2-174">이 명령은 hello에 Azure 자동화 runbook으로 설정 저장 **자동화 계정을** hello Azure 포털의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-174">Save this command set as an Azure Automation runbook in hello **Automation Accounts** section of hello Azure portal.</span></span>

## <span data-ttu-id="3ffc2-175"><a id="examples"></a>예제</span><span class="sxs-lookup"><span data-stu-id="3ffc2-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="3ffc2-176">다음은 Windows 기반 Azure 가상 컴퓨터를 만드는 toobuild Azure PowerShell 명령 집합 위에 hello 단계를 사용 하는 두 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-176">Here are two examples of using hello steps above toobuild Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="3ffc2-177">예 1</span><span class="sxs-lookup"><span data-stu-id="3ffc2-177">Example 1</span></span>
<span data-ttu-id="3ffc2-178">PowerShell 필요한 명령 집합, Active Directory 도메인 컨트롤러에 대 한 toocreate hello 초기 가상 컴퓨터를:</span><span class="sxs-lookup"><span data-stu-id="3ffc2-178">I need a PowerShell command set toocreate hello initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="3ffc2-179">Windows Server 2012 R2 Datacenter 이미지 hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-179">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="3ffc2-180">이름이 hello AZDC1 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-180">Has hello name AZDC1.</span></span>
* <span data-ttu-id="3ffc2-181">독립 실행형 컴퓨터임</span><span class="sxs-lookup"><span data-stu-id="3ffc2-181">Is a standalone computer.</span></span>
* <span data-ttu-id="3ffc2-182">20GB의 추가 데이터 디스크가 있음</span><span class="sxs-lookup"><span data-stu-id="3ffc2-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="3ffc2-183">Hello 고정 IP 주소 192.168.244.4에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-183">Has hello static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="3ffc2-184">Hello AZDatacenter 가상 네트워크의 hello 백 엔드 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-184">Is in hello BackEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="3ffc2-185">Hello TailspinToys Azure 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-185">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="3ffc2-186">다음 hello 해당 Azure PowerShell 명령 집합 toocreate 가독성을 위해 각 블록 사이 빈 줄이 가상 컴퓨터를은입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-186">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
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

### <a name="example-2"></a><span data-ttu-id="3ffc2-187">예 2</span><span class="sxs-lookup"><span data-stu-id="3ffc2-187">Example 2</span></span>
<span data-ttu-id="3ffc2-188">PowerShell 필요한 명령 집합 toocreate 업무의 서버에 대 한 가상 컴퓨터를:</span><span class="sxs-lookup"><span data-stu-id="3ffc2-188">I need a PowerShell command set toocreate a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="3ffc2-189">Windows Server 2012 R2 Datacenter 이미지 hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-189">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="3ffc2-190">이름이 hello LOB1 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-190">Has hello name LOB1.</span></span>
* <span data-ttu-id="3ffc2-191">Hello corp.contoso.com 도메인의 구성원이입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-191">Is a member of hello corp.contoso.com domain.</span></span>
* <span data-ttu-id="3ffc2-192">200GB의 추가 데이터 디스크가 있음</span><span class="sxs-lookup"><span data-stu-id="3ffc2-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="3ffc2-193">Hello AZDatacenter 가상 네트워크의 hello 프런트 엔드 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-193">Is in hello FrontEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="3ffc2-194">Hello TailspinToys Azure 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-194">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="3ffc2-195">여기서는 hello 해당 Azure PowerShell 명령 집합 toocreate이 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-195">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
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


## <a name="next-steps"></a><span data-ttu-id="3ffc2-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3ffc2-196">Next steps</span></span>
<span data-ttu-id="3ffc2-197">127 GB 보다 큰 OS 디스크 해야 할 경우 다음을 할 수 있습니다 [hello 운영 체제 드라이브 확장](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ffc2-197">If you need an OS disk that is larger than 127 GB, you can [expand hello OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

