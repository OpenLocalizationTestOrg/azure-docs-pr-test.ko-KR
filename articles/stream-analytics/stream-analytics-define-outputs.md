---
title: "Stream Analytics 출력: 저장소에 대한 옵션, 분석 | Microsoft Docs"
description: "분석 결과에 대한 Power BI를 포함하는 스트림 분석 데이터 출력 옵션을 대상으로 하는 방법을 알아봅니다."
keywords: "데이터 변환, 분석 결과, 데이터 저장소 옵션"
services: stream-analytics,documentdb,sql-database,event-hubs,service-bus,storage
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ba6697ac-e90f-4be3-bafd-5cfcf4bd8f1f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 99f8113f0464960e898293397fbe3de90d669857
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-outputs-options-for-storage-analysis"></a>스트림 분석 출력: 저장소에 대한 옵션, 분석
스트림 분석 작업을 만들 때 hello 결과 데이터는 사용 하는 방법을 고려 합니다. Hello 스트림 분석 작업의 hello 결과 보는 방법 및 됩니다 저장할 것?

순서 tooenable 다양 한 응용 프로그램 패턴에서에서 Azure 스트림 분석에 출력을 저장 하 고 분석 결과 보는 다른 옵션이 있습니다. 쉽게 tooview 작업 출력을 쉽게 있고 데이터 웨어하우스 및 기타 용도의 hello 소비 및 저장소 hello 작업 출력의 유연성을 제공 합니다. 어떠한 출력도 hello 작업에 구성 된 hello 작업이 시작 되 고 이벤트 전송이 시작 되기 전에 존재 해야 합니다. 예를 들어 Blob 저장소를 사용 하 여 출력을 출력으로 hello 작업 자동으로 저장소 계정을 만들지 않습니다. Hello ASA 작업을 시작 하기 전에 hello 사용자가 만든 toobe가 필요 합니다.

