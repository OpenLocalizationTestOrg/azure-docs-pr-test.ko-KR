---
title: "Azure 데이터 레이크 aaaU SQL 프로그래밍 기능 가이드 | Microsoft Docs"
description: "클라우드 기반 빅 데이터 플랫폼을 toocreate 수 있도록 하는 서비스에서 Azure 데이터 레이크 hello 집합에 알아봅니다."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
ms.assetid: 63be271e-7c44-4d19-9897-c2913ee9599d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: saveenr
ms.openlocfilehash: cc8f126234c6106a0dc633ce85a1d9ab1e634e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-programmability-guide"></a>U-SQL 프로그래밍 기능 가이드

U-SQL은 빅 데이터 유형의 워크로드를 위해 설계된 쿼리 언어입니다. Hello U-SQL의 고유한 기능 중 하나에 hello 확장성 및 C#에서 제공 되는 프로그래밍 기능 hello SQL과 유사한 선언적 언어의 hello 조합입니다. 이 가이드에서는 hello 확장성 및 C#에서 사용할 수 있는 hello U SQL 언어의 프로그래밍 기능에 집중 합니다.

## <a name="requirements"></a>요구 사항

[Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)를 다운로드하고 설치합니다.

## <a name="get-started-with-u-sql"></a>U-SQL 시작  

U-SQL 스크립트를 다음 hello를 살펴보겠습니다.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso",   1500.0, "2017-03-39"),
            ("Woodgrove", 2700.0, "2017-04-10")
        ) AS 
              D( customer, amount );
@results =
    SELECT
        customer,
    amount,
    date
    FROM @a;    
