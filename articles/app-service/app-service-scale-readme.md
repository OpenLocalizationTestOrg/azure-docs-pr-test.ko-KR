---
title: "Azure 앱 서비스: 앱 서비스 응용 프로그램 크기 조정"
description: "Hello의 장단점 앱 서비스의 응용 프로그램을 확장에 대해 알아봅니다."
keywords: "앱 서비스, Azure 앱 서비스, 규모, 확장성, 앱 서비스 계획, 앱 서비스 비용"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Azure 앱 서비스: 앱 서비스 응용 프로그램 크기 조정
Azure 앱 서비스에서 호스팅되는 응용 프로그램은 [대규모로 확장](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/)할 수 있습니다.
하지만 응용 프로그램의 크기를 조정하는 작업은 "보편적으로 적용되는" 솔루션이 없는 복잡한 문제입니다. 응용 프로그램을 확장 하는 toocorrectly 3 주요 영역을 가장 기본적 주지 tooyour 응용 프로그램 성공:

1. 응용 프로그램 아키텍처와 약점 이해
   * 응용 프로그램이 상태 저장인가요? 상태 비저장인가요?
   * 응용 프로그램의 모든 hello 구성 요소는 무엇입니까?
     * Hello 응용 프로그램의 hello 병목 상태를 어디 입니까?
   * 부하는 적용 된 tooyour 앱 첫 번째 끊긴다는 무엇입니까?
2. 이해 hello 부하 및 성능 요구 사항을 예상 합니다.
   * Tooserve 하나 천 사용자 hello 응용 프로그램에 필요 합니까? 또는 1 백만?
   * 트래픽이 단일 지리적 위치에서 생기나요? 아니면 전역적으로 생기나요?
   * 계절적 변동이 있나요? 트래픽 정점이 있나요?
   * Hello 응용 프로그램 응답 속도 1초? 1밀리초인가요?
3. 이해 및 제대로 활용 하 여 hello 플랫폼 호스팅 응용 프로그램입니다.
   * 기능의 해야 tooachieve 내 눈금 목표를 활용 하나요?

이 섹션은 모든 hello 요인과 hello 필요한 앱 서비스 기능 tooachieve 확장성 목표를 활용 하는 전략을 고안 도움말을 이해 하는 데 도움이 됩니다.

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

