---
title: "U-SQL aaaDevelop 사용자 정의 연산자 (Udo) | Microsoft Docs"
description: "Toodevelop 사용자 정의 연산자 toobe 사용 하 고 작업을 다시 Data Lake 분석에 사용 하는 방법에 대해 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: e5189e4e-9438-46d1-8686-ed4836bf3356
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 6b86618efd3751cd9a5e91875879d7dd6d6a7b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="1f4c4-103">U-SQL UDO(사용자 정의 연산자) 개발</span><span class="sxs-lookup"><span data-stu-id="1f4c4-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="1f4c4-104">자세한 방법을 toodevelop 사용자 정의 연산자 tooprocess 데이터 U-SQL 작업에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-104">Learn how toodevelop user-defined operators tooprocess data in a U-SQL job.</span></span>

<span data-ttu-id="1f4c4-105">U-SQL에 대한 일반적인 용도의 어셈블리 개발에 대한 지침은 [Azure Data Lake Analytics 작업에 대한 U-SQL 어셈블리 개발](data-lake-analytics-u-sql-develop-assemblies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="1f4c4-106">U-SQL에서 사용자 정의 연산자 정의 및 사용</span><span class="sxs-lookup"><span data-stu-id="1f4c4-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="1f4c4-107">**toocreate U-SQL 작업을 제출 하 고**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-107">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="1f4c4-108">Hello Visual Studio에서에서 선택 **파일 > 새로 만들기 > 프로젝트 > U-SQL 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-108">From hello Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="1f4c4-109">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-109">Click **OK**.</span></span> <span data-ttu-id="1f4c4-110">Visual Studio는 Script.usql 파일로 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="1f4c4-111">**솔루션 탐색기**에서 Script.usql을 확장하고 **Script.usql.cs**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="1f4c4-112">Hello를 hello 파일에 코드를 다음에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-112">Paste hello following code into hello file:</span></span>

        using Microsoft.Analytics.Interfaces;
        using System.Collections.Generic;

        namespace USQL_UDO
        {
            public class CountryName : IProcessor
            {
                private static IDictionary<string, string> CountryTranslation = new Dictionary<string, string>
                {
                    {
                        "Deutschland", "Germany"
                    },
                    {
                        "Suisse", "Switzerland"
                    },
                    {
                        "UK", "United Kingdom"
                    },
                    {
                        "USA", "United States of America"
                    },
                    {
                        "中国", "PR China"
                    }
                };

                public override IRow Process(IRow input, IUpdatableRow output)
                {

                    string UserID = input.Get<string>("UserID");
                    string Name = input.Get<string>("Name");
                    string Address = input.Get<string>("Address");
                    string City = input.Get<string>("City");
                    string State = input.Get<string>("State");
                    string PostalCode = input.Get<string>("PostalCode");
                    string Country = input.Get<string>("Country");
                    string Phone = input.Get<string>("Phone");

                    if (CountryTranslation.Keys.Contains(Country))
                    {
                        Country = CountryTranslation[Country];
                    }
                    output.Set<string>(0, UserID);
                    output.Set<string>(1, Name);
                    output.Set<string>(2, Address);
                    output.Set<string>(3, City);
                    output.Set<string>(4, State);
                    output.Set<string>(5, PostalCode);
                    output.Set<string>(6, Country);
                    output.Set<string>(7, Phone);

                    return output.AsReadOnly();
                }
            }
        }
6. <span data-ttu-id="1f4c4-113">열기 **Script.usql**, 및 붙여넣기 hello U-SQL 스크립트를 다음과 같은:</span><span class="sxs-lookup"><span data-stu-id="1f4c4-113">Open **Script.usql**, and paste hello following U-SQL script:</span></span>

        @drivers =
            EXTRACT UserID      string,
                    Name        string,
                    Address     string,
                    City        string,
                    State       string,
                    PostalCode  string,
                    Country     string,
                    Phone       string
            FROM "/Samples/Data/AmbulanceData/Drivers.txt"
            USING Extractors.Tsv(Encoding.Unicode);

        @drivers_CountryName =
            PROCESS @drivers
            PRODUCE UserID string,
                    Name string,
                    Address string,
                    City string,
                    State string,
                    PostalCode string,
                    Country string,
                    Phone string
            USING new USQL_UDO.CountryName();    

        OUTPUT @drivers_CountryName
            too"/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. <span data-ttu-id="1f4c4-114">Hello Data Lake 분석 계정, 데이터베이스 및 스키마를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-114">Specify hello Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="1f4c4-115">**솔루션 탐색기**에서 **Script.usql**을 마우스 오른쪽 클릭하고 **빌드 스크립트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="1f4c4-116">**솔루션 탐색기**에서 **Script.usql**을 마우스 오른쪽 클릭하고 **스크립트 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="1f4c4-117">tooyour Azure 구독을 연결 하지 않은 경우 증명된 tooenter Azure 계정 자격 증명 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-117">If you haven't connected tooyour Azure subscription, you will be prompted tooenter your Azure account credentials.</span></span>
11. <span data-ttu-id="1f4c4-118">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-118">Click **Submit**.</span></span> <span data-ttu-id="1f4c4-119">제출 결과 및 작업 링크는 hello 결과 창에서 hello 전송이 완료 될 때.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-119">Submission results and job link are available in hello Results window when hello submission is completed.</span></span>
12. <span data-ttu-id="1f4c4-120">Hello 클릭 **새로 고침** 단추 toosee hello 최신 작업 상태 및 새로 고침 hello 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-120">Click hello **Refresh** button toosee hello latest job status and refresh hello screen.</span></span>

<span data-ttu-id="1f4c4-121">**toosee hello 출력**</span><span class="sxs-lookup"><span data-stu-id="1f4c4-121">**toosee hello output**</span></span>

1. <span data-ttu-id="1f4c4-122">**서버 탐색기**를 확장 하 고 **Azure**를 확장 하 고 **Data Lake 분석**, Data Lake 분석 계정, **저장소계정**hello 기본 저장소를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="1f4c4-123">샘플 및 출력을 확장하고 **Drivers.csv**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f4c4-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="1f4c4-124">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1f4c4-124">See also</span></span>
* [<span data-ttu-id="1f4c4-125">PowerShell을 사용하여 데이터 레이크 분석 시작하기</span><span class="sxs-lookup"><span data-stu-id="1f4c4-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="1f4c4-126">데이터 레이크 분석 hello Azure 포털을 사용 하 여 시작</span><span class="sxs-lookup"><span data-stu-id="1f4c4-126">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="1f4c4-127">U-SQL 응용 프로그램 개발에 Visual Studio용 데이터 레이크 도구 사용하기</span><span class="sxs-lookup"><span data-stu-id="1f4c4-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
