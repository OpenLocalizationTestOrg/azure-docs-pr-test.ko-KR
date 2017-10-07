---
title: "Application Insights에서 원격 분석의 aaaContinuous 내보내기 | Microsoft Docs"
description: "Microsoft Azure에서 진단 및 사용 현황 데이터 toostorage 내보내고 여기에서 다운로드 합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a>Application Insights에서 원격 분석 내보내기
Hello 표준 보존 기간 보다 오랫동안 tookeep 원격 분석을 선택 하십시오. 또는 일부 특수한 방식으로 처리하시겠습니까? 그렇다면 연속 내보내기가 적합합니다. JSON 형식으로 Microsoft Azure에서 내보낸된 toostorage hello 이벤트 hello Application Insights 포털에서 볼 수 있습니다. 여기에서 데이터를 다운로드 및 무엇이 든 코드를 작성할 수 있습니다 tooprocess 할 것입니다.  

연속 내보내기를 사용할 경우 추가 요금이 발생할 수 있습니다. [가격 책정 모델](http://azure.microsoft.com/pricing/details/application-insights/)을 확인하세요.

연속 내보내기의를 설정 하기 전에 몇 가지 대안 tooconsider 할 수 있습니다.

* 메트릭 또는 검색 블레이드의 hello 위쪽 hello 내보내기 단추를 사용 하면 테이블 및 차트 tooan Excel 스프레드시트를 전송할 수 있습니다.

* [분석](app-insights-analytics.md)은 원격 분석을 위한 강력한 쿼리 언어를 제공합니다. 결과를 내보낼 수도 있습니다.
* 너무에 찾고 있는 경우[Power BI에서 데이터를 탐색](app-insights-export-power-bi.md), 연속 내보내기가 사용 하지 않고 할 수 있습니다.
* hello [데이터 REST API 액세스](https://dev.applicationinsights.io/) 원격 분석을 프로그래밍 방식으로 액세스할 수 있습니다.

연속 내보내기 (여기서 것 유지 될 수 있는 대해 원하는 만큼) 하 여 데이터 toostorage을 복사한 후은 일반적인 hello에 대 한 Application Insights에서 계속 제공 [보존 기간](app-insights-data-retention-privacy.md)합니다.

## <a name="setup"></a> 연속 내보내기 만들기
1. 앱에 대 한 Application Insights 리소스 hello에 연속 내보내기가 열고 선택 **추가**:

    ![아래로 스크롤하여 연속 내보내기 클릭](./media/app-insights-export-telemetry/01-export.png)

2. Hello 원격 분석 데이터 형식을 선택 tooexport 원하는 합니다.

3. 생성 또는 선택할는 [Azure 저장소 계정](../storage/common/storage-introduction.md) toostore hello 데이터입니다.

    > [!Warning]
    > 기본적으로 hello 저장소 위치는 설정 toohello Application Insights 리소스와 동일한 지리적 지역입니다. 다른 지역에 저장하는 경우 전송 요금이 발생할 수 있습니다.

    ![추가, 내보내기 대상, 저장소 계정을 클릭한 다음 새 저장소를 만들거나 기존 저장소 선택](./media/app-insights-export-telemetry/02-add.png)

4. 만들거나 hello 저장소에서 컨테이너를 선택 합니다.

    ![이벤트 유형 선택 클릭](./media/app-insights-export-telemetry/create-container.png)

내보내기를 만들면 진행을 시작합니다. 만 hello 내보내기를 만든 후 들어오는 데이터를 가져옵니다.

약 1 시간 hello 저장소에 데이터 표시 될 때까지 지연 될 수 있습니다.

### <a name="tooedit-continuous-export"></a>연속 내보내기를 tooedit

Toochange hello 이벤트 유형을 나중 편집 hello 내보내기:

![이벤트 유형 선택 클릭](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a>연속 내보내기를 toostop

toostop hello 내보내기 사용 안 함을 클릭 합니다. 활성화를 다시 클릭 하면 새 데이터로 hello 내보내기를 다시 시작 됩니다. 내보내기 해제 된 동안 hello 포털에서 도착 하는 hello 데이터를 가져올 수 없습니다.

toostop hello 내보내기 영구적으로 삭제 합니다. 이렇게 해도 저장소에서 데이터를 삭제하지 않습니다.

### <a name="cant-add-or-change-an-export"></a>내보내기를 추가 또는 변경할 수 있나요?
* tooadd 또는 변경 내보내기 소유자, 참가자 또는 응용 프로그램 통찰력 참가자 액세스 권한을 해야합니다. [역할에 대해 알아봅니다][roles].

## <a name="analyze"></a> 어떤 이벤트를 얻나요?
hello 내보낸된 데이터는 hello 원시 원격 분석 응용 프로그램에서 수신 위치 데이터는 계산 hello 클라이언트 IP 주소에서 추가 있습니다.

여는 삭제 되었으며 데이터 [샘플링](app-insights-sampling.md) hello 내보낸 데이터에 포함 되지 않습니다.

계산된 다른 메트릭은 포함되지 않습니다. 예를 들어 म 하지 평균 CPU 활용도 내보내지만 hello 평균이 계산 되는 hello 원시 원격 분석 내보냅니다지 않습니다.

hello 데이터도 포함 된 hello 결과 [가용성 웹 테스트](app-insights-monitor-web-app-availability.md) 설정 합니다.

> [!NOTE]
> **샘플링** 응용 프로그램에서 많은 양의 데이터를 하는 경우 hello 샘플링 기능이 작동 하 고 hello 생성 된 원격 분석의 일부만 보낼 수 있습니다. [샘플링에 대해 자세히 알아봅니다.](app-insights-sampling.md)
>
>

## <a name="get"></a>Hello 데이터 검사
Hello 포털에서 직접 hello 저장소를 검사할 수 있습니다. **찾아보기**를 클릭하고 저장소 계정을 선택한 후 **컨테이너**를 엽니다.

Visual Studio에서 Azure 저장소 tooinspect 열고 **보기**, **클라우드 탐색기**합니다. (Tooinstall hello Azure SDK 메뉴 명령을 해당를 설정 하지 않은 경우 해야: 열기 hello **새 프로젝트** 대화 상자를 확장 하 고 Visual C# / 클라우드 선택 하 고 **Microsoft Azure SDK for.NET 가져오기**.)

blob 저장소를 열면 blob 파일 집합이 포함된 컨테이너가 보입니다. hello 계측 키 Application Insights 리소스 이름, 원격 분석-유형/날짜/시간에서 파생 된 각 파일의 URI입니다. (hello 리소스 이름은 모두 소문자 및 hello 계측 키 대시를 생략 합니다.)

![적합 한 도구와 hello blob 저장소를 검사 합니다.](./media/app-insights-export-telemetry/04-data.png)

hello 날짜 및 시간 UTC 이며 hello 원격 분석 hello 저장소에 보관 된-생성 된 hello 시간이 아닌 경우. 하므로 코드 toodownload hello 데이터를 작성 하는 경우 hello 데이터를 통해 선형으로 이동할 수 있습니다.

Hello 경로의 hello 형태는 다음과 같습니다.

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

Where

* `blobCreationTimeUtc`blob를 만든 시간 hello에 내부 저장소를 준비는
* `blobDeliveryTimeUtc`blob 복사 toohello 내보내기 대상 저장소를가 하는 경우 hello 시간

## <a name="format"></a> 데이터 형식
* 각 blob은 다중 '\n'-separated 행을 포함하는 텍스트 파일입니다. 약 1/2 분의 시간 동안 처리 된 hello 원격 분석을 포함 합니다.
* 각 행은 요청 또는 페이지 보기와 같은 원격 분석 데이터 요소를 나타냅니다.
* 각 행은 서식이 지정되지 않은 JSON 파일입니다. 원할 경우 toosit 및 한번 stare, Visual Studio에서 열 선택, 고급, 서식 파일을 편집 합니다.

![적합 한 도구와 보기 hello 원격 분석](./media/app-insights-export-telemetry/06-json.png)

시간 기간은 틱 단위이며 10,000틱은 1ms입니다. 이러한 값 1ms 시간을 표시 하는 예를 들어 hello 브라우저를 보내고 받았습니다의 요청 toosend tooreceive hello 브라우저에서 페이지 및 1.8s tooprocess hello:

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[세부 데이터는 hello 속성 형식 및 값에 대 한 참조를 모델링합니다.](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a>Hello 데이터 처리
작은 규모에서 떨어져 있는 일부 코드 toopull 데이터 작성, 스프레드시트에 읽기 및 등 수 있습니다. 예:

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

더 큰 코드 샘플에 대해서는 [작업자 역할 사용][exportasa]을 참조하세요.

## <a name="delete"></a>이전 데이터 삭제
저장소 용량을 관리 하 고 필요한 경우 hello 오래 된 데이터 삭제에 대 한 책임이 note 하십시오.

## <a name="if-you-regenerate-your-storage-key"></a>저장소 키를 다시 생성하는 경우...
Hello tooyour 키 저장소를 변경 하면 연속 내보내기를 작동이 중지 됩니다. Azure 계정에 알림이 표시됩니다.

Hello 연속 내보내기가 블레이드를 열고 내보내기의 편집 합니다. 내보내기 대상 hello 편집 하지만 동일한 저장소 선택 hello 둡니다. Tooconfirm 확인을 클릭 합니다.

![편집 hello 연속 내보내기을 열고 내보내기 대상을 다음 닫습니다.](./media/app-insights-export-telemetry/07-resetstore.png)

hello 연속 내보내기를 다시 시작 됩니다.

## <a name="export-samples"></a>내보내기 샘플

* [스트림 분석을 사용 하 여 내보내기 tooSQL][exportasa]
* [Stream Analytics 샘플 2](app-insights-export-stream-analytics.md)

더 큰 눈금에서 고려해 [HDInsight](https://azure.microsoft.com/services/hdinsight/) -hello 클라우드에서 Hadoop 클러스터. HDInsight 다양 한 기술 관리 하 고 빅 데이터 분석을 제공 하 고 Application Insights에서 내보낸 tooprocess 데이터를 사용할 수 있습니다.

## <a name="q--a"></a>질문과 대답
* *하지만 원하는 모든 것은 차트의 일회성 다운로드입니다.*  

    예, 수행할 수 있습니다. Hello 블레이드의 hello 위쪽 클릭 **데이터 내보내기**합니다.
* *내보내기를 설정했지만 내 저장소에 데이터가 없습니다.*

    Application Insights 받는지 모든 원격 분석 응용 프로그램에서 hello 내보내기를 설정한 후? 새 데이터만 받게 됩니다.
* *export를 tooset I 했으나 액세스가 거부 되었습니다.*

    Hello 계정 조직에서 소유 하 고, 있으면 toobe hello 소유자 또는 참가자 그룹의 구성원입니다.
* *직선 toomy 자체 온-프레미스 저장소를 내보낼 수 있습니까?*

    아니요. 죄송합니다. 우리의 내보내기 엔진은 현재 Azure 저장소에서만 작동합니다.  
* *모든 제한 toohello 양의 내 저장소에 저장 하는 데이터는 무엇입니까?*

    아니요. म 합니다 유지 데이터 될 때까지 밀어 hello 내보내기를 삭제 합니다. Blob 저장소에 대 한 외부 제한을 hello 도달할 수 있지만 매우 큰 경우 중지 됩니다. 중인지 tooyou toocontrol 저장소 사용 크기입니다.  
* *Hello 저장소에서 볼 수 blob?*

  * 모든 데이터 형식에 대해 선택한 tooexport, 새로운 blob (데이터 파일이 있는 경우) 1 분 마다 생성 됩니다.
  * 또한, 트래픽이 많은 응용 프로그램은 추가 파티션이 할당됩니다. 이 경우 모든 각 유닛이 매 분마다 blob을 생성합니다.
* *Hello toomy 키 저장소를 다시 생성 I 또는 hello 컨테이너의 hello 이름을 변경 하 고 hello 내보내기 현재 작동 하지 않습니다.*

    Hello 내보내기를 편집 하 고 hello 내보내기 대상 블레이드를 엽니다. 동일한 저장소 이전과 마찬가지로 선택 hello 두고 tooconfirm 확인을 클릭 합니다. 내보내기가 다시 시작됩니다. 지난 몇 일 동안 hello 내 hello 변경 되었으면 데이터가 손실 되지 않고 있습니다.
* *Hello 내보내기 일시 중지할 수 있습니까?*

    예. 사용 안함을 클릭합니다.

## <a name="code-samples"></a>코드 샘플

* [Stream Analytics 샘플](app-insights-export-stream-analytics.md)
* [스트림 분석을 사용 하 여 내보내기 tooSQL][exportasa]
* [세부 데이터는 hello 속성 형식 및 값에 대 한 참조를 모델링합니다.](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
