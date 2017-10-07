---
title: "Linux Vm의 경우 Azure 포털의 기존 네트워크에 aaaDeploy | Microsoft Docs"
description: "Hello 포털을 사용 하는 기존 Azure 가상 네트워크로 Linux VM을 배포 합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a>어떻게 toodeploy hello Azure 포털으로 기존 Azure 가상 네트워크로 Linux 가상 컴퓨터

이 문서에서는 어떻게 toodeploy 기존 가상 네트워크 (VNet)로 가상 컴퓨터 (VM). VNet 및 네트워크 보안 그룹과 같은 Azure 자산은 정적이고 거의 배포되지 않는 수명이 긴 리소스인 것이 좋습니다. VNet에 배포한 후에 부정적인 영향을 줌 toohello 인프라 없이 상수 재배포가 재사용할 수 있습니다. 기존의 행사로 VNet에 대해 생각 하드웨어 네트워크 스위치-필요는 없습니다 tooconfigure 각 배포와 새로운 하드웨어 전환 합니다.  

올바르게 구성 된 VNet에 계속할 수 있습니다 toodeploy 새 서버 해당 VNet에 반복 해 hello VNet의 hello 수명 기간 동안 필요한 경우에 자주 변경.

## <a name="create-hello-resource-group"></a>Hello 리소스 그룹 만들기

먼저 만듭니다 리소스 그룹 tooorganize이이 연습에서 만드는 모든 항목입니다. Azure 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a>Hello VNet 만들기

다음으로 VNet toolaunch hello를 Vm으로 빌드하십시오. hello VNet 서브넷 1 개를 포함 하 고 이후 단계에서이 서브넷 hello 네트워크 보안 그룹과 연결 됩니다.

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a>VNic toohello 서브넷 추가

가상 네트워크 카드 (VNics)은 중요 toodifferent Vm 연결할 수 있습니다. 이 방법은 hello Vm 말할 수 하는 동안 정적 리소스로 hello VNic를 유지 합니다. VNic 만들고 hello 이전 단계에서 만든 hello 서브넷과 연결 합니다.

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a>Hello 네트워크 보안 그룹 만들기

Azure 네트워크 보안 그룹은 hello 네트워크 계층에서 해당 tooa 방화벽입니다. Azure 네트워크 보안 그룹에 대한 자세한 내용은 [네트워크 보안 그룹이란?](../../virtual-network/virtual-networks-nsg.md)을 참조하세요.

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>인바운드 SSH 허용 규칙 추가

hello에서 액세스를 해야 하는 hello VM 인터넷, 인바운드 포트 22 트래픽 toobe 허용 하는 규칙이 VM이 생성 하는 hello hello 네트워크 tooport 22 통해 전달 하도록 합니다.

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a>Hello 서브넷과 hello NSG 연결

VNet hello와 작성 hello 서브넷을 네트워크 보안 그룹을 hello hello 서브넷 연관 시킵니다. 네트워크 보안 그룹은 전체 서브넷 또는 개별 VNic와 연결될 수 있습니다. Hello 방화벽 hello 서브넷 수준에서 트래픽을 필터링으로 모든 VNics 및 hello 서브넷 내에서 Vm hello hello 네트워크 보안 그룹에 의해 보호 됩니다. hello 방법이 hello 네트워크 보안 그룹 되 고 단일 VNic 방금와 연결 된 하 고 하나의 VM을 보호 합니다.

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Hello VNet에 VM hello 및 NSG를 배포 합니다.

Hello Linux VM에 기존 Azure 리소스 그룹, VNet, 서브넷 및 VNic 배포 toohello는 hello Azure 포털을 사용 합니다.

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

Hello 포털 toochoose 기존 리소스를 사용 하 여 hello 기존 네트워크 내부 Azure toodeploy hello VM 지시할 수 있습니다. VNet 및 서브넷이 배포되면 Azure 지역 내에서 정적 또는 영구적으로 리소스로 유지할 수 있습니다.  

## <a name="next-steps"></a>다음 단계

* [Azure 리소스 관리자 템플릿 toocreate 특정 배포를 사용 하 여](../windows/cli-deploy-templates.md)
* [Azure CLI 명령을 직접 사용하여 Linux VM에 대한 고유한 사용자 지정 환경 만들기](create-cli-complete.md)
* [템플릿을 사용하여 Azure에서 Linux VM 만들기](create-ssh-secured-vm-from-template.md)
