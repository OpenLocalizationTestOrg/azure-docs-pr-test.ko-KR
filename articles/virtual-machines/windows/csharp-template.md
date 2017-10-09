---
title: "C# 및 리소스 관리자 템플릿을 사용 하 여 VM a aaaDeploy | Microsoft Docs"
description: "리소스 관리자 템플릿 toodeploy Azure VM toohow toouse C#에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: bfba66e8-c923-4df2-900a-0c2643b81240
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: davidmu
ms.openlocfilehash: 91d470228cfeed72336b488ffef4dfbb25bc3a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a>C# 및 Resource Manager 템플릿을 사용하여 Azure 가상 컴퓨터 배포
이 문서에서는 C#을 사용 하는 Azure 리소스 관리자 템플릿 toodeploy 합니다. 만든 hello 템플릿을 단일 서브넷으로 새 가상 네트워크에서 Windows Server를 실행 하는 단일 가상 컴퓨터를 배포 합니다.

에 대 한 자세한 설명은 hello 가상 컴퓨터 리소스를 참조 하세요. [가상 컴퓨터는 Azure 리소스 관리자 템플릿](template-description.md)합니다. 서식 파일의 모든 hello 리소스에 대 한 자세한 내용은 참조 [Azure 리소스 관리자 템플릿 연습](../../azure-resource-manager/resource-manager-template-walkthrough.md)합니다.

다음이 단계 toodo 약 10 분이 필요합니다.

## <a name="create-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기

이 단계에서는 수 있도록 Visual Studio가 설치 및 콘솔 응용 프로그램 사용 toodeploy hello 템플릿을 만들 있습니다.

1. [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio)를 아직 설치하지 않았으면 설치합니다. 선택 **.NET 데스크톱 개발** 작업 페이지 hello 되 고 클릭 **설치**합니다. Hello 요약을 볼 수 있습니다는 **.NET Framework 4 4.6 개발 도구** 가 자동으로 선택 됩니다. Visual Studio를 이미 설치한 경우 Visual Studio 시작 관리자 hello를 사용 하 여 hello.NET 작업을 추가할 수 있습니다.
2. Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 클릭합니다.
3. **템플릿** > **Visual C#**선택, **콘솔 응용 프로그램 (.NET Framework)**, 입력 *myDotnetProject* hello 이름에 대 한 프로젝트를 hello 프로젝트의 위치 선택 hello hello 및 클릭 **확인**합니다.

## <a name="install-hello-packages"></a>Hello 패키지 설치

NuGet 패키지는 hello 가장 쉬운 방법은 tooinstall hello 라이브러리 할 toofinish 다음이 단계입니다. tooget hello 라이브러리는 Visual Studio에 필요한 다음이 단계를 수행 합니다.

1. **도구** > **Nuget 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.
2. Hello 콘솔에서 다음이 명령을 입력 합니다.

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a>Hello 파일 만들기

이 단계에서는 hello 리소스를 배포 하는 템플릿 파일 및 매개 변수 값 toohello 서식 파일을 제공 하는 매개 변수 파일을 만듭니다. 권한 부여 되는 파일을 사용 하는 tooperform Azure 리소스 관리자 작업을 만들 수도 있습니다.

### <a name="create-hello-template-file"></a>Hello 서식 파일 만들기

1. 솔루션 탐색기에서 *myDotnetProject* > **추가** > **새 항목**을 마우스 오른쪽 단추로 클릭한 다음 *Visual C# 항목*에서 **텍스트 파일**을 선택합니다. 이름 hello 파일 *CreateVMTemplate.json*, 클릭 하 고 **추가**합니다.
2. 이 JSON 코드 toohello 만든 파일을 추가 합니다.

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

3. Hello CreateVMTemplate.json 파일을 저장 합니다.

### <a name="create-hello-parameters-file"></a>Hello 매개 변수 파일 만들기

toospecify hello 서식 파일에 정의 된 hello 리소스 매개 변수 값을 hello 값을 포함 하는 매개 변수 파일을 만듭니다.

1. 솔루션 탐색기에서 *myDotnetProject* > **추가** > **새 항목**을 마우스 오른쪽 단추로 클릭한 다음 *Visual C# 항목*에서 **텍스트 파일**을 선택합니다. 이름 hello 파일 *Parameters.json*, 클릭 하 고 **추가**합니다.
2. 이 JSON 코드 toohello 만든 파일을 추가 합니다.

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

4. Hello Parameters.json 파일을 저장 합니다.