```

@a라는 RowSet를 정의하고 @a를 통해 @results라는 RowSet를 만듭니다.

## <a name="c-types-and-expressions-in-u-sql-script"></a>U-SQL 스크립트의 C# 형식 및 식

U-SQL 식은 `AND`, `OR` 및 `NOT`과 같은 U-SQL 논리 연산자와 결합된 C# 식입니다. U-SQL 식은 SELECT, EXTRACT, WHERE, HAVING, GROUP BY 및 DECLARE와 함께 사용할 수 있습니다.

예를 들어 다음 스크립트는 hello 문자열을 구문 분석 hello SELECT 절에는 DateTime 값입니다.

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

hello 다음 스크립트 문자열 구문 분석 하는 DECLARE 문에서 DateTime 값입니다.

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a>데이터 형식 변환에 C# 식 사용
다음 예제는 hello C# 식을 사용 하 여 datetime 데이터 변환을 수행할 수는 방법을 보여 줍니다. 이 특정 시나리오에서 문자열 날짜/시간 데이터는 자정 00시: 00 시간 표기법으로 변환 된 toostandard datetime입니다.

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a>오늘 날짜에 C# 식 사용
toopull 오늘 날짜를 사용할 수 다음 C# 식은 hello:

```
DateTime.Now.ToString("M/d/yyyy")
```

방법의 예로 toouse 스크립트에서이 식은:

```
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```



## <a name="using-net-assemblies"></a>.NET 어셈블리 사용
U-SQL의 확장성 모델은 사용자 지정 코드를 tooadd hello 기능에 크게 의존 합니다. 현재 U-SQL 사용 하면 간단한 방법으로 tooadd 자신의 Microsoft 있습니다. .NET 기반 코드 (특히, C#)입니다. 하지만 다른 .NET 언어(예: VB.NET 또는 F#)로 작성된 사용자 지정 코드를 추가할 수도 있습니다. 

### <a name="register-a-net-assembly"></a>.NET 어셈블리 등록

Hello CREATE ASSEMBLY 문을 tooplace U SQL 데이터베이스에.NET 어셈블리를 사용 합니다. 데이터베이스에 어셈블리를 U-SQL 스크립트 hello 참조 어셈블리 문을 사용 하 여 해당 어셈블리를 사용할 수 있습니다. 

코드에서 보여 주는 방법을 다음 hello tooregister 어셈블리:

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

코드에서 보여 주는 방법을 다음 hello tooreference 어셈블리:

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

Hello 참조 [어셈블리 등록 명령을](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) 이 항목에서 자세히 다루는 합니다.


### <a name="use-assembly-versioning"></a>어셈블리 버전 관리 사용
현재, U-SQL hello.NET Framework 버전 4.5를 사용합니다. 따라서 사용자 고유의 어셈블리와 해당 버전의 hello 런타임이 호환 되는지 확인 합니다.

앞에서 언급했듯이 U-SQL은 64비트(x64) 형식 코드를 실행합니다. 않으므로 코드 x64 컴파일된 toorun 있는지 확인 합니다. 그렇지 않으면 오류가 hello 잘못 된 형식 앞에 표시 된 합니다.

업로드된 각 어셈블리 DLL, 리소스 파일(예: 다양한 런타임), 네이티브 어셈블리 또는 구성 파일의 크기는 최대 400MB입니다. hello 리소스 배포를 통해 또는 참조 tooassemblies 및 추가 파일을 통해 배포 된 리소스의 전체 크기는 3GB를 초과할 수 없습니다.

마지막으로 U-SQL 데이터베이스마다 지정된 어셈블리 버전을 하나만 포함할 수 있습니다. 예를 들어 버전 7 및 8 버전의 hello NewtonSoft Json.Net 라이브러리 모두, 필요한 경우 필요한 tooregister 서로 다른 두 데이터베이스에서 해당 합니다. 또한 각 스크립트 tooone 버전 지정된 된 어셈블리 DLL 참조할 수 있습니다. 이런 점에서 U-SQL hello C# 어셈블리 관리 및 버전 관리를 의미 체계를 따릅니다.


## <a name="use-user-defined-functions-udf"></a>UDF(사용자 정의 함수) 사용
U-SQL 사용자 정의 함수 또는 UDF는 매개 변수를 받아들이고 (예: 복잡 한 계산의 경우) 작업을 수행 하는 값으로 해당 작업의 hello 결과 반환 하는 루틴을 프로그래밍 하 합니다. hello 반환 UDF의 값에는 단일 스칼라만 될 수 있습니다. U-SQL UDF는 다른 C# 스칼라 함수와 같이 U-SQL 기본 스크립트에서 호출할 수 있습니다.

U-SQL 사용자 정의 함수는 **public** 및 **static**으로 초기화하는 것이 좋습니다.

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

첫 번째 hello 간단한 UDF를 만드는 예를 살펴보겠습니다.

이 사용 사례 시나리오에서는 toodetermine hello 회계 기간을 hello 회계 분기 등 hello 첫 번째 로그인 hello 특정 사용자에 대 한 회계 월 필요 합니다. hello는 시나리오에서 hello 연도의 첫 번째 회계 월이 6 월.

toocalculate 회계 기간 hello 다음 C# 함수를 소개 합니다.

```
public static string GetFiscalPeriod(DateTime dt)
{
    int FiscalMonth=0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter=0;
    if (FiscalMonth >=1 && FiscalMonth<=3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return "Q" + FiscalQuarter.ToString() + ":P" + FiscalMonth.ToString();
}
```

단순히 회계 월과 분기를 계산하고 문자열 값을 반환합니다. 첫 번째 회계 분기 hello의 첫 번째 월 hello 년 6 월에 대 한 "Q1:P1" 사용합니다. 7월에 대해서는 "Q1:P2"를 사용하고 이런 방식으로 계속 적용합니다.

이것은 일반 C# 기능 U-SQL 프로젝트에 진행 중인 toouse는 했습니다.

이 시나리오에서 코드 숨김 섹션 hello 모양을 다음과 같습니다.

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":" + FiscalMonth.ToString();
        }

    }

}
```

이제 하겠습니다 toocall이이 함수 hello 기본 U-SQL 스크립트에서. toodo이 tooprovide를 비롯 하 여 hello 네임 스페이스는이 예에서 NameSpace.Class.Function(parameter) hello 함수에 대 한 정규화 된 이름을 사용할 것입니다.

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

다음은 hello 실제 U-SQL 기본 스크립트입니다.

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt DateTime,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
    MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

다음은 hello 스크립트 실행의 hello 출력 파일입니다.

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

이 예제에서는 U-SQL에서 인라인 UDF를 간단하게 사용하는 방법을 보여 줍니다.

### <a name="keep-state-between-udf-invocations"></a>UDF 호출 사이 상태 유지
U-SQL C# 프로그래밍 기능 개체 수 수 더 복잡 한, hello 코드 숨김 전역 변수를 통해 대화형 기능을 활용 합니다. 비즈니스 사용 사례 시나리오를 따르는 hello를 살펴 보겠습니다.

대규모 조직에서는 사용자가 다양한 내부 응용 프로그램 간에 전환할 수 있습니다. 여기에는 Microsoft Dynamics CRM, PowerBI 등이 포함될 수 있습니다. 고객 tooapply 사용자가 어떤 hello 사용 추세 및에 서로 다른 응용 프로그램 전환 하는 방법에 대 한 원격 분석 분석을 할 수 있습니다. hello hello 비즈니스용 ´ ֲ toooptimize 응용 프로그램 사용. 또한 toocombine 서로 다른 응용 프로그램 또는 특정 로그온 루틴 합니다 수 있습니다.

tooachieve toodetermine 세션 Id 및 hello에 발생 한 마지막 세션 사이 지연 기간 있는이 목표입니다.

그런 다음 할당할 toohello 생성된 되는이 로그인 tooall 세션 및 이전 로그인 toofind 필요 동일한 응용 프로그램입니다. hello 첫 번째 인증은 기본 U-SQL 스크립트 하지 않는 허용 우리 tooapply 계산 LAG 함수를 이미 계산 열에 대해 합니다. hello 두 번째 문제는 hello tookeep hello 내에서 모든 세션에 대 한 특정 세션 있다는 것 같은 기간입니다.

toosolve이이 문제는 코드 숨김 섹션 내 전역 변수를 사용 하 여 했습니다: `static public string globalSession;`합니다.

전역 변수가이 우리의 스크립트를 실행 하는 동안 적용 된 toohello 전체 행 집합입니다.

다음은 U-SQL 프로그램의 hello 코드 숨김 섹션이입니다.

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQLApplication21
{
    public class UserSession
    {
        static public string globalSession;
        static public string StampUserSession(string eventTime, string PreviousRow, string Session)
        {

            if (!string.IsNullOrEmpty(PreviousRow))
            {
                double timeGap = Convert.ToDateTime(eventTime).Subtract(Convert.ToDateTime(PreviousRow)).TotalMinutes;
                if (timeGap <= 60) {return Session;}
                else {return Guid.NewGuid().ToString();}
            }
            else {return Guid.NewGuid().ToString();}

        }

        static public string getStampUserSession(string Session)
        {
            if (Session != globalSession && !string.IsNullOrEmpty(Session)) { globalSession = Session; }
            return globalSession;
        }

    }
}
```

이 예제에서는 전역 변수 hello `static public string globalSession;` hello 내에서 사용할 `getStampUserSession` 함수 및 가져오기 각 시간 hello 매개 변수가 변경 된 세션을 다시 초기화 합니다.

hello U-SQL 기본 스크립트는 다음과 같습니다.

```
DECLARE @in string = @"\UserSession\test1.tsv";
DECLARE @out1 string = @"\UserSession\Out1.csv";
DECLARE @out2 string = @"\UserSession\Out2.csv";
DECLARE @out3 string = @"\UserSession\Out3.csv";

@records =
    EXTRACT DataId string,
            EventDateTime string,           
            UserName string,
            UserSessionTimestamp string

    FROM @in
    USING Extractors.Tsv();

@rs1 =
    SELECT 
        EventDateTime,
        UserName,
    LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,          
        string.IsNullOrEmpty(LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,           
        USQLApplication21.UserSession.StampUserSession
           (
            EventDateTime,
            LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC),
            LAG(UserSessionTimestamp, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)
           ) AS UserSessionTimestamp
    FROM @records;

@rs2 =
    SELECT 
        EventDateTime,
        UserName,
        LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,
        string.IsNullOrEmpty( LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,
        USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp) AS UserSessionTimestamp
    FROM @rs1
    WHERE UserName != "UserName";

OUTPUT @rs2
    too@out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

함수 `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` 여기 hello 두 번째 메모리 행 집합 계산 하는 동안 호출 됩니다. Hello 전달 `UserSessionTimestamp` 열 및 반환 값까지 hello `UserSessionTimestamp` 변경 되었습니다.

hello 출력 파일은 다음과 같습니다.

```
"2016-02-19T07:32:36.8420000-08:00","User1",,True,"72a0660e-22df-428e-b672-e0977007177f"
"2016-02-17T11:52:43.6350000-08:00","User2",,True,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-17T11:59:08.8320000-08:00","User2","2016-02-17T11:52:43.6350000-08:00",False,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-11T07:04:17.2630000-08:00","User3",,True,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-11T07:10:33.9720000-08:00","User3","2016-02-11T07:04:17.2630000-08:00",False,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-15T21:27:41.8210000-08:00","User3","2016-02-11T07:10:33.9720000-08:00",False,"4d2bc48d-bdf3-4591-a9c1-7b15ceb8e074"
"2016-02-16T05:48:49.6360000-08:00","User3","2016-02-15T21:27:41.8210000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-16T06:22:43.6390000-08:00","User3","2016-02-16T05:48:49.6360000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-17T16:29:53.2280000-08:00","User3","2016-02-16T06:22:43.6390000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T16:39:07.2430000-08:00","User3","2016-02-17T16:29:53.2280000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T17:20:39.3220000-08:00","User3","2016-02-17T16:39:07.2430000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-19T05:23:54.5710000-08:00","User3","2016-02-17T17:20:39.3220000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T05:48:37.7510000-08:00","User3","2016-02-19T05:23:54.5710000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T06:40:27.4830000-08:00","User3","2016-02-19T05:48:37.7510000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T07:27:37.7550000-08:00","User3","2016-02-19T06:40:27.4830000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T19:35:40.9450000-08:00","User3","2016-02-19T07:27:37.7550000-08:00",False,"3f385f0b-3e68-4456-ac74-ff6cef093674"
"2016-02-20T00:07:37.8250000-08:00","User3","2016-02-19T19:35:40.9450000-08:00",False,"685f76d5-ca48-4c58-b77d-bd3a9ddb33da"
"2016-02-11T09:01:33.9720000-08:00","User4",,True,"9f0cf696-c8ba-449a-8d5f-1ca6ed8f2ee8"
"2016-02-17T06:30:38.6210000-08:00","User4","2016-02-11T09:01:33.9720000-08:00",False,"8b11fd2a-01bf-4a5e-a9af-3c92c4e4382a"
"2016-02-17T22:15:26.4020000-08:00","User4","2016-02-17T06:30:38.6210000-08:00",False,"4e1cb707-3b5f-49c1-90c7-9b33b86ca1f4"
"2016-02-18T14:37:27.6560000-08:00","User4","2016-02-17T22:15:26.4020000-08:00",False,"f4e44400-e837-40ed-8dfd-2ea264d4e338"
"2016-02-19T01:20:31.4800000-08:00","User4","2016-02-18T14:37:27.6560000-08:00",False,"2136f4cf-7c7d-43c1-8ae2-08f4ad6a6e08"
```

이 예제에서는 적용된 toohello 전체 메모리 행 집합은 하는 코드 숨김 섹션 내 전역 변수를 사용 하는 보다 복잡 한 사용 사례 시나리오를 보여 줍니다.

## <a name="use-user-defined-types-udt"></a>UDT(사용자 정의 형식) 사용
UDT(사용자 정의 형식)는 U-SQL의 또 다른 프로그래밍 기능입니다. U-SQL UDT는 일반 C# 사용자 정의 형식처럼 작동합니다. C#은 기본 및 사용자 지정 사용자 정의 형식 hello 사용을 허용 하는 강력한 형식의 언어입니다.

U-SQL 암시적으로 직렬화 하거나 행 집합에서 꼭지점을 잇는 hello UDT 전달 될 때 임의의 Udt를 역직렬화 할 수 없습니다. 이 hello이 사용자는 tooprovide 명시적 포맷터 hello IFormatter 인터페이스를 사용 하 여 의미 합니다. U-SQL hello로 이로써 serialize hello UDT에 대 한 메서드 및 합니다.

> [!NOTE]
> U-SQL의 기본 제공 추출기 outputters 현재 serialize 하거나 없습니다 hello IFormatter 설정 된 경우에 파일에서 UDT 데이터 tooor을 역직렬화 합니다. 따라서 출력 문 hello로 UDT 데이터 tooa 파일을 작성할 아니면 toopass가 추출기와 함께 읽을 때로 문자열 또는 바이트 배열입니다. 그런 다음 hello serialization을 호출 하 고 코드 (즉, hello UDT의 tostring (메서드)를) 명시적으로 역직렬화 합니다. 사용자 정의 추출기 및 다른 hello에 outputters 전달, 읽고 쓸 수 Udt입니다.

다음과 같이 toouse EXTRACTOR 또는 이전 SELECT), (부족 OUTPUTTER에서 UDT를 시도 했습니다.

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

Hello 다음 오류가 수신 했습니다.

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used toooutput column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how tooserialize this type, or call a serialization method on hello type in
hello preceding SELECT. C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

UDT와 toowork outputter, 하거나 했으므로 tooserialize 것와 toostring hello tostring () 메서드 또는 사용자 지정 outputter 만듭니다.

UDT는 현재 GROUP BY에서 사용할 수 없습니다. GROUP BY에 UDT 사용 하면 다음 오류가 hello throw 됩니다.

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want toouse with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

UDT toodefine을 해야 합니다.

* Hello 다음 네임 스페이스를 추가 합니다.

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* 추가 `Microsoft.Analytics.Interfaces`, hello UDT 인터페이스에 대 한 필요 합니다. 또한 `System.IO` 필요한 toodefine hello IFormatter 인터페이스 일 수 있습니다.

* SqlUserDefinedType 특성을 사용하여 사용자 정의 형식을 정의합니다.

**SqlUserDefinedType** U-SQL toomark 사용 되는 사용자 정의 형식 (UDT)으로 어셈블리의 형식 정의입니다. hello 특성에 hello 속성 hello hello UDT의 물리적 특성을 반영합니다. 이 클래스는 상속될 수 없습니다.

SqlUserDefinedType은 UDT 정의에 필요한 특성입니다.

hello 클래스의 생성자를 hello:  

* SqlUserDefinedTypeAttribute(형식 포맷터)

* 유형 포맷터: 필수 매개 변수 toodefine UDT 포맷터-특히 hello 유형의 hello `IFormatter` 인터페이스는 여기에 전달 해야 합니다.

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* 일반적인 UDT hello 다음 예제와 같이 hello IFormatter 인터페이스의 정의 필요 합니다.

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

hello `IFormatter` 인터페이스를 직렬화 및 역직렬화 하는 개체 그래프의 루트 형식 hello와 \<typeparamref 이름 = "T" >.

\<typeparam 이름 = "T" > hello 개체 그래프 tooserialize에 대해 루트 형식 hello 및 역직렬화 합니다.

* **Deserialize**: 제공 된 hello 스트림에서 hello 데이터를 역직렬화 하 고 개체의 그래프를 hello를 다시 구성 합니다.

* **직렬화**: 루트 제공 toohello 스트림을 제공 하는 hello로 개체 또는 개체 그래프를 Serialize 합니다.

`MyType`인스턴스: hello 형식의 인스턴스입니다.  
`IColumnWriter`기록기 / `IColumnReader` 판독기: hello 열 스트림 원본으로 사용 합니다.  
`ISerializationContext`상황에 맞는: 직렬화 하는 동안 hello 스트림에 대 한 hello 소스 또는 대상 컨텍스트를 지정 하는 플래그 집합을 정의 하는 열거형입니다.

* **중간**: hello 소스 또는 대상 컨텍스트를 해당 지속형된 저장소 아님을 지정 합니다.

* **지 속성**: hello 소스 또는 대상 컨텍스트를 해당 지속형된 저장소 인지 지정 합니다.

일반 C# 형식으로 U-SQL UDT 정의는 +/==/!= 등의 연산자에 대한 재정의를 포함할 수 있습니다. 정적 메서드도 포함할 수 있습니다. 예를 들어 하겠습니다 toouse이이 UDT로 매개 변수 tooa U SQL MIN 집계 함수, 있는지 toodefine < 연산자 재정의 합니다.

이 가이드의 hello 형식 (Q1:P10) Qn:Pn hello 특정 날짜부터 회계 기간 id에 대 한 예에 설명 된 것입니다. 다음 예제는 hello toodefine 사용자 지정 입력 하는 방법을 회계 기간 값을 보여 줍니다.

다음은 사용자 지정 UDT 및 IFormatter 인터페이스가 포함된 코드 숨김 섹션의 예제입니다.

```
[SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
public struct FiscalPeriod
{
    public int Quarter { get; private set; }

    public int Month { get; private set; }

    public FiscalPeriod(int quarter, int month):this()
    {
    this.Quarter = quarter;
    this.Month = month;
    }

    public override bool Equals(object obj)
    {
    if (ReferenceEquals(null, obj))
    {
        return false;
    }

    return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
    }

    public bool Equals(FiscalPeriod other)
    {
return this.Quarter.Equals(other.Quarter) && this.Month.Equals(other.Month);
    }

    public bool GreaterThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
    }

    public bool LessThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
    }

    public override int GetHashCode()
    {
    unchecked
    {
        return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
    }
    }

    public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
    {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
    }

    public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.Equals(c2);
    }

    public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
    {
    return !c1.Equals(c2);
    }
    public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.GreaterThan(c2);
    }
    public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.LessThan(c2);
    }
    public override string ToString()
    {
    return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
    }

}

public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
{
    public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
    {
    using (var binaryWriter = new BinaryWriter(writer.BaseStream))
    {
        binaryWriter.Write(instance.Quarter);
        binaryWriter.Write(instance.Month);
        binaryWriter.Flush();
    }
    }

    public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
    {
    using (var binaryReader = new BinaryReader(reader.BaseStream))
    {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
        return result;
    }
    }
}
```

hello 정의 된 형식이 포함 되어 두 개의 숫자: 분기 및 월. 여기서 ==/!=/>/< 연산자 및 ToString() 정적 메서드가 정의됩니다.

앞에서 설명한 대로 UDT는 SELECT 식에서 사용할 수 있지만, 사용자 지정 직렬화 없이는 OUTPUTTER/EXTRACTOR에서 사용할 수 없습니다. Tostring () 문자열로 serialize 된 하거나 사용자 지정 OUTPUTTER/EXTRACTOR를 사용해 서 toobe 포함 되어 있습니다.

이제 UDT 사용법에 대해 살펴보겠습니다. 코드 숨김 섹션에서 다음 우리의 GetFiscalPeriod function toohello 변경 했습니다.

```
public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
{
    int FiscalMonth = 0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter = 0;
    if (FiscalMonth >= 1 && FiscalMonth <= 3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return new FiscalPeriod(FiscalQuarter, FiscalMonth);
}
```

볼 수 있듯이 우리 FiscalPeriod 형식의 hello 값을 반환 합니다.

여기 어떻게 toouse 것에서 자세히 U-SQL 기본 스크립트의 예를 제공 합니다. 이 예제에서는 U-SQL 스크립트에서 UDT를 호출하는 다른 형식을 보여줍니다.

```
DECLARE @input_file string = @"c:\work\cosmos\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"c:\work\cosmos\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT 
        guid AS start_id,
        dt,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Quarter AS fiscalquarter,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Month AS fiscalmonth,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt) + new USQL_Programmability.CustomFunctions.FiscalPeriod(1,7) AS fiscalperiod_adjusted,
        user,
        des
    FROM @rs0;

@rs2 =
    SELECT 
           start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           fiscalquarter,
           fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS fiscalperiod,

       // This user-defined type was created in hello prior SELECT.  Passing hello UDT toothis subsequent SELECT would have failed if hello UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```

다음은 전체 코드 숨김 섹션의 예제입니다.

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }

        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }



        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) &&    this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }
    }
}
```

## <a name="use-user-defined-aggregates-udagg"></a>UDAGG(사용자 정의 집계) 사용
UDAGG(사용자 정의 집계)는 U-SQL에 제공되지 않는 집계 관련 함수입니다. hello 예제 수 사용자 지정 수학 계산, 문자열 연결 문자열을 사용한 조작을 집계 tooperform 수 등에입니다.

hello 사용자 정의 집계 기본 클래스 정의 다음과 같습니다.

```c#
    [SqlUserDefinedAggregate]
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
    {
        protected IAggregate();

        public abstract void Accumulate(T1 t1, T2 t2);
        public abstract void Init();
        public abstract TResult Terminate();
    }
