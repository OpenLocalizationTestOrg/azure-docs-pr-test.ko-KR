---
title: "솔루션을 미리 구성 된 유지 관리 aaaPredictive | Microsoft Docs"
description: "Hello Azure IoT Suite 예측 유지 관리에 대 한 설명을 미리 솔루션을 구성 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a>예측 정비 사전 구성 솔루션 개요

hello *예측 유지 관리* [솔루션 미리 구성 된] [ lnk_preconfigured_solutions] hello 중 하나인 [Microsoft Azure IoT Suite] [ lnk_iot_suite] 솔루션 미리 구성 합니다. 이 솔루션은 실시간 장치 원격 분석 컬렉션과 [Azure Machine Learning][lnk-machine-learning]을 사용하여 생성되는 예측 모델을 통합합니다.

Azure IoT Suite 신속 하 게 하 고 쉽게 tooand 모니터 자산 연결 하 고 사용할 수 실시간 대시보드 및 시각화에 대 한 원격 분석 분석 합니다. Hello 예측 유지 관리 솔루션에 hello 대시보드 및 시각화를 알려 효율성 드라이브 하 고 스트림을 수익을 향상 시킬 수 있는 새 인텔리전스 합니다.

## <a name="hello-scenario"></a>hello 시나리오

Fabrikam은 경쟁력 있는 가격으로 우수한 고객 경험을 제공하는 데 중점을 두고 있는 지역 항공사입니다. 항공기 지연의 이유 중 하나는 정비 문제이며 항공 엔진 정비는 특히 어려운 부분입니다. Fabrikam 안 엔진 실패 비행 중 해서든, 하므로 해당 엔진을 정기적으로 검사 하 고 tooa 계획에 따라 유지 관리 예약 됩니다. 그러나 엔진 착용 항상 하지 비행기 hello 동일 합니다. 엔진에 대해 필요 이상의 정비를 수행하는 경우도 있습니다. 무엇보다, 정비가 수행될 때까지 항공기를 이륙할 수 없는 문제가 발생합니다. 비행기 위치에 있는 오른쪽 기술자를 hello 또는 예비 부품을 사용할 수 없는 면 이러한 문제는 특히 비용이 증가할 수 있습니다.

Fabrikam의 비행기의 hello 엔진 비행 중 엔진을 모니터링 하는 센서와 계측 됩니다. Fabrikam은 hello 비행 중 수집 된 hello 예측 유지 관리 솔루션 toocollect hello 센서 데이터를 사용 합니다. 엔진 작업의 누적 년 후 오류 데이터, Fabrikam의 데이터 과학자는 방식으로 toopredict hello 남은 연수 (RUL) 비행기 엔진의 모델링 됩니다. hello 모델 데이터 hello 엔진 센서 중 4 개에서 및 tooeventual 실패 하는 엔진 마모 간의 상관 관계를 사용 합니다. Fabrikam tooperform 정기적 검사 tooensure 안전성을 계속 하는 동안 모든 비행 후 각 엔진에 대 한 hello 모델 toocompute hello RUL를 지금 사용할 수 있는 것입니다. hello 모델 hello 비행 중 hello 엔진에서 수집 하는 hello 원격 분석을 사용 합니다. Fabrikam은 이제 향후 고장 시점을 예측하고 정비 및 수리를 사전에 계획할 수 있습니다.

> [!NOTE]
> hello 솔루션 모델 실제 엔진 마모 데이터를 사용합니다.

Hello 지점 유지 관리에 필요한 경우를 예측 하 여 Fabrikam 작업 tooreduce 비용을 최적화할 수 있습니다.

유지 관리 코디네이터는 다음 작업을 수행하도록 스케줄러와 함께 작동합니다.

- 특정 위치에서 중지 비행기와 toocoincide 유지 관리를 계획 합니다.
- 충분 한 시간 ´ ü ± 서비스 hello 비행기 toobe 일정 중단이 발생 하지 않고 확인 합니다.
- tooschedule 기술자 tooensure 비행기 대기 시간 없이 효율적으로 처리 합니다.

재고 관리자는 정비 계획을 수신하기 때문에 주문 공정 및 예비 부품 재고를 최적화할 수 있습니다.

