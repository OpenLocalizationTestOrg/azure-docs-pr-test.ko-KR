---
title: "고정 공용 IP 주소-Azure 포털을 사용 하 여 VM aaaCreate | Microsoft Docs"
description: "고정 공용 IP 주소를 사용 하 여 사용 하 여 VM toocreate Azure 포털 hello 하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a>고정 공용 IP 주소로 hello Azure 포털을 사용 하 여 VM 만들기

> [!div class="op_single_selector"]
> * [Azure 포털](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [템플릿](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell(클래식)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 Microsoft hello 클래식 배포 모델 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a>고정 공용 IP를 사용하여 VM 만들기

단계를 수행 하는 전체 hello hello Azure 포털의에서 주소는 고정 공용 IP 사용 하 여 VM이 toocreate:

1. 브라우저에서 탐색 toohello [Azure 포털](https://portal.azure.com) 및 필요에 따라 Azure 계정으로 로그인 합니다.
2. Hello 포털의 왼쪽 위 모서리 hello 클릭 **새로**>>**계산**>**Windows Server 2012 R2 Datacenter**합니다.
3. Hello에 **배포 모델 선택** 목록에서 선택 **리소스 관리자** 클릭 **만들기**합니다.
4. Hello에 **기본 사항** 블레이드에서 아래와 같이 hello VM 정보를 입력 한 다음 클릭 **확인**합니다.
   
    ![Azure 포털 - 기본 사항](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. Hello에 **크기를 선택** 블레이드에서 클릭 **표준 A1** 아래와 같이 다음를 클릭 하 고 **선택**합니다.
   
    ![Azure 포털 - 크기 선택](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. Hello에 **설정** 블레이드에서 클릭 **공용 IP 주소**, hello에 다음 **공용 IP 주소 만들기** 블레이드 아래 **할당**, 클릭 **정적** 다음과 같이 합니다. 그런 다음 **확인**을 클릭합니다.
   
    ![Azure 포털 - 공용 IP 주소 만들기](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. Hello에 **설정** 블레이드에서 클릭 **확인**합니다.
8. 검토 hello **요약** 블레이드에서 아래와 같이 하 고 클릭 한 다음 **확인**합니다.
   
    ![Azure 포털 - 공용 IP 주소 만들기](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. Hello 대시보드에서 새 타일을 확인 합니다.
   
    ![Azure 포털 - 공용 IP 주소 만들기](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. Hello VM을 만든 후 hello **설정을** 블레이드는 아래와 같이 표시 됩니다
    
    ![Azure 포털 - 공용 IP 주소 만들기](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

