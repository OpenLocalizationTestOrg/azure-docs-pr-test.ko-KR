---
title: "Linux 용 Azure 가상 컴퓨터 확장 aaaOMS | Microsoft Docs"
description: "가상 컴퓨터 확장을 사용 하 여 Linux 가상 컴퓨터에 hello OMS 에이전트를 배포 합니다."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a>Linux용 OMS 가상 컴퓨터 확장

## <a name="overview"></a>개요

OMS(Operations Management Suite)는 클라우드와 온-프레미스 자산에서 모니터링, 경고 및 경고 수정 기능을 제공합니다. Linux 용 OMS 에이전트 가상 컴퓨터 확장 hello 게시 되 고 Microsoft에서 지원 됩니다. Azure 가상 컴퓨터에 hello OMS 에이전트를 설치 하 고 기존 OMS 작업 영역에 가상 컴퓨터를 등록 하는 hello 확장 합니다. 이 문서 정보 hello Linux 용 OMS 가상 컴퓨터 확장 hello에 대 한 플랫폼, 구성 및 배포 옵션을 지원 합니다.

## <a name="prerequisites"></a>필수 조건

### <a name="operating-system"></a>운영 체제

OMS 에이전트 확장 hello 이러한 Linux 배포에 대해 실행할 수 있습니다.

| 배포 | 버전 |
|---|---|
| CentOS Linux | 5, 6 및 7 |
| Oracle Linux | 5, 6 및 7 |
| Red Hat Enterprise Linux Server | 5, 6 및 7 |
| Debian GNU/Linux | 6, 7 및 8 |
| Ubuntu | 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS |
| SUSE Linux Enterprise Server | 11 및 12 |

### <a name="internet-connectivity"></a>인터넷 연결

Linux 용 OMS 에이전트 확장 hello hello 대상 가상 컴퓨터는 연결 된 toohello 필요 인터넷 합니다. 

## <a name="extension-schema"></a>확장 스키마

hello 다음 JSON 스키마를 보여 줍니다 hello hello OMS 에이전트 확장에 대 한 합니다. hello 확장 hello 대상 OMS 작업 영역;에서 hello 작업 영역 ID와 작업 영역 키 필요 hello OMS 포털에서 이러한 값을 찾을 수 있습니다. 중요 한 데이터로 처리 되어야 hello 작업 영역 키를 보호 설정 구성에 저장 되어야 합니다. Azure VM 확장으로 보호 된 데이터를 설정 하는 암호화 되 고 hello 대상 가상 컴퓨터에 암호를 해독할 됩니다. **workspaceId** 및 **workspaceKey**는 대/소문자를 구분합니다.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a>속성 값

| 이름 | 값/예제 |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.EnterpriseCloud.Monitoring |
| type | OmsAgentForLinux |
| typeHandlerVersion | 1.4 |
| workspaceId(예) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey(예) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ== |


## <a name="template-deployment"></a>템플릿 배포

Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다. 서식 파일은 온 보 딩 tooOMS 같은 구성 된 후 배포 해야 하는 하나 이상의 가상 컴퓨터를 배포 하는 경우에 적합 합니다. Hello에 hello OMS 에이전트 VM 확장을 포함 하는 샘플 리소스 관리자 템플릿이 있습니다 [Azure 빠른 시작 갤러리](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm)합니다. 

가상 컴퓨터 확장에 대 한 hello JSON 구성 hello 가상 컴퓨터 리소스 내에 중첩 된 또는 hello 루트 또는 리소스 관리자 JSON 서식 파일의 최상위 수준에 배치할 수 있습니다. hello JSON 구성의 배치 hello hello 리소스 이름 및 형식을의 hello 값을 영향을 줍니다. 자세한 내용은 [자식 리소스의 이름 및 형식 설정](../../azure-resource-manager/resource-manager-template-child-resource.md)을 참조하세요. 

hello 다음 예에서는 가정 hello OMS 확장 hello 가상 컴퓨터 리소스 내에 중첩 됩니다. Hello JSON hello에 위치한 hello 확장을 리소스를 중첩할 때 `"resources": []` hello 가상 컴퓨터의 개체입니다.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

Hello 서식 파일의 루트 hello에 hello 확장 JSON를 배치할 때 참조 toohello 부모 가상 컴퓨터를 포함 하는 hello 리소스 이름 및 hello 유형은 hello 중첩 된 구성에 반영 합니다.  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a>Azure CLI 배포

hello Azure CLI 사용된 toodeploy hello OMS 에이전트 VM 확장 tooan 기존 가상 컴퓨터를 수 있습니다. OMS 작업 영역에서 설정과 hello OMS 키와 OMS ID를 대체 합니다. 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a>문제 해결 및 지원

### <a name="troubleshoot"></a>문제 해결

Hello Azure 포털에서에서 하 고 hello Azure CLI를 사용 하 여 확장 배포의 hello 상태에 대 한 데이터를 검색할 수 있습니다. hello 명령을 사용 하 여 다음을 실행 하는 특정된 VM에 대 한 확장의 toosee hello 배포 상태 hello Azure CLI 합니다.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

확장 실행은 기록된 toohello 다음 파일을 출력 합니다.

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a>오류 코드 및 해당 의미

| 오류 코드 | 의미 | 가능한 작업 |
| :---: | --- | --- |
| 10 | VM이 이미 연결 된 tooan OMS 작업 영역 | tooconnect hello VM toohello 작업 영역 hello 확장 스키마에 지정 된 stopOnMultipleConnections toofalse 공용 설정에서 설정 하거나이 속성을 제거 합니다. 이 VM은 연결된 각 작업 영역에 대해 한 번만 비용이 청구됩니다. |
| 11 | 제공 된 잘못 된 구성 toohello 확장 | Hello 앞 예제 tooset 배포에 필요한 모든 속성 값을 따릅니다. |
| 12 | hello dpkg 패키지 관리자 잠겨 있습니다. | 모든 dpkg 업데이트 작업이 hello 컴퓨터에서 완료 하 고 다시 시도 있는지 확인 하십시오. |
| 20 | 조기 호출 사용 설정 | [Azure Linux 에이전트 업데이트 hello](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello 사용 가능한 최신 버전입니다. |
| 51 | 이 확장 hello VM의 운영 체제에서 지원 되지 않습니다. | |
| 55 | Toohello Microsoft Operations Management Suite 서비스에 연결할 수 없음 | 인터넷 액세스 또는 올바른 HTTP 프록시가 제공 된다는 것 hello 시스템 중 하나에 있는지 확인 합니다. 또한 hello 작업 영역 ID의 hello 정확성을 확인 |

Hello에서 추가 문제 해결 정보를 확인할 수 있습니다 [Linux에 대 한 OMS 에이전트 문제 해결 가이드](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#)합니다.

### <a name="support"></a>지원

이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다 Azure 전문가의 hello hello [MSDN Azure 및 스택 오버플로 포럼](https://azure.microsoft.com/en-us/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/) 지원 받기를 선택 합니다. Azure 지원을 사용 하는 방법에 대 한 내용은 하세요 hello [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)합니다.
