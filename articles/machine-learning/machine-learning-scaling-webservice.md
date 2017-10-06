---
title: "Azure 기계 학습 웹 서비스의 aaaHow tooincrease 동시성 | Microsoft Docs"
description: "추가 끝점을 추가 하 여 Azure 기계 학습의 tooincrease 동시성 서비스 웹 하는 방법을 알아봅니다."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "azure 기계 학습, 웹 서비스, 조작화, 확장, 끝점, 동시성"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a>끝점을 추가하여 Azure Machine Learning 웹 서비스 확장
> [!NOTE]
> 이 항목에서는 기술을 적용 가능한 tooa 설명 **클래식** 컴퓨터 학습 웹 서비스입니다. 
> 
> 

기본적으로 각 게시 된 웹 서비스 구성된 toosupport 동시 요청 수가 20 이며 최대 동시 요청 수가 200 될 수 있습니다. Hello Azure 클래식 포털 방식으로 tooset이이 값을 제공 하며, Azure 기계 학습에는 자동으로 hello 설정을 tooprovide hello 최상의 성능을 웹 서비스에 대 한 최적화 하 고 hello 포털 값은 무시 됩니다. 

최대 동시 호출 값 200은 지 원하는 것 보다 더 높은 부하를 사용 하 여 toocall hello API를 사용 하도록 하려는 경우 여러 끝점 hello에 만들어야 동일한 웹 서비스입니다. 그런 다음 모든 끝점에 부하를 무작위로 분산해야 합니다.

hello 웹 서비스의 크기를 조정 하는 것은 일반적인 작업입니다. 몇 가지 이유로 tooscale는 동시 요청 수가 200 보다 toosupport, 여러 끝점을 통해 가용성을 높여 주는 또는 hello 웹 서비스에 대 한 별도 끝점을 제공 합니다. Hello에 대 한 추가 끝점을 추가 하 여 hello 비율을 늘릴 수 같은 웹 서비스를 통해 [Azure 클래식 포털](https://manage.windowsazure.com/) 또는 hello [Azure 기계 학습 웹 서비스](https://services.azureml.net/) 포털입니다.

새로운 끝점 추가에 대한 자세한 내용은 [끝점 만들기](machine-learning-create-endpoint.md)를 참조하세요.

높은 동시성 count를 사용 하 여 비율이 높음까지 hello API를 호출 하지 하는 경우에 저하 될 수 있는 점을 염두에 두십시오. 드물게 시간 제한 및/또는 스파이크 높은 부하에 대해 구성 된 API에 상대적으로 낮은 부하를 두면 hello 대기 시간에 표시 될 수 있습니다.

hello 동기 Api는 일반적으로 짧은 대기 시간을 원할 경우 상황에 사용 됩니다. 대기 시간 여기 의미 hello 시간 hello API toocomplete 하나의 요청에 대 한 사용 하 고 모든 네트워크 지연을 고려 하지 않습니다. 대기 시간이 50ms인 API가 있다고 가정합시다. hello 높은 제한 수준으로 사용 가능한 용량 및 최대 동시 호출 toofully 소비할 = 20, toocall 20 * 1000이이 API를 해야 / 초 당 50 = 400 시간. 이 확장 추가, 200의 최대 동시 호출 수 toocall hello API 4000 마다 한 번을 50 ms 대기 시간을 가정 하는 두 번째 수 있습니다.

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
