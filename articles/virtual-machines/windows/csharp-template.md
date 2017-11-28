---
title: "C# 및 Resource Manager 템플릿을 사용하여 VM 배포 | Microsoft Docs"
description: "C# 및 Resource Manager 템플릿을 사용하여 Azure VM을 배포하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: bd1c860db026f948202cd1f3aa763b4547c597b4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="1b801-103">C# 및 Resource Manager 템플릿을 사용하여 Azure 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="1b801-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="1b801-104">이 문서에서는 C#을 사용하여 Azure Resource Manager 템플릿을 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-104">This article shows you how to deploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="1b801-105">만든 템플릿은 단일 서브넷을 사용하는 새 가상 네트워크에서 Windows Server를 실행하는 단일 가상 컴퓨터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="1b801-106">가상 컴퓨터 리소스에 대한 자세한 설명은 [Azure Resource Manager 템플릿의 가상 컴퓨터](template-description.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b801-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="1b801-107">템플릿에 있는 모든 리소스에 대한 자세한 내용은 [Azure Resource Manager 템플릿 연습](../../azure-resource-manager/resource-manager-template-walkthrough.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b801-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="1b801-108">이러한 단계를 수행하려면 약 10분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-108">It takes about 10 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="1b801-109">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="1b801-109">Create a Visual Studio project</span></span>

<span data-ttu-id="1b801-110">이 단계에서는 Visual Studio가 설치되어 있는지 확인하고 템플릿을 배포하는 데 사용하는 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-110">In this step, you make sure that Visual Studio is installed and you create a console application used to deploy the template.</span></span>

1. <span data-ttu-id="1b801-111">[Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio)를 아직 설치하지 않았으면 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="1b801-112">작업 페이지에서 **.NET 데스크톱 개발**을 선택한 다음 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-112">Select **.NET desktop development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="1b801-113">요약에서 **.NET Framework 4 - 4.6 개발 도구**가 자동으로 선택되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-113">In the summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="1b801-114">Visual Studio를 이미 설치한 경우 Visual Studio 시작 관리자를 사용하여 .NET 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-114">If you have already installed Visual Studio, you can add the .NET workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="1b801-115">Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="1b801-116">**템플릿** > **Visual C#**에서 **콘솔 앱(.NET Framework)**을 선택하고, 프로젝트의 이름에 *myDotnetProject*를 입력하고 프로젝트의 위치를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-the-packages"></a><span data-ttu-id="1b801-117">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="1b801-117">Install the packages</span></span>

<span data-ttu-id="1b801-118">NuGet 패키지는 이러한 단계를 완료하는데 필요한 라이브러리를 설치하는 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-118">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="1b801-119">Visual Studio에서 필요한 라이브러리를 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-119">To get the libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="1b801-120">**도구** > **Nuget 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="1b801-121">콘솔에서 다음이 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-121">Type these commands in the console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-the-files"></a><span data-ttu-id="1b801-122">파일 만들기</span><span class="sxs-lookup"><span data-stu-id="1b801-122">Create the files</span></span>

<span data-ttu-id="1b801-123">이 단계에서는 리소스를 배포하는 템플릿 파일과 템플릿에 매개 변수 값을 제공하는 매개 변수 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-123">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="1b801-124">또한 Azure Resource Manager 작업을 수행하는 데 사용되는 권한 부여 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-124">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

### <a name="create-the-template-file"></a><span data-ttu-id="1b801-125">템플릿 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="1b801-125">Create the template file</span></span>

1. <span data-ttu-id="1b801-126">솔루션 탐색기에서 *myDotnetProject* > **추가** > **새 항목**을 마우스 오른쪽 단추로 클릭한 다음 *Visual C# 항목*에서 **텍스트 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="1b801-127">파일 이름을 *CreateVMTemplate.json*으로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-127">Name the file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="1b801-128">만든 파일에 이 JSON 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-128">Add this JSON code to the file that you created:</span></span>

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

3. <span data-ttu-id="1b801-129">CreateVMTemplate.json 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-129">Save the CreateVMTemplate.json file.</span></span>

### <a name="create-the-parameters-file"></a><span data-ttu-id="1b801-130">매개 변수 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="1b801-130">Create the parameters file</span></span>

<span data-ttu-id="1b801-131">템플릿에 정의된 리소스 매개 변수의 값을 지정하려면 값이 들어 있는 매개 변수 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-131">To specify values for the resource parameters that are defined in the template, you create a parameters file that contains the values.</span></span>

1. <span data-ttu-id="1b801-132">솔루션 탐색기에서 *myDotnetProject* > **추가** > **새 항목**을 마우스 오른쪽 단추로 클릭한 다음 *Visual C# 항목*에서 **텍스트 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="1b801-133">파일 이름을 *Parameters.json*으로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-133">Name the file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="1b801-134">만든 파일에 이 JSON 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-134">Add this JSON code to the file that you created:</span></span>

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

4. <span data-ttu-id="1b801-135">Parameters.json 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-135">Save the Parameters.json file.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="1b801-136">권한 부여 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="1b801-136">Create the authorization file</span></span>

