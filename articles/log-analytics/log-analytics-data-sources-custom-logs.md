---
title: "사용자 지정 aaaCollect OMS 로그 분석 로그인 | Microsoft Docs"
description: "Log Analytics는 Windows와 Linux 컴퓨터의 텍스트 파일에서 이벤트를 수집할 수 있습니다.  이 문서에서는 toodefine 새로운 사용자 지정 로그 및 hello 레코드의 세부 정보 작성 방법과 hello OMS 리포지토리에 설명 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: aca7f6bb-6f53-4fd4-a45c-93f12ead4ae1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: a75d058c371fecf7c43690a797d4e650c1570317
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-logs-in-log-analytics"></a>Log Analytics의 사용자 지정 로그
hello 사용자 지정 로그 데이터 원본 로그 분석에는 Windows 및 Linux 컴퓨터에 있는 텍스트 파일에서 toocollect 이벤트를 허용 합니다. 대부분의 응용 프로그램 Windows 이벤트 로그 또는 Syslog와 같은 표준 로깅 서비스 대신 tootext 파일 정보를 기록합니다.  Hello 로그인 hello를 사용 하 여 tooindividual 필드의 각 레코드를 구문 분석할 수 수집 면 [사용자 정의 필드](log-analytics-custom-fields.md) 로그 분석의 기능입니다.

![사용자 지정 로그 수집](media/log-analytics-data-sources-custom-logs/overview.png)

수집 된 hello 로그 파일 toobe hello 조건에 따라 일치 해야 합니다.

- hello 로그 항목이 줄에 하나씩 있을 하거나 타임 스탬프 짝이 되는 각 항목의 시작 부분 hello에 서식을 hello 다음 중 하나를 사용 해야 합니다.

    YYYY-MM-DD HH:MM:SS <br>M/D/YYYY HH:MM:SS AM/PM <br>Mon DD,YYYY HH:MM:SS

- hello 로그 파일을 허용 하지 않아야 순환 업데이트 새 항목 hello 파일은 덮어쓰여집니다.
- hello 로그 파일은 ASCII 또는 utf-8 인코딩을 사용 해야 합니다.  UTF-16 등의 다른 형식은 지원되지 않습니다.

>[!NOTE]
>Hello 로그 파일에 중복 된 항목이 있는 경우 로그 분석 로그를 수집 합니다.  그러나 hello 검색 결과 일치 하지 않을 수 hello 필터 결과 hello 결과 개수 보다 더 많은 이벤트를 표시 하는 위치입니다.  이 동작을 일으키는 hello 응용 프로그램을 만든 경우 hello 로그 toodetermine 유효성을 검사 하 고 hello 사용자 지정 로그 컬렉션 정의 만들기 전에 가능한 경우 해결 됩니다.  
>
  
## <a name="defining-a-custom-log"></a>사용자 지정 로그 정의
프로시저 toodefine 사용자 지정 로그 파일을 다음 hello를 사용 합니다.  사용자 지정 로그를 추가 하는 샘플의 연습은이 문서의 끝을 toohello 스크롤하십시오.

### <a name="step-1-open-hello-custom-log-wizard"></a>1단계. Hello 사용자 지정 로그 마법사를 열려면
사용자 지정 로그 마법사 hello hello OMS 포털에서 실행 되며 새 사용자 지정 로그 toocollect toodefine 있습니다.

1. Hello OMS 포털에서 이동 너무**설정을**합니다.
2. **데이터**를 클릭한 다음 **사용자 지정 로그**를 클릭합니다.
3. 기본적으로 모든 구성 변경 내용은 tooall 에이전트를 자동으로 이동 됩니다.  Linux 에이전트에 대 한 구성 파일에는 toohello Fluentd 데이터 수집기를 전송 됩니다.  각 Linux 에이전트에서 수동으로이 파일 toomodify 원하는 hello 확인란의 선택을 취소 한 다음 *구성 toomy Linux 컴퓨터 아래 적용*합니다.
4. 클릭 **추가 +** tooopen hello 사용자 지정 로그 마법사.

### <a name="step-2-upload-and-parse-a-sample-log"></a>2단계. 샘플 로그 업로드 및 구문 분석
Hello 사용자 지정 로그의 샘플을 업로드 하 여 시작 합니다.  hello 마법사는 구문 분석 하 고 toovalidate 하기 위해이 파일에 hello 항목을 표시 합니다.  로그 분석 hello 구분 기호를 지정 하는 tooidentify 각 레코드를 사용 합니다.

