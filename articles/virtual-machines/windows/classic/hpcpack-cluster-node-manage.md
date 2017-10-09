---
title: "aaaManage HPC Pack 클러스터 계산 노드 | Microsoft Docs"
description: "PowerShell 스크립트 도구 tooadd, 제거, 시작을 확인 하 고 Azure의 HPC Pack 2012 R2 클러스터 계산 노드를 중지 합니다."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Hello 번호와 Azure에서 HPC Pack 클러스터에서 계산 노드의 가용성 관리
Azure Vm에서 HPC Pack 2012 R2 클러스터를 만든 경우 tooeasily 추가, 제거, 시작 (프로 비전), 또는 중지 (프로 비전 해제) 몇 가지 방법으로 클러스터의 노드 Vm을 계산 하는 것이 좋습니다. toodo 이러한 작업을 hello 헤드 노드 VM에 설치 된 Azure PowerShell 스크립트를 실행 합니다. 이러한 스크립트 도움말 비용을 제어할 수 있도록 hello 번호 및 HPC 팩 클러스터 리소스의 가용성을 제어 합니다.

> [!IMPORTANT] 
> 이 문서에는 hello 클래식 배포 모델을 사용 하 여 만든 azure에서 Pack 2012 R2 클러스터만 tooHPC 적용 됩니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.
> 또한이 문서에서 설명 하는 hello PowerShell 스크립트 HPC 팩 2016에서 사용할 수 없는 합니다.

## <a name="prerequisites"></a>필수 조건
* **Azure Vm에서 HPC Pack 2012 R2 클러스터**: hello 클래식 배포 모델에는 HPC Pack 2012 R2 클러스터를 만듭니다. 예를 들어 hello Azure Marketplace에서에서 hello HPC Pack 2012 R2 VM 이미지와 Azure PowerShell 스크립트를 사용 하 여 hello 배포를 자동화할 수 있습니다. 정보 및 필수 구성 요소에 대 한 참조 [hello HPC Pack IaaS 배포 스크립트는 HPC 클러스터 만들기](hpcpack-cluster-powershell-script.md)합니다.
  
    배포 후 hello 노드 관리 스크립트에서에서 찾기 hello %CCP\_홈 hello 헤드 노드의 %bin 폴더입니다. 관리자 권한으로 각각 hello 스크립트를 실행 합니다.
* **Azure 게시 설정 파일 또는 관리 인증서**: hello 헤드 노드에서 toodo hello 다음 중 하나를 해야 합니다.
  
  * **가져오기 hello Azure 게시 설정 파일**합니다. toodo hello 헤드 노드에 Azure PowerShell cmdlet을 다음이 실행된 hello:
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * **헤드 노드에 hello hello Azure 관리 인증서를 구성**합니다. Hello.cer 파일이 있으면 hello CurrentUser\My 인증서 저장소에 가져온 후 hello Azure PowerShell cmdlet (azure 클라우드 또는 AzureChinaCloud) Azure 환경에 대 한 다음를 실행 합니다.
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a>계산 노드 VM 추가
Hello로 계산 노드를 추가 **Add-hpciaasnode.ps1** 스크립트입니다.

### <a name="syntax"></a>구문
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a>매개 변수
* **ServiceName**: hello 새 계산 노드 Vm 클라우드 서비스의 이름에 추가 됩니다.
* **ImageName**: hello Azure 클래식 포털 또는 Azure PowerShell cmdlet을 통해 가져올 수 있는 Azure VM 이미지 이름을 **Get-azurevmimage**합니다. hello 이미지 hello 요구 사항을 준수를 충족 해야 합니다.
  
  1. Windows 운영 체제를 설치해야 합니다.
  2. HPC Pack hello 계산 노드 역할에 설치 되어야 합니다.
  3. hello 이미지가 공용 Azure VM 이미지가 하지 hello 사용자 범주의 개인 이미지 여야 합니다.
* **수량**: 계산 노드 Vm toobe 추가할 수 있습니다.
* **InstanceSize**: 계산 노드 Vm hello의 크기입니다.
* **DomainUserName**: 사용 되는 toojoin hello 새 Vm toohello 도메인은 도메인 사용자 이름입니다.
* **DomainUserPassword**: hello 도메인 사용자의 암호입니다.
* **NodeNameSeries** (선택 사항): 노드 이름 지정 패턴 hello에 대 한 계산 합니다. hello 형식 이어야 &lt; *루트\_이름*&gt;&lt;*시작\_번호*&gt;%입니다. 예를 들어 MyCN %10% 의미는 일련의 hello MyCN11에서 시작 하는 노드 이름을 계산 합니다. 지정 하지 않으면 hello 스크립트 사용 하 여 hello hello HPC 클러스터에서 노드 명명 시리즈를 구성 합니다.

