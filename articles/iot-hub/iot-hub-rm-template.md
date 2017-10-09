---
title: "서식 파일 (.NET)를 사용 하 여 Azure IoT Hub aaaCreate | Microsoft Docs"
description: "어떻게 toouse Azure 리소스 관리자 템플릿 toocreate IoT Hub는 C# 프로그램을 사용 합니다."
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
ms.openlocfilehash: 6140deff3553701f994502fd4a60178f874e27cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="10316-103">Azure Resource Manager 템플릿을 사용하여 IoT Hub 만들기(.NET)</span><span class="sxs-lookup"><span data-stu-id="10316-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="10316-104">Toocreate Azure 리소스 관리자를 사용 하 고 Azure IoT 허브를 프로그래밍 방식으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10316-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="10316-105">이 자습서에서는 Azure 리소스 관리자 템플릿 toocreate C# 프로그램에서 IoT hub toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="10316-106">Azure에는 리소스를 만들고 작업하는 [Azure Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10316-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="10316-107">이 문서에서는 hello Azure 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="10316-108">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="10316-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="10316-109">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="10316-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="10316-110">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="10316-110">An active Azure account.</span></span> <br/><span data-ttu-id="10316-111">계정이 없는 경우 몇 분 만에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10316-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="10316-112">Azure Resource Manager 템플릿 파일을 저장할 수 있는 [Azure Storage 계정][lnk-storage-account]입니다.</span><span class="sxs-lookup"><span data-stu-id="10316-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="10316-113">[Azure PowerShell 1.0][lnk-powershell-install] 이상.</span><span class="sxs-lookup"><span data-stu-id="10316-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="10316-114">Visual Studio 프로젝트 준비</span><span class="sxs-lookup"><span data-stu-id="10316-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="10316-115">Visual Studio에서 hello를 사용 하 여 Visual C# Windows 클래식 데스크톱 프로젝트 만들기 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="10316-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="10316-116">이름 hello 프로젝트 **CreateIoTHub**합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-116">Name hello project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="10316-117">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="10316-118">NuGet 패키지 관리자에서 확인 **Include 시험판**, 등과 hello **찾아보기** 페이지 검색에 대 한 **Microsoft.Azure.Management.ResourceManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-118">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="10316-119">Hello 패키지를 선택를 클릭 **설치**에 **변경 내용 검토** 클릭 **확인**, 클릭 **동의** tooaccept hello 라이선스입니다.</span><span class="sxs-lookup"><span data-stu-id="10316-119">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="10316-120">NuGet 패키지 관리자에서 **Microsoft.IdentityModel.Clients.ActiveDirectory**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="10316-121">클릭 **설치**에 **변경 내용 검토** 클릭 **확인**, 클릭 **동의** tooaccept hello 라이선스입니다.</span><span class="sxs-lookup"><span data-stu-id="10316-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="10316-122">Program.cs에 hello 기존 항목 바꾸기 **를 사용 하 여** 코드 다음 hello로 문:</span><span class="sxs-lookup"><span data-stu-id="10316-122">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="10316-123">Program.cs에서 정적 변수 hello 자리 표시자 값 대체를 수행 하는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-123">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="10316-124">이 자습서의 앞부분에서 **ApplicationId**, **SubscriptionId**, **TenantId** 및 **암호**를 적어 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="10316-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="10316-125">**Azure 저장소 계정 이름은** Azure 리소스 관리자 템플릿 파일을 저장할 Azure 저장소 계정 hello hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="10316-125">**Your Azure Storage account name** is hello name of hello Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="10316-126">**리소스 그룹 이름은** hello hello IoT 허브를 만들 때 사용 하 여 hello 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="10316-126">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="10316-127">hello 이름은 기존 또는 새 리소스 그룹 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10316-127">hello name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="10316-128">**배포 이름** 에 대 한 이름이 hello 배포와 같은 **Deployment_01**합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="10316-129">서식 파일 toocreate IoT hub를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-129">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="10316-130">리소스 그룹에는 JSON 템플릿 및 매개 변수 파일 toocreate IoT 허브를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-130">Use a JSON template and parameter file toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="10316-131">Azure 리소스 관리자 템플릿 toomake 변경 tooan 기존 IoT hub를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10316-131">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="10316-132">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **새 항목**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="10316-133">이라는 JSON 파일을 추가 **template.json** tooyour 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="10316-133">Add a JSON file called **template.json** tooyour project.</span></span>

2. <span data-ttu-id="10316-134">표준 IoT 허브 toohello tooadd **미국 동부** 영역, replace hello 내용의 **template.json** 리소스 정의 다음 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-134">tooadd a standard IoT hub toohello **East US** region, replace hello contents of **template.json** with hello following resource definition.</span></span> <span data-ttu-id="10316-135">IoT Hub를 지 원하는 지역 hello 현재 목록에 대 한 참조 [Azure 상태][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="10316-135">For hello current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

3. <span data-ttu-id="10316-136">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **새 항목**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="10316-137">이라는 JSON 파일을 추가 **parameters.json** tooyour 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="10316-137">Add a JSON file called **parameters.json** tooyour project.</span></span>

