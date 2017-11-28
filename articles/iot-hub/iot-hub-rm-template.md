---
title: "템플릿을 사용하여 Azure IoT Hub 만들기(.NET) | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 C# 프로그램으로 IoT Hub를 만드는 방법입니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a447b40c-c728-487e-875d-db554db5adc3
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 0f197a28e0c51b06d0b47a03c29fe1fde0c6b78d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="12d54-103">Azure Resource Manager 템플릿을 사용하여 IoT Hub 만들기(.NET)</span><span class="sxs-lookup"><span data-stu-id="12d54-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="12d54-104">Azure 리소스 관리자를 사용하여 Azure IoT Hub를 프로그래밍 방식으로 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="12d54-105">이 자습서는 Azure Resource Manager 템플릿을 사용하여 C# 프로그램에서 IoT Hub를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="12d54-106">Azure에는 리소스를 만들고 작업하는 [Azure Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="12d54-107">이 문서에서는 Azure Resource Manager 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="12d54-108">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="12d54-109">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="12d54-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="12d54-110">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="12d54-110">An active Azure account.</span></span> <br/><span data-ttu-id="12d54-111">계정이 없는 경우 몇 분 만에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="12d54-112">Azure Resource Manager 템플릿 파일을 저장할 수 있는 [Azure Storage 계정][lnk-storage-account]입니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="12d54-113">[Azure PowerShell 1.0][lnk-powershell-install] 이상.</span><span class="sxs-lookup"><span data-stu-id="12d54-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="12d54-114">Visual Studio 프로젝트 준비</span><span class="sxs-lookup"><span data-stu-id="12d54-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="12d54-115">Visual Studio에서 **콘솔 앱(.NET Framework)** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 바탕 화면 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="12d54-116">프로젝트 이름을 **CreateIoTHub**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-116">Name the project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="12d54-117">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="12d54-118">NuGet 패키지 관리자에서 **시험판 포함**을 선택하고 **찾아보기** 페이지에서 **Microsoft.Azure.Management.ResourceManager**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-118">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="12d54-119">패키지를 선택하고 **설치**를 클릭하고 **변경 내용 검토**에서 **확인**을 클릭한 다음 **동의함**을 클릭하여 라이선스에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-119">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="12d54-120">NuGet 패키지 관리자에서 **Microsoft.IdentityModel.Clients.ActiveDirectory**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="12d54-121">**설치**를 클릭하고 **변경 내용 검토**에서 **확인**을 클릭한 다음 **동의함**을 클릭하여 라이선스에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="12d54-122">Program.cs에서 기존 **using** 문을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-122">In Program.cs, replace the existing **using** statements with the following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="12d54-123">Program.cs에서 다음 정적 변수를 추가하여 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-123">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="12d54-124">이 자습서의 앞부분에서 **ApplicationId**, **SubscriptionId**, **TenantId** 및 **암호**를 적어 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="12d54-125">**Azure Storage 계정 이름**은 Azure Resource Manager 템플릿 파일을 저장할 Azure Storage 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-125">**Your Azure Storage account name** is the name of the Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="12d54-126">**리소스 그룹 이름**은 IoT Hub를 만들 때 사용할 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-126">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="12d54-127">이름은 기존 또는 새 리소스 그룹일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-127">The name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="12d54-128">**배포 이름**은 **Deployment_01**과 같은 배포의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    static string storageAddress = "https://{Your storage account name}.blob.core.windows.net";
    static string rgName = "{Resource group name}";
    static string deploymentName = "{Deployment name}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="12d54-129">IoT hub를 만들 템플릿 제출</span><span class="sxs-lookup"><span data-stu-id="12d54-129">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="12d54-130">JSON 템플릿과 매개 변수 파일을 사용하여 리소스 그룹에 IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-130">Use a JSON template and parameter file to create an IoT hub in your resource group.</span></span> <span data-ttu-id="12d54-131">Azure Resource Manager 템플릿을 사용하여 기존 IoT Hub를 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-131">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="12d54-132">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **새 항목**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="12d54-133">프로젝트에 **template.json**이라는 JSON 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-133">Add a JSON file called **template.json** to your project.</span></span>

2. <span data-ttu-id="12d54-134">표준 IoT Hub를 **미국 동부** 지역에 추가하려면 **template.json**의 콘텐츠를 다음 리소스 정의로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-134">To add a standard IoT hub to the **East US** region, replace the contents of **template.json** with the following resource definition.</span></span> <span data-ttu-id="12d54-135">IoT Hub를 지원하는 현재 지역 목록에 대해서는 [Azure 상태][lnk-status]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d54-135">For the current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

3. <span data-ttu-id="12d54-136">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **새 항목**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="12d54-137">프로젝트에 **parameters.json**이라는 JSON 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-137">Add a JSON file called **parameters.json** to your project.</span></span>

