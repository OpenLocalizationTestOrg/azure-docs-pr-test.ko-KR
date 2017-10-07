---
title: "aaaAuto hello 클래식 포털에서 클라우드 서비스의 크기를 조정 | Microsoft Docs"
description: "(클래식) Toouse 클라우드 서비스 웹 역할 또는 작업자 역할을 Azure에 대 한 자동 크기 조정 규칙 클래식 포털 tooconfigure hello 하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a>Tooconfigure 자동 hello 클래식 포털에서 클라우드 서비스에 대 한 크기 조정 하는 방법
> [!div class="op_single_selector"]
> * [Azure 포털](cloud-services-how-to-scale-portal.md)
> * [Azure 클래식 포털](cloud-services-how-to-scale.md)

Hello 눈금 페이지 hello Azure 클래식 포털에서 웹 역할 또는 작업자 역할에 대 한 자동 크기 조정 설정을 구성할 수 있습니다. 또는 규칙 기반 자동 크기 조정 대신 수동 크기 조정을 구성할 수 있습니다.

> [!NOTE]
> 이 문서에서는 클라우드 서비스 웹 및 작업자 역할에 중점을 둡니다. 가상 컴퓨터(클래식)를 직접 만든 경우 이 가상 컴퓨터는 클라우드 서비스에서 호스트됩니다. 이 정보 중 일부에 가상 컴퓨터의 toothese 유형을 적용 합니다. 가상 컴퓨터의 가용성 집합의 크기 조정 바로 종료 되을 켜고 구성한 hello 크기 조정 규칙에 따라 있습니다. 가상 컴퓨터 및 가용성 집합에 대 한 자세한 내용은 참조 [관리 hello 가상 컴퓨터의 가용성](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Hello 응용 프로그램에 대해 크기 조정을 구성 하기 전에 다음 정보를 고려해 야 합니다.

* 크기 조정은 코어 사용량의 영향을 받습니다.

    역할 인스턴스가 클수록 더 많은 코어를 사용합니다. 구독에 대 한 hello 코어 한도 내 에서만 응용 프로그램을 확장할 수 있습니다. 예를 들어 구독의 코어 제한이 20이라고 해보겠습니다. 두 개의 중간 규모의 클라우드 서비스 (총 4 코어)와 응용 프로그램을 실행 하는 경우만 여 확장할 수 있습니다 다른 클라우드 서비스 배포를 구독에서 hello 나머지 코어 16 개. 크기에 대한 자세한 내용은 [클라우드 서비스 크기](cloud-services-sizes-specs.md)를 참조하세요.

* 메시지 임계값을 기반으로 응용 프로그램의 크기를 조정하려면 큐를 만든 후 역할에 연결해야 합니다. 자세한 내용은 참조 [어떻게 toouse hello 큐 저장소 서비스](../storage/queues/storage-dotnet-how-to-use-queues.md)합니다.

* 연결 된 tooyour 된 리소스의 크기를 조정할 수 클라우드 서비스입니다. 리소스를 연결 하는 방법에 대 한 자세한 내용은 참조 [하는 방법: 리소스 tooa 클라우드 서비스를 연결](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service)합니다.

* 응용 프로그램의 고가용성을 tooenable을 확인 해야 두 개 이상의 역할 인스턴스를 배포 합니다. 자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)을 참조하세요.

## <a name="schedule-scaling"></a>크기 조정 예약
기본적으로 모든 역할은 특정 일정을 따르지 않습니다. 따라서 모든 설정이 변경 되었습니다. tooall 시간과 hello 연도 전체에서 모든 날짜에 적용 됩니다. Hello 다음 모드 중 하나에 대 한 수동 또는 자동 크기 조정 하는 것을 설정할 수 있습니다.

* 평일
* 주말
* 주중 야간
* 주중 오전
* 특정 날짜
* 특정 날짜 범위

hello 일정 설정에에서 구성 되어 hello [Azure 클래식 포털](https://manage.windowsazure.com/) hello에  
**클라우드 서비스** > **\[클라우드 서비스\]** > **크기** > **\[프로덕션 또는 스테이징\]** 페이지)에서 구성됩니다.

Hello 클릭 **예약 시간 설정** 단추 toochange 각 역할에 대해 원하는 합니다.

![일정에 따라 클라우드 서비스 자동 크기 조정][scale_schedules]

## <a name="manual-scale"></a>수동 크기 조정
Hello에 **배율** 페이지 있습니다 수동으로 거 나 낮출 수 hello 클라우드 서비스에서 실행 되는 인스턴스 수입니다. 일정을 만들지 않은 경우이 설정은 각 생성 일정 또는 tooall 시간에 대해 구성 됩니다.

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/), 클릭 **클라우드 서비스**, hello 클라우드 서비스 tooopen hello 대시보드 hello 이름을 클릭 하 고 있습니다.
   
   > [!TIP]
   > 클라우드 서비스 보이지 않으면 toochange에서 할 수 있습니다 **프로덕션** 너무**준비** 또는 그 반대의 경우도 마찬가지입니다.