**새 줄** hello 기본 구분 기호 이며 줄에 하나씩 단일 항목이 포함 된 로그 파일에 사용 됩니다.  Hello 줄 날짜 및 시간 hello 사용 가능한 형식 중 하나로 시작 하 여 다음을 지정할 수 있습니다 하는 경우는 **타임 스탬프** 구분 기호는 둘 이상의 줄에 걸쳐 있는 항목을 지원 합니다.

타임 스탬프 구분 기호를 사용 하는 경우 OMS에 저장 된 각 레코드의 hello TimeGenerated 속성 됩니다 hello 날짜/시간 hello 로그 파일에서 해당 항목에 대해 지정 된 채울 수 있습니다.  새 줄 구분 기호를 사용 하는 경우 TimeGenerated은 날짜 및 시간은 로그 분석 수집 hello 항목으로 채워집니다.

> [!NOTE]
> 현재 로그 분석 hello 날짜/시간에서 UTC로 타임 스탬프 구분 기호를 사용 하 여 로그 수집을 처리 합니다.  곧 hello 에이전트에서 변경 된 toouse hello 표준 시간대 사용 됩니다.
>
>

1. 클릭 **찾아보기** tooa 샘플 파일을 찾습니다.  일부 브라우저에서는 이 단추의 레이블이 **파일 선택** 인 경우도 있습니다.
2. **다음**을 누릅니다.
3. 사용자 지정 로그 마법사 hello를 식별 하는 hello 파일 및 목록 hello 레코드를 업로드 합니다.
4. 사용 되는 tooidentify 새 레코드를 구성 된 hello 구분 기호 및 로그 파일의 hello 레코드를 가장 잘 식별 하는 select hello 구분 기호를 변경 합니다.
5. **다음**을 누릅니다.

### <a name="step-3-add-log-collection-paths"></a>3단계. 로그 수집 경로 추가
Hello 사용자 지정 로그를 찾을 수 있는 hello 에이전트에서 하나 이상의 경로 정의 해야 합니다.  특정 경로 및 hello 로그 파일에 대 한 이름을 입력 하거나 또는 와일드 카드 hello 이름에 대 한 경로 지정할 수 있습니다.  이렇게 하면 매일 새 파일을 만드는 응용 프로그램을 지원하거나 하나의 파일이 일정한 크기에 도달하는 경우를 지원합니다.  하나의 로그 파일에 여러 경로를 제공할 수도 있습니다.

예를 들어 응용 프로그램 수 로그 파일을 매일 날짜로를 만들어 hello log20100316.txt에서와 같이 hello 이름에 포함 합니다. 이러한 로그에 대 한 패턴 수도 *로그\*.txt* hello 응용 프로그램을 다음 tooany 로그 파일을 적용할 수 있는 명명 체계입니다.

hello 다음 표에서 유효한 패턴의 예 toospecify 서로 다른 파일.

| 설명 | Path |
|:--- |:--- |
| Windows 에이전트에서 확장명이 .txt인 *C:\Logs* 내 모든 파일 |C:\Logs\\\*.txt |
| Windows 에이전트에서 이름이 log로 시작되고 확장명이 .txt인 *C:\Logs* 내 모든 파일 |C:\Logs\log\*.txt |
| Linux 에이전트에서 확장명이 .txt인 */var/log/audit* 내 모든 파일 |/var/log/audit/*.txt |
| Linux 에이전트에서 이름이 log로 시작되고 확장명이 .txt인 */var/log/audit* 내 모든 파일 |/var/log/audit/log\*.txt |

1. 어떤 경로 형식을 추가 하는 Windows 또는 Linux toospecify를 선택 합니다.
2. Hello 경로 입력 하 고 hello 클릭  **+**  단추입니다.
3. 모든 추가 경로 대 한 hello 프로세스를 반복 합니다.

### <a name="step-4-provide-a-name-and-description-for-hello-log"></a>4단계. 이름 및 hello 로그에 대 한 설명을 제공 합니다.
hello 지정한 이름이 사용 됩니다 hello 로그 형식에 대해 위에서 설명한 것 처럼.  항상으로 끝납니다 _CL toodistinguish 것으로 사용자 지정 로그 합니다.

