---
title: "Azure Portal에서 가상 머신 확장 집합 만들기 | Microsoft Docs"
description: "Azure Portal에서 가상 머신 확장 집합을 빠르게 만드는 방법 알아보기"
keywords: "가상 머신 크기 집합"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 12/19/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a501a852a317ec7d087904c3a675ebefce1bece0
ms.sourcegitcommit: 562a537ed9b96c9116c504738414e5d8c0fd53b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2018
---
# <a name="create-a-virtual-machine-scale-set-in-the-azure-portal"></a>Azure Portal에서 가상 머신 확장 집합 만들기
가상 머신 확장 집합을 사용하면 동일한 자동 크기 조정 가상 머신 집합을 배포하고 관리할 수 있습니다. 확장 집합의 VM 수를 수동으로 조정하거나 CPU와 같은 리소스 사용량, 메모리 요구량 또는 네트워크 트래픽을 기반으로 자동으로 크기를 조정하는 규칙을 정의할 수도 있습니다. 이 시작 문서에서는 Azure Portal에서 가상 머신 확장 집합을 만듭니다. 확장 집합은 [Azure CLI 2.0](virtual-machine-scale-sets-create-cli.md) 또는 [Azure PowerShell](virtual-machine-scale-sets-create-powershell.md)을 사용하여 만들 수도 있습니다.

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.


## <a name="log-in-to-azure"></a>Azure에 로그인
Azure Portal( http://portal.azure.com )에 로그인합니다.


## <a name="create-virtual-machine-scale-set"></a>가상 머신 확장 집합 만들기
RHEL, CentOS, Ubuntu 또는 SLES와 같은 Windows Server 이미지 또는 Linux 이미지를 사용하여 확장 집합을 배포할 수 있습니다.

1. Azure Portal의 왼쪽 위에 있는 **새로 만들기** 단추를 클릭합니다.
2. *확장 집합*을 검색하고 **가상 머신 확장 집합**을 선택한 다음 **만들기**를 선택합니다.
3. 확장 집합의 이름을 입력합니다(예: *myScaleSet*).
4. 원하는 OS 유형을 선택합니다(예: *Windows Server 2016 Datacenter*).
5. 원하는 리소스 그룹 이름(예: *myResourceGroup*) 및 위치(예: *미국 동부*)를 입력합니다.
6. 원하는 사용자 이름을 입력한 후 원하는 인증 유형을 선택합니다.
    - **암호**는 12자 이상 길이여야 하며 1개의 소문자, 1개의 대문자, 1개의 숫자 및 1개의 특수 문자 등 네 가지 복잡성 요구 사항 중 적어도 세 가지를 충족해야 합니다. 자세한 내용은 [사용자 이름 및 암호 요구 사항](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm)을 참조하세요.
    - Linux OS 디스크 이미지를 선택하는 경우 **SSH 공개 키**를 대신 선택할 수 있습니다. 공개 키만을 제공합니다(예: *~/.ssh/id_rsa.pub*). 포털에서 Azure Cloud Shell을 사용하여 [SSH 키를 만들고 사용](../virtual-machines/linux/mac-create-ssh-keys.md)할 수 있습니다.

7. **공용 IP 주소 이름**을 입력합니다(예: *myPublicIP*).
8. 고유한 **도메인 이름 레이블**을 입력합니다(예: *myuniquedns*). 이 DNS 레이블은 확장 집합 앞에 있는 부하 분산 장치에 대한 FQDN의 기준을 형성합니다.
9. 확장 집합 옵션을 확인하려면 **만들기**를 선택합니다.

    ![Azure Portal에서 가상 머신 확장 집합 만들기](./media/virtual-machine-scale-sets-create-portal/create-scale-set.png)


## <a name="connect-to-a-vm-in-the-scale-set"></a>확장 집합의 VM에 연결
포털에서 확장 집합을 만들 때 부하 분산 장치가 생성됩니다. NAT(네트워크 주소 변환) 규칙은 RDP 또는 SSH와 같은 원격 연결에 대한 확장 집합 인스턴스에 트래픽을 분산하는 데 사용됩니다.

확장 집합 인스턴스에 대한 이러한 NAT 규칙 및 연결 정보를 보려면:

1. 이전 단계에서 만든 리소스 그룹을 선택합니다(예: *myResourceGroup*).
2. 리소스 목록에서 **부하 분산 장치**를 선택합니다(예: *myScaleSetLab*).
3. 창의 왼쪽에 있는 메뉴에서 **인바운드 NAT 규칙**을 선택합니다.

    ![인바운드 NAT 규칙을 사용하면 가상 머신 확장 집합 인스턴스에 연결할 수 있습니다.](./media/virtual-machine-scale-sets-create-portal/inbound-nat-rules.png)

이러한 NAT 규칙을 사용하여 확장 집합의 각 VM에 연결할 수 있습니다. 각 VM 인스턴스는 대상 IP 주소 및 TCP 포트 값을 나열합니다. 예를 들어 대상 IP 주소가 *104.42.1.19*이고 TCP 포트가 *50001*인 경우 다음과 같이 VM 인스턴스에 연결합니다.

- Windows 확장 집합의 경우 `104.42.1.19:50001`에서 RDP를 사용하여 VM 인스턴스에 연결합니다.
- Linux 확장 집합의 경우 `ssh azureuser@104.42.1.19 -p 50001`에서 SSH를 사용하여 VM 인스턴스에 연결합니다.

대화 상자가 나타나면 확장 집합을 만들 때 이전 단계에서 지정한 자격 증명을 입력합니다. 확장 집합 인스턴스는 정상적으로 상호 작용할 수 있는 기본 VM입니다. 확장 집합 인스턴스에서 응용 프로그램을 배포하고 실행하는 방법에 대한 자세한 내용은 [가상 머신 확장 집합에 응용 프로그램 배포](virtual-machine-scale-sets-deploy-app.md)를 참조하세요.


## <a name="clean-up-resources"></a>리소스 정리
더 이상 필요하지 않을 때 리소스 그룹, 확장 집합 및 모든 관련 리소스를 삭제합니다. 이렇게 하려면 VM에 대한 리소스 그룹을 선택하고 **삭제**를 클릭합니다.


## <a name="next-steps"></a>다음 단계
이 시작 문서에서는 Azure Portal에서 기본 확장 집합을 만들었습니다. 확장성 및 자동화를 향상시키려면 다음 방법 문서를 사용하여 확장 집합을 확장합니다.

- [가상 머신 확장 집합에 응용 프로그램 배포](virtual-machine-scale-sets-deploy-app.md)
- [Azure PowerShell](virtual-machine-scale-sets-autoscale-powershell.md), [Azure CLI](virtual-machine-scale-sets-autoscale-cli.md) 또는 [Azure Portal](virtual-machine-scale-sets-autoscale-portal.md)을 사용하여 자동 크기 조정
- [확장 집합 VM 인스턴스에 자동 OS 업그레이드 사용](virtual-machine-scale-sets-automatic-upgrade.md)
