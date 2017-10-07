---
title: "Azure에서 Windows 클라이언트 이미지의 aaaUse | Microsoft Docs"
description: "Visual Studio 구독 toouse 개발/테스트 시나리오에 대 한 toodeploy Windows 7, Windows 8 또는 Azure에서 Windows 10을 활용 방법"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 4ac7c3d9872673030f4ea0f0ab38625dd9d9c1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a>개발/테스트 시나리오용으로 Azure에서 Windows 클라이언트 사용
적절한 Visual Studio(이전의 MSDN) 구독이 있으면 Azure에서 개발/테스트 시나리오에 Windows 7, Windows 8 또는 Windows 10을 사용할 수 있습니다. 이 문서에서는 Azure 갤러리 이미지 Azure를 사용 하 여 hello의 Windows 클라이언트를 실행 하기 위한 hello 자격 요건을 설명 합니다.

## <a name="subscription-eligibility"></a>구독 적격성
활성 Visual Studio 구독자, 즉 Visual Studio 구독 라이선스를 받은 사용자는 개발 및 테스트용으로 Windows 클라이언트를 사용할 수 있습니다. Windows 클라이언트는 모든 유형의 Azure 구독에서 실행 중인 Azure 가상 컴퓨터와 사용자의 자체 하드웨어에서 사용 가능합니다. Windows 클라이언트에 Azure 일반 프로덕션 용도로 사용 되거나 사용 Visual Studio는 활성 구독자가 아닌 사용자가 배포 된 tooor 아닐 수 있습니다.

사용자 편의 위해 기울였습니다 특정 Windows 10 이미지를 사용할 수 있는 내 hello Azure 갤러리에서 [적격 개발/테스트 제공](#eligible-offers)합니다. 제공 서비스의 모든 형식 내에서 visual Studio 구독자 수도 [적절 하 게 준비 하 고 만들](prepare-for-upload-vhd-image.md) 64 비트 Windows 7, Windows 8 또는 Windows 10 이미지를 차례로 [tooAzure 업로드](upload-generalized-managed.md)합니다. hello 사용 제한 toodev/테스트 활성 Visual Studio 구독자가 유지 됩니다.

## <a name="eligible-offers"></a>적격 제품
테이블 세부 정보 hello 다음 hello Id hello Azure 갤러리를 통해 적격 toodeploy Windows 10에 제공 합니다. Windows 10 hello 이미지는 다음 제안을 표시 toohello만입니다. Visual Studio 구독자가 필요한 toorun Windows 클라이언트에서 서로 다른 제안 유형 해야 너무[적절 하 게 준비 하 고 만들](prepare-for-upload-vhd-image.md) 64 비트 Windows 7, Windows 8 또는 Windows 10 이미지 및 [tooAzure업로드](upload-generalized-managed.md).

| 제품 이름 | 제품 번호 | 사용 가능한 클라이언트 이미지 |
|:--- |:---:|:---:|
| [종량제 개발/테스트](https://azure.microsoft.com/offers/ms-azr-0023p/) |0023P |Windows 10 |
| [Visual Studio Enterprise(MPN) 구독자](https://azure.microsoft.com/offers/ms-azr-0029p/) |0029P |Windows 10 |
| [Visual Studio Professional 구독자](https://azure.microsoft.com/offers/ms-azr-0059p/) |0059P |Windows 10 |
| [Visual Studio Test Professional 구독자](https://azure.microsoft.com/offers/ms-azr-0060p/) |0060P |Windows 10 |
| [Visual Studio Premium with MSDN(혜택)](https://azure.microsoft.com/offers/ms-azr-0061p/) |0061P |Windows 10 |
| [Visual Studio Enterprise 구독자](https://azure.microsoft.com/offers/ms-azr-0063p/) |0063P |Windows 10 |
| [Visual Studio Enterprise(BizSpark) 구독자](https://azure.microsoft.com/offers/ms-azr-0064p/) |0064P |Windows 10 |
| [Enterprise 개발/테스트](https://azure.microsoft.com/ofers/ms-azr-0148p/) |0148P |Windows 10 |

## <a name="check-your-azure-subscription"></a>Azure 구독 확인
제안 ID을 알 수 없는 경우에 hello Azure 포털에서 이러한 두 가지 방법 중 하나를 통해 얻을 수 있습니다.  

- 구독 블레이드에서 hello:

  ![Hello Azure 포털에서에서 ID 세부 정보를 제공 합니다.](./media/client-images/offer-id-azure-portal.png) 

- 또는 **청구**를 클릭하고 구독 ID를 클릭합니다. hello 제안 ID hello 결제 블레이드에 나타납니다.

Hello에서 hello 제안 ID를 볼 수도 있습니다 ['구독' 탭](http://account.windowsazure.com/Subscriptions) hello Azure 계정 포털:

![Hello Azure 계정 포털에서 ID 세부 정보를 제공 합니다.](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a>다음 단계
이제 [PowerShell](quick-create-powershell.md), [Resource Manager 템플릿](ps-template.md) 또는 [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)를 사용하여 VM을 배포할 수 있습니다.

