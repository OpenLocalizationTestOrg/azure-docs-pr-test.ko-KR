---
title: "C#을 사용하여 Azure Virtual Machine 만들기 및 관리 | Microsoft Docs"
description: "C# 및 Azure Resource Manager를 사용하여 가상 컴퓨터 및 모든 지원 리소스를 배포합니다."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 87524373-5f52-4f4b-94af-50bf7b65c277
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 5d9021c2f65b70e36d5ea82992c9fb9d2d6d394a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="b8074-103">C#을 사용하여 Azure에서 Windows VM 생성 및 관리</span><span class="sxs-lookup"><span data-stu-id="b8074-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="b8074-104">[Azure 가상 컴퓨터](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)(VM)에 몇 가지 지원 Azure 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="b8074-105">이 문서에서는 C#을 사용하여 VM 리소스 만들기, 관리 및 삭제에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="b8074-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b8074-107">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="b8074-108">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="b8074-108">Install the package</span></span>
> * <span data-ttu-id="b8074-109">자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-109">Create credentials</span></span>
> * <span data-ttu-id="b8074-110">리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-110">Create resources</span></span>
> * <span data-ttu-id="b8074-111">관리 작업 수행</span><span class="sxs-lookup"><span data-stu-id="b8074-111">Perform management tasks</span></span>
> * <span data-ttu-id="b8074-112">리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="b8074-112">Delete resources</span></span>
> * <span data-ttu-id="b8074-113">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="b8074-113">Run the application</span></span>

<span data-ttu-id="b8074-114">이러한 단계를 수행하려면 약 20분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="b8074-115">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="b8074-116">[Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio)를 아직 설치하지 않았으면 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="b8074-117">작업 페이지에서 **.NET 데스크톱 개발**을 선택한 다음 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-117">Select **.NET desktop development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="b8074-118">요약에서 **.NET Framework 4 - 4.6 개발 도구**가 자동으로 선택되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-118">In the summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="b8074-119">Visual Studio를 이미 설치한 경우 Visual Studio 시작 관리자를 사용하여 .NET 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-119">If you have already installed Visual Studio, you can add the .NET workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="b8074-120">Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="b8074-121">**템플릿** > **Visual C#**에서 **콘솔 앱(.NET Framework)**을 선택하고, 프로젝트의 이름에 *myDotnetProject*를 입력하고 프로젝트의 위치를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-the-package"></a><span data-ttu-id="b8074-122">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="b8074-122">Install the package</span></span>

<span data-ttu-id="b8074-123">NuGet 패키지는 이러한 단계를 완료하는데 필요한 라이브러리를 설치하는 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-123">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="b8074-124">Visual Studio에서 필요한 라이브러리를 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-124">To get the libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="b8074-125">**도구** > **Nuget 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="b8074-126">콘솔에 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-126">Type this command in the console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="b8074-127">자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-127">Create credentials</span></span>

<span data-ttu-id="b8074-128">이 단계를 시작하기 전에 [Active Directory 서비스 사용자](../../azure-resource-manager/resource-group-create-service-principal-portal.md)에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-128">Before you start this step, make sure that you have access to an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="b8074-129">또한 이후 단계에서 필요한 응용 프로그램 ID, 인증 키 및 테넌트 ID를 기록해 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-129">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="b8074-130">권한 부여 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-130">Create the authorization file</span></span>

1. <span data-ttu-id="b8074-131">솔루션 탐색기에서 *myDotnetProject* > **추가** > **새 항목**을 마우스 오른쪽 단추로 클릭한 다음 *Visual C# 항목*에서 **텍스트 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="b8074-132">파일 이름을 *azureauth.properties*로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-132">Name the file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="b8074-133">다음과 같은 권한 부여 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-133">Add these authorization properties:</span></span>

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    <span data-ttu-id="b8074-134">**&lt;subscription-id&gt;**를 구독 식별자, **&lt;application-id&gt;**를 Active Directory 응용 프로그램 식별자, **&lt;authentication-key&gt;**를 응용 프로그램 키, **&lt;tenant-id&gt;**를 테넌트 식별자로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