```

**SqlUserDefinedAggregate** hello 형식을 사용자 정의 집계로 등록 해야 함을 나타냅니다. 이 클래스는 상속될 수 없습니다.

SqlUserDefinedType 특성은 UDAGG 정의의 **선택 사항**입니다.


hello 기본 클래스를 사용 하 toopass 3 추상 매개 변수: 두 개의 입력된 매개 변수도 hello 결과로 하나입니다. hello 데이터 형식 변수는 클래스를 상속 하는 동안 정의 해야 합니다.

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    { … }

    public override void Accumulate(string guid, string user)
    { … }

    public override string Terminate()
    { … }
}
```

* **Init**는 계산하는 동안 각 그룹에 대해 한 번씩 호출됩니다. 각 집계 그룹에 대한 초기화 루틴을 제공합니다.  
* **Accumulate**는 각 값에 대해 한 번씩 실행됩니다. Hello 집계 알고리즘에 대 한 hello 주요 기능을 제공 합니다. 클래스를 상속 하는 동안 정의 된 다양 한 데이터 형식에 사용 되는 tooaggregate 값 수 있습니다. 변수 데이터 형식의 매개 변수 두 개를 사용할 수 있습니다.
* **종료** hello 끝 각 그룹에 대 한 toooutput hello 결과 처리에 대 한 집계 그룹당 한 번씩 실행 됩니다.

