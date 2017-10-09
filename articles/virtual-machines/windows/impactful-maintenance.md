---
title: "Azure의 Windows Vm에 대 한 유지 관리 aaaImpactful | Microsoft Docs"
description: "Windows 가상 컴퓨터를 강력하게 유지 관리합니다."
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 98afaea0fdca796177e075b33615b03f1e7a0fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="impactful-maintenance-for-virtual-machines"></a>강력한 가상 컴퓨터 유지 관리

Vm에 기본 인프라 tooplanned 유지 관리 toohello 인해 다시 부팅 되는 몇 가지 경우가 있습니다. Azure에서 호스트 Vm의 가용성을 주의깊게 toothe 되 고, hello 다음 toouse 있습니다 수 이제 있습니다.

-   알림이는 hello 영향 전에 30 일 이내에 전송 합니다.

-   각 VM 당 가시성 toohello 유지 관리 기간입니다.

-   유연성 및 hello 정확한 시간에 Vm에 영향을 주는 유지 관리에 대 한 설정에서 제어 합니다.

Microsoft Azure의 유지 관리는 반복적으로 예약됩니다. 초기 반복 순서 tooreduce hello 위험 출시 된 새로운 수정 및 기능에 관련 된 작은 범위가 있습니다. 후기 반복에서 구현 여러 영역에 걸쳐 있을 수 있습니다 (되지 hello에서에서 동일한 지역 쌍). VM은 단일 유지 관리 반복에 포함됩니다. 반복이 중단되면 나머지 VM은 미래의 다른 반복에 포함됩니다.

hello 계획 된 유지 관리 반복은 두 단계: Pre-emptive 유지 관리 기간 및 예약 된 유지 관리 기간.

hello **Pre-emptive 유지 관리 기간** Vm에 대 한 hello 유연성 tooinitiate hello 관리를 제공 합니다. 이러한 작업을 통해 Vm에는 영향을 확인, 시퀀스 hello 업데이트와 유지 되 고 각 VM 간의 hello 시간 hello 수 있습니다. 각 VM toosee 유지 관리에 대 한 계획 되어 있는지 여부를 쿼리하고 수 마지막 요청이 시작 된 유지 관리의 hello 결과 확인 합니다.

hello **예약 된 유지 관리 기간** 때 Azure hello 유지 관리를 위해 Vm에 예약 했습니다. 다음에 나오는 선점형 유지 관리 기간을이 기간 동안 hello 유지 관리 기간을 쿼리할 수 있지만 더 이상 수 tooorchestrate hello 유지 관리 될 키를 누릅니다.

## <a name="availability-considerations-during-planned-maintenance"></a>계획된 유지 관리 동안의 가용성 고려 사항 

### <a name="paired-regions"></a>쌍을 이루는 지역

각 Azure 영역의 다른 영역 hello 내와 쌍을 이루는 동일한 지역, 지역 쌍을 함께 수행 합니다. 유지 관리를 실행할 때 Azure는 해당 쌍의 단일 영역에 가상 컴퓨터 인스턴스 hello만 업데이트 됩니다. 예를 들어 hello 북 중미의 가상 컴퓨터를 업데이트할 때 Azure 업데이트 되지 것입니다: 미국 중남부에서 모든 가상 컴퓨터 hello에서 같은 시간입니다. 이는 별도의 다른 시간에 예약하여 지역 간의 장애 조치(failover) 또는 부하 분산을 사용하도록 설정합니다. 그러나 다른 영역에서 유지 관리 유럽 북부 수와 같은 hello 동일 미국 동부로 시간입니다.
[Azure 지역 쌍](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)에 대해 자세히 알아보세요.

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>단일 인스턴스 Vm vs입니다. 가용성 집합 또는 VM 크기 집합

Azure에서 가상 컴퓨터를 사용 하 여 작업을 배포할 때는 Vm hello 가용성 집합 순서 tooprovide 고가용성 tooyour 응용 프로그램 내에서 만들 수 있습니다. 이 구성을 통해 가동 중단 또는 유지 관리 이벤트 중에도 하나 이상의 가상 컴퓨터를 사용할 수 있습니다.

가용성 집합 내에서 개별 Vm too20 업데이트 도메인을 분산 됩니다. 계획된 유지 관리 동안에는 단일 업데이트 도메인만 지정된 시간에 영향을 받습니다. 계획 된 유지 관리 하는 동안 영향 받고 업데이트 도메인의 hello 순서 순차적으로 진행 되지 않을 수 있습니다. 단일 인스턴스 Vm (가용성 집합의 일부가 아님), 즉 다음 없는 방식으로 toopredict 하거나와 함께 Vm 수는 영향을 확인 합니다.

가상 컴퓨터 크기 집합 toodeploy 하는 Azure 계산 리소스를 사용 하면 되 고 단일 리소스로 동일한 Vm 집합이 관리 합니다.
hello 크기 집합 비슷한 보장 tooan 가용성 업데이트 도메인의 형태로 집합을 제공 합니다. 

