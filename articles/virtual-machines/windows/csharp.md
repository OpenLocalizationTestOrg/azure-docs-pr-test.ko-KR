---
title: "aaaCreate 하 고 관리할 수 있는 Azure 가상 컴퓨터를 사용 하 여 C# | Microsoft Docs"
description: "가상 컴퓨터와 해당 지원 리소스를 모두 toodeploy C# 및 Azure 리소스 관리자를 사용 합니다."
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
ms.openlocfilehash: 8beeabde731bbaa25e68d2b9c5abbf71acbe377f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a>C#을 사용하여 Azure에서 Windows VM 생성 및 관리 #

[Azure 가상 컴퓨터](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)(VM)에 몇 가지 지원 Azure 리소스가 필요합니다. 이 문서에서는 C#을 사용하여 VM 리소스 만들기, 관리 및 삭제에 대해 설명합니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Visual Studio 프로젝트 만들기
> * Hello 패키지 설치
> * 자격 증명 만들기
> * 리소스 만들기
> * 관리 작업 수행
> * 리소스 삭제
> * Hello 응용 프로그램 실행

다음이 단계 toodo 약 20 분이 필요합니다.

## <a name="create-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기

1. [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio)를 아직 설치하지 않았으면 설치합니다. 선택 **.NET 데스크톱 개발** 작업 페이지 hello 되 고 클릭 **설치**합니다. Hello 요약을 볼 수 있습니다는 **.NET Framework 4 4.6 개발 도구** 가 자동으로 선택 됩니다. Visual Studio를 이미 설치한 경우 Visual Studio 시작 관리자 hello를 사용 하 여 hello.NET 작업을 추가할 수 있습니다.
2. Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 클릭합니다.
3. **템플릿** > **Visual C#**선택, **콘솔 응용 프로그램 (.NET Framework)**, 입력 *myDotnetProject* hello 이름에 대 한 프로젝트를 hello 프로젝트의 위치 선택 hello hello 및 클릭 **확인**합니다.

## <a name="install-hello-package"></a>Hello 패키지 설치

NuGet 패키지는 hello 가장 쉬운 방법은 tooinstall hello 라이브러리 할 toofinish 다음이 단계입니다. tooget hello 라이브러리는 Visual Studio에 필요한 다음이 단계를 수행 합니다.

1. **도구** > **Nuget 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.
2. Hello 콘솔에서이 명령을 입력 합니다.

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a>자격 증명 만들기

이 단계를 시작 하기 전에 액세스 tooan 했는지 확인 [Active Directory 서비스 사용자](../../azure-resource-manager/resource-group-create-service-principal-portal.md)합니다. 이후 단계에서 또한 hello 응용 프로그램 ID, 인증 키 hello 및 필요한 hello 테 넌 트 ID을 기록해 야 합니다.

### <a name="create-hello-authorization-file"></a>Hello 권한 부여 파일 만들기

1. 솔루션 탐색기에서 *myDotnetProject* > **추가** > **새 항목**을 마우스 오른쪽 단추로 클릭한 다음 *Visual C# 항목*에서 **텍스트 파일**을 선택합니다. 이름 hello 파일 *azureauth.properties*, 클릭 하 고 **추가**합니다.
2. 다음과 같은 권한 부여 속성을 추가합니다.

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

    대체  **&lt;-&gt;**  구독 식별자를 가진  **&lt;응용 프로그램 id&gt;**  Active Directory 응용 프로그램 hello로 식별자,  **&lt;인증 키&gt;**  hello 응용 프로그램 키를 포함 하 고  **&lt;테 넌 트 id&gt;**  hello 테 넌 트와 식별자입니다.

3. Hello azureauth.properties 파일을 저장 합니다. 
4. Windows hello 전체 경로 tooauthorization 만든 파일에 있는 AZURE_AUTH_LOCATION 라는 환경 변수를 설정 합니다. 예를 들어 hello 다음 PowerShell 명령을 사용할 수 있습니다.

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a>Hello 관리 클라이언트 만들기

1. 사용자가 만든 hello 프로젝트에 대 한 hello Program.cs 파일을 열고 hello 파일의 맨 위쪽에 문을 toohello 기존 문을 사용 하 여이 추가 합니다.

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. toocreate hello management 클라이언트에서는이 코드 toohello Main 메서드에 추가 합니다.

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a>리소스 만들기

### <a name="create-hello-resource-group"></a>Hello 리소스 그룹 만들기

모든 리소스는 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md)에 포함되어야 합니다.

toospecify 값에 대 한 응용 프로그램 hello 및 hello 리소스 그룹 만들기,이 코드 toohello Main 메서드에 추가 합니다.

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a>Hello 가용성 집합 만들기

[가용성 집합](tutorial-availability-sets.md) 쉽게 드립니다 toomaintain hello 가상 컴퓨터 응용 프로그램에서 사용 합니다.

toocreate hello 가용성 설정,이 코드 toohello Main 메서드에 추가 합니다.

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a>Hello 공용 IP 주소 만들기