toodeclare 올바른 입력 및 출력 데이터 형식을 다음과 같이 hello 클래스 정의 사용 합니다.

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* 첫 번째 매개 변수 tooaccumulate T1:
* 첫 번째 매개 변수 tooaccumulate T2:
* TResult: Terminate의 반환 형식

예:

```
public class GuidAggregate : IAggregate<string, int, int>
```

또는

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a>U-SQL에서 UDAGG 사용
toouse UDAGG, 먼저 코드 숨김에 정의 하거나 이전에 설명한 대로 hello 존재 프로그래밍 기능 DLL에서에서 참조 합니다.

다음 구문 다음 hello를 사용 하 여:

```
AGG<UDAGG_functionname>(param1,param2)
```

UDAGG의 예제는 다음과 같습니다.

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    {
        guid_agg = "";
    }

    public override void Accumulate(string guid, string user)
    {
        if (user.ToUpper()== "USER1")
        {
        guid_agg += "{" + guid + "}";
        }
    }

    public override string Terminate()
    {
        return guid_agg;
    }

}
```

기본 U-SQL 스크립트:

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @" \usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    SELECT
        user,
        AGG<USQL_Programmability.GuidAggregate>(guid,user) AS guid_list
    FROM @rs0
    GROUP BY user;

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

이 사용 사례 시나리오에서는 hello 특정 사용자에 대 한 Guid 클래스를 연결 합니다.

## <a name="use-user-defined-objects-udo"></a>UDO(사용자 정의 개체) 사용
U-SQL 위의 UDO 또는 사용자 정의 개체 라고 하는 사용자 지정 프로그래밍 기능 개체를 toodefine 있습니다.

hello 다음은 U-SQL에는 UDO의 목록입니다.

* 사용자 정의 추출기
    * 행 단위 추출
    * 사용자 지정 구조화 된 파일에서 데이터 추출을 tooimplement 사용

* 사용자 정의 출력자
    * 행 단위 출력
    * Toooutput 사용자 지정 데이터 형식이 나 사용자 지정 파일 형식 사용

* 사용자 정의 처리기
    * 한 행씩 가져와 한 행씩 생성
    * 사용 되는 tooreduce hello 열의 수 또는 새 열을 기존 열 집합에서 파생 된 값으로 생성

* 사용자 정의 적용자
    * 한 행을 사용 toon 행이 0을 생성 하는
    * OUTER/CROSS APPLY 사용

* 사용자 정의 결합자
    * 행 집합 결합--사용자 정의 JOIN

* 사용자 정의 리듀서
    * n개 행을 가져와 한 행씩 생성
    * Tooreduce hello 행 수를 사용합니다.

UDO는 일반적으로 다음 U-SQL 조건 hello의 일부로 U-SQL 스크립트에 명시적으로 호출 됩니다.

* EXTRACT
* OUTPUT
* PROCESS
* COMBINE
* REDUCE

> [!NOTE]  
> UDO의 제한 된 tooconsume 0.5 g b 메모리를 됩니다.  이 메모리 제한을 toolocal 실행 될 때 적용 되지 않습니다.

## <a name="use-user-defined-extractors"></a>UDE(사용자 정의 추출기) 사용
U-SQL 추출 문을 사용 하 여 tooimport 외부 데이터를 허용 합니다. EXTRACT 문은 기본 제공 UDO 추출기를 사용할 수 있습니다.  

* *Extractors.Text()*: 다른 인코딩의 구분 기호로 분리된 텍스트 파일에서 데이터를 추출합니다.

* *Extractors.Csv()*: 다른 인코딩의 쉼표로 구분된 값(CSV) 파일에서 데이터를 추출합니다.

* *Extractors.Tsv()*: 다른 인코딩의 탭으로 구분된 값(TSV) 파일에서 데이터를 추출합니다.

유용한 toodevelop 사용자 지정 추출기 수 있습니다. 이 유용 데이터를 가져오는 동안 할까요 toodo hello 다음 작업 중 하나:

* 열을 분할하고 개별 값을 수정하여 입력 데이터를 수정합니다. hello 프로세서 기능 열을 결합 하는 데 좋습니다.
* 구조화되지 않은 데이터(예: 웹 페이지 및 전자 메일) 또는 반 구조화되지 않은 데이터(예: XML/JSON)를 구문 분석합니다.
* 지원되지 않는 인코딩 데이터를 구문 분석합니다.

사용자 정의 extractor toodefine toocreate 필요 UDE, 또는 `IExtractor` 인터페이스입니다. 열/행 구분 기호 및 인코딩, 필요한 toobe hello 클래스의 hello 생성자에 정의 된 같은 기준으로 모든 입력 매개 변수 toohello extractor 합니다. hello `IExtractor` 인터페이스 hello에 대 한 정의 있어야 `IEnumerable<IRow>` 다음과 같이 재정의:

```
[SqlUserDefinedExtractor]
public class SampleExtractor : IExtractor
{
     public SampleExtractor(string row_delimiter, char col_delimiter)
     { … }

     public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
     { … }
}
```

hello **SqlUserDefinedExtractor** 특성으로 사용자 정의 extractor hello 형식을 등록 해야 함을 나타냅니다. 이 클래스는 상속될 수 없습니다.

SqlUserDefinedExtractor는 UDE 정의의 선택적 특성이며, Hello UDE 개체에 대 한 toodefine AtomicFileProcessing 속성을 사용 하는 것입니다.

* bool AtomicFileProcessing   

* **true**는 추출기에 원자성 입력 파일(JSON, XML 등)이 필요함을 나타냅니다.
* **false**는 추출기에서 분할/분산 파일(CSV, SEQ 등)을 처리할 수 있음을 나타냅니다.

hello 주요 UDE 프로그래밍 기능 개체는 **입력** 및 **출력**합니다. hello 입력된 개체는으로 입력된 데이터를 사용 하는 tooenumerate `IUnstructuredReader`합니다. hello 출력 개체에는 hello extractor 활동의 결과로 사용 되는 tooset 출력 데이터입니다.

hello 입력된 데이터를 통해 액세스 `System.IO.Stream` 및 `System.IO.StreamReader`합니다.

입력된 열 열거형에 대 한 म 먼저 hello 입력된 스트림을 사용 하 여 분할 행 구분 기호입니다.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

그런 다음 입력 행을 열 파트로 세분합니다.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

tooset 출력 데이터를 사용 하 여 hello `output.Set` 메서드.

사용자 지정 extractor hello toounderstand만 출력의 열과 값 정의 된 hello 출력 유용 합니다. 메서드 호출을 설정합니다.

```
output.Set<string>(count, part);
```

호출 하 여 hello 실제 extractor 출력 트리거될 `yield return output.AsReadOnly();`합니다.

다음은 hello extractor 예.

```
[SqlUserDefinedExtractor(AtomicFileProcessing = true)]
public class FullDescriptionExtractor : IExtractor
{
     private Encoding _encoding;
     private byte[] _row_delim;
     private char _col_delim;