<span data-ttu-id="1b801-137">템플릿을 배포하기 전에 [Active Directory 서비스 사용자](../../resource-group-authenticate-service-principal.md)에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-137">Before you can deploy a template, make sure that you have access to an [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="1b801-138">서비스 주체에서 Azure Resource Manager에서 요청을 인증받기 위한 토큰을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-138">From the service principal, you acquire a token for authenticating requests to Azure Resource Manager.</span></span> <span data-ttu-id="1b801-139">또한 권한 부여 파일에서 필요한 응용 프로그램 ID, 인증 키 및 테넌트 ID를 기록해 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-139">You should also record the application ID, the authentication key, and the tenant ID that you need in the authorization file.</span></span>

1. <span data-ttu-id="1b801-140">솔루션 탐색기에서 *myDotnetProject* > **추가** > **새 항목**을 마우스 오른쪽 단추로 클릭한 다음 *Visual C# 항목*에서 **텍스트 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="1b801-141">파일 이름을 *azureauth.properties*로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-141">Name the file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="1b801-142">다음과 같은 권한 부여 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-142">Add these authorization properties:</span></span>

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

    <span data-ttu-id="1b801-143">**&lt;subscription-id&gt;**를 구독 식별자, **&lt;application-id&gt;**를 Active Directory 응용 프로그램 식별자, **&lt;authentication-key&gt;**를 응용 프로그램 키, **&lt;tenant-id&gt;**를 테넌트 식별자로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

3. <span data-ttu-id="1b801-144">azureauth.properties 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-144">Save the azureauth.properties file.</span></span>
4. <span data-ttu-id="1b801-145">AZURE_AUTH_LOCATION이라는 Windows 환경 변수를 만든 권한 부여 파일의 전체 경로로 설정합니다. 예를 들어 다음 PowerShell 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with the full path to authorization file that you created, for example the following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-the-management-client"></a><span data-ttu-id="1b801-146">관리 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="1b801-146">Create the management client</span></span>

1. <span data-ttu-id="1b801-147">만들었던 프로젝트에 대한 Program.cs 파일을 연 후, 다음 using 문을 파일의 위쪽에 기존 문에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-147">Open the Program.cs file for the project that you created, and then add these using statements to the existing statements at top of the file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="1b801-148">관리 클라이언트를 만들려면 다음 코드를 Main 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-148">To create the management client, add this code to the Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="1b801-149">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="1b801-149">Create a resource group</span></span>

<span data-ttu-id="1b801-150">응용 프로그램에 대한 값을 지정하려면 다음 코드를 Main 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-150">To specify values for the application, add code to the Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="1b801-151">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1b801-151">Create a storage account</span></span>

<span data-ttu-id="1b801-152">템플릿 및 매개 변수는 Azure의 저장소 계정에서 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-152">The template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="1b801-153">이 단계에서는 계정을 만들고 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-153">In this step, you create the account and upload the files.</span></span> 

<span data-ttu-id="1b801-154">계정을 만들려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-154">To create the account, add this code to the Main method:</span></span>

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

## <a name="deploy-the-template"></a><span data-ttu-id="1b801-155">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="1b801-155">Deploy the template</span></span>

<span data-ttu-id="1b801-156">만든 저장소 계정에서 템플릿 및 매개 변수를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-156">Deploy the template and parameters from the storage account that was created.</span></span> 

<span data-ttu-id="1b801-157">템플릿을 배포하려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-157">To deploy the template, add this code to the Main method:</span></span>

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter to delete the resource group...");
Console.ReadLine();
```

## <a name="delete-the-resources"></a><span data-ttu-id="1b801-158">리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="1b801-158">Delete the resources</span></span>

<span data-ttu-id="1b801-159">Azure에서 사용되는 리소스에 대한 요금이 부과되기 때문에, 더 이상 필요하지 않은 리소스를 항상 삭제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-159">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="1b801-160">리소스 그룹에서 각 리소스를 개별적으로 삭제할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-160">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="1b801-161">리소스 그룹을 삭제하면 모든 해당 리소스가 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-161">Delete the resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="1b801-162">리소스 그룹을 삭제하려면 Main 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-162">To delete the resource group, add this code to the Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-the-application"></a><span data-ttu-id="1b801-163">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="1b801-163">Run the application</span></span>

<span data-ttu-id="1b801-164">이 콘솔 응용 프로그램을 처음부터 끝까지 완전히 실행하려면 약 5분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-164">It should take about five minutes for this console application to run completely from start to finish.</span></span> 

1. <span data-ttu-id="1b801-165">콘솔 응용 프로그램을 실행하려면 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-165">To run the console application, click **Start**.</span></span>

2. <span data-ttu-id="1b801-166">**Enter** 키를 눌러 리소스를 삭제하기 전에 Azure Portal에서 리소스 만들기를 확인하는 데에 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-166">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="1b801-167">배포에 대한 정보를 보려면 배포 상태를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-167">Click the deployment status to see information about the deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b801-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b801-168">Next steps</span></span>
* <span data-ttu-id="1b801-169">배포에 문제가 있는 경우 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](../../resource-manager-common-deployment-errors.md)을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-169">If there were issues with the deployment, a next step would be to look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="1b801-170">[C#를 사용하여 Azure Virtual Machine 배포](csharp.md)를 검토하여 가상 컴퓨터 및 지원 리소스 배포 방법에 대해 알아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1b801-170">Learn how to deploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
