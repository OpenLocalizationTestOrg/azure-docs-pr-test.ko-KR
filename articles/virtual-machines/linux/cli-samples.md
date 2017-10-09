---
title: "CLI 샘플 aaaAzure | Microsoft Docs"
description: "Azure CLI 샘플"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/08/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 776c947e6daca564242fc77b0527dcb124fa057d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-linux-virtual-machines"></a>Linux 가상 컴퓨터에 대한 Azure CLI 샘플

hello 다음 표는 hello Azure CLI를 사용 하 여 빌드된 링크 toobash 스크립트.

| | |
|---|---|
|**가상 컴퓨터 만들기**||
| [가상 컴퓨터 만들기](./../scripts/virtual-machines-linux-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | 최소한의 구성으로 Linux 가상 컴퓨터를 만듭니다. |
| [완벽히 구성된 가상 컴퓨터 만들기](./../scripts/virtual-machines-linux-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.|
| [고가용성 가상 컴퓨터 만들기](./../scripts/virtual-machines-linux-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | 고가용성의 부하가 분산된 구성으로 여러 가상 컴퓨터를 만듭니다. |
| [Docker가 활성화된 VM 만들기](./../scripts/virtual-machines-linux-cli-sample-create-docker-host.md?toc=%2fcli%2fazure%2ftoc.json) | 가상 컴퓨터를 만들고 이 VM을 Docker 호스트로 구성하고 NGINX 컨테이너를 실행합니다. |
| [VM 만들기 및 구성 스크립트 실행](./../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md?toc=%2fcli%2fazure%2ftoc.json) | Hello Azure 사용자 지정 스크립트 확장 tooinstall NGINX를 사용 하는 가상 컴퓨터를 만듭니다. |
| [WordPress가 설치된 VM 만들기](./../scripts/virtual-machines-linux-cli-sample-create-vm-wordpress.md?toc=%2fcli%2fazure%2ftoc.json) | Hello Azure 사용자 지정 스크립트 확장 tooinstall WordPress를 사용 하는 가상 컴퓨터를 만듭니다. |
| [관리되는 OS 디스크에서 VM 만들기](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json) | 기존 관리되는 디스크를 OS 디스크로 연결하여 가상 컴퓨터를 만듭니다. |
| [스냅숏에서 VM 만들기](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | 먼저 관리 되는 디스크 스냅숏에서 만들고 운영 체제 디스크로 hello 새 관리 되는 디스크를 연결 하는 다음 스냅숏에서 가상 컴퓨터를 만듭니다. |
|**저장소 관리**||
| [VHD에서 관리 디스크 만들기](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json) | 특수화된 VHD의 관리 디스크를 OS 디스크로 만들거나 데이터 VHD의 관리 디스크를 데이터 디스크로 만듭니다.  |
| [스냅숏에서 관리 디스크 만들기](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | 스냅숏에서 관리 디스크를 만듭니다. |
| [관리 되는 디스크 toosame 또는 다른 구독 복사](../scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | 관리 되는 복사본이 디스크 toosame 또는 다른 구독 하지만 동일한 hello 지역 hello 부모 디스크를 관리 합니다. 
| [스냅숏을 VHD tooa 저장소 계정으로 내보내기](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-storage-account.md?toc=%2fcli%2fmodule%2ftoc.json) | 다른 지역에 VHD tooa 저장소 계정으로 관리 되는 스냅숏을 내보냅니다. |
| [스냅숏 toosame 또는 다른 구독 복사](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | 스냅숏 toosame 복사본 또는 hello 동일 하지만 다른 구독 hello 부모 스냅숏으로 영역입니다. |
|**네트워크 가상 컴퓨터**||
| [가상 컴퓨터 간의 네트워크 트래픽 보안](./../scripts/virtual-machines-linux-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | 두 개의 가상 컴퓨터, 모든 관련된 리소스 및 내부 및 외부 NSG(네트워크 보안 그룹)를 만듭니다. |
|**가상 컴퓨터 보호**||
| [VM 및 데이터 디스크 암호화](./../scripts/virtual-machines-linux-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Azure Key Vault, 암호화 키 및 서비스 주체를 만든 다음 VM을 암호화합니다. |
|**가상 컴퓨터 모니터링**||
| [Operations Management Suite를 사용하여 VM 모니터링](./../scripts/virtual-machines-linux-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | 가상 컴퓨터의 이름을 만들고 hello Operations Management Suite 에이전트를 설치 hello OMS 작업 영역에서 VM을 등록 합니다.  |
|**가상 컴퓨터 문제 해결**||
| [VM 운영 체제 디스크 문제 해결](./../scripts/virtual-machines-linux-cli-sample-mount-os-disk.md?toc=%2fcli%2fazure%2ftoc.json) | 두 번째 VM에 데이터 디스크로 하나의 VM에서 hello 운영 체제 디스크를 탑재합니다. |
| | |
