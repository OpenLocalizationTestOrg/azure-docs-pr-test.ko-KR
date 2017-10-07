---
title: "aaaEnable 모니터링 및 Microsoft Azure에서 진단 | Microsoft Docs"
description: "자세한 방법을 tooset Azure에서 리소스에 대 한 진단 구성 합니다."
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 865d010c5846fff6d871e20eca2bc4ac35028354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>모니터링 및 진단 사용
Hello에 [Azure 포털](https://portal.azure.com), 리소스에 대 한 풍부한 자주, 모니터링 및 진단 데이터를 구성할 수 있습니다. Hello를 사용할 수도 있습니다 [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) 또는 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure 진단 프로그래밍 방식으로 합니다.

Azure의 진단, 모니터링 및 메트릭 데이터는 선택한 저장소 계정에 저장됩니다. 이렇게 하면 toouse 있습니다 어떤 tooling tooread hello 데이터 저장소 탐색기에서 원하는 tooPower BI toothird 타사 도구입니다.

## <a name="when-you-create-a-resource"></a>리소스를 만드는 경우
대부분 서비스를 사용 하면 tooenable 진단 hello에 처음 만들 때 [Azure 포털](https://portal.azure.com)합니다.

1. 너무 이동**새로** 에 관심이 있는 hello 리소스를 선택 합니다.
2. **선택적 구성**을 선택합니다.
    ![진단 블레이드](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. **진단**을 선택하고 **On**을 클릭합니다. Toochoose hello 저장소 계정의 진단 toobe에 저장 되도록 해야 합니다. 있습니다 진단 tooa 저장소 계정을 보낼 때 저장소 및 트랜잭션에 대해 일반 데이터 요금이 청구 될 수 있습니다.
4. 클릭 **확인** hello 리소스를 만듭니다.

## <a name="change-settings-for-an-existing-resource"></a>기존 리소스에 대한 설정 변경
리소스를 이미 만든 경우 toochange hello 진단 설정 (예: 데이터 컬렉션의 toochange hello 수준) hello Azure 포털에서에서 해당 바로 수행할 수 있습니다.

1. Toohello 리소스를 이동 하 고 hello 클릭 **설정을** 명령입니다.
2. **진단**을 선택합니다.
3. hello **진단** 블레이드는 모든 hello 가지 진단 및 해당 리소스에 대 한 컬렉션 데이터를 모니터링 합니다. 일부 리소스에 대 한 선택할 수도 있습니다는 **보존** 정책 tooclean hello 데이터용 저장소 계정에서이 작업을 합니다.
    ![저장소 진단](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. 설정을 선택 하면 클릭 hello **저장** 명령입니다. 설정 하는 경우 그 hello에 대 한 처음으로 데이터 tooshow를 모니터링에 대 한 약간 걸릴 수 있습니다.

### <a name="categories-of-data-collection-for-virtual-machines"></a>가상 컴퓨터에 대한 데이터 컬렉션 범주
가상 컴퓨터에 대 한 모든 메트릭 및 로그를 기록할지 1 분 간격으로 수 있도록 항상 hello 최신 정보를 대부분 컴퓨터에 대 한 합니다.

* **기본 메트릭** : 프로세서, 메모리 등 가상 컴퓨터에 대한 상태 메트릭입니다.
* **네트워크 및 웹 메트릭** : 네트워크 연결 및 웹 서비스에 대한 메트릭입니다.
* **.NET 메트릭** : hello.NET 및 ASP.NET 응용 프로그램에 가상 컴퓨터에서 실행 되는 메트릭
* **SQL 메트릭** : Microsoft SQL Service를 실행하는 경우 해당 성능 메트릭입니다.
* **Windows 이벤트 응용 프로그램 로그** : toohello 응용 프로그램 채널 전송 되는 Windows 이벤트
* **Windows 이벤트 시스템 로그** : toohello 시스템 채널 전송 되는 Windows 이벤트입니다. [Microsoft 맬웨어 방지 프로그램](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409)의 모든 이벤트도 포함됩니다.
* **Windows 이벤트 보안 로그** : toohello 보안 채널을 전송 하는 Windows 이벤트
* **진단 인프라 로그** : hello 진단 컬렉션 인프라에 대 한 로깅
* **IIS 로그** : IIS 서버에 대한 로그입니다.

Note이 이번에 특정 배포판의 Linux가 지원 되지 않으며, 하, hello 게스트 에이전트 hello 가상 컴퓨터에 설치 해야 합니다.

## <a name="next-steps"></a>다음 단계
* 작업 이벤트가 발생하거나 메트릭이 임계값을 초과할 때마다 [경고 알림을 수신](insights-receive-alert-notifications.md)합니다.
* [서비스 메트릭스를 모니터링](insights-how-to-customize-monitoring.md) toomake 서비스를 사용 가능 하 고 응답 합니다.
* [인스턴스 수를 자동으로 크기 조정](insights-how-to-scale.md) toomake 있는지 요구에 따라 서비스 확장 합니다.
* [응용 프로그램 성능 모니터링](../application-insights/app-insights-azure-web-apps.md) toounderstand 하려면 정확 하 게 코드 작업 수행 방식을 hello 클라우드에서 합니다.
* [이벤트 및 활동 로그 보기](insights-debugging-with-events.md) toolearn 모든 서비스에 발생 한 것입니다.
* [서비스 상태를 추적할](insights-service-health.md) toofind Azure에 성능 저하 또는 서비스 중단을 발생 하는 경우 아웃 합니다.

