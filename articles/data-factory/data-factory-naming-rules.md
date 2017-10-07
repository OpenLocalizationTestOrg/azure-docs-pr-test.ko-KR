---
title: "Azure Data Factory 엔터티 이름을 지정 하는 것에 대 한 aaaRules | Microsoft Docs"
description: "데이터 팩터리 엔터티에 대한 이름 지정 규칙을 설명합니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a>Azure Data Factory - 이름 지정 규칙
다음 표에서 hello 데이터 팩터리 아티팩트의 명명 규칙을 제공 합니다.

| 이름 | 이름 고유성 | 유효성 검사 |
|:--- |:--- |:--- |
| 데이터 팩터리 |Microsoft Azure에서 고유합니다. 이름은 대/소문자, 즉, `MyDF` 및 `mydf` toohello 참조 같은 데이터 팩터리입니다. |<ul><li>각 데이터 팩터리는 동 점된 tooexactly 단일 Azure 구독.</li><li>개체 이름은 문자 또는 숫자로 시작 해야 하며 문자, 숫자 및 hello 대시 (-) 문자만 포함할 수 있습니다.</li><li>모든 대시(-) 문자는 앞뒤에 문자 또는 숫자가 와야 합니다. 컨테이너 이름에서 연속 대시는 허용되지 않습니다.</li><li>이름은 3-63자까지 가능합니다.</li></ul> |
| 연결된 서비스/테이블/파이프라인 |데이터 팩터리에서 고유합니다. 이름은 대/소문자를 구분하지 않습니다. |<ul><li>테이블 이름에서 최대 문자 수는 260개입니다.</li><li>개체 이름은 문자, 숫자 또는 밑줄(_)로 시작해야 합니다.</li><li>사용할 수 없는 문자: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |
| 리소스 그룹 |Microsoft Azure에서 고유합니다. 이름은 대/소문자를 구분하지 않습니다. |<ul><li>최대 문자 수: 1,000개</li><li>이름은 문자, 숫자 및 hello 문자를 포함할 수 있습니다: "-", "_",","및"."</li></ul> |

