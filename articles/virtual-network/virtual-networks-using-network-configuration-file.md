---
title: "Azure 가상 네트워크 (클래식)-네트워크 구성 파일 aaaConfigure | Microsoft Docs"
description: "자세한 내용은 어떻게 toocreate 및 내보내기, 변경 및 네트워크 구성 파일을 가져오는 하 여 가상 네트워크 (클래식)를 수정 합니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a>네트워크 구성 파일을 사용하여 가상 네트워크(클래식) 구성
> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 배포 모델을 사용 하는 것이 좋습니다.

수 만들고 hello Azure CLI (명령줄 인터페이스) 1.0 또는 Azure PowerShell을 사용 하 여 네트워크 구성 파일을 통한 가상 네트워크 (클래식)를 구성 합니다. 네트워크 구성 파일을 사용 하 여 hello Azure 리소스 관리자 배포 모델을 통해 가상 네트워크를 수정 하거나 만들 수 없습니다. Azure 포털 toocreate hello를 사용 하 여 또는 네트워크 구성 파일을 사용 하 여 가상 네트워크 (클래식)를 수정 하, 사용할 수 있지만 Azure 포털 toocreate 네트워크 구성 파일을 사용 하지 않고 가상 네트워크 (클래식) hello 수 없습니다.

만들기 및 네트워크 구성 파일을 사용 하 여 가상 네트워크 (클래식)를 구성 내보내기, 변경 및 hello 파일을 가져오는 필요 합니다.

## <a name="export"></a>네트워크 구성 파일 내보내기

PowerShell 또는 hello Azure CLI tooexport 네트워크 구성 파일을 사용할 수 있습니다. PowerShell은 Azure CLI hello json 파일을 내보내는 동안 XML 파일로를 내보냅니다.

### <a name="powershell"></a>PowerShell
 
1. [Azure PowerShell을 설치 하 고 tooAzure 로그인](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
2. Hello 디렉터리 변경 (및 존재 확인) 및 파일 이름을 hello에 다음 명령을 실행 후 원하는 hello 명령 tooexport hello 네트워크 구성 파일로:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Azure CLI 1.0

1. [Hello Azure CLI 1.0 설치](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 남은 Azure CLI 1.0 명령 프롬프트에서 단계를 완료 합니다.
2. TooAzure hello를 입력 하 여 로그인 `azure login` 명령입니다.
3. Hello를 입력 하 여 asm 모드에 있는 확인 `azure config mode asm` 명령입니다.
4. Hello 디렉터리 변경 (및 존재 확인) 및 파일 이름을 hello에 다음 명령을 실행 후 원하는 hello 명령 tooexport hello 네트워크 구성 파일로:
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a>네트워크 구성 파일 만들기 또는 수정

네트워크 구성 파일 (PowerShell 사용) 하는 경우 XML 파일 또는 json 파일 (경우 hello Azure CLI를 사용 하 여). 모든 텍스트 또는 XML/json 편집기 hello 파일을 편집할 수 있습니다. hello [네트워크 구성 파일 스키마 설정](https://msdn.microsoft.com/library/azure/jj157100.aspx) 아티클은 모든 설정에 대 한 세부 정보를 포함 합니다. Hello 설정의 추가 설명을 참조 하십시오. [가상 네트워크와 설정을 보려면](virtual-network-manage-network.md#view-vnet)합니다. hello 변경 toohello 파일:

- 맞아야 hello 스키마 또는 가져오기 hello 네트워크 구성 파일 실행 되지 않습니다.
- 구독에 대한 모든 기존 네트워크 설정을 덮어쓰므로 수정할 때는 특히 주의하세요. 예를 들어 hello 예제 네트워크 구성 파일에 나오는 참조 합니다. Hello 원본 파일에 포함 된 두 개의 예를 들어 **VirtualNetworkSite** 인스턴스, 그리고 하는 hello 예제에 나와 있는 것 처럼, 하 게 변경 합니다. Azure hello hello에 대 한 가상 네트워크 삭제 hello 파일을 가져올 때 **VirtualNetworkSite** 인스턴스 hello 파일에서 제거 합니다. 이 간단한 시나리오에서는 리소스가 없는 hello 가상 네트워크에 있던 가정 했습니다 마치 hello 가상 네트워크를 삭제할 수 없습니다, 그리고 및 hello 가져오기 실패 합니다.

> [!IMPORTANT]
> Azure 고려 하는 서브넷으로 tooit 배포 **사용에서**합니다. 사용 중인 서브넷은 수정할 수 없습니다. 네트워크 구성 파일에서 서브넷 정보를 수정 하기 전에 아무 것도 수정 하 고 있지 않습니다 toohello 서브넷 tooa 다른 서브넷 배포를 이동 합니다. 참조 [VM 또는 역할 인스턴스 tooa 다른 서브넷 이동](virtual-networks-move-vm-role-to-subnet.md) 대 한 자세한 내용은 합니다.

### <a name="example-xml-for-use-with-powershell"></a>PowerShell과 함께 사용할 XML 예제

hello 다음 네트워크 구성 파일 예에서는 가상 네트워크를 만들어 명명 된 *myVirtualNetwork* 의 주소 공간과 *10.0.0.0/16* hello에 *미국 동부* Azure 지역입니다. 라는 하나의 서브넷을 포함 하는 가상 네트워크 hello *mySubnet* 의 주소 접두사가 *10.0.0.0/24*합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

내보낸 hello 네트워크 구성 파일의 내용이 들어 있을 경우 수 복사 hello XML hello 이전 예에서 하 새 파일에 붙여 넣습니다.

### <a name="example-json-for-use-with-hello-azure-cli-10"></a>예제 JSON hello Azure CLI 1.0로 사용 하기 위해

hello 다음 네트워크 구성 파일 예에서는 가상 네트워크를 만들어 명명 된 *myVirtualNetwork* 의 주소 공간과 *10.0.0.0/16* hello에 *미국 동부* Azure 지역입니다. 라는 하나의 서브넷을 포함 하는 가상 네트워크 hello *mySubnet* 의 주소 접두사가 *10.0.0.0/24*합니다.

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

내보낸 hello 네트워크 구성 파일의 내용이 들어 있을 경우 수 복사 hello json hello 이전 예에서 하 새 파일에 붙여 넣습니다.

## <a name="import"></a>네트워크 구성 파일 가져오기

PowerShell 또는 hello Azure CLI tooimport 네트워크 구성 파일을 사용할 수 있습니다. PowerShell은 Azure CLI hello json 파일을 가져오는 동안 XML 파일을 가져옵니다. Hello 가져오기에 실패 하면 해당 hello 파일 hello 준수 확인 [네트워크 구성 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)합니다. 

### <a name="powershell"></a>PowerShell
 
1. [Azure PowerShell을 설치 하 고 tooAzure 로그인](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
2. Hello 디렉터리와 파일 이름을 다음 필요에 따라 명령을 hello 변경한 하십시오 hello 명령 tooimport hello 네트워크 구성 파일을 실행 합니다.
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Azure CLI 1.0

1. [Hello Azure CLI 1.0 설치](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 남은 Azure CLI 1.0 명령 프롬프트에서 단계를 완료 합니다.
2. TooAzure hello를 입력 하 여 로그인 `azure login` 명령입니다.
3. Hello를 입력 하 여 asm 모드에 있는 확인 `azure config mode asm` 명령입니다.
4. Hello 디렉터리와 파일 이름을 다음 필요에 따라 명령을 hello 변경한 하십시오 hello 명령 tooimport hello 네트워크 구성 파일을 실행 합니다.

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