## <a name="azure-data-lake-store"></a>Azure Data Lake Store
스트림 분석은 [Azure Data Lake 저장소](https://azure.microsoft.com/services/data-lake-store/)를 지원합니다. 이 저장소를 통해 운영 및 예비 분석에 대 한 원하는 크기, 유형 및 수집 속도의 toostore 데이터입니다. 또한, 스트림 분석 요구 toobe 권한이 tooaccess hello 데이터 레이크 저장소. 권한 부여 및 toosign hello 데이터 레이크 저장소 (필요한 경우)에 대해이 hello에 대해서는 설명에 대 한 내용은 [데이터 레이크 출력 문서](stream-analytics-data-lake-output.md)합니다.

### <a name="authorize-an-azure-data-lake-store"></a>Azure Data Lake 저장소 권한 부여
데이터 레이크 저장소를 hello Azure 포털에서에서 출력으로 선택 하는 경우 메시지 표시 tooauthorize 연결 tooan 기존 Data Lake 저장소 됩니다.  

![Data Lake 저장소 권한 부여](./media/stream-analytics-define-outputs/06-stream-analytics-define-outputs.png)  

데이터 레이크 저장소 아래와 같이 출력 hello에 대 한 hello 속성을 입력 합니다.

![Data Lake 저장소 권한 부여](./media/stream-analytics-define-outputs/07-stream-analytics-define-outputs.png)  

hello 아래 표에 hello 속성 이름 및 데이터 레이크 저장소 출력을 만드는 데 필요한 설명 합니다.

<table>
<tbody>
<tr>
<td><B>속성 이름</B></td>
<td><B>설명</B></td>
</tr>
<tr>
<td>출력 별칭</td>
<td>쿼리 toodirect hello 쿼리 출력 toothis Data Lake 저장소에에서 사용 되는 친숙 한 이름입니다.</td>
</tr>
<tr>
<td>계정 이름</td>
<td>hello 이름 hello 출력을 보내는 데이터 레이크 저장소 계정입니다. 드롭 다운 toohello 포털에 기록 toowhich hello 사용자 권한이 데이터 레이크 저장소 계정 목록이 표시 됩니다.</td>
</tr>
<tr>
<td>경로 접두사 패턴[<I>선택 사항</I>]</td>
<td>파일에 사용 된 경로 toowrite hello hello 내에서 파일 데이터 레이크 저장소 계정을 지정 합니다. <BR>{date}, {time}<BR>예제 1: folder1/logs/{date}/{time}<BR>예제 2: folder1/logs/{date}</td>
</tr>
<tr>
<td>날짜 형식[<I>선택 사항</I>]</td>
<td>Hello 날짜 토큰이 hello 접두사 경로에 사용 되며, hello 날짜 형식을 사용자 파일 구성할 지를 선택할 수 있습니다. 예: YYYY/MM/DD</td>
</tr>
<tr>
<td>시간 형식[<I>선택 사항</I>]</td>
<td>Hello 시간 토큰이 hello 접두사 경로에 사용 되며, 경우에 파일 구성 됩니다 hello 시간 형식을 지정 합니다. 현재 hello만 지원 점은 HH입니다.</td>
</tr>
<tr>
<td>이벤트 직렬화 형식</td>
<td>출력 데이터에 대한 직렬화 형식입니다. JSON, CSV 및 Avro를 지원합니다.</td>
</tr>
<tr>
<td>인코딩</td>
<td>CSV 또는 JSON 형식인 경우 인코딩을 지정해야 합니다. U t F-8 hello만 현재 지원 인코딩 형식입니다.</td>
</tr>
<tr>
<td>구분 기호</td>
<td>CSV 직렬화에만 적용됩니다. 스트림 분석은 CSV 데이터를 직렬화하기 위해 다양하고 일반적인 구분 기호를 지원합니다. 지원되는 값은 쉼표, 세미콜론, 공백, 탭 및 세로 막대입니다.</td>
</tr>
<tr>
<td>형식</td>
<td>JSON 직렬화에만 적용됩니다. 줄 바꿈을 하 여 지정 hello 출력 각 JSON 개체를 새 줄으로 구분 하 여 형식이 지정 됩니다. 배열 지정 hello 출력 JSON 개체의 배열으로 형식이 지정 됩니다.</td>
</tr>
</tbody>
</table>

### <a name="renew-data-lake-store-authorization"></a>Data Lake 저장소 권한 부여 갱신
Toore 해야-암호는 작업을 만들거나 마지막으로 인증 된 이후에 변경 된 경우 사용자 데이터 레이크 저장소 계정을 인증 합니다.

![Data Lake 저장소 권한 부여](./media/stream-analytics-define-outputs/08-stream-analytics-define-outputs.png)  

## <a name="sql-database"></a>SQL 데이터베이스
[Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/) 를 사용할 수 있습니다. 스트림 분석 작업 Azure SQL 데이터베이스에서 tooan 기존 테이블을 작성 합니다.  Note 해당 hello 테이블 스키마는 작업에서 출력 되 고 해당 형식과 hello 필드에 정확히 일치 해야 합니다. [Azure SQL 데이터 웨어하우스](https://azure.microsoft.com/documentation/services/sql-data-warehouse/) hello SQL 데이터베이스 출력 옵션을 함께 (이 미리 보기 기능)를 통해 출력으로 지정할 수도 있습니다. hello 아래 표에 hello 속성 이름 및 SQL 데이터베이스 출력을 생성 하는 것에 대 한 설명입니다.

| 속성 이름 | 설명 |
| --- | --- |
| 출력 별칭 |쿼리 toodirect hello 쿼리 출력 toothis 데이터베이스에 사용 되는 친숙 한 이름입니다. |
| 데이터베이스 |출력을 보내는 hello 데이터베이스의 hello 이름 |
| 서버 이름 |hello SQL 데이터베이스 서버 이름 |
| 사용자 이름 |hello access toowrite toohello 데이터베이스에 사용자 이름 |
| 암호 |hello 암호 tooconnect toohello 데이터베이스 |
| 테이블 |hello 테이블 이름 hello 출력 기록 될 위치입니다. hello 테이블 이름은 대/소문자 구분 하 고이 테이블의 hello 스키마에는 필드 및 작업 출력에서 생성 하는 개체 유형의 정확히 toohello 수와 일치 해야 합니다. |

> [!NOTE]
> 현재 Azure SQL 데이터베이스 제공 hello 스트림 분석에서 작업 출력에 대 한 지원 됩니다. 그러나 데이터베이스가 연결된 SQL Server를 실행하는 Azure 가상 컴퓨터는 지원되지 않습니다. 이 이후 릴리스에서 주체 toochange입니다.
> 
> 

## <a name="blob-storage"></a>Blob 저장소
Blob 저장소 hello 클라우드에 많은 양의 구조화 되지 않은 데이터를 저장 하기 위한 비용 효율적이 고 확장 가능한 솔루션을 제공 합니다.  Azure Blob 저장소와 사용법에 대 한 소개를 hello 설명서를 참조 합니다. [toouse Blob 어떻게](../storage/blobs/storage-dotnet-how-to-use-blobs.md)합니다.

hello 아래 표에 hello 속성 이름 및 blob 출력을 생성 하는 것에 대 한 설명입니다.

<table>
<tbody>
<tr>
<td>속성 이름</td>
<td>설명</td>
</tr>
<tr>
<td>출력 별칭</td>
<td>쿼리 toodirect hello 쿼리 출력 toothis blob 저장소에 사용 되는 친숙 한 이름입니다.</td>
</tr>
<tr>
<td>저장소 계정</td>
<td>출력을 보내는 hello 저장소 계정의 hello 이름입니다.</td>
</tr>
<tr>
<td>저장소 계정 키</td>
<td>hello 저장소 계정과 연결 된 hello 비밀 키입니다.</td>
</tr>
<tr>
<td>저장소 컨테이너</td>
<td>컨테이너는 hello Microsoft Azure Blob 서비스에에서 저장 된 blob에 대 한 논리적 그룹화를 제공 합니다. Blob toohello Blob 서비스에 업로드할 때 해당 blob에 대 한 컨테이너를 지정 해야 합니다.</td>
</tr>
<tr>
<td>경로 접두사 패턴 [선택 사항]</td>
<td>hello 파일 경로 toowrite hello 지정 된 컨테이너 내에서 blob을 사용 합니다.<BR>Hello 경로 내 toouse hello blob 작성 된 2 변수 toospecify hello 주파수 다음의 하나 이상의 인스턴스를 선택할 수 있습니다.<BR>{date}, {time}<BR>예제 1: cluster1/logs/{date}/{time}<BR>예제 2: cluster1/logs/{date}</td>
</tr>
<tr>
<td>날짜 형식[선택 사항]</td>
<td>Hello 날짜 토큰이 hello 접두사 경로에 사용 되며, hello 날짜 형식을 사용자 파일 구성할 지를 선택할 수 있습니다. 예: YYYY/MM/DD</td>
</tr>
<tr>
<td>시간 형식[선택 사항]</td>
<td>Hello 시간 토큰이 hello 접두사 경로에 사용 되며, 경우에 파일 구성 됩니다 hello 시간 형식을 지정 합니다. 현재 hello만 지원 점은 HH입니다.</td>
</tr>
<tr>
<td>이벤트 직렬화 형식</td>
<td>출력 데이터에 대한 직렬화 형식입니다.  JSON, CSV 및 Avro를 지원합니다.</td>
</tr>
<tr>
<td>인코딩</td>
<td>CSV 또는 JSON 형식인 경우 인코딩을 지정해야 합니다. U t F-8 hello만 현재 지원 인코딩 형식입니다.</td>
</tr>
<tr>
<td>구분 기호</td>
<td>CSV 직렬화에만 적용됩니다. 스트림 분석은 CSV 데이터를 직렬화하기 위해 다양하고 일반적인 구분 기호를 지원합니다. 지원되는 값은 쉼표, 세미콜론, 공백, 탭 및 세로 막대입니다.</td>
</tr>
<tr>
<td>형식</td>
<td>JSON 직렬화에만 적용됩니다. 줄 바꿈을 하 여 지정 hello 출력 각 JSON 개체를 새 줄으로 구분 하 여 형식이 지정 됩니다. 배열 지정 hello 출력 JSON 개체의 배열으로 형식이 지정 됩니다. 이 배열은 hello 작업 중지 또는 Stream Analytics toohello 다음 시간 창에서 이동한가 경우에 중지 됩니다. 일반적으로 것는 구분 된 JSON, 특수 한 처리 hello 파일을 출력 하는 동안 필요 하지 않으므로 여전히에 쓰여지는 하는 것이 좋습니다 toouse 선입니다.</td>
</tr>
</tbody>
</table>

## <a name="event-hub"></a>이벤트 허브
[이벤트 허브](https://azure.microsoft.com/services/event-hubs/) 는 확장성이 뛰어난 게시-구독 이벤트 수집기입니다. 초당 수 백만의 이벤트를 수집할 수 있습니다.  스트림 분석 작업의 출력을 hello 다른 스트리밍 작업의 hello 입력 될 때 출력으로 이벤트 허브의 용도 중 하나 표시 합니다.

몇 가지 매개 변수를 출력으로 필요한 tooconfigure 이벤트 허브 데이터 스트림을 있습니다.

| 속성 이름 | 설명 |
| --- | --- |
| 출력 별칭 |쿼리 toodirect hello 쿼리 출력 toothis 이벤트 허브에서에서 사용 되는 친숙 한 이름입니다. |
| 서비스 버스 네임스페이스 |서비스 버스 네임스페이스는 메시징 엔터티 집합에 대한 컨테이너입니다. 새 이벤트 허브를 만들 때 서비스 버스 네임스페이스도 만들었습니다. |
| 이벤트 허브 |이벤트 허브 출력의 hello 이름 |
| 이벤트 허브 정책 이름 |hello 공유 액세스 정책 hello 이벤트 허브 구성 탭에서 만들 수 있습니다. 각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다. |
| 이벤트 허브 정책 키 |tooauthenticate 액세스 toohello 서비스 버스 네임 스페이스를 사용 하는 hello 공유 액세스 키 |
| 파티션 키 열 [선택 사항] |이벤트 허브 출력에 대 한 hello 파티션 키를 포함 하는이 열이 있습니다. |
| 이벤트 직렬화 형식 |출력 데이터에 대한 직렬화 형식입니다.  JSON, CSV 및 Avro를 지원합니다. |
| 인코딩 |CSV 및 JSON에 대 한 u t F-8은 hello만 현재 지원 인코딩 형식 |
| 구분 기호 |CSV 직렬화에만 적용됩니다. 스트림 분석은 CSV 형식에서 데이터를 직렬화하기 위해 다양하고 일반적인 구분 기호를 지원합니다. 지원되는 값은 쉼표, 세미콜론, 공백, 탭 및 세로 막대입니다. |
| 형식 |JSON 형식에만 적용됩니다. 줄 바꿈을 하 여 지정 hello 출력 각 JSON 개체를 새 줄으로 구분 하 여 형식이 지정 됩니다. 배열 지정 hello 출력 JSON 개체의 배열으로 형식이 지정 됩니다. |

## <a name="power-bi"></a>Power BI
[Power BI](https://powerbi.microsoft.com/) 분석 결과의 다양 하 게 시각화할 경험에 대 한 스트림 분석 작업 tooprovide에 대 한 출력으로 사용할 수 있습니다. 작업 대시보드, 보고서 생성 및 메트릭 제어 보고에 이 기능을 이용할 수 있습니다.

### <a name="authorize-a-power-bi-account"></a>Power BI 계정 권한 부여
1. Power BI를 hello Azure 포털에서에서 출력으로 선택 하는 경우 기존 Power BI 사용자 또는 새 Power BI 계정 toocreate 증명된 tooauthorize 여야 합니다.  
   
   ![Power BI 사용자 권한 부여](./media/stream-analytics-define-outputs/01-stream-analytics-define-outputs.png)  
2. 아직 없다면 새 계정을 만들고 지금 권한 부여를 클릭합니다.  Hello 다음과 같은 화면이 표시 됩니다.  
   
   ![Azure 계정 Power BI](./media/stream-analytics-define-outputs/02-stream-analytics-define-outputs.png)  
3. 이 단계에서는 hello 회사 또는 학교 제공 hello Power BI 출력 권한 부여를 위한 계정입니다. 아직 Power BI에 등록하지 않은 경우 지금 등록을 선택합니다. hello Power BI에 사용할 회사 또는 학교 계정 다를 수 있습니다 hello 현재 로그인 하는 Azure 구독 계정.

### <a name="configure-hello-power-bi-output-properties"></a>Hello Power BI 출력 속성 구성
Hello Power BI 계정 인증을 사용 하는 후에 Power BI 출력에 대 한 hello 속성을 구성할 수 있습니다. 다음 hello 표는 속성 이름의 hello 목록과 해당 설명 tooconfigure Power BI 출력 합니다.

| 속성 이름 | 설명 |
| --- | --- |
| 출력 별칭 |쿼리 toodirect hello 쿼리 출력 toothis PowerBI 출력에에서 사용 되는 친숙 한 이름입니다. |
| 그룹 작업 영역 |선택할 수 있습니다 다른 Power BI 사용자와 데이터를 공유 tooenable 내 Power BI 그룹 계정 또는 toowrite tooa 그룹 하지 않을 경우 "내 작업 영역"을 선택 합니다.  기존 그룹 업데이트 hello Power BI 인증을 갱신 해야 합니다. |
| 데이터 집합 이름 |Power BI hello에 대 한 필요한 데이터 집합 이름을 toouse 출력을 제공 합니다. |
| 테이블 이름 |Power BI 출력 hello의 hello 데이터 집합 아래에 테이블 이름을 제공 합니다. 현재, 스트림 분석 작업의 Power BI 출력에는 하나의 데이터 집합에 하나의 테이블만 있을 수 있습니다. |

Power BI 출력 및 대시보드를 구성 하는 연습 및 hello를 참조 하십시오 [Azure Stream Analytics 및 Power BI](stream-analytics-power-bi-dashboard.md) 문서.

> [!NOTE]
> 명시적으로 만들지 마십시오 hello 데이터 집합 및 테이블 hello Power BI 대시보드에. hello 데이터 집합 및 테이블은 자동으로 채워집니다 hello 작업이 시작 됩니다. hello 작업 Power BI에 대리 펌핑 출력을 시작 하는 경우. note hello 작업 쿼리는 모든 결과, hello 데이터 집합 생성 하지 하 고 테이블 생성 되지 것입니다. 또한 Power BI는 데이터 집합과 포함 된 테이블에 이미 있던 경우 hello hello와 같은 이름을 하나 제공이 Stream Analytics 작업에서 기존 데이터를 hello 주의 합니다.
> 
> 

### <a name="schema-creation"></a>스키마 생성
Azure 스트림 분석에 아직 없는 경우 Power BI 데이터 집합 및 hello 사용자를 대신 하 여 테이블을 만듭니다. 다른 모든 경우에는 새 값으로 hello 테이블이 업데이트 됩니다. 현재는 hello 제한 데이터 집합 내에서 해당 테이블을 하나만 존재할 수 있습니다.

### <a name="data-type-conversion-from-asa-toopower-bi"></a>데이터 형식 ASA tooPower BI에서 변환
Azure 스트림 분석 hello 출력 스키마를 변경 하는 경우 런타임에 동적으로 hello 데이터 모델을 업데이트 합니다. 열 이름 변경, 열 형식 변경 하 고 hello 추가 하거나 제거 열 모두 추적 됩니다.

이 표에에서 사용 되는 데이터 형식 변환 hello [스트림 분석 데이터 형식](https://msdn.microsoft.com/library/azure/dn835065.aspx) tooPower BIs [엔터티 데이터 모델 (EDM) 형식을](https://powerbi.microsoft.com/documentation/powerbi-developer-walkthrough-push-data/) POWER BI 데이터 집합 및 테이블을 존재 하지 않는 경우.


Stream Analytics에서 | tooPower BI
-----|-----|------------
bigint | Int64
nvarchar(max) | string
datetime | DateTime
float | Double
레코드 배열 | 문자열 형식, 상수 값 "IRecord" 또는 "IArray"

### <a name="schema-update"></a>스키마 업데이트
스트림 분석 hello 첫 번째 hello 출력의 이벤트 집합에 따라 hello 데이터 모델 스키마를 유추 합니다. 이상에서 필요한 경우 hello 데이터 모델 스키마는 업데이트 된 tooaccommodate 들어오는 이벤트 hello 원래 스키마에 맞지 않을 수 있습니다.

hello `SELECT *` 쿼리 피해 야 행 전체 tooprevent 동적 스키마를 업데이트 합니다. 또한 toopotential 성능에 영향도 될 수 indeterminacy hello 결과 대 한 사용한 hello 시간입니다. Power BI 대시보드에 표시 된 toobe 해야 하는 hello 정확한 필드를 선택 해야 합니다. 또한 hello 데이터 값 데이터 형식을 선택 하는 hello로 규격 이어야 합니다.


이전/현재 | Int64 | string | DateTime | Double
-----------------|-------|--------|----------|-------
Int64 | Int64 | string | 문자열 | Double
Double | Double | string | 문자열 | Double
string | 문자열 | 문자열 | 문자열 |  | string | 
DateTime | string | string |  DateTime | string


### <a name="renew-power-bi-authorization"></a>Power BI 권한 부여 갱신
Toore 해야-암호는 작업을 만들거나 마지막으로 인증 된 이후에 변경 된 경우 사용자 Power BI 계정을 인증 합니다. Multi-factor Authentication (MFA)은 Azure Active Directory (AAD) 테 넌 트에 구성 된 경우에 toorenew Power BI 권한 부여 2 주마다 해야 합니다. 이 문제의 증상은 작업 출력 없음 "Authenticate 사용자 오류가" hello 작업 로그에서:

  ![Power BI 새로 고침 토큰 오류](./media/stream-analytics-define-outputs/03-stream-analytics-define-outputs.png)  

tooresolve이이 문제를 실행 중인 작업을 중지 하 고 Power BI 출력 tooyour 이동 합니다.  Hello "갱신 인증" 링크를 클릭 하 고 마지막으로 중지 된 시간 tooavoid 데이터 손실 hello에서 작업을 다시 시작 합니다.

  ![Power BI 갱신 권한 부여](./media/stream-analytics-define-outputs/04-stream-analytics-define-outputs.png)  

## <a name="table-storage"></a>테이블 저장소
[Azure 테이블 저장소](../storage/common/storage-introduction.md) 응용 프로그램 toomeet 사용자 요구를 자동으로 확장할 수 있도록 고가용성, 확장성이 매우 뛰어난 저장소를 제공 합니다. 테이블 저장소는 Microsoft의 NoSQL 키/특성 저장소 한 hello 스키마에 덜 제약 조건이 있는 구조화 된 데이터를 활용할 수 있습니다. Azure 테이블 저장소에 사용 되는 toostore 데이터 지 속성 및 검색 하는 효율적인 수 있습니다.

hello 아래 표에 hello 속성 이름 및 테이블 출력을 생성 하는 것에 대 한 설명입니다.

| 속성 이름 | 설명 |
| --- | --- |
| 출력 별칭 |쿼리 toodirect hello 쿼리 출력 toothis 테이블 저장소에 사용 되는 친숙 한 이름입니다. |
| 저장소 계정 |출력을 보내는 hello 저장소 계정의 hello 이름입니다. |
| 저장소 계정 키 |hello 저장소 계정과 연결 된 선택 키를 hello입니다. |
| 테이블 이름 |hello 테이블의 hello 이름입니다. 존재 하지 않는 경우 hello 테이블 작성 됩니다. |
| Partition Key |hello 출력 열 포함 hello 파티션 키의 hello 이름입니다. hello 파티션 키는 엔터티의 기본 키의 hello 첫 번째 부분을 구성 하는 지정 된 테이블 내 hello 파티션에 대 한 고유 식별자입니다. 크기가 too1 KB 하거나 나타낼 수 있는 문자열 값입니다. |
| Row Key |hello 이름 hello 출력 열 포함 hello 행 키입니다. hello 행 키는 지정 된 파티션 내 엔터티에 대 한 고유 식별자입니다. Hello는 엔터티의 기본 키의 두 번째 부분을 형성합니다. hello 행 키는 크기가 too1 KB 하거나 나타낼 수 있는 문자열 값입니다. |
| 배치 크기 |일괄 처리 작업에 대 한 레코드 hello 수입니다. Toohello 참조 hello 기본값은 대부분의 작업에 대 한 충분 한 일반적으로 [테이블 작업을 일괄 처리 사양](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx) 에 대 한 자세한 내용은이 설정을 수정 합니다. |

## <a name="service-bus-queues"></a>Service Bus 큐
[서비스 버스 큐](https://msdn.microsoft.com/library/azure/hh367516.aspx) 는 첫 번째 In, 선입 선출 (FIFO) 메시지 배달 tooone 자세한 경쟁 소비자를 제공 합니다. 일반적으로 메시지는 예상된 toobe hello 수신기는 toohello 큐에 추가 된 각 메시지는 수신 처리 하며 하나의 메시지 소비자만 hello 임시 순서에 의해 수신 및 처리 합니다.

hello 아래 표에 hello 속성 이름 및 큐 출력을 생성 하는 것에 대 한 설명입니다.

| 속성 이름 | 설명 |
| --- | --- |
| 출력 별칭 |쿼리 toodirect hello 쿼리 출력 toothis 서비스 버스 큐에에서 사용 되는 친숙 한 이름입니다. |
| 서비스 버스 네임스페이스 |서비스 버스 네임스페이스는 메시징 엔터티 집합에 대한 컨테이너입니다. |
| 큐 이름 |서비스 버스 큐 hello의 hello 이름입니다. |
| 큐 정책 이름 |큐를 만들 때에 hello 큐 구성 탭에서 공유 액세스 정책을 만들 수 있습니다. 각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다. |
| 큐 정책 키 |tooauthenticate 액세스 toohello 서비스 버스 네임 스페이스를 사용 하는 hello 공유 액세스 키 |
| 이벤트 직렬화 형식 |출력 데이터에 대한 직렬화 형식입니다.  JSON, CSV 및 Avro를 지원합니다. |
| 인코딩 |CSV 및 JSON에 대 한 u t F-8은 hello만 현재 지원 인코딩 형식 |
| 구분 기호 |CSV 직렬화에만 적용됩니다. 스트림 분석은 CSV 형식에서 데이터를 직렬화하기 위해 다양하고 일반적인 구분 기호를 지원합니다. 지원되는 값은 쉼표, 세미콜론, 공백, 탭 및 세로 막대입니다. |
| 형식 |JSON 형식에만 적용됩니다. 줄 바꿈을 하 여 지정 hello 출력 각 JSON 개체를 새 줄으로 구분 하 여 형식이 지정 됩니다. 배열 지정 hello 출력 JSON 개체의 배열으로 형식이 지정 됩니다. |

## <a name="service-bus-topics"></a>Service Bus 토픽
서비스 버스 큐는 보낸 사람 tooreceiver에서 하나의 tooone 통신 메서드를 제공 하는 동안 [서비스 버스 항목](https://msdn.microsoft.com/library/azure/hh367516.aspx) 대 다 형식의 통신을 제공 합니다.

hello 아래 표에 hello 속성 이름 및 테이블 출력을 생성 하는 것에 대 한 설명입니다.

| 속성 이름 | 설명 |
| --- | --- |
| 출력 별칭 |쿼리 toodirect hello 쿼리 출력 toothis 서비스 버스 항목에에서 사용 되는 친숙 한 이름입니다. |
| 서비스 버스 네임스페이스 |서비스 버스 네임스페이스는 메시징 엔터티 집합에 대한 컨테이너입니다. 새 이벤트 허브를 만들 때 서비스 버스 네임스페이스도 만들었습니다. |
| 토픽 이름 |항목은 메시징 엔터티, 비슷한 tooevent 허브 및 큐입니다. 다양 한 다양 한 장치와 서비스에서에서 이벤트 스트림을 디자인 된 toocollect 일입니다. 토픽을 만들 때 특정 이름도 지정됩니다. 구독을 만든 경우가 아니면 tooa 항목 표시 되지 것입니다 hello 메시지가 전송를 구분 하므로 hello 항목 아래에서 하나 이상의 구독이 |
| 토픽 정책 이름 |항목을 만들 때에 hello 항목 구성 탭에서 공유 액세스 정책을 만들 수 있습니다. 각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다. |
| 토픽 정책 키 |tooauthenticate 액세스 toohello 서비스 버스 네임 스페이스를 사용 하는 hello 공유 액세스 키 |
| 이벤트 직렬화 형식 |출력 데이터에 대한 직렬화 형식입니다.  JSON, CSV 및 Avro를 지원합니다. |
| 인코딩 |CSV 또는 JSON 형식인 경우 인코딩을 지정해야 합니다. U t F-8은 hello만 현재 지원 인코딩 형식 |
| 구분 기호 |CSV 직렬화에만 적용됩니다. 스트림 분석은 CSV 형식에서 데이터를 직렬화하기 위해 다양하고 일반적인 구분 기호를 지원합니다. 지원되는 값은 쉼표, 세미콜론, 공백, 탭 및 세로 막대입니다. |

## <a name="azure-cosmos-db"></a>Azure Cosmos DB
[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/)는 완벽하게 관리되는 NoSQL 문서 데이터베이스 서비스로, 스키마 없는 데이터에 대한 쿼리 및 트랜잭션, 예측 가능하고 신뢰할 수 있는 성능 및 신속한 개발을 제공합니다.

목록 세부 정보 hello 속성 이름 및 Azure Cosmos DB 출력을 만들기 위한 그 설명을 아래 번호입니다.

* **출력 별칭** – ASA 쿼리에서이 출력 하는 별칭 toorefer  
* **계정 이름** – hello 이름 또는 끝점 URI hello Cosmos DB 계정입니다.  
* **계정 키** – hello Cosmos DB 계정에 대 한 hello 공유 액세스 키입니다.  
* **데이터베이스** – hello Cosmos DB 데이터베이스 이름입니다.  
* **컬렉션 이름 패턴** – hello 컬렉션 이름 또는 hello 컬렉션 toobe 사용에 대 한 해당 패턴입니다. hello 컬렉션 이름 형식은 파티션은 0부터 시작 하는 여기서 hello 선택적 {partition} 토큰을 사용 하 여 생성할 수 있습니다. 다음은 유효한 입력 샘플입니다.  
  1\) MyCollection – "MyCollection"이라는 이름의 컬렉션이 있어야 합니다.  
  2\) MyCollection{partition} – "MyCollection0”, “MyCollection1”, “MyCollection2” 등의 컬렉션이 있어야 합니다.  
* **파티션 키** – 선택 사항. 컬렉션 이름 패턴에 {parition} 토큰을 사용하는 경우에만 필요합니다. 출력 컬렉션 간에 분할에 대 한 출력 toospecify hello 키를 사용 하는 이벤트에 대 한 hello 필드의 hello 이름입니다. 단일 컬렉션 출력의 경우 임의의 출력 열(예: PartitionId)이 사용될 수 있습니다.  
* **문서 ID** – 선택 사항입니다. 출력 이벤트의 hello 필드의 hello 이름을 사용 하는 삽입 또는 업데이트 작업은 기반으로 toospecify hello 기본 키입니다.  


## <a name="get-help"></a>도움말 보기
추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>다음 단계
도입 된 tooStream hello 사물 인터넷에서에서 데이터에 대해 분석을 스트리밍에 대 한 관리 되는 서비스를 분석 한 후 합니다. 이 서비스에 대해 자세히 toolearn 참조:

* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
