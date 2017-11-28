---
title: "Azure PowerShell에서 SQL Server 가상 컴퓨터 만들기(클래식) | Microsoft Docs"
description: "SQL Server 가상 컴퓨터 갤러리 이미지를 사용하여 Azure VM을 만드는 단계 및 PowerShell 스크립트를 제공합니다. 이 항목에서는 클래식 배포 모드를 사용합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: c3bd4329e8a22ce8503d6593560d29c2a3135e83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="4e17a-104">Azure PowerShell을 사용하여 SQL Server 가상 컴퓨터 프로비전(클래식)</span><span class="sxs-lookup"><span data-stu-id="4e17a-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="4e17a-105">이 문서에서는 PowerShell cmdlet을 사용하여 Azure에서 SQL Server 가상 컴퓨터를 만드는 방법에 대한 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-105">This article provides steps for how to create a SQL Server virtual machine in Azure by using the PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4e17a-106">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4e17a-107">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4e17a-108">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="4e17a-109">이 항목의 Resource Manager 버전에 대해서는 [Azure PowerShell Resource Manager를 사용하여 SQL Server 가상 컴퓨터 프로비전](../sql/virtual-machines-windows-ps-sql-create.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e17a-109">For the Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="4e17a-110">PowerShell 설치 및 구성:</span><span class="sxs-lookup"><span data-stu-id="4e17a-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="4e17a-111">Azure 계정이 없는 경우 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="4e17a-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="4e17a-112">[최신 Azure PowerShell 명령을 다운로드하여 설치합니다](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4e17a-112">[Download and install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="4e17a-113">Windows PowerShell을 시작하고 **Add-AzureAccount** 명령을 사용하여 Azure 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-113">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="4e17a-114">대상 Azure 지역 확인</span><span class="sxs-lookup"><span data-stu-id="4e17a-114">Determine your target Azure region</span></span>

<span data-ttu-id="4e17a-115">SQL Server 가상 컴퓨터를 특정 Azure 지역에 있는 클라우드 서비스에서 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="4e17a-116">다음 단계에서 지역, 저장소 계정 및 클라우드 서비스를 확인할 수 있으며, 이는 자습서의 나머지 부분에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-116">The following steps help you to determine your region, storage account, and cloud service that will be used for the rest of the tutorial.</span></span>

1. <span data-ttu-id="4e17a-117">SQL Server VM을 호스트하기 위해 사용하려는 데이터 센터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-117">Determine the data center that you want to use to host your SQL Server VM.</span></span> <span data-ttu-id="4e17a-118">다음 PowerShell 명령은 사용 가능한 지역 이름 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-118">The following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="4e17a-119">원하는 위치를 식별했으면 **$dcLocation** 이라는 변수를 해당 지역으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-119">Once you've identified your preferred location, set a variable named **$dcLocation** to that region.</span></span> <span data-ttu-id="4e17a-120">예를 들어 다음 명령은 지역을 "미국 동부"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-120">For example, the following command sets the region to "East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="4e17a-121">구독 및 저장소 계정 설정</span><span class="sxs-lookup"><span data-stu-id="4e17a-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="4e17a-122">새 가상 컴퓨터에 대해 사용할 Azure 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-122">Determine the Azure subscription you will use for the new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="4e17a-123">대상 Azure 구독을 **$subscr** 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-123">Assign your target Azure subscription to the **$subscr** variable.</span></span> <span data-ttu-id="4e17a-124">그런 다음 이를 현재 Azure 구독으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="4e17a-125">기존 저장소 계정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="4e17a-126">다음 스크립트는 선택한 지역에 있는 모든 저장소 계정을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-126">The following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="4e17a-127">새 저장소 계정이 필요한 경우 먼저 New-AzureStorageAccount 명령을 사용하여 저장소 계정 이름(모두 소문자)을 만듭니다. `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="4e17a-127">If you require a new storage account, first create an all-lower-case storage account name with the New-AzureStorageAccount command as in the following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="4e17a-128">대상 저장소 계정 이름을 **$staccount**에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-128">Assign the target storage account name to the **$staccount**.</span></span> <span data-ttu-id="4e17a-129">**Set-AzureSubscription** 을 사용하여 구독 및 현재 저장소 계정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-129">Then use **Set-AzureSubscription** to set the subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="4e17a-130">SQL Server 가상 컴퓨터 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="4e17a-131">갤러리에서 사용 가능한 SQL Server 가상 컴퓨터 이미지의 목록을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-131">Find out the list of available SQL Server virtual machines images from the gallery.</span></span> <span data-ttu-id="4e17a-132">이러한 모든 이미지에는 "SQL"로 시작하는 **ImageFamily** 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="4e17a-133">다음 쿼리는 SQL Server를 미리 설치했을 때 사용 가능한 이미지 패밀리를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-133">The following query displays the image family available to you that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="4e17a-134">가상 컴퓨터 이미지 패밀리를 찾으면 해당 패밀리에 여러 개의 게시된 이미지가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-134">When you find the  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="4e17a-135">다음 스크립트를 사용하여 선택한 이미지 패밀리에 대해 게시된 최신 가상 컴퓨터 이미지 이름을 찾습니다(예: **Windows Server 2012 R2의 SQL Server 2016 RTM Enterprise**).</span><span class="sxs-lookup"><span data-stu-id="4e17a-135">Use the following script to find the latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-the-virtual-machine"></a><span data-ttu-id="4e17a-136">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="4e17a-136">Create the virtual machine</span></span>

<span data-ttu-id="4e17a-137">마지막으로, PowerShell을 사용하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-137">Finally, create the virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="4e17a-138">새 VM을 호스트할 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-138">Create a cloud service to host the new VM.</span></span> <span data-ttu-id="4e17a-139">기존 클라우드 서비스를 대신 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-139">Note that it is also possible to use an existing cloud service instead.</span></span> <span data-ttu-id="4e17a-140">클라우드 서비스의 짧은 이름을 사용하여 새 변수 **$svcname** 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-140">Create a new variable **$svcname** with the short name of the cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="4e17a-141">가상 컴퓨터 이름 및 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-141">Specify the virtual machine name and a size.</span></span> <span data-ttu-id="4e17a-142">가상 컴퓨터 크기에 대한 자세한 내용은 [Azure에 대한 Virtual Machine 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e17a-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see the link to the other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="4e17a-143">로컬 관리자 계정 및 암호 지정</span><span class="sxs-lookup"><span data-stu-id="4e17a-143">Specify the local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type the name and password of the local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="4e17a-144">다음 스크립트를 실행하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-144">Run the following script to create the virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="4e17a-145">추가 설명과 구성 옵션은 **Azure PowerShell을 사용하여 Windows 기반 Virtual Machines 만들기 및 미리 구성** 의 [명령 집합 빌드](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e17a-145">For additional explanation and configuration options, see the **Build your command set** section in [Use Azure PowerShell to create and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="4e17a-146">PowerShell 스크립트 예</span><span class="sxs-lookup"><span data-stu-id="4e17a-146">Example PowerShell script</span></span>

<span data-ttu-id="4e17a-147">다음 스크립트에서는 **Windows Server 2012 R2의 SQL Server 2016 RTM Enterprise** 가상 컴퓨터를 만드는 전체 스크립트의 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-147">The following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="4e17a-148">이 스크립트를 사용하는 경우 이 항목의 이전 단계를 기반으로 하여 초기 변수를 사용자 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-148">If you use this script, you must customize the initial variables based on the previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set the current subscription and storage account
# Comment out the New-AzureStorageAccount line if the account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select the most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create the new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create the VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type the name and password of the local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create the SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="4e17a-149">원격 데스크톱을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="4e17a-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="4e17a-150">현재 사용자의 문서 폴더에 .RDP 파일을 만들고 이러한 가상 컴퓨터를 시작하여 설정을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-150">Create the RDP files in the current user's document folder to launch these virtual machines to complete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="4e17a-151">문서 디렉터리에서 RDP 파일을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-151">In the documents directory, launch the RDP file.</span></span> <span data-ttu-id="4e17a-152">앞에서 입력한 관리자의 사용자 이름 및 암호에 연결합니다(예: 사용자 이름이 VMAdmin이면 사용자로 "\VMAdmin"을 지정하고 암호 입력).</span><span class="sxs-lookup"><span data-stu-id="4e17a-152">Connect with the administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as the user and provide the password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-the-configuration-of-the-sql-server-machine-for-remote-access"></a><span data-ttu-id="4e17a-153">원격 액세스를 위한 SQL Server 컴퓨터 구성 완료</span><span class="sxs-lookup"><span data-stu-id="4e17a-153">Complete the configuration of the SQL Server Machine for remote access</span></span>

<span data-ttu-id="4e17a-154">원격 데스크톱을 사용하여 컴퓨터에 로그온한 후 [Azure VM에서 SQL Server 연결을 구성하기 위한 단계](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)의 지침에 따라 SQL Server를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-154">After logging on to the machine with remote desktop, configure SQL Server based on the instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e17a-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e17a-155">Next steps</span></span>

<span data-ttu-id="4e17a-156">[가상 컴퓨터 설명서](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)에서 PowerShell을 사용하여 가상 컴퓨터를 프로비전하는 추가 지침을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-156">You can find additional instructions for provisioning virtual machines with PowerShell in the [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="4e17a-157">대부분의 경우 다음 단계는 이 새로운 SQL Server VM에 데이터베이스를 마이그레이션하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-157">In many cases, the next step is to migrate your databases to this new SQL Server VM.</span></span> <span data-ttu-id="4e17a-158">데이터베이스 마이그레이션 지침은 [Azure VM에서 SQL Server로 데이터베이스 마이그레이션](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e17a-158">For database migration guidance, see [Migrating a Database to SQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="4e17a-159">또한 Azure Portal을 사용하여 SQL Virtual Virtual Machines를 만드는 방법을 알아보려면 [Azure에서 SQL Server Virtual Machine 프로비전](../sql/virtual-machines-windows-portal-sql-server-provision.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e17a-159">If you're also interested in using the Azure portal to create SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="4e17a-160">자습서는 포털을 통해 이 PowerShell 항목에서 사용되는 클래식 모델이 아닌 권장되는 리소스 관리자 모델을 사용하여 VM을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-160">Note that the tutorial that walks you through the portal creates VMs using the recommended Resource Manager model, rather than the classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="4e17a-161">이러한 리소스 외에도 [Azure Virtual Machines에서 SQL Server 실행과 관련된 기타 항목](../sql/virtual-machines-windows-sql-server-iaas-overview.md)을 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4e17a-161">In addition to these resources, we recommend that you review [other topics related to running SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