3. <span data-ttu-id="b8074-135">azureauth.properties 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-135">Save the azureauth.properties file.</span></span> 
4. <span data-ttu-id="b8074-136">AZURE_AUTH_LOCATION이라는 Windows 환경 변수를 만든 권한 부여 파일의 전체 경로로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with the full path to authorization file that you created.</span></span> <span data-ttu-id="b8074-137">예를 들어 다음과 같은 PowerShell 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-137">For example, the following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-the-management-client"></a><span data-ttu-id="b8074-138">관리 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-138">Create the management client</span></span>

1. <span data-ttu-id="b8074-139">만들었던 프로젝트에 대한 Program.cs 파일을 연 후, 다음 using 문을 파일의 위쪽에 기존 문에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-139">Open the Program.cs file for the project that you created, and then add these using statements to the existing statements at top of the file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="b8074-140">관리 클라이언트를 만들려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-140">To create the management client, add this code to the Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="b8074-141">리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-141">Create resources</span></span>

### <a name="create-the-resource-group"></a><span data-ttu-id="b8074-142">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-142">Create the resource group</span></span>

<span data-ttu-id="b8074-143">모든 리소스는 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md)에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="b8074-144">응용 프로그램의 값을 지정하고 리소스 그룹을 만들려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-144">To specify values for the application and create the resource group, add this code to the Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-the-availability-set"></a><span data-ttu-id="b8074-145">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-145">Create the availability set</span></span>

<span data-ttu-id="b8074-146">[가용성 집합](tutorial-availability-sets.md)은 응용 프로그램에서 사용되는 가상 컴퓨터를 쉽게 유지 관리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-146">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

<span data-ttu-id="b8074-147">가용성 집합을 만들려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-147">To create the availability set, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-the-public-ip-address"></a><span data-ttu-id="b8074-148">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-148">Create the public IP address</span></span>

<span data-ttu-id="b8074-149">[공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)는 가상 컴퓨터와 통신하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

<span data-ttu-id="b8074-150">가상 컴퓨터의 공용 IP 주소를 만들려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-150">To create the public IP address for the virtual machine, add this code to the Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-the-virtual-network"></a><span data-ttu-id="b8074-151">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-151">Create the virtual network</span></span>

<span data-ttu-id="b8074-152">가상 컴퓨터는 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)의 서브넷에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="b8074-153">서브넷 및 가상 네트워크를 만들려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-153">To create a subnet and a virtual network, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-the-network-interface"></a><span data-ttu-id="b8074-154">네트워크 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-154">Create the network interface</span></span>

<span data-ttu-id="b8074-155">가상 컴퓨터는 가상 네트워크에서 통신하기 위해 네트워크 인터페이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-155">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

<span data-ttu-id="b8074-156">네트워크 인터페이스를 만들려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-156">To create a network interface, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating network interface...");
var networkInterface = azure.NetworkInterfaces.Define("myNIC")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetwork(network)
    .WithSubnet("mySubnet")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithExistingPrimaryPublicIPAddress(publicIPAddress)
    .Create();
 ```

### <a name="create-the-virtual-machine"></a><span data-ttu-id="b8074-157">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="b8074-157">Create the virtual machine</span></span>

<span data-ttu-id="b8074-158">모든 지원 리소스를 만들었으므로 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-158">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="b8074-159">가상 컴퓨터를 만들려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-159">To create the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating virtual machine...");
azure.VirtualMachines.Define(vmName)
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("azureuser")
    .WithAdminPassword("Azure12345678")
    .WithComputerName(vmName)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

> [!NOTE]
> <span data-ttu-id="b8074-160">이 자습서는 Windows Server 운영 체제의 버전을 실행하는 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-160">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="b8074-161">기타 이미지 선택에 대해 자세히 알아보려면 [Windows PowerShell 및 Azure CLI를 사용하여 Azure 가상 컴퓨터 탐색 및 선택](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8074-161">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="b8074-162">마켓플레이스 이미지 대신 기존 디스크를 사용하려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-162">If you want to use an existing disk instead of a marketplace image, use this code:</span></span>

```
var managedDisk = azure.Disks.Define("myosdisk")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd")
    .WithSizeInGB(128)
    .WithSku(DiskSkuTypes.PremiumLRS)
    .Create();

