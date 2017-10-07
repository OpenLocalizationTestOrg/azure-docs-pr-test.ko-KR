---
title: "자동차를 움직일 상태 및 구동 BI 대시보드에 aaaPower 습관-Azure | Microsoft Docs"
description: "습관 지원 하 고 차량 상태에 대해 Cortana 인텔리전스 toogain 실시간 및 예측 insights hello 기능을 사용 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a>차량 원격 분석 솔루션 템플릿 Power BI 대시보드 설정 지침
이 **메뉴** toohello 장이 플레이이 북에 연결 합니다. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

hello 차량 원격 분석 분석 솔루션에서는 딜러 car, automobile 제조업체 및 보험 회사 Cortana 인텔리전스 toogain 실시간 및 예측에 대 한 통찰력 차량 상태 및 구동의 hello 기능 활용 방법 R&d 및 마케팅 캠페인 고객의 습관 toodrive 개선 hello 영역에서 발생 합니다. 이 문서는 구성 하는 방법을 hello Power BI 보고서와 대시보드 구독에 hello 솔루션을 배포한 후에 대 한 단계별 지침을 포함 합니다. 

## <a name="prerequisites"></a>필수 조건
1. Hello 배포 [원격 분석 분석](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) 솔루션  
2. [Microsoft Power BI 데스크톱 설치](http://www.microsoft.com/download/details.aspx?id=45331)
3. [Azure 구독](https://azure.microsoft.com/pricing/free-trial/). Azure 구독이 없으면 Azure 무료 구독 시작
4. Microsoft Power BI 계정

## <a name="cortana-intelligence-suite-components"></a>Cortana Intelligence Suite 구성 요소
Hello 차량 원격 분석 분석 솔루션 서식 파일의 일부로 hello 다음 Cortana Intelligence 서비스 구독에 배포 됩니다.

* **이벤트 허브** - 수백만 개의 차량 원격 분석 이벤트를 Azure에 수집합니다.
* **스트림 분석** - 차량 상태에 대한 실시간 통찰력을 얻고 다양한 일괄 처리 분석을 위해 해당 데이터를 장기간용 저장소에 보관합니다.
* **기계 학습** 실시간 이상 탐지에 대 한 및 일괄 처리 예측 insights toogain 합니다.
* **HDInsight** 규모로 tootransform 사용된 데이터는
* **Data Factory** 오케스트레이션, 예약, 리소스 관리 및 모니터링 hello 일괄 처리 파이프라인을 처리 합니다.

**Power BI** - 실시간 데이터 및 예측 분석 시각화를 위해 이 솔루션을 다양한 대시보드에 제공합니다. 

hello 솔루션에서는 두 개의 서로 다른 데이터 소스: **차량 신호 및 진단 데이터 집합 시뮬레이션** 및 **차량 카탈로그**합니다.

차량 텔레매틱스 시뮬레이터가 이 솔루션의 일부로 포함되어 있습니다. 진단 정보를 내보냅니다 고, 시간에서 hello 차량 및 구동 패턴 지정된 된 지점에서의 해당 toohello 상태를 알립니다. 

hello 차량 카탈로그는 참조 데이터 집합 포함 VIN toomodel 매핑을

## <a name="power-bi-dashboard-preparation"></a>Power BI 대시보드 준비
### <a name="setup-power-bi-real-time-dashboard"></a>Power BI에 대한 실시간 대시보드 설정

**Hello 실시간 대시보드 응용 프로그램을 시작** hello 수동 작업 지침에 따라 해야 hello 배포가 완료 되 면

* 실시간 대시보드 응용 프로그램 RealtimeDashboardApp.zip을 다운로드한 다음 압축을 풉니다.
*  Hello 압축 푼된 폴더에서 응용 프로그램 구성 파일 'RealtimeDashboardApp.exe.config' hello 값이 변경 내용을 저장 하 고 수동 작업 지침은 hello에 Eventhub, Blob 저장소 및 ML 서비스 연결에 대 한 대체 appSettings를 엽니다.
* RealtimeDashboardApp.exe 응용 프로그램을 실행합니다. 로그인 창 팝업, 유효한 PowerBI 자격 증명을 제공 되며 hello 클릭 **Accept** 단추입니다. 그런 다음 hello 앱 toorun을 시작 됩니다.

   ![로그인 tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Power BI 대시보드 권한](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* 로그인 tooPowerBI 웹 사이트 및 실시간 대시보드를 만듭니다.

이제, 사용 중인 다양 한 시각화 기능 toogain 실시간 함께 준비 tooconfigure hello Power BI 대시보드 및 차량 상태 및 구동에서 예측 insights 습관입니다. 보고 하 고 hello 대시보드를 구성 하는 모든 hello tooan 시간 toocreate 약 45 분이 필요 합니다. 

### <a name="configure-power-bi-reports"></a>Power BI 보고서 구성
hello 실시간 보고서와 hello 대시보드 30 ~ 45 분 toocomplete 약 걸립니다. 너무 찾아보기[http://powerbi.com](http://powerbi.com) 및 로그인 합니다.

![로그인 tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

새 데이터 집합이 Power BI에 생성됩니다. Hello 클릭 **ConnectedCarsRealtime** 데이터 집합입니다.

![연결된 자동차 실시간 데이터 집합 선택](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

Hello 빈 보고서를 사용 하 여 저장 **Ctrl + s**합니다.

![빈 보고서 저장](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

보고서 이름 *차량 원격 분석 실시간 보고서*를 제공합니다.

![보고서 이름 제공](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a>실시간 보고서
이 솔루션에는 다음과 같은 세 가지 실시간 보고서가 있습니다.

1. 운행 중인 차량
2. 유지보수가 필요한 차량
3. 차량 상태 통계

선택할 수 tooconfigure 모든 hello 세 개의 실시간 보고서 또는 모든 단계 후에 중지 있으며 toohello hello 일괄 처리 보고서 구성의 다음 섹션을 계속 진행 합니다. 모든 toocreate 권장 hello 3 hello 솔루션의 hello 실시간 경로의 toovisualize hello 전체 정보를 보고 합니다.  

### <a name="1-vehicles-in-operation"></a>1. 운행 중인 차량
두 번 클릭 **1 페이지** 너무 이름을 "차량 작업에서"  
    ![연결된 자동차 - 운행 중인 차량](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)  

**필드**에서 **vin**을 선택하고 시각화 형식을 **“카드”**로 선택합니다.  

카드 시각화는 그림에 나와 있는 것처럼 생성됩니다.  
    ![연결된 자동차 - vin 선택](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

새 시각화를 tooadd hello 빈 영역을 클릭 합니다.  

필드에서 **시/군/구** 및 **vin**을 선택합니다. 시각화에도 변경**"맵"**합니다. **vin** 을 값 영역으로 끕니다. 끌기 **도시** 필드에서 너무**범례** 영역입니다.   
    ![연결된 자동차 - 카드 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)

선택 **형식** 섹션에서 **시각화**, 클릭 **제목** hello 변경 **텍스트** 너무**"차량에서 도시별 작업이"**합니다.  
    ![연결된 자동차 - 도시별 운행 중인 차량](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)   

최종 시각화는 그림과 같이 표시됩니다.    
    ![연결된 자동차 - 최종 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

새 시각화를 tooadd hello 빈 영역을 클릭 합니다.  

선택 **도시** 및 **vin**, 너무 시각화 형식 변경**묶은 세로 막대형 차트**합니다. **축 영역**의 **시/군/구** 필드 및 **값 영역**의 **vin** 필드를 확인합니다.  

**“vin 개수”**별로 차트를 정렬합니다.  
    ![연결된 자동차 - vin 개수](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)  

변경 차트 **제목** 너무**"차량 도시별 작업에서"**  

Hello 클릭 **형식** 섹션을 다음 선택 **데이터 색**, hello 클릭 **"On"** 너무**모두 표시**  
    ![연결된 자동차 - 모든 데이터 색 표시](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)  

색 아이콘을 클릭 하 여 개별 도시 hello 색을 변경 합니다.  
    ![연결된 자동차 - 색 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

새 시각화를 tooadd hello 빈 영역을 클릭 합니다.  

시각화에서 **묶은 세로 막대형 차트** 시각화를 선택하고 **시/군/구** 필드를 **축** 영역에, **모델**을 **범례** 영역에, **vin**을 **값** 영역으로 끕니다.  
    ![연결된 자동차 - 묶은 세로 막대형 차트](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)  
    ![연결된 자동차 - 렌더링](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)

이 페이지의 모든 시각화를 페이지에 나와 있는 것처럼 다시 배열합니다.  
    ![연결된 자동차 - 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

Hello "차량 작업에서" 실시간 보고서를 구성 했습니다. Toocreate hello 다음 실시간 보고서를 계속 또는 중지 구성 하는 hello 대시보드 합니다. 

### <a name="2-vehicles-requiring-maintenance"></a>2. 유지보수가 필요한 차량
클릭 ![추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd 새 보고서를 이름을 바꾸거나 너무**"유지 관리를 요구 하는 차량"**

![연결된 자동차 - 유지보수가 필요한 차량](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

선택 **vin** 필드와 시각화 유형 변경**카드**합니다.  
    ![연결된 자동차 - Vin 카드 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)  

Hello 데이터 집합의 "MaintenanceLabel" 이라는 필드를 만들려고 했습니다. 이 할당량 값은 “0” 또는 “1”일 수 있습니다. 솔루션의 일부로 프로 비전 하 고 실시간 경로 hello와 통합 hello Azure 기계 학습 모델에 의해 설정 됩니다. hello 값 "1"는 차량 유지 관리가 필요한 것을 나타냅니다. 

tooadd는 **페이지 수준** 유지 관리를 요구 하는 차량 데이터를 표시 하는 것에 대 한 필터: 

1. 끌어서 hello **"MaintenanceLabel"** 필드 **페이지 수준 필터**합니다.  
   ![연결된 자동차 - 페이지 수준 필터](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)  
2. MaintenanceLabel 페이지 수준 필터 아래쪽에 있는 **기본 필터링** 을 클릭합니다.  
   ![연결된 자동차 - 기본 필터링](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)  
3. 필터 값을 너무 설정**"1"**    
   ![연결된 자동차 - 필터 값](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)  

새 시각화를 tooadd hello 빈 영역을 클릭 합니다.  

시각화에서 **묶은 세로 막대형 차트**를 선택합니다.  
![연결된 자동차 - Vind 카드 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)  
![연결된 자동차 - 묶은 세로 막대형 차트](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)

끌어서 필드 **모델** 에 **축** 영역 **Vin** 너무**값** 영역입니다. 그런 다음 시각화를 **vin 개수**별로 정렬합니다.  변경 차트 **제목** 너무**"모델에 의해 유지 관리를 요구 하는 차량"**  

**vin** 필드를 **시각화** 탭의 **필드** ![필드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) 섹션에 있는 **색 채도**로 끕니다.  
![연결된 자동차 - 색 채도](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)  

**형식** 섹션의 시각화에서 **데이터 색**을 변경합니다.  
최소 색을 **F2C812**로 변경하고,  
최대 색을 **FF6300**으로 변경합니다.  
![연결된 자동차 - 색 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)  
![연결된 자동차 - 새 시각화 색](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)  

새 시각화를 tooadd hello 빈 영역을 클릭 합니다.  

시각화에서 **묶은 세로 막대형 차트**를 선택하고 **vin** 필드를 **값** 영역으로, **시/군/구** 필드를 **축** 영역으로 끕니다. **“vin 개수”**별로 차트를 정렬합니다. 변경 차트 **제목** 너무**"도시별 유지 관리를 요구 하는 차량"**   
![연결된 자동차 - 도시별 유지보수가 필요한 차량](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)  

새 시각화를 tooadd hello 빈 영역을 클릭 합니다.  

선택 **다중 행 카드** 시각화에서 시각화를 끌어 **모델** 및 **vin** hello에 **필드** 영역입니다.  
![연결된 자동차 - 여러 행 카드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)    

Hello 시각화의 모든 재배열 hello 최종 보고서 모양은 다음과 같습니다.  
![연결된 자동차 - 여러 행 카드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

Hello "유지 관리를 요구 하는 차량" 실시간 보고서를 구성 했습니다. Toocreate hello 다음 실시간 보고서를 계속 또는 중지 구성 하는 hello 대시보드 합니다. 

### <a name="3-vehicles-health-statistics"></a>3. 차량 상태 통계
클릭 ![추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd 새 보고서, 너무 이름 바꾸기**"차량 상태 통계"**  

선택 **계기** 시각화에서 시각화를 끌어와서 hello **속도** 필드 **값, 최소값, 최대값** 영역입니다.  
![연결된 자동차 - 여러 행 카드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)  

기본 집계 hello 변경 **속도** 에 **영역 값** 너무**평균** 

기본 집계 hello 변경 **속도** 에 **최소 영역** 너무**최소**

기본 집계 hello 변경 **속도** 에 **최대 영역** 너무**최대**

![연결된 자동차 - 여러 행 카드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

Hello 이름 바꾸기 **계기 제목** 너무**"속도 평균"** 

![연결된 자동차 - 계기](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

새 시각화를 tooadd hello 빈 영역을 클릭 합니다.  

마찬가지로 **평균 엔진 오일**, **평균 연료** 및 **평균 엔진 온도**에 대한 **계기**를 추가합니다.  

단계 위에 기준으로 각 계기에 필드의 기본 집계 hello 변경 **"속도 평균"** 계기입니다.

![연결된 자동차 - 계기](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

새 시각화를 tooadd hello 빈 영역을 클릭 합니다.

선택 **꺾은선형 및 묶은 세로 막대형 차트** 시각화에서 끌어 **도시** 필드 **Shared Axis**를 끌어 **속도**, **tirepressure 및 engineoil 필드** 에 **열 값** 영역도 해당 집계 유형을 변경**평균**합니다. 

끌어서 hello **engineTemperature** 필드를 **Line Values** 영역도 hello 집계 형식을 변경**평균**합니다. 

![연결된 자동차 - 시각화 필드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

변경 hello 차트 **제목** 너무**"평균 속도, 타이어 압력, 석유 엔진 및 엔진 온도"**합니다.  

![연결된 자동차 - 시각화 필드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

새 시각화를 tooadd hello 빈 영역을 클릭 합니다.

선택 **Treemap** 시각화에서 시각화를 끌어 hello **모델** hello 필드 **그룹** 영역과 끌어서 hello 필드  **MaintenanceProbability** hello에 **값** 영역입니다.

변경 hello 차트 **제목** 너무**"Vehicle 모델 유지 관리 요구"**합니다.

![연결된 자동차 - 차트 제목 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

새 시각화를 tooadd hello 빈 영역을 클릭 합니다.

선택 **100% 기준 누적 가로 막대형 차트** 시각화를 끌어 hello **도시** hello 필드 **축** 영역과 끌어서 hello **MaintenanceProbability**, **RecallProbability** hello에 대 한 필드 **값** 영역입니다.

![연결된 자동차 - 새 시각화 추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

클릭 **형식**선택, **데이터 색**, 및 집합 hello **MaintenanceProbability** 색 toohello 값 **"F2C80F"**합니다.

변경 hello **제목** hello의 차트 너무**"확률의 자동차를 움직일 유지 관리 및 다시 호출 하 여 도시"**합니다.

![연결된 자동차 - 새 시각화 추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

새 시각화를 tooadd hello 빈 영역을 클릭 합니다.

선택 **영역형 차트** 시각화에서 시각화를 끌어 hello **모델** hello 필드 **축** 영역과 끌어서 hello **engineOil, tirepressure, 속도 MaintenanceProbability** hello에 대 한 필드 **값** 영역입니다. 해당 집계 유형을 변경**"평균"**합니다. 

![연결된 자동차 - 집계 유형 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

Hello 차트의 제목을 hello도 변경**"엔진 석유 평균, 모델에 의해 압력, 속도 및 유지 관리 확률 타이어"**합니다.

![연결된 자동차 - 차트 제목 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

Hello 빈 영역 tooadd 새 시각화를 클릭 합니다.

1. 시각화에서 **분산형 차트** 시각화를 선택합니다.
2. 끌어서 hello **모델** hello 필드 **세부 정보** 및 **범례** 영역입니다.
3. 끌어서 hello **연료** hello 필드 **x 축** 영역 hello 집계도 변경**평균**합니다.
4. 끌기 **engineTemparature** 에 **y 축 영역**, hello 집계도 변경**평균**
5. 끌어서 hello **vin** hello 필드 **크기** 영역입니다.

![연결된 자동차 - 새 시각화 추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

변경 hello 차트 **제목** 너무**"연료의 평균, 모델에 의해 엔진 온도"**합니다.

![연결된 자동차 - 차트 제목 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

아래와 같이 hello 최종 보고서는 같습니다.

![연결된 자동차 - 최종 보고서](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a>실시간 대시보드를 toohello hello 보고서의 시각화를 고정
다음 tooDashboards hello 더하기 아이콘을 클릭 하 여 빈 대시보드를 만듭니다. "차량 원격 분석 대시보드"로 이름을 지정할 수 있습니다.

![연결된 자동차 - 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

보고서 toohello 대시보드 위에 hello의 시각화를 고정 hello 합니다. 

![연결된 자동차 - 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

모든 세 개의 보고서 만들어집니다 hello 및 시각화에 해당 하는 hello가 고정 된 toohello 대시보드 hello 대시보드 다음과 같이 표시 됩니다. 모든 hello 보고서를 만들지 않은 경우 대시보드를 다른 보일 수 있습니다. 

![연결된 자동차 - 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

축하합니다. Hello 실시간 대시보드를 성공적으로 만들었습니다. Tooexecute CarEventGenerator.exe 및 RealtimeDashboardApp.exe을 계속 하면서 실시간 업데이트 hello 대시보드에 표시 됩니다. 다음 단계는 약 10 개 too15 분 toocomplete hello를 취해야 합니다.

## <a name="setup-power-bi-batch-processing-dashboard"></a>Power BI 일괄 처리 대시보드 설정
> [!NOTE]
> 2 시간 (에서 성공적으로 완료 hello 배포의 hello) hello 끝 tooend 일괄 처리를 처리 파이프라인 toofinish 실행에 대 한 걸리고 년 분량의 생성 된 데이터를 처리 합니다. 따라서 toofinish hello 다음 단계를 진행 하기 전에 처리 하는 hello를 기다립니다. 
> 
> 

**Hello Power BI designer 파일을 다운로드**

* 미리 구성 된 Power BI designer 파일 수동 작업 지침은 hello 배포의 일부로 포함 됩니다.
* 2를 찾습니다. 설치 프로그램 PowerBI 일괄 처리 대시보드 라는 일괄 처리 대시보드에 대 한 hello PowerBI 템플릿을 다운로드할 수 있습니다 **ConnectedCarsPbiReport.pbix**합니다.
* • 로컬로 저장

**Power BI 보고서 구성**

* 디자이너 파일 열기 hello '**ConnectedCarsPbiReport.pbix**' Power BI Desktop을 사용 하 여 합니다. 설치 하지 않으면 이미 있으면 경우 Power BI Desktop에서 hello [Power BI Desktop 설치](http://www.microsoft.com/download/details.aspx?id=45331)합니다. 
* Hello 클릭 **쿼리 편집**합니다.

![Power BI 쿼리 편집](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* Hello를 두 번 클릭 **소스**합니다.

![Power BI 원본 설정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* Hello 배포의 일환으로 사용자를 프로 비전 가져왔습니다 hello Azure SQL server와 함께 서버 연결 문자열을 업데이트 합니다.  Hello 수동 작업 지침은 아래에서 찾는 위치 

    4. Azure SQL Database
    
    * 서버: somethingsrv.database.windows.net
    * 데이터베이스: connectedcar
    * 사용자 이름: username
    * 암호: Azure Portal에서 SQL Server 암호를 관리할 수 있습니다

* **데이터베이스** 를 *connectedcar*로 둡니다.

![Power BI 데이터베이스 설정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* **확인**을 클릭합니다.
* 나타납니다 **Windows 자격 증명** 도 변경, 탭은 기본적으로 선택**자격 증명을 데이터베이스** 를 클릭 하 여 **데이터베이스** 오른쪽에 탭 합니다.
* Hello 제공 **Username** 및 **암호** 배포 설치 중 지정 된 Azure SQL 데이터베이스의 합니다.

![데이터베이스 자격 증명 제공](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* **연결**
* 세 가지 나머지 쿼리 hello 오른쪽 창에는 각각에 대 한 hello 단계를 반복한 다음 hello 데이터 원본 연결 정보를 업데이트 합니다.
* **닫기 및 로드**를 클릭합니다. Power BI Desktop 파일 데이터 집합은 연결 된 tooSQL Azure 데이터베이스 테이블입니다.
* **닫습니다** .

![Power BI 데스크톱 닫기](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* 클릭 **저장** toosave hello 변경 단추입니다. 

이제 hello 솔루션에서 toohello 일괄 처리 경로 해당 하는 모든 hello 보고서를 구성 했습니다. 

## <a name="upload-toopowerbicom"></a>너무 업로드*powerbi.com*
1. Http://powerbi.com 및 로그인에 toohello Power BI 웹 포털을 탐색 합니다.
2. **데이터 가져오기**  
3. Hello Power BI 데스크톱 파일을 업로드 합니다.  
4. tooupload, 클릭 **데이터 가져오기 파일이->-> 로컬 파일**  
5. Toohello 이동 **"**ConnectedCarsPbiReport.pbix**"**  
6. Hello 파일이 업로드 되 면 백 tooyour를 탐색된 하 고 있습니다. Power BI 작업 공간 됩니다.  

데이터 집합, 보고서 및 빈 대시보드가 생성됩니다.  

Pin 호출 tooa 새 대시보드 차트 **차량 원격 분석 분석 대시보드** 에 **Power BI**합니다. 위에서 만든 hello 빈 대시보드를 클릭 한 다음 toohello를 탐색 **보고서** 섹션 클릭 hello 새로 보고서를 업로드 합니다.  

![차량 원격 분석 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

**참고 hello 보고서에 6 개 페이지가 있습니다.**  
1페이지: 차량 밀도  
2페이지: 실시간 차량 상태  
3페이지: 적극적으로 운전한 차량   
4페이지: 리콜된 차량  
5페이지: 연료 효율이 높게 운전한 차량  
6페이지: Contoso 로고  

![연결된 자동차 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

**페이지 3 자에서**, hello 다음 고정 합니다.  

1. vin 개수  
   ![연결된 자동차 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. 모델별 적극적으로 운전한 차량 - 폭포 차트   
   ![차량 원격 분석 - 차트 4 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

**5 페이지에서에서**, hello 다음 고정 합니다. 

1. vin 개수    
   ![차량 원격 분석 - 차트 5 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. 모델별 연료 효율이 좋은 차량: 묶은 세로 막대형 차트   
   ![차량 원격 분석 - 차트 6 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

**4 페이지에서에서**, hello 다음 고정 합니다.  

1. vin 개수  
   ![차량 원격 분석 - 차트 7 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. 시/군/구, 모델별 리콜된 차량: 트리맵   
   ![차량 원격 분석 - 차트 8 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

**6 페이지에서에서**, hello 다음 고정 합니다.  

1. Contoso 모터 로고   
   ![차량 원격 분석 - 차트 9 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

**Hello 대시보드 구성**  

1. Toohello 대시보드를 탐색 합니다.
2. 각 차트 위에 놓고 hello 전체 대시보드 이미지 아래에 제공 된 hello 이름 지정에 따라 이름을 바꿉니다. 또한 hello 대시보드 아래와 같은 toolook 주위 hello 차트를 이동 합니다.  
   ![차량 원격 분석 - 대시보드 2 구성](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![차량 원격 분석 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. 이 문서에서 설명한 것 처럼 모든 hello 보고서를 만든 경우 hello 최종 완료 된 대시보드 찾아야 hello 다음 그림 처럼 합니다. 

![차량 원격 분석 - 대시보드 2 구성](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

축하합니다. 성공적으로 만들었음을 hello 보고서 및 대시보드 toogain 실시간으로 예측 hello 및 차량 상태 및 구동에서 일괄 처리 insights 습관입니다.  
