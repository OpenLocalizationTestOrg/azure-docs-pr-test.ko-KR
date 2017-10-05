---
title: "리소스 공급자 REST API를 사용하여 Azure IoT Hub 만들기 | Microsoft Docs"
description: "리소스 공급자 REST API를 사용하여 IoT Hub를 만드는 방법입니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 52814ee5-bc10-4abe-9eb2-f8973096c2d8
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e443259507aacbefca141be4c9c1688ab19bf6ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-resource-provider-rest-api-net"></a><span data-ttu-id="364b7-103">리소스 공급자 REST API(.NET)를 사용하여 IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="364b7-103">Create an IoT hub using the resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="364b7-104">[IoT Hub 리소스 공급자 REST API][lnk-rest-api]를 사용하여 Azure IoT Hub를 프로그래밍 방식으로 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-104">You can use the [IoT Hub resource provider REST API][lnk-rest-api] to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="364b7-105">이 자습서는 IoT Hub 리소스 공급자 REST API를 사용하여 C# 프로그램에서 IoT Hub를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-105">This tutorial shows you how to use the IoT Hub resource provider REST API to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="364b7-106">Azure에는 리소스를 만들고 작업하는 [Azure Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="364b7-107">이 문서에서는 Azure Resource Manager 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="364b7-108">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="364b7-109">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="364b7-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="364b7-110">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="364b7-110">An active Azure account.</span></span> <br/><span data-ttu-id="364b7-111">계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="364b7-112">[Azure PowerShell 1.0][lnk-powershell-install] 이상.</span><span class="sxs-lookup"><span data-stu-id="364b7-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="364b7-113">Visual Studio 프로젝트 준비</span><span class="sxs-lookup"><span data-stu-id="364b7-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="364b7-114">Visual Studio에서 **콘솔 앱(.NET Framework)** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 바탕 화면 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="364b7-115">프로젝트 이름을 **CreateIoTHubREST**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-115">Name the project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="364b7-116">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="364b7-117">NuGet 패키지 관리자에서 **시험판 포함**을 선택하고 **찾아보기** 페이지에서 **Microsoft.Azure.Management.ResourceManager**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-117">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="364b7-118">패키지를 선택하고 **설치**를 클릭하고 **변경 내용 검토**에서 **확인**을 클릭한 다음 **동의함**을 클릭하여 라이선스에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-118">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="364b7-119">NuGet 패키지 관리자에서 **Microsoft.IdentityModel.Clients.ActiveDirectory**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="364b7-120">**설치**를 클릭하고 **변경 내용 검토**에서 **확인**을 클릭한 다음 **동의함**을 클릭하여 라이선스에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="364b7-121">Program.cs에서 기존 **using** 문을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-121">In Program.cs, replace the existing **using** statements with the following code:</span></span>

    ```csharp
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```