1. Hello 로그에 대 한 이름을 입력 합니다.  hello  **\_CL** 접미사가 자동으로 제공 됩니다.
2. 선택적인 **설명**을 추가합니다.
3. 클릭 **다음** toosave hello 사용자 지정 로그 정의 합니다.

### <a name="step-5-validate-that-hello-custom-logs-are-being-collected"></a>5단계. Hello 사용자 지정 로그를 수집 하는 유효성 검사
로그 분석에서 새 사용자 지정 로그 tooappear에서 초기 데이터 hello에 대 한 tooan 시간을 걸릴 수 있습니다.  Hello에서 항목을 수집을 시작 하면 정의 된 hello 사용자 지정 로그에 hello 지 점으로부터 지정한 로그 hello 경로에서 발견 합니다.  Hello 사용자 지정 로그를 만드는 중에 업로드 하는 hello 항목 유지 되지 않습니다 되지만 찾을 hello 로그 파일에 이미 기존 항목을 수집 합니다.

로그 분석 시작 hello 사용자 지정 로그에서에서 수집 되 면 해당 레코드는 로그 검색을 통해 가능 합니다.  Hello 사용자 지정 로그 hello로 지정한 사용 하 여 hello 이름을 **형식** 쿼리에 합니다.

> [!NOTE]
> Hello RawData 속성 hello 검색에서 없는 경우에 tooclose 필요 하 고 브라우저를 다시 열 수 있습니다.
>
>

### <a name="step-6-parse-hello-custom-log-entries"></a>6단계. Hello 사용자 지정 로그 항목을 구문 분석
hello 전체 로그 항목 라는 단일 속성에 저장 될 **RawData**합니다.  대개 tooseparate hello 다른 여러 hello 레코드에 저장 된 개별 속성에 각 항목에 대 한 정보 해야 합니다.  이렇게 하면 hello를 사용 하 여 [사용자 정의 필드](log-analytics-custom-fields.md) 로그 분석의 기능입니다.

Hello 사용자 지정 로그 항목을 구문 분석 하는 자세한 단계는 여기 제공 되지 않습니다.  Toohello를 참조 하십시오 [사용자 정의 필드](log-analytics-custom-fields.md) 이 정보에 대 한 설명서입니다.

## <a name="disabling-a-custom-log"></a>사용자 지정 로그 비활성화
생성된 사용자 지정 로그 정의는 제거할 수 없지만 모든 수집 경로를 제거하여 비활성화할 수 있습니다.

1. Hello OMS 포털에서 이동 너무**설정을**합니다.
2. **데이터**를 클릭한 다음 **사용자 지정 로그**를 클릭합니다.
3. 클릭 **세부 정보** 다음 toohello 사용자 지정 로그 정의 toodisable 합니다.
4. 각 사용자 지정 로그 정의 hello에 대 한 hello 컬렉션 경로 제거 합니다.

## <a name="data-collection"></a>데이터 수집
Log Analytics는 각 사용자 지정 로그로부터 새로운 항목을 약 5분마다 수집합니다.  hello 에이전트는 해당 위치를 수집 하는 각 로그 파일에 기록 합니다.  Hello 에이전트 일정 시간 동안 오프 라인이 되 면 다음 로그 분석에서 수집 합니다 항목 마지막 중단, hello 에이전트 오프 라인 상태일 때 해당 항목을 만든 경우에.

hello 로그 항목의 전체 내용이 hello 라는 tooa 단일 속성이 기록 **RawData**합니다.  분석 및 정의 하 여 개별적으로 검색할 수 있는 여러 속성에이 구문을 분석할 수 있습니다 [사용자 지정 필드](log-analytics-custom-fields.md) hello 사용자 지정 로그를 만든 후 합니다.

## <a name="custom-log-record-properties"></a>사용자 지정 로그 레코드 속성
사용자 지정 로그 레코드를 제공 하 고 다음 표에 hello에 대 한 속성을 hello 하는 hello 로그 이름 가진 유형을 가져야 합니다.

| 속성 | 설명 |
|:--- |:--- |
| TimeGenerated |날짜 및 시간을 레코드 hello 로그 분석에 의해 수집 된 합니다.  Hello 로그 시간 기반 구분 기호를 사용 하는 경우 이것이 hello 항목에서 수집 하는 hello 시간입니다. |
| SourceSystem |에이전트 hello 레코드 종류에서 수집 되었습니다. <br> OpsManager – Windows 에이전트, 직접 연결 또는 System Center Operations Manager <br> Linux – 모든 Linux 에이전트 |
| RawData |Hello의 전체 텍스트 항목을 수집 합니다. |
| ManagementGroupName |에이전트 시스템 센터 작업 관리에 대 한 hello 관리 그룹의 이름입니다.  다른 에이전트의 경우 AOI-\<작업 영역 ID\>입니다. |

