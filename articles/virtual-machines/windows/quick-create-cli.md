---
title: "Azure 빠른 시작 - Windows VM 만들기 CLI | Microsoft Docs"
description: "Azure CLI를 사용하여 Windows 가상 컴퓨터를 만드는 방법을 빠르게 이해합니다."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5939af4cf071664415d57ccbaee3413d61aa69e9
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-cli"></a>Azure CLI를 사용하여 Windows 가상 컴퓨터 만들기

명령줄 또는 스크립트에서 Azure 리소스를 만들고 관리하는 데 Azure CLI가 사용됩니다. 이 가이드에서는 Azure CLI를 사용하여 Windows Server 2016이 실행되는 가상 컴퓨터를 배포하는 방법을 자세히 설명합니다. 배포가 완료되면 서버에 연결하고 IIS를 설치합니다.

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 빠른 시작에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다. `az --version`을 실행하여 버전을 찾습니다. 설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요. 


## <a name="create-a-resource-group"></a>리소스 그룹 만들기

[az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기

[az vm create](/cli/azure/vm#az_vm_create)로 VM을 만듭니다. 

다음 예제에서는 *myVM*이라는 VM을 만듭니다. 이 예제에서는 관리 사용자 이름으로 *azureuser*를 사용하고 암호로 *myPassword12*를 사용합니다. 이러한 값을 사용자 환경에 적절한 값으로 업데이트합니다. 가상 컴퓨터와의 연결을 만들 때 이러한 값이 필요합니다.

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

VM을 만든 경우 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다. `publicIpAaddress`을 기록해 둡니다. 이 주소는 VM에 액세스하는 데 사용됩니다.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>웹 트래픽에 대해 포트 80 열기 

기본적으로 Azure에 배포된 Windows 가상 컴퓨터에는 RDP 연결만이 가능합니다. 이 VM이 웹 서버가 되는 경우 인터넷에서 포트 80을 열어야 합니다. [az vm open-port](/cli/azure/vm#open-port) 명령을 사용하여 원하는 포트를 엽니다.  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-to-virtual-machine"></a>가상 컴퓨터에 연결

다음 명령을 사용하여 가상 컴퓨터와의 원격 데스크톱 세션을 만듭니다. 해당 IP 주소를 가상 컴퓨터의 공용 IP 주소로 바꿉니다. 가상 컴퓨터를 만들 때 사용되는 자격 증명을 묻는 메시지가 표시되면 입력합니다.

```bash 
mstsc /v:Public IP Address
```

## <a name="install-iis-using-powershell"></a>PowerShell을 사용하여 IIS 설치

이제 Azure VM에 로그인했으므로 IIS를 설치하고 웹 트래픽을 허용하는 로컬 방화벽 규칙을 사용하려면 PowerShell의 단일 줄을 사용할 수 있습니다. PowerShell 프롬프트를 열고 다음 명령을 실행합니다.

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a>IIS 시작 페이지 보기

IIS를 설치하고 현재 포트 80이 인터넷에서 VM에 열려 있으면 사용자가 선택한 웹 브라우저를 사용하여 기본 IIS 시작 페이지를 볼 수 있습니다. 위에 설명한 공용 IP 주소를 사용하여 기본 페이지를 방문해야 합니다. 

![IIS 기본 사이트](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>리소스 정리

더 이상 필요하지 않은 경우 [az group delete](/cli/azure/group#delete) 명령을 사용하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 간단한 가상 컴퓨터, 네트워크 보안 그룹 규칙을 배포했으며 웹 서버를 설치했습니다. Azure 가상 컴퓨터에 대한 자세한 내용을 알아보려면 Windows VM의 자습서를 계속 진행합니다.

> [!div class="nextstepaction"]
> [Azure Windows 가상 컴퓨터 자습서](./tutorial-manage-vm.md)