A [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hello 가상 컴퓨터와 필요한 toocommunicate 됩니다.

hello 가상 컴퓨터용 toocreate hello 공용 IP 주소에이 코드 toohello Main 메서드에 추가 합니다.
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a>Hello 가상 네트워크 만들기

가상 컴퓨터는 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)의 서브넷에 있어야 합니다.

toocreate는 서브넷과 가상 네트워크에이 코드 toohello Main 메서드에 추가 합니다.

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a>Hello 네트워크 인터페이스 만들기

가상 컴퓨터에는 hello 가상 네트워크에서 네트워크 인터페이스 toocommunicate가 필요 합니다.

toocreate 네트워크 인터페이스에이 코드 toohello Main 메서드에 추가 합니다.

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

### <a name="create-hello-virtual-machine"></a>Hello 가상 컴퓨터 만들기

리소스를 지 원하는 모든 hello, 만든 가상 컴퓨터를 만들 수 있습니다.

toocreate hello 가상 컴퓨터에서이 코드 toohello Main 메서드에 추가 합니다.

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
> 이 자습서는 hello Windows Server 운영 체제의 버전을 실행 하는 가상 컴퓨터를 만듭니다. 다른 이미지 선택에 대 한 더 toolearn 참조 [탐색 하 고 Windows PowerShell 및 Azure CLI hello를 사용 하 여 Azure 가상 컴퓨터 이미지 선택](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
> 
>

Toouse 마켓플레이스 이미지 대신 기존 디스크를 사용 하도록 하려는 경우이 코드를 사용 하세요.

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

## <a name="perform-management-tasks"></a>관리 작업 수행

가상 컴퓨터의 hello 수명 주기 동안 시작, 중지, 또는 가상 컴퓨터를 삭제 하는 등의 toorun 관리 작업을 할 수 있습니다. 또한 toocreate 코드 tooautomate 반복적 복잡 한 작업을 지정할 수 있습니다.

Toodo VM hello를 사용 하 여 작업을 해야 하는 경우 해당 형식의 인스턴스 tooget이 필요 합니다.

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a>Hello VM에 대 한 정보 가져오기

이 코드 toohello Main 메서드에 추가 하는 hello 가상 컴퓨터에 대 한 tooget 정보:

```
Console.WriteLine("Getting information about hello virtual machine...");
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
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="stop-hello-vm"></a>Hello VM 중지

가상 컴퓨터를 중지 하 고 해당 설정을 모두 그대로 유지 하지만 계속 toobe 유료로 제공, 가상 컴퓨터를 중지 하 고 할당을 취소 하거나 수 있습니다. 가상 컴퓨터를 할당을 해제하면 연결된 모든 리소스의 할당이 취소되고 대금 청구가 끝납니다.

toostop hello 가상 컴퓨터를 할당 취소 하지 않고이 코드 toohello Main 메서드에 추가 합니다.

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

Toodeallocate hello 가상 컴퓨터를 하려면 hello 전원 꺼짐 통화 toothis 코드를 변경 합니다.

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a>Hello VM 시작

toostart hello 가상 컴퓨터에서이 코드 toohello Main 메서드에 추가 합니다.

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a>Hello VM의 크기를 조정합니다

가상 컴퓨터의 크기를 결정할 때 배포의 여러 측면을 고려해야 합니다. 자세한 내용은 [VM 크기](sizes.md)를 참조하세요.  

이 코드 toohello Main 메서드에 추가 하는 hello 가상 컴퓨터의 toochange 크기:

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>데이터 디스크 toohello VM 추가

tooadd 데이터 디스크 toohello 가상 컴퓨터를이 코드 toohello Main 메서드 tooadd 한 LUN 0이 고 캐싱 유형의 ReadWrite 크기가 2 GB 되는 데이터 디스크를 추가 합니다.

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a>리소스 삭제

Azure에서 사용 되는 리소스에 대 한 요금이 청구 되므로 항상 것은 더 이상 필요 없는 것이 좋습니다 toodelete 리소스입니다. Toodelete hello 가상 컴퓨터 및 리소스를 지 원하는 모든 hello, 모든 있는 toodo hello 리소스 그룹 삭제 됩니다.

toodelete hello 리소스 그룹에서이 코드 toohello Main 메서드에 추가 합니다.

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행

이 콘솔 응용 프로그램 toorun 시작 toofinish에서 완전히에 대 일 분 정도 취해야 합니다. 

1. toorun hello 콘솔 응용 프로그램을 클릭 하 여 **시작**합니다.

2. 누르기 전에 **Enter** toostart 삭제 리소스를 가져올 수 있었습니다 몇 분 정도 hello 리소스 tooverify hello 만들기 hello Azure 포털의에서. Hello 배포 상태 toosee hello 배포에 대 한 정보를 클릭 합니다.

## <a name="next-steps"></a>다음 단계
* 활용 템플릿 toocreate를 사용 하 여 가상 컴퓨터 정보 hello를 사용 하 여 [C# 및 리소스 관리자 템플릿을 사용 하 여 Azure 가상 컴퓨터 배포](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
* Hello를 사용 하는 방법에 대 한 자세한 정보 [.NET 용 Azure 라이브러리](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet)합니다.