## <a name="log-searches-with-custom-log-records"></a>사용자 지정 로그 레코드를 사용한 로그 검색
사용자 지정 로그의 레코드를 다른 데이터 원본의 레코드와 마찬가지로 hello OMS 리포지토리에 저장 됩니다.  특정 로그에서 수집 된 검색 tooretrieve 레코드의 hello Type 속성을 사용할 수 있도록 hello 로그를 정의 하는 경우 제공 하는 hello 이름과 일치 하는 형식을 갖게 됩니다.

hello 다음 표에서 사용자 지정 로그에서 레코드를 검색 하는 로그 검색의 다른 예.

| 쿼리 | 설명 |
|:--- |:--- |
| Type=MyApp_CL |이름 MyApp_CL인 사용자 지정 로그의 모든 이벤트. |
| Type=MyApp_CL Severity_CF=error |이름이 *Severity_CF*인 사용자 지정 필드의 값이 *error*이고 이름이 MyApp_CL인 사용자 지정 로그의 모든 이벤트. |

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.

> | 쿼리 | 설명 |
|:--- |:--- |
| MyApp_CL |이름 MyApp_CL인 사용자 지정 로그의 모든 이벤트. |
| MyApp_CL &#124; where Severity_CF=="error" |이름이 *Severity_CF*인 사용자 지정 필드의 값이 *error*이고 이름이 MyApp_CL인 사용자 지정 로그의 모든 이벤트. |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a>사용자 지정 로그 추가 샘플 연습
hello 다음 섹션 안내 사용자 지정 로그를 만드는 예제입니다.  수집 되 고 hello 샘플 로그 시작 날짜 및 코드, 상태 및 메시지에 대 한 시간 및 다음 쉼표로 구분 된 필드의 각 줄에 단일 항목에 있습니다.  몇 가지 샘플 항목이 아래에 표시되어 있습니다.

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect toodatabase
    2016-03-10 01:31:34 303,Error,Application lost connection toodatabase

### <a name="upload-and-parse-a-sample-log"></a>샘플 로그 업로드 및 구문 분석
Hello 로그 파일 중 하나를 제공 하 고 수집 됩니다 hello 이벤트를 볼 수 있습니다.  이 경우 New Line(새 줄)은 충분한 구분 기호입니다.  그러나 hello 로그의 단일 항목을 여러 줄에 걸쳐 수, 하는 경우 타임 스탬프 구분 기호는 toobe 사용 해야 합니다.

![샘플 로그 업로드 및 구문 분석](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a>로그 수집 경로 추가
hello 로그 파일에 배치 됩니다 *C:\MyApp\Logs*합니다.  매일 hello 패턴에서 hello 날짜를 포함 하는 이름의 새 파일이 생성 됩니다 *appYYYYMMDD.log*합니다.  이 로그에 충분한 패턴은 *C:\MyApp\Logs\\\*.log*입니다.

![로그 수집 경로](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-hello-log"></a>이름 및 hello 로그에 대 한 설명을 제공 합니다.
*MyApp_CL*이라는 이름을 사용하여 **설명**을 입력합니다.

![로그 이름](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-hello-custom-logs-are-being-collected"></a>Hello 사용자 지정 로그를 수집 하는 유효성 검사
쿼리 사용 *형식 MyApp_CL =* tooreturn 모든 hello 수집 된 로그에서를 기록 합니다.

![사용자 지정 필드가 없는 로그 쿼리](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-hello-custom-log-entries"></a>Hello 사용자 지정 로그 항목을 구문 분석
사용자 정의 필드 toodefine hello 사용 하 여 *EventTime*, *코드*, *상태*, 및 *메시지* 필드 및 우리는 hello hello 차이 볼 수 있습니다 hello 쿼리에서 반환 되는 레코드입니다.

![사용자 지정 필드가 있는 로그 쿼리](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a>다음 단계
* 사용 하 여 [사용자 지정 필드](log-analytics-custom-fields.md) tooparse hello hello tooindividual 필드에 사용자 지정 로그 항목입니다.
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다.
