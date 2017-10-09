---
title: "빠른 시작-aaaAzure Windows VM CLI 만들기 | Microsoft Docs"
description: "신속 하 게 toocreate hello Azure CLI 사용 하 여 Windows 가상 컴퓨터를 알아봅니다."
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
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a>Hello Azure CLI로 Windows 가상 컴퓨터 만들기

hello Azure CLI 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다. Windows Server 2016을 실행 하는 가상 컴퓨터 Azure CLI toodeploy hello를 사용 하 여이 가이드 정보입니다. 배포가 완료 되 면 toohello 서버 연결 고 IIS를 설치 했습니다.

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

이 퀵 스타트의 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 필요 tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여 이후 버전입니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 


## <a name="create-a-resource-group"></a>리소스 그룹 만들기

[az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치 합니다.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기

[az vm create](/cli/azure/vm#create)로 VM을 만듭니다. 

hello 다음 예제에서는 V *myVM*합니다. 이 예에서는 *azureuser* 관리 사용자 이름에 대 한 및 *myPassword12* hello 암호와 합니다. 이러한 값 toosomething 적절 한 tooyour 환경을 업데이트 합니다. Hello 가상 컴퓨터와 연결을 만들 때 이러한 값이 필요 합니다.

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

Hello VM을 만든 hello Azure CLI 정보 비슷한 toohello 다음 예제에 표시 됩니다. Hello를 메모해 `publicIpAaddress`합니다. 이 주소는 사용 되는 tooaccess hello VM입니다.

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

기본적으로 Azure에 배포 된 tooWindows 가상 컴퓨터에서 RDP 연결만 허용 됩니다. 이 VM은 toobe 웹 서버에서 한 걸음 경우 hello 인터넷에서에서 tooopen 포트 80 해야 합니다. 사용 하 여 hello [az vm-포트를 열](/cli/azure/vm#open-port) 명령 tooopen hello 원하는 포트입니다.  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a>Toovirtual 컴퓨터 연결

사용 하 여 hello 다음 명령은 toocreate hello 가상 컴퓨터와 원격 데스크톱 세션입니다. 가상 컴퓨터의 공용 IP 주소 hello와 hello IP 주소를 대체 합니다. 메시지가 표시 되 면 hello 가상 컴퓨터를 만들 때 사용 하는 hello 자격 증명을 입력 합니다.

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a>PowerShell을 사용하여 IIS 설치

를 toohello Azure VM에에서 로그인 한 했으므로 PowerShell tooinstall IIS 전혀 사용할 수 있으며 hello 로컬 방화벽 규칙 tooallow 웹 트래픽을 사용 하도록 설정. PowerShell 프롬프트를 열고 hello 다음 명령을 실행 합니다.

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>보기 hello IIS 시작 페이지

IIS가 설치 및 포트 80이 hello 인터넷에서에서 VM에 이제 열려 choice tooview hello 기본 IIS 시작 페이지의 웹 브라우저를 사용할 수 있습니다. 있는지 toouse hello 공용 IP 주소 toovisit hello 기본 페이지 위에 설명한 수 있습니다. 

![IIS 기본 사이트](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>리소스 정리

더 이상 필요 hello를 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 명령입니다.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 간단한 가상 컴퓨터, 네트워크 보안 그룹 규칙을 배포했으며 웹 서버를 설치했습니다. Azure 가상 컴퓨터에 대해 자세히 toolearn Windows vm의 toohello 자습서를 계속 합니다.

> [!div class="nextstepaction"]
> [Azure Windows 가상 컴퓨터 자습서](./tutorial-manage-vm.md)
