---
title: "가상 컴퓨터 크기 집합 using aaaCreate hello Azure 포털 | Microsoft Docs"
description: "Azure Portal을 사용하여 확장 집합을 배포합니다."
keywords: "가상 컴퓨터 확장 집합"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a>방법으로 가상 컴퓨터 크기 집합 a toocreate hello Azure 포털
이 자습서에서는 얼마나 쉬운지 가상 컴퓨터 크기 집합 toocreate 단 몇 분 후에 hello Azure 포털을 사용 하 여 보여 줍니다. Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/) 을 만듭니다.

## <a name="choose-hello-vm-image-from-hello-marketplace"></a>Hello 마켓플레이스에서 hello VM 이미지를 선택 합니다.
Hello 포털에서 CentOS, CoreOS, Debian, 열기 Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server 또는 Windows Server 이미지를 사용 하 여 설정 하는 눈금을 쉽게 배포할 수 있습니다.

첫째, toohello 이동 [Azure 포털](https://portal.azure.com) 웹 브라우저에서 합니다. 클릭 `New`, 검색할 `scale set`를 선택한 후 hello `Virtual machine scale set` 항목:

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a>Hello 크기 집합 만들기
이제 hello 기본 설정을 사용 하 고 신속 하 게 hello 크기 집합을 만들 수 있습니다.

* Hello에 `Basics` 블레이드에서 hello 크기 집합의 이름을 입력 합니다. 이 이름은 기본 hello 됩니다의 hello hello 크기 집합 앞에 hello 부하 분산 장치의 FQDN, 해야 hello 이름을 모든 Azure에서 고유 합니다.
* 원하는 OS 유형을 선택하고, 원하는 사용자 이름을 입력한 후 원하는 인증 유형을 선택합니다. 암호를 선택 하면 긴 하 고는 세 가지 hello 4 개의 다음 복잡성 요구 사항을 충족 하는 12 자 이상 이어야 합니다: 하나의 \t-소문자, 대문자 한 문자, 숫자, 및 특수 문자를 하나 있습니다. 자세한 내용은 [사용자 이름 및 암호 요구 사항](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm)을 참조하세요. 선택 하면 `SSH public key`에서 공개 키, 개인 키로 되지 있는지 tooonly 붙여넣기 여야 합니다.

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* 여부나를 배치 그룹이 여러 개를 넘으면 toolimit hello 배율 설정 tooa 단일 배치 그룹은 여부를 선택 합니다. 크기 조정 설정 하는 100 개 이상의 Vm 용량 too1 000) (위쪽에 특정 제한 사항과 함께 수 hello 크기 집합 toospan 배치 그룹을 허용 합니다. 자세한 내용은 [SDK 설명서](./virtual-machine-scale-sets-placement-groups.md)를 참조하세요.
* 원하는 리소스 그룹 이름 및 위치를 입력한 다음 `OK`를 클릭합니다.
* Hello에 `Virtual machine scale set service settings` 블레이드: 원하는 도메인 이름 레이블 (hello base의 hello 크기 집합 앞에 hello 부하 분산 장치에 대 한 FQDN hello)를 입력 합니다. 이 레이블은 모든 Azure에서 고유해야 합니다.
* 원하는 운영 체제 디스크 이미지, 인스턴스 수 및 컴퓨터 크기를 선택합니다.
* 원하는 디스크 유형 선택: 관리 또는 관리 되지 않습니다. 자세한 내용은 [SDK 설명서](./virtual-machine-scale-sets-managed-disks.md)를 참조하세요. Toohave hello 크기 집합을 선택 하는 경우 여러 배치 그룹으로 확장, 관리 되는 디스크 크기 조정 설정 toospan 배치 그룹에 대 한 필요 하므로이 옵션을 사용할 수 없습니다.
* 자동 크기 조정을 사용하거나 사용하지 않도록 설정하고 사용하도록 설정하는 경우 다음을 구성합니다.

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* Hello에 `Summary` 블레이드, 유효성 검사를 수행 하는 경우 클릭 `OK` toostart hello 확장 배포를 설정 합니다.


## <a name="connect-tooa-vm-in-hello-scale-set"></a>Hello 크기 집합의 tooa VM 연결
Toolimit를 선택한 경우 눈금 tooa 단일 배치 그룹을 설정한 다음 toohello에 크기 집합을 쉽게 연결 하는 NAT 구성 된 규칙 toolet hello 크기 집합이 배포 (toocreate 필요할 hello 규모에 맞게 tooconnect toohello 가상 컴퓨터를 설정 하지는 jumpbox hello에 크기 집합 hello와 동일한 가상 네트워크). toosee toohello 이동, `Inbound NAT Rules` hello 크기 집합에 대 한 hello 부하 분산 장치 탭:

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

Tooeach hello 눈금에는 VM이 NAT 규칙을 사용 하 여 집합을 연결할 수 있습니다. 예를 들어, Windows 크기 집합에 대 한 들어오는 포트 50000에서 NAT 규칙이 있을 경우 수 RDP 통해 toothat 컴퓨터에서 연결할 `<load-balancer-ip-address>:50000`합니다. Hello 명령을 사용 하 여 연결 하듯이 Linux 크기 집합에 대해 `ssh -p 50000 <username>@<load-balancer-ip-address>`합니다.

## <a name="next-steps"></a>다음 단계
CLI hello에서 toodeploy 비율을 설정 하는 방법에 대 한 설명서를 참조 하십시오. [이 설명서](virtual-machine-scale-sets-cli-quick-create.md)합니다.

PowerShell에서 toodeploy 비율을 설정 하는 방법에 대 한 설명서를 참조 하십시오. [이 설명서](virtual-machine-scale-sets-windows-create.md)합니다.

Visual Studio에서 toodeploy 비율을 설정 하는 방법에 대 한 설명서를 참조 하십시오. [이 설명서](virtual-machine-scale-sets-vs-create.md)합니다.

일반 설명서에 대 한 체크 아웃 hello [크기 집합에 대 한 설명서 개요 페이지](virtual-machine-scale-sets-overview.md)합니다.

일반 정보에 대 한 체크 아웃 hello [크기 집합에 대 한 기본 방문 페이지](https://azure.microsoft.com/services/virtual-machine-scale-sets/)합니다.