4. <span data-ttu-id="10316-138">Hello 내용 바꾸기 **parameters.json** hello 다음와 같은 hello 새 IoT 허브에 대 한 이름을 설정 하는 매개 변수 정보로 **{이니셜} mynewiothub**합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-138">Replace hello contents of **parameters.json** with hello following parameter information that sets a name for hello new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="10316-139">사용자 이름이 나 이니셜과 포함 되어야 하므로 hello IoT 허브 이름을 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-139">hello IoT hub name must be globally unique so it should include your name or initials:</span></span>

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

5. <span data-ttu-id="10316-140">**서버 탐색기**tooyour Azure 구독을 연결 하 고 Azure 저장소에서 계정 컨테이너를 만듭니다 **템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-140">In **Server Explorer**, connect tooyour Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="10316-141">Hello에 **속성** 패널, 집합 hello **공용 읽기 액세스 권한을** hello에 대 한 권한을 **템플릿** 컨테이너 너무**Blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-141">In hello **Properties** panel, set hello **Public Read Access** permissions for hello **templates** container too**Blob**.</span></span>

6. <span data-ttu-id="10316-142">**서버 탐색기**, hello를 마우스 오른쪽 단추로 클릭 **템플릿** 컨테이너와 클릭 **Blob 컨테이너 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-142">In **Server Explorer**, right-click on hello **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="10316-143">Hello 클릭 **Blob 업로드** 단추, hello 두 개의 파일 **parameters.json** 및 **templates.json**, 클릭 하 고 **열려** tooupload hello JSON 파일 toohello **템플릿** 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="10316-143">Click hello **Upload Blob** button, select hello two files, **parameters.json** and **templates.json**, and then click **Open** tooupload hello JSON files toohello **templates** container.</span></span> <span data-ttu-id="10316-144">hello JSON 데이터를 포함 하는 hello blo hello Url이:</span><span class="sxs-lookup"><span data-stu-id="10316-144">hello URLs of hello blobs containing hello JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="10316-145">다음 메서드 tooProgram.cs hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-145">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="10316-146">다음 코드 toohello hello 추가 **CreateIoTHub** 메서드 toosubmit hello 템플릿 및 매개 변수 파일 toohello Azure 리소스 관리자:</span><span class="sxs-lookup"><span data-stu-id="10316-146">Add hello following code toohello **CreateIoTHub** method toosubmit hello template and parameter files toohello Azure Resource Manager:</span></span>

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

9. <span data-ttu-id="10316-147">다음 코드 toohello hello 추가 **CreateIoTHub** hello 상태 및 hello 새 IoT 허브에 대 한 hello 키를 표시 하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="10316-147">Add hello following code toohello **CreateIoTHub** method that displays hello status and hello keys for hello new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="10316-148">완전 하 고 실행 hello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="10316-148">Complete and run hello application</span></span>

<span data-ttu-id="10316-149">이제 hello를 호출 하 여 hello 응용 프로그램을 완료할 수 **CreateIoTHub** 메서드 전에 빌드 및 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-149">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="10316-150">추가 코드 toohello의 끝 다음 hello hello **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="10316-150">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="10316-151">**빌드**, **솔루션 빌드**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="10316-152">오류를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-152">Correct any errors.</span></span>

3. <span data-ttu-id="10316-153">클릭 **디버그** 차례로 **디버깅 시작** toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="10316-153">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="10316-154">배포 toorun hello에 대 일 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10316-154">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="10316-155">응용 프로그램이 추가 tooverify hello 새 IoT 허브를 방문 hello [Azure 포털] [ lnk-azure-portal] 및 리소스 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-155">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="10316-156">또는 hello를 사용 하 여 **Get AzureRmResource** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10316-156">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="10316-157">이 예제 응용 프로그램은 대금이 청구되는 S1 표준 IoT Hub를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="10316-158">Hello 통해 hello IoT 허브를 삭제할 수 있습니다 [Azure 포털] [ lnk-azure-portal] 또는 hello를 사용 하 여 **제거 AzureRmResource** 했으면 PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10316-158">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10316-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="10316-159">Next steps</span></span>
<span data-ttu-id="10316-160">IoT hub는 Azure 리소스 관리자 템플릿을 사용 하 여 C# 프로그램을 배포한 이제 tooexplore 더 이상 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10316-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want tooexplore further:</span></span>

* <span data-ttu-id="10316-161">Hello의 hello 기능에 대 한 읽기 [IoT 허브 리소스 공급자 REST API][lnk-rest-api]합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-161">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="10316-162">읽기 [Azure 리소스 관리자 개요] [ lnk-azure-rm-overview] toolearn hello Azure 리소스 관리자의 기능에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="10316-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="10316-163">IoT 허브에 대 한 개발에 대 한 더 toolearn hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="10316-163">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="10316-164">[소개 tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="10316-164">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="10316-165">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="10316-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="10316-166">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="10316-166">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="10316-167">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="10316-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