4. <span data-ttu-id="12d54-138">새 IoT Hub의 이름을 **{your initials}mynewiothub** 등으로 설정하는 다음 매개 변수 정보로 **parameters.json**의 내용을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-138">Replace the contents of **parameters.json** with the following parameter information that sets a name for the new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="12d54-139">IoT Hub 이름은 전역적으로 고유해야 하므로 사용자의 이름 또는 이니셜을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-139">The IoT hub name must be globally unique so it should include your name or initials:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": { "value": "mynewiothub" }
      }
    }
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

5. <span data-ttu-id="12d54-140">**서버 탐색기**에서 Azure 구독에 연결하고 Azure Storage 계정에서 **templates**라는 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-140">In **Server Explorer**, connect to your Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="12d54-141">**속성** 패널에서 **templates** 컨테이너의 **공용 읽기 액세스** 권한을 **Blob**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-141">In the **Properties** panel, set the **Public Read Access** permissions for the **templates** container to **Blob**.</span></span>

6. <span data-ttu-id="12d54-142">**서버 탐색기**에서 **templates** 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **Blob 컨테이너 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-142">In **Server Explorer**, right-click on the **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="12d54-143">**Blob 업로드** 단추를 클릭하고, **parameters.json** 및 **templates.json** 파일을 선택한 다음 **열기**를 클릭하여 JSON 파일을 **templates** 컨테이너에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-143">Click the **Upload Blob** button, select the two files, **parameters.json** and **templates.json**, and then click **Open** to upload the JSON files to the **templates** container.</span></span> <span data-ttu-id="12d54-144">JSON 데이터를 포함하는 Blob의 URL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-144">The URLs of the blobs containing the JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="12d54-145">Program.cs에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-145">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="12d54-146">**CreateIoTHub** 메서드에 다음 코드를 추가하여 Azure Resource Manager에게 템플릿 및 매개 변수 파일을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-146">Add the following code to the **CreateIoTHub** method to submit the template and parameter files to the Azure Resource Manager:</span></span>

    ```csharp
    var createResponse = client.Deployments.CreateOrUpdate(
        rgName,
        deploymentName,
        new Deployment()
        {
          Properties = new DeploymentProperties
          {
            Mode = DeploymentMode.Incremental,
            TemplateLink = new TemplateLink
            {
              Uri = storageAddress + "/templates/template.json"
            },
            ParametersLink = new ParametersLink
            {
              Uri = storageAddress + "/templates/parameters.json"
            }
          }
        });
    ```

9. <span data-ttu-id="12d54-147">새 IoT Hub의 상태 및 키를 표시하는 다음 코드를 **CreateIoTHub** 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-147">Add the following code to the **CreateIoTHub** method that displays the status and the keys for the new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed to create iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="12d54-148">응용 프로그램을 완료하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-148">Complete and run the application</span></span>

<span data-ttu-id="12d54-149">이제 응용 프로그램을 빌드하고 실행하기 전에 **CreateIoTHub** 메서드를 호출하여 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-149">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="12d54-150">**Main** 메서드의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-150">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="12d54-151">**빌드**, **솔루션 빌드**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="12d54-152">오류를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-152">Correct any errors.</span></span>

3. <span data-ttu-id="12d54-153">**디버그**, **디버깅 시작**을 차례로 클릭하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-153">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="12d54-154">배포를 실행하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-154">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="12d54-155">응용 프로그램이 새 IoT Hub에 추가되었는지 확인하려면 [Azure Portal][lnk-azure-portal]을 방문하여 리소스 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-155">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="12d54-156">또는 **Get AzureRmResource** PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-156">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="12d54-157">이 예제 응용 프로그램은 대금이 청구되는 S1 표준 IoT Hub를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="12d54-158">완료되면 [Azure Portal][lnk-azure-portal] 또는 **Remove-AzureRmResource** PowerShell cmdlet을 사용하여 IoT Hub를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-158">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12d54-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12d54-159">Next steps</span></span>
<span data-ttu-id="12d54-160">Azure Resource Manager 템플릿을 사용하여 C# 프로그램에서 IoT Hub를 배포했으므로 구체적인 내용을 알아볼 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="12d54-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want to explore further:</span></span>

* <span data-ttu-id="12d54-161">[IoT Hub 리소스 공급자 REST API][lnk-rest-api]의 기능을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="12d54-161">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="12d54-162">Azure Resource Manager의 기능에 대해 자세히 알아보려면 [Azure Resource Manager 개요][lnk-azure-rm-overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d54-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="12d54-163">IoT Hub를 개발하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d54-163">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="12d54-164">[C SDK 소개][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="12d54-164">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="12d54-165">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="12d54-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="12d54-166">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d54-166">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="12d54-167">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="12d54-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