### <a name="example"></a>예제
hello 다음 예제에서는 추가 20 크기가 대형 인 계산 노드 Vm 클라우드 서비스의 hello *hpcservice1*hello VM 이미지에 따라 *hpccnimage1*합니다.

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a>계산 노드 VM 제거
Hello로 계산 노드 제거 **Remove-hpciaasnode.ps1** 스크립트입니다.

### <a name="syntax"></a>구문
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a>매개 변수
* **이름**: 클러스터 노드 toobe의 이름을 제거 합니다. 와일드카드가 지원됩니다. hello 매개 변수 집합 이름은 Name가입니다. 두 hello를 지정할 수 없습니다 **이름** 및 **노드** 매개 변수입니다.
* **노드**: hello HPC PowerShell cmdlet을 통해 가져올 수 있는 hello HpcNode 개체를 제거 하는 hello 노드 toobe [Get-hpcnode](https://technet.microsoft.com/library/dn887927.aspx)합니다. hello 매개 변수 집합 이름은 Node입니다. 두 hello를 지정할 수 없습니다 **이름** 및 **노드** 매개 변수입니다.
* **DeleteVHD** (선택 사항): toodelete hello 제거 된 Vm에 대 한 hello 연결 된 디스크를 설정 합니다.
* **Force** (선택 사항): 제거 하기 전에 tooforce HPC 노드를 오프 라인으로 설정 합니다.
* **확인** (선택 사항): 확인 hello 명령을 실행 하기 전에 확인 합니다.
* **WhatIf**: toodescribe 어떤 설정 했을 때 hello 명령을 실제로 실행 하지 않고도 hello 명령을 실행 합니다.

### <a name="example"></a>예제
hello 다음 예제에서는 오프 라인 hello 노드를 강제 시작 하는 이름을 *HPCNode-CN-* hello 노드와 연결 된 디스크를 제거 하 고 있습니다.

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a>계산 노드 VM 시작
시작 하는 계산 노드 hello로 **Start-hpciaasnode.ps1** 스크립트입니다.

### <a name="syntax"></a>구문
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a>매개 변수
* **이름**: hello 클러스터 노드 toobe 형태의 시작 합니다. 와일드카드가 지원됩니다. hello 매개 변수 집합 이름은 Name가입니다. 두 hello를 지정할 수 없습니다 **이름** 및 **노드** 매개 변수입니다.
* **노드**-hello HPC PowerShell cmdlet을 통해 가져올 수 있는 hello HpcNode 개체를 시작 하는 hello 노드 toobe [Get-hpcnode](https://technet.microsoft.com/library/dn887927.aspx)합니다. hello 매개 변수 집합 이름은 Node입니다. 두 hello를 지정할 수 없습니다 **이름** 및 **노드** 매개 변수입니다.

### <a name="example"></a>예제
hello 다음 예제에서는 시작 노드 이름이 시작 *HPCNode-CN-*합니다.

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a>계산 노드 VM 중지
Hello로 계산 노드 중지 **중지 HpcIaaSNode.ps1** 스크립트입니다.

### <a name="syntax"></a>구문
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a>매개 변수
* **이름**-hello 클러스터 노드 toobe 형태의 중지 되었습니다. 와일드카드가 지원됩니다. hello 매개 변수 집합 이름은 Name가입니다. 두 hello를 지정할 수 없습니다 **이름** 및 **노드** 매개 변수입니다.
* **노드**: hello HPC PowerShell cmdlet을 통해 가져올 수 있는 hello HpcNode 개체를 중지 하는 hello 노드 toobe [Get-hpcnode](https://technet.microsoft.com/library/dn887927.aspx)합니다. hello 매개 변수 집합 이름은 Node입니다. 두 hello를 지정할 수 없습니다 **이름** 및 **노드** 매개 변수입니다.
* **Force** (선택 사항): 중지 하기 전에 tooforce HPC 노드를 오프 라인으로 설정 합니다.

### <a name="example"></a>예제
hello 다음 예제에서는 오프 라인 노드를 강제 시작 하는 이름을 *HPCNode-CN-* 다음 중지 hello 노드 및 합니다.

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a>다음 단계
* 증가 또는 hello 작업 및 hello 클러스터에서 작업의 현재 작업량에 따라 hello 클러스터 노드를 축소, 참조 tooautomatically [자동으로 리소스 확장 및 축소 hello HPC Pack 클러스터에서 Azure에 따라 toohello 클러스터 작업](hpcpack-cluster-node-autogrowshrink.md).

