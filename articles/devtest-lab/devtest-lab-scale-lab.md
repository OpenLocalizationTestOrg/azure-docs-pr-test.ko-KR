---
title: "aaaScale 할당량 및 제한 Azure DevTest Labs 랩에서 | Microsoft Docs"
description: "자세한 내용은 방법 tooscale Azure DevTest Labs에 랩"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a>DevTest Labs의 할당량 및 한도 규모 조정
DevTest Labs를 사용할 때는 개가 특정 기본 제한 toosome hello DevTest Labs 서비스에 영향을 줄 수 있는 Azure 리소스를 확인할 수 있습니다. 이러한 제한은 참조 tooas **할당량**합니다.

> [!NOTE]
> hello DevTest Labs 서비스 할당량을 적용 하지 않습니다. 발생할 수 있는 할당량은 기본 제약 조건이 hello 전체 Azure 구독입니다.

할당량에 도달할 때까지 각 Azure 리소스를 사용할 수 있습니다. 각 구독에는 별도의 할당량이 있으며 구독마다 사용량이 추적됩니다.

예를 들어 각 구독의 기본 할당량은 20 코어입니다. 따라서 랩에서 코어가 4개인 VM을 만드는 경우 총 5개의 VM을 만들 수 있습니다. 

[Azure 구독 및 서비스 제한](https://docs.microsoft.com/azure/azure-subscription-service-limits) hello Azure 리소스에 대 한 가장 일반적인 할당량 중 일부를 나열 합니다. 랩 환경에서는 가장 일반적으로 사용 되는 리소스를 hello 및 할당량 포함 VM 코어, 공용 IP 주소, 네트워크 인터페이스, 관리 하는 디스크, RBAC 역할 할당 및 express 경로 회로 발생할 수 있습니다.

## <a name="view-your-usage-and-quotas"></a>사용량 및 할당량 보기
이러한 단계 어떻게 tooview hello toosee 및 특정 Azure 리소스에 대 한 구독에서 현재 할당량 사용한 각 할당량의 비율을 보여 줍니다.

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
1. 선택 **더 서비스**를 선택한 후 **청구** hello 목록에서 합니다.
1. Hello [결제] 블레이드에서 구독을 선택 합니다.
4. **사용량 + 할당량**을 선택합니다.

   ![사용량 및 할당량 단추](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   사용 현황 + 할당량 hello 블레이드 표시 되 면 해당 구독 및 hello 비율로 리소스 당 사용 되는 hello 할당량에서 사용할 수 있는 다른 리소스를 나열 합니다.

   ![할당량 및 사용량](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a>구독에 더 많은 리소스 요청
에 설명 된 대로 tooa 최대치를 구독에 있는 리소스의 hello 기본도 늘릴 수는 할당량 끝에 도달 하면 [Azure 구독 및 서비스 제한](https://docs.microsoft.com/azure/azure-subscription-service-limits)합니다.

이러한 단계에서는 보여 toorequest 할당량을 늘리려면 어떻게 hello를 통해 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.

1. **추가 서비스**, **청구**, **사용량 + 할당량**을 차례로 선택합니다.
1. 안녕하세요 사용 + 할당량 블레이드 선택 hello **증가 요청** 단추입니다.

   ![증가 요청 단추](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. toocomplete hello 요청을 제출, hello의 세 탭 모두에 hello 필요한 정보를 입력 하 고 **새로운 지원 요청** 폼입니다.

   ![증가 요청 양식](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

[이해 Azure 제한 및 증가](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) 할당량 toorequest Azure 지원에 연락 하는 방법에 대 한 자세한 정보를 제공 합니다. 증가 합니다.



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>다음 단계
* Hello 탐색 [DevTest Labs Azure 리소스 관리자 퀵 스타트 템플릿 갤러리](https://github.com/Azure/azure-devtestlab/tree/master/Samples)합니다.
