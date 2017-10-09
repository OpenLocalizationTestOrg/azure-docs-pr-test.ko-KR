---
title: "Azure 포털 hello aaaOpen 포트 tooa 사용 하 여 VM | Microsoft Docs"
description: "자세한 방법을 tooopen 포트 끝점 tooyour Windows VM을 만들 / hello 리소스 관리자 배포 모델을 사용 하 여 hello Azure 포털에서"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a>Tooopen은 tooa hello Azure 포털 사용 하는 가상 컴퓨터 포트 하는 방법
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>빠른 명령
[Azure PowerShell을 사용하여 수행할 수도 있습니다](nsg-quickstart-powershell.md).

먼저 네트워크 보안 그룹을 만듭니다. Hello 포털에서 리소스 그룹을 선택, 선택 **추가**다음 검색 하 고 선택 **네트워크 보안 그룹**:

![네트워크 보안 그룹 추가](./media/nsg-quickstart-portal/add-nsg.png)

네트워크 보안 그룹의 이름을 입력하고, 리소스 그룹을 선택하거나 만들고, 위치를 선택합니다. 작업을 완료하면 **만들기**를 선택합니다.

![네트워크 보안 그룹 만들기](./media/nsg-quickstart-portal/create-nsg.png)

새 네트워크 보안 그룹을 선택합니다. '인바운드 보안 규칙'를 선택 하 고 hello 선택 **추가** 단추 toocreate 규칙:

![인바운드 규칙 추가](./media/nsg-quickstart-portal/add-inbound-rule.png)

공통 선택 **서비스** hello 드롭 다운 메뉴에서와 같은 *HTTP*합니다. 선택할 수도 있습니다 *사용자 지정* tooprovide 특정 포트 toouse 합니다. 원하는 경우 hello 우선 순위 또는 이름을 변경 합니다. hello 우선 순위에 영향을 hello 순서-규칙이 적용 되는 hello 숫자 값이 낮을수록 hello hello 이전 hello 규칙이 적용 됩니다. 선택할 수도 있습니다 **고급** 특정 hello 위쪽이 화면 tooenter에 IP 블록 또는 포트 범위 예를 들어 원본입니다. 준비 되 면 선택 **확인** toocreate hello 규칙:

![인바운드 규칙 만들기](./media/nsg-quickstart-portal/create-inbound-rule.png)

마지막 단계는 tooassociate 서브넷 또는 특정 네트워크 인터페이스를 네트워크 보안 그룹입니다. 서브넷과 hello 네트워크 보안 그룹을 연결 해 보겠습니다. **서브넷**을 선택한 후 **연결**을 선택합니다.

![서브넷에 네트워크 보안 그룹 연결](./media/nsg-quickstart-portal/associate-subnet.png)

가상 네트워크를 선택 하 고 hello 적절 한 서브넷을 선택 합니다.

![가상 네트워킹에 네트워크 보안 그룹 연결](./media/nsg-quickstart-portal/select-vnet-subnet.png)

이제 네트워크 보안 그룹을 만들고, 포트 80에서 트래픽을 허용하는 인바운드 규칙을 만들었으며 해당 규칙을 서브넷과 연결했습니다. Toothat 서브넷 연결 모든 Vm은 포트 80에서 연결할 수 있습니다.

## <a name="more-information-on-network-security-groups"></a>네트워크 보안 그룹에 대한 자세한 정보
빠른 명령을 여기 hello를 사용 하면를 tooget 및 트래픽 이동을 tooyour VM으로 실행 합니다. 네트워크 보안 그룹 많은 향상 된 기능 및 제어 tooyour 리소스 액세스에 대 한 세분성을 제공합니다. [여기서 네트워크 보안 그룹 및 ACL 규칙 만들기](../../virtual-network/virtual-networks-create-nsg-arm-ps.md)에 대해 자세히 읽어보세요.

고가용성 웹 응용 프로그램인 경우 VM을 Azure Load Balancer 뒤에 배치해야 합니다. hello 부하 분산 장치 트래픽 tooVMs 트래픽 필터링이 제공 하는 네트워크 보안 그룹에 배포 합니다. 자세한 내용은 참조 [어떻게 tooload 균형 Linux 가상 컴퓨터에서 Azure toocreate 항상 사용 가능한 응용 프로그램](tutorial-load-balancer.md)합니다.

## <a name="next-steps"></a>다음 단계
이 예제에서는 간단한 규칙 tooallow HTTP 트래픽을 만들었습니다. Hello 문서 다음에 보다 자세한 환경을 만드는 방법에 대 한 정보를 찾을 수 있습니다.

* [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)
* [NSG(네트워크 보안 그룹)란?](../../virtual-network/virtual-networks-nsg.md)