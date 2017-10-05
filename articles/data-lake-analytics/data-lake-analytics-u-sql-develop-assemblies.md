---
title: "Azure Data Lake Analytics 작업용 U-SQL 어셈블리 개발 | Microsoft Docs"
description: "Data Lake Analytics 작업에 사용 및 재사용되는 어셈블리를 개발하는 방법을 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: c49f80f8dcd330d7f46726241e7178351b9cc28f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="5e31e-103">Azure Data Lake Analytics 작업용 U-SQL 어셈블리 개발</span><span class="sxs-lookup"><span data-stu-id="5e31e-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="5e31e-104">코드 숨김을 Data Lake Analytics 작업에 사용 및 재사용되는 어셈블리로 전환하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-104">Learn how to turn code-behind into assemblies to be used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="5e31e-105">U-SQL을 사용하면 C#, VB.Net 또는 F# 등의 .Net 언어로 사용자 고유의 사용자 지정 코드를 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-105">U-SQL makes it easy to add your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="5e31e-106">사용자 고유의 런타임을 배포하여 다른 언어를 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-106">You can even deploy your own runtime to support other languages.</span></span>

<span data-ttu-id="5e31e-107">사용자 지정 코드를 사용하는 가장 쉬운 방법은 Visual Studio의 코드 숨김 기능을 위해 Data Lake 도구를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-107">The easiest way to use custom code is to use the Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="5e31e-108">자세한 내용은 [자습서: Visual Studio용 Data Lake 도구를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e31e-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="5e31e-109">코드 숨김 사용에는 다음 몇 가지 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="5e31e-110">스크립트를 제출할 때마다 소스 코드가 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-110">The source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="5e31e-111">코드 숨김은 다른 작업과 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="5e31e-112">이러한 단점을 해결하기 위해 코드 숨김을 어셈블리로 전환하고 Data Lake Analytics 카탈로그에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-112">To address these drawbacks, you can turn code-behind into assemblies, and register the assemblies to the Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e31e-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5e31e-113">Prerequisites</span></span>
* <span data-ttu-id="5e31e-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 업데이트 4 또는 Visual Studio 2012와 Visual C++ 설치</span><span class="sxs-lookup"><span data-stu-id="5e31e-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="5e31e-115">Microsoft Azure SDK for.NET 버전 2.5 이상.</span><span class="sxs-lookup"><span data-stu-id="5e31e-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="5e31e-116">웹 플랫폼 설치 관리자 또는 Visual Studio 설치 관리자를 사용하여 설치</span><span class="sxs-lookup"><span data-stu-id="5e31e-116">Install it using the Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="5e31e-117">데이터 레이크 분석 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="5e31e-118">[Azure Portal을 사용하여 Azure Data Lake Analytics 시작](data-lake-analytics-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e31e-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="5e31e-119">[AZure 데이터 레이크 분석 U-SQL 스튜디오 시작하기](data-lake-analytics-u-sql-get-started.md) 자습서를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="5e31e-119">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="5e31e-120">Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="5e31e-120">Connect to Azure.</span></span>
* <span data-ttu-id="5e31e-121">원본 데이터 업로드는 [Azure Data Lake Analytics U-SQL 스튜디오 시작하기](data-lake-analytics-u-sql-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e31e-121">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="5e31e-122">U-SQL용 어셈블리 개발</span><span class="sxs-lookup"><span data-stu-id="5e31e-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="5e31e-123">**U-SQL 작업을 만들고 제출하기**</span><span class="sxs-lookup"><span data-stu-id="5e31e-123">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="5e31e-124">**파일** 메뉴에서 **새로 만들기**를 클릭한 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-124">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="5e31e-125">**설치됨**, **템플릿**, **Azure Data Lake**, **U-SQL(ADLA)**을 확장하고 **클래스 라이브러리(U-SQL 응용 프로그램용)** 템플릿을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select the **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="5e31e-126">Class1.cs에서 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="5e31e-127">다음은 코드 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-127">The following is a code sample.</span></span>

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. <span data-ttu-id="5e31e-128">**빌드** 메뉴를 클릭한 다음 **솔루션 빌드**를 클릭하여 dll을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e31e-128">Click the **Build** menu, and then click **Build Solution** to create the dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="5e31e-129">어셈블리 등록</span><span class="sxs-lookup"><span data-stu-id="5e31e-129">Register assemblies</span></span>

<span data-ttu-id="5e31e-130">[Data Lake Analytics(U-SQL) 카탈로그 사용](data-lake-analytics-use-u-sql-catalog.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e31e-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-the-assemblies"></a><span data-ttu-id="5e31e-131">어셈블리 사용</span><span class="sxs-lookup"><span data-stu-id="5e31e-131">Use the assemblies</span></span>

<span data-ttu-id="5e31e-132">[Azure Data Lake Tools for Visual Studio Code 사용](data-lake-analytics-data-lake-tools-for-vscode.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e31e-132">See [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5e31e-133">참고 항목</span><span class="sxs-lookup"><span data-stu-id="5e31e-133">See also</span></span>
* [<span data-ttu-id="5e31e-134">PowerShell을 사용하여 데이터 레이크 분석 시작하기</span><span class="sxs-lookup"><span data-stu-id="5e31e-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="5e31e-135">Azure 포털을 사용하여 데이터 레이크 분석 시작하기</span><span class="sxs-lookup"><span data-stu-id="5e31e-135">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="5e31e-136">U-SQL 응용 프로그램 개발에 Visual Studio용 데이터 레이크 도구 사용하기</span><span class="sxs-lookup"><span data-stu-id="5e31e-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="5e31e-137">Data Lake Analytics(U-SQL) 카탈로그 사용</span><span class="sxs-lookup"><span data-stu-id="5e31e-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="5e31e-138">Azure Data Lake Tools for Visual Studio Code 사용</span><span class="sxs-lookup"><span data-stu-id="5e31e-138">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)