    public FullDescriptionExtractor(Encoding encoding, string row_delim = "\r\n", char col_delim = '\t')
    {
         this._encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
         this._row_delim = this._encoding.GetBytes(row_delim);
         this._col_delim = col_delim;

    }

    public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
    {
         string line;
         //Read hello input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split hello input by hello column delimiter
             string[] parts = line.Split(this._col_delim);
             int count = 0; // start with first column
             foreach (string part in parts)
             {
    if (count == 0)
             {  // for column “guid”, re-generated guid
                 Guid new_guid = Guid.NewGuid();
                 output.Set<Guid>(count, new_guid);
             }
             else if (count == 2)
             {
                 // for column “user”, convert tooUPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep hello rest of hello columns as-is
                 output.Set<string>(count, part);
             }
             count += 1;
             }

         }
         yield return output.AsReadOnly();
         }
         yield break;
     }
}
```

이 사용 사례 시나리오에서 hello extractor "guid" 열에 대 한 hello GUID 다시 생성 하 고 "user" 열 tooupper 사례의 hello 값으로 변환 합니다. 사용자 지정 추출기는 입력 데이터를 구문 분석하고 이를 조작하여 더 복잡한 결과를 생성할 수 있습니다.

다음은 사용자 지정 추출기를 사용하는 기본 U-SQL 스크립트입니다.

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file
        USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a>사용자 정의 출력자 사용
사용자 정의 outputter U-SQL 기능이 기본 제공 tooextend 수 있는 다른 U-SQL UDO입니다. 비슷한 toohello 추출기는 몇 가지 기본 제공 outputters 합니다.

* *Outputters.Text()*: 텍스트 파일의 인코딩이 서로 다른 데이터 toodelimited를 기록 합니다.
* *Outputters.Csv()*: 데이터 toocomma 구분 된 값의 인코딩이 서로 다르고 (CSV) 파일에 기록 합니다.
* *Outputters.Tsv()*: 데이터 tootab 구분 된 값의 인코딩이 서로 다르고 (TSV) 파일에 기록 합니다.

사용자 지정 outputter 정의 된 사용자 지정 형식으로 toowrite 데이터를 허용 합니다. 이 작업을 수행 하는 hello에 대 한 유용할 수 있습니다.

* 데이터 toosemi 구조적 또는 비구조적 파일을 작성 합니다.
* 지원되지 않는 인코딩 데이터 쓰기
* 출력 데이터 수정 또는 사용자 지정 특성 추가

사용자 정의 outputter toodefine toocreate hello 필요 `IOutputter` 인터페이스입니다.

다음은 기본 hello `IOutputter` 클래스 구현:

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

열/행 구분 기호, 인코딩 및 등 필요 toobe hello 클래스의 hello 생성자에 정의 된 같은 기준으로 모든 입력 매개 변수 toohello outputter 합니다. hello `IOutputter` 인터페이스에 대 한 정의 있어야 `void Output` 재정의 합니다. hello 특성 `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` 원자성 파일 처리를 위해 필요에 따라 설정할 수 있습니다. 자세한 내용은 hello 다음 세부 정보를 참조 하세요.

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class MyOutputter : IOutputter
{

    public MyOutputter(myparam1, myparam2)
    {
      …
    }

    public override void Close()
    {
      …
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
      …
    }
}
```

* `Output`은 각 입력 행에 대해 호출됩니다. Hello 반환 `IUnstructuredWriter output` 행 집합입니다.
* hello 생성자 클래스를 사용 하는 사용 되는 toopass 매개 변수 toohello 사용자 정의 outputter 합니다.
* `Close`사용 toooptionally toorelease 비용이 많이 드는 상태를 재정의 하거나 hello 마지막 행이 기록 된 경우를 확인 합니다.

**SqlUserDefinedOutputter** 특성으로 사용자 정의 outputter hello 형식을 등록 해야 함을 나타냅니다. 이 클래스는 상속될 수 없습니다.

SqlUserDefinedOutputter는 사용자 정의 출력자 정의의 선택적 특성이며, Toodefine hello AtomicFileProcessing 속성을 사용 하는 합니다.

* bool AtomicFileProcessing   

* **true**는 출력자에 원자성 출력 파일(JSON, XML 등)이 필요함을 나타냅니다.
* **false**는 출력자에서 분할/분산 파일(CSV, SEQ 등)을 처리할 수 있음을 나타냅니다.

hello 주 프로그래밍 기능 개체는 **행** 및 **출력**합니다. hello **행** 개체는으로 출력 데이터를 사용 하는 tooenumerate `IRow` 인터페이스입니다. **출력** 는 사용 되는 tooset 출력 데이터 toohello 대상 파일이 나와 있습니다.

hello 출력 통해 데이터에 액세스 hello `IRow` 인터페이스입니다. 출력 데이터는 한 번에 한 행씩 전달됩니다.

hello IRow 인터페이스의 hello Get 메서드를 호출 하 여 hello 개별 값 열거 됩니다.

```
row.Get<string>("column_name")
```

개별 열 이름은 `row.Schema`를 호출하여 결정될 수 있습니다.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

이 방법을 사용 하면 모든 메타 데이터 스키마에 대 한 유연한 outputter toobuild 있습니다.

hello 출력 데이터가 쓰여집니다 toofile를 사용 하 여 `System.IO.StreamWriter`합니다. hello 스트림 매개 변수가 너무 설정 된`output.BaseStrea` 의 일부로 `IUnstructuredWriter output`합니다.

각 행 반복 후 중요 한 tooflush hello 데이터 버퍼 toohello 파일 인지 확인 합니다. 또한 hello `StreamWriter` hello 삭제 가능한 특성으로 사용 하도록 설정 (기본값)과 hello로 개체를 사용 해야 **를 사용 하 여** 키워드:

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

그렇지 않으면 매번 반복 후에 Flush() 메서드를 명시적으로 호출합니다. 다음 예제는 hello에이 표시 됩니다.

### <a name="set-headers-and-footers-for-user-defined-outputter"></a>사용자 정의 출력자의 머리글 및 바닥글 설정
tooset 헤더를 단일 반복 실행 흐름을 사용 합니다.

```
public override void Output(IRow row, IUnstructuredWriter output)
{
 …
if (isHeaderRow)
{
    …                
}

 …
if (isHeaderRow)
{
    isHeaderRow = false;
}
 …
}
}
```

hello에 대 한 코드를 먼저 hello `if (isHeaderRow)` 블록이 한 번만 실행 됩니다.

Hello 바닥글의 hello 참조 toohello 인스턴스를 사용 하 여 `System.IO.Stream` 개체 (`output.BaseStream`). Hello 바닥글 hello hello의 close () 메서드를에서 작성 `IOutputter` 인터페이스입니다.  (자세한 내용은 다음 예에서는 hello 참조).

다음의 사용자 정의 출력자에 대한 예제입니다.

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class HTMLOutputter : IOutputter
{
    // Local variables initialization
    private string row_delimiter;
    private char col_delimiter;
    private bool isHeaderRow;
    private Encoding encoding;
    private bool IsTableHeader = true;
    private Stream g_writer;

    // Parameters definition            
    public HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    this.isHeaderRow = isHeader;
    this.encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
    }

    // hello Close method is used toowrite hello footer toohello file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference tooIO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization tooenumerate column names
    ISchema schema = row.Schema;

    // This is a data-independent header--HTML table definition
    if (IsTableHeader)
    {
        streamWriter.Write("<table border=1>");
        IsTableHeader = false;
    }

    // HTML table attributes
    string header_wrapper_on = "<th>";
    string header_wrapper_off = "</th>";
    string data_wrapper_on = "<td>";
    string data_wrapper_off = "</td>";

    // Header row output--runs only once
    if (isHeaderRow)
    {
        streamWriter.Write("<tr>");
        for (int i = 0; i < schema.Count(); i++)
        {
        var col = schema[i];
        streamWriter.Write(header_wrapper_on + col.Name + header_wrapper_off);
        }
        streamWriter.Write("</tr>");
    }

    // Data row output
    streamWriter.Write("<tr>");                
    for (int i = 0; i < schema.Count(); i++)
    {
        var col = schema[i];
        string val = "";
        try
        {
        // Data type enumeration--required toomatch hello distinct list of types from OUTPUT statement
        switch (col.Type.Name.ToString().ToLower())
        {
            case "string": val = row.Get<string>(col.Name).ToString(); break;
            case "guid": val = row.Get<Guid>(col.Name).ToString(); break;
            default: break;
        }
        }
        // Handling NULL values--keeping them empty
        catch (System.NullReferenceException)
        {
        }
        streamWriter.Write(data_wrapper_on + val + data_wrapper_off);
    }
    streamWriter.Write("</tr>");

    if (isHeaderRow)
    {
        isHeaderRow = false;
    }
    // Reference toohello instance of hello IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define hello factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