이러한 작업 Fabrikam toominimize 비행기 명확 하 게 시간을 설정 하 고 승객 및 직원 일 동 hello 안전성을 보장 하면서 운영 비용을 절감 합니다.

toounderstand 어떻게 [Azure IoT Suite] [ lnk_iot_suite] hello 기능 고객 필요한 toorealize hello 가능성을 제공 하는지 검토이 예측 유지 관리의 [인포 그래픽] [lnk_infographic].

## <a name="how-hello-predictive-maintenance-solution-is-built"></a>Hello 예측 유지 관리 솔루션 빌드 방법

hello 솔루션은 사용할 수 있는 기존 Azure 기계 학습 모델 템플릿 tooshow IoT Suite 서비스를 통해 수집 된 장치 원격 분석에서 작업 하는 이러한 기능 합니다. Microsoft 만들었습니다는 [회귀 모델] [ lnk_regression_model] 공개적으로 사용할 수 있는 데이터를 기반으로 하는 비행기 엔진<sup>\[1\]</sup>, 단계별 및 toouse 모델 hello 하는 방법에 대 한 지침입니다.

이 템플릿에서 만든 hello 회귀 모델을 사용 하는 hello Azure IoT 예측 유지 관리 솔루션입니다. hello 모델을 Azure 구독에 배포 하 고 자동으로 생성 된 API를 통해 노출 합니다. hello 테스트 (총 100)의 4를 나타내는 데이터의 하위 집합을 포함 하는 hello 솔루션 엔진 및 총 21) (의 4 hello 센서 데이터 스트림을 합니다. 이 데이터는 충분히 tooprovide hello 학습 된 모델에서 올바른 결과입니다.

*\[1\] A. Saxena and K. Goebel(2008). "Turbofan 엔진 성능 저하 시뮬레이션 데이터 집합", NASA Ames Prognostics Data Repository(http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*

## <a name="get-started-with-predictive-maintenance"></a>예측 유지 관리 시작

이 자습서 tooprovision 예측 유지 관리 솔루션을 hello 하는 방법을 보여 줍니다. 또한 안내 합니다 hello hello 예측 유지 관리 솔루션의 기본 기능입니다. 이러한 기능 중 대부분 hello 미리 구성 된 솔루션과 함께 배포 하는 hello 솔루션 대시보드를 통해 액세스할 수 있습니다.

toocomplete이이 자습서에서는 활성 Azure 구독이 필요 합니다.

> [!NOTE]
> 계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 평가판][lnk_free_trial]을 참조하세요.

1. 너무 로그온[azureiotsuite.com] [ lnk-azureiotsuite] Azure를 사용 하 여 계정 자격 증명을 누르고  **+**  toocreate 솔루션입니다.
1. 클릭 **선택** hello **예측 유지 관리** 바둑판식으로 배열입니다.
1. 예측 정비 사전 구성 솔루션에 **솔루션 이름**을 입력합니다.
1. 선택 hello **지역** 및 **구독** toouse tooprovision hello 솔루션을 원할 수 있습니다.
1. 클릭 **솔루션 만들기** toobegin hello를 프로 비전 프로세스입니다. 이 프로세스는 일반적으로 몇 분 toorun을 걸립니다.

### <a name="wait-for-hello-provisioning-process-toocomplete"></a>프로비저닝 프로세스 toocomplete hello에 대 한 대기

1. 솔루션에 hello 타일을 클릭 **프로 비전** 상태입니다.
1. 공지 hello **상태를 프로 비전** Azure 구독에서 Azure 서비스 배포 됩니다.
1. 프로 비전이 완료 되 면 hello 상태가 변경 될 너무**준비**합니다.
1. Hello 오른쪽 창에 솔루션의 hello 타일 toosee hello 자세히를 클릭 합니다. 이 창의 hello 솔루션 대시보드 및 액세스 hello 기계 학습 작업 영역을 시작할 수 있습니다.

> [!NOTE]
> Hello 미리 구성 된 솔루션을 배포 하는 문제가 발생 하는 경우 검토 [hello azureiotsuite.com 사이트에 대 한 권한을] [ lnk-permissions] 및 hello [FAQ] [ lnk-faq]. Hello 문제가 지속 되 면 hello에 서비스 티켓을 만들 [포털][lnk-portal]합니다.

솔루션에 대 한 목록에 없는 세부 정보 toosee 예상할 수 있습니까? [사용자 의견](https://feedback.azure.com/forums/321918-azure-iot)에 기능 제안을 보내주세요.

## <a name="view-hello-solution"></a>보기 hello 솔루션

이 섹션에서는 UI hello 솔루션을 안내합니다.

### <a name="predictive-maintenance-dashboard"></a>대시보드에서 예측 유지 관리

PowerBI JavaScript 컨트롤을 사용 하는 hello 웹 응용 프로그램에서이 페이지 (hello 참조 [powerbi-visuals 리포지토리][lnk-powerbi]) toovisualize:

* hello blob 저장소에 hello 스트림 분석 작업의 데이터를 출력 합니다.
* 비행기 엔진 당 hello RUL 및 주기 수입니다.

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a>Hello 클라우드 솔루션의 hello 동작을 관찰합니다.

Hello Azure 포털에서 toohello 리소스 그룹 이동 hello 솔루션 이름이 선택한 tooview 프로 비전 된 리소스입니다.

![][img-resource-group]

Hello 미리 구성 된 솔루션의 프로 비전 할 때 전자 메일 링크 toohello 기계 학습 작업 영역에 나타납니다. Hello에서 toohello 기계 학습 작업 영역을 탐색할 수 있습니다 [azureiotsuite.com] [ lnk-azureiotsuite] 프로 비전 된 솔루션에 대 한 페이지입니다. 타일은 hello 솔루션은 hello 하는 경우이 페이지에서 사용할 수 **준비** 상태입니다.

![][img-machine-learning]

Hello 솔루션 포털에서 해당 hello 샘플이 프로 비전 되어 4 개의 시뮬레이션 된 장치 toorepresent 두 비행기 각각 4 개의 센서 비행기 당 두 개의 엔진으로 볼 수 있습니다. Toohello 솔루션 포털을 처음 표시할 때 hello 시뮬레이션 중지 됩니다.

![][img-simulation-stopped]

클릭 **시뮬레이션 시작** toobegin hello 시뮬레이션 합니다. 센서 기록, RUL, 주기 및 RUL hello 기록 hello 대시보드를 채웁니다.

![][img-simulation-running]

RUL 160 (예시 목적을 위해 선택 대 한 임의의 임계값) 보다 작은 경우 RUL 표시할 경고 기호 다음 toohello를 hello 솔루션 포털에 표시 됩니다. hello 솔루션 포털에는 hello 비행기 엔진 노란색으로 강조 표시합니다. Hello RUL 값 전반적으로 일반 하향 추세를 포함 하는 방법 사항을 참고 하십시오. 하지만 다음과 같은 toobounce 및 축소 합니다. 이 동작은 hello 다양 한 주기 길이 및 hello 모델 정확도에서 발생합니다.

![][img-simulation-warning]

hello 전체 시뮬레이션 약 35 분 toocomplete 148 주기를 사용합니다. 약 5 분에서 처음으로 hello에 대 한 hello 160 RUL 임계값을 충족 하 고 두 엔진에서 약 8 분 hello 임계값에 도달 합니다.

hello 시뮬레이션 148 사이클 hello 전체 데이터 집합을 실행 하 고 최종 RUL 및 주기 값에 settles.

언제 든 hello 시뮬레이션을 중지할 수 있습니다 지점 하지만 클릭 하면 **시작 시뮬레이션** 재생 hello hello 데이터 집합의 hello 시작에서 시뮬레이션 합니다.

## <a name="next-steps"></a>다음 단계

Azure IoT 예측 유지 관리 시나리오, 읽기를 사용 하는 방법에 대 한 자세한 toolearn [hello 사물 인터넷에서에서 값을 캡처할][lnk_capture_value]합니다.

수행 된 [연습] [ lnk-predictive-walkthrough] hello 예측 유지 관리 솔루션의 합니다.

탐색할 수도 있습니다 hello 중 일부 다른 기능 및 hello IoT Suite 미리 구성 된 솔루션의 기능:

* [IoT Suite에 대한 질문과 대답][lnk-faq]
* [Hello 접지에서 IoT 보안][lnk-security-groundup]

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/