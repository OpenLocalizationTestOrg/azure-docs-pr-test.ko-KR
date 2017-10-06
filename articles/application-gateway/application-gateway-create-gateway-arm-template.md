---
title: "Azure 응용 프로그램 게이트웨이-템플릿 aaaCreate | Microsoft Docs"
description: "이 페이지에서는 지침 toocreate Azure 응용 프로그램 게이트웨이 hello Azure 리소스 관리자 템플릿을 사용 하 여"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a>Hello Azure 리소스 관리자 템플릿을 사용 하 여 응용 프로그램 게이트웨이 만들기

> [!div class="op_single_selector"]
> * [Azure 포털](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure 클래식 PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager 템플릿](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

Azure Application Gateway는 계층 7 부하 분산 장치입니다. Hello 클라우드 또는 온-프레미스에 있는지 여부를 장애 조치 및 다른 서버 간에 HTTP 요청 성능 라우팅을 제공 합니다. Application Gateway는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타 여러 기능을 포함하여 다양한 ADC(Application Delivery Controller)를 제공합니다. 지원 되는 기능의 전체 목록은 toofind 방문 [응용 프로그램 게이트웨이 개요](application-gateway-introduction.md)

이 문서 다운로드 및 GitHub에서 기존 Azure 리소스 관리자 템플릿을 수정 하 고, GitHub, PowerShell 및 Azure CLI hello에서 hello 템플릿을 배포을 보여 줍니다.

Hello Azure 리소스 관리자 템플릿을 변경 하지 않고 GitHub에서 직접 단순히 배포 하는 경우 GitHub에서 toodeploy 서식 파일을 건너뜁니다.

## <a name="scenario"></a>시나리오

이 시나리오에서는

* 웹 응용 프로그램 방화벽을 사용하여 Application Gateway를 만드는 방법
* 예약된 CIDR 블록이 10.0.0.0/16이고 이름이 VirtualNetwork1인 가상 네트워크를 만듭니다.
* CIDR 블록으로 10.0.0.0/28을 사용하는 Appgatewaysubnet이라고 하는 서브넷을 만듭니다.
* Tooload hello 트래픽 분산을 원하는 hello 웹 서버에 대 한 두 개의 이전에 구성 된 백 엔드 Ip를 설정 합니다. 이 서식 파일 예제에서는 hello 백 엔드 Ip는 10.0.1.10 및 10.0.1.11 합니다.

> [!NOTE]
> 이러한 설정은이 서식 파일에 대 한 hello 매개 변수입니다. toocustomize hello 템플릿 규칙, hello 수신기, SSL 및 hello azuredeploy.json 파일에서 다른 옵션을 변경할 수 있습니다.

![시나리오](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>다운로드 하 고 hello Azure 리소스 관리자 서식 파일 이해

GitHub에서 hello 기존 Azure 리소스 관리자 템플릿 toocreate 가상 네트워크 및 서브넷 2 개를 다운로드, 변경 수도, 있으며 다시 사용할 수 있습니다. 따라서 toodo 단계를 수행 하는 hello를 사용 합니다.

1. 너무 이동[웹 응용 프로그램 방화벽이 설정 되어 있으면 응용 프로그램 게이트웨이 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf)합니다.
1. **azuredeploy.json**을 클릭하고 **RAW**를 클릭합니다.
1. 컴퓨터에 hello 파일 tooa 로컬 폴더를 저장 합니다.
1. Azure 리소스 관리자 템플릿을 익숙한 경우에 7 toostep을 건너뜁니다.
1. Hello 저장 한 파일을 열고 아래 hello 내용을 확인 **매개 변수** 줄에서
1. Azure 리소스 관리자 템플릿 매개 변수는 배포하는 동안 채울 수 있는 값에 대한 자리 표시자를 제공합니다.

  | 매개 변수 | 설명 |
  | --- | --- |
  | **subnetPrefix** |Hello 응용 프로그램 게이트웨이 서브넷에 대 한 CIDR 블록입니다. |
  | **applicationGatewaySize** | Hello 응용 프로그램 게이트웨이의 크기입니다.  WAF는 중형 및 대형만 허용합니다. |
  | **backendIpaddress1** |Hello 첫 번째 웹 서버의 IP 주소입니다. |
  | **backendIpaddress2** |Hello 두 번째 웹 서버의 IP 주소입니다. |
  | **wafEnabled** | Toodetermine WAF 사용 되는 경우 설정 합니다.|
  | **wafMode** | Hello 웹 응용 프로그램 방화벽의 모드입니다.  사용 가능한 옵션은 **방지** 또는 **검색**입니다.|
  | **wafRuleSetType** | WAF에 대한 규칙 집합 유형.  현재 OWASP hello만 지원 되는 옵션입니다. |
  | **wafRuleSetVersion** |규칙 집합 버전. OWASP CRS 2.2.9 퀵 및 3.0은 현재 지원 되는 hello 옵션입니다. |

1. Hello 내용을 확인 **리소스** 통지 hello 다음과 같은 속성 및:

   * **type**. Hello 템플릿으로 생성 되는 리소스의 형식입니다. 이 경우 hello 형식이 `Microsoft.Network/applicationGateways`, 응용 프로그램 게이트웨이 나타냅니다.
   * **이름**. Hello 리소스에 대 한 이름입니다. 공지 hello 사용 `[parameters('applicationGatewayName')]`, 해당 hello 이름이 입력으로 제공 되는 매개 변수 파일 또는가 배포 중입니다.
   * **properties**. Hello 리소스에 대 한 속성 목록입니다. 이 템플릿은 응용 프로그램 게이트웨이 만드는 동안 hello 가상 네트워크와 공용 IP 주소를 사용합니다.

   > [!NOTE]
   > 템플릿에 대한 자세한 내용은 [Resource Manager 템플릿 참조](/templates/)를 참조하세요.

1. 너무 탐색[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf)합니다.
1. **azuredeploy-parameters.json**을 클릭하고 **RAW**를 클릭합니다.
1. 컴퓨터에 hello 파일 tooa 로컬 폴더를 저장 합니다.
1. Hello 저장 한 파일을 열고 hello hello 매개 변수 값을 편집 합니다. 다음 시나리오에서 설명 하는 값 toodeploy hello 응용 프로그램 게이트웨이 hello를 사용 합니다.

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. Hello 파일을 저장 합니다. 와 같은 온라인 JSON 유효성 검사 도구를 사용 하 여 hello JSON 템플릿과 템플릿 매개 변수를 테스트할 수 있습니다 [JSlint.com](http://www.jslint.com/)합니다.

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a>PowerShell을 사용 하 여 hello Azure 리소스 관리자 템플릿을 배포합니다

Azure PowerShell을 처음 사용 하는 경우: [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 및 hello 지침 toosign Azure에 따르고 구독을 선택 합니다.

1. 로그인 tooPowerShell

    ```powershell
    Login-AzureRmAccount
    ```

1. Hello 계정에 대 한 hello 구독을 확인 합니다.

    ```powershell
    Get-AzureRmSubscription
    ```

    사용자가 입력 정보 요청된 tooauthenticate 자격 증명입니다.

1. Azure 구독 toouse 선택 합니다.

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. 필요한 경우 hello를 사용 하 여 리소스 그룹을 만들 **새로 AzureResourceGroup** cmdlet. 다음 예제는 hello, 미국 동부 위치에 AppgatewayRG 라는 리소스 그룹을 만듭니다.

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. Hello 실행 **새로 AzureRmResourceGroupDeployment** cmdlet toodeploy hello 새 가상 네트워크 hello 앞에 다운로드 하 고 수정 된 서식 파일 및 매개 변수 파일을 사용 하 여 합니다.
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 hello Azure 리소스 관리자 템플릿을 배포합니다

Azure CLI를 사용 하 여 다운로드 한 toodeploy hello Azure 리소스 관리자 템플릿을 hello 다음 단계를 수행 합니다.

1. Azure CLI 처음 사용 하는 경우 참조 [설치 하 고 Azure CLI hello 구성](/cli/azure/install-azure-cli) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.

1. 실행 hello, 필요한 경우 `az group create` 명령 toocreate hello 다음 코드 조각에에서 나와 있는 것 처럼 리소스 그룹입니다. Hello hello 명령의 출력을 확인 합니다. hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    **-n (or --name)**. Hello 새로운 리소스 그룹의 이름입니다. 이 시나리오에서는 *appgatewayRG*입니다.
    
    **-l(또는 --location)**. Azure 지역 hello 새 리소스 그룹이 생성 됩니다. 이 시나리오에서는 *westus*입니다.

1. Hello 실행 `az group deployment create` cmdlet toodeploy hello 새 가상 네트워크 hello 템플릿 및 매개 변수를 사용 하 여 파일을 다운로드 하 고 hello 앞 단계에서에서 수정할 수 있습니다. hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a>-배포를 사용 하 여 hello Azure 리소스 관리자 템플릿을 배포합니다

-배포를 Azure 리소스 관리자 템플릿을 다른 방식으로 toouse가입니다. Hello Azure 포털을 사용 하 여 쉽게 toouse 템플릿을 경우

1. 너무 이동[웹 응용 프로그램 방화벽 응용 프로그램 게이트웨이 만들기](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/)합니다.

1. 클릭 **tooAzure 배포**합니다.

    ![TooAzure 배포](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. Hello 포털에 배포 템플릿 hello에 대 한 hello 매개 변수를 입력 하 고 클릭 **확인**합니다.

    ![매개 변수](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. 선택 **toohello 약관 위에서 설명한 동의** 클릭 **구매**합니다.

1. Hello 사용자 지정 배포 블레이드에서 클릭 **만들기**합니다.

## <a name="providing-certificate-data-tooresource-manager-templates"></a>인증서 데이터 tooResource 관리자 템플릿으로 제공

템플릿을 사용 하 여 SSL을 사용 하는 경우 hello 인증서 toobe 업로드 되 고 대신 base64 문자열에 제공 되어야 합니다. tooconvert.pfx 또는.cer tooa base64 문자열 hello 다음 명령 중 하나를 사용 합니다. hello 다음 명령을 hello 인증서 tooa base64 문자열을 변환, toohello 템플릿을 제공 될 수 있는 합니다. hello 예상 출력은 변수에 저장 하 고 hello 서식 파일에 붙여넣을 수 있는 문자열입니다.

### <a name="macos"></a>macOS
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a>Windows
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a>모든 리소스 삭제

이 문서의 단계를 수행 하는 hello 중 하나를 수행 만든 모든 리소스를 toodelete:

### <a name="powershell"></a>PowerShell

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a>Azure CLI

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a>다음 단계

SSL 오프 로드 tooconfigure 방문: [SSL 오프 로드에 대 한 응용 프로그램 게이트웨이 구성](application-gateway-ssl.md)합니다.

내부 부하 분산 장치는 응용 프로그램 게이트웨이 toouse tooconfigure 방문: [내부 부하 분산 장치 (ILB) 응용 프로그램 게이트웨이 만들](application-gateway-ilb.md)합니다.

부하 분산 옵션에 대한 자세한 정보는 다음을 방문하세요.

* [Azure 부하 분산 장치](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

