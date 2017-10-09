---
title: "aaaCreate 및 Azure 가상 컴퓨터를 사용 하 여 Java 관리 | Microsoft Docs"
description: "가상 컴퓨터와 해당 지원 리소스를 모두 toodeploy Java 및 Azure 리소스 관리자를 사용 합니다."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 31ac8d59f92ecff887e64906940933dd6fd50815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a>Java를 사용하여 Azure에서 Windows VM 만들기 및 관리

[Azure VM(Virtual Machine)](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에 몇 가지 지원 Azure 리소스가 필요합니다. 이 문서에서는 Java를 사용하여 VM 리소스 만들기, 관리 및 삭제에 대해 설명합니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Maven 프로젝트 만들기
> * 종속성 추가
> * 자격 증명 만들기
> * 리소스 만들기
> * 관리 작업 수행
> * 리소스 삭제
> * Hello 응용 프로그램 실행

다음이 단계 toodo 약 20 분이 필요합니다.

## <a name="create-a-maven-project"></a>Maven 프로젝트 만들기

1. 아직 수행하지 않았다면 [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html)를 설치합니다.
2. [Maven](http://maven.apache.org/download.cgi)을 설치합니다.
3. 새 폴더 및 hello 프로젝트를 만듭니다.
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a>종속성 추가

1. Hello에서 `testAzureApp` 폴더, 열기 hello `pom.xml` 파일을 너무 hello 빌드 구성을 추가&lt;프로젝트&gt; 응용 프로그램의 tooenable hello 빌딩:

    ```xml
    <build>
      <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.App</mainClass>
            </configuration>
        </plugin>
      </plugins>
    </build>
    ```

2. Hello 종속성 필요한 tooaccess hello Azure Java SDK에 추가 합니다.

    ```xml
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-compute</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-resources</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-network</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.squareup.okio</groupId>
      <artifactId>okio</artifactId>
      <version>1.13.0</version>
    </dependency>
    <dependency> 
      <groupId>com.nimbusds</groupId>
      <artifactId>nimbus-jose-jwt</artifactId>
      <version>3.6</version>
    </dependency>
    <dependency>
      <groupId>net.minidev</groupId>
      <artifactId>json-smart</artifactId>
      <version>1.0.6.3</version>
    </dependency>
    <dependency>
      <groupId>javax.mail</groupId>
      <artifactId>mail</artifactId>
      <version>1.4.5</version>
    </dependency>
    ```

3. Hello 파일을 저장 합니다.

## <a name="create-credentials"></a>자격 증명 만들기

이 단계를 시작 하기 전에 액세스 tooan 했는지 확인 [Active Directory 서비스 사용자](../../azure-resource-manager/resource-group-create-service-principal-portal.md)합니다. 이후 단계에서 또한 hello 응용 프로그램 ID, 인증 키 hello 및 필요한 hello 테 넌 트 ID을 기록해 야 합니다.

### <a name="create-hello-authorization-file"></a>Hello 권한 부여 파일 만들기

1. 라는 파일을 만들어 `azureauth.properties` 하 고 이러한 속성 tooit 추가:

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

2. Hello 파일을 저장 합니다.
3. Hello 전체 경로 toohello 인증 파일 프로그램 셸의 AZURE_AUTH_LOCATION 라는 환경 변수를 설정 합니다.

### <a name="create-hello-management-client"></a>Hello 관리 클라이언트 만들기

1. 열기 hello `App.java` 아래 파일 `src\main\java\com\fabrikam` hello 위쪽에이 패키지 문을 인지 확인 합니다.

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. 이러한 추가 hello 패키지 문 아래 import 문의:
   
    ```java
    import com.microsoft.azure.management.Azure;
    import com.microsoft.azure.management.compute.AvailabilitySet;
    import com.microsoft.azure.management.compute.AvailabilitySetSkuTypes;
    import com.microsoft.azure.management.compute.CachingTypes;
    import com.microsoft.azure.management.compute.InstanceViewStatus;
    import com.microsoft.azure.management.compute.DiskInstanceView;
    import com.microsoft.azure.management.compute.VirtualMachine;
    import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
    import com.microsoft.azure.management.network.PublicIPAddress;
    import com.microsoft.azure.management.network.Network;
    import com.microsoft.azure.management.network.NetworkInterface;
    import com.microsoft.azure.management.resources.ResourceGroup;
    import com.microsoft.azure.management.resources.fluentcore.arm.Region;
    import com.microsoft.azure.management.resources.fluentcore.model.Creatable;
    import com.microsoft.rest.LogLevel;
    import java.io.File;
    import java.util.Scanner;
    ```

2. toocreate hello Active Directory 자격 증명 toomake 요청 해야 하는 hello App 클래스의이 코드 toohello main 메서드를 추가 합니다.
   
    ```java
    try {    
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
            .withLogLevel(LogLevel.BASIC)
            .authenticate(credFile)
            .withDefaultSubscription();
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }

    ```

## <a name="create-resources"></a>리소스 만들기

### <a name="create-hello-resource-group"></a>Hello 리소스 그룹 만들기

모든 리소스는 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md)에 포함되어야 합니다.

toospecify 값에 대 한 응용 프로그램 hello 및 hello 리소스 그룹 만들기 hello 기본 방법에서이 코드 toohello try 블록을 추가 합니다.

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a>Hello 가용성 집합 만들기

[가용성 집합](tutorial-availability-sets.md) 쉽게 드립니다 toomaintain hello 가상 컴퓨터 응용 프로그램에서 사용 합니다.

toocreate hello 가용성 설정, hello main 메서드에이 코드 toohello try 블록을 추가 합니다.

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a>Hello 공용 IP 주소 만들기

A [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hello 가상 컴퓨터와 필요한 toocommunicate 됩니다.

hello 가상 컴퓨터용 toocreate hello 공용 IP 주소 hello main 메서드에이 코드 toohello try 블록을 추가 합니다.

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a>Hello 가상 네트워크 만들기

가상 컴퓨터는 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)의 서브넷에 있어야 합니다.

toocreate는 서브넷과 가상 네트워크 hello main 메서드에이 코드 toohello try 블록을 추가 합니다.

```java
System.out.println("Creating virtual network...");
Network network = azure.networks()
    .define("myVN")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withAddressSpace("10.0.0.0/16")
    .withSubnet("mySubnet","10.0.0.0/24")
    .create();
```

### <a name="create-hello-network-interface"></a>Hello 네트워크 인터페이스 만들기

가상 컴퓨터에는 hello 가상 네트워크에서 네트워크 인터페이스 toocommunicate가 필요 합니다.

네트워크 인터페이스 toocreate hello main 메서드에이 코드 toohello try 블록을 추가 합니다.

```java
System.out.println("Creating network interface...");
NetworkInterface networkInterface = azure.networkInterfaces()
    .define("myNIC")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetwork(network)
    .withSubnet("mySubnet")
    .withPrimaryPrivateIPAddressDynamic()
    .withExistingPrimaryPublicIPAddress(publicIPAddress)
    .create();
```

### <a name="create-hello-virtual-machine"></a>Hello 가상 컴퓨터 만들기

리소스를 지 원하는 모든 hello, 만든 가상 컴퓨터를 만들 수 있습니다.

toocreate 가상 컴퓨터를 hello hello 기본 방법에서이 코드 toohello try 블록을 추가 합니다.

```java
System.out.println("Creating virtual machine...");
VirtualMachine virtualMachine = azure.virtualMachines()
    .define("myVM")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("azureuser")
    .withAdminPassword("Azure12345678")
    .withComputerName("myVM")
    .withExistingAvailabilitySet(availabilitySet)
    .withSize("Standard_DS1")
    .create();
Scanner input = new Scanner(System.in);
System.out.println("Press enter tooget information about hello VM...");
input.nextLine();
```

> [!NOTE]
> 이 자습서는 hello Windows Server 운영 체제의 버전을 실행 하는 가상 컴퓨터를 만듭니다. 다른 이미지 선택에 대 한 더 toolearn 참조 [탐색 하 고 Windows PowerShell 및 Azure CLI hello를 사용 하 여 Azure 가상 컴퓨터 이미지 선택](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
> 
>

Toouse 마켓플레이스 이미지 대신 기존 디스크를 사용 하도록 하려는 경우이 코드를 사용 하세요. 

```java
ManagedDisk managedDisk = azure.disks.define("myosdisk") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd") 
    .withSizeInGB(128) 
    .withSku(DiskSkuTypes.PremiumLRS) 
    .create(); 

azure.virtualMachines.define("myVM") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withExistingPrimaryNetworkInterface(networkInterface) 
    .withSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows) 
    .withExistingAvailabilitySet(availabilitySet) 
    .withSize(VirtualMachineSizeTypes.StandardDS1) 
    .create(); 
``` 

## <a name="perform-management-tasks"></a>관리 작업 수행

가상 컴퓨터의 hello 수명 주기 동안 시작, 중지, 또는 가상 컴퓨터를 삭제 하는 등의 toorun 관리 작업을 할 수 있습니다. 또한 toocreate 코드 tooautomate 반복적 복잡 한 작업을 지정할 수 있습니다.

필요한 toodo VM hello로 아무 것도 해당 형식의 인스턴스 tooget가 필요 합니다. 이 코드 toohello try 블록의 hello main 메서드를 추가 합니다.

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a>Hello VM에 대 한 정보 가져오기

hello 가상 컴퓨터에 대 한 tooget 정보 hello main 메서드에이 코드 toohello try 블록을 추가 합니다.

```java
System.out.println("hardwareProfile");
System.out.println("    vmSize: " + vm.size());
System.out.println("storageProfile");
System.out.println("  imageReference");
System.out.println("    publisher: " + vm.storageProfile().imageReference().publisher());
System.out.println("    offer: " + vm.storageProfile().imageReference().offer());
System.out.println("    sku: " + vm.storageProfile().imageReference().sku());
System.out.println("    version: " + vm.storageProfile().imageReference().version());
System.out.println("  osDisk");
System.out.println("    osType: " + vm.storageProfile().osDisk().osType());
System.out.println("    name: " + vm.storageProfile().osDisk().name());
System.out.println("    createOption: " + vm.storageProfile().osDisk().createOption());
System.out.println("    caching: " + vm.storageProfile().osDisk().caching());
System.out.println("osProfile");
System.out.println("    computerName: " + vm.osProfile().computerName());
System.out.println("    adminUserName: " + vm.osProfile().adminUsername());
System.out.println("    provisionVMAgent: " + vm.osProfile().windowsConfiguration().provisionVMAgent());
System.out.println("    enableAutomaticUpdates: " + vm.osProfile().windowsConfiguration().enableAutomaticUpdates());
System.out.println("networkProfile");
System.out.println("    networkInterface: " + vm.primaryNetworkInterfaceId());
System.out.println("vmAgent");
System.out.println("  vmAgentVersion: " + vm.instanceView().vmAgent().vmAgentVersion());
System.out.println("    statuses");
for(InstanceViewStatus status : vm.instanceView().vmAgent().statuses()) {
    System.out.println("    code: " + status.code());
    System.out.println("    displayStatus: " + status.displayStatus());
    System.out.println("    message: " + status.message());
    System.out.println("    time: " + status.time());
}
System.out.println("disks");
for(DiskInstanceView disk : vm.instanceView().disks()) {
    System.out.println("  name: " + disk.name());
    System.out.println("  statuses");
    for(InstanceViewStatus status : disk.statuses()) {
        System.out.println("    code: " + status.code());
        System.out.println("    displayStatus: " + status.displayStatus());
        System.out.println("    time: " + status.time());
    }
}
System.out.println("VM general status");
System.out.println("  provisioningStatus: " + vm.provisioningState());
System.out.println("  id: " + vm.id());
System.out.println("  name: " + vm.name());
System.out.println("  type: " + vm.type());
System.out.println("VM instance status");
for(InstanceViewStatus status : vm.instanceView().statuses()) {
    System.out.println("  code: " + status.code());
    System.out.println("  displayStatus: " + status.displayStatus());
}
System.out.println("Press enter toocontinue...");
input.nextLine();   
```

### <a name="stop-hello-vm"></a>Hello VM 중지

가상 컴퓨터를 중지 하 고 해당 설정을 모두 그대로 유지 하지만 계속 toobe 유료로 제공, 가상 컴퓨터를 중지 하 고 할당을 취소 하거나 수 있습니다. 가상 컴퓨터를 할당을 해제하면 연결된 모든 리소스의 할당이 취소되고 대금 청구가 끝납니다.

toostop hello 가상 컴퓨터를 할당 취소 하지 않고 hello main 메서드에이 코드 toohello try 블록을 추가 합니다.

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

Toodeallocate hello 가상 컴퓨터를 하려면 hello 전원 꺼짐 통화 toothis 코드를 변경 합니다.

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a>Hello VM 시작

toostart 가상 컴퓨터를 hello hello 기본 방법에서이 코드 toohello try 블록을 추가 합니다.

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a>Hello VM의 크기를 조정합니다

가상 컴퓨터의 크기를 결정할 때 배포의 여러 측면을 고려해야 합니다. 자세한 내용은 [VM 크기](sizes.md)를 참조하세요.  

hello 가상 컴퓨터의 toochange 크기 hello main 메서드에이 코드 toohello try 블록을 추가 합니다.

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>데이터 디스크 toohello VM 추가

tooadd 크기가 2 GB 있는 데이터 디스크 toohello 가상 컴퓨터에 0이 고 캐싱 유형의 ReadWrite LUN hello 기본 방법에서이 코드 toohello try 블록을 추가 합니다.

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a>리소스 삭제

Azure에서 사용 되는 리소스에 대 한 요금이 청구 되므로 항상 것은 더 이상 필요 없는 것이 좋습니다 toodelete 리소스입니다. Toodelete hello 가상 컴퓨터 및 리소스를 지 원하는 모든 hello, 모든 있는 toodo hello 리소스 그룹 삭제 됩니다.

1. toodelete hello 리소스 그룹에서이 코드 toohello try 블록 hello main 메서드에 추가 합니다.
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. Hello App.java 파일을 저장 합니다.

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행

이 콘솔 응용 프로그램 toorun 시작 toofinish에서 완전히에 대 일 분 정도 취해야 합니다.

1. toorun 응용 프로그램 hello이 Maven 명령을 사용 합니다.

    ```
    mvn compile exec:java
    ```

2. 누르기 전에 **Enter** toostart 삭제 리소스를 가져올 수 있었습니다 몇 분 정도 hello 리소스 tooverify hello 만들기 hello Azure 포털의에서. Hello 배포 상태 toosee hello 배포에 대 한 정보를 클릭 합니다.


## <a name="next-steps"></a>다음 단계
* Hello를 사용 하는 방법에 대 한 자세한 정보 [Java 용 Azure 라이브러리](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview)합니다.

