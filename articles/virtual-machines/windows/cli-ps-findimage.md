---
title: "Azure에서 이미지를 Windows VM aaaSelect | Microsoft Docs"
description: "게시자, 제품, SKU 및 마켓플레이스 VM 이미지에 대 한 버전 toouse Azure PowerSHell toodetermine hello 하는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a>Windows VM toofind hello Azure PowerShell을 사용한 Azure 마켓플레이스 이미지 방법

이 항목에서는 toouse Azure PowerShell toofind VM hello Azure 마켓플레이스 이미지 하는 방법을 설명 합니다. Windows VM을 만들 때이 정보 toospecify 마켓플레이스 이미지를 사용 합니다.

설치 하 고 최신 hello 구성 되었는지 확인 [Azure PowerShell 모듈](/powershell/azure/install-azurerm-ps)합니다.



## <a name="table-of-commonly-used-windows-images"></a>일반적으로 사용하는 Windows 이미지 테이블
| PublisherName | 제안 | SKU |
|:--- |:--- |:--- |:--- |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter-Server-Core |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter-with-Containers |
| MicrosoftWindowsServer |WindowsServer |2016-Nano-Server |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2008-R2-SP1 |
| MicrosoftDynamicsNAV |DynamicsNAV |2017 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2016 |
| MicrosoftSQLServer |SQL2016-WS2016 |Enterprise |
| MicrosoftSQLServer |SQL2014SP2-WS2012R2 |Enterprise |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |

## <a name="find-specific-images"></a>특정 이미지 찾기


새 가상 컴퓨터를 Azure 리소스 관리자를 만들 때 일부 경우에 필요 toospecify 이미지를 다음과 같은 이미지 속성 hello hello 결합 합니다.

* 게시자
* 제안
* SKU

예를 들어, 이러한 값을 사용 하 여 hello로 [집합 AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet 또는 리소스 그룹 템플릿을 만든 VM toobe 유형의 hello를 지정 해야 합니다.

이러한 값 toodetermine 해야 할 경우 hello를 실행할 수 있습니다 [Get AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), 및 [Get AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlet toonavigate hello 이미지입니다. 다음 값을 확인합니다.

1. Hello 이미지 게시자 목록입니다.
2. 지정된 게시자에 제안을 나열합니다.
3. 지정된 제안에 SKU를 나열합니다.

다음 명령 hello로 hello 게시자를 먼저 나열:

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

선택한 게시자 이름을 입력 하 고 hello 다음 명령을 실행 합니다.

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

선택한 제품 이름에 입력 하 고 hello 다음 명령을 실행 합니다.

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Hello의 hello 출력에서 `Get-AzureRMVMImageSku` 명령, toospecify hello 이미지는 새 가상 컴퓨터에 필요한 모든 hello 정보입니다.

hello 다음 전체 예제를 보여 줍니다.

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

출력:

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

Hello "MicrosoftWindowsServer" 게시자:

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

출력:

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

"Windows Server" hello에 대 한 다음을 제공 합니다.

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

출력:

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

SKU 이름을 선택 하는 hello 복사한 hello에 대 한 모든 hello 정보가 있으면이 목록에서 `Set-AzureRMVMSourceImage` PowerShell cmdlet 또는 리소스 그룹 템플릿에 대 한 합니다.

## <a name="next-steps"></a>다음 단계
정확 하 게 hello 이미지를 선택할 수 이제 toouse를 원하는 합니다. toocreate 가상 컴퓨터를 찾을 수 있는 hello 이미지 정보를 사용 하 여 신속 하 게 참조 [PowerShell을 사용한 Windows 가상 컴퓨터를 만들](quick-create-powershell.md)합니다.
