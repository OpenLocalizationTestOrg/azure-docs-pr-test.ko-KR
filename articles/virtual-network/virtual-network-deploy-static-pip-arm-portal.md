---
title: "고정 공용 IP 주소를 사용하는 VM 만들기 - Azure Portal | Microsoft Docs"
description: "Azure Portal을 사용하여 고정 공용 IP 주소를 사용하는 VM을 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 233e4eea8439320c1c7446e2c2b2e9d379351a3e
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-portal"></a>Azure Portal을 사용하여 고정 공용 IP 주소를 사용하는 VM 만들기

> [!div class="op_single_selector"]
> * [Azure 포털](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [템플릿](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell(클래식)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 클래식 배포 모델 대신 이 모델을 사용하도록 권장합니다.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a>고정 공용 IP를 사용하여 VM 만들기

Azure Portal에 고정 공용 IP 주소가 있는 VM을 만들려면 다음 단계를 완료합니다.

1. 브라우저에서 [Azure 포털](https://portal.azure.com) 로 이동하고 필요한 경우 Azure 계정으로 로그인합니다.
2. 포털의 왼쪽 맨 위에서 **새로 만들기**>>**계산**>**Windows Server 2012 R2 Datacenter**를 차례로 클릭합니다.
3. **배포 모델 선택** 목록에서 **리소스 관리자**를 선택하고 **만들기**를 클릭합니다.
4. **기본 사항** 블레이드에서 아래와 같이 VM 정보를 입력한 다음 **확인**을 클릭합니다.
   
    ![Azure 포털 - 기본 사항](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. **크기 선택** 블레이드에서 아래와 같이 **A1 표준**을 클릭한 다음 **선택**을 클릭합니다.
   
    ![Azure 포털 - 크기 선택](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. **설정** 블레이드에서 **공용 IP 주소**를 클릭한 다음 **공용 IP 주소 만들기** 블레이드의 **할당**에서 아래와 같이 **고정**을 클릭합니다. 그런 다음 **확인**을 클릭합니다.
   
    ![Azure 포털 - 공용 IP 주소 만들기](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. **설정** 블레이드에서 **확인**을 클릭합니다.
8. 아래와 같이 **요약** 블레이드를 검토한 다음 **확인**을 클릭합니다.
   
    ![Azure 포털 - 공용 IP 주소 만들기](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. 대시보드에서 새 타일을 확인합니다.
   
    ![Azure 포털 - 공용 IP 주소 만들기](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. VM이 만들어지면 아래와 같이 **설정** 블레이드가 표시됩니다.
    
    ![Azure 포털 - 공용 IP 주소 만들기](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