6. <span data-ttu-id="364b7-122">Program.cs에서 다음 정적 변수를 추가하여 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-122">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="364b7-123">이 자습서의 앞부분에서 **ApplicationId**, **SubscriptionId**, **TenantId** 및 **암호**를 적어 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="364b7-124">**리소스 그룹 이름**은 IoT Hub를 만들 때 사용할 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-124">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="364b7-125">기존 또는 새 리소스 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="364b7-126">**IoT Hub 이름**은 **MyIoTHub**와 같이 사용자가 만든 IoT Hub의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-126">**IoT Hub name** is the name of the IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="364b7-127">IoT hub의 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-127">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="364b7-128">**배포 이름**은 **Deployment_01**과 같은 배포의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";

    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```
[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-the-resource-provider-rest-api-to-create-an-iot-hub"></a><span data-ttu-id="364b7-129">리소스 공급자 REST API를 사용하여 IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="364b7-129">Use the resource provider REST API to create an IoT hub</span></span>

<span data-ttu-id="364b7-130">[IoT Hub 리소스 공급자 REST API][lnk-rest-api]를 사용하여 리소스 그룹에 새 IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-130">Use the [IoT Hub resource provider REST API][lnk-rest-api] to create an IoT hub in your resource group.</span></span> <span data-ttu-id="364b7-131">리소스 공급자 REST API를 사용하여 기존 IoT Hub를 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-131">You can also use the resource provider REST API to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="364b7-132">Program.cs에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-132">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="364b7-133">**CreateIoTHub** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-133">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="364b7-134">이 코드에서는 헤더에서 인증 토큰을 사용하여 **HttpClient** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-134">This code creates an **HttpClient** object with the authentication token in the headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="364b7-135">**CreateIoTHub** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-135">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="364b7-136">이 코드는 JSON 표현을 만들고 생성하는 IoT Hub를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-136">This code describes the IoT hub to create and generates a JSON representation.</span></span> <span data-ttu-id="364b7-137">IoT Hub를 지원하는 현재 위치 목록에 대해서는 [Azure 상태][lnk-status]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364b7-137">For the current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

    ```csharp
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };

    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```

4. <span data-ttu-id="364b7-138">**CreateIoTHub** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-138">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="364b7-139">이 코드는 Azure에 REST 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-139">This code submits the REST request to Azure.</span></span> <span data-ttu-id="364b7-140">그런 다음, 코드는 응답을 확인하며 배포 작업의 상태를 모니터링하는 데 사용할 수 있는 URL을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-140">The code then checks the response and retrieves the URL you can use to monitor the state of the deployment task:</span></span>

    ```csharp
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;

    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }

    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```

5. <span data-ttu-id="364b7-141">**CreateIoTHub** 메서드의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-141">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="364b7-142">이 코드는 배포가 완료되기를 대기하는 이전 단계에서 검색된 **asyncStatusUri** 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-142">This code uses the **asyncStatusUri** address retrieved in the previous step to wait for the deployment to complete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="364b7-143">**CreateIoTHub** 메서드의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-143">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="364b7-144">이 코드는 사용자가 만들고 콘솔에 출력한 IoT Hub의 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-144">This code retrieves the keys of the IoT hub you created and prints them to the console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="364b7-145">응용 프로그램을 완료하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-145">Complete and run the application</span></span>

<span data-ttu-id="364b7-146">이제 응용 프로그램을 빌드하고 실행하기 전에 **CreateIoTHub** 메서드를 호출하여 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-146">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="364b7-147">**Main** 메서드의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-147">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="364b7-148">**빌드**, **솔루션 빌드**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="364b7-149">오류를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-149">Correct any errors.</span></span>

3. <span data-ttu-id="364b7-150">**디버그**, **디버깅 시작**을 차례로 클릭하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-150">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="364b7-151">배포를 실행하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-151">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="364b7-152">응용 프로그램이 새 IoT Hub에 추가되었는지 확인하려면 [Azure Portal][lnk-azure-portal]을 방문하여 리소스 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-152">To verify that your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="364b7-153">또는 **Get AzureRmResource** PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-153">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="364b7-154">이 예제 응용 프로그램은 대금이 청구되는 S1 표준 IoT Hub를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="364b7-155">작업이 완료되면 [Azure Portal][lnk-azure-portal]을 통해 또는 **Remove-AzureRmResource** PowerShell cmdlet을 사용하여 IoT Hub를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-155">When you are finished, you can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="364b7-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="364b7-156">Next steps</span></span>
<span data-ttu-id="364b7-157">리소스 공급자 REST API를 사용하여 IoT Hub를 배포했으면 구체적인 내용을 알아볼 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="364b7-157">Now you have deployed an IoT hub using the resource provider REST API, you may want to explore further:</span></span>

* <span data-ttu-id="364b7-158">[IoT Hub 리소스 공급자 REST API][lnk-rest-api]의 기능을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="364b7-158">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="364b7-159">Azure Resource Manager의 기능에 대해 자세히 알아보려면 [Azure Resource Manager 개요][lnk-azure-rm-overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364b7-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="364b7-160">IoT Hub를 개발하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364b7-160">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="364b7-161">[C SDK 소개][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="364b7-161">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="364b7-162">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="364b7-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="364b7-163">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364b7-163">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="364b7-164">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="364b7-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
