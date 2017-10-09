---
title: "가상 네트워크 aaaCreate | Azure 리소스 관리자 템플릿 | Microsoft Docs"
description: "가상 a toocreate Azure 리소스 관리자 템플릿을 사용 하 여 네트워크 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿을 사용하여 가상 네트워크 만들기

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure에는 Azure Resource Manager 및 클래식이라는 두 가지 배포 모델이 있습니다. Hello 리소스 관리자 배포 모델을 통해 리소스를 만드는 것이 좋습니다. hello 읽기에 대해 더 알아봅니다 toolearn hello 두 모델 간의 차이 hello [이해 Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md) 문서.
 
이 문서에서는 Azure 리소스 관리자 템플릿을 사용 하 여 toocreate hello 리소스 관리자 배포를 통해 VNet을 모델링 하는 방법을 설명 합니다. 리소스 관리자를 통해 다른 도구를 사용 하 여 VNet을 만들 하거나 hello 다음 목록에서에서 다른 옵션을 선택 하 여 hello 클래식 배포 모델을 통해 VNet을 만들 수도 있습니다.

> [!div class="op_single_selector"]
- [포털](virtual-networks-create-vnet-arm-pportal.md)
- [PowerShell](virtual-networks-create-vnet-arm-ps.md)
- [CLI](virtual-networks-create-vnet-arm-cli.md)
- [템플릿](virtual-networks-create-vnet-arm-template-click.md)
- [포털(클래식)](virtual-networks-create-vnet-classic-pportal.md)
- [PowerShell(클래식)](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [CLI(클래식)](virtual-networks-create-vnet-classic-cli.md)

에 대해 설명 합니다 방법을 toodownload 수정 및 ARM 템플릿을 GitHub에서 기존 및 GitHub, PowerShell 및 Azure CLI hello hello 템플릿을 배포 합니다.

단순히 hello ARM 템플릿을 변경 하지 않고 GitHub에서 직접 배포 하는 경우 너무 건너뛸[github에서 서식 파일을 배포](#deploy-the-arm-template-by-using-click-to-deploy)합니다.

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>다운로드 하 고 hello Azure 리소스 관리자 서식 파일 이해
GitHub에서 VNet 및 서브넷 2 개를 만들기 위한 hello 기존 서식 파일을 다운로드, 변경 수도, 있으며 다시 사용할 수 있습니다. 따라서 toodo hello 다음 단계를 완료 합니다.

1. 너무 이동[hello 샘플 템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)합니다.
2. **azuredeploy.json**을 클릭하고 **RAW**를 클릭합니다.
3. 컴퓨터에 hello 파일 tooa 로컬 폴더를 저장 합니다.
4. 서식 파일에 익숙한 경우 7 toostep를 건너뜁니다.
5. 방금 저장 한 hello 파일을 열고 아래 hello 내용을 확인 **매개 변수** 줄 5에에서 있습니다. ARM 템플릿 매개 변수는 배포하는 동안 채울 수 있는 값에 대한 자리 표시자를 제공합니다.
   
   | 매개 변수 | 설명 |
   | --- | --- |
   | **위치** |Azure 지역 VNet hello를 만들 위치 |
   | **vnetName** |Hello에 대 한 이름을 새 VNet |
   | **addressPrefix** |주소 공간 CIDR 형식에서 VNet hello에 대 한 |
   | **subnet1Name** |이름 hello에 대 한 첫 번째 VNet |
   | **subnet1Prefix** |Hello 첫 번째 서브넷에 대 한 CIDR 블록 |
   | **subnet2Name** |Hello에 대 한 이름을 VNet의 두 번째 |
   | **subnet2Prefix** |Hello 두 번째 서브넷에 대 한 CIDR 블록 |
   
   > [!IMPORTANT]
   > GitHub에서 유지 관리되는 Azure 리소스 관리자 템플릿은 시간이 지나면서 달라질 수 있습니다. 사용 하기 전에 hello 서식 파일을 확인 하 고 있는지 확인 합니다.
   > 
   > 
6. Hello 내용을 확인 **리소스** hello 다음을 확인 합니다.
   
   * **type**. Hello 템플릿으로 생성 되는 리소스의 형식입니다. 이 경우 VNet를 나타내는 **Microsoft.Network/virtualNetworks**입니다.
   * **이름**. Hello 리소스에 대 한 이름입니다. 공지 hello 사용 **[parameters('vnetName')]**, 어떤 의미 hello hello 사용자 또는 매개 변수 파일에서 배포 중 입력으로 제공 하는 이름이 됩니다.
   * **properties**. Hello 리소스에 대 한 속성 목록입니다. 이 템플릿은 VNet 만드는 동안 hello 주소 공간 및 서브넷 속성을 사용합니다.
7. 너무 탐색[hello 샘플 템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)합니다.
8. **azuredeploy-paremeters.json**을 클릭하고 **RAW**를 클릭합니다.
9. 컴퓨터에 hello 파일 tooa 로컬 폴더를 저장 합니다.
10. 방금 저장 한 hello 파일을 열고 hello hello 매개 변수 값을 편집 합니다. 다음 toodeploy hello hello 시나리오에 설명 된 VNet 아래의 값에는 hello를 사용 합니다.

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. Hello 파일을 저장 합니다.


## <a name="deploy-hello-template-using-powershell"></a>PowerShell을 사용 하 여 hello 템플릿을 배포합니다

다음 PowerShell을 사용 하 여 다운로드 한 단계 toodeploy hello 템플릿을 hello를 완료 합니다.

1. PowerShell 설치 및 구성 Azure hello의 hello 단계를 완료 하 여 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) 문서.
2. 다음 명령은 toocreate hello 새 리소스 그룹을 실행 합니다.

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    hello 명령은 명명 된 리소스 그룹을 만듭니다 *TestRG* hello에 *중미* azure 지역입니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.

    예상 출력:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. 다음 명령을 toodeploy hello hello 템플릿 및 매개 변수 파일 다운로드 하 고 위에서 수정를 사용 하 여 새 VNet hello를 실행 합니다.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    예상 출력:
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. 실행된 hello 다음 명령은 hello의 tooview hello 속성 새 VNet:

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    예상 출력:

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a>-배포를 사용 하 여 hello 템플릿을 배포합니다

Microsoft 및 열기 toohello 커뮤니티에서 유지 관리 미리 정의 된 Azure 리소스 관리자 템플릿 업로드 tooa GitHub 리포지토리를 다시 사용할 수 있습니다. 이러한 템플릿은 GitHub에서 배포할 수 있습니다 또는 다운로드 하 고 수정 toofit 요구 사항. toodeploy 템플릿으로 두 서브넷으로 VNet을 만드는 단계를 수행 하는 전체 hello:

1. 브라우저에서 탐색 너무[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates)합니다.
2. 템플릿 hello 목록 아래로 스크롤하여 클릭 **101 vnet-2 서브넷**합니다. Hello 확인 **README.md** 파일을 다음과 같이 합니다.

    ![Github의 READEME.md 파일](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. 클릭 **tooAzure 배포**합니다. 필요한 경우 Azure 로그인 자격 증명을 입력합니다. 
4. Hello에 **매개 변수** 블레이드에서 hello 값 toouse toocreate 새 VNet을 클릭 한 다음 입력 **확인**합니다. hello 다음 그림과 hello 시나리오에 대 한 hello 값:
   
    ![ARM 템플릿 매개 변수](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. 클릭 **리소스 그룹** 선택한 리소스 그룹 tooadd hello VNet, 하거나 클릭 **새로 만들기** tooadd hello VNet tooa 새 리소스 그룹입니다. hello 다음 그림은 hello 리소스 이라는 새 리소스 그룹에 대 한 그룹 설정을 **TestRG**:

    ![리소스 그룹](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. 필요한 경우 변경할 hello **구독** 및 **위치** VNet에 대 한 설정입니다.
7. Hello의 타일로 toosee hello VNet를 하지 않으려면 **시작 보드**, 사용 하지 않도록 설정 **Pin tooStartboard**합니다.
8. 클릭 **약관**hello 조건을 읽고 클릭 **구입** tooagree 합니다. 
9. 클릭 **만들기** toocreate hello VNet입니다.
   
    ![Preview 포털에서 배포 타일 제출](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. Hello 배포 완료 되 면 hello Azure 포털에서 **더 많은 서비스**, 형식 *가상 네트워크* hello 필터 상자가 표시 되 면 가상 네트워크 toosee hello 가상 네트워크 블레이드 클릭 합니다. Hello 블레이드에서 클릭 *TestVNet*합니다. Hello에 *TestVNet* 블레이드에서 클릭 **서브넷** hello 다음 그림에에서 나와 있는 것 처럼 toosee 만든 hello 서브넷:
    
     ![Preview 포털에서 VNet 만들기](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a>다음 단계

자세한 내용은 방법 tooconnect:

- 읽는 hello 여 가상 컴퓨터 (VM) tooa 가상 네트워크 [Windows VM을 만들](../virtual-machines/virtual-machines-windows-hero-tutorial.md) 또는 [Linux VM을 만들](../virtual-machines/linux/quick-create-portal.md) 문서입니다. Hello 아티클의 hello 단계에서 VNet 및 서브넷을 만드는 대신 및 선택할 수 있습니다는 기존 VNet 서브넷 tooconnect VM을 합니다.
- hello를 참조 하 여 가상 네트워크 tooother 가상 네트워크를 hello [Vnet 연결](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) 문서.
- 가상 네트워크 tooan hello 온-프레미스 사이트 간 가상 사설망 (VPN) 또는 express 경로 회로 사용 하 여 네트워크. 자세한 방법은 hello [사이트 간 VPN을 사용 하 여 VNet tooan 온-프레미스 네트워크 연결](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) 및 [VNet tooan ExpressRoute 회로 연결](../expressroute/expressroute-howto-linkvnet-arm.md) 문서입니다.
