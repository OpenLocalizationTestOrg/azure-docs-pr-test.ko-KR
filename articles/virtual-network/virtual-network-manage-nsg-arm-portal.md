---
title: "hello Azure 포털을 사용 하 여 aaaManage Nsg | Microsoft Docs"
description: "자세한 내용은 방법 toomanage hello Azure 포털을 사용 하 여 Nsg를 기존 합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a>Hello 포털을 사용 하 여 Nsg를 관리 합니다.

> [!div class="op_single_selector"]
> * [포털](virtual-network-manage-nsg-arm-portal.md)
> * [PowerShell](virtual-network-manage-nsg-arm-ps.md)
> * [Azure CLI](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 Microsoft hello 클래식 배포 모델 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a>정보 검색
기존 NSG를 보고 기존 NSG에 대한 규칙을 검색하며 NSG가 연결된 리소스에 대해 알아볼 수 있습니다.

### <a name="view-existing-nsgs"></a>기존 NSG 보기

tooview 모든 단계를 수행 하는 전체 hello 구독에서 Nsg를 기존:

1. 브라우저에서 toohttp://portal.azure.com를 탐색 하 고, 필요한 경우 Azure 계정을 사용해 합니다.

2. **찾아보기 >** > **네트워크 보안 그룹**을 클릭합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. Hello Nsg의 hello 목록을 확인 **네트워크 보안 그룹** 블레이드입니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a>리소스 그룹에서 NSG 보기

Nsg의 hello tooview hello 목록 **RG NSG** 리소스 그룹, 단계를 수행 하는 전체 hello:

1. **리소스 그룹 >** > **RG-NSG** > **...**을 클릭합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. 리소스의 hello 목록에서 항목을 찾을 hello NSG 아이콘 표시 hello에 나와 있는 것 처럼 **리소스** 블레이드 아래 합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a>NSG에 대한 모든 규칙 나열

명명 된 NSG의 tooview hello 규칙 **NSG 프런트 엔드**완료, 다음 단계 hello:

1. Hello에서 **네트워크 보안 그룹** 블레이드에서 또는 hello **리소스** 위에 표시 된 블레이드 클릭 **NSG 프런트 엔드**합니다.

2. Hello에 **설정** 탭을 클릭 **인바운드 보안 규칙**합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. hello **인바운드 보안 규칙** 블레이드는 아래와 같이 표시 됩니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. Hello에 **설정** 탭을 클릭 **아웃 바운드 보안 규칙** toosee hello 아웃 바운드 규칙입니다.

    > [!NOTE]
    > tooview 기본 규칙을 클릭 하 여 hello **규칙 기본** hello hello 규칙을 표시 하는 hello 블레이드 맨 위에 있는 아이콘입니다.
    >

### <a name="view-nsgs-associations"></a>NSG 연결 보기

tooview 어떤 리소스 hello **NSG 프런트 엔드** NSG는 다음 단계와 연결 하 고 완전 hello:

1. Hello에서 **네트워크 보안 그룹** 블레이드에서 또는 hello **리소스** 위에 표시 된 블레이드 클릭 **NSG 프런트 엔드**합니다.

2. Hello에 **설정** 탭을 클릭 **서브넷** 어떤 서브넷은 tooview toohello NSG를 연결 합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. Hello에 **설정** 탭을 클릭 **네트워크 인터페이스** tooview Nic 이란 관련 toohello NSG 합니다.

## <a name="manage-rules"></a>규칙 관리
기존 NSG 규칙 tooan 추가, 기존 규칙을 편집 하 고 규칙을 제거할 수 있습니다.

### <a name="add-a-rule"></a>규칙 추가
허용 하는 규칙 tooadd **인바운드** 트래픽 tooport **443** 모든 컴퓨터 toohello에서 **NSG 프런트 엔드** NSG, 단계를 수행 하는 전체 hello:

1. Hello에서 **네트워크 보안 그룹** 블레이드에서 또는 hello **리소스** 위에 표시 된 블레이드 클릭 **NSG 프런트 엔드**합니다.
2. Hello에 **설정** 탭을 클릭 **인바운드 보안 규칙**합니다.
3. Hello에 **인바운드 보안 규칙** 블레이드에서 클릭 **추가**합니다. 그런 다음, hello **인바운드 보안 규칙 추가** 블레이드에서 아래와 같이 hello 값을 작성 한 다음 클릭 **확인**합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    몇 초 후 hello hello에서 새 규칙을 확인 **인바운드 보안 규칙** 블레이드입니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a>규칙 변경
tooallow 위에서 만든 toochange hello 규칙 hello에서 트래픽 인바운드 **인터넷** 단계를 수행 하는 유일한, 전체 hello:

1. Hello에서 **네트워크 보안 그룹** 블레이드에서 또는 hello **리소스** 위에 표시 된 블레이드 클릭 **NSG 프런트 엔드**합니다.
2. Hello에 **설정** 탭에서 위에서 만든 hello 규칙을 클릭 합니다.
3. Hello에 **허용 https** 블레이드, 변경 hello **소스** 아래와 같이 속성을 클릭 한 다음 **저장**합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a>규칙 삭제

toodelete hello 규칙 위에서 만든, 전체 hello 단계를 수행 합니다.

1. Hello에서 **네트워크 보안 그룹** 블레이드에서 또는 hello **리소스** 위에 표시 된 블레이드 클릭 **NSG 프런트 엔드**합니다.
2. Hello에 **설정** 탭에서 위에서 만든 hello 규칙을 클릭 합니다.
3. Hello에 **허용 https** 블레이드에서 클릭 **삭제**, 클릭 하 고 **예**합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a>연결 관리
NSG toosubnets 및 Nic를 연결할 수 있습니다. 또한 연결된 모든 리소스에서 NSG를 분리할 수 있습니다.

### <a name="associate-an-nsg-tooa-nic"></a>NSG tooa NIC에 연결
tooassociate hello **NSG 프런트 엔드** NSG toohello **TestNICWeb1** NIC를 다음 단계 완료 hello:

1. Hello에서 **네트워크 보안 그룹** 블레이드에서 또는 hello **리소스** 위에 표시 된 블레이드 클릭 **NSG 프런트 엔드**합니다.
2. Hello에 **설정** 탭을 클릭 **네트워크 인터페이스** > **연결** > **TestNICWeb1**합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a>NIC에서 NSG 분리

toodissociate hello **NSG 프런트 엔드** hello에서 NSG **TestNICWeb1** NIC를 다음 단계 완료 hello:

1. Hello Azure 포털에서에서 클릭 **리소스 그룹 >** > **RG NSG** > **...**   >  **TestNICWeb1**합니다.

2. Hello에 **TestNICWeb1** 블레이드에서 클릭 **의 보안 변경 중...**   >  **None**합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> 기존 NSG이 블레이드 tooassociate hello NIC tooany를 사용할 수 있습니다.
>

### <a name="dissociate-an-nsg-from-a-subnet"></a>서브넷에서 NSG 분리

toodissociate hello **NSG 프런트 엔드** hello에서 NSG **프런트 엔드** 서브넷, 단계를 수행 하는 전체 hello:

1. Hello Azure 포털에서에서 클릭 **리소스 그룹 >** > **RG NSG** > **...**   >  **TestVNet**합니다.

2. Hello에 **설정** 블레이드에서 클릭 **서브넷** > **프런트 엔드** > **네트워크 보안 그룹**  >  **None**합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. Hello에 **프런트 엔드** 블레이드에서 클릭 **저장**합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a>NSG tooa 서브넷 연결

tooassociate hello **NSG 프런트 엔드** NSG toohello **FronEnd** 다시 서브넷, 단계를 수행 하는 전체 hello:

1. Hello Azure 포털에서에서 클릭 **리소스 그룹 >** > **RG NSG** > **...**   >  **TestVNet**합니다.
2. Hello에 **설정** 블레이드에서 클릭 **서브넷** > **프런트 엔드** > **네트워크 보안 그룹**  >  **NSG 프런트 엔드**합니다.
3. Hello에 **프런트 엔드** 블레이드에서 클릭 **저장**합니다.

> [!NOTE]
> Thh NSG의에서 한 NSG tooa 서브넷에 연결할 수도 있습니다 **설정을** 블레이드입니다.
>

## <a name="delete-an-nsg"></a>NSG 삭제
NSG tooany 리소스를 연결 되지 않은 경우에 삭제할 수 있습니다. 다음 단계 완료 hello NSG toodelete: 합니다.

1. Hello Azure 포털에서에서 클릭 **리소스 그룹 >** > **RG NSG** > **...**   >  **NSG 프런트 엔드**합니다.
2. Hello에 **설정** 블레이드에서 클릭 **네트워크 인터페이스**합니다.
3. 나열 된 모든 Nic가 없을 경우 hello NIC를 클릭 하 고에 2 단계에 따라 [NIC에서 NSG를 분리](#Dissociate-an-NSG-from-a-NIC)합니다.
4. 각 NIC에 3단계를 반복합니다.
5. Hello에 **설정** 블레이드에서 클릭 **서브넷**합니다.
6. 나열 된 모든 서브넷에 있는 경우 hello 서브넷을 클릭 하 고 2와 3 단계에 따라 [서브넷에서 NSG를 분리](#Dissociate-an-NSG-from-a-subnet)합니다.
7. 왼쪽된 toohello 스크롤합니다 **NSG 프런트 엔드** 블레이드에서 클릭 **삭제** > **예**합니다.

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a>다음 단계
* [로깅을 사용합니다](virtual-network-nsg-manage-log.md) .
