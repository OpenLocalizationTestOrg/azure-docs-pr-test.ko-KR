---
title: "VM 네트워크 처리량 aaaOptimize | Microsoft Docs"
description: "Azure 가상 컴퓨터 toooptimize 처리량 네트워크 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a>Azure Virtual Machine에 대한 네트워크 처리량 최적화

Azure VM(Virtual Machine)에는 네트워크 처리량에 대해 추가로 최적화할 수 있는 기본 네트워크 설정이 있습니다. 이 문서에서는 toooptimize 처리량 Microsoft Azure Windows 및 Ubuntu, CentOS 및 Red Hat와 같은 주요 분포를 비롯 한 Linux Vm 네트워크 하는 방법을 설명 합니다.

## <a name="windows-vm"></a>Windows VM

Windows VM으로 지원 되는 경우 [네트워킹 Accelerated](virtual-network-create-vm-accelerated-networking.md), 처리량에 맞는 최적의 구성을 hello 해당 기능을 사용 하면 됩니다. RSS(수신측 배율)를 사용하는 다른 모든 Windows VM은 RSS 없는 VM보다 더 높은 최대 처리량에 도달할 수 있습니다. RSS는 Windows VM에서 기본적으로 사용되지 않도록 설정될 수 있습니다. RSS를 사용 하는지 여부를 toodetermine 단계를 수행 하는 hello 및 tooenable 완료 해제 되어 있는 것입니다.

1. Hello 입력 `Get-NetAdapterRss` PowerShell 명령 toosee 네트워크 어댑터에 대 한 RSS를 사용 하는 경우. Hello에 다음 예제 출력에서에서 반환 된 hello `Get-NetAdapterRss`, RSS를 사용 하지 않습니다.

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. 다음 명령은 tooenable RSS hello를 입력 합니다.

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    hello 이전 명령에는 출력은 없습니다. 1 분 정도 대 한 임시 연결 손실 생김 NIC 설정을 변경 하는 hello 명령입니다. Hello 연결이 손실 중에 다시 연결 대화 상자가 나타납니다. 일반적으로 hello 세 번째 시도 후 연결이 복원 합니다.
3. Hello를 입력 하 여 hello VM에서에서 RSS 활성화 되어 있는지 확인 `Get-NetAdapterRss` 명령을 다시 합니다. 성공 하면 다음 예제 출력 hello 반환 됩니다.

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a>Linux VM

RSS는 Azure Linux VM에 기본적으로 항상 사용되도록 설정됩니다. 2017 년 1 월 이후에 출시 Linux 커널을 Linux VM tooachieve 더 높은 네트워크 처리량을 사용할 수 있는 새 네트워크 최적화 옵션을 포함 합니다.

### <a name="ubuntu"></a>Ubuntu

순서 tooget hello 최적화에서 먼저는 6 월 2017 년을 기준으로 toohello 지 원하는 최신 버전을 업데이트 합니다.
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
Hello 업데이트가 완료 후 다음 명령을 tooget hello 최신 커널 hello를 입력 합니다.

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

선택적 명령:

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a>Ubuntu Azure Preview 커널
> [!WARNING]
> 커널 없을 수 있습니다이 Azure Linux 미리 보기에는 동일한 수준의 가용성과 안정성 마켓플레이스 이미지와 커널을 공급 릴리스 있는 일반적으로 hello 합니다. hello 기능은 지원 되지 않습니다, 기능, 제한 있을 수 있습니다 및 hello 기본 커널 것 만큼 신뢰성이 되지 않을 수 있습니다. 따라서 프로덕션 작업에는 이 커널을 사용하지 마세요.

Azure Linux 커널을 제안 hello를 설치 하 여 중요 한 처리량 성능을 얻을 수 있습니다. tootry이이 커널이 줄 too/etc/apt/sources.list 추가

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

그런 다음 아래 명령을 루트로 실행합니다.
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a>CentOS

순서 tooget hello 최적화에서 먼저은 년 7 월 2017 년을 기준으로 toohello 지 원하는 최신 버전을 업데이트 합니다.
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
Hello 업데이트가 완료 후 설치 hello 최신 Linux Integration Services (LIS).
hello 처리량 최적화 4.2.2-2에서 시작 LIS에는입니다. 다음 명령을 tooinstall LIS hello를 입력 합니다.

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a>Red Hat

순서 tooget hello 최적화에서 먼저은 년 7 월 2017 년을 기준으로 toohello 지 원하는 최신 버전을 업데이트 합니다.
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
Hello 업데이트가 완료 후 설치 hello 최신 Linux Integration Services (LIS).
hello 처리량 최적화에 LIS, 4.2에서 시작 하는입니다. 다음 명령을 toodownload hello를 입력 하 고 LIS를 설치 합니다. 키를 누릅니다.

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

Hello를 확인 하 여 Hyper-v에 대 한 자세한 내용은 Linux Integration Services 버전 4.2에 대 한 [다운로드 페이지](https://www.microsoft.com/download/details.aspx?id=55106)합니다.

## <a name="next-steps"></a>다음 단계
* Hello VM가 최적화를 사용 하 여 hello 결과 참조 [대역폭/처리량 Azure VM 테스트](virtual-network-bandwidth-testing.md) 시나리오에 대 한 합니다.
* [Azure Virtual Network FAQ(질문과 대답)](virtual-networks-faq.md)에 대해 자세히 알아보기
