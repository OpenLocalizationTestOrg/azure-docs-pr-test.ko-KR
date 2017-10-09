---
title: "aaaWhat은 Azure 스케줄러는? | Microsoft Docs"
description: "Azure 스케줄러 있습니다 toodeclaratively hello 클라우드에서 toorun 동작에 설명 합니다. 그런 다음 해당 작업을 예약하고 자동으로 실행합니다."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a>Azure 스케줄러 정의
Azure 스케줄러 있습니다 toodeclaratively hello 클라우드에서 toorun 동작에 설명 합니다. 그런 다음 해당 작업을 예약하고 자동으로 실행합니다.  스케줄러가 작업을 사용 하 여 수행 [Azure 포털 hello](scheduler-get-started-portal.md), 코드, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), 또는 Azure PowerShell.

스케줄러는 예약된 작업을 만들고 유지 관리하며 호출합니다.  스케줄러는 작업을 호스트하거나 코드를 실행하지 않습니다. Azure, 온-프레미스 또는 다른 공급자를 통해 다른 곳에서 호스트되는 코드를 *호출*하기만 합니다. HTTP, HTTPS, 저장소 큐, 서비스 버스 큐 또는 서비스 버스 항목을 통해 호출합니다.

스케줄러 일정 [작업](scheduler-concepts-terms.md), 하나를 검토할 수, 및 일정 작업 toobe 실행 명확 하 게 하 고 안정적으로 작업 실행 결과 기록을 보관 합니다. Azure WebJobs (Azure 앱 서비스의 웹 응용 프로그램 기능 hello의 일부) 및 기타 Azure 예약 기능 hello 백그라운드에서 스케줄러를 사용 합니다. hello [스케줄러 REST API](https://msdn.microsoft.com/library/mt629143.aspx) 사용 하면 이러한 작업에 대 한 hello 통신을 관리 합니다. 이와 같이 스케줄러는 [복잡한 일정 및 고급 되풀이](scheduler-advanced-complexity.md) 를 간편하게 지원합니다.

스케줄러의 toohello 사용량을 활용 하는 몇 가지 시나리오가 있습니다. 예:

* *응용 프로그램 작업 되풀이:* 주기적으로 Twitter에서 피드로 데이터를 수집합니다.
* *일별 유지 관리:* 일별 로그 잘라내기, 백업 수행 및 기타 유지 관리 작업입니다. 예를 들어 관리자가 수도 tooback hello 데이터베이스를 오전 1 시에 매일 hello에 대 한 다음 9 개월입니다.

스케줄러에서는 toocreate, 업데이트, 삭제, 보기 및 작업 관리 및 [작업 컬렉션을](scheduler-concepts-terms.md) hello 포털 및 스크립트를 사용 하 여 프로그래밍 방식으로 합니다.

## <a name="see-also"></a>참고 항목
 [Azure 스케줄러 개념, 용어 및 엔터티 계층 구조](scheduler-concepts-terms.md)

 [Hello Azure 포털에서에서 스케줄러 사용 시작](scheduler-get-started-portal.md)

 [Azure 스케줄러의 버전 및 요금 청구](scheduler-plans-billing.md)

 [일정을 toobuild 복잡 한 방법 및 Azure 스케줄러와 고급 되풀이](scheduler-advanced-complexity.md)

 [Azure 스케줄러 REST API 참조](https://msdn.microsoft.com/library/mt629143)

 [Azure 스케줄러 PowerShell cmdlet 참조](scheduler-powershell-reference.md)

 [Azure 스케줄러 고가용성 및 안정성](scheduler-high-availability-reliability.md)

 [Azure 스케줄러 제한, 기본값 및 오류 코드](scheduler-limits-defaults-errors.md)

 [Azure 스케줄러 아웃바운드 인증](scheduler-outbound-authentication.md)

