---
title: "Azure 데이터 레이크 분석 작업에 대 한 aaaDevelop U-SQL 어셈블리 | Microsoft Docs"
description: "Toodevelop 어셈블리 toobe 사용 하 고 작업을 다시 Data Lake 분석에 사용 하는 방법에 대해 알아봅니다. "
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
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a>Azure Data Lake Analytics 작업용 U-SQL 어셈블리 개발
어떻게 tooturn 코드 숨김을 사용 하 고 데이터 레이크 분석 작업에 사용할 어셈블리 toobe에 알아봅니다. 

U-SQL C#, VB.Net 또는 F # 같은.Net 언어에서 고유한 사용자 지정 코드는 쉽게 tooadd가 있도록 합니다. 도 다른 언어 사용자 고유의 런타임 toosupport를 배포할 수 있습니다.

hello 가장 쉬운 방법은 toouse 사용자 지정 코드는 Visual Studio의 코드 숨김 기능에 대 한 toouse hello 데이터 레이크 도구입니다. 자세한 내용은 [자습서: Visual Studio용 Data Lake 도구를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 참조하세요. 코드 숨김 사용에는 다음 몇 가지 단점이 있습니다.

- 모든 스크립트 전송용 hello 소스 코드 업로드를 가져옵니다.
- 코드 숨김은 다른 작업과 공유할 수 없습니다.

tooaddress 이러한 단점은 어셈블리에 코드 숨김을 설정 하 고 hello 어셈블리 toohello Data Lake 분석 카탈로그를 등록할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
* Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 업데이트 4 또는 Visual Studio 2012와 Visual C++ 설치
* Microsoft Azure SDK for.NET 버전 2.5 이상.  Hello 웹 플랫폼 설치 관리자 또는 Visual Studio 설치 관리자를 사용 하 여 설치
* 데이터 레이크 분석 계정입니다.  [Azure Portal을 사용하여 Azure Data Lake Analytics 시작](data-lake-analytics-get-started-portal.md)을 참조하세요.
* Hello를 통해 이동 [Azure 데이터 레이크 분석 U-SQL 스튜디오 시작](data-lake-analytics-u-sql-get-started.md) 자습서입니다.
* TooAzure를 연결 합니다.
* Hello 원본 데이터를 업로드, 참조 [Azure 데이터 레이크 분석 U-SQL 스튜디오 시작](data-lake-analytics-u-sql-get-started.md)합니다. 

## <a name="develop-assemblies-for-u-sql"></a>U-SQL용 어셈블리 개발

**toocreate U-SQL 작업을 제출 하 고**

1. Hello에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.
2. 확장 **설치 됨**, **템플릿**, **Azure 데이터 레이크**, **U-SQL(ADLA)**선택, hello **클래스 라이브러리 (에 대 한 U-SQL 응용 프로그램)** 템플릿과 클릭 **확인**합니다.
3. Class1.cs에서 코드를 작성합니다.  hello 다음 코드 샘플입니다.

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
4. Hello 클릭 **빌드** 메뉴를 차례로 클릭 **솔루션 빌드** toocreate hello dll입니다.

## <a name="register-assemblies"></a>어셈블리 등록

[Data Lake Analytics(U-SQL) 카탈로그 사용](data-lake-analytics-use-u-sql-catalog.md)을 참조하세요.


## <a name="use-hello-assemblies"></a>Hello 어셈블리 사용

참조 [hello Azure 데이터 레이크 도구를 사용 하 여 Visual Studio 코드에 대 한](data-lake-analytics-data-lake-tools-for-vscode.md)합니다.

## <a name="see-also"></a>참고 항목
* [PowerShell을 사용하여 데이터 레이크 분석 시작하기](data-lake-analytics-get-started-powershell.md)
* [데이터 레이크 분석 hello Azure 포털을 사용 하 여 시작](data-lake-analytics-get-started-portal.md)
* [U-SQL 응용 프로그램 개발에 Visual Studio용 데이터 레이크 도구 사용하기](data-lake-analytics-data-lake-tools-get-started.md)
* [Data Lake Analytics(U-SQL) 카탈로그 사용](data-lake-analytics-use-u-sql-catalog.md)
* [Visual Studio 코드에 대 한 hello Azure 데이터 레이크 도구를 사용 합니다.](data-lake-analytics-data-lake-tools-for-vscode.md)
