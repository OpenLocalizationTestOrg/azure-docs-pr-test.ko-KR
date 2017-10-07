---
title: "사용 하 여 Azure IoT 허브 aaaCreate 리소스 공급자 REST API hello | Microsoft Docs"
description: "어떻게 toouse IoT Hub 리소스 공급자 REST API toocreate를 hello 합니다."
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
ms.openlocfilehash: 98d240ccce47dec13a255bce28943b40f5354ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a><span data-ttu-id="8120e-103">Hello 리소스 공급자 REST API (.NET)를 사용 하 여 IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-103">Create an IoT hub using hello resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="8120e-104">Hello를 사용할 수 있습니다 [IoT 허브 리소스 공급자 REST API] [ lnk-rest-api] toocreate 및 Azure IoT 허브를 프로그래밍 방식으로 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-104">You can use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="8120e-105">이 자습서에서는 어떻게 toouse hello IoT 허브 리소스 공급자 REST API toocreate C# 프로그램에서 IoT hub를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-105">This tutorial shows you how toouse hello IoT Hub resource provider REST API toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="8120e-106">Azure에는 리소스를 만들고 작업하는 [Azure Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8120e-107">이 문서에서는 hello Azure 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="8120e-108">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="8120e-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="8120e-109">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="8120e-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="8120e-110">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="8120e-110">An active Azure account.</span></span> <br/><span data-ttu-id="8120e-111">계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="8120e-112">[Azure PowerShell 1.0][lnk-powershell-install] 이상.</span><span class="sxs-lookup"><span data-stu-id="8120e-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="8120e-113">Visual Studio 프로젝트 준비</span><span class="sxs-lookup"><span data-stu-id="8120e-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="8120e-114">Visual Studio에서 hello를 사용 하 여 Visual C# Windows 클래식 데스크톱 프로젝트 만들기 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="8120e-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="8120e-115">이름 hello 프로젝트 **CreateIoTHubREST**합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-115">Name hello project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="8120e-116">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="8120e-117">NuGet 패키지 관리자에서 확인 **Include 시험판**, 등과 hello **찾아보기** 페이지 검색에 대 한 **Microsoft.Azure.Management.ResourceManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-117">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="8120e-118">Hello 패키지를 선택를 클릭 **설치**에 **변경 내용 검토** 클릭 **확인**, 클릭 **동의** tooaccept hello 라이선스입니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-118">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="8120e-119">NuGet 패키지 관리자에서 **Microsoft.IdentityModel.Clients.ActiveDirectory**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="8120e-120">클릭 **설치**에 **변경 내용 검토** 클릭 **확인**, 클릭 **동의** tooaccept hello 라이선스입니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="8120e-121">Program.cs에 hello 기존 항목 바꾸기 **를 사용 하 여** 코드 다음 hello로 문:</span><span class="sxs-lookup"><span data-stu-id="8120e-121">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

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

6. <span data-ttu-id="8120e-122">Program.cs에서 정적 변수 hello 자리 표시자 값 대체를 수행 하는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-122">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="8120e-123">이 자습서의 앞부분에서 **ApplicationId**, **SubscriptionId**, **TenantId** 및 **암호**를 적어 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="8120e-124">**리소스 그룹 이름은** hello hello IoT 허브를 만들 때 사용 하 여 hello 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-124">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="8120e-125">기존 또는 새 리소스 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="8120e-126">**IoT Hub 이름을** hello IoT Hub와 같은 만들의 hello 이름인 **MyIoTHub**합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-126">**IoT Hub name** is hello name of hello IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="8120e-127">IoT hub의 hello 이름 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-127">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="8120e-128">**배포 이름** 에 대 한 이름이 hello 배포와 같은 **Deployment_01**합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a><span data-ttu-id="8120e-129">Hello 리소스 공급자 REST API toocreate IoT hub 사용</span><span class="sxs-lookup"><span data-stu-id="8120e-129">Use hello resource provider REST API toocreate an IoT hub</span></span>