azure.VirtualMachines.Define("myVM")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

## <a name="perform-management-tasks"></a><span data-ttu-id="b8074-163">관리 작업 수행</span><span class="sxs-lookup"><span data-stu-id="b8074-163">Perform management tasks</span></span>

<span data-ttu-id="b8074-164">가상 컴퓨터의 수명 주기 동안 가상 컴퓨터 시작, 중지 또는 삭제 등의 관리 작업을 실행하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-164">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="b8074-165">또한 반복적이거나 복잡한 작업을 자동화하는 코드를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-165">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

<span data-ttu-id="b8074-166">VM에서 작업을 수행해야 하는 경우 VM의 인스턴스를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-166">When you need to do anything with the VM, you need to get an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-the-vm"></a><span data-ttu-id="b8074-167">VM 관련 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="b8074-167">Get information about the VM</span></span>

<span data-ttu-id="b8074-168">가상 컴퓨터에 대한 정보를 가져오려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-168">To get information about the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Getting information about the virtual machine...");
Console.WriteLine("hardwareProfile");
Console.WriteLine("   vmSize: " + vm.Size);
Console.WriteLine("storageProfile");
Console.WriteLine("  imageReference");
Console.WriteLine("    publisher: " + vm.StorageProfile.ImageReference.Publisher);
Console.WriteLine("    offer: " + vm.StorageProfile.ImageReference.Offer);
Console.WriteLine("    sku: " + vm.StorageProfile.ImageReference.Sku);
Console.WriteLine("    version: " + vm.StorageProfile.ImageReference.Version);
Console.WriteLine("  osDisk");
Console.WriteLine("    osType: " + vm.StorageProfile.OsDisk.OsType);
Console.WriteLine("    name: " + vm.StorageProfile.OsDisk.Name);
Console.WriteLine("    createOption: " + vm.StorageProfile.OsDisk.CreateOption);
Console.WriteLine("    caching: " + vm.StorageProfile.OsDisk.Caching);
Console.WriteLine("osProfile");
Console.WriteLine("  computerName: " + vm.OSProfile.ComputerName);
Console.WriteLine("  adminUsername: " + vm.OSProfile.AdminUsername);
Console.WriteLine("  provisionVMAgent: " + vm.OSProfile.WindowsConfiguration.ProvisionVMAgent.Value);
Console.WriteLine("  enableAutomaticUpdates: " + vm.OSProfile.WindowsConfiguration.EnableAutomaticUpdates.Value);
Console.WriteLine("networkProfile");
foreach (string nicId in vm.NetworkInterfaceIds)
{
    Console.WriteLine("  networkInterface id: " + nicId);
}
Console.WriteLine("vmAgent");
Console.WriteLine("  vmAgentVersion" + vm.InstanceView.VmAgent.VmAgentVersion);
Console.WriteLine("    statuses");
foreach (InstanceViewStatus stat in vm.InstanceView.VmAgent.Statuses)
{
    Console.WriteLine("    code: " + stat.Code);
    Console.WriteLine("    level: " + stat.Level);
    Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
    Console.WriteLine("    message: " + stat.Message);
    Console.WriteLine("    time: " + stat.Time);
}
Console.WriteLine("disks");
foreach (DiskInstanceView disk in vm.InstanceView.Disks)
{
    Console.WriteLine("  name: " + disk.Name);
    Console.WriteLine("  statuses");
    foreach (InstanceViewStatus stat in disk.Statuses)
    {
        Console.WriteLine("    code: " + stat.Code);
        Console.WriteLine("    level: " + stat.Level);
        Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
        Console.WriteLine("    time: " + stat.Time);
    }
}
Console.WriteLine("VM general status");
Console.WriteLine("  provisioningStatus: " + vm.ProvisioningState);
Console.WriteLine("  id: " + vm.Id);
Console.WriteLine("  name: " + vm.Name);
Console.WriteLine("  type: " + vm.Type);
Console.WriteLine("  location: " + vm.Region);
Console.WriteLine("VM instance status");
foreach (InstanceViewStatus stat in vm.InstanceView.Statuses)
{
    Console.WriteLine("  code: " + stat.Code);
    Console.WriteLine("  level: " + stat.Level);
    Console.WriteLine("  displayStatus: " + stat.DisplayStatus);
}
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="stop-the-vm"></a><span data-ttu-id="b8074-169">VM을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-169">Stop the VM</span></span>