U-SQL 기본 스크립트:

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.html";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
         FROM @input_file
         USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 
    too@output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

HTML 출력자이며, 테이블 데이터로 HTML 파일을 만듭니다.

### <a name="call-outputter-from-u-sql-base-script"></a>U-SQL 기본 스크립트에서 출력자 호출
hello 기본 U-SQL 스크립트에서 사용자 지정 outputter toocall hello outputter 개체의 새 인스턴스를 hello 만든 toobe에 있습니다.

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

기본 스크립트에 개체 tooavoid hello의 인스턴스를 만들지는 이전 예에서 같이 함수 래퍼를 만들 수 있습니다.

```c#
        // Define hello factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

이 경우 원래 호출은 hello hello 다음과 같습니다.

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a>UDP(사용자 정의 처리기) 사용
사용자 정의 프로세서 또는 UDP, 프로그래밍 기능을 적용 하 여 tooprocess hello 들어오는 행을 수 있는 U-SQL UDO의 형식입니다. UDP toocombine 열, 값을 수정 있으며 필요한 경우 새 열을 추가 합니다. 기본적으로, tooprocess 행 집합 tooproduce 필요한 데이터 요소 수 있습니다.

UDP toodefine toocreate 필요는 `IProcessor` hello로 인터페이스 `SqlUserDefinedProcessor` UDP에 대 한 선택적 특성입니다.

이 인터페이스는 hello에 대 한 hello 정의 포함 해야 `IRow` hello 다음 예제와 같이 인터페이스 행 집합을 재정의 합니다.

```
[SqlUserDefinedProcessor]
public class MyProcessor: IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
        …
 }
}
```

**SqlUserDefinedProcessor** hello 종류를 사용자 정의 처리기로 등록 해야 함을 나타냅니다. 이 클래스는 상속될 수 없습니다.

hello SqlUserDefinedProcessor 특성은 **선택적** UDP 정의 대 한 합니다.

hello 주 프로그래밍 기능 개체는 **입력** 및 **출력**합니다. hello 입력된 개체에 사용 되는 tooenumerate 입력된 열 및 출력 및 hello 프로세서 작업의 결과로 tooset 출력 데이터는 합니다.

입력된 열 열거형에 대 한 사용 하 여 hello `input.Get` 메서드.

```
string column_name = input.Get<string>("column_name");
```

hello에 대 한 매개 변수 `input.Get` 메서드는 hello의 일부로 전달 되는 열 `PRODUCE` hello 절 `PROCESS` hello U-SQL 기본 스크립트의 문. Toouse 필요 hello 올바른 데이터 여기에 입력 하십시오.

출력을 위해 hello를 사용 하 여 `output.Set` 메서드.

반드시 toonote 열과 hello로 정의 된 값에만 해당 사용자 지정 공급자를 출력 `output.Set` 메서드를 호출 합니다.

```
output.Set<string>("mycolumn", mycolumn);
```

호출 하 여 hello 프로세서 실제 출력 트리거될 `return output.AsReadOnly();`합니다.

다음은 처리기 예제입니다.

```
[SqlUserDefinedProcessor]
public class FullDescriptionProcessor : IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
     string user = input.Get<string>("user");
     string des = input.Get<string>("des");
     string full_description = user.ToUpper() + "=>" + des;
     output.Set<string>("dt", input.Get<string>("dt"));
     output.Set<string>("full_description", full_description);
     output.Set<Guid>("new_guid", Guid.NewGuid());
     output.Set<Guid>("guid", input.Get<Guid>("guid"));
     return output.AsReadOnly();
 }
}
```

이 사용 사례 시나리오에서는 hello 프로세서는 hello 기존 열-이 경우 "user"에서 대문자 및 "des"를 결합 하 여 "full_description" 라는 새 열을 생성 합니다. 또한 GUID 다시 생성 하 고 hello 원래 값과 새 GUID 값을 반환 합니다.

C# 중 메서드를 호출 hello 이전 예제의 보시 `output.Set` 메서드를 호출 합니다.

다음은 사용자 지정 처리기를 사용하는 기본 U-SQL 스크립트의 예제입니다.

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
     PROCESS @rs0
     PRODUCE dt String,
             full_description String,
             guid Guid,
             new_guid Guid
     USING new USQL_Programmability.FullDescriptionProcessor();

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a>사용자 정의 적용자 사용
U-SQL 사용자 정의 내용 쿼리의 hello 외부 테이블 식에서 반환 되는 각 행에 대 한 사용자 지정 C# tooinvoke 함수가 있습니다. hello 오른쪽 입력 hello 왼쪽된 입력 으로부터 각 행에 대해 계산 되 고 생성 되는 hello 행 hello 최종 출력에 대 한 조합 됩니다. hello hello APPLY 연산자에서 생성 되는 열 목록에는 hello hello 왼쪽 및 오른쪽 입력 hello의 열 집합의 hello 조합 합니다.

사용자 정의 적용 자 hello USQL 선택 식의 일부로 호출 되 고 됩니다.

일반적인 hello toohello hello 다음과 같은 내용 적용 자 모양 사용자 지정을 호출 합니다.

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

SELECT 식의 적용자 사용에 대한 자세한 내용은 [U-SQL SELECT: CROSS APPLY 및 OUTER APPLY에서 선택](https://msdn.microsoft.com/library/azure/mt621307.aspx)(영문)을 참조하세요.

hello 사용자 정의 된 내용 적용 자 기본 클래스 정의 다음과 같습니다.

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

사용자 정의 적용 자 toodefine toocreate hello 필요 `IApplier` hello로 인터페이스 [`SqlUserDefinedApplier`] 사용자 지정 내용 적용 자 정의 대 한 선택적 특성입니다.

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
    public ParserApplier()
    {
        …
    }

    public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
    {
        …
    }
}
```

* 적용 hello 외부 테이블의 각 행에 대해 호출 됩니다. Hello 반환 `IUpdatableRow` 행 집합을 출력 합니다.
* hello 생성자 클래스는 사용 되는 toopass 매개 변수 toohello 사용자 정의 내용입니다.

**SqlUserDefinedApplier** hello 형식을 사용자 정의 내용으로 등록 해야 함을 나타냅니다. 이 클래스는 상속될 수 없습니다.

**SqlUserDefinedApplier**는 사용자 정의 적용자 정의의 **선택 사항**입니다.


hello 주 프로그래밍 개체는 다음과 같습니다.

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

입력 행 집합은 `IRow` 입력으로 전달됩니다. hello 출력 행으로 생성 됩니다 `IUpdatableRow` 출력 인터페이스입니다.

Hello를 호출 하 여 개별 열 이름을 확인할 수 있습니다 `IRow` 스키마 메서드.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

들어오는 hello에서 tooget hello 실제 데이터 값 `IRow`의 hello get () 메서드 사용 `IRow` 인터페이스입니다.

```
mycolumn = row.Get<int>("mycolumn")
```

또는 hello 스키마 열 이름을 사용 하 여:

```
row.Get<int>(row.Schema[0].Name)
```

hello 출력 값을 설정 해야 `IUpdatableRow` 출력:

```
output.Set<int>("mycolumn", mycolumn)
```

사용자 지정 내용 적용 자 사용 열과 값으로 정의 된 출력만 중요 한 toounderstand는 `output.Set` 메서드를 호출 합니다.

