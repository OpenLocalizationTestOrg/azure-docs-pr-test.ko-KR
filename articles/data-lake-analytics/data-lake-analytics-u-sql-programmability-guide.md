---
title: "Azure Data Lake에 대한 U-SQL 프로그래밍 기능 가이드 | Microsoft Docs"
description: "클라우드 기반 빅 데이터 플랫폼을 만들 수 있는 Azure Data Lake의 서비스 집합에 대해 알아봅니다."
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
ms.openlocfilehash: e4e298475d7be7d51c8bd55be498371ed6ce77a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="438d1-103">U-SQL 프로그래밍 기능 가이드</span><span class="sxs-lookup"><span data-stu-id="438d1-103">U-SQL programmability guide</span></span>

<span data-ttu-id="438d1-104">U-SQL은 빅 데이터 유형의 워크로드를 위해 설계된 쿼리 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="438d1-105">U-SQL의 고유한 기능 중 하나는 SQL과 같은 선언적 언어와 C#에서 제공하는 확장성 및 프로그래밍 기능을 결합한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-105">One of the unique features of U-SQL is the combination of the SQL-like declarative language with the extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="438d1-106">이 가이드에서는 C#에서 사용할 수 있는 U-SQL 언어의 확장성과 프로그래밍 기능을 집중적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-106">In this guide, we concentrate on the extensibility and programmability of the U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="438d1-107">요구 사항</span><span class="sxs-lookup"><span data-stu-id="438d1-107">Requirements</span></span>

<span data-ttu-id="438d1-108">[Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="438d1-109">U-SQL 시작</span><span class="sxs-lookup"><span data-stu-id="438d1-109">Get started with U-SQL</span></span>  

<span data-ttu-id="438d1-110">다음 U-SQL 스크립트를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-110">Let’s look at the following U-SQL script:</span></span>

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

<span data-ttu-id="438d1-111">@a라는 RowSet를 정의하고 @a를 통해 @results라는 RowSet를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="438d1-112">U-SQL 스크립트의 C# 형식 및 식</span><span class="sxs-lookup"><span data-stu-id="438d1-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="438d1-113">U-SQL 식은 `AND`, `OR` 및 `NOT`과 같은 U-SQL 논리 연산자와 결합된 C# 식입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="438d1-114">U-SQL 식은 SELECT, EXTRACT, WHERE, HAVING, GROUP BY 및 DECLARE와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="438d1-115">예를 들어 다음 스크립트는 SELECT 절의 DateTime 문자열 값을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-115">For example, the following script parses a string a DateTime value in the SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="438d1-116">다음 스크립트는 DECLARE 문의 DateTime 문자열 값을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-116">The following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="438d1-117">데이터 형식 변환에 C# 식 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="438d1-118">다음 예제는 C# 식을 사용하여 datetime 데이터 변환을 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-118">The following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="438d1-119">이 특정 시나리오에서 datetime 문자열 데이터는 자정 00:00:00 시간 표기법을 사용하는 표준 datetime으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-119">In this particular scenario, string datetime data is converted to standard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="438d1-120">오늘 날짜에 C# 식 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="438d1-121">오늘 날짜를 가져오려면 다음 C# 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-121">To pull today’s date, we can use the following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="438d1-122">다음은 스크립트에서 이 식을 사용하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-122">Here's an example of how to use this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="438d1-123">.NET 어셈블리 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-123">Using .NET assemblies</span></span>
<span data-ttu-id="438d1-124">U-SQL 확장성 모델은 사용자 지정 코드를 추가할 수 있는 기능에 크게 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-124">U-SQL’s extensibility model relies heavily on the ability to add custom code.</span></span> <span data-ttu-id="438d1-125">현재 U-SQL은 사용자 고유의 Microsoft .NET 기반 코드(특히 C#)를 손쉽게 추가할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-125">Currently, U-SQL provides you with easy ways to add your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="438d1-126">하지만 다른 .NET 언어(예: VB.NET 또는 F#)로 작성된 사용자 지정 코드를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="438d1-127">.NET 어셈블리 등록</span><span class="sxs-lookup"><span data-stu-id="438d1-127">Register a .NET assembly</span></span>

<span data-ttu-id="438d1-128">CREATE ASSEMBLY 문을 사용하여 U-SQL 데이터베이스에 .NET 어셈블리를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-128">Use the CREATE ASSEMBLY statement to place a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="438d1-129">데이터베이스에 어셈블리가 배치되면 U-SQL 스크립트가 REFERENCE ASSEMBLY 문을 통해 이러한 어셈블리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using the REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="438d1-130">다음 코드는 어셈블리를 등록하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-130">The following code shows how to register an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="438d1-131">다음 코드는 어셈블리를 참조하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-131">The following code shows how to reference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="438d1-132">이 항목을 더 자세히 설명하는 [어셈블리 등록 지침](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="438d1-132">Consult the [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="438d1-133">어셈블리 버전 관리 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-133">Use assembly versioning</span></span>
<span data-ttu-id="438d1-134">현재 U-SQL은 .NET Framework 버전 4.5를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-134">Currently, U-SQL uses the .NET Framework version 4.5.</span></span> <span data-ttu-id="438d1-135">따라서 자신의 어셈블리가 해당 런타임 버전과 호환되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-135">So ensure that your own assemblies are compatible with that version of the runtime.</span></span>

<span data-ttu-id="438d1-136">앞에서 언급했듯이 U-SQL은 64비트(x64) 형식 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="438d1-137">따라서 코드가 x64에서 실행되도록 컴파일되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-137">So make sure that your code is compiled to run on x64.</span></span> <span data-ttu-id="438d1-138">그렇지 않으면 앞에서 설명한 잘못된 형식 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-138">Otherwise you get the incorrect format error shown earlier.</span></span>

<span data-ttu-id="438d1-139">업로드된 각 어셈블리 DLL, 리소스 파일(예: 다양한 런타임), 네이티브 어셈블리 또는 구성 파일의 크기는 최대 400MB입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="438d1-140">DEPLOY RESOURCE를 통해 또는 참조 어셈블리를 통해 배포된 리소스 및 추가 파일의 총 크기는 3GB를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-140">The total size of deployed resources, either via DEPLOY RESOURCE or via references to assemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="438d1-141">마지막으로 U-SQL 데이터베이스마다 지정된 어셈블리 버전을 하나만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="438d1-142">예를 들어 NewtonSoft Json.Net 라이브러리의 버전 7과 버전 8이 모두 필요하면 서로 다른 두 데이터베이스에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-142">For example, if you need both version 7 and version 8 of the NewtonSoft Json.Net library, you need to register them in two different databases.</span></span> <span data-ttu-id="438d1-143">또한 각 스크립트는 지정된 어셈블리 DLL의 한 가지 버전만 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-143">Furthermore, each script can only refer to one version of a given assembly DLL.</span></span> <span data-ttu-id="438d1-144">이러한 점에서 U-SQL은 C# 어셈블리 관리 및 버전 관리 의미 체계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-144">In this respect, U-SQL follows the C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="438d1-145">UDF(사용자 정의 함수) 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="438d1-146">U-SQL UDF(사용자 정의 함수)는 매개 변수를 받아들이고, 작업(예: 복잡한 계산)을 수행하며, 해당 작업의 결과를 값으로 반환하는 프로그래밍 루틴입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return the result of that action as a value.</span></span> <span data-ttu-id="438d1-147">UDF의 반환 값은 단지 단일 스칼라일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-147">The return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="438d1-148">U-SQL UDF는 다른 C# 스칼라 함수와 같이 U-SQL 기본 스크립트에서 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="438d1-149">U-SQL 사용자 정의 함수는 **public** 및 **static**으로 초기화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="438d1-150">먼저 UDF를 만드는 간단한 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-150">First let’s look at the simple example of creating a UDF.</span></span>

<span data-ttu-id="438d1-151">이 사용 사례 시나리오에서는 특정 사용자에 대한 첫 번째 로그인의 회계 분기 및 회계 월을 포함하는 회계 기간을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-151">In this use-case scenario, we need to determine the fiscal period, including the fiscal quarter and fiscal month of the first sign-in for the specific user.</span></span> <span data-ttu-id="438d1-152">시나리오에서 해당 연도의 첫 번째 회계 월은 6월입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-152">The first fiscal month of the year in our scenario is June.</span></span>

<span data-ttu-id="438d1-153">회계 기간을 계산하기 위해 다음 C# 함수를 도입합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-153">To calculate fiscal period, we introduce the following C# function:</span></span>

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

<span data-ttu-id="438d1-154">단순히 회계 월과 분기를 계산하고 문자열 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="438d1-155">첫 번째 회계 분기의 첫 번째 월인 6월에 대해서는 "Q1:P1"을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-155">For June, the first month of the first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="438d1-156">7월에 대해서는 "Q1:P2"를 사용하고 이런 방식으로 계속 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="438d1-157">이것은 U-SQL 프로젝트에 사용할 일반 C# 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-157">This is a regular C# function that we are going to use in our U-SQL project.</span></span>

<span data-ttu-id="438d1-158">이 시나리오의 코드 숨김 섹션은 다음과 같은 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-158">Here is how the code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="438d1-159">이제 기본 U-SQL 스크립트에서 이 함수를 호출할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-159">Now we are going to call this function from the base U-SQL script.</span></span> <span data-ttu-id="438d1-160">이렇게 하려면 함수에 대해 네임스페이스를 포함하는 정규화된 이름을 제공해야 합니다. 이 경우 NameSpace.Class.Function(매개 변수)입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-160">To do this, we have to provide a fully qualified name for the function, including the namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="438d1-161">다음은 실제 U-SQL 기본 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-161">Following is the actual U-SQL base script:</span></span>

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
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="438d1-162">다음은 스크립트 실행의 출력 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-162">Following is the output file of the script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="438d1-163">이 예제에서는 U-SQL에서 인라인 UDF를 간단하게 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="438d1-164">UDF 호출 사이 상태 유지</span><span class="sxs-lookup"><span data-stu-id="438d1-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="438d1-165">U-SQL C# 프로그래밍 기능 개체는 코드 숨김 전역 변수를 통한 상호 작용을 활용하여 더 정교해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through the code-behind global variables.</span></span> <span data-ttu-id="438d1-166">다음과 같은 비즈니스 사용 사례 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-166">Let’s look at the following business use-case scenario.</span></span>

<span data-ttu-id="438d1-167">대규모 조직에서는 사용자가 다양한 내부 응용 프로그램 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="438d1-168">여기에는 Microsoft Dynamics CRM, PowerBI 등이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="438d1-169">고객을 위해 사용자가 다양한 응용 프로그램 사이를 전환하는 방법, 사용 추세 등에 대한 원격 분석을 적용하는 것이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-169">Customers might want to apply a telemetry analysis of how users switch between different applications, what the usage trends are, and so on.</span></span> <span data-ttu-id="438d1-170">비즈니스의 목표는 응용 프로그램 사용을 최적화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-170">The goal for the business is to optimize application usage.</span></span> <span data-ttu-id="438d1-171">다양한 응용 프로그램이나 특정 로그인 루틴을 결합하는 것이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-171">They also might want to combine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="438d1-172">이러한 목표를 달성하려면 세션 ID 및 마지막으로 발생한 세션 간의 지연 시간을 판단해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-172">To achieve this goal, we have to determine session IDs and lag time between the last session that occurred.</span></span>

<span data-ttu-id="438d1-173">이전 로그인을 찾은 다음 이 로그인을 동일한 응용 프로그램에 생성되는 모든 세션에 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-173">We need to find a previous sign-in and then assign this sign-in to all sessions that are being generated to the same application.</span></span> <span data-ttu-id="438d1-174">첫 번째 과제는 U-SQL 기본 스크립트를 사용하면 LAG 함수로 이미 계산된 열에 계산을 적용할 수 없다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-174">The first challenge is that U-SQL base script doesn't allow us to apply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="438d1-175">두 번째 과제는 같은 기간 내의 모든 세션에 대해 특정 세션을 유지해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-175">The second challenge is that we have to keep the specific session for all sessions within the same time period.</span></span>

<span data-ttu-id="438d1-176">이 문제를 해결하기 위해 코드 숨김 섹션 내에 전역 변수 `static public string globalSession;`을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-176">To solve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="438d1-177">이 전역 변수는 스크립트를 실행하는 동안 전체 행 집합에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-177">This global variable is applied to the entire rowset during our script execution.</span></span>

<span data-ttu-id="438d1-178">다음은 U-SQL 프로그램의 코드 숨김 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-178">Here is the code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="438d1-179">이 예제는 `getStampUserSession` 함수 내에 사용되고 Session 매개 변수가 변경될 때마다 다시 초기화되는 전역 변수 `static public string globalSession;`을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-179">This example shows the global variable `static public string globalSession;` used inside the `getStampUserSession` function and getting reinitialized each time the Session parameter is changed.</span></span>

<span data-ttu-id="438d1-180">U-SQL 기본 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-180">The U-SQL base script is as follows:</span></span>

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
    TO @out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="438d1-181">여기서 `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` 함수는 두 번째 메모리 행 집합을 계산하는 동안 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during the second memory rowset calculation.</span></span> <span data-ttu-id="438d1-182">`UserSessionTimestamp` 열을 전달하고 `UserSessionTimestamp`가 변경될 때까지 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-182">It passes the `UserSessionTimestamp` column and returns the value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="438d1-183">출력 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-183">The output file is as follows:</span></span>

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

<span data-ttu-id="438d1-184">이 예제는 전체 메모리 행 집합에 적용된 코드 숨김 섹션 내부에 전역 변수를 사용하는 보다 세밀한 사용 사례 시나리오를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied to the entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="438d1-185">UDT(사용자 정의 형식) 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="438d1-186">UDT(사용자 정의 형식)는 U-SQL의 또 다른 프로그래밍 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="438d1-187">U-SQL UDT는 일반 C# 사용자 정의 형식처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="438d1-188">C#는 기본 제공 및 사용자 지정 UDT를 사용할 수 있는 강력한 형식의 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-188">C# is a strongly typed language that allows the use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="438d1-189">U-SQL은 UDT가 행 집합의 꼭짓점 간에 전달되는 동안 임의의 UDT를 암시적으로 직렬화하거나 역직렬화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when the UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="438d1-190">다시 말해 사용자가 IFormatter 인터페이스를 사용하여 명시적인 포맷터를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-190">This means that the user has to provide an explicit formatter by using the IFormatter interface.</span></span> <span data-ttu-id="438d1-191">이렇게 하면 U-SQL에 UDT에 대한 직렬화 및 역직렬화 메서드가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-191">This provides U-SQL with the serialize and de-serialize methods for the UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="438d1-192">U-SQL의 기본 제공 추출기 및 출력기는 현재 IFormatter 집합이 있는 파일 사이에서 UDT 데이터를 직렬화하거나 역직렬화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data to or from files even with the IFormatter set.</span></span> <span data-ttu-id="438d1-193">따라서 OUTPUT 문이 있는 파일에 UDT 데이터를 작성하는 경우 또는 추출기로 UDT 데이터를 읽는 경우 UDT 데이터를 문자열 또는 바이트 배열로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-193">So when you're writing UDT data to a file with the OUTPUT statement, or reading it with an extractor, you have to pass it as a string or byte array.</span></span> <span data-ttu-id="438d1-194">그런 다음 직렬화 및 역직렬화 코드(즉 UDT의 ToString() 메서드)를 명시적으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-194">Then you call the serialization and deserialization code (that is, the UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="438d1-195">반면 사용자 정의 추출기 및 출력자는 UDT를 읽고 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-195">User-defined extractors and outputters, on the other hand, can read and write UDTs.</span></span>

<span data-ttu-id="438d1-196">다음과 같이 (이전 SELECT의 외부에 있는) EXTRACTOR 또는 OUTPUTTER에서 UDT를 사용하려고 시도하면:</span><span class="sxs-lookup"><span data-stu-id="438d1-196">If we try to use UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="438d1-197">다음 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-197">We receive the following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used to output column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how to serialize this type, or call a serialization method on the type in
the preceding SELECT.   C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="438d1-198">Outptutter에서 UDT를 사용하려면 ToString() 메서드를 사용하여 문자열로 직렬화하거나 사용자 지정 Outputter를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-198">To work with UDT in outputter, we either have to serialize it to string with the ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="438d1-199">UDT는 현재 GROUP BY에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="438d1-200">GROUP BY에 UDT를 사용하면 다음과 같은 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-200">If UDT is used in GROUP BY, the following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want to use with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="438d1-201">UDT를 정의하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-201">To define a UDT, we have to:</span></span>

* <span data-ttu-id="438d1-202">다음 네임스페이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-202">Add the following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="438d1-203">UDT 인터페이스에 필요한 `Microsoft.Analytics.Interfaces`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-203">Add `Microsoft.Analytics.Interfaces`, which is required for the UDT interfaces.</span></span> <span data-ttu-id="438d1-204">더불어 `System.IO`가 IFormatter 인터페이스를 정의하는 데 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-204">In addition, `System.IO` might be needed to define the IFormatter interface.</span></span>

* <span data-ttu-id="438d1-205">SqlUserDefinedType 특성을 사용하여 사용자 정의 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="438d1-206">**SqlUserDefinedType**은 어셈블리의 형식 정의를 U-SQL UDT로 표시하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-206">**SqlUserDefinedType** is used to mark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="438d1-207">특성의 속성에는 UDT의 물리적 특성이 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-207">The properties on the attribute reflect the physical characteristics of the UDT.</span></span> <span data-ttu-id="438d1-208">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-208">This class cannot be inherited.</span></span>

<span data-ttu-id="438d1-209">SqlUserDefinedType은 UDT 정의에 필요한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="438d1-210">클래스 생성자:</span><span class="sxs-lookup"><span data-stu-id="438d1-210">The constructor of the class:</span></span>  

* <span data-ttu-id="438d1-211">SqlUserDefinedTypeAttribute(형식 포맷터)</span><span class="sxs-lookup"><span data-stu-id="438d1-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="438d1-212">형식 포맷터: UDT 포맷터를 정의하는 필수 매개 변수이며 구체적으로 `IFormatter` 인터페이스 형식이 여기로 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-212">Type formatter: Required parameter to define an UDT formatter--specifically, the type of the `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="438d1-213">다음 예제와 같이, 일반적인 UDT도 IFormatter 인터페이스에 대한 정의가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-213">Typical UDT also requires definition of the IFormatter interface, as shown in the following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="438d1-214">`IFormatter` 인터페이스는 \<typeparamref name="T">의 루트 형식으로 개체 그래프를 직렬화하고 역직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-214">The `IFormatter` interface serializes and de-serializes an object graph with the root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="438d1-215">\<typeparamref name="T"> - 직렬화/역직렬화할 개체 그래프의 루트 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-215">\<typeparam name="T">The root type for the object graph to serialize and de-serialize.</span></span>

* <span data-ttu-id="438d1-216">**Deserialize**: 제공된 스트림의 데이터를 역직렬화하고 개체 그래프를 다시 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-216">**Deserialize**: De-serializes the data on the provided stream and reconstitutes the graph of objects.</span></span>

* <span data-ttu-id="438d1-217">**Serialize**: 제공된 스트림에 지정된 루트를 사용하여 개체 또는 개체 그래프를 직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-217">**Serialize**: Serializes an object, or graph of objects, with the given root to the provided stream.</span></span>

<span data-ttu-id="438d1-218">`MyType` instance: 해당 형식 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-218">`MyType` instance: Instance of the type.</span></span>  
<span data-ttu-id="438d1-219">`IColumnWriter` writer / `IColumnReader` reader: 기본 열 스트림입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-219">`IColumnWriter` writer / `IColumnReader` reader: The underlying column stream.</span></span>  
<span data-ttu-id="438d1-220">`ISerializationContext` context: 직렬화하는 동안 스트림에 대한 원본 또는 대상 컨텍스트를 지정하는 플래그 집합을 정의하는 열거형입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-220">`ISerializationContext` context: Enum that defines a set of flags that specifies the source or destination context for the stream during serialization.</span></span>

* <span data-ttu-id="438d1-221">**Intermediate**: 원본 또는 대상 컨텍스트가 지속형 저장소가 아님을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-221">**Intermediate**: Specifies that the source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="438d1-222">**Persistence**: 원본 또는 대상 컨텍스트가 지속형 저장소임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-222">**Persistence**: Specifies that the source or destination context is a persisted store.</span></span>

<span data-ttu-id="438d1-223">일반 C# 형식으로 U-SQL UDT 정의는 +/==/!= 등의 연산자에 대한 재정의를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="438d1-224">정적 메서드도 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-224">It can also include static methods.</span></span> <span data-ttu-id="438d1-225">예를 들어 U-SQL MIN 집계 함수에 이 UDT를 매개 변수로 사용하는 경우 < 연산자 override를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-225">For example, if we are going to use this UDT as a parameter to a U-SQL MIN aggregate function, we have to define < operator override.</span></span>

<span data-ttu-id="438d1-226">이 가이드의 앞부분에서 Qn:Pn(Q1:P10) 형식의 특정 날짜로 회계 기간을 식별하는 예제를 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-226">Earlier in this guide, we demonstrated an example for fiscal period identification from the specific date in the format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="438d1-227">다음 예제에서는 회계 기간 값에 대한 사용자 지정 형식을 정의하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-227">The following example shows how to define a custom type for fiscal period values.</span></span>

<span data-ttu-id="438d1-228">다음은 사용자 지정 UDT 및 IFormatter 인터페이스가 포함된 코드 숨김 섹션의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="438d1-229">정의된 형식에는 두 개의 숫자(Quarter 및 Month)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-229">The defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="438d1-230">여기서 ==/!=/>/< 연산자 및 ToString() 정적 메서드가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="438d1-231">앞에서 설명한 대로 UDT는 SELECT 식에서 사용할 수 있지만, 사용자 지정 직렬화 없이는 OUTPUTTER/EXTRACTOR에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="438d1-232">ToString()을 사용하여 문자열로 직렬화하거나 사용자 지정 OUTPUTTER/EXTRACTOR와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-232">It either has to be serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="438d1-233">이제 UDT 사용법에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="438d1-234">코드 숨김 섹션에서 GetFiscalPeriod 함수를 다음과 같이 변경했습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-234">In a code-behind section, we changed our GetFiscalPeriod function to the following:</span></span>

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

<span data-ttu-id="438d1-235">여기서 볼 수 있듯이 FiscalPeriod 형식의 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-235">As you can see, it returns the value of our FiscalPeriod type.</span></span>

<span data-ttu-id="438d1-236">다음은 U-SQL 기본 스크립트에서 이 값을 사용하는 방법에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-236">Here we provide an example of how to use it further in U-SQL base script.</span></span> <span data-ttu-id="438d1-237">이 예제에서는 U-SQL 스크립트에서 UDT를 호출하는 다른 형식을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

       // This user-defined type was created in the prior SELECT.  Passing the UDT to this subsequent SELECT would have failed if the UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="438d1-238">다음은 전체 코드 숨김 섹션의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="438d1-239">UDAGG(사용자 정의 집계) 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="438d1-240">UDAGG(사용자 정의 집계)는 U-SQL에 제공되지 않는 집계 관련 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="438d1-241">예제에는 사용자 지정 수학 계산, 문자열 연결 또는 문자열 조작 등을 수행하는 집계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-241">The example can be an aggregate to perform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="438d1-242">UDAGG(사용자 정의 집계) 기본 클래스 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-242">The user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="438d1-243">**SqlUserDefinedAggregate**는 UDAGG로 등록해야 하는 형식임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-243">**SqlUserDefinedAggregate** indicates that the type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="438d1-244">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-244">This class cannot be inherited.</span></span>

<span data-ttu-id="438d1-245">SqlUserDefinedType 특성은 UDAGG 정의의 **선택 사항**입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="438d1-246">기본 클래스를 사용하면 세 개의 추상 매개 변수(두 개는 입력 매개 변수로, 하나는 결과로)를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-246">The base class allows you to pass three abstract parameters: two as input parameters and one as the result.</span></span> <span data-ttu-id="438d1-247">데이터 형식은 변수이며, 클래스를 상속하는 동안 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-247">The data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="438d1-248">**Init**는 계산하는 동안 각 그룹에 대해 한 번씩 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="438d1-249">각 집계 그룹에 대한 초기화 루틴을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="438d1-250">**Accumulate**는 각 값에 대해 한 번씩 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="438d1-251">집계 알고리즘의 주요 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-251">It provides the main functionality for the aggregation algorithm.</span></span> <span data-ttu-id="438d1-252">클래스를 상속하는 동안 정의된 다양한 데이터 형식으로 값을 집계하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-252">It can be used to aggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="438d1-253">변수 데이터 형식의 매개 변수 두 개를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="438d1-254">**Terminate**는 처리가 끝날 때 집계 그룹당 한 번씩 실행되어 각 그룹에 대한 결과를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-254">**Terminate** is executed once per aggregation group at the end of processing to output the result for each group.</span></span>

<span data-ttu-id="438d1-255">올바른 입력 및 출력 데이터 형식을 선언하려면 다음과 같이 클래스 정의를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-255">To declare correct input and output data types, use the class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="438d1-256">T1: Accumulate의 첫 번째 매개 변수</span><span class="sxs-lookup"><span data-stu-id="438d1-256">T1: First parameter to accumulate</span></span>
* <span data-ttu-id="438d1-257">T2: Accumulate의 두 번째 매개 변수</span><span class="sxs-lookup"><span data-stu-id="438d1-257">T2: First parameter to accumulate</span></span>
* <span data-ttu-id="438d1-258">TResult: Terminate의 반환 형식</span><span class="sxs-lookup"><span data-stu-id="438d1-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="438d1-259">예:</span><span class="sxs-lookup"><span data-stu-id="438d1-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="438d1-260">또는</span><span class="sxs-lookup"><span data-stu-id="438d1-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="438d1-261">U-SQL에서 UDAGG 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="438d1-262">UDAGG를 사용하려면 먼저 코드 숨김에 정의하거나 앞에서 설명한 대로 기존 프로그래밍 기능 DLL에서 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-262">To use UDAGG, first define it in code-behind or reference it from the existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="438d1-263">그런 다음, 다음 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-263">Then use the following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="438d1-264">UDAGG의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="438d1-265">기본 U-SQL 스크립트:</span><span class="sxs-lookup"><span data-stu-id="438d1-265">And base U-SQL script:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="438d1-266">이 사용 사례 시나리오에서는 특정 사용자에 대한 GUID 클래스를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-266">In this use-case scenario, we concatenate class GUIDs for the specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="438d1-267">UDO(사용자 정의 개체) 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="438d1-268">U-SQL을 사용하면 UDO(사용자 정의 개체)라는 사용자 지정 프로그래밍 기능 개체를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-268">U-SQL enables you to define custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="438d1-269">U-SQL의 UDO 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-269">The following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="438d1-270">사용자 정의 추출기</span><span class="sxs-lookup"><span data-stu-id="438d1-270">User-defined extractors</span></span>
    * <span data-ttu-id="438d1-271">행 단위 추출</span><span class="sxs-lookup"><span data-stu-id="438d1-271">Extract row by row</span></span>
    * <span data-ttu-id="438d1-272">사용자 지정 구조화된 파일에서 데이터 추출을 구현하는 데 사용됨</span><span class="sxs-lookup"><span data-stu-id="438d1-272">Used to implement data extraction from custom structured files</span></span>

* <span data-ttu-id="438d1-273">사용자 정의 출력자</span><span class="sxs-lookup"><span data-stu-id="438d1-273">User-defined outputters</span></span>
    * <span data-ttu-id="438d1-274">행 단위 출력</span><span class="sxs-lookup"><span data-stu-id="438d1-274">Output row by row</span></span>
    * <span data-ttu-id="438d1-275">사용자 지정 데이터 형식 또는 사용자 지정 파일 형식을 출력하는 데 사용됨</span><span class="sxs-lookup"><span data-stu-id="438d1-275">Used to output custom data types or custom file formats</span></span>

* <span data-ttu-id="438d1-276">사용자 정의 처리기</span><span class="sxs-lookup"><span data-stu-id="438d1-276">User-defined processors</span></span>
    * <span data-ttu-id="438d1-277">한 행씩 가져와 한 행씩 생성</span><span class="sxs-lookup"><span data-stu-id="438d1-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="438d1-278">열 수를 줄이거나 기존 열 집합에서 파생된 값으로 새 열을 생성하는 데 사용됨</span><span class="sxs-lookup"><span data-stu-id="438d1-278">Used to reduce the number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="438d1-279">사용자 정의 적용자</span><span class="sxs-lookup"><span data-stu-id="438d1-279">User-defined appliers</span></span>
    * <span data-ttu-id="438d1-280">한 행씩 가져와 0-n 개 행 생성</span><span class="sxs-lookup"><span data-stu-id="438d1-280">Take one row and produce 0 to n rows</span></span>
    * <span data-ttu-id="438d1-281">OUTER/CROSS APPLY 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="438d1-282">사용자 정의 결합자</span><span class="sxs-lookup"><span data-stu-id="438d1-282">User-defined combiners</span></span>
    * <span data-ttu-id="438d1-283">행 집합 결합--사용자 정의 JOIN</span><span class="sxs-lookup"><span data-stu-id="438d1-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="438d1-284">사용자 정의 리듀서</span><span class="sxs-lookup"><span data-stu-id="438d1-284">User-defined reducers</span></span>
    * <span data-ttu-id="438d1-285">n개 행을 가져와 한 행씩 생성</span><span class="sxs-lookup"><span data-stu-id="438d1-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="438d1-286">행 수를 줄이는 데 사용됨</span><span class="sxs-lookup"><span data-stu-id="438d1-286">Used to reduce the number of rows</span></span>

<span data-ttu-id="438d1-287">UDO는 일반적으로 다음 U-SQL 문의 일부로 U-SQL 스크립트에서 명시적으로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-287">UDO is typically called explicitly in U-SQL script as part of the following U-SQL statements:</span></span>

* <span data-ttu-id="438d1-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="438d1-288">EXTRACT</span></span>
* <span data-ttu-id="438d1-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="438d1-289">OUTPUT</span></span>
* <span data-ttu-id="438d1-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="438d1-290">PROCESS</span></span>
* <span data-ttu-id="438d1-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="438d1-291">COMBINE</span></span>
* <span data-ttu-id="438d1-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="438d1-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="438d1-293">UDO는 0.5Gb 메모리를 사용하도록 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-293">UDO’s are limited to consume 0.5Gb memory.</span></span>  <span data-ttu-id="438d1-294">이 메모리 제한은 로컬 실행에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-294">This memory limitation does not apply to local executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="438d1-295">UDE(사용자 정의 추출기) 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-295">Use user-defined extractors</span></span>
<span data-ttu-id="438d1-296">U-SQL을 사용하면 EXTRACT 문을 사용하여 외부 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-296">U-SQL allows you to import external data by using an EXTRACT statement.</span></span> <span data-ttu-id="438d1-297">EXTRACT 문은 기본 제공 UDO 추출기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="438d1-298">*Extractors.Text()*: 다른 인코딩의 구분 기호로 분리된 텍스트 파일에서 데이터를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="438d1-299">*Extractors.Csv()*: 다른 인코딩의 쉼표로 구분된 값(CSV) 파일에서 데이터를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="438d1-300">*Extractors.Tsv()*: 다른 인코딩의 탭으로 구분된 값(TSV) 파일에서 데이터를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="438d1-301">사용자 지정 추출기를 개발하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-301">It can be useful to develop a custom extractor.</span></span> <span data-ttu-id="438d1-302">다음 작업 중 하나를 수행하려는 경우 데이터를 가져오는 동안 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-302">This can be helpful during data import if we want to do any of the following tasks:</span></span>

* <span data-ttu-id="438d1-303">열을 분할하고 개별 값을 수정하여 입력 데이터를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="438d1-304">PROCESSOR 기능이 열을 결합하는 데 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-304">The PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="438d1-305">구조화되지 않은 데이터(예: 웹 페이지 및 전자 메일) 또는 반 구조화되지 않은 데이터(예: XML/JSON)를 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="438d1-306">지원되지 않는 인코딩 데이터를 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="438d1-307">UDE(사용자 정의 추출기)를 정의하려면 `IExtractor` 인터페이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-307">To define a user-defined extractor, or UDE, we need to create an `IExtractor` interface.</span></span> <span data-ttu-id="438d1-308">열/행 구분 기호 및 인코딩 등과 같은 추출기에 대한 모든 입력 매개 변수는 클래스의 생성자에서 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-308">All input parameters to the extractor, such as column/row delimiters, and encoding, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="438d1-309">다음과 같이 `IExtractor` 인터페이스는 `IEnumerable<IRow>` override에 대한 정의도 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-309">The `IExtractor`  interface should also contain a definition for the `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="438d1-310">**SqlUserDefinedExtractor** 특성은 UDE(사용자 정의 추출기)로 등록해야 하는 형식임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-310">The **SqlUserDefinedExtractor** attribute indicates that the type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="438d1-311">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-311">This class cannot be inherited.</span></span>

<span data-ttu-id="438d1-312">SqlUserDefinedExtractor는 UDE 정의의 선택적 특성이며,</span><span class="sxs-lookup"><span data-stu-id="438d1-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="438d1-313">UDE 개체의 AtomicFileProcessing 속성을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-313">It used to define AtomicFileProcessing property for the UDE object.</span></span>

* <span data-ttu-id="438d1-314">bool AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="438d1-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="438d1-315">**true**는 추출기에 원자성 입력 파일(JSON, XML 등)이 필요함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="438d1-316">**false**는 추출기에서 분할/분산 파일(CSV, SEQ 등)을 처리할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="438d1-317">주 UDE 프로그래밍 개체는 **input** 및 **output**입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-317">The main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="438d1-318">input 개체는 입력 데이터를 `IUnstructuredReader`로 열거하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-318">The input object is used to enumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="438d1-319">output 개체는 출력 데이터를 추출기 작업의 결과로 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-319">The output object is used to set output data as a result of the extractor activity.</span></span>

<span data-ttu-id="438d1-320">입력 데이터는 `System.IO.Stream` 및 `System.IO.StreamReader`를 통해 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-320">The input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="438d1-321">입력 열 열거형의 경우 먼저 행 구분 기호를 사용하여 입력 스트림을 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-321">For input columns enumeration, we first split the input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="438d1-322">그런 다음 입력 행을 열 파트로 세분합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="438d1-323">출력 데이터를 설정하려면 `output.Set` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-323">To set output data, we use the `output.Set` method.</span></span>

<span data-ttu-id="438d1-324">사용자 지정 추출기는 출력에 정의된 열 및 값만 출력한다는 점을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-324">It's important to understand that the custom extractor only outputs columns and values that are defined with the output.</span></span> <span data-ttu-id="438d1-325">메서드 호출을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="438d1-326">실제 추출기 출력은 `yield return output.AsReadOnly();`를 호출하여 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-326">The actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="438d1-327">다음은 추출기 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-327">Following is the extractor example:</span></span>

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
         //Read the input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split the input by the column delimiter
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
                 // for column “user”, convert to UPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep the rest of the columns as-is
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

<span data-ttu-id="438d1-328">이 사용 사례 시나리오에서 추출기는 “guid” 열에 대한 GUID를 다시 생성하고 “user” 열의 값을 대문자로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-328">In this use-case scenario, the extractor regenerates the GUID for “guid” column and converts the values of “user” column to upper case.</span></span> <span data-ttu-id="438d1-329">사용자 지정 추출기는 입력 데이터를 구문 분석하고 이를 조작하여 더 복잡한 결과를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="438d1-330">다음은 사용자 지정 추출기를 사용하는 기본 U-SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

OUTPUT @rs0 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="438d1-331">사용자 정의 출력자 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-331">Use user-defined outputters</span></span>
<span data-ttu-id="438d1-332">사용자 정의 출력자는 기본 제공 U-SQL 기능을 확장할 수 있는 또 다른 U-SQL UDO입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-332">User-defined outputter is another U-SQL UDO that allows you to extend built-in U-SQL functionality.</span></span> <span data-ttu-id="438d1-333">추출기와 마찬가지로 여러 개의 기본 제공 출력자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-333">Similar to the extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="438d1-334">*Outputters.Text()*: 다른 인코딩의 구분 기호로 분리된 텍스트 파일에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-334">*Outputters.Text()*: Writes data to delimited text files of different encodings.</span></span>
* <span data-ttu-id="438d1-335">*Outputters.Csv()*: 다른 인코딩의 쉼표로 구분된 값(CSV) 파일에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-335">*Outputters.Csv()*: Writes data to comma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="438d1-336">*Outputters.Tsv()*: 다른 인코딩의 탭으로 구분된 값(TSV) 파일에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-336">*Outputters.Tsv()*: Writes data to tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="438d1-337">사용자 지정 출력자를 사용하면 사용자 정의된 형식으로 데이터를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-337">Custom outputter allows you to write data in a custom defined format.</span></span> <span data-ttu-id="438d1-338">이 기능은 다음 작업에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-338">This can be useful for the following tasks:</span></span>

* <span data-ttu-id="438d1-339">반 구조화되거나 구조화되지 않은 파일에 데이터 쓰기</span><span class="sxs-lookup"><span data-stu-id="438d1-339">Writing data to semi-structured or unstructured files.</span></span>
* <span data-ttu-id="438d1-340">지원되지 않는 인코딩 데이터 쓰기</span><span class="sxs-lookup"><span data-stu-id="438d1-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="438d1-341">출력 데이터 수정 또는 사용자 지정 특성 추가</span><span class="sxs-lookup"><span data-stu-id="438d1-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="438d1-342">사용자 정의 출력자를 정의하려면 `IOutputter` 인터페이스를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-342">To define user-defined outputter, we need to create the `IOutputter` interface.</span></span>

<span data-ttu-id="438d1-343">다음은 기본 `IOutputter` 클래스 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-343">Following is the base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="438d1-344">열/행 구분 기호, 인코딩 등과 같은 출력자에 대한 모든 입력 매개 변수는 클래스의 생성자에서 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-344">All input parameters to the outputter, such as column/row delimiters, encoding, and so on, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="438d1-345">`IOutputter` 인터페이스는 `void Output` override에 대한 정의도 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-345">The `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="438d1-346">`[SqlUserDefinedOutputter(AtomicFileProcessing = true)` 특성은 원자성 파일 처리를 위해 선택적으로 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-346">The attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="438d1-347">자세한 내용은 다음 세부 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="438d1-347">For more information, see the following details.</span></span>

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

* <span data-ttu-id="438d1-348">`Output`은 각 입력 행에 대해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-348">`Output` is called for each input row.</span></span> <span data-ttu-id="438d1-349">`IUnstructuredWriter output` 행 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-349">It returns the `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="438d1-350">생성자 클래스는 사용자 정의 출력자에 매개 변수를 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-350">The Constructor class is used to pass parameters to the user-defined outputter.</span></span>
* <span data-ttu-id="438d1-351">`Close`는 비용이 높은 상태를 해제하거나 마지막 행이 기록된 시점을 판단하기 위해 선택적으로 재정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-351">`Close` is used to optionally override to release expensive state or determine when the last row was written.</span></span>

<span data-ttu-id="438d1-352">**SqlUserDefinedOutputter** 특성은 사용자 정의 출력자로 등록해야 하는 형식임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-352">**SqlUserDefinedOutputter** attribute indicates that the type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="438d1-353">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-353">This class cannot be inherited.</span></span>

<span data-ttu-id="438d1-354">SqlUserDefinedOutputter는 사용자 정의 출력자 정의의 선택적 특성이며,</span><span class="sxs-lookup"><span data-stu-id="438d1-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="438d1-355">AtomicFileProcessing 속성을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-355">It's used to define the AtomicFileProcessing property.</span></span>

* <span data-ttu-id="438d1-356">bool AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="438d1-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="438d1-357">**true**는 출력자에 원자성 출력 파일(JSON, XML 등)이 필요함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="438d1-358">**false**는 출력자에서 분할/분산 파일(CSV, SEQ 등)을 처리할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="438d1-359">주요 프로그래밍 개체는 **row** 및 **output**입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-359">The main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="438d1-360">**row** 개체는 출력 데이터를 `IRow` 인터페이스로 나열하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-360">The **row** object is used to enumerate output data as `IRow` interface.</span></span> <span data-ttu-id="438d1-361">**Output**은 대상 파일에 출력 데이터를 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-361">**Output** is used to set output data to the target file.</span></span>

<span data-ttu-id="438d1-362">출력 데이터는 `IRow` 인터페이스를 통해 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-362">The output data is accessed through the `IRow` interface.</span></span> <span data-ttu-id="438d1-363">출력 데이터는 한 번에 한 행씩 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="438d1-364">개별 값은 IRow 인터페이스의 Get 메서드를 호출하여 열거됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-364">The individual values are enumerated by calling the Get method of the IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="438d1-365">개별 열 이름은 `row.Schema`를 호출하여 결정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="438d1-366">이렇게 하면 모든 메타데이터 스키마에 대해 유연한 출력자를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-366">This approach enables you to build a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="438d1-367">출력 데이터는 `System.IO.StreamWriter`를 사용하여 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-367">The output data is written to file by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="438d1-368">Stream 매개 변수는 `IUnstructuredWriter output`의 일부로 `output.BaseStrea`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-368">The stream parameter is set to `output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="438d1-369">각 행을 반복한 후에 파일에 데이터 버퍼를 플러시하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-369">Note that it's important to flush the data buffer to the file after each row iteration.</span></span> <span data-ttu-id="438d1-370">또한 Disposable 특성이 활성화된 상태에서(기본값) **using** 키워드와 함께 `StreamWriter` 개체를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-370">In addition, the `StreamWriter` object must be used with the Disposable attribute enabled (default) and with the **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="438d1-371">그렇지 않으면 매번 반복 후에 Flush() 메서드를 명시적으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="438d1-372">이 내용은 다음 예제에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-372">We show this in the following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="438d1-373">사용자 정의 출력자의 머리글 및 바닥글 설정</span><span class="sxs-lookup"><span data-stu-id="438d1-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="438d1-374">헤더를 설정하려면 단일 반복 실행 흐름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-374">To set a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="438d1-375">첫 번째 `if (isHeaderRow)` 블록의 코드는 한 번만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-375">The code in the first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="438d1-376">바닥글의 경우 `System.IO.Stream` 개체(`output.BaseStream`)의 인스턴스에 대한 참조를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-376">For the footer, use the reference to the instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="438d1-377">`IOutputter` 인터페이스의 Close() 메서드에 바닥글을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-377">Write the footer in the Close() method of the `IOutputter` interface.</span></span>  <span data-ttu-id="438d1-378">(자세한 내용은 다음 예제를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="438d1-378">(For more information, see the following example.)</span></span>

<span data-ttu-id="438d1-379">다음의 사용자 정의 출력자에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-379">Following is an example of a user-defined outputter:</span></span>

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

    // The Close method is used to write the footer to the file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference to IO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization to enumerate column names
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
        // Data type enumeration--required to match the distinct list of types from OUTPUT statement
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
    // Reference to the instance of the IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define the factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="438d1-380">U-SQL 기본 스크립트:</span><span class="sxs-lookup"><span data-stu-id="438d1-380">And U-SQL base script:</span></span>

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
    TO @output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="438d1-381">HTML 출력자이며, 테이블 데이터로 HTML 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="438d1-382">U-SQL 기본 스크립트에서 출력자 호출</span><span class="sxs-lookup"><span data-stu-id="438d1-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="438d1-383">기본 U-SQL 스크립트에서 사용자 지정 출력자를 호출하려면 출력자 개체의 새 인스턴스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-383">To call a custom outputter from the base U-SQL script, the new instance of the outputter object has to be created.</span></span>

```sql
OUTPUT @rs0 TO @output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="438d1-384">앞의 예에서 설명했듯이, 기본 스크립트로 개체 인스턴스를 작성하지 않기 위해 함수 래퍼를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-384">To avoid creating an instance of the object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define the factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="438d1-385">이 경우 원래 호출은 다음과 같은 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-385">In this case, the original call looks like the following:</span></span>

```
OUTPUT @rs0 
TO @output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="438d1-386">UDP(사용자 정의 처리기) 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-386">Use user-defined processors</span></span>
<span data-ttu-id="438d1-387">UDP(사용자 정의 처리기)는 프로그래밍 기능을 적용하여 들어오는 행을 처리할 수 있는 U-SQL UDO의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you to process the incoming rows by applying programmability features.</span></span> <span data-ttu-id="438d1-388">UDP를 사용하면 열을 결합하고, 값을 수정하고, 필요한 경우 새 열을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-388">UDP enables you to combine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="438d1-389">기본적으로 필요한 데이터 요소를 생성하기 위해 행 집합을 처리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-389">Basically, it helps to process a rowset to produce required data elements.</span></span>

<span data-ttu-id="438d1-390">UDP를 정의하려면 UDP의 선택 사항인 `SqlUserDefinedProcessor` 특성을 포함한 `IProcessor` 인터페이스를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-390">To define a UDP, we need to create an `IProcessor` interface with the `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="438d1-391">다음 예제와 같이 이 인터페이스는 `IRow` 인터페이스 행 집합 override에 대한 정의를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-391">This interface should contain the definition for the `IRow` interface rowset override, as shown in the following example:</span></span>

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

<span data-ttu-id="438d1-392">**SqlUserDefinedProcessor**는 UDP로 등록해야 하는 형식임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-392">**SqlUserDefinedProcessor** indicates that the type should be registered as a user-defined processor.</span></span> <span data-ttu-id="438d1-393">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-393">This class cannot be inherited.</span></span>

<span data-ttu-id="438d1-394">SqlUserDefinedProcessor 특성은 UDP 정의의 **선택 사항**입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-394">The SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="438d1-395">주 프로그래밍 개체는 **input** 및 **output**입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-395">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="438d1-396">input 개체는 입력 열을 열거하고, output 개체는 출력 데이터를 처리기 작업의 결과로 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-396">The input object is used to enumerate input columns and output, and to set output data as a result of the processor activity.</span></span>

<span data-ttu-id="438d1-397">입력 열을 열거하는 경우 `input.Get` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-397">For input columns enumeration, we use the `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="438d1-398">`input.Get` 메서드에 대한 매개 변수는 U-SQL 기본 스크립트의 `PROCESS` 문의 `PRODUCE` 절의 일부로 전달되는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-398">The parameter for `input.Get` method is a column that's passed as part of the `PRODUCE` clause of the `PROCESS` statement of the U-SQL base script.</span></span> <span data-ttu-id="438d1-399">여기서는 올바른 데이터 형식을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-399">We need to use the correct data type here.</span></span>

<span data-ttu-id="438d1-400">출력의 경우 `output.Set` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-400">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="438d1-401">사용자 지정 생산자는 `output.Set` 메서드 호출로 정의된 열과 값만을 출력한다는 점을 아는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-401">It's important to note that custom producer only outputs columns and values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="438d1-402">실제 처리기 출력은 `return output.AsReadOnly();`를 호출하여 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-402">The actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="438d1-403">다음은 처리기 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-403">Following is a processor example:</span></span>

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

<span data-ttu-id="438d1-404">이 사용 사례 시나리오에서 처리기는 기존 열, 이 경우 “user” 대문자와 “des”를 결합하여 “full_description”이라는 새 열을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-404">In this use-case scenario, the processor is generating a new column called “full_description” by combining the existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="438d1-405">또한 GUID를 다시 생성하고 원래 및 새 GUID 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-405">It also regenerates a GUID and returns the original and new GUID values.</span></span>

<span data-ttu-id="438d1-406">이전 예제에서 볼 수 있듯이 `output.Set` 메서드 호출 중에 C# 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-406">As you can see from the previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="438d1-407">다음은 사용자 지정 처리기를 사용하는 기본 U-SQL 스크립트의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="438d1-408">사용자 정의 적용자 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-408">Use user-defined appliers</span></span>
<span data-ttu-id="438d1-409">U-SQL 사용자 정의 적용자를 사용하면 쿼리의 외부 테이블 식에서 반환한 각 행에 대해 사용자 지정 C # 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-409">A U-SQL user-defined applier enables you to invoke a custom C# function for each row that's returned by the outer table expression of a query.</span></span> <span data-ttu-id="438d1-410">오른쪽 입력은 왼쪽 입력에서 각 행에 대해 평가되고, 생성된 행은 최종 출력을 위해 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-410">The right input is evaluated for each row from the left input, and the rows that are produced are combined for the final output.</span></span> <span data-ttu-id="438d1-411">APPLY 연산자에서 생성한 열 목록은 왼쪽 및 오른쪽 입력에 있는 열 집합의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-411">The list of columns that are produced by the APPLY operator are the combination of the set of columns in the left and the right input.</span></span>

<span data-ttu-id="438d1-412">사용자 정의 적용자는 U-SQL SELECT 식의 일부로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-412">User-defined applier is being invoked as part of the USQL SELECT expression.</span></span>

<span data-ttu-id="438d1-413">사용자 정의 적용자에 대한 일반적인 호출은 다음과 같은 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-413">The typical call to the user-defined applier looks like the following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used to pass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="438d1-414">SELECT 식의 적용자 사용에 대한 자세한 내용은 [U-SQL SELECT: CROSS APPLY 및 OUTER APPLY에서 선택](https://msdn.microsoft.com/library/azure/mt621307.aspx)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="438d1-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="438d1-415">사용자 정의 적용자 기본 클래스 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-415">The user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="438d1-416">사용자 정의 적용자를 정의하려면 사용자 정의 적용자 정의에서 선택적인 [`SqlUserDefinedApplier`] 특성을 포함한 `IApplier` 인터페이스를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-416">To define a user-defined applier, we need to create the `IApplier` interface with the [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="438d1-417">Apply는 Outer 테이블의 각 행에 대해 호출되며,</span><span class="sxs-lookup"><span data-stu-id="438d1-417">Apply is called for each row of the outer table.</span></span> <span data-ttu-id="438d1-418">`IUpdatableRow` 출력 행 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-418">It returns the `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="438d1-419">생성자 클래스는 사용자 정의 적용자에 매개 변수를 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-419">The Constructor class is used to pass parameters to the user-defined applier.</span></span>

<span data-ttu-id="438d1-420">**SqlUserDefinedApplier**는 사용자 정의 적용자로 등록해야 하는 형식임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-420">**SqlUserDefinedApplier** indicates that the type should be registered as a user-defined applier.</span></span> <span data-ttu-id="438d1-421">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-421">This class cannot be inherited.</span></span>

<span data-ttu-id="438d1-422">**SqlUserDefinedApplier**는 사용자 정의 적용자 정의의 **선택 사항**입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="438d1-423">주요 프로그래밍 개체는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-423">The main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="438d1-424">입력 행 집합은 `IRow` 입력으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="438d1-425">출력 행은 `IUpdatableRow` 출력 인터페이스로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-425">The output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="438d1-426">개별 열 이름은 `IRow` 스키마 메서드를 호출하여 결정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-426">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="438d1-427">들어오는 `IRow`에서 실제 데이터 값을 가져오려면 `IRow` 인터페이스의 Get() 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-427">To get the actual data values from the incoming `IRow`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="438d1-428">또는 스키마 열 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-428">Or we use the schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="438d1-429">출력 값은 `IUpdatableRow` 출력으로 설정해야 합니다</span><span class="sxs-lookup"><span data-stu-id="438d1-429">The output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="438d1-430">사용자 지정 적용자는 `output.Set` 메서드 호출로 정의된 열과 값만 출력한다는 점을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-430">It is important to understand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="438d1-431">실제 출력은 `yield return output.AsReadOnly();`를 호출하여 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-431">The actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="438d1-432">사용자 정의 적용자 매개 변수는 생성자에 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-432">The user-defined applier parameters can be passed to the constructor.</span></span> <span data-ttu-id="438d1-433">적용자는 기본 U-SQL 스크립트에서 Applier를 호출하는 동안 정의되어야 하는 가변 개수의 열을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-433">Applier can return a variable number of columns that need to be defined during the applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="438d1-434">다음은 사용자 정의 적용자 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-434">Here is the user-defined applier example:</span></span>

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

<span data-ttu-id="438d1-435">다음은 이 사용자 정의 적용자에 대한 기본 U-SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-435">Following is the base U-SQL script for this user-defined applier:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="438d1-436">이 사용 사례 시나리오에서 사용자 정의 적용자는 car fleet 속성에 대한 쉼표로 구분된 값 파서 역할을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for the car fleet properties.</span></span> <span data-ttu-id="438d1-437">입력 파일 행은 다음과 같은 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-437">The input file rows look like the following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="438d1-438">이 파일은 제조업체 모델 등의 자동차 속성을 포함하는 속성 열이 탭으로 분리된 일반적인 TSV 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="438d1-439">이러한 속성은 테이블 열로 구문 분석되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-439">Those properties must be parsed to the table columns.</span></span> <span data-ttu-id="438d1-440">제공된 적용자를 사용하면 전달되는 매개 변수를 기반으로 결과 행 집합에 동적인 수의 속성을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-440">The applier that's provided also enables you to generate a dynamic number of properties in the result rowset, based on the parameter that's passed.</span></span> <span data-ttu-id="438d1-441">모든 속성을 생성하거나 특정 속성 집합만 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="438d1-442">사용자 정의 적용자는 applier 개체의 새 인스턴스로 호출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-442">The user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="438d1-443">또는 래퍼 팩터리 메서드 호출을 통해 호출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-443">Or with the invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="438d1-444">사용자 정의 결합자 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-444">Use user-defined combiners</span></span>
<span data-ttu-id="438d1-445">UDC(사용자 정의 결합자)를 사용하면 사용자 지정 논리를 기반으로 하여 왼쪽 및 오른쪽 행 집합의 행을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-445">User-defined combiner, or UDC, enables you to combine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="438d1-446">UDC는 COMBINE 식으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="438d1-447">결합자는 입력 행 집합, 그룹화 열, 예상 결과 스키마 및 추가 정보에 대해 필요한 정보를 제공하는 COMBINE 식으로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-447">A combiner is being invoked with the COMBINE expression that provides the necessary information about both the input rowsets, the grouping columns, the expected result schema, and additional information.</span></span>

<span data-ttu-id="438d1-448">기본 U-SQL 스크립트에서 결합자를 호출하려면 다음 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-448">To call a combiner in a base U-SQL script, we use the following syntax:</span></span>

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

<span data-ttu-id="438d1-449">자세한 내용은 [COMBINE 식(U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="438d1-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="438d1-450">UDC를 정의하려면 UDC 정의에서 선택적인 [`SqlUserDefinedCombiner`] 속성을 포함한 `ICombiner` 인터페이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-450">To define a user-defined combiner, we need to create the `ICombiner` interface with the [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="438d1-451">기본 `ICombiner` 클래스 정의:</span><span class="sxs-lookup"><span data-stu-id="438d1-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="438d1-452">`ICombiner` 인터페이스의 사용자 지정 구현은 `IEnumerable<IRow>` Combine override에 대한 정의를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-452">The custom implementation of an `ICombiner` interface should contain the definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="438d1-453">**SqlUserDefinedCombiner** 특성은 사용자 정의 결합자로 등록해야 하는 형식임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-453">The **SqlUserDefinedCombiner** attribute indicates that the type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="438d1-454">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-454">This class cannot be inherited.</span></span>

<span data-ttu-id="438d1-455">**SqlUserDefinedCombiner**는 결합자 모드 속성을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-455">**SqlUserDefinedCombiner** is used to define the Combiner mode property.</span></span> <span data-ttu-id="438d1-456">사용자 정의 결합자 정의의 선택적 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="438d1-457">CombinerMode Mode</span><span class="sxs-lookup"><span data-stu-id="438d1-457">CombinerMode     Mode</span></span>

<span data-ttu-id="438d1-458">CombinerMode 열거형은 다음 값을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-458">CombinerMode enum can take the following values:</span></span>

* <span data-ttu-id="438d1-459">Full  (0) 모든 출력 행이 잠재적으로 왼쪽과 오른쪽에서 동일한 키 값을 가진 모든 입력 행에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-459">Full  (0) Every output row potentially depends on all the input rows from left and right       with the same key value.</span></span>

* <span data-ttu-id="438d1-460">Left  (1) 모든 출력 행이 왼쪽에서 단일 입력 행(그리고 잠재적으로 오른쪽에서 동일한 키 값을 가진 모든 행)에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-460">Left  (1) Every output row depends on a single input row from the left (and potentially all rows       from the right with the same key value).</span></span>

* <span data-ttu-id="438d1-461">Right (2)     모든 출력 행이 오른쪽에서 단일 입력 행(그리고 잠재적으로 왼쪽에서 동일한 키 값을 가진 모든 행)에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-461">Right (2)     Every output row depends on a single input row from the right (and potentially all rows       from the left with the same key value).</span></span>

* <span data-ttu-id="438d1-462">Inner (3) 모든 출력 행이 왼쪽과 오른쪽에서 동일한 값을 가진 단일 입력 행에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-462">Inner (3) Every output row depends on a single input row from left and right with the same value.</span></span>

<span data-ttu-id="438d1-463">예: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="438d1-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="438d1-464">주요 프로그래밍 개체:</span><span class="sxs-lookup"><span data-stu-id="438d1-464">The main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="438d1-465">입력 행 집합은 **left** 및 **right** `IRowset` 형식의 인터페이스로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="438d1-466">두 행 집합은 처리하기 위해 모두 열거되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="438d1-467">각 인터페이스를 한 번만 열거할 수 있으므로 필요에 따라 열거하고 캐시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-467">You can only enumerate each interface once, so we have to enumerate and cache it if necessary.</span></span>

<span data-ttu-id="438d1-468">캐싱을 위해 LINQ 쿼리 실행의 결과로 List\<T\> 형식의 메모리 구조체를 만들 수 있습니다(구체적으로 List<`IRow`>).</span><span class="sxs-lookup"><span data-stu-id="438d1-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="438d1-469">익명 데이터 형식도 열거하는 동안에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-469">The anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="438d1-470">LINQ 쿼리에 대한 자세한 내용은 [LINQ 쿼리 소개(C#)](https://msdn.microsoft.com/library/bb397906.aspx)를 참조하고, IEnumerable\<T\> 인터페이스에 대한 자세한 내용은 [IEnumerable\<T\> 인터페이스](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="438d1-470">See [Introduction to LINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="438d1-471">들어오는 `IRowset`에서 실제 데이터 값을 가져오려면 `IRow` 인터페이스의 Get() 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-471">To get the actual data values from the incoming `IRowset`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="438d1-472">개별 열 이름은 `IRow` 스키마 메서드를 호출하여 결정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-472">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="438d1-473">또는 스키마 열 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-473">Or by using the schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="438d1-474">LINQ를 사용한 일반적인 열거형은 다음과 같은 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-474">The general enumeration with LINQ looks like the following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="438d1-475">두 가지 행 집합을 열거한 후 모든 행을 반복할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-475">After enumerating both rowsets, we are going to loop through all rows.</span></span> <span data-ttu-id="438d1-476">왼쪽 행 집합의 각 행에 대해 결합자의 조건을 충족하는 모든 행을 찾을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-476">For each row in the left rowset, we are going to find all rows that satisfy the condition of our combiner.</span></span>

<span data-ttu-id="438d1-477">출력 값은 `IUpdatableRow` 출력으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-477">The output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="438d1-478">실제 출력은 `yield return output.AsReadOnly();`를 호출하여 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-478">The actual output is triggered by calling to `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="438d1-479">다음은 결합자 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="438d1-480">이 사용 사례 시나리오에서는 판매점에 대한 분석 보고서를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-480">In this use-case scenario, we are building an analytics report for the retailer.</span></span> <span data-ttu-id="438d1-481">목표는 $20,000이 넘고 특정 시간 프레임 내에 일반 판매점보다 인터넷 웹 사이트를 통해 빠르게 판매된 모든 제품을 찾는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-481">The goal is to find all products that cost more than $20,000 and that sell through the website faster than through the regular retailer within a certain time frame.</span></span>

<span data-ttu-id="438d1-482">다음은 기본 U-SQL 스크립트이며,</span><span class="sxs-lookup"><span data-stu-id="438d1-482">Here is the base U-SQL script.</span></span> <span data-ttu-id="438d1-483">일반 JOIN과 결합자 사이의 논리를 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-483">You can compare the logic between a regular JOIN and a combiner:</span></span>

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

OUTPUT @rs1 TO @output_file1 USING Outputters.Tsv();
OUTPUT @rs2 TO @output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="438d1-484">사용자 정의 결합자는 applier 개체의 새 인스턴스로 호출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-484">A user-defined combiner can be called as a new instance of the applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="438d1-485">또는 래퍼 팩터리 메서드 호출을 통해 호출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-485">Or with the invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="438d1-486">사용자 정의 리듀서 사용</span><span class="sxs-lookup"><span data-stu-id="438d1-486">Use user-defined reducers</span></span>

<span data-ttu-id="438d1-487">U-SQL을 사용하면 IReducer 인터페이스를 구현하고 사용자 정의 연산자 확장성 프레임워크를 사용하여 C#으로 사용자 지정 행 집합 리듀서를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-487">U-SQL enables you to write custom rowset reducers in C# by using the user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="438d1-488">UDR(사용자 정의 리듀서)은 데이터를 추출하는(가져오기) 동안 불필요한 행을 제거하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-488">User-defined reducer, or UDR, can be used to eliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="438d1-489">행 및 열을 조작하고 평가하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-489">It also can be used to manipulate and evaluate rows and columns.</span></span> <span data-ttu-id="438d1-490">프로그래밍 기능 논리를 기반으로 추출해야 하는 행을 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-490">Based on programmability logic, it can also define which rows need to be extracted.</span></span>

<span data-ttu-id="438d1-491">UDR 클래스를 정의하려면 선택적 `SqlUserDefinedReducer` 특성을 사용하여 `IReducer` 인터페이스를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-491">To define a UDR class, we need to create an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="438d1-492">이 클래스 인터페이스는 `IEnumerable` 인터페이스 행 집합 override에 대한 정의를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-492">This class interface should contain a definition for the `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="438d1-493">**SqlUserDefinedReducer** 특성은 사용자 정의 리듀서로 등록해야 하는 형식임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-493">The **SqlUserDefinedReducer** attribute indicates that the type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="438d1-494">이 클래스는 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-494">This class cannot be inherited.</span></span>
<span data-ttu-id="438d1-495">**SqlUserDefinedReducer**는 UDR(사용자 정의 리듀서) 정의의 선택적 특성이며,</span><span class="sxs-lookup"><span data-stu-id="438d1-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="438d1-496">IsRecursive 속성을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-496">It's used to define IsRecursive property.</span></span>

* <span data-ttu-id="438d1-497">bool IsRecursive</span><span class="sxs-lookup"><span data-stu-id="438d1-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="438d1-498">**true**는 idempotent 유형의 리듀서인지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="438d1-499">주 프로그래밍 개체는 **input** 및 **output**입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-499">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="438d1-500">input 개체는 입력 행을 열거하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-500">The input object is used to enumerate input rows.</span></span> <span data-ttu-id="438d1-501">Output 개체는 감소 작업의 결과로 출력 행을 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-501">Output is used to set output rows as a result of reducing activity.</span></span>

<span data-ttu-id="438d1-502">입력 행 열거형의 경우 `Row.Get` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-502">For input rows enumeration, we use the `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="438d1-503">`Row.Get` 메서드에 대한 매개 변수는 U-SQL 기본 스크립트의 `REDUCE` 문의 `PRODUCE` 클래스의 일부로 전달되는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-503">The parameter for the `Row.Get` method is a column that's passed as part of the `PRODUCE` class of the `REDUCE` statement of the U-SQL base script.</span></span> <span data-ttu-id="438d1-504">여기서도 올바른 데이터 형식을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-504">We need to use the correct data type here as well.</span></span>

<span data-ttu-id="438d1-505">출력의 경우 `output.Set` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-505">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="438d1-506">사용자 지정 리듀서는 `output.Set` 메서드 호출로 정의된 값만 출력한다는 것을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-506">It is important to understand that custom reducer only outputs values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="438d1-507">실제 리듀서 출력은 `yield return output.AsReadOnly();`를 호출하여 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-507">The actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="438d1-508">다음은 리듀서 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="438d1-509">이 사용 사례 시나리오에서 리듀서는 사용자 이름이 비어 있는 행을 건너 뜁니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-509">In this use-case scenario, the reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="438d1-510">행 집합의 각 행에 대해 각각의 필수 열을 읽은 다음 사용자 이름의 길이를 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-510">For each row in rowset, it reads each required column, then evaluates the length of the user name.</span></span> <span data-ttu-id="438d1-511">사용자 이름 값 길이가 0보다 큰 경우에만 실제 행을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-511">It outputs the actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="438d1-512">다음은 사용자 지정 리듀서를 사용하는 기본 U-SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="438d1-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
    TO @output_file 
    USING Outputters.Text();
```
