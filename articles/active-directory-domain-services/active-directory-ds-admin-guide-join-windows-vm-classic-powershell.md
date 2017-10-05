---
title: "Azure Active Directory Domain Services: 관리 가이드 | Microsoft 문서"
description: "Windows 가상 컴퓨터를 Azure PowerShell 및 클래식 배포 모델을 사용하여 관리되는 도메인에 가입합니다."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1bb1546fb616131a1e1868a0d0610c4cad5d73e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain-using-powershell"></a><span data-ttu-id="85f35-103">PowerShell을 사용하여 Windows Server 가상 컴퓨터를 관리되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="85f35-103">Join a Windows Server virtual machine to a managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="85f35-104">Azure 클래식 포털 - Windows</span><span class="sxs-lookup"><span data-stu-id="85f35-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="85f35-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="85f35-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="85f35-106">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="85f35-107">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="85f35-108">Azure AD 도메인 서비스는 현재 리소스 관리자 모델을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-108">Azure AD Domain Services does not currently support the Resource Manager model.</span></span>
>
>

<span data-ttu-id="85f35-109">다음 단계에서는 구성 요소 접근 방식을 사용하여 Windows 기반 Azure 가상 컴퓨터를 만들고 미리 구성하는 Azure PowerShell 명령 집합을 사용자 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-109">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="85f35-110">다음 단계는 Windows 기반 Azure 가상 컴퓨터를 빌드하고 Azure AD 도메인 서비스 관리되는 도메인에 가입하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-110">These steps help you build a Windows-based Azure virtual machine and join it to an Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="85f35-111">다음 단계에서는 빈 칸 채우기 접근 방식에 따라 Azure PowerShell 명령 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="85f35-112">이 접근 방식은 PowerShell을 처음 접하거나 성공적인 구성을 위해 지정할 값을 알기를 원하는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-112">This approach can be useful if you are new to PowerShell or you want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="85f35-113">고급 PowerShell 사용자는 명령을 가져와 고유한 변수 값("$"로 시작하는 줄)을 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-113">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="85f35-114">[Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview) 의 지침을 사용하여 로컬 컴퓨터에 Azure PowerShell을 설치합니다(아직 설치하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="85f35-114">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="85f35-115">그런 다음 Windows PowerShell 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="85f35-116">1단계: 사용자 계정 추가</span><span class="sxs-lookup"><span data-stu-id="85f35-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="85f35-117">PowerShell 프롬프트에서 **Add-AzureAccount**를 입력하고 **Enter**.</span><span class="sxs-lookup"><span data-stu-id="85f35-117">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="85f35-118">Azure 구독과 연관된 메일 주소를 입력하고 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-118">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="85f35-119">계정에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-119">Type in the password for your account.</span></span>
4. <span data-ttu-id="85f35-120">**로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="85f35-121">2단계: 구독 및 저장소 계정 설정</span><span class="sxs-lookup"><span data-stu-id="85f35-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="85f35-122">Windows PowerShell 명령 프롬프트에서 다음 명령을 실행하여 Azure 구독 및 저장소 계정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-122">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="85f35-123">< 및 > 문자를 포함하여 따옴표 안의 모든 항목을 올바른 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-123">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="85f35-124">**Get-AzureSubscription** 명령의 출력에 표시된 SubscriptionName 속성에서 올바른 구독 이름을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-124">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="85f35-125">**Select-AzureSubscription** 명령을 실행한 후 **Get-AzureStorageAccount** 명령의 출력에 표시된 Label 속성에서 올바른 저장소 계정 이름을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-125">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-the-virtual-machine-and-join-it-to-the-managed-domain"></a><span data-ttu-id="85f35-126">3단계: 단계별 연습 - 가상 컴퓨터 프로비전 및 관리되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="85f35-126">Step 3: Step-by-step walkthrough - provision the virtual machine and join it to the managed domain</span></span>
<span data-ttu-id="85f35-127">다음은 이 가상 컴퓨터를 만드는 해당 Azure PowerShell 명령 집합입니다. 각 블록 사이의 빈 줄은 가독성을 위해 추가된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-127">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="85f35-128">프로비전할 Windows 가상 컴퓨터에 대한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-128">Specify information about the Windows virtual machine to be provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="85f35-129">D-, DS- 또는 G-시리즈 가상 컴퓨터에 대한 InstanceSize 값은 [Azure용 가상 컴퓨터 및 클라우드 서비스 크기](https://msdn.microsoft.com/library/azure/dn197896.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85f35-129">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="85f35-130">관리되는 도메인에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-130">Provide information about the managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="85f35-131">클라우드 서비스의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-131">Specify the name of the cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="85f35-132">VM이 가입되는 가상 네트워크의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-132">Specify the name of the virtual network to which the VM should be joined.</span></span> <span data-ttu-id="85f35-133">AAD-DS 관리되는 도메인을 이 가상 네트워크에서 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-133">Ensure that the AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="85f35-134">VM을 프로비전하는 데 사용할 VM 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-134">Select the VM image to be used to provision the VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="85f35-135">VM을 구성합니다. VM 이름, 인스턴스 크기 및 사용할 이미지를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-135">Configure the VM - set VM name, instance size & image to be used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="85f35-136">VM에 대한 로컬 관리자 자격 증명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-136">Obtain local administrator credentials for the VM.</span></span> <span data-ttu-id="85f35-137">강력한 로컬 관리자 암호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

<span data-ttu-id="85f35-138">VM이 관리되는 도메인에 가입하려면 'AAD DC 관리자' 그룹에 속하는 사용자 계정의 자격 증명을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-138">Obtain credentials for a user account belonging to 'AAD DC Administrators' group to join VM to the managed domain.</span></span> <span data-ttu-id="85f35-139">도메인 이름을 지정하지 않습니다. 예를 들어 예제에서는 'bob'을 사용자 이름으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-139">Do not specify the domain name - for instance, in our example, we specify 'bob' as the user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type the name (DO NOT INCLUDE THE DOMAIN) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

<span data-ttu-id="85f35-140">VM을 구성합니다. 도메인 가입 요구 사항 및 필요한 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-140">Configure the VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="85f35-141">VM에 대한 서브넷을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-141">Set a subnet for the VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="85f35-142">선택 사항: 도메인의 IP 주소를 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-142">Optional: Point to the IP address of the domain.</span></span> <span data-ttu-id="85f35-143">가상 네트워크에 대한 DNS 서버가 되도록 Azure AD 도메인 서비스 관리되는 도메인의 IP 주소를 설정하는 경우 이 단계가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-143">If you set the IP addresses of the Azure AD Domain Services managed domain to be the DNS servers for the virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="85f35-144">이제 도메인에 가입된 Windows VM을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-144">Now, provision the domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-to-provision-a-windows-vm-and-automatically-join-it-to-an-aad-domain-services-managed-domain"></a><span data-ttu-id="85f35-145">Windows VM을 프로비전하고 AAD 도메인 서비스 관리되는 도메인에 자동으로 가입하는 스크립트</span><span class="sxs-lookup"><span data-stu-id="85f35-145">Script to provision a Windows VM and automatically join it to an AAD Domain Services managed domain</span></span>
<span data-ttu-id="85f35-146">이 PowerShell 명령 집합은 다음과 같은 LOB(기간 업무) 서버용 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="85f35-147">Windows Server 2012 R2 Datacenter 이미지를 사용함</span><span class="sxs-lookup"><span data-stu-id="85f35-147">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="85f35-148">매우 작은 가상 컴퓨터임</span><span class="sxs-lookup"><span data-stu-id="85f35-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="85f35-149">이름이 Contoso100-test임</span><span class="sxs-lookup"><span data-stu-id="85f35-149">Has the name Contoso100-test.</span></span>
* <span data-ttu-id="85f35-150">contoso100 관리되는 도메인에 자동으로 가입된 도메인임</span><span class="sxs-lookup"><span data-stu-id="85f35-150">Is automatically domain joined to the contoso100 managed domain.</span></span>
* <span data-ttu-id="85f35-151">관리되는 도메인과 동일한 가상 네트워크에 추가됨</span><span class="sxs-lookup"><span data-stu-id="85f35-151">Is added to the same virtual network as the managed domain.</span></span>

<span data-ttu-id="85f35-152">Windows 가상 컴퓨터를 만들고 자동으로 Azure AD 도메인 서비스 관리되는 도메인에 가입하는 전체 샘플 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85f35-152">Here is the full sample script to create the Windows virtual machine and automatically join it to the Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

    $domainadmincred=Get-Credential –Message "Now type the name (not including the domain) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="85f35-153">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="85f35-153">Related Content</span></span>
* [<span data-ttu-id="85f35-154">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="85f35-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="85f35-155">Azure AD 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="85f35-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