<span data-ttu-id="b8074-170">가상 컴퓨터를 중지하고 해당 설정을 모두 그대로 유지하면 계속 요금이 청구될 수 있습니다. 그렇지 않으려면 가상 컴퓨터를 중지하고 할당을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-170">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="b8074-171">가상 컴퓨터를 할당을 해제하면 연결된 모든 리소스의 할당이 취소되고 대금 청구가 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="b8074-172">할당을 취소하지 않고 가상 컴퓨터를 중지하려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-172">To stop the virtual machine without deallocating it, add this code to the Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

<span data-ttu-id="b8074-173">가상 컴퓨터의 할당을 취소하려는 경우 PowerOff 호출을 이 코드로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-173">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span></span>

```
vm.Deallocate();
```

### <a name="start-the-vm"></a><span data-ttu-id="b8074-174">VM 시작</span><span class="sxs-lookup"><span data-stu-id="b8074-174">Start the VM</span></span>

<span data-ttu-id="b8074-175">가상 컴퓨터를 시작하려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-175">To start the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="resize-the-vm"></a><span data-ttu-id="b8074-176">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="b8074-176">Resize the VM</span></span>

<span data-ttu-id="b8074-177">가상 컴퓨터의 크기를 결정할 때 배포의 여러 측면을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="b8074-178">자세한 내용은 [VM 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8074-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="b8074-179">가상 컴퓨터의 크기를 변경하려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-179">To change size of the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="b8074-180">VM에 데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="b8074-180">Add a data disk to the VM</span></span>

<span data-ttu-id="b8074-181">가상 컴퓨터에 데이터 디스크를 추가하려면 Main 메서드에 다음 코드를 추가하여 크기가 2GB이고 LUN이 0이며 캐싱 형식이 읽기/쓰기인 데이터 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-181">To add a data disk to the virtual machine, add this code to the Main method to add a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk to vm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter to delete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="b8074-182">리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="b8074-182">Delete resources</span></span>

<span data-ttu-id="b8074-183">Azure에서 사용되는 리소스에 대한 요금이 부과되기 때문에, 더 이상 필요하지 않은 리소스를 항상 삭제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-183">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="b8074-184">가상 컴퓨터 및 모든 지원 리소스를 삭제하려는 경우, 리소스 그룹을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-184">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

<span data-ttu-id="b8074-185">리소스 그룹을 삭제하려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-185">To delete the resource group, add this code to the Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-the-application"></a><span data-ttu-id="b8074-186">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="b8074-186">Run the application</span></span>

<span data-ttu-id="b8074-187">이 콘솔 응용 프로그램을 처음부터 끝까지 완전히 실행하려면 약 5분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-187">It should take about five minutes for this console application to run completely from start to finish.</span></span> 

1. <span data-ttu-id="b8074-188">콘솔 응용 프로그램을 실행하려면 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-188">To run the console application, click **Start**.</span></span>

2. <span data-ttu-id="b8074-189">**Enter** 키를 눌러 리소스를 삭제하기 전에 Azure Portal에서 리소스 만들기를 확인하는 데에 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-189">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="b8074-190">배포에 대한 정보를 보려면 배포 상태를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-190">Click the deployment status to see information about the deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8074-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8074-191">Next steps</span></span>
* <span data-ttu-id="b8074-192">[C# 및 Resource Manager 템플릿을 사용하여 Azure 가상 컴퓨터 배포](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)의 정보를 사용하여 가상 컴퓨터를 만드는 데 템플릿을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-192">Take advantage of using a template to create a virtual machine by using the information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="b8074-193">[.NET용 Azure 라이브러리](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet) 사용에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b8074-193">Learn more about using the [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

