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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a>Azure Resource Manager 템플릿을 사용하여 IoT Hub 만들기(.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Toocreate Azure 리소스 관리자를 사용 하 고 Azure IoT 허브를 프로그래밍 방식으로 관리할 수 있습니다. 이 자습서에서는 Azure 리소스 관리자 템플릿 toocreate C# 프로그램에서 IoT hub toouse 합니다.

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Azure Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.  이 문서에서는 hello Azure 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* Visual Studio 2015 또는 Visual Studio 2017.
* 활성 Azure 계정. <br/>계정이 없는 경우 몇 분 만에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.
* Azure Resource Manager 템플릿 파일을 저장할 수 있는 [Azure Storage 계정][lnk-storage-account]입니다.
* [Azure PowerShell 1.0][lnk-powershell-install] 이상.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Visual Studio 프로젝트 준비

1. Visual Studio에서 hello를 사용 하 여 Visual C# Windows 클래식 데스크톱 프로젝트 만들기 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일 프로젝트. 이름 hello 프로젝트 **CreateIoTHub**합니다.

2. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리**를 클릭합니다.

3. NuGet 패키지 관리자에서 확인 **Include 시험판**, 등과 hello **찾아보기** 페이지 검색에 대 한 **Microsoft.Azure.Management.ResourceManager**합니다. Hello 패키지를 선택를 클릭 **설치**에 **변경 내용 검토** 클릭 **확인**, 클릭 **동의** tooaccept hello 라이선스입니다.

4. NuGet 패키지 관리자에서 **Microsoft.IdentityModel.Clients.ActiveDirectory**를 검색합니다.  클릭 **설치**에 **변경 내용 검토** 클릭 **확인**, 클릭 **동의** tooaccept hello 라이선스입니다.

5. Program.cs에 hello 기존 항목 바꾸기 **를 사용 하 여** 코드 다음 hello로 문:

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. Program.cs에서 정적 변수 hello 자리 표시자 값 대체를 수행 하는 hello를 추가 합니다. 이 자습서의 앞부분에서 **ApplicationId**, **SubscriptionId**, **TenantId** 및 **암호**를 적어 두었습니다. **Azure 저장소 계정 이름은** Azure 리소스 관리자 템플릿 파일을 저장할 Azure 저장소 계정 hello hello 이름입니다. **리소스 그룹 이름은** hello hello IoT 허브를 만들 때 사용 하 여 hello 리소스 그룹 이름입니다. hello 이름은 기존 또는 새 리소스 그룹 수 있습니다. **배포 이름** 에 대 한 이름이 hello 배포와 같은 **Deployment_01**합니다.

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

## <a name="submit-a-template-toocreate-an-iot-hub"></a>서식 파일 toocreate IoT hub를 제출 합니다.

리소스 그룹에는 JSON 템플릿 및 매개 변수 파일 toocreate IoT 허브를 사용 합니다. Azure 리소스 관리자 템플릿 toomake 변경 tooan 기존 IoT hub를 사용할 수 있습니다.

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **새 항목**을 차례로 클릭합니다. 이라는 JSON 파일을 추가 **template.json** tooyour 프로젝트.

2. 표준 IoT 허브 toohello tooadd **미국 동부** 영역, replace hello 내용의 **template.json** 리소스 정의 다음 hello로 합니다. IoT Hub를 지 원하는 지역 hello 현재 목록에 대 한 참조 [Azure 상태][lnk-status]:

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

3. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **새 항목**을 차례로 클릭합니다. 이라는 JSON 파일을 추가 **parameters.json** tooyour 프로젝트.

4. Hello 내용 바꾸기 **parameters.json** hello 다음와 같은 hello 새 IoT 허브에 대 한 이름을 설정 하는 매개 변수 정보로 **{이니셜} mynewiothub**합니다. 사용자 이름이 나 이니셜과 포함 되어야 하므로 hello IoT 허브 이름을 전역적으로 고유 해야 합니다.

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

5. **서버 탐색기**tooyour Azure 구독을 연결 하 고 Azure 저장소에서 계정 컨테이너를 만듭니다 **템플릿**합니다. Hello에 **속성** 패널, 집합 hello **공용 읽기 액세스 권한을** hello에 대 한 권한을 **템플릿** 컨테이너 너무**Blob**합니다.

6. **서버 탐색기**, hello를 마우스 오른쪽 단추로 클릭 **템플릿** 컨테이너와 클릭 **Blob 컨테이너 보기**합니다. Hello 클릭 **Blob 업로드** 단추, hello 두 개의 파일 **parameters.json** 및 **templates.json**, 클릭 하 고 **열려** tooupload hello JSON 파일 toohello **템플릿** 컨테이너입니다. hello JSON 데이터를 포함 하는 hello blo hello Url이:

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. 다음 메서드 tooProgram.cs hello를 추가 합니다.

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. 다음 코드 toohello hello 추가 **CreateIoTHub** 메서드 toosubmit hello 템플릿 및 매개 변수 파일 toohello Azure 리소스 관리자:

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

9. 다음 코드 toohello hello 추가 **CreateIoTHub** hello 상태 및 hello 새 IoT 허브에 대 한 hello 키를 표시 하는 메서드입니다.

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a>완전 하 고 실행 hello 응용 프로그램

이제 hello를 호출 하 여 hello 응용 프로그램을 완료할 수 **CreateIoTHub** 메서드 전에 빌드 및 실행 합니다.

1. 추가 코드 toohello의 끝 다음 hello hello **Main** 메서드:

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. **빌드**, **솔루션 빌드**를 차례로 클릭합니다. 오류를 수정합니다.

3. 클릭 **디버그** 차례로 **디버깅 시작** toorun hello 응용 프로그램입니다. 배포 toorun hello에 대 일 분 정도 걸릴 수 있습니다.

4. 응용 프로그램이 추가 tooverify hello 새 IoT 허브를 방문 hello [Azure 포털] [ lnk-azure-portal] 및 리소스 목록을 표시 합니다. 또는 hello를 사용 하 여 **Get AzureRmResource** PowerShell cmdlet.

> [!NOTE]
> 이 예제 응용 프로그램은 대금이 청구되는 S1 표준 IoT Hub를 추가합니다. Hello 통해 hello IoT 허브를 삭제할 수 있습니다 [Azure 포털] [ lnk-azure-portal] 또는 hello를 사용 하 여 **제거 AzureRmResource** 했으면 PowerShell cmdlet.

## <a name="next-steps"></a>다음 단계
IoT hub는 Azure 리소스 관리자 템플릿을 사용 하 여 C# 프로그램을 배포한 이제 tooexplore 더 이상 사용할 수 있습니다.

* Hello의 hello 기능에 대 한 읽기 [IoT 허브 리소스 공급자 REST API][lnk-rest-api]합니다.
* 읽기 [Azure 리소스 관리자 개요] [ lnk-azure-rm-overview] toolearn hello Azure 리소스 관리자의 기능에 대 한 자세한 합니다.

IoT 허브에 대 한 개발에 대 한 더 toolearn hello 다음 문서를 참조 하십시오.

* [소개 tooC SDK][lnk-c-sdk]
* [Azure IoT SDK][lnk-sdks]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

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