고가용성을 위해 가상 컴퓨터를 구성 하는 방법에 대 한 자세한 내용은 참조 [ *Windows 가상 컴퓨터의 가용성을 hello 관리*](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

### <a name="scheduled-events"></a>예약된 이벤트

메타 데이터 서비스를 azure 가상 컴퓨터가 Azure에서 호스트에 대 한 정보를 toodiscover 있습니다. 예약 된 이벤트가 예정 된 이벤트에 대 한 화면 정보 노출 hello 범주 중 하나 (예를 들어 다시 부팅) 응용 프로그램을 준비 하 고 제한할 수 있도록 중단 합니다.

예약 된 이벤트에 대 한 자세한 내용은 참조 너무[Azure 메타 데이터 서비스-예약 된 이벤트](../virtual-machines-scheduled-events.md)합니다.

## <a name="maintenance-discovery-and-notifications"></a>유지 관리 검색 및 알림

유지 관리 일정이 표시 toocustomers 개별 Vm의 hello 수준에서 적용 됩니다. Azure를 사용 하면 포털, API, PowerShell 또는 CLI tooquery 선점형 및 예약 된 유지 관리 기간에 대 한 합니다. 또한 hello 경우에서 알림 (전자 메일)을 받을 가능성이 있는 hello 프로세스 중 하나 (이상)의 Vm에는 영향을 합니다.

선점형 유지 관리 및 예약된 유지 관리 단계는 모두 알림으로 시작합니다. Azure 구독 당 단일 알림 tooreceive가 있기만 하면 됩니다. 기본적으로 toohello 구독의 관리자 및 공동 관리자 hello 알림이 보내집니다. 또한 유지 관리 알림을 hello 대상 그룹을 구성할 수 있습니다.

### <a name="view-hello-maintenance-window-in-hello-portal"></a>Hello 포털에서 보기 hello 유지 관리 기간 

Hello Azure 포털을 사용할 수 있으며 유지 관리를 위해 예약 된 Vm을 찾아보십시오.

1.  Azure 포털 toohello에 로그인 합니다.

2.  클릭 하 고 hello 엽니다 **가상 컴퓨터** 블레이드입니다.

3.  Hello 클릭 **열** 에서 사용 가능한 열 toochoose 목록이 tooopen hello 단추

4.  선택 하 고 hello 추가 **유지 관리 기간** 열입니다. 유지 관리에 대 한 예정 된 Vm가 hello 유지 관리 기간을 표시 합니다. a에 대한 유지 관리가 완료되거나 중단되면 유지 관리 기간이 더 이상 표시되지 않습니다.

### <a name="query-maintenance-details-using-hello-azure-api"></a>Hello Azure API를 사용 하 여 유지 관리 정보를 쿼리 합니다.

사용 하 여 hello [VM API 정보를 가져올](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) hello 인스턴스 toodiscover hello 유지 관리 세부 정보 보기에는 개별 VM 찾습니다. hello 응답 hello 요소 다음에 포함 됩니다.

  - isCustomerInitiatedMaintenanceAllowed: 이제 hello VM에서 선점형 재배포를 시작할 수 있는지 여부를 나타냅니다.

  - preMaintenanceWindowStartTime: hello hello 선점형 유지 관리 기간의 시작 시간입니다.

  - preMaintenanceWindowEndTime: hello hello 선점형 유지 관리 기간의 종료 시간입니다. 이 시간 이후이 VM으로 수 tooinitiate 유지 관리할 수 없습니다.
    
  - maintenanceWindowStartTime: hello VM 영향을 받을 때 hello 예약 된 유지 관리 기간의 시간을 시작 합니다.

  - maintenanceWindowEndTime: hello hello 예약 된 유지 관리 기간의 종료 시간입니다.
  
  - lastOperationResultCode: hello 마지막 재배포 유지 관리 작업의 결과입니다.
 
  - lastOperationMessage: 마지막 재배포 유지 관리 작업의 hello 결과 설명 하는 메시지입니다.

## <a name="pre-emptive-redeploy"></a>선점형 다시 배포

선점형 재배포 작업이 Azure에서 적용 된 tooyour Vm을 유지 관리 하는 hello 유연성 toocontrol hello 시간을 제공 합니다. 계획 된 유지 관리를 다시 부팅 하 여 Vm toobe 각각에 대 한 정확한 시간 hello 결정할 수 있습니다 선점형 유지 관리 기간으로 시작 합니다. 이러한 기능이 유용한 사용 사례는 다음과 같습니다.

-   유지 관리 요구 toobe hello 최종 사용자와 조정합니다.

-   Azure에서 제공 하는 hello 예약 된 유지 관리 기간이 충분 하지 않습니다.
    Toobe 요일 hello 가장 바쁜 시간에 발생 하는 hello 창 또는 너무 길어서 수 있습니다.

-   다중 인스턴스 또는 다중 계층 응용 프로그램에 대 한 두 개의 Vm 또는 특정 순서 toofollow 사이의 시간이 충분 해야합니다.

VM에서 선점형 재배포에 대 한 호출 hello VM tooan 이미 노드를 업데이트 하 고 다음 공급 다시에 모든 구성 옵션 및 관련된 리소스 그대로 유지 하 고 이동 합니다. 이렇게 하면 임시 디스크 hello 손실 되며 동적 IP 주소와 연결 된 동안에 가상 네트워크 인터페이스 업데이트 됩니다.

선점형 다시 배포는 VM당 한 번만 활성화됩니다. Hello 프로세스 중 오류가 발생 하는 hello 작업이 중단 되 면 VM은 영향을 받지 hello 이므로 hello 계획 된 유지 관리 반복에서 제외 됩니다. 새 일정에 나중에 접속 선택한 새 기회 tooschedule 및 시퀀스 hello 영향을 Vm에 제공 합니다.