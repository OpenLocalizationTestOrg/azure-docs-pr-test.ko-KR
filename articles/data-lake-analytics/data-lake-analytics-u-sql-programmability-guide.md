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
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="ed251-103">U-SQL 프로그래밍 기능 가이드</span><span class="sxs-lookup"><span data-stu-id="ed251-103">U-SQL programmability guide</span></span>

<span data-ttu-id="ed251-104">U-SQL은 빅 데이터 유형의 워크로드를 위해 설계된 쿼리 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="ed251-105">Hello U-SQL의 고유한 기능 중 하나에 hello 확장성 및 C#에서 제공 되는 프로그래밍 기능 hello SQL과 유사한 선언적 언어의 hello 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-105">One of hello unique features of U-SQL is hello combination of hello SQL-like declarative language with hello extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="ed251-106">이 가이드에서는 hello 확장성 및 C#에서 사용할 수 있는 hello U SQL 언어의 프로그래밍 기능에 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-106">In this guide, we concentrate on hello extensibility and programmability of hello U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="ed251-107">요구 사항</span><span class="sxs-lookup"><span data-stu-id="ed251-107">Requirements</span></span>

<span data-ttu-id="ed251-108">[Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="ed251-109">U-SQL 시작</span><span class="sxs-lookup"><span data-stu-id="ed251-109">Get started with U-SQL</span></span>  

<span data-ttu-id="ed251-110">U-SQL 스크립트를 다음 hello를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-110">Let’s look at hello following U-SQL script:</span></span>

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

<span data-ttu-id="ed251-111">@a라는 RowSet를 정의하고 @a를 통해 @results라는 RowSet를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="ed251-112">U-SQL 스크립트의 C# 형식 및 식</span><span class="sxs-lookup"><span data-stu-id="ed251-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="ed251-113">U-SQL 식은 `AND`, `OR` 및 `NOT`과 같은 U-SQL 논리 연산자와 결합된 C# 식입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="ed251-114">U-SQL 식은 SELECT, EXTRACT, WHERE, HAVING, GROUP BY 및 DECLARE와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="ed251-115">예를 들어 다음 스크립트는 hello 문자열을 구문 분석 hello SELECT 절에는 DateTime 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-115">For example, hello following script parses a string a DateTime value in hello SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="ed251-116">hello 다음 스크립트 문자열 구문 분석 하는 DECLARE 문에서 DateTime 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-116">hello following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="ed251-117">데이터 형식 변환에 C# 식 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="ed251-118">다음 예제는 hello C# 식을 사용 하 여 datetime 데이터 변환을 수행할 수는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-118">hello following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="ed251-119">이 특정 시나리오에서 문자열 날짜/시간 데이터는 자정 00시: 00 시간 표기법으로 변환 된 toostandard datetime입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-119">In this particular scenario, string datetime data is converted toostandard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="ed251-120">오늘 날짜에 C# 식 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="ed251-121">toopull 오늘 날짜를 사용할 수 다음 C# 식은 hello:</span><span class="sxs-lookup"><span data-stu-id="ed251-121">toopull today’s date, we can use hello following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="ed251-122">방법의 예로 toouse 스크립트에서이 식은:</span><span class="sxs-lookup"><span data-stu-id="ed251-122">Here's an example of how toouse this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="ed251-123">.NET 어셈블리 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-123">Using .NET assemblies</span></span>
<span data-ttu-id="ed251-124">U-SQL의 확장성 모델은 사용자 지정 코드를 tooadd hello 기능에 크게 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-124">U-SQL’s extensibility model relies heavily on hello ability tooadd custom code.</span></span> <span data-ttu-id="ed251-125">현재 U-SQL 사용 하면 간단한 방법으로 tooadd 자신의 Microsoft 있습니다. .NET 기반 코드 (특히, C#)입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-125">Currently, U-SQL provides you with easy ways tooadd your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="ed251-126">하지만 다른 .NET 언어(예: VB.NET 또는 F#)로 작성된 사용자 지정 코드를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="ed251-127">.NET 어셈블리 등록</span><span class="sxs-lookup"><span data-stu-id="ed251-127">Register a .NET assembly</span></span>

<span data-ttu-id="ed251-128">Hello CREATE ASSEMBLY 문을 tooplace U SQL 데이터베이스에.NET 어셈블리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-128">Use hello CREATE ASSEMBLY statement tooplace a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="ed251-129">데이터베이스에 어셈블리를 U-SQL 스크립트 hello 참조 어셈블리 문을 사용 하 여 해당 어셈블리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using hello REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="ed251-130">코드에서 보여 주는 방법을 다음 hello tooregister 어셈블리:</span><span class="sxs-lookup"><span data-stu-id="ed251-130">hello following code shows how tooregister an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="ed251-131">코드에서 보여 주는 방법을 다음 hello tooreference 어셈블리:</span><span class="sxs-lookup"><span data-stu-id="ed251-131">hello following code shows how tooreference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="ed251-132">Hello 참조 [어셈블리 등록 명령을](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) 이 항목에서 자세히 다루는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-132">Consult hello [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="ed251-133">어셈블리 버전 관리 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-133">Use assembly versioning</span></span>
<span data-ttu-id="ed251-134">현재, U-SQL hello.NET Framework 버전 4.5를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-134">Currently, U-SQL uses hello .NET Framework version 4.5.</span></span> <span data-ttu-id="ed251-135">따라서 사용자 고유의 어셈블리와 해당 버전의 hello 런타임이 호환 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-135">So ensure that your own assemblies are compatible with that version of hello runtime.</span></span>

<span data-ttu-id="ed251-136">앞에서 언급했듯이 U-SQL은 64비트(x64) 형식 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="ed251-137">않으므로 코드 x64 컴파일된 toorun 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-137">So make sure that your code is compiled toorun on x64.</span></span> <span data-ttu-id="ed251-138">그렇지 않으면 오류가 hello 잘못 된 형식 앞에 표시 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-138">Otherwise you get hello incorrect format error shown earlier.</span></span>

<span data-ttu-id="ed251-139">업로드된 각 어셈블리 DLL, 리소스 파일(예: 다양한 런타임), 네이티브 어셈블리 또는 구성 파일의 크기는 최대 400MB입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="ed251-140">hello 리소스 배포를 통해 또는 참조 tooassemblies 및 추가 파일을 통해 배포 된 리소스의 전체 크기는 3GB를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-140">hello total size of deployed resources, either via DEPLOY RESOURCE or via references tooassemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="ed251-141">마지막으로 U-SQL 데이터베이스마다 지정된 어셈블리 버전을 하나만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="ed251-142">예를 들어 버전 7 및 8 버전의 hello NewtonSoft Json.Net 라이브러리 모두, 필요한 경우 필요한 tooregister 서로 다른 두 데이터베이스에서 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-142">For example, if you need both version 7 and version 8 of hello NewtonSoft Json.Net library, you need tooregister them in two different databases.</span></span> <span data-ttu-id="ed251-143">또한 각 스크립트 tooone 버전 지정된 된 어셈블리 DLL 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-143">Furthermore, each script can only refer tooone version of a given assembly DLL.</span></span> <span data-ttu-id="ed251-144">이런 점에서 U-SQL hello C# 어셈블리 관리 및 버전 관리를 의미 체계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-144">In this respect, U-SQL follows hello C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="ed251-145">UDF(사용자 정의 함수) 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="ed251-146">U-SQL 사용자 정의 함수 또는 UDF는 매개 변수를 받아들이고 (예: 복잡 한 계산의 경우) 작업을 수행 하는 값으로 해당 작업의 hello 결과 반환 하는 루틴을 프로그래밍 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return hello result of that action as a value.</span></span> <span data-ttu-id="ed251-147">hello 반환 UDF의 값에는 단일 스칼라만 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-147">hello return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="ed251-148">U-SQL UDF는 다른 C# 스칼라 함수와 같이 U-SQL 기본 스크립트에서 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="ed251-149">U-SQL 사용자 정의 함수는 **public** 및 **static**으로 초기화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="ed251-150">첫 번째 hello 간단한 UDF를 만드는 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-150">First let’s look at hello simple example of creating a UDF.</span></span>

<span data-ttu-id="ed251-151">이 사용 사례 시나리오에서는 toodetermine hello 회계 기간을 hello 회계 분기 등 hello 첫 번째 로그인 hello 특정 사용자에 대 한 회계 월 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-151">In this use-case scenario, we need toodetermine hello fiscal period, including hello fiscal quarter and fiscal month of hello first sign-in for hello specific user.</span></span> <span data-ttu-id="ed251-152">hello는 시나리오에서 hello 연도의 첫 번째 회계 월이 6 월.</span><span class="sxs-lookup"><span data-stu-id="ed251-152">hello first fiscal month of hello year in our scenario is June.</span></span>

<span data-ttu-id="ed251-153">toocalculate 회계 기간 hello 다음 C# 함수를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-153">toocalculate fiscal period, we introduce hello following C# function:</span></span>

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

<span data-ttu-id="ed251-154">단순히 회계 월과 분기를 계산하고 문자열 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="ed251-155">첫 번째 회계 분기 hello의 첫 번째 월 hello 년 6 월에 대 한 "Q1:P1" 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-155">For June, hello first month of hello first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="ed251-156">7월에 대해서는 "Q1:P2"를 사용하고 이런 방식으로 계속 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="ed251-157">이것은 일반 C# 기능 U-SQL 프로젝트에 진행 중인 toouse는 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-157">This is a regular C# function that we are going toouse in our U-SQL project.</span></span>

<span data-ttu-id="ed251-158">이 시나리오에서 코드 숨김 섹션 hello 모양을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-158">Here is how hello code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="ed251-159">이제 하겠습니다 toocall이이 함수 hello 기본 U-SQL 스크립트에서.</span><span class="sxs-lookup"><span data-stu-id="ed251-159">Now we are going toocall this function from hello base U-SQL script.</span></span> <span data-ttu-id="ed251-160">toodo이 tooprovide를 비롯 하 여 hello 네임 스페이스는이 예에서 NameSpace.Class.Function(parameter) hello 함수에 대 한 정규화 된 이름을 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-160">toodo this, we have tooprovide a fully qualified name for hello function, including hello namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="ed251-161">다음은 hello 실제 U-SQL 기본 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-161">Following is hello actual U-SQL base script:</span></span>

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

<span data-ttu-id="ed251-162">다음은 hello 스크립트 실행의 hello 출력 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-162">Following is hello output file of hello script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="ed251-163">이 예제에서는 U-SQL에서 인라인 UDF를 간단하게 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="ed251-164">UDF 호출 사이 상태 유지</span><span class="sxs-lookup"><span data-stu-id="ed251-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="ed251-165">U-SQL C# 프로그래밍 기능 개체 수 수 더 복잡 한, hello 코드 숨김 전역 변수를 통해 대화형 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through hello code-behind global variables.</span></span> <span data-ttu-id="ed251-166">비즈니스 사용 사례 시나리오를 따르는 hello를 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-166">Let’s look at hello following business use-case scenario.</span></span>

<span data-ttu-id="ed251-167">대규모 조직에서는 사용자가 다양한 내부 응용 프로그램 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="ed251-168">여기에는 Microsoft Dynamics CRM, PowerBI 등이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="ed251-169">고객 tooapply 사용자가 어떤 hello 사용 추세 및에 서로 다른 응용 프로그램 전환 하는 방법에 대 한 원격 분석 분석을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-169">Customers might want tooapply a telemetry analysis of how users switch between different applications, what hello usage trends are, and so on.</span></span> <span data-ttu-id="ed251-170">hello hello 비즈니스용 ´ ֲ toooptimize 응용 프로그램 사용.</span><span class="sxs-lookup"><span data-stu-id="ed251-170">hello goal for hello business is toooptimize application usage.</span></span> <span data-ttu-id="ed251-171">또한 toocombine 서로 다른 응용 프로그램 또는 특정 로그온 루틴 합니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-171">They also might want toocombine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="ed251-172">tooachieve toodetermine 세션 Id 및 hello에 발생 한 마지막 세션 사이 지연 기간 있는이 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-172">tooachieve this goal, we have toodetermine session IDs and lag time between hello last session that occurred.</span></span>

<span data-ttu-id="ed251-173">그런 다음 할당할 toohello 생성된 되는이 로그인 tooall 세션 및 이전 로그인 toofind 필요 동일한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-173">We need toofind a previous sign-in and then assign this sign-in tooall sessions that are being generated toohello same application.</span></span> <span data-ttu-id="ed251-174">hello 첫 번째 인증은 기본 U-SQL 스크립트 하지 않는 허용 우리 tooapply 계산 LAG 함수를 이미 계산 열에 대해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-174">hello first challenge is that U-SQL base script doesn't allow us tooapply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="ed251-175">hello 두 번째 문제는 hello tookeep hello 내에서 모든 세션에 대 한 특정 세션 있다는 것 같은 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-175">hello second challenge is that we have tookeep hello specific session for all sessions within hello same time period.</span></span>

<span data-ttu-id="ed251-176">toosolve이이 문제는 코드 숨김 섹션 내 전역 변수를 사용 하 여 했습니다: `static public string globalSession;`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-176">toosolve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="ed251-177">전역 변수가이 우리의 스크립트를 실행 하는 동안 적용 된 toohello 전체 행 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-177">This global variable is applied toohello entire rowset during our script execution.</span></span>

<span data-ttu-id="ed251-178">다음은 U-SQL 프로그램의 hello 코드 숨김 섹션이입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-178">Here is hello code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="ed251-179">이 예제에서는 전역 변수 hello `static public string globalSession;` hello 내에서 사용할 `getStampUserSession` 함수 및 가져오기 각 시간 hello 매개 변수가 변경 된 세션을 다시 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-179">This example shows hello global variable `static public string globalSession;` used inside hello `getStampUserSession` function and getting reinitialized each time hello Session parameter is changed.</span></span>

<span data-ttu-id="ed251-180">hello U-SQL 기본 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-180">hello U-SQL base script is as follows:</span></span>

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

<span data-ttu-id="ed251-181">함수 `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` 여기 hello 두 번째 메모리 행 집합 계산 하는 동안 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during hello second memory rowset calculation.</span></span> <span data-ttu-id="ed251-182">Hello 전달 `UserSessionTimestamp` 열 및 반환 값까지 hello `UserSessionTimestamp` 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-182">It passes hello `UserSessionTimestamp` column and returns hello value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="ed251-183">hello 출력 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-183">hello output file is as follows:</span></span>

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

<span data-ttu-id="ed251-184">이 예제에서는 적용된 toohello 전체 메모리 행 집합은 하는 코드 숨김 섹션 내 전역 변수를 사용 하는 보다 복잡 한 사용 사례 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied toohello entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="ed251-185">UDT(사용자 정의 형식) 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="ed251-186">UDT(사용자 정의 형식)는 U-SQL의 또 다른 프로그래밍 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="ed251-187">U-SQL UDT는 일반 C# 사용자 정의 형식처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="ed251-188">C#은 기본 및 사용자 지정 사용자 정의 형식 hello 사용을 허용 하는 강력한 형식의 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-188">C# is a strongly typed language that allows hello use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="ed251-189">U-SQL 암시적으로 직렬화 하거나 행 집합에서 꼭지점을 잇는 hello UDT 전달 될 때 임의의 Udt를 역직렬화 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when hello UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="ed251-190">이 hello이 사용자는 tooprovide 명시적 포맷터 hello IFormatter 인터페이스를 사용 하 여 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-190">This means that hello user has tooprovide an explicit formatter by using hello IFormatter interface.</span></span> <span data-ttu-id="ed251-191">U-SQL hello로 이로써 serialize hello UDT에 대 한 메서드 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-191">This provides U-SQL with hello serialize and de-serialize methods for hello UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="ed251-192">U-SQL의 기본 제공 추출기 outputters 현재 serialize 하거나 없습니다 hello IFormatter 설정 된 경우에 파일에서 UDT 데이터 tooor을 역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data tooor from files even with hello IFormatter set.</span></span> <span data-ttu-id="ed251-193">따라서 출력 문 hello로 UDT 데이터 tooa 파일을 작성할 아니면 toopass가 추출기와 함께 읽을 때로 문자열 또는 바이트 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-193">So when you're writing UDT data tooa file with hello OUTPUT statement, or reading it with an extractor, you have toopass it as a string or byte array.</span></span> <span data-ttu-id="ed251-194">그런 다음 hello serialization을 호출 하 고 코드 (즉, hello UDT의 tostring (메서드)를) 명시적으로 역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-194">Then you call hello serialization and deserialization code (that is, hello UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="ed251-195">사용자 정의 추출기 및 다른 hello에 outputters 전달, 읽고 쓸 수 Udt입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-195">User-defined extractors and outputters, on hello other hand, can read and write UDTs.</span></span>

<span data-ttu-id="ed251-196">다음과 같이 toouse EXTRACTOR 또는 이전 SELECT), (부족 OUTPUTTER에서 UDT를 시도 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-196">If we try toouse UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="ed251-197">Hello 다음 오류가 수신 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-197">We receive hello following error:</span></span>

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

<span data-ttu-id="ed251-198">UDT와 toowork outputter, 하거나 했으므로 tooserialize 것와 toostring hello tostring () 메서드 또는 사용자 지정 outputter 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-198">toowork with UDT in outputter, we either have tooserialize it toostring with hello ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="ed251-199">UDT는 현재 GROUP BY에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="ed251-200">GROUP BY에 UDT 사용 하면 다음 오류가 hello throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-200">If UDT is used in GROUP BY, hello following error is thrown:</span></span>

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

<span data-ttu-id="ed251-201">UDT toodefine을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-201">toodefine a UDT, we have to:</span></span>

* <span data-ttu-id="ed251-202">Hello 다음 네임 스페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-202">Add hello following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="ed251-203">추가 `Microsoft.Analytics.Interfaces`, hello UDT 인터페이스에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-203">Add `Microsoft.Analytics.Interfaces`, which is required for hello UDT interfaces.</span></span> <span data-ttu-id="ed251-204">또한 `System.IO` 필요한 toodefine hello IFormatter 인터페이스 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-204">In addition, `System.IO` might be needed toodefine hello IFormatter interface.</span></span>

* <span data-ttu-id="ed251-205">SqlUserDefinedType 특성을 사용하여 사용자 정의 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="ed251-206">**SqlUserDefinedType** U-SQL toomark 사용 되는 사용자 정의 형식 (UDT)으로 어셈블리의 형식 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-206">**SqlUserDefinedType** is used toomark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="ed251-207">hello 특성에 hello 속성 hello hello UDT의 물리적 특성을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-207">hello properties on hello attribute reflect hello physical characteristics of hello UDT.</span></span> <span data-ttu-id="ed251-208">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-208">This class cannot be inherited.</span></span>

<span data-ttu-id="ed251-209">SqlUserDefinedType은 UDT 정의에 필요한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="ed251-210">hello 클래스의 생성자를 hello:</span><span class="sxs-lookup"><span data-stu-id="ed251-210">hello constructor of hello class:</span></span>  

* <span data-ttu-id="ed251-211">SqlUserDefinedTypeAttribute(형식 포맷터)</span><span class="sxs-lookup"><span data-stu-id="ed251-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="ed251-212">유형 포맷터: 필수 매개 변수 toodefine UDT 포맷터-특히 hello 유형의 hello `IFormatter` 인터페이스는 여기에 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-212">Type formatter: Required parameter toodefine an UDT formatter--specifically, hello type of hello `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="ed251-213">일반적인 UDT hello 다음 예제와 같이 hello IFormatter 인터페이스의 정의 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-213">Typical UDT also requires definition of hello IFormatter interface, as shown in hello following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="ed251-214">hello `IFormatter` 인터페이스를 직렬화 및 역직렬화 하는 개체 그래프의 루트 형식 hello와 \<typeparamref 이름 = "T" >.</span><span class="sxs-lookup"><span data-stu-id="ed251-214">hello `IFormatter` interface serializes and de-serializes an object graph with hello root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="ed251-215">\<typeparam 이름 = "T" > hello 개체 그래프 tooserialize에 대해 루트 형식 hello 및 역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-215">\<typeparam name="T">hello root type for hello object graph tooserialize and de-serialize.</span></span>

* <span data-ttu-id="ed251-216">**Deserialize**: 제공 된 hello 스트림에서 hello 데이터를 역직렬화 하 고 개체의 그래프를 hello를 다시 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-216">**Deserialize**: De-serializes hello data on hello provided stream and reconstitutes hello graph of objects.</span></span>

* <span data-ttu-id="ed251-217">**직렬화**: 루트 제공 toohello 스트림을 제공 하는 hello로 개체 또는 개체 그래프를 Serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-217">**Serialize**: Serializes an object, or graph of objects, with hello given root toohello provided stream.</span></span>

<span data-ttu-id="ed251-218">`MyType`인스턴스: hello 형식의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-218">`MyType` instance: Instance of hello type.</span></span>  
<span data-ttu-id="ed251-219">`IColumnWriter`기록기 / `IColumnReader` 판독기: hello 열 스트림 원본으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-219">`IColumnWriter` writer / `IColumnReader` reader: hello underlying column stream.</span></span>  
<span data-ttu-id="ed251-220">`ISerializationContext`상황에 맞는: 직렬화 하는 동안 hello 스트림에 대 한 hello 소스 또는 대상 컨텍스트를 지정 하는 플래그 집합을 정의 하는 열거형입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-220">`ISerializationContext` context: Enum that defines a set of flags that specifies hello source or destination context for hello stream during serialization.</span></span>

* <span data-ttu-id="ed251-221">**중간**: hello 소스 또는 대상 컨텍스트를 해당 지속형된 저장소 아님을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-221">**Intermediate**: Specifies that hello source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="ed251-222">**지 속성**: hello 소스 또는 대상 컨텍스트를 해당 지속형된 저장소 인지 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-222">**Persistence**: Specifies that hello source or destination context is a persisted store.</span></span>

<span data-ttu-id="ed251-223">일반 C# 형식으로 U-SQL UDT 정의는 +/==/!= 등의 연산자에 대한 재정의를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="ed251-224">정적 메서드도 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-224">It can also include static methods.</span></span> <span data-ttu-id="ed251-225">예를 들어 하겠습니다 toouse이이 UDT로 매개 변수 tooa U SQL MIN 집계 함수, 있는지 toodefine < 연산자 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-225">For example, if we are going toouse this UDT as a parameter tooa U-SQL MIN aggregate function, we have toodefine < operator override.</span></span>

<span data-ttu-id="ed251-226">이 가이드의 hello 형식 (Q1:P10) Qn:Pn hello 특정 날짜부터 회계 기간 id에 대 한 예에 설명 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-226">Earlier in this guide, we demonstrated an example for fiscal period identification from hello specific date in hello format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="ed251-227">다음 예제는 hello toodefine 사용자 지정 입력 하는 방법을 회계 기간 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-227">hello following example shows how toodefine a custom type for fiscal period values.</span></span>

<span data-ttu-id="ed251-228">다음은 사용자 지정 UDT 및 IFormatter 인터페이스가 포함된 코드 숨김 섹션의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="ed251-229">hello 정의 된 형식이 포함 되어 두 개의 숫자: 분기 및 월.</span><span class="sxs-lookup"><span data-stu-id="ed251-229">hello defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="ed251-230">여기서 ==/!=/>/< 연산자 및 ToString() 정적 메서드가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="ed251-231">앞에서 설명한 대로 UDT는 SELECT 식에서 사용할 수 있지만, 사용자 지정 직렬화 없이는 OUTPUTTER/EXTRACTOR에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="ed251-232">Tostring () 문자열로 serialize 된 하거나 사용자 지정 OUTPUTTER/EXTRACTOR를 사용해 서 toobe 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-232">It either has toobe serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="ed251-233">이제 UDT 사용법에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="ed251-234">코드 숨김 섹션에서 다음 우리의 GetFiscalPeriod function toohello 변경 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-234">In a code-behind section, we changed our GetFiscalPeriod function toohello following:</span></span>

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

<span data-ttu-id="ed251-235">볼 수 있듯이 우리 FiscalPeriod 형식의 hello 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-235">As you can see, it returns hello value of our FiscalPeriod type.</span></span>

<span data-ttu-id="ed251-236">여기 어떻게 toouse 것에서 자세히 U-SQL 기본 스크립트의 예를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-236">Here we provide an example of how toouse it further in U-SQL base script.</span></span> <span data-ttu-id="ed251-237">이 예제에서는 U-SQL 스크립트에서 UDT를 호출하는 다른 형식을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

<span data-ttu-id="ed251-238">다음은 전체 코드 숨김 섹션의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="ed251-239">UDAGG(사용자 정의 집계) 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="ed251-240">UDAGG(사용자 정의 집계)는 U-SQL에 제공되지 않는 집계 관련 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="ed251-241">hello 예제 수 사용자 지정 수학 계산, 문자열 연결 문자열을 사용한 조작을 집계 tooperform 수 등에입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-241">hello example can be an aggregate tooperform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="ed251-242">hello 사용자 정의 집계 기본 클래스 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-242">hello user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="ed251-243">**SqlUserDefinedAggregate** hello 형식을 사용자 정의 집계로 등록 해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-243">**SqlUserDefinedAggregate** indicates that hello type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="ed251-244">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-244">This class cannot be inherited.</span></span>

<span data-ttu-id="ed251-245">SqlUserDefinedType 특성은 UDAGG 정의의 **선택 사항**입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="ed251-246">hello 기본 클래스를 사용 하 toopass 3 추상 매개 변수: 두 개의 입력된 매개 변수도 hello 결과로 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-246">hello base class allows you toopass three abstract parameters: two as input parameters and one as hello result.</span></span> <span data-ttu-id="ed251-247">hello 데이터 형식 변수는 클래스를 상속 하는 동안 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-247">hello data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="ed251-248">**Init**는 계산하는 동안 각 그룹에 대해 한 번씩 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="ed251-249">각 집계 그룹에 대한 초기화 루틴을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="ed251-250">**Accumulate**는 각 값에 대해 한 번씩 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="ed251-251">Hello 집계 알고리즘에 대 한 hello 주요 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-251">It provides hello main functionality for hello aggregation algorithm.</span></span> <span data-ttu-id="ed251-252">클래스를 상속 하는 동안 정의 된 다양 한 데이터 형식에 사용 되는 tooaggregate 값 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-252">It can be used tooaggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="ed251-253">변수 데이터 형식의 매개 변수 두 개를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="ed251-254">**종료** hello 끝 각 그룹에 대 한 toooutput hello 결과 처리에 대 한 집계 그룹당 한 번씩 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-254">**Terminate** is executed once per aggregation group at hello end of processing toooutput hello result for each group.</span></span>

<span data-ttu-id="ed251-255">toodeclare 올바른 입력 및 출력 데이터 형식을 다음과 같이 hello 클래스 정의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-255">toodeclare correct input and output data types, use hello class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="ed251-256">첫 번째 매개 변수 tooaccumulate T1:</span><span class="sxs-lookup"><span data-stu-id="ed251-256">T1: First parameter tooaccumulate</span></span>
* <span data-ttu-id="ed251-257">첫 번째 매개 변수 tooaccumulate T2:</span><span class="sxs-lookup"><span data-stu-id="ed251-257">T2: First parameter tooaccumulate</span></span>
* <span data-ttu-id="ed251-258">TResult: Terminate의 반환 형식</span><span class="sxs-lookup"><span data-stu-id="ed251-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="ed251-259">예:</span><span class="sxs-lookup"><span data-stu-id="ed251-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="ed251-260">또는</span><span class="sxs-lookup"><span data-stu-id="ed251-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="ed251-261">U-SQL에서 UDAGG 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="ed251-262">toouse UDAGG, 먼저 코드 숨김에 정의 하거나 이전에 설명한 대로 hello 존재 프로그래밍 기능 DLL에서에서 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-262">toouse UDAGG, first define it in code-behind or reference it from hello existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="ed251-263">다음 구문 다음 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ed251-263">Then use hello following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="ed251-264">UDAGG의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="ed251-265">기본 U-SQL 스크립트:</span><span class="sxs-lookup"><span data-stu-id="ed251-265">And base U-SQL script:</span></span>

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

<span data-ttu-id="ed251-266">이 사용 사례 시나리오에서는 hello 특정 사용자에 대 한 Guid 클래스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-266">In this use-case scenario, we concatenate class GUIDs for hello specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="ed251-267">UDO(사용자 정의 개체) 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="ed251-268">U-SQL 위의 UDO 또는 사용자 정의 개체 라고 하는 사용자 지정 프로그래밍 기능 개체를 toodefine 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-268">U-SQL enables you toodefine custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="ed251-269">hello 다음은 U-SQL에는 UDO의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-269">hello following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="ed251-270">사용자 정의 추출기</span><span class="sxs-lookup"><span data-stu-id="ed251-270">User-defined extractors</span></span>
    * <span data-ttu-id="ed251-271">행 단위 추출</span><span class="sxs-lookup"><span data-stu-id="ed251-271">Extract row by row</span></span>
    * <span data-ttu-id="ed251-272">사용자 지정 구조화 된 파일에서 데이터 추출을 tooimplement 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-272">Used tooimplement data extraction from custom structured files</span></span>

* <span data-ttu-id="ed251-273">사용자 정의 출력자</span><span class="sxs-lookup"><span data-stu-id="ed251-273">User-defined outputters</span></span>
    * <span data-ttu-id="ed251-274">행 단위 출력</span><span class="sxs-lookup"><span data-stu-id="ed251-274">Output row by row</span></span>
    * <span data-ttu-id="ed251-275">Toooutput 사용자 지정 데이터 형식이 나 사용자 지정 파일 형식 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-275">Used toooutput custom data types or custom file formats</span></span>

* <span data-ttu-id="ed251-276">사용자 정의 처리기</span><span class="sxs-lookup"><span data-stu-id="ed251-276">User-defined processors</span></span>
    * <span data-ttu-id="ed251-277">한 행씩 가져와 한 행씩 생성</span><span class="sxs-lookup"><span data-stu-id="ed251-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="ed251-278">사용 되는 tooreduce hello 열의 수 또는 새 열을 기존 열 집합에서 파생 된 값으로 생성</span><span class="sxs-lookup"><span data-stu-id="ed251-278">Used tooreduce hello number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="ed251-279">사용자 정의 적용자</span><span class="sxs-lookup"><span data-stu-id="ed251-279">User-defined appliers</span></span>
    * <span data-ttu-id="ed251-280">한 행을 사용 toon 행이 0을 생성 하는</span><span class="sxs-lookup"><span data-stu-id="ed251-280">Take one row and produce 0 toon rows</span></span>
    * <span data-ttu-id="ed251-281">OUTER/CROSS APPLY 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="ed251-282">사용자 정의 결합자</span><span class="sxs-lookup"><span data-stu-id="ed251-282">User-defined combiners</span></span>
    * <span data-ttu-id="ed251-283">행 집합 결합--사용자 정의 JOIN</span><span class="sxs-lookup"><span data-stu-id="ed251-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="ed251-284">사용자 정의 리듀서</span><span class="sxs-lookup"><span data-stu-id="ed251-284">User-defined reducers</span></span>
    * <span data-ttu-id="ed251-285">n개 행을 가져와 한 행씩 생성</span><span class="sxs-lookup"><span data-stu-id="ed251-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="ed251-286">Tooreduce hello 행 수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-286">Used tooreduce hello number of rows</span></span>

<span data-ttu-id="ed251-287">UDO는 일반적으로 다음 U-SQL 조건 hello의 일부로 U-SQL 스크립트에 명시적으로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-287">UDO is typically called explicitly in U-SQL script as part of hello following U-SQL statements:</span></span>

* <span data-ttu-id="ed251-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="ed251-288">EXTRACT</span></span>
* <span data-ttu-id="ed251-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="ed251-289">OUTPUT</span></span>
* <span data-ttu-id="ed251-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="ed251-290">PROCESS</span></span>
* <span data-ttu-id="ed251-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="ed251-291">COMBINE</span></span>
* <span data-ttu-id="ed251-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="ed251-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="ed251-293">UDO의 제한 된 tooconsume 0.5 g b 메모리를 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-293">UDO’s are limited tooconsume 0.5Gb memory.</span></span>  <span data-ttu-id="ed251-294">이 메모리 제한을 toolocal 실행 될 때 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-294">This memory limitation does not apply toolocal executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="ed251-295">UDE(사용자 정의 추출기) 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-295">Use user-defined extractors</span></span>
<span data-ttu-id="ed251-296">U-SQL 추출 문을 사용 하 여 tooimport 외부 데이터를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-296">U-SQL allows you tooimport external data by using an EXTRACT statement.</span></span> <span data-ttu-id="ed251-297">EXTRACT 문은 기본 제공 UDO 추출기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="ed251-298">*Extractors.Text()*: 다른 인코딩의 구분 기호로 분리된 텍스트 파일에서 데이터를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="ed251-299">*Extractors.Csv()*: 다른 인코딩의 쉼표로 구분된 값(CSV) 파일에서 데이터를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="ed251-300">*Extractors.Tsv()*: 다른 인코딩의 탭으로 구분된 값(TSV) 파일에서 데이터를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="ed251-301">유용한 toodevelop 사용자 지정 추출기 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-301">It can be useful toodevelop a custom extractor.</span></span> <span data-ttu-id="ed251-302">이 유용 데이터를 가져오는 동안 할까요 toodo hello 다음 작업 중 하나:</span><span class="sxs-lookup"><span data-stu-id="ed251-302">This can be helpful during data import if we want toodo any of hello following tasks:</span></span>

* <span data-ttu-id="ed251-303">열을 분할하고 개별 값을 수정하여 입력 데이터를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="ed251-304">hello 프로세서 기능 열을 결합 하는 데 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-304">hello PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="ed251-305">구조화되지 않은 데이터(예: 웹 페이지 및 전자 메일) 또는 반 구조화되지 않은 데이터(예: XML/JSON)를 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="ed251-306">지원되지 않는 인코딩 데이터를 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="ed251-307">사용자 정의 extractor toodefine toocreate 필요 UDE, 또는 `IExtractor` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-307">toodefine a user-defined extractor, or UDE, we need toocreate an `IExtractor` interface.</span></span> <span data-ttu-id="ed251-308">열/행 구분 기호 및 인코딩, 필요한 toobe hello 클래스의 hello 생성자에 정의 된 같은 기준으로 모든 입력 매개 변수 toohello extractor 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-308">All input parameters toohello extractor, such as column/row delimiters, and encoding, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="ed251-309">hello `IExtractor` 인터페이스 hello에 대 한 정의 있어야 `IEnumerable<IRow>` 다음과 같이 재정의:</span><span class="sxs-lookup"><span data-stu-id="ed251-309">hello `IExtractor`  interface should also contain a definition for hello `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="ed251-310">hello **SqlUserDefinedExtractor** 특성으로 사용자 정의 extractor hello 형식을 등록 해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-310">hello **SqlUserDefinedExtractor** attribute indicates that hello type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="ed251-311">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-311">This class cannot be inherited.</span></span>

<span data-ttu-id="ed251-312">SqlUserDefinedExtractor는 UDE 정의의 선택적 특성이며,</span><span class="sxs-lookup"><span data-stu-id="ed251-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="ed251-313">Hello UDE 개체에 대 한 toodefine AtomicFileProcessing 속성을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-313">It used toodefine AtomicFileProcessing property for hello UDE object.</span></span>

* <span data-ttu-id="ed251-314">bool AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="ed251-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="ed251-315">**true**는 추출기에 원자성 입력 파일(JSON, XML 등)이 필요함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="ed251-316">**false**는 추출기에서 분할/분산 파일(CSV, SEQ 등)을 처리할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="ed251-317">hello 주요 UDE 프로그래밍 기능 개체는 **입력** 및 **출력**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-317">hello main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="ed251-318">hello 입력된 개체는으로 입력된 데이터를 사용 하는 tooenumerate `IUnstructuredReader`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-318">hello input object is used tooenumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="ed251-319">hello 출력 개체에는 hello extractor 활동의 결과로 사용 되는 tooset 출력 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-319">hello output object is used tooset output data as a result of hello extractor activity.</span></span>

<span data-ttu-id="ed251-320">hello 입력된 데이터를 통해 액세스 `System.IO.Stream` 및 `System.IO.StreamReader`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-320">hello input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="ed251-321">입력된 열 열거형에 대 한 म 먼저 hello 입력된 스트림을 사용 하 여 분할 행 구분 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-321">For input columns enumeration, we first split hello input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="ed251-322">그런 다음 입력 행을 열 파트로 세분합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="ed251-323">tooset 출력 데이터를 사용 하 여 hello `output.Set` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed251-323">tooset output data, we use hello `output.Set` method.</span></span>

<span data-ttu-id="ed251-324">사용자 지정 extractor hello toounderstand만 출력의 열과 값 정의 된 hello 출력 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-324">It's important toounderstand that hello custom extractor only outputs columns and values that are defined with hello output.</span></span> <span data-ttu-id="ed251-325">메서드 호출을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="ed251-326">호출 하 여 hello 실제 extractor 출력 트리거될 `yield return output.AsReadOnly();`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-326">hello actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="ed251-327">다음은 hello extractor 예.</span><span class="sxs-lookup"><span data-stu-id="ed251-327">Following is hello extractor example:</span></span>

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

<span data-ttu-id="ed251-328">이 사용 사례 시나리오에서 hello extractor "guid" 열에 대 한 hello GUID 다시 생성 하 고 "user" 열 tooupper 사례의 hello 값으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-328">In this use-case scenario, hello extractor regenerates hello GUID for “guid” column and converts hello values of “user” column tooupper case.</span></span> <span data-ttu-id="ed251-329">사용자 지정 추출기는 입력 데이터를 구문 분석하고 이를 조작하여 더 복잡한 결과를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="ed251-330">다음은 사용자 지정 추출기를 사용하는 기본 U-SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

## <a name="use-user-defined-outputters"></a><span data-ttu-id="ed251-331">사용자 정의 출력자 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-331">Use user-defined outputters</span></span>
<span data-ttu-id="ed251-332">사용자 정의 outputter U-SQL 기능이 기본 제공 tooextend 수 있는 다른 U-SQL UDO입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-332">User-defined outputter is another U-SQL UDO that allows you tooextend built-in U-SQL functionality.</span></span> <span data-ttu-id="ed251-333">비슷한 toohello 추출기는 몇 가지 기본 제공 outputters 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-333">Similar toohello extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="ed251-334">*Outputters.Text()*: 텍스트 파일의 인코딩이 서로 다른 데이터 toodelimited를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-334">*Outputters.Text()*: Writes data toodelimited text files of different encodings.</span></span>
* <span data-ttu-id="ed251-335">*Outputters.Csv()*: 데이터 toocomma 구분 된 값의 인코딩이 서로 다르고 (CSV) 파일에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-335">*Outputters.Csv()*: Writes data toocomma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="ed251-336">*Outputters.Tsv()*: 데이터 tootab 구분 된 값의 인코딩이 서로 다르고 (TSV) 파일에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-336">*Outputters.Tsv()*: Writes data tootab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="ed251-337">사용자 지정 outputter 정의 된 사용자 지정 형식으로 toowrite 데이터를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-337">Custom outputter allows you toowrite data in a custom defined format.</span></span> <span data-ttu-id="ed251-338">이 작업을 수행 하는 hello에 대 한 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-338">This can be useful for hello following tasks:</span></span>

* <span data-ttu-id="ed251-339">데이터 toosemi 구조적 또는 비구조적 파일을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-339">Writing data toosemi-structured or unstructured files.</span></span>
* <span data-ttu-id="ed251-340">지원되지 않는 인코딩 데이터 쓰기</span><span class="sxs-lookup"><span data-stu-id="ed251-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="ed251-341">출력 데이터 수정 또는 사용자 지정 특성 추가</span><span class="sxs-lookup"><span data-stu-id="ed251-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="ed251-342">사용자 정의 outputter toodefine toocreate hello 필요 `IOutputter` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-342">toodefine user-defined outputter, we need toocreate hello `IOutputter` interface.</span></span>

<span data-ttu-id="ed251-343">다음은 기본 hello `IOutputter` 클래스 구현:</span><span class="sxs-lookup"><span data-stu-id="ed251-343">Following is hello base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="ed251-344">열/행 구분 기호, 인코딩 및 등 필요 toobe hello 클래스의 hello 생성자에 정의 된 같은 기준으로 모든 입력 매개 변수 toohello outputter 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-344">All input parameters toohello outputter, such as column/row delimiters, encoding, and so on, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="ed251-345">hello `IOutputter` 인터페이스에 대 한 정의 있어야 `void Output` 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-345">hello `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="ed251-346">hello 특성 `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` 원자성 파일 처리를 위해 필요에 따라 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-346">hello attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="ed251-347">자세한 내용은 hello 다음 세부 정보를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ed251-347">For more information, see hello following details.</span></span>

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

* <span data-ttu-id="ed251-348">`Output`은 각 입력 행에 대해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-348">`Output` is called for each input row.</span></span> <span data-ttu-id="ed251-349">Hello 반환 `IUnstructuredWriter output` 행 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-349">It returns hello `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="ed251-350">hello 생성자 클래스를 사용 하는 사용 되는 toopass 매개 변수 toohello 사용자 정의 outputter 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-350">hello Constructor class is used toopass parameters toohello user-defined outputter.</span></span>
* <span data-ttu-id="ed251-351">`Close`사용 toooptionally toorelease 비용이 많이 드는 상태를 재정의 하거나 hello 마지막 행이 기록 된 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-351">`Close` is used toooptionally override toorelease expensive state or determine when hello last row was written.</span></span>

<span data-ttu-id="ed251-352">**SqlUserDefinedOutputter** 특성으로 사용자 정의 outputter hello 형식을 등록 해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-352">**SqlUserDefinedOutputter** attribute indicates that hello type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="ed251-353">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-353">This class cannot be inherited.</span></span>

<span data-ttu-id="ed251-354">SqlUserDefinedOutputter는 사용자 정의 출력자 정의의 선택적 특성이며,</span><span class="sxs-lookup"><span data-stu-id="ed251-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="ed251-355">Toodefine hello AtomicFileProcessing 속성을 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-355">It's used toodefine hello AtomicFileProcessing property.</span></span>

* <span data-ttu-id="ed251-356">bool AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="ed251-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="ed251-357">**true**는 출력자에 원자성 출력 파일(JSON, XML 등)이 필요함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="ed251-358">**false**는 출력자에서 분할/분산 파일(CSV, SEQ 등)을 처리할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="ed251-359">hello 주 프로그래밍 기능 개체는 **행** 및 **출력**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-359">hello main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="ed251-360">hello **행** 개체는으로 출력 데이터를 사용 하는 tooenumerate `IRow` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-360">hello **row** object is used tooenumerate output data as `IRow` interface.</span></span> <span data-ttu-id="ed251-361">**출력** 는 사용 되는 tooset 출력 데이터 toohello 대상 파일이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-361">**Output** is used tooset output data toohello target file.</span></span>

<span data-ttu-id="ed251-362">hello 출력 통해 데이터에 액세스 hello `IRow` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-362">hello output data is accessed through hello `IRow` interface.</span></span> <span data-ttu-id="ed251-363">출력 데이터는 한 번에 한 행씩 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="ed251-364">hello IRow 인터페이스의 hello Get 메서드를 호출 하 여 hello 개별 값 열거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-364">hello individual values are enumerated by calling hello Get method of hello IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="ed251-365">개별 열 이름은 `row.Schema`를 호출하여 결정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="ed251-366">이 방법을 사용 하면 모든 메타 데이터 스키마에 대 한 유연한 outputter toobuild 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-366">This approach enables you toobuild a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="ed251-367">hello 출력 데이터가 쓰여집니다 toofile를 사용 하 여 `System.IO.StreamWriter`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-367">hello output data is written toofile by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="ed251-368">hello 스트림 매개 변수가 너무 설정 된`output.BaseStrea` 의 일부로 `IUnstructuredWriter output`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-368">hello stream parameter is set too`output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="ed251-369">각 행 반복 후 중요 한 tooflush hello 데이터 버퍼 toohello 파일 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-369">Note that it's important tooflush hello data buffer toohello file after each row iteration.</span></span> <span data-ttu-id="ed251-370">또한 hello `StreamWriter` hello 삭제 가능한 특성으로 사용 하도록 설정 (기본값)과 hello로 개체를 사용 해야 **를 사용 하 여** 키워드:</span><span class="sxs-lookup"><span data-stu-id="ed251-370">In addition, hello `StreamWriter` object must be used with hello Disposable attribute enabled (default) and with hello **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="ed251-371">그렇지 않으면 매번 반복 후에 Flush() 메서드를 명시적으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="ed251-372">다음 예제는 hello에이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-372">We show this in hello following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="ed251-373">사용자 정의 출력자의 머리글 및 바닥글 설정</span><span class="sxs-lookup"><span data-stu-id="ed251-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="ed251-374">tooset 헤더를 단일 반복 실행 흐름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-374">tooset a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="ed251-375">hello에 대 한 코드를 먼저 hello `if (isHeaderRow)` 블록이 한 번만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-375">hello code in hello first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="ed251-376">Hello 바닥글의 hello 참조 toohello 인스턴스를 사용 하 여 `System.IO.Stream` 개체 (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="ed251-376">For hello footer, use hello reference toohello instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="ed251-377">Hello 바닥글 hello hello의 close () 메서드를에서 작성 `IOutputter` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-377">Write hello footer in hello Close() method of hello `IOutputter` interface.</span></span>  <span data-ttu-id="ed251-378">(자세한 내용은 다음 예에서는 hello 참조).</span><span class="sxs-lookup"><span data-stu-id="ed251-378">(For more information, see hello following example.)</span></span>

<span data-ttu-id="ed251-379">다음의 사용자 정의 출력자에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-379">Following is an example of a user-defined outputter:</span></span>

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

<span data-ttu-id="ed251-380">U-SQL 기본 스크립트:</span><span class="sxs-lookup"><span data-stu-id="ed251-380">And U-SQL base script:</span></span>

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

<span data-ttu-id="ed251-381">HTML 출력자이며, 테이블 데이터로 HTML 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="ed251-382">U-SQL 기본 스크립트에서 출력자 호출</span><span class="sxs-lookup"><span data-stu-id="ed251-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="ed251-383">hello 기본 U-SQL 스크립트에서 사용자 지정 outputter toocall hello outputter 개체의 새 인스턴스를 hello 만든 toobe에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-383">toocall a custom outputter from hello base U-SQL script, hello new instance of hello outputter object has toobe created.</span></span>

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="ed251-384">기본 스크립트에 개체 tooavoid hello의 인스턴스를 만들지는 이전 예에서 같이 함수 래퍼를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-384">tooavoid creating an instance of hello object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

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

<span data-ttu-id="ed251-385">이 경우 원래 호출은 hello hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-385">In this case, hello original call looks like hello following:</span></span>

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="ed251-386">UDP(사용자 정의 처리기) 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-386">Use user-defined processors</span></span>
<span data-ttu-id="ed251-387">사용자 정의 프로세서 또는 UDP, 프로그래밍 기능을 적용 하 여 tooprocess hello 들어오는 행을 수 있는 U-SQL UDO의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you tooprocess hello incoming rows by applying programmability features.</span></span> <span data-ttu-id="ed251-388">UDP toocombine 열, 값을 수정 있으며 필요한 경우 새 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-388">UDP enables you toocombine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="ed251-389">기본적으로, tooprocess 행 집합 tooproduce 필요한 데이터 요소 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-389">Basically, it helps tooprocess a rowset tooproduce required data elements.</span></span>

<span data-ttu-id="ed251-390">UDP toodefine toocreate 필요는 `IProcessor` hello로 인터페이스 `SqlUserDefinedProcessor` UDP에 대 한 선택적 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-390">toodefine a UDP, we need toocreate an `IProcessor` interface with hello `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="ed251-391">이 인터페이스는 hello에 대 한 hello 정의 포함 해야 `IRow` hello 다음 예제와 같이 인터페이스 행 집합을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-391">This interface should contain hello definition for hello `IRow` interface rowset override, as shown in hello following example:</span></span>

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

<span data-ttu-id="ed251-392">**SqlUserDefinedProcessor** hello 종류를 사용자 정의 처리기로 등록 해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-392">**SqlUserDefinedProcessor** indicates that hello type should be registered as a user-defined processor.</span></span> <span data-ttu-id="ed251-393">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-393">This class cannot be inherited.</span></span>

<span data-ttu-id="ed251-394">hello SqlUserDefinedProcessor 특성은 **선택적** UDP 정의 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-394">hello SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="ed251-395">hello 주 프로그래밍 기능 개체는 **입력** 및 **출력**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-395">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="ed251-396">hello 입력된 개체에 사용 되는 tooenumerate 입력된 열 및 출력 및 hello 프로세서 작업의 결과로 tooset 출력 데이터는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-396">hello input object is used tooenumerate input columns and output, and tooset output data as a result of hello processor activity.</span></span>

<span data-ttu-id="ed251-397">입력된 열 열거형에 대 한 사용 하 여 hello `input.Get` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed251-397">For input columns enumeration, we use hello `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="ed251-398">hello에 대 한 매개 변수 `input.Get` 메서드는 hello의 일부로 전달 되는 열 `PRODUCE` hello 절 `PROCESS` hello U-SQL 기본 스크립트의 문.</span><span class="sxs-lookup"><span data-stu-id="ed251-398">hello parameter for `input.Get` method is a column that's passed as part of hello `PRODUCE` clause of hello `PROCESS` statement of hello U-SQL base script.</span></span> <span data-ttu-id="ed251-399">Toouse 필요 hello 올바른 데이터 여기에 입력 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ed251-399">We need toouse hello correct data type here.</span></span>

<span data-ttu-id="ed251-400">출력을 위해 hello를 사용 하 여 `output.Set` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed251-400">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="ed251-401">반드시 toonote 열과 hello로 정의 된 값에만 해당 사용자 지정 공급자를 출력 `output.Set` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-401">It's important toonote that custom producer only outputs columns and values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="ed251-402">호출 하 여 hello 프로세서 실제 출력 트리거될 `return output.AsReadOnly();`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-402">hello actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="ed251-403">다음은 처리기 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-403">Following is a processor example:</span></span>

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

<span data-ttu-id="ed251-404">이 사용 사례 시나리오에서는 hello 프로세서는 hello 기존 열-이 경우 "user"에서 대문자 및 "des"를 결합 하 여 "full_description" 라는 새 열을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-404">In this use-case scenario, hello processor is generating a new column called “full_description” by combining hello existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="ed251-405">또한 GUID 다시 생성 하 고 hello 원래 값과 새 GUID 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-405">It also regenerates a GUID and returns hello original and new GUID values.</span></span>

<span data-ttu-id="ed251-406">C# 중 메서드를 호출 hello 이전 예제의 보시 `output.Set` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-406">As you can see from hello previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="ed251-407">다음은 사용자 지정 처리기를 사용하는 기본 U-SQL 스크립트의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

## <a name="use-user-defined-appliers"></a><span data-ttu-id="ed251-408">사용자 정의 적용자 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-408">Use user-defined appliers</span></span>
<span data-ttu-id="ed251-409">U-SQL 사용자 정의 내용 쿼리의 hello 외부 테이블 식에서 반환 되는 각 행에 대 한 사용자 지정 C# tooinvoke 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-409">A U-SQL user-defined applier enables you tooinvoke a custom C# function for each row that's returned by hello outer table expression of a query.</span></span> <span data-ttu-id="ed251-410">hello 오른쪽 입력 hello 왼쪽된 입력 으로부터 각 행에 대해 계산 되 고 생성 되는 hello 행 hello 최종 출력에 대 한 조합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-410">hello right input is evaluated for each row from hello left input, and hello rows that are produced are combined for hello final output.</span></span> <span data-ttu-id="ed251-411">hello hello APPLY 연산자에서 생성 되는 열 목록에는 hello hello 왼쪽 및 오른쪽 입력 hello의 열 집합의 hello 조합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-411">hello list of columns that are produced by hello APPLY operator are hello combination of hello set of columns in hello left and hello right input.</span></span>

<span data-ttu-id="ed251-412">사용자 정의 적용 자 hello USQL 선택 식의 일부로 호출 되 고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-412">User-defined applier is being invoked as part of hello USQL SELECT expression.</span></span>

<span data-ttu-id="ed251-413">일반적인 hello toohello hello 다음과 같은 내용 적용 자 모양 사용자 지정을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-413">hello typical call toohello user-defined applier looks like hello following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="ed251-414">SELECT 식의 적용자 사용에 대한 자세한 내용은 [U-SQL SELECT: CROSS APPLY 및 OUTER APPLY에서 선택](https://msdn.microsoft.com/library/azure/mt621307.aspx)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed251-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="ed251-415">hello 사용자 정의 된 내용 적용 자 기본 클래스 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-415">hello user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="ed251-416">사용자 정의 적용 자 toodefine toocreate hello 필요 `IApplier` hello로 인터페이스 [`SqlUserDefinedApplier`] 사용자 지정 내용 적용 자 정의 대 한 선택적 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-416">toodefine a user-defined applier, we need toocreate hello `IApplier` interface with hello [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="ed251-417">적용 hello 외부 테이블의 각 행에 대해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-417">Apply is called for each row of hello outer table.</span></span> <span data-ttu-id="ed251-418">Hello 반환 `IUpdatableRow` 행 집합을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-418">It returns hello `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="ed251-419">hello 생성자 클래스는 사용 되는 toopass 매개 변수 toohello 사용자 정의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-419">hello Constructor class is used toopass parameters toohello user-defined applier.</span></span>

<span data-ttu-id="ed251-420">**SqlUserDefinedApplier** hello 형식을 사용자 정의 내용으로 등록 해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-420">**SqlUserDefinedApplier** indicates that hello type should be registered as a user-defined applier.</span></span> <span data-ttu-id="ed251-421">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-421">This class cannot be inherited.</span></span>

<span data-ttu-id="ed251-422">**SqlUserDefinedApplier**는 사용자 정의 적용자 정의의 **선택 사항**입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="ed251-423">hello 주 프로그래밍 개체는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-423">hello main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="ed251-424">입력 행 집합은 `IRow` 입력으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="ed251-425">hello 출력 행으로 생성 됩니다 `IUpdatableRow` 출력 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-425">hello output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="ed251-426">Hello를 호출 하 여 개별 열 이름을 확인할 수 있습니다 `IRow` 스키마 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed251-426">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="ed251-427">들어오는 hello에서 tooget hello 실제 데이터 값 `IRow`의 hello get () 메서드 사용 `IRow` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-427">tooget hello actual data values from hello incoming `IRow`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="ed251-428">또는 hello 스키마 열 이름을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ed251-428">Or we use hello schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="ed251-429">hello 출력 값을 설정 해야 `IUpdatableRow` 출력:</span><span class="sxs-lookup"><span data-stu-id="ed251-429">hello output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="ed251-430">사용자 지정 내용 적용 자 사용 열과 값으로 정의 된 출력만 중요 한 toounderstand는 `output.Set` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-430">It is important toounderstand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="ed251-431">호출 하 여 hello 실제 출력 트리거될 `yield return output.AsReadOnly();`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-431">hello actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="ed251-432">toohello 생성자 hello 사용자 정의 내용 적용 자 매개 변수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-432">hello user-defined applier parameters can be passed toohello constructor.</span></span> <span data-ttu-id="ed251-433">내용은 toobe 기본 U-SQL 스크립트에 hello 내용 적용 자 호출 하는 동안 정의 해야 하는 열 수가 달라를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-433">Applier can return a variable number of columns that need toobe defined during hello applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="ed251-434">사용자 정의 hello 내용 적용 자 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-434">Here is hello user-defined applier example:</span></span>

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

<span data-ttu-id="ed251-435">다음은이 사용자 지정 내용에 대 한 hello 기본 U-SQL 스크립트:</span><span class="sxs-lookup"><span data-stu-id="ed251-435">Following is hello base U-SQL script for this user-defined applier:</span></span>

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

<span data-ttu-id="ed251-436">이 사용 사례 시나리오에서 사용자 지정 내용 적용 자 카드로 hello 자동차에 대 한 쉼표로 구분 된 값이 파서 함 대 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for hello car fleet properties.</span></span> <span data-ttu-id="ed251-437">hello 입력된 파일 행 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-437">hello input file rows look like hello following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="ed251-438">이 파일은 제조업체 모델 등의 자동차 속성을 포함하는 속성 열이 탭으로 분리된 일반적인 TSV 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="ed251-439">이러한 속성은 구문 분석 된 toohello 테이블 열 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-439">Those properties must be parsed toohello table columns.</span></span> <span data-ttu-id="ed251-440">제공 하는 hello 적용 자 toogenerate를 동적 다양 한 속성이 hello에 결과 행 집합을 전달 되는 hello 매개 변수를 기반 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-440">hello applier that's provided also enables you toogenerate a dynamic number of properties in hello result rowset, based on hello parameter that's passed.</span></span> <span data-ttu-id="ed251-441">모든 속성을 생성하거나 특정 속성 집합만 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="ed251-442">사용자 정의 적용 자 hello 내용 적용 자 개체의 새 인스턴스로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-442">hello user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="ed251-443">또는 hello 래퍼 팩터리 메서드 호출으로:</span><span class="sxs-lookup"><span data-stu-id="ed251-443">Or with hello invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="ed251-444">사용자 정의 결합자 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-444">Use user-defined combiners</span></span>
<span data-ttu-id="ed251-445">UDC, 또는 사용자 지정 결합 하면 왼쪽 및 오른쪽 행 집합 으로부터, 사용자 지정 논리에 따라 toocombine 행.</span><span class="sxs-lookup"><span data-stu-id="ed251-445">User-defined combiner, or UDC, enables you toocombine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="ed251-446">UDC는 COMBINE 식으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="ed251-447">Hello 두 hello 입력된 행 집합에 대 한 필요한 정보를 제공 하는 hello 결합 되어 감사가 만들어집니다 식으로 호출 되는 조합 기, 열을 그룹화, hello hello 예상 결과 스키마 및 추가 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-447">A combiner is being invoked with hello COMBINE expression that provides hello necessary information about both hello input rowsets, hello grouping columns, hello expected result schema, and additional information.</span></span>

<span data-ttu-id="ed251-448">기본 U-SQL 스크립트에 결합 toocall 구문 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-448">toocall a combiner in a base U-SQL script, we use hello following syntax:</span></span>

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

<span data-ttu-id="ed251-449">자세한 내용은 [COMBINE 식(U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed251-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="ed251-450">사용자 지정 결합 toodefine toocreate hello 필요 `ICombiner` hello로 인터페이스 [`SqlUserDefinedCombiner`] 사용자 지정 결합 정의 대 한 선택적 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-450">toodefine a user-defined combiner, we need toocreate hello `ICombiner` interface with hello [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="ed251-451">기본 `ICombiner` 클래스 정의:</span><span class="sxs-lookup"><span data-stu-id="ed251-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="ed251-452">사용자 지정 구현을 hello는 `ICombiner` 인터페이스에 대 한 hello 정의 포함 해야는 `IEnumerable<IRow>` 재정의 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-452">hello custom implementation of an `ICombiner` interface should contain hello definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="ed251-453">hello **SqlUserDefinedCombiner** 특성을 사용자 지정 결합으로 hello 형식을 등록 해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-453">hello **SqlUserDefinedCombiner** attribute indicates that hello type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="ed251-454">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-454">This class cannot be inherited.</span></span>

<span data-ttu-id="ed251-455">**SqlUserDefinedCombiner** 사용 되는 toodefine hello 결합 모드 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-455">**SqlUserDefinedCombiner** is used toodefine hello Combiner mode property.</span></span> <span data-ttu-id="ed251-456">사용자 정의 결합자 정의의 선택적 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="ed251-457">CombinerMode Mode</span><span class="sxs-lookup"><span data-stu-id="ed251-457">CombinerMode     Mode</span></span>

<span data-ttu-id="ed251-458">CombinerMode enum hello 다음 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-458">CombinerMode enum can take hello following values:</span></span>

* <span data-ttu-id="ed251-459">전체 (0) 각 출력 행의 모든 hello 입력된 행에 따라 달라질 왼쪽과 오른쪽 hello을 동일한 키 값.</span><span class="sxs-lookup"><span data-stu-id="ed251-459">Full  (0) Every output row potentially depends on all hello input rows from left and right       with hello same key value.</span></span>

* <span data-ttu-id="ed251-460">왼쪽 (1) hello 왼쪽에서 단일 입력된 행에 모든 출력 행에 따라 달라 집니다 (및 잠재적으로 모든 행 hello hello로 오른쪽에서 동일한 키 값).</span><span class="sxs-lookup"><span data-stu-id="ed251-460">Left  (1) Every output row depends on a single input row from hello left (and potentially all rows       from hello right with hello same key value).</span></span>

* <span data-ttu-id="ed251-461">오른쪽 (2) hello 오른쪽에서 단일 입력된 행에 모든 출력 행에 따라 달라 집니다 (및 잠재적으로 모든 행 hello로 hello 왼쪽에서 동일한 키 값).</span><span class="sxs-lookup"><span data-stu-id="ed251-461">Right (2)     Every output row depends on a single input row from hello right (and potentially all rows       from hello left with hello same key value).</span></span>

* <span data-ttu-id="ed251-462">왼쪽과 오른쪽을 hello에서 모든 출력 행을 단일 입력에 따라 달라 집니다 (3) 내부 행 동일한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-462">Inner (3) Every output row depends on a single input row from left and right with hello same value.</span></span>

<span data-ttu-id="ed251-463">예: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="ed251-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="ed251-464">hello 주 프로그래밍 기능 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-464">hello main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="ed251-465">입력 행 집합은 **left** 및 **right** `IRowset` 형식의 인터페이스로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="ed251-466">두 행 집합은 처리하기 위해 모두 열거되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="ed251-467">하므로 tooenumerate 있어야 하 고 필요한 경우 캐시를 한 번 각 인터페이스를 열거할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-467">You can only enumerate each interface once, so we have tooenumerate and cache it if necessary.</span></span>

<span data-ttu-id="ed251-468">캐싱을 위해 LINQ 쿼리 실행의 결과로 List\<T\> 형식의 메모리 구조체를 만들 수 있습니다(구체적으로 List<`IRow`>).</span><span class="sxs-lookup"><span data-stu-id="ed251-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="ed251-469">hello 익명의 데이터 형식으로 열거 하는 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-469">hello anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="ed251-470">참조 [tooLINQ 쿼리 소개 (C#)](https://msdn.microsoft.com/library/bb397906.aspx) LINQ 쿼리에 대 한 자세한 내용은 및 [IEnumerable\<T\> 인터페이스](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) IEnumerable에대한자세한내용은\<T\> 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-470">See [Introduction tooLINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="ed251-471">들어오는 hello에서 tooget hello 실제 데이터 값 `IRowset`의 hello get () 메서드 사용 `IRow` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-471">tooget hello actual data values from hello incoming `IRowset`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="ed251-472">Hello를 호출 하 여 개별 열 이름을 확인할 수 있습니다 `IRow` 스키마 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed251-472">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="ed251-473">또는 hello 스키마 열 이름을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ed251-473">Or by using hello schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="ed251-474">LINQ 통한 일반 열거형 hello hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-474">hello general enumeration with LINQ looks like hello following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="ed251-475">두 행 집합을 열거 하는 경우, 한 후 모든 행을 tooloop을 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-475">After enumerating both rowsets, we are going tooloop through all rows.</span></span> <span data-ttu-id="ed251-476">Hello 왼쪽된 행 집합의 각 행에 대해 하겠습니다 toofind 우리의 조합 기의 hello 조건을 만족 하는 모든 행입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-476">For each row in hello left rowset, we are going toofind all rows that satisfy hello condition of our combiner.</span></span>

<span data-ttu-id="ed251-477">hello 출력 값을 설정 해야 `IUpdatableRow` 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-477">hello output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="ed251-478">hello 실제 출력 너무 호출에 의해 트리거되는`yield return output.AsReadOnly();`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-478">hello actual output is triggered by calling too`yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="ed251-479">다음은 결합자 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="ed251-480">이 사용 사례 시나리오 hello 소매 업체에 대 한 분석 보고서 작성.</span><span class="sxs-lookup"><span data-stu-id="ed251-480">In this use-case scenario, we are building an analytics report for hello retailer.</span></span> <span data-ttu-id="ed251-481">hello 목표는 특정 시간 프레임 내에서 일반 소매점 hello 통해 보다 빠르게 hello 웹 사이트를 통해 비용 20000 이상 모든 제품 판매 toofind입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-481">hello goal is toofind all products that cost more than $20,000 and that sell through hello website faster than through hello regular retailer within a certain time frame.</span></span>

<span data-ttu-id="ed251-482">Hello 기본 U-SQL 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-482">Here is hello base U-SQL script.</span></span> <span data-ttu-id="ed251-483">일반 조인을는 조합 기 간의 hello 논리를 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-483">You can compare hello logic between a regular JOIN and a combiner:</span></span>

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

<span data-ttu-id="ed251-484">사용자 정의 조합 기 hello 내용 적용 자 개체의 새 인스턴스로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-484">A user-defined combiner can be called as a new instance of hello applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="ed251-485">또는 hello 래퍼 팩터리 메서드 호출으로:</span><span class="sxs-lookup"><span data-stu-id="ed251-485">Or with hello invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="ed251-486">사용자 정의 리듀서 사용</span><span class="sxs-lookup"><span data-stu-id="ed251-486">Use user-defined reducers</span></span>

<span data-ttu-id="ed251-487">U-SQL 사용 하면 C#에서 사용자 지정 행 집합 이경소켓 toowrite hello 사용자 정의 연산자 확장 프레임 워크를 사용 하 고 IReducer 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-487">U-SQL enables you toowrite custom rowset reducers in C# by using hello user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="ed251-488">리 듀 서 사용자 정의 또는 UDR, 데이터 추출 (가져오기) 하는 동안 사용 되는 tooeliminate 불필요 한 행을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-488">User-defined reducer, or UDR, can be used tooeliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="ed251-489">또한 고 될 수 toomanipulate 사용 되는 행과 열을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-489">It also can be used toomanipulate and evaluate rows and columns.</span></span> <span data-ttu-id="ed251-490">프로그래밍 논리를 기반를 정의할 수도 있습니다 행 toobe 추출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-490">Based on programmability logic, it can also define which rows need toobe extracted.</span></span>

<span data-ttu-id="ed251-491">toocreate 필요 toodefine UDR 클래스는 `IReducer` 인터페이스는 선택적으로 `SqlUserDefinedReducer` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-491">toodefine a UDR class, we need toocreate an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="ed251-492">이 클래스 인터페이스 hello에 대 한 정의 포함 해야 `IEnumerable` 행 집합 인터페이스를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-492">This class interface should contain a definition for hello `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="ed251-493">hello **SqlUserDefinedReducer** 특성으로 사용자 정의 리 듀 서 hello 형식을 등록 해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-493">hello **SqlUserDefinedReducer** attribute indicates that hello type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="ed251-494">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-494">This class cannot be inherited.</span></span>
<span data-ttu-id="ed251-495">**SqlUserDefinedReducer**는 UDR(사용자 정의 리듀서) 정의의 선택적 특성이며,</span><span class="sxs-lookup"><span data-stu-id="ed251-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="ed251-496">Toodefine IsRecursive 속성을 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-496">It's used toodefine IsRecursive property.</span></span>

* <span data-ttu-id="ed251-497">bool IsRecursive</span><span class="sxs-lookup"><span data-stu-id="ed251-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="ed251-498">**true**는 idempotent 유형의 리듀서인지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="ed251-499">hello 주 프로그래밍 기능 개체는 **입력** 및 **출력**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-499">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="ed251-500">hello 입력 개체가 사용 되는 tooenumerate 입력된 행입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-500">hello input object is used tooenumerate input rows.</span></span> <span data-ttu-id="ed251-501">출력은 감소 활동의 결과로 사용 되는 tooset 출력 행입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-501">Output is used tooset output rows as a result of reducing activity.</span></span>

<span data-ttu-id="ed251-502">입력된 행 열거형에 대 한 사용 하 여 hello `Row.Get` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed251-502">For input rows enumeration, we use hello `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="ed251-503">hello에 대 한 매개 변수를 hello `Row.Get` 메서드는 hello의 일부로 전달 되는 열 `PRODUCE` hello의 클래스 `REDUCE` hello U-SQL 기본 스크립트의 문.</span><span class="sxs-lookup"><span data-stu-id="ed251-503">hello parameter for hello `Row.Get` method is a column that's passed as part of hello `PRODUCE` class of hello `REDUCE` statement of hello U-SQL base script.</span></span> <span data-ttu-id="ed251-504">Toouse 필요 hello 올바른 데이터 형식을 여기 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-504">We need toouse hello correct data type here as well.</span></span>

<span data-ttu-id="ed251-505">출력을 위해 hello를 사용 하 여 `output.Set` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed251-505">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="ed251-506">사용자 지정 리 듀 서 지 원하는 유일한 출력 값으로 정의 된 hello 중요 toounderstand는 `output.Set` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-506">It is important toounderstand that custom reducer only outputs values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="ed251-507">호출 하 여 hello 실제 리 듀 서 출력 트리거될 `yield return output.AsReadOnly();`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-507">hello actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="ed251-508">다음은 리듀서 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="ed251-509">이 사용 사례 시나리오에서는 hello 리 듀 서 빈 사용자 이름 가진 행을 건너뛰는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-509">In this use-case scenario, hello reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="ed251-510">행 집합의 각 행에 대해이 클래스는 필요한 각 열을 읽은 다음 hello 사용자 이름의 hello 길이 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-510">For each row in rowset, it reads each required column, then evaluates hello length of hello user name.</span></span> <span data-ttu-id="ed251-511">사용자 이름의 값 길이 0 보다 큰 경우에 hello 실제 행을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-511">It outputs hello actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="ed251-512">다음은 사용자 지정 리듀서를 사용하는 기본 U-SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="ed251-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
