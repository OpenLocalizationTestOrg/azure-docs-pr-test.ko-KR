---
title: "Azure 가상 컴퓨터-포털에 대 한 IP 주소 aaaMultiple | Microsoft Docs"
description: "여러 IP 해결 하는 tooassign 방법을 알아보려면 Azure 포털 hello tooa 가상 컴퓨터를 사용 하 여 | 리소스 관리자입니다."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: 34075766ac68c8de38c258a4d70e35881f28bb0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 여러 IP 주소 toovirtual 컴퓨터 할당

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
이 문서에서는 toocreate hello Azure 리소스 관리자 배포 모델을 사용 하 여 가상 컴퓨터 (VM) Azure 포털을 hello 하는 방법을 설명 합니다. Hello 클래식 배포 모델을 통해 만든 tooresources 여러 IP 주소를 할당할 수 없습니다. Azure 배포 모델을 읽을 hello에 대 한 자세한 toolearn [배포 모델을 이해](../resource-manager-deployment-model.md) 문서.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>여러 IP 주소를 사용하여 VM 만들기

여러 개의 IP 주소 또는 정적 개인 IP 주소를 사용 하 여 VM toocreate 원하는 hello Azure CLI 또는 PowerShell을 사용 하 여 만들어야 합니다. 방법 hello PowerShell 또는 CLI 옵션을이 문서 toolearn hello 위쪽에서를 클릭 합니다. 단일 동적 개인 IP 주소 및 hello hello 단계를 수행 하 여 hello 포털을 사용 하는 단일 공용 IP 주소 (선택 사항) 사용 하 여 VM을 만들 수 [Windows VM을 만들](../virtual-machines/virtual-machines-windows-hero-tutorial.md) 또는 [Linux VM을 만들](../virtual-machines/linux/quick-create-portal.md) 문서입니다. 동적 toostatic hello IP 주소 유형을 변경할 수 있으며 hello의 단계를 따라 hello 포털을 사용 하 여 IP 주소를 추가 hello VM을 만든 후 [추가 IP 주소 tooa VM](#add) 이 문서의 섹션.

## <a name="add"></a>IP 주소 tooa VM 추가

개인 및 공용 IP 주소 tooa NIC를 수행 하는 hello 단계를 완료 하 여 추가할 수 있습니다. hello hello 다음 섹션의에서 예제에서는 이미 있다고 가정 VM hello에 설명 된 hello 3 IP 구성이 [시나리오](#Scenario) 이 문서에서는 하지만 필요 하지는 않도록 합니다.

### <a name="coreadd"></a>핵심 단계

1. 필요한 경우을 옵트인 toohello Azure 포털 https://portal.azure.com 및 기호를 찾습니다.
2. Hello 포털에서 클릭 **더 많은 서비스** > 형식 *가상 컴퓨터* 필터 상자 hello와 클릭 **가상 컴퓨터**합니다.
3. Hello에 **가상 컴퓨터** 블레이드에서 hello VM tooadd IP 주소를 클릭 합니다. 클릭 **네트워크 인터페이스** hello 가상 컴퓨터 블레이드, 표시 되 고 선택 hello 네트워크에서 tooadd hello IP 인터페이스를 해결 합니다. Hello에 표시 된 hello 예제에서 NIC 라는 hello 그림을 따라 *myNIC* hello 라는 VM에서에서 *myVM* 선택:

    ![네트워크 인터페이스](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. Hello 블레이드에서 나타나는 선택한 NIC hello에 대 한 클릭 **IP 구성을**합니다.

이어지는 hello 섹션 중 하나에서 단계를 완료 hello, tooadd 원하는 IP 주소의 hello 형식을 기반으로 합니다.

### <a name="add-a-private-ip-address"></a>**개인 IP 주소 추가**

다음 단계 tooadd 새 개인 IP 주소는 hello를 완료 합니다.

1. Hello에서 단계를 완료 하는 hello [단계 핵심](#coreadd) 이 문서의 섹션.
2. **추가**를 클릭합니다. Hello에 **IP 추가 구성** 나타나는 블레이드 라는 IP 구성을 만든 *IPConfig-4* 와 *10.0.0.7* 로 *정적* 개인 IP 주소, 한 다음 클릭 **확인**합니다.

    > [!NOTE]
    > 고정 IP 주소를 추가할 때에 NIC에 연결 된 hello 서브넷 hello에는 사용 되지 않는, 유효한 주소를 지정 해야 합니다. Hello 주소를 선택 하면 사용할 수 없는 경우 hello 포털 hello IP 주소에 대 한 X 볼 수 있으며 다른 tooselect 필요 합니다.

3. 확인을 클릭 한 후 hello 블레이드 닫히고 나열 된 hello 새 IP 구성이 표시 됩니다. 클릭 **확인** tooclose hello **IP 추가 구성** 블레이드입니다.
4. 클릭할 수 있는 **추가** 추가 IP 구성을 tooadd 닫기 열려 있는 모든 블레이드 toofinish 추가 IP 주소 또는 합니다.
5. 추가 hello 개인 IP 주소 수 toohello VM 운영 체제 hello에 운영 체제에 대 한 hello 단계를 완료 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션.

### <a name="add-a-public-ip-address"></a>공용 IP 주소 추가

공용 IP 주소는 새 IP 구성 또는 기존 IP 구성에 공용 IP 주소 리소스 tooeither를 연결 하 여 추가 됩니다.

> [!NOTE]
> 공용 IP 주소에는 명목 요금이 부과됩니다. 가격 책정, 주소 IP에 대 한 자세한 toolearn 읽을 hello [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지. 구독에서 사용할 수 있는 공용 IP 주소의 제한이 toohello 수가입니다. hello 제한, hello 읽기에 대 한 자세한 toolearn [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서.
> 

### <a name="create-public-ip"></a>공용 IP 주소 리소스 만들기

공용 IP 주소는 공용 IP 주소 리소스에 대한 한 가지 설정입니다. 원하는 현재 연결된 tooan IP 구성 되지 않은 공용 IP 주소 리소스를 설정한 경우 tooassociate tooan IP 구성 단계를 수행 하는 hello를 건너뛰고 필요한 만큼 따르려면 hello 섹션 중 하나에 hello 단계를 완료 합니다. 사용 가능한 공용 IP 주소 리소스를 설정 하지 않은 경우 단계 toocreate 하나를 수행 하는 hello를 완료 합니다.

1. 필요한 경우을 옵트인 toohello Azure 포털 https://portal.azure.com 및 기호를 찾습니다.
3. Hello 포털에서 클릭 **새로** > **네트워킹** > **공용 IP 주소**합니다.
4. Hello에 **공용 IP 주소 만들기** 나타나는 블레이드를 입력 한 **이름**을 선택는 **IP 주소 할당** 형식은 **구독**, 즉 **리소스 그룹**, 및 **위치**, 클릭 **만들기**hello 다음 그림에에서 나온 것 처럼:

    ![공용 IP 주소 리소스 만들기](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. 전체 hello tooassociate hello 공용 IP 주소 리소스 tooan IP 구성에 따라 hello 섹션 중 하나에서 안내 합니다.

#### <a name="associate-hello-public-ip-address-resource-tooa-new-ip-configuration"></a>Hello 공용 IP 주소 리소스 tooa 새 IP 구성에 연결

1. Hello에서 단계를 완료 하는 hello [단계 핵심](#coreadd) 이 문서의 섹션.
2. **추가**를 클릭합니다. Hello에 **IP 추가 구성** 나타나는 블레이드 라는 IP 구성을 만든 *IPConfig-4*합니다. Hello를 사용 하도록 설정 **공용 IP 주소** hello에서 기존에 사용할 수 있는 공용 IP 주소 리소스를 선택 하 고 **공용 IP 주소 선택** 블레이드를 표시 합니다.

    Hello 공용 IP 주소 리소스를 선택한 후 클릭 **확인** 고 hello 블레이드 닫힙니다. Hello의 hello 단계를 완료 하 여 만들 수는 기존 공용 IP 주소에 없으면 [공용 IP 주소 리소스를 만들](#create-public-ip) 이 문서의 섹션. 

3. Hello 새 IP 구성 검토 합니다. 개인 IP 주소를 명시적으로 할당 되지 않은, 경우에 모든 IP 구성에 개인 IP 주소 해야 하기 때문에 toohello IP 구성의 자동으로 할당 된 하나.
4. 클릭할 수 있는 **추가** 추가 IP 구성을 tooadd 닫기 열려 있는 모든 블레이드 toofinish 추가 IP 주소 또는 합니다.
5. Hello에 운영 체제에는 hello 단계를 완료 하 여 hello 개인 IP 주소 toohello VM 운영 체제 추가 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션. Hello 공용 IP 주소 toohello 운영 체제를 추가 하지 마십시오.

#### <a name="associate-hello-public-ip-address-resource-tooan-existing-ip-configuration"></a>Hello 공용 IP 주소 리소스 tooan 기존 IP 구성에 연결

1. Hello에서 단계를 완료 하는 hello [단계 핵심](#coreadd) 이 문서의 섹션.
2. Hello IP 구성을 tooadd hello 공용 IP 주소 리소스를 클릭 합니다.
3. 나타나는 hello IPConfig 블레이드에서 클릭 **IP 주소**합니다.
4. Hello에 **공용 IP 주소 선택** 블레이드에 표시 되는 공용 IP 주소를 선택 합니다.
5. 클릭 **저장** 고 hello 블레이드 닫힙니다. Hello의 hello 단계를 완료 하 여 만들 수는 기존 공용 IP 주소에 없으면 [공용 IP 주소 리소스를 만들](#create-public-ip) 이 문서의 섹션.
3. Hello 새 IP 구성 검토 합니다.
4. 클릭할 수 있는 **추가** 추가 IP 구성을 tooadd 닫기 열려 있는 모든 블레이드 toofinish 추가 IP 주소 또는 합니다. Hello 공용 IP 주소 toohello 운영 체제를 추가 하지 마십시오.


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
