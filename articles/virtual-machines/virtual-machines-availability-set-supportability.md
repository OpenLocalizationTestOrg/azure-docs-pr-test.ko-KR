---
title: "Azure Vm tooan 기존 가용성 집합을 추가 하는 aaaSupportability | Microsoft Docs"
description: "Azure Vm tooan 기존 가용성 집합을 추가 하는 지원 가능성을 고려 합니다."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a>Azure Vm tooan 기존 가용성 집합을 추가 하는 지원 가능성

제한 사항 새 가상 컴퓨터 (Vm) tooan 기존 가용성 집합을 추가 하는 경우에 가끔 발생할 수 있습니다. 다음 차트 세부 정보에서 혼합할 수 있는 VM 시리즈 hello 동일한 가용성 집합 번호입니다.

Hello 지원 가능성 매트릭스 toomix 다양 한 유형의 Vm 다음과 같습니다.

시리즈 및 가용성 집합|두 번째 VM|A|Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|첫 번째 VM|||||||
|A||확인|확인|확인|확인|확인|
|Av2||확인|확인|확인|확인|확인|
|D||확인|확인|확인|확인|확인|
|Dv2||확인|확인|확인|확인|확인|
|Dv3||확인|확인|확인|확인|확인|

다른 모든 계열이 hello 특정 하드웨어 필요 하기 때문에 동일한 가용성 집합의 수는 없습니다.
