---
title: "aaaCreate 네트워크 보안 그룹-Azure 포털 | Microsoft Docs"
description: "자세한 내용은 어떻게 toocreate hello Azure 포털을 사용 하 여 네트워크 보안 그룹을 배포 합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5bc8fc2e-1e81-40e2-8231-0484cd5605cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74ecc7db06bb69f2041aa64d7b38b63eb379a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-portal"></a>네트워크 보안 그룹 hello Azure 포털을 사용 하 여 만들기

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다. 수도 있습니다 [hello 클래식 배포 모델에서 Nsg를 만들](virtual-networks-create-nsg-classic-ps.md)합니다.

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

위의 hello 시나리오를 기반으로 hello 예제 PowerShell 명령 아래에 이미 만든 단순한 환경 필요 합니다. 이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축 배포 하 여 [이 서식 파일](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), 클릭 **tooAzure 배포**, 대체 hello 기본 매개 변수 값 필요한 경우, 및의 지침에 따라 hello hello 포털 하는 경우. hello 단계를 사용 하 여 아래 **RG NSG** hello 리소스 그룹 hello 템플릿의 이름을 hello에 배포 되었습니다.

## <a name="create-hello-nsg-frontend-nsg"></a>Hello NSG 프런트 엔드 NSG 만들기
toocreate hello **NSG 프런트 엔드** NSG 위의 hello 시나리오와 같이 hello 아래의 단계를 수행 합니다.

1. 브라우저에서 toohttp://portal.azure.com를 탐색 하 고, 필요한 경우 Azure 계정을 사용해 합니다.
2. **찾아보기>** > **네트워크 보안 그룹**을 클릭합니다.
   
    ![Azure Portal - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. Hello에 **네트워크 보안 그룹** 블레이드에서 클릭 **추가**합니다.
   
    ![Azure Portal - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. Hello에 **네트워크 보안 그룹 만들기** 블레이드에서 라는 NSG 만들기 *NSG 프런트 엔드* hello에 *RG NSG* 리소스 그룹을 클릭 한 다음 **만들기**.
   
    ![Azure Portal - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a>기존 NSG에서 규칙 만들기
hello Azure 포털에서에서 기존 NSG에서 규칙 toocreate 아래 hello 단계를 따릅니다.

1. **찾아보기 >** > **네트워크 보안 그룹**을 클릭합니다.
2. Nsg의 hello 목록에서 클릭 **NSG 프런트 엔드** > **인바운드 보안 규칙**
   
    ![Azure Portal - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. Hello 목록이 **인바운드 보안 규칙**, 클릭 **추가**합니다.
   
    ![Azure Portal - 규칙 추가](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. Hello에 **인바운드 보안 규칙 추가** 블레이드에서 라는 규칙을 만들 *웹 규칙* 의 우선 순위를 가진 *200* 를 통해 액세스할 수 있도록 *TCP* tooport *80* tooany VM에서 소스를 선택한 다음 **확인**합니다. 이러한 설정 중 대부분은 이미 기본값입니다.
   
    ![Azure Portal - 규칙 설정](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. 몇 초 후 hello hello NSG에에서 새 규칙이 표시 됩니다.
   
    ![Azure Portal - 새 규칙](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. 단계를 반복 too6 toocreate 라는 인바운드 규칙 *rdp 규칙* 의 우선 순위를 가진 *250* 를 통해 액세스할 수 있도록 *TCP* tooport *3389* 모든 소스에서 VM tooany 합니다.

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a>Hello NSG toohello 프런트 엔드 서브넷 연결
1. **찾아보기 >** > **리소스 그룹** > **RG-NSG**를 클릭합니다.
2. Hello에 **RG NSG** 블레이드에서 클릭 **중...**   >  **TestVNet**합니다.
   
    ![Azure Portal - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. Hello에 **설정** 블레이드에서 클릭 **서브넷** > **프런트 엔드** > **네트워크 보안 그룹**  >  **NSG 프런트 엔드**합니다.
   
    ![Azure Portal - 서브넷 설정](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. Hello에 **프런트 엔드** 블레이드에서 클릭 **저장**합니다.
   
    ![Azure Portal - 서브넷 설정](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a>Hello NSG 백 엔드 NSG 만들기
toocreate hello **NSG 백 엔드** NSG 연결 toohello **백 엔드** 서브넷, 아래 hello 단계 수행 합니다.

1. 단계를 반복 hello [만들기 hello NSG 프런트 엔드 NSG](#Create-the-NSG-FrontEnd-NSG) toocreate 라는 NSG *NSG 백 엔드*
2. 단계를 반복 hello [기존 NSG에서 규칙을 만들](#Create-rules-in-an-existing-NSG) toocreate hello **인바운드** hello 테이블 아래에 규칙입니다.
   
   | 인바운드 규칙 | 아웃바운드 규칙 |
   | --- | --- |
   | ![Azure Portal - 인바운드 규칙](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure Portal - 아웃바운드 규칙](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. 단계를 반복 hello [hello NSG toohello 프런트 엔드 서브넷 연결](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG 백 엔드** NSG toohello **백 엔드** 서브넷입니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[기존 Nsg를 관리 합니다.](virtual-network-manage-nsg-arm-portal.md)
* [로깅을 사용합니다](virtual-network-nsg-manage-log.md) .

