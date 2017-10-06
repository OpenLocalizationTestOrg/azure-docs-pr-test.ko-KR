---
title: "aaaGet Azure 포털에서 Azure 스케줄러를 시작 합니다. | Microsoft Docs"
description: "Azure 포털에서 Azure 스케줄러 시작"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a>Azure 포털에서 Azure 스케줄러 시작
것은 Azure Scheduler에서 쉽게 toocreate 예약 된 작업입니다. 이 자습서에서는 알아봅니다 어떻게 toocreate 작업 합니다. 스케줄러의 모니터링 및 관리 기능도 알아봅니다.

## <a name="create-a-job"></a>작업 만들기
1. 역시 로그인[Azure 포털](https://portal.azure.com/)합니다.  
2. 클릭 **+ 새로 만들기** > 형식 *스케줄러* hello 검색 상자에 > 선택 **스케줄러** 결과에서 > 클릭 **만들기**합니다.
   
    ![][marketplace-create]
3. 간단히 GET 요청으로 http://www.microsoft.com/을 히트하는 작업을 만들어 보겠습니다. Hello에 **스케줄러 작업** 화면에서 다음 정보는 hello 입력:
   
   1. **이름:** `getmicrosoft`  
   2. **구독:** Azure 구독입니다.   
   3. **작업 컬렉션:** 기존 작업 컬렉션을 선택하거나 **새로 만들기**를 클릭하고 > 이름을 입력합니다.
4. 다음 **동작 설정**, hello 다음 값을 정의 합니다.
   
   1. **작업 유형:** ` HTTP`  
   2. **메서드:** `GET`  
   3. **URL:** ` http://www.microsoft.com`  
      
      ![][action-settings]
5. 마지막으로, 일정을 정의해 보겠습니다. hello 작업 작업은 일회성 작업으로 정의할 수 있지만 되풀이 일정을 선택:
   
   1. **되풀이**: `Recurring`
   2. **시작**: 오늘 날짜
   3. **되풀이 간격**: `12 Hours`
   4. **종료 날짜**: 오늘 날짜부터 이틀 후  
      
      ![][recurrence-schedule]
6. **만들기**

## <a name="manage-and-monitor-jobs"></a>작업 관리 및 모니터링
작업을 만든 후 기본 Azure 대시보드 hello에에서 나타납니다. Hello 작업 및 새 클릭 탭 뒤 hello로 창이 열립니다.

1. properties  
2. 작업 설정  
3. 일정  
4. 기록
5. 사용자
   
   ![][job-overview]

### <a name="properties"></a>properties
이 읽기 전용 속성 hello 스케줄러 작업에 대 한 hello 관리 메타 데이터를 설명합니다.

   ![][job-properties]

### <a name="action-settings"></a>작업 설정
Hello에서 작업을 클릭 하면 **작업** 화면에서는 작업 tooconfigure 있습니다. Hello에 구성 하지 않은 경우 빨리 만들기 마법사, 고급 설정을 구성할 수 있습니다.

모든 동작 유형에 대 한 hello 다시 시도 정책 및 hello 오류 시 수행할 동작을 변경할 수 있습니다.

HTTP 및 HTTPS 작업 동작 유형에 대 한 HTTP 동사를 허용 하는 hello 메서드 tooany를 변경할 수 있습니다. 있습니다 수 또한 추가, 삭제 또는 hello 헤더 및 기본 인증 정보를 변경 합니다.

저장소 큐 동작 유형에 대 한 hello 저장소 계정, 큐 이름, SAS 토큰 및 본문을 변경할 수 있습니다.

서비스 버스 동작 유형에 대 한 hello 네임 스페이스, 항목/큐 경로, 인증 설정, 전송 종류, 메시지 속성 및 메시지 본문을 변경할 수 있습니다.

   ![][job-action-settings]

### <a name="schedule"></a>일정
따라서 hello에서 만든 toochange hello 일정 원하는 경우 빨리 만들기 마법사, hello 일정을 다시 구성할 수 있습니다.

이 영업 기회 toobuild [복잡 한 일정 및 작업에서 고급 되풀이](scheduler-advanced-complexity.md)

종료 날짜 및 시간 (hello 작업이. 되풀이 되) 하는 경우 시간, 되풀이 일정 및 hello 및 hello 시작 날짜를 변경할 수 있습니다.

   ![][job-schedule]

### <a name="history"></a>기록
hello **기록** 탭에는 hello 선택한 작업에 대 한 hello 시스템의 모든 작업 실행에 대해 선택한 메트릭이 표시 됩니다. 이러한 메트릭은 스케줄러의 hello 상태에 대 한 실시간 값을 제공합니다.

1. 가동 상태  
2. 세부 정보  
3. 다시 시도 횟수
4. 발생 빈도: 첫 번째, 두 번째, 세 번째 등
5. 실행 시작 시간  
6. 실행 종료 시간
   
   ![][job-history]

실행된 tooview 클릭할 수 있습니다 해당 **기록 세부 정보**, 모든 실행에 대 한 hello 전체 응답을 포함 합니다. 이 대화 상자 toocopy hello 응답 toohello 클립보드를 허용 합니다.

   ![][job-history-details]

### <a name="users"></a>사용자
Azure RBAC(역할 기반 액세스 제어)를 통해 Azure 스케줄러에 대한 세밀한 액세스 관리가 가능합니다. 사용자 탭 toouse hello 너무 참조 하는 방법 toolearn[신속히 알아봅니다 액세스 제어](../active-directory/role-based-access-control-configure.md)

## <a name="see-also"></a>참고 항목
 [스케줄러란?](scheduler-intro.md)

 [스케줄러 개념, 용어 및 엔터티 계층 구조](scheduler-concepts-terms.md)

 [Azure 스케줄러의 버전 및 요금 청구](scheduler-plans-billing.md)

 [일정을 toobuild 복잡 한 방법 및 Azure 스케줄러와 고급 되풀이](scheduler-advanced-complexity.md)

 [스케줄러 REST API 참조](https://msdn.microsoft.com/library/mt629143)

 [스케줄러 PowerShell Cmdlet 참조](scheduler-powershell-reference.md)

 [스케줄러 고가용성 및 안정성](scheduler-high-availability-reliability.md)

 [스케줄러 제한, 기본값 및 오류 코드](scheduler-limits-defaults-errors.md)

 [스케줄러 아웃바운드 인증](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