2. **크기 조정**을 클릭합니다.
3. 확장 옵션을 즐길 toochange hello 일정을 선택 합니다. *더 예약 된 시간* 정의 된 일정이 없습니다 있으면 hello 기본값입니다.
4. Hello **메트릭 별 크기 조정** 선택한 섹션 **NONE**합니다. 이 설정은 모든 역할에 대 한 hello 기본값입니다.
5. Hello 클라우드 서비스의 각 역할 인스턴스 toouse hello 수 변경에 대 한 슬라이더를 있습니다.
   
    ![클라우드 서비스 역할 크기 수동 조정][manual_scale]
   
    더 많은 인스턴스를 해야 하는 경우 toochange hello 할 수 있습니다 [클라우드 서비스가 가상 컴퓨터 크기](cloud-services-sizes-specs.md)합니다.
6. **Save**를 클릭합니다.  
   선택 사항을 기반으로 역할 인스턴스가 추가되거나 제거됩니다.

> [!TIP]
> 표시 되 면 항상 ![][tip_icon] 마우스 tooit 이동 하 고 특정 설정에 대해 도움말을 볼 수 있습니다.

## <a name="automatic-scale---cpu"></a>자동 크기 조정 - CPU
이 모드는 CPU 사용량의 평균 비율 hello가 지정 된 임계값 보다 높거나 낮은 조정 합니다. 이 경우 역할 인스턴스가 만들어지거나 삭제됩니다.

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/), 클릭 **클라우드 서비스**, hello 클라우드 서비스 tooopen hello 대시보드 hello 이름을 클릭 하 고 있습니다.
   
   > [!TIP]
   > 클라우드 서비스 보이지 않으면 toochange에서 할 수 있습니다 **프로덕션** 너무**준비** 또는 그 반대의 경우도 마찬가지입니다.

2. **크기 조정**을 클릭합니다.
3. 확장 옵션을 즐길 toochange hello 일정을 선택 합니다. *더 예약 된 시간* 정의 된 일정이 없습니다 있으면 hello 기본값입니다.
4. Hello **메트릭 별 크기 조정** 선택한 섹션 **CPU**합니다.
5. 이제 역할 인스턴스, hello 대상 CPU 사용량 (스케일 업 a tootrigger) 및 인스턴스 수 tooscale 위쪽 / 아래쪽으로 최소 및 최대 범위를 구성할 수 있습니다.

![CPU 로드에 따라 클라우드 서비스 역할 크기 조정][cpu_scale]

> [!TIP]
> 표시 되 면 항상 ![][tip_icon] 마우스 tooit 이동 하 고 특정 설정에 대해 도움말을 볼 수 있습니다.

## <a name="automatic-scale---queue"></a>자동 크기 조정 - 큐
이 모드는 hello 큐의 메시지 수가 지정 된 임계값 보다 크거나 작은 되 면 자동으로 조정 합니다. 이 경우 역할 인스턴스가 만들어지거나 삭제됩니다.

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/), 클릭 **클라우드 서비스**, hello 클라우드 서비스 tooopen hello 대시보드 hello 이름을 클릭 하 고 있습니다.
   
   > [!TIP]
   > 클라우드 서비스 보이지 않으면 toochange에서 할 수 있습니다 **프로덕션** 너무**준비** 또는 그 반대의 경우도 마찬가지입니다.

2. **크기 조정**을 클릭합니다.
3. Hello **메트릭 별 크기 조정** 선택한 섹션 **큐**합니다.
4. 이제 hello 큐 및 각 인스턴스와에서 위쪽과 아래쪽 인스턴스 tooscale 개수에 대 한 큐 메시지 tooprocess 수가 역할 인스턴스는 최소 및 최대 범위를 구성할 수 있습니다.

![메시지 큐에 따라 클라우드 서비스 역할 크기 조정][queue_scale]

> [!TIP]
> 표시 되 면 항상 ![][tip_icon] 마우스 tooit 이동 하 고 특정 설정에 대해 도움말을 볼 수 있습니다.

## <a name="scale-linked-resources"></a>연결된 리소스 크기 조정
역할을 크기를 조정 하는 경우에 종종 hello 응용 프로그램 에서도 사용 하는 유용한 tooscale hello 데이터베이스는 합니다. Hello 데이터베이스 toohello 클라우드 서비스를 연결 하는 경우 해당 리소스에 대 한 설정을 hello 적절 한 링크를 클릭 하 여 크기 조정 하는 hello를 액세스할 수 있습니다.

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/), 클릭 **클라우드 서비스**, hello 클라우드 서비스 tooopen hello 대시보드 hello 이름을 클릭 하 고 있습니다.
   
   > [!TIP]
   > 클라우드 서비스 보이지 않으면 toochange에서 할 수 있습니다 **프로덕션** 너무**준비** 또는 그 반대의 경우도 마찬가지입니다.

2. **크기 조정**을 클릭합니다.
3. Hello **연결 된 리소스** 섹션 및 클릭 **이 데이터베이스에 대 한 크기 조정 관리**합니다.
   
   > [!NOTE]
   > **연결된 리소스** 섹션이 보이지 않는 경우 연결된 리소스가 없는 것일 수 있습니다.

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