<span data-ttu-id="8120e-130">사용 하 여 hello [IoT 허브 리소스 공급자 REST API] [ lnk-rest-api] toocreate 리소스 그룹에서 IoT hub 합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-130">Use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="8120e-131">Hello 리소스 공급자 REST API toomake 변경 tooan 기존 IoT 허브를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-131">You can also use hello resource provider REST API toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="8120e-132">다음 메서드 tooProgram.cs hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-132">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="8120e-133">다음 코드 toohello hello 추가 **CreateIoTHub** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8120e-133">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="8120e-134">이 코드에서는 **HttpClient** hello 인증 토큰 hello 헤더에 있는 개체:</span><span class="sxs-lookup"><span data-stu-id="8120e-134">This code creates an **HttpClient** object with hello authentication token in hello headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="8120e-135">다음 코드 toohello hello 추가 **CreateIoTHub** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8120e-135">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="8120e-136">이 코드는 hello IoT 허브 toocreate에 설명 하 고 JSON 표현을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-136">This code describes hello IoT hub toocreate and generates a JSON representation.</span></span> <span data-ttu-id="8120e-137">Hello 현재 목록이 IoT Hub를 지 원하는 위치에 대 한 참조 [Azure 상태][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="8120e-137">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

4. <span data-ttu-id="8120e-138">다음 코드 toohello hello 추가 **CreateIoTHub** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8120e-138">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="8120e-139">이 코드는 hello REST 요청 tooAzure 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-139">This code submits hello REST request tooAzure.</span></span> <span data-ttu-id="8120e-140">hello 코드 다음 hello 응답을 확인 하 고 검색 hello URL toomonitor hello 상태의 hello 배포 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-140">hello code then checks hello response and retrieves hello URL you can use toomonitor hello state of hello deployment task:</span></span>

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

5. <span data-ttu-id="8120e-141">추가 코드 toohello의 끝 다음 hello hello **CreateIoTHub** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8120e-141">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="8120e-142">이 코드 hello를 사용 하 여 **asyncStatusUri** 배포 toocomplete hello에 대 한 이전 단계 toowait hello에에서 주소를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-142">This code uses hello **asyncStatusUri** address retrieved in hello previous step toowait for hello deployment toocomplete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="8120e-143">추가 코드 toohello의 끝 다음 hello hello **CreateIoTHub** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8120e-143">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="8120e-144">이 코드의 hello IoT 허브에서 사용자가 만들고 toohello 콘솔을 인쇄 hello 키를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-144">This code retrieves hello keys of hello IoT hub you created and prints them toohello console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="8120e-145">완전 하 고 실행 hello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8120e-145">Complete and run hello application</span></span>

<span data-ttu-id="8120e-146">이제 hello를 호출 하 여 hello 응용 프로그램을 완료할 수 **CreateIoTHub** 메서드 전에 빌드 및 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-146">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="8120e-147">추가 코드 toohello의 끝 다음 hello hello **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="8120e-147">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="8120e-148">**빌드**, **솔루션 빌드**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="8120e-149">오류를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-149">Correct any errors.</span></span>

3. <span data-ttu-id="8120e-150">클릭 **디버그** 차례로 **디버깅 시작** toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-150">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="8120e-151">배포 toorun hello에 대 일 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-151">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="8120e-152">응용 프로그램이 추가 tooverify hello 새 IoT 허브를 방문 hello [Azure 포털] [ lnk-azure-portal] 및 리소스 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-152">tooverify that your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="8120e-153">또는 hello를 사용 하 여 **Get AzureRmResource** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8120e-153">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="8120e-154">이 예제 응용 프로그램은 대금이 청구되는 S1 표준 IoT Hub를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="8120e-155">완료 되 면 hello IoT hub hello 통해 삭제할 수 있습니다 [Azure 포털] [ lnk-azure-portal] 또는 hello를 사용 하 여 **제거 AzureRmResource** 했으면 PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8120e-155">When you are finished, you can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8120e-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8120e-156">Next steps</span></span>
<span data-ttu-id="8120e-157">Hello 리소스 공급자 REST API를 사용 하 여 IoT hub를 배포한 이제 tooexplore 더 이상 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-157">Now you have deployed an IoT hub using hello resource provider REST API, you may want tooexplore further:</span></span>

* <span data-ttu-id="8120e-158">Hello의 hello 기능에 대 한 읽기 [IoT 허브 리소스 공급자 REST API][lnk-rest-api]합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-158">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="8120e-159">읽기 [Azure 리소스 관리자 개요] [ lnk-azure-rm-overview] toolearn hello Azure 리소스 관리자의 기능에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8120e-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="8120e-160">IoT 허브에 대 한 개발에 대 한 더 toolearn hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8120e-160">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="8120e-161">[소개 tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="8120e-161">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="8120e-162">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="8120e-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="8120e-163">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8120e-163">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8120e-164">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="8120e-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