호출 하 여 hello 실제 출력 트리거될 `yield return output.AsReadOnly();`합니다.

toohello 생성자 hello 사용자 정의 내용 적용 자 매개 변수를 전달할 수 있습니다. 내용은 toobe 기본 U-SQL 스크립트에 hello 내용 적용 자 호출 하는 동안 정의 해야 하는 열 수가 달라를 반환할 수 있습니다.

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

사용자 정의 hello 내용 적용 자 예제는 다음과 같습니다.

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
private string parsingPart;

public ParserApplier(string parsingPart)
{
    if (parsingPart.ToUpper().Contains("ALL")
    || parsingPart.ToUpper().Contains("MAKE")
    || parsingPart.ToUpper().Contains("MODEL")
    || parsingPart.ToUpper().Contains("YEAR")
    || parsingPart.ToUpper().Contains("TYPE")
    || parsingPart.ToUpper().Contains("MILLAGE")
    )
    {
    this.parsingPart = parsingPart;
    }
    else
    {
    throw new ArgumentException("Incorrect parameter. Please use: 'ALL[MAKE|MODEL|TYPE|MILLAGE]'");
    }
}

public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
{

    string[] properties = input.Get<string>("properties").Split(',');

    //  only process with correct number of properties
    if (properties.Count() == 5)
    {

    string make = properties[0];
    string model = properties[1];
    string year = properties[2];
    string type = properties[3];
    int millage = -1;

    // Only return millage if it is number, otherwise, -1
    if (!int.TryParse(properties[4], out millage))
    {
        millage = -1;
    }

    if (parsingPart.ToUpper().Contains("MAKE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("make", make);
    if (parsingPart.ToUpper().Contains("MODEL") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("model", model);
    if (parsingPart.ToUpper().Contains("YEAR") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("year", year);
    if (parsingPart.ToUpper().Contains("TYPE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("type", type);
    if (parsingPart.ToUpper().Contains("MILLAGE") || parsingPart.ToUpper().Contains("ALL")) output.Set<int>("millage", millage);
    }
    yield return output.AsReadOnly();            
}
}
```

다음은이 사용자 지정 내용에 대 한 hello 기본 U-SQL 스크립트:

```
DECLARE @input_file string = @"c:\usql-programmability\car_fleet.tsv";
DECLARE @output_file string = @"c:\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        stocknumber int,
        vin String,
        properties String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        r.stocknumber,
        r.vin,
        properties.make,
        properties.model,
        properties.year,
        properties.type,
        properties.millage
    FROM @rs0 AS r
    CROSS APPLY
    new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

이 사용 사례 시나리오에서 사용자 지정 내용 적용 자 카드로 hello 자동차에 대 한 쉼표로 구분 된 값이 파서 함 대 속성입니다. hello 입력된 파일 행 hello 다음과 같습니다.

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

이 파일은 제조업체 모델 등의 자동차 속성을 포함하는 속성 열이 탭으로 분리된 일반적인 TSV 파일입니다. 이러한 속성은 구문 분석 된 toohello 테이블 열 이어야 합니다. 제공 하는 hello 적용 자 toogenerate를 동적 다양 한 속성이 hello에 결과 행 집합을 전달 되는 hello 매개 변수를 기반 있습니다. 모든 속성을 생성하거나 특정 속성 집합만 생성할 수 있습니다.

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

사용자 정의 적용 자 hello 내용 적용 자 개체의 새 인스턴스로 호출할 수 있습니다.

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

또는 hello 래퍼 팩터리 메서드 호출으로:

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a>사용자 정의 결합자 사용
UDC, 또는 사용자 지정 결합 하면 왼쪽 및 오른쪽 행 집합 으로부터, 사용자 지정 논리에 따라 toocombine 행. UDC는 COMBINE 식으로 사용됩니다.

Hello 두 hello 입력된 행 집합에 대 한 필요한 정보를 제공 하는 hello 결합 되어 감사가 만들어집니다 식으로 호출 되는 조합 기, 열을 그룹화, hello hello 예상 결과 스키마 및 추가 정보입니다.

기본 U-SQL 스크립트에 결합 toocall 구문 다음 hello를 사용 합니다.

```
Combine_Expression :=
    'COMBINE' Combine_Input
    'WITH' Combine_Input
    Join_On_Clause
    Produce_Clause
    [Readonly_Clause]
    [Required_Clause]
    USING_Clause.
```

자세한 내용은 [COMBINE 식(U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx)을 참조하세요.

사용자 지정 결합 toodefine toocreate hello 필요 `ICombiner` hello로 인터페이스 [`SqlUserDefinedCombiner`] 사용자 지정 결합 정의 대 한 선택적 특성입니다.

기본 `ICombiner` 클래스 정의:

```
public abstract class ICombiner : IUserDefinedOperator
{
protected ICombiner();
public virtual IEnumerable<IRow> Combine(List<IRowset> inputs,
       IUpdatableRow output);
public abstract IEnumerable<IRow> Combine(IRowset left, IRowset right,
       IUpdatableRow output);
}
```

사용자 지정 구현을 hello는 `ICombiner` 인터페이스에 대 한 hello 정의 포함 해야는 `IEnumerable<IRow>` 재정의 결합 합니다.

```
[SqlUserDefinedCombiner]
public class MyCombiner : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    …
}
}
```

hello **SqlUserDefinedCombiner** 특성을 사용자 지정 결합으로 hello 형식을 등록 해야 함을 나타냅니다. 이 클래스는 상속될 수 없습니다.

**SqlUserDefinedCombiner** 사용 되는 toodefine hello 결합 모드 속성입니다. 사용자 정의 결합자 정의의 선택적 특성입니다.

CombinerMode Mode

CombinerMode enum hello 다음 값을 사용할 수 있습니다.

* 전체 (0) 각 출력 행의 모든 hello 입력된 행에 따라 달라질 왼쪽과 오른쪽 hello을 동일한 키 값.

* 왼쪽 (1) hello 왼쪽에서 단일 입력된 행에 모든 출력 행에 따라 달라 집니다 (및 잠재적으로 모든 행 hello hello로 오른쪽에서 동일한 키 값).

* 오른쪽 (2) hello 오른쪽에서 단일 입력된 행에 모든 출력 행에 따라 달라 집니다 (및 잠재적으로 모든 행 hello로 hello 왼쪽에서 동일한 키 값).

* 왼쪽과 오른쪽을 hello에서 모든 출력 행을 단일 입력에 따라 달라 집니다 (3) 내부 행 동일한 값입니다.

예: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]


hello 주 프로그래밍 기능 개체입니다.

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

입력 행 집합은 **left** 및 **right** `IRowset` 형식의 인터페이스로 전달됩니다. 두 행 집합은 처리하기 위해 모두 열거되어야 합니다. 하므로 tooenumerate 있어야 하 고 필요한 경우 캐시를 한 번 각 인터페이스를 열거할 수만 있습니다.

캐싱을 위해 LINQ 쿼리 실행의 결과로 List\<T\> 형식의 메모리 구조체를 만들 수 있습니다(구체적으로 List<`IRow`>). hello 익명의 데이터 형식으로 열거 하는 동안 사용할 수 있습니다.

참조 [tooLINQ 쿼리 소개 (C#)](https://msdn.microsoft.com/library/bb397906.aspx) LINQ 쿼리에 대 한 자세한 내용은 및 [IEnumerable\<T\> 인터페이스](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) IEnumerable에대한자세한내용은\<T\> 인터페이스입니다.

들어오는 hello에서 tooget hello 실제 데이터 값 `IRowset`의 hello get () 메서드 사용 `IRow` 인터페이스입니다.

```
mycolumn = row.Get<int>("mycolumn")
```

Hello를 호출 하 여 개별 열 이름을 확인할 수 있습니다 `IRow` 스키마 메서드.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

또는 hello 스키마 열 이름을 사용 하 여:

```
c# row.Get<int>(row.Schema[0].Name)
```

LINQ 통한 일반 열거형 hello hello 다음과 같이 표시 됩니다.

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

두 행 집합을 열거 하는 경우, 한 후 모든 행을 tooloop을 하겠습니다. Hello 왼쪽된 행 집합의 각 행에 대해 하겠습니다 toofind 우리의 조합 기의 hello 조건을 만족 하는 모든 행입니다.

hello 출력 값을 설정 해야 `IUpdatableRow` 출력 합니다.

```
output.Set<int>("mycolumn", mycolumn)
```

hello 실제 출력 너무 호출에 의해 트리거되는`yield return output.AsReadOnly();`합니다.

다음은 결합자 예제입니다.

```
[SqlUserDefinedCombiner]
public class CombineSales : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    var internetSales =
    (from row in left.Rows
          select new
          {
              ProductKey = row.Get<int>("ProductKey"),
              OrderDateKey = row.Get<int>("OrderDateKey"),
              SalesAmount = row.Get<decimal>("SalesAmount"),
              TaxAmt = row.Get<decimal>("TaxAmt")
          }).ToList();

    var resellerSales =
    (from row in right.Rows
     select new
     {
     ProductKey = row.Get<int>("ProductKey"),
     OrderDateKey = row.Get<int>("OrderDateKey"),
     SalesAmount = row.Get<decimal>("SalesAmount"),
     TaxAmt = row.Get<decimal>("TaxAmt")
     }).ToList();

    foreach (var row_i in internetSales)
    {
    foreach (var row_r in resellerSales)
    {

        if (
        row_i.OrderDateKey > 0
        && row_i.OrderDateKey < row_r.OrderDateKey
        && row_i.OrderDateKey == 20010701
        && (row_r.SalesAmount + row_r.TaxAmt) > 20000)
        {
        output.Set<int>("OrderDateKey", row_i.OrderDateKey);
        output.Set<int>("ProductKey", row_i.ProductKey);
        output.Set<decimal>("Internet_Sales_Amount", row_i.SalesAmount + row_i.TaxAmt);
        output.Set<decimal>("Reseller_Sales_Amount", row_r.SalesAmount + row_r.TaxAmt);
        }

    }
    }
    yield return output.AsReadOnly();
}
}
```

이 사용 사례 시나리오 hello 소매 업체에 대 한 분석 보고서 작성. hello 목표는 특정 시간 프레임 내에서 일반 소매점 hello 통해 보다 빠르게 hello 웹 사이트를 통해 비용 20000 이상 모든 제품 판매 toofind입니다.

Hello 기본 U-SQL 스크립트는 다음과 같습니다. 일반 조인을는 조합 기 간의 hello 논리를 비교할 수 있습니다.

```sql
DECLARE @LocalURI string = @"\usql-programmability\";

DECLARE @input_file_internet_sales string = @LocalURI+"FactInternetSales.txt";
DECLARE @input_file_reseller_sales string = @LocalURI+"FactResellerSales.txt";
DECLARE @output_file1 string = @LocalURI+"output_file1.tsv";
DECLARE @output_file2 string = @LocalURI+"output_file2.tsv";

@fact_internet_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    CustomerKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_internet_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@fact_reseller_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    ResellerKey int ,
    EmployeeKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_reseller_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@rs1 =
SELECT
    fis.OrderDateKey,
    fis.ProductKey,
    fis.SalesAmount+fis.TaxAmt AS Internet_Sales_Amount,
    frs.SalesAmount+frs.TaxAmt AS Reseller_Sales_Amount
FROM @fact_internet_sales AS fis
     INNER JOIN @fact_reseller_sales AS frs
     ON fis.ProductKey == frs.ProductKey
WHERE
    fis.OrderDateKey < frs.OrderDateKey
    AND fis.OrderDateKey == 20010701
    AND frs.SalesAmount+frs.TaxAmt > 20000;

@rs2 =
COMBINE @fact_internet_sales AS fis
WITH @fact_reseller_sales AS frs
ON fis.ProductKey == frs.ProductKey
PRODUCE OrderDateKey int,
        ProductKey int,
        Internet_Sales_Amount decimal,
        Reseller_Sales_Amount decimal
USING new USQL_Programmability.CombineSales();

OUTPUT @rs1 too@output_file1 USING Outputters.Tsv();
OUTPUT @rs2 too@output_file2 USING Outputters.Tsv();
```

사용자 정의 조합 기 hello 내용 적용 자 개체의 새 인스턴스로 호출할 수 있습니다.

```
USING new MyNameSpace.MyCombiner();
```


또는 hello 래퍼 팩터리 메서드 호출으로:

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a>사용자 정의 리듀서 사용

U-SQL 사용 하면 C#에서 사용자 지정 행 집합 이경소켓 toowrite hello 사용자 정의 연산자 확장 프레임 워크를 사용 하 고 IReducer 인터페이스를 구현 합니다.

리 듀 서 사용자 정의 또는 UDR, 데이터 추출 (가져오기) 하는 동안 사용 되는 tooeliminate 불필요 한 행을 수 있습니다. 또한 고 될 수 toomanipulate 사용 되는 행과 열을 평가 합니다. 프로그래밍 논리를 기반를 정의할 수도 있습니다 행 toobe 추출 해야 합니다.

toocreate 필요 toodefine UDR 클래스는 `IReducer` 인터페이스는 선택적으로 `SqlUserDefinedReducer` 특성입니다.

이 클래스 인터페이스 hello에 대 한 정의 포함 해야 `IEnumerable` 행 집합 인터페이스를 재정의 합니다.

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
        …
    }

}
```

hello **SqlUserDefinedReducer** 특성으로 사용자 정의 리 듀 서 hello 형식을 등록 해야 함을 나타냅니다. 이 클래스는 상속될 수 없습니다.
**SqlUserDefinedReducer**는 UDR(사용자 정의 리듀서) 정의의 선택적 특성이며, Toodefine IsRecursive 속성을 사용 하는 합니다.

* bool IsRecursive    
* **true**는 idempotent 유형의 리듀서인지 여부를 나타냅니다.

hello 주 프로그래밍 기능 개체는 **입력** 및 **출력**합니다. hello 입력 개체가 사용 되는 tooenumerate 입력된 행입니다. 출력은 감소 활동의 결과로 사용 되는 tooset 출력 행입니다.

입력된 행 열거형에 대 한 사용 하 여 hello `Row.Get` 메서드.

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

hello에 대 한 매개 변수를 hello `Row.Get` 메서드는 hello의 일부로 전달 되는 열 `PRODUCE` hello의 클래스 `REDUCE` hello U-SQL 기본 스크립트의 문. Toouse 필요 hello 올바른 데이터 형식을 여기 뿐입니다.

출력을 위해 hello를 사용 하 여 `output.Set` 메서드.

사용자 지정 리 듀 서 지 원하는 유일한 출력 값으로 정의 된 hello 중요 toounderstand는 `output.Set` 메서드를 호출 합니다.

```
output.Set<string>("mycolumn", guid);
```

호출 하 여 hello 실제 리 듀 서 출력 트리거될 `yield return output.AsReadOnly();`합니다.

다음은 리듀서 예제입니다.

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
    string guid;
    DateTime dt;
    string user;
    string des;

    foreach (IRow row in input.Rows)
    {
        guid = row.Get<string>("guid");
        dt = row.Get<DateTime>("dt");
        user = row.Get<string>("user");
        des = row.Get<string>("des");

        if (user.Length > 0)
        {
        output.Set<string>("guid", guid);
        output.Set<DateTime>("dt", dt);
        output.Set<string>("user", user);
        output.Set<string>("des", des);

        yield return output.AsReadOnly();
        }
    }
    }

}
```

이 사용 사례 시나리오에서는 hello 리 듀 서 빈 사용자 이름 가진 행을 건너뛰는 됩니다. 행 집합의 각 행에 대해이 클래스는 필요한 각 열을 읽은 다음 hello 사용자 이름의 hello 길이 계산 합니다. 사용자 이름의 값 길이 0 보다 큰 경우에 hello 실제 행을 출력 합니다.

다음은 사용자 지정 리듀서를 사용하는 기본 U-SQL 스크립트입니다.

```
DECLARE @input_file string = @"\usql-programmability\input_file_reducer.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    REDUCE @rs0 PRESORT guid
    ON guid  
    PRODUCE guid string, dt DateTime, user String, des String
    USING new USQL_Programmability.EmptyUserReducer();

@rs2 =
    SELECT guid AS start_id,
           dt AS start_time,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS start_fiscalperiod,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```