### <a name="create-hello-authorization-file"></a>Hello 권한 부여 파일 만들기

서식 파일을 배포 하려면 먼저 액세스 tooan 있는지 확인 [Active Directory 서비스 사용자](../../resource-group-authenticate-service-principal.md)합니다. Hello 서비스 보안 주체에서 요청 tooAzure 리소스 관리자를 인증 하기 위한 토큰을 획득 합니다. Hello 응용 프로그램 ID, 인증 키 hello 및는 hello 권한 부여 파일에 필요한 hello 테 넌 트 ID를도 기록해 야 합니다.

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
4. 예를 들어 다음 PowerShell 명령을 사용 하 여 hello을 windows hello 전체 경로 tooauthorization 만든 파일에 있는 AZURE_AUTH_LOCATION 라는 환경 변수 설정:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a>Hello 관리 클라이언트 만들기

1. 사용자가 만든 hello 프로젝트에 대 한 hello Program.cs 파일을 열고 hello 파일의 맨 위쪽에 문을 toohello 기존 문을 사용 하 여이 추가 합니다.

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
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

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

hello 응용 프로그램에 대 한 toospecify 값 toohello Main 메서드에 코드를 추가 합니다.

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a>저장소 계정 만들기

hello 템플릿 및 매개 변수는 Azure의 저장소 계정에서 배포 됩니다. 이 단계에서는 hello 계정을 만들고 hello 파일을 업로드 합니다. 

toocreate 계정 hello,이 코드 toohello Main 메서드에 추가 합니다.

```
string storageAccountName = SdkContext.RandomResourceName("st", 10);

Console.WriteLine("Creating storage account...");
var storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USWest)
    .WithExistingResourceGroup(resourceGroup)
    .Create();

var storageKeys = storage.GetKeys();
string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=" + storage.Name
    + ";AccountKey=" + storageKeys[0].Value
    + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
var serviceClient = account.CreateCloudBlobClient();

Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("templates");
container.CreateIfNotExistsAsync().Wait();
var containerPermissions = new BlobContainerPermissions()
    { PublicAccess = BlobContainerPublicAccessType.Container };
container.SetPermissionsAsync(containerPermissions).Wait();

Console.WriteLine("Uploading template file...");
var templateblob = container.GetBlockBlobReference("CreateVMTemplate.json");
templateblob.UploadFromFile("..\\..\\CreateVMTemplate.json");

Console.WriteLine("Uploading parameters file...");
var paramblob = container.GetBlockBlobReference("Parameters.json");
paramblob.UploadFromFile("..\\..\\Parameters.json");
```

## <a name="deploy-hello-template"></a>Hello 템플릿을 배포합니다

Hello 템플릿 및 생성 된 hello 저장소 계정에서 매개 변수를 배포 합니다. 

toodeploy hello 서식 파일을이 코드 toohello Main 메서드에 추가 합니다.

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter toodelete hello resource group...");
Console.ReadLine();
```

## <a name="delete-hello-resources"></a>Hello 리소스 삭제

Azure에서 사용 되는 리소스에 대 한 요금이 청구 되므로 항상 것은 더 이상 필요 없는 것이 좋습니다 toodelete 리소스입니다. 각 리소스는 리소스 그룹에서 별도로 toodelete을 필요 하지 않습니다. Hello 리소스 그룹을 삭제 하 고 모든 리소스를 자동으로 삭제 됩니다. 

toodelete hello 리소스 그룹에서이 코드 toohello Main 메서드에 추가 합니다.

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행

이 콘솔 응용 프로그램 toorun 시작 toofinish에서 완전히에 대 일 분 정도 취해야 합니다. 

1. toorun hello 콘솔 응용 프로그램을 클릭 하 여 **시작**합니다.

2. 누르기 전에 **Enter** toostart 삭제 리소스를 가져올 수 있었습니다 몇 분 정도 hello 리소스 tooverify hello 만들기 hello Azure 포털의에서. Hello 배포 상태 toosee hello 배포에 대 한 정보를 클릭 합니다.

## <a name="next-steps"></a>다음 단계
* 다음 단계에서 toolook 것 hello 배포 문제가 있는 경우 [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](../../resource-manager-common-deployment-errors.md)합니다.
* 자세한 내용은 방법 toodeploy 가상 컴퓨터 및 지원 리소스를 검토 하 여 [배포는 Azure 가상 컴퓨터를 사용 하 여 C#](csharp.md)합니다.
