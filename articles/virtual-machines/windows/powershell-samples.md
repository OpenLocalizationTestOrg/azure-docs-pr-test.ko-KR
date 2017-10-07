---
title: "가상 컴퓨터 PowerShell 샘플 aaaAzure | Microsoft Docs"
description: "Azure Virtual Machine PowerShell 샘플"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 89fd26aa979687cdcdf9ae4e60be7d0d2eaeae91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a>Azure Virtual Machine PowerShell 샘플

hello 다음 표는 Windows 가상 컴퓨터 만들기 및 관리 하는 링크 tooPowerShell 스크립트 예제.

| | |
|---|---|
|**가상 컴퓨터 만들기**||
| [완벽히 구성된 가상 컴퓨터 만들기](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.|
| [고가용성 가상 컴퓨터 만들기](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 고가용성의 부하가 분산된 구성으로 여러 가상 컴퓨터를 만듭니다.|
| [VM 만들기 및 구성 스크립트 실행](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Hello Azure 사용자 지정 스크립트 확장 tooinstall IIS를 사용 하는 가상 컴퓨터를 만듭니다. |
| [VM 만들기 및 DSC 구성 실행](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Hello Azure DSC 필요한 상태 구성 () 확장 tooinstall IIS를 사용 하는 가상 컴퓨터를 만듭니다. |
| [VHD 업로드 및 VM 만들기](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | 로컬 VHD Uplaods tooAzure 파일, 및 hello VHD에서에서 이미지 만들고 그런 다음 해당 이미지에서 VM을 만듭니다. |
| [관리되는 OS 디스크에서 VM 만들기](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 기존 관리되는 디스크를 OS 디스크로 연결하여 가상 컴퓨터를 만듭니다. |
| [스냅숏에서 VM 만들기](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 먼저 관리 되는 디스크 스냅숏에서 만들고 운영 체제 디스크로 hello 새 관리 되는 디스크를 연결 하는 다음 스냅숏에서 가상 컴퓨터를 만듭니다. |
|**저장소 관리**||
| [동일하거나 다른 구독의 VHD에서 관리 디스크 만들기](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 동일하거나 다른 구독에서 특수화된 VHD의 관리 디스크를 OS 디스크로 만들거나 데이터 VHD의 관리 디스크를 데이터 디스크로 만듭니다.  |
| [스냅숏에서 관리 디스크 만들기](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 스냅숏에서 관리 디스크를 만듭니다. |
| [관리 되는 디스크 toosame 또는 다른 구독 복사](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | 관리 되는 복사본이 디스크 toosame 또는 다른 구독 하지만 동일한 hello 지역 hello 부모 디스크를 관리 합니다. 
| [스냅숏을 VHD tooa 저장소 계정으로 내보내기](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 다른 지역에 VHD tooa 저장소 계정으로 관리 되는 스냅숏을 내보냅니다. |
| [VHD에서 스냅숏 만들기](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 스냅숏 VHD toocreate에서 스냅숏에서 여러 개의 동일한 관리 되는 디스크에에서 만듭니다 짧은 시간.  |
| [스냅숏 toosame 또는 다른 구독 복사](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 스냅숏 toosame 복사본 또는 hello 동일 하지만 다른 구독 hello 부모 스냅숏으로 영역입니다. |
|**가상 컴퓨터 보호**||
| [VM 및 데이터 디스크 암호화](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | Azure Key Vault, 암호화 키 및 서비스 주체를 만든 다음 VM을 암호화합니다. |
|**가상 컴퓨터 모니터링**||
| [Operations Management Suite를 사용하여 VM 모니터링](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 가상 컴퓨터의 이름을 만들고 hello Operations Management Suite 에이전트를 설치 hello OMS 작업 영역에서 VM을 등록 합니다.  |
| | |

