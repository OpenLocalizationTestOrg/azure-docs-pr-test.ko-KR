---
title: "Azure Data Lake Tools: Azure Data Lake Tools for Visual Studio Code 사용 | Microsoft Docs"
description: "Toouse Azure 데이터 레이크 Tools for Visual Studio Code toocreate 테스트 및 U-SQL 스크립트 실행 방법에 대해 알아봅니다. "
Keywords: "VScode, Azure 데이터 레이크 도구, 로컬 실행 로컬 디버그, 디버깅, 로컬 미리 보기 저장소 파일 업로드 toostorage 경로"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a>Azure Data Lake Tools for Visual Studio Code 사용

Toouse Azure 데이터 레이크 Tools for Visual Studio Code (VS Code) toocreate 테스트 및 U-SQL 스크립트 실행 방법에 대해 알아봅니다. hello 정보 비디오를 따라 hello에 대해서는:

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a>필수 조건

데이터 레이크 도구는 VS Code에서 지 원하는 hello 플랫폼에 설치할 수 있습니다. Windows, Linux 및 MacOS hello 지원 플랫폼에는 포함 합니다. hello 다른 플랫폼에는 다음 필수 구성 요소는 hello:

- Windows

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)
    - [Java SE Runtime Environment 버전 8 업데이트 77 이상](https://java.com/download/manual.jsp) - Hello java.exe 경로 toohello 시스템 환경 변수 경로 추가 합니다. 구성 지침은 [또는 하는 방법 설정 hello 경로 시스템 변수를 변경?]( https://www.java.com/download/help/path.xml)합니다. hello 경로가 tooC:\Program Files\Java\jdk1.8.0_77\jre\bin 유사 합니다.
    - [.NET Core SDK 1.0.3 또는 .NET Core 1.1 런타임](https://www.microsoft.com/net/download).
    
- Linux(Ubuntu 14.04 LTS 권장)

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx) tooinstall 코드 hello를 hello 다음 명령을 입력 합니다.

              sudo dpkg -i code_<version_number>_amd64.deb

    - [Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/) 

        - tooupdate hello deb 패키지 원본 hello 다음 명령을 입력 합니다.

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - 모노, tooinstall hello 다음 명령을 입력 합니다.

                sudo apt-get install mono-complete

            > [!NOTE] 
            > Mono 4.6은 지원되지 않습니다. 4.2.x 버전을 설치하기 전에 먼저 4.6 버전을 완전히 제거합니다.  

        - [Java SE Runtime Environment 버전 8 업데이트 77 이상](https://java.com/download/manual.jsp) - 설치 지침은 hello [Java에 대 한 Linux 64 비트 설치 지침]( https://java.com/en/download/help/linux_x64_install.xml) 페이지.
        - [.NET Core SDK 1.0.3 또는 .NET Core 1.1 런타임](https://www.microsoft.com/net/download).
- MacOS

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)
    - [Mono 4.2.4.x](http://download.mono-project.com/archive/4.2.4/macos-10-x86/) 
    - [Java SE Runtime Environment 버전 8 업데이트 77 이상](https://java.com/download/manual.jsp) - 설치 지침은 hello [Java에 대 한 Linux 64 비트 설치 지침](https://java.com/en/download/help/mac_install.xml) 페이지.
    - [.NET Core SDK 1.0.3 또는 .NET Core 1.1 런타임](https://www.microsoft.com/net/download).

## <a name="install-data-lake-tools"></a>Data Lake Tools 설치

Hello 필수 구성 요소를 설치한 후에 VS Code에 대 한 데이터 레이크 도구를 설치할 수 있습니다.

**데이터 레이크 도구 tooinstall**

1. Visual Studio Code를 엽니다.
2. Ctrl + P를 선택 하 고 다음 명령을 hello를 입력 하십시오.
```
ext install usql-vscode-ext
```
Visual Studio 코드 확장 목록을 볼 수 있습니다. 그 중 하나는 **Azure Data Lake Tools**입니다.

3. 선택 **설치** 다음 너무**Azure 데이터 레이크 도구**합니다. 몇 초 후 hello **설치** 너무 변경 단추**다시 로드**합니다.
4. 선택 **다시 로드** tooactivate hello 확장 합니다.
5. 선택 **확인** tooconfirm 합니다. Hello에서 Azure 데이터 레이크 도구를 볼 수 있듯이 **확장** 창.
    ![Data Lake Tools for Visual Studio Code 확장 창](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)

## <a name="activate-azure-data-lake-tools"></a>Azure Data Lake 도구 활성화
새.usql 파일을 만들거나 기존.usql 파일 tooactivate hello 확장을 엽니다. 

## <a name="connect-tooazure"></a>TooAzure 연결

컴파일 및 Data Lake 분석 U-SQL 스크립트를 실행할 수 있습니다, 전에 tooyour Azure 계정을 연결 해야 합니다.

**tooconnect tooAzure**

1.  Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다. 
2.  **ADL: Login**을 입력합니다. hello에 hello 로그인 정보가 표시 **출력** 창.

    ![Data Lake Tools for Visual Studio Code 명령 팔레트](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Data Lake Tools for Visual Studio Code 장치 로그인 정보](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)
3. 선택 Ctrl + 클릭 hello 로그인 URL: https://aka.ms/devicelogin tooopen hello 로그인 웹 페이지입니다. Hello 코드를 입력 **G567LX42V** hello 텍스트 상자를 선택한 후에 **계속**합니다.

   ![Data Lake Tools for Visual Studio Code 로그인 코드 붙여넣기](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  지침 toosign hello hello 웹 페이지에서 수행 합니다. Azure 계정 이름은 hello의 hello 왼쪽 아래 모서리에 hello 상태 표시줄에 표시 연결 되었을 때 **VS Code** 창. 

    > [!NOTE] 
    > 계정에 활성화된 두 가지 요인이 있는 경우 PIN을 사용하는 것보다 전화 인증을 사용하는 것이 좋습니다.

hello 명령을 입력 하는 아웃 toosign **ADL: 로그 아웃**합니다.

## <a name="list-your-data-lake-analytics-accounts"></a>Data Lake Analytics 계정 나열

Data Lake 분석 계정 목록이 가져오기 tootest hello 연결입니다.

**Azure 구독에서 toolist hello Data Lake 분석 계정**

1. Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.
2. **ADL: List Accounts**를 입력합니다. hello에 hello 계정 표시 **출력** 창.

## <a name="open-hello-sample-script"></a>열기 hello 샘플 스크립트
명령 팔레트 hello (Ctrl + Shift + P)를 열고 다음을 입력 **ADL: 열기 예제 스크립트**합니다. 그러면 이 샘플의 다른 인스턴스가 열립니다. 이 인스턴스에서 스크립트를 편집, 구성, 제출할 수도 있습니다.

## <a name="work-with-u-sql"></a>U-SQL 사용

U-SQL 파일 또는 폴더 toowork U-SQL으로 열 필요 있습니다.

**tooopen U-SQL 프로젝트에 대 한 폴더**

1. Visual Studio Code에서 선택 hello **파일** 메뉴를 선택한 후 **폴더 열기**합니다.
2. 폴더를 지정한 다음 **폴더 선택**을 선택합니다.
3. 선택 hello **파일** 메뉴를 선택한 후 **새로**합니다. 제목 없음 1 파일 toohello 프로젝트에 추가 됩니다.
4. Hello hello 제목 없음 1 파일에 코드를 다음을 입력 합니다.

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    hello 스크립트 hello /output 폴더에 포함 된 일부 데이터 departments.csv 파일을 만듭니다.

5. Hello 파일으로 저장 **myUSQL.usql** hello 폴더 열렸습니다. Adltools_settings.json 구성 파일에는 toohello 프로젝트도 추가 됩니다.
4. 페이지를 열고 다음과 같은 속성 hello를 사용 하 여 adltools_settings.json를 구성 합니다.

    - Account: Azure 구독에 있는 Data Lake Analytics 계정입니다.
    - Database: 사용자 계정의 데이터베이스입니다. hello 기본값은 **마스터**합니다.
    - Schema: 데이터베이스의 스키마입니다. hello 기본값은 **dbo**합니다.
    - 선택적 설정
        - 우선 순위: hello 우선 순위 범위는 1부터 1 too1000에서 hello 가장 높은 우선 순위입니다. hello 기본값은 **1000**합니다.
        - 병렬 처리: 1 too150에서 hello 병렬 처리 수준 범위가입니다. hello 기본값은 hello 최대 병렬 처리 Azure Data Lake 분석 계정에 사용할 수 있습니다. 
        
        > [!NOTE] 
        > Hello 설정이 유효 하지 않은 경우 hello 기본값이 사용 됩니다.

    ![Data Lake Tools for Visual Studio Code 구성 파일](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    Data Lake 분석 계정이 계산 필요 toocompile U-SQL 작업을 실행 합니다. 컴파일 및 U-SQL 작업을 실행 하기 전에 hello 컴퓨터 계정을 구성 해야 합니다.
    
Hello 구성 저장 된 후 hello 계정, 데이터베이스 및 스키마 정보 hello 해당.usql 파일의 hello 왼쪽 아래 모퉁이에 hello 상태 표시줄에 나타납니다. 
 
 
비교 tooopening 하면 폴더를 열 때 파일:

- 코드 숨김 파일 사용 코드 숨김은 hello 단일 파일 모드에서 지원 되지 않습니다.
- 구성 파일 사용 폴더를 열 때 hello 작업 폴더의에서 hello 스크립트는 단일 구성 파일을 공유 합니다.


U-SQL 스크립트 hello hello Data Lake 분석 서비스를 통해 원격으로 컴파일합니다. Hello를 실행 하면 **컴파일** 명령, hello U-SQL 스크립트 tooyour Data Lake 분석 계정에 전송 됩니다. 이상 버전에서는 Visual Studio Code hello 컴파일 결과를 받습니다. Toohello 원격 컴파일 인해 Visual Studio Code hello 구성 파일에 tooconnect tooyour Data Lake 분석 계정 hello 정보를 표시 하는 필요 합니다.

**toocompile는 U-SQL 스크립트**

1. Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다. 
2. **ADL:Compile Script**를 누릅니다. hello 컴파일 결과에 표시 hello **출력** 창. 또한 스크립트 파일을 마우스 오른쪽 단추로 클릭 하 고 다음 선택 **ADL: 컴파일 스크립트** toocompile는 U-SQL 작업 합니다. hello에 hello 컴파일 결과 표시 **출력** 창.
 

**toosubmit는 U-SQL 스크립트**

1. Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다. 
2. **ADL:Submit Job**을 누릅니다.  또한 스크립트 파일을 마우스 오른쪽 단추로 클릭한 다음 **ADL: Submit Job**을 선택할 수도 있습니다. 

Hello에 hello 전송 로그 표시 U-SQL 작업을 제출 하면 **출력** VS Code의 창. Hello 제출 되 면 hello 작업 URL이도 나타납니다. 웹 브라우저 tootrack hello 실시간 작업 상태에 hello 작업 URL을 열 수 있습니다.

hello 작업 세부 정보의 tooenable hello 출력 설정 **jobInformationOutputPath** hello에 **vs hello u sql_settings.json에 대 한 코드** 파일입니다.
 
## <a name="use-a-code-behind-file"></a>코드 숨김 파일 사용

코드 숨김 파일은 단일 U-SQL 스크립트와 연결되는 C# 파일입니다. 스크립트 전용 tooUDO, UDA, UDT 및 UDF hello 코드 숨김 파일에서 정의할 수 있습니다. hello UDO, UDA, UDT 및 UDF 용도 hello 스크립트에서 직접 hello 어셈블리를 먼저 등록 하지 않고 합니다. hello 코드 숨김 파일에에서 저장 됩니다 hello 동일 피어 링 U-SQL 스크립트 파일과 해당 폴더입니다. Hello 스크립트 xxx.usql 이름이 이면 hello 코드 숨김 xxx.usql.cs로 지정 됩니다. Hello 코드 숨김 파일을 수동으로 삭제 하면 관련된 U-SQL 스크립트에 대 한 코드 숨김 기능 hello 비활성화 됩니다. U-SQL 스크립트의 고객 코드 만들기에 대한 자세한 내용은 [U-SQL에서 사용자 지정 코드 만들기 및 사용: 사용자 정의 함수]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/)를 참조하세요.

toosupport 코드 숨김을 작업 폴더를 열어야 합니다. 

**toogenerate 코드 숨김 파일**

1. 원본 파일을 엽니다. 
2. Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.
3. **ADL:Generate Code Behind**를 누릅니다. 코드 숨김 파일을 만들 hello에 동일한 폴더입니다. 

또한 스크립트 파일을 마우스 오른쪽 단추로 클릭한 다음 **ADL: Generate Code Behind**를 선택할 수도 있습니다. 

toocompile 및 코드 숨김 파일과 함께 U-SQL 스크립트 hello 독립 실행형 U-SQL 스크립트 파일 같은 hello은 제출 합니다.

다음 두 가지 스크린샷입니다 hello 코드 숨김 파일 및 관련된 U-SQL 스크립트 파일을 보여 줍니다.
 
![Data Lake Tools for Visual Studio Code 코드 숨김](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools for Visual Studio Code 코드 숨김 스크립트 파일](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a>어셈블리 사용

어셈블리를 개발에 대한 정보는 [Azure Data Lake Analytics 작업에 U-SQL 어셈블리 개발](data-lake-analytics-u-sql-develop-assemblies.md)을 참조하세요.

Hello Data Lake 분석 카탈로그에 데이터 레이크 도구 tooregister 사용자 지정 코드 어셈블리를 사용할 수 있습니다.

**tooregister 어셈블리**

Hello 통해 hello 어셈블리를 등록할 수 **ADL: 어셈블리 등록** 또는 **ADL: 구성을 통해 어셈블리 등록** 명령입니다.

**hello ADL 통해 tooregister: 어셈블리 등록 명령**
1.  Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.
2.  **ADL:Register Assembly**를 입력합니다. 
3.  Hello 로컬 어셈블리 경로 지정 합니다. 
4.  Data Lake Analytics 계정을 선택합니다.
5.  데이터베이스를 선택합니다.

결과: hello 포털 브라우저에서 열 및 hello 어셈블리 등록 프로세스를 보여 줍니다.  

다른 편리 tootrigger hello **ADL: 어셈블리 등록** 명령 파일 탐색기에서 tooright 클릭 hello.dll 파일입니다. 

**tooregister에 있지만 ADL hello: 구성 명령을 통해 어셈블리 등록**
1.  Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.
2.  **ADL: Register Assembly through Configuration**을 입력합니다. 
3.  Hello 로컬 어셈블리 경로 지정 합니다. 
4.  hello JSON 파일이 표시 됩니다. 검토 하 고 필요한 경우 hello 어셈블리 종속성 및 리소스 매개 변수를 편집 합니다. 지침은 hello에 표시 됩니다 **출력** 창. tooproceed toohello 어셈블리 등록 (Ctrl + S) hello JSON 파일을 저장 합니다.

![Data Lake Tools for Visual Studio Code 코드 숨김](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- 어셈블리 종속성: Azure 데이터 레이크 도구 autodetects hello DLL의 모든 종속 관계에 있는지 여부. 감지 된 hello 종속성 hello JSON 파일에 표시 됩니다. 
>- 리소스: hello 어셈블리 등록의 일부로 DLL 리소스 (예:.txt,.png, 및.csv)을 업로드할 수 있습니다. 

또 다른 방법은 tootrigger hello **ADL: 구성을 통해 어셈블리 등록** 명령 파일 탐색기에서 tooright 클릭 hello.dll 파일입니다. 

hello U-SQL 코드 다음 방법을 보여 줍니다. 방법을 toocall 어셈블리입니다. Hello 샘플 hello 어셈블리 이름은 *테스트*합니다.

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a>액세스 hello Data Lake 분석 카탈로그

TooAzure에 연결한 후 다음 단계 tooaccess hello U-SQL 카탈로그 hello를 사용할 수 있습니다.

**tooaccess hello Azure Data Lake 분석 메타 데이터**

1.  Ctrl+Shift+P를 선택한 다음 **ADL: List Tables**를 입력합니다.
2.  Hello Data Lake 분석 계정 중 하나를 선택 합니다.
3.  Hello Data Lake 분석 데이터베이스 중 하나를 선택 합니다.
4.  Hello 스키마 중 하나를 선택 합니다. 테이블의 hello 목록을 볼 수 있습니다.

## <a name="view-data-lake-analytics-jobs"></a>Data Lake Analytics 작업 보기

**tooview Data Lake 분석 작업**
1.  명령 팔레트 hello (Ctrl + Shift + P)를 열고 선택 **ADL: 표시할 작업**합니다. 
2.  Data Lake Analytics 또는 로컬 계정을 선택합니다. 
3.  계정 tooappear hello에 대 한 hello 작업 목록에 대 한 대기입니다.
4.  작업 목록에서 작업을 선택, 데이터 레이크 도구 hello Azure 포털에서에서 작업 세부 정보를 hello 열리고 VS Code의 hello JobInfo 파일이 표시 됩니다.

![Data Lake Tools for Visual Studio Code IntelliSense 개체 형식](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a>Azure Data Lake Storage 통합

다음 작업에 Azure Data Lake Storage 관련 명령을 사용할 수 있습니다.
 - Hello Azure 데이터 레이크 저장소 리소스를 찾아봅니다. 
 - 미리 보기 hello Azure 데이터 레이크 저장소 파일입니다.  
 - Hello 업로드 VS 코드에서 직접 tooAzure 데이터 레이크 저장소 파일입니다. 

### <a name="list-hello-storage-path"></a>목록 hello 저장소 경로 
마우스 오른쪽 단추 클릭 또는 hello 명령 팔레트 통해 hello 저장소 경로 나열할 수 있습니다.

**hello 명령 팔레트를 통한 toolist hello 저장소 경로**

1.  명령 팔레트 hello (Ctrl + Shift + P)를 열고 다음을 입력 **ADL: 목록 저장소 경로**합니다.

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  Hello 저장소 경로 나열 하기 위한 기본적인된 방법 프로그램을 선택 합니다. 이 구절에서는 **Enter a path**를 예로 사용합니다.

    ![Visual Studio 코드는 한 가지 방법은 toolist hello 저장 경로 대 한 데이터 레이크 도구](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- VS Code 모든 Data Lake 분석 계정에 마지막으로 방문한 경로 hello를 유지합니다. 예: /tt/ss
    >- 브라우저에서 루트 경로: 선택한 Data Lake 분석 계정 또는 로컬 경로에서 hello 목록 루트 경로입니다.
    >- 경로 입력: 선택한 Data Lake Analytics 계정 또는 로컬 경로의 지정된 경로를 나열합니다.
    
3. Hello 로컬 경로 또는 Data Lake 분석 계정에서 계정을 선택 합니다.

    ![Data Lake Tools for Visual Studio Code more 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. 선택 **자세한** toolist 자세한 Data Lake 분석 계정 및 Data Lake 분석 계정 선택 합니다.

    ![Data Lake Tools for Visual Studio Code 계정 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  Azure 저장소 경로를 입력합니다. 예: /output

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로 입력](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  결과: hello 명령 팔레트에서 hello 경로 정보를 나열 합니다.

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로 결과 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

Hello를 통해 toolist hello에 대 한 상대 경로 보다 쉽게 단추로 상황에 맞는 메뉴를 클릭 합니다.

**toolist hello 저장 경로 통해 마우스 오른쪽 단추로 클릭**

1.  경로 문자열 tooselect hello를 마우스 오른쪽 단추로 클릭 **목록 저장소 경로**합니다.

       ![Data Lake Tools for Visual Studio Code에서 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. 상대 경로 선택된 하는 hello hello 명령 팔레트에 표시 됩니다.

   ![Data Lake Tools for Visual Studio Code에서 선택한 상대 경로](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  Hello 로컬 경로 또는 Data Lake 분석 계정에서 계정을 선택 합니다.

       ![Data Lake Tools for Visual Studio Code 계정 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  결과: hello 명령 팔레트 hello 폴더와 hello 현재 경로 대 한 파일을 나열 합니다.

       ![Hello 현재 경로에서 Visual Studio 코드 목록에 대 한 데이터 레이크 도구](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a>미리 보기 hello 저장소 파일
마우스 오른쪽 단추 클릭 또는 hello 명령 팔레트 통해 hello 저장소 파일을 미리 볼 수 있습니다.

**명령 팔레트 hello 통해 toopreview hello 저장소 파일**

1.  명령 팔레트 hello (Ctrl + Shift + P)를 열고 다음을 입력 **ADL: 미리 보기 저장소 파일**합니다.

       ![Data Lake Tools for Visual Studio Code에서 저장소 파일 미리 보기](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  Hello 로컬 경로 또는 Data Lake 분석 계정에서 계정을 선택 합니다.

       ![Data Lake Tools for Visual Studio Code에서 계정 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  선택 **자세한** toolist 자세한 Data Lake 분석 계정 및 Data Lake 분석 계정 선택 합니다.

       ![Data Lake Tools for Visual Studio Code 계정 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  Azure 저장소 경로 또는 파일을 입력합니다. 예: /output/SearchLog.txt

       ![Data Lake Tools for Visual Studio Code에서 저장소 경로 및 파일 입력](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  결과: hello 명령 팔레트에서 hello 경로 정보를 나열 합니다.

       ![Data Lake Tools for Visual Studio Code 파일 미리 보기 결과](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

**toolist hello 저장 경로 통해 마우스 오른쪽 단추로 클릭**

1.  파일을 toopreview 단추로 hello 파일 경로 클릭 합니다.

   ![Data Lake Tools for Visual Studio Code에서 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  Hello 로컬 경로 또는 Data Lake 분석 계정에서 계정을 선택 합니다.

       ![Data Lake Tools for Visual Studio Code 계정 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  결과: VS Code hello hello 파일의 결과 미리 보기를 표시합니다.

       ![Data Lake Tools for Visual Studio Code 파일 미리 보기 결과](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a>파일 업로드 

Hello 명령을 입력 하 여 파일을 업로드할 수 **ADL: 파일 업로드** 또는 **ADL: 구성을 통해 파일 업로드**합니다.

**tooupload 파일은 있지만 ADL hello: 파일 업로드 명령**
1. Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 하거나 hello 스크립트 편집기를 마우스 오른쪽 단추로 클릭 하 고 다음을 입력 **파일 업로드**합니다.
2.  tooupload hello 파일에서 로컬 경로 입력 합니다.

    ![Data Lake Tools for Visual Studio Code에서 로컬 경로 입력](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. 목록 hello 저장소 경로 hello 방법 중 하나를 선택 합니다. 이 구절에서는 **Enter a path**를 예로 사용합니다.

    ![Data Lake Tools for Visual Studio Code에서 저장소 경로 나열](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- VS Code 모든 Data Lake 분석 계정에 마지막으로 방문한 경로 hello를 유지합니다. 예: /tt/ss
    >- 브라우저에서 루트 경로: 선택한 Data Lake 분석 계정 또는 로컬 경로에서 hello 목록 루트 경로입니다.
    >- 경로 입력: 선택한 Data Lake Analytics 계정 또는 로컬 경로의 지정된 경로를 나열합니다.

4. Hello 로컬 경로 또는 Data Lake 분석 계정에서 계정을 선택 합니다.

    ![Data Lake Tools for Visual Studio Code에서 저장소를 마우스 오른쪽 단추로 클릭](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. Azure 저장소 경로를 입력합니다. 예: /output

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. Azure 저장소 경로를 찾습니다. **Choose current folder**를 선택합니다.

    ![Data Lake Tools for Visual Studio Code에서 폴더 선택](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  결과: hello **출력** hello 파일 업로드 상태 창에 표시 됩니다.

       ![Data Lake Tools for Visual Studio Code에서 상태 업로드](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

**tooupload 파일은 있지만 ADL hello: 구성 명령을 통해 파일 업로드**
1.  Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 하거나 hello 스크립트 편집기를 마우스 오른쪽 단추로 클릭 하 고 다음을 입력 **구성을 통해 파일 업로드**합니다.
2.  VS Code에서 JSON 파일을 표시합니다. 파일 경로 입력 하 고 hello에 여러 파일을 업로드할 수 있습니다 동시 합니다. 지침은 hello에 표시 됩니다 **출력** 창. tooproceed tooupload hello 파일 (Ctrl + S) hello JSON 파일을 저장 합니다.

       ![Data Lake Tools for Visual Studio Code 파일 경로](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  결과: hello **출력** hello 파일 업로드 상태 창에 표시 됩니다.

       ![Data Lake Tools for Visual Studio Code에서 상태 업로드](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

또 다른 방법은 tooupload 파일 toostorage hello 방식은 단추로 hello 파일의 전체 경로 또는 hello 파일의 상대 경로 hello 스크립트 편집기에 대 한 메뉴를 클릭 합니다. Hello 로컬 파일 경로 입력 한 다음 hello 계정을 선택 합니다. hello **출력** hello 업로드 상태 창에 표시 됩니다. 

### <a name="open-azure-storage-explorer"></a>Azure Storage Explorer 열기
열 수 **Azure 저장소 탐색기** hello 명령을 입력 하 여 **ADL: 웹 Azure 저장소 탐색기 열기** hello 오른쪽 클릭 상황에 맞는 메뉴에서 선택 하 여 합니다.

**Azure 저장소 탐색기 tooopen**

1. Ctrl + Shift + P tooopen hello 명령 팔레트를 선택 합니다.
2. 입력 **열려 있는 웹 Azure 저장소 탐색기** 또는 상대 경로 또는 hello hello 스크립트 편집기에서 전체 경로 마우스 오른쪽 단추로 클릭 한 다음 선택 **열려 있는 웹 Azure 저장소 탐색기**합니다.
3. Data Lake Analytics 계정을 선택합니다.

데이터 레이크 도구 hello Azure 포털에서에서 hello Azure 저장소 경로를 엽니다. Hello 경로 미리 보기 hello hello 웹 파일을 찾을 수 있습니다.

### <a name="local-run-and-local-debug-for-windows-users"></a>Windows 사용자에 대한 로컬 실행 및 로컬 디버그
로컬 데이터를 테스트 하 고 코드를 게시 된 tooData Lake 분석 하기 전에 로컬에서 스크립트의 유효성을 검사 하는 U-SQL 로컬 실행 합니다. hello 로컬 디버그 기능을 사용 하면 있습니다 toocomplete hello 코드 되기 전에 작업을 다음 tooData Lake 분석을 전송 합니다. 
- C# 코드 숨김을 디버그합니다. 
- Hello 코드를 단계별로 실행 합니다. 
- 로컬에서 스크립트의 유효성을 검사합니다.

로컬 실행 및 로컬 디버그에 대한 지침은 [Visual Studio Code로 U-SQL 로컬 실행 및 로컬 디버그](data-lake-tools-for-vscode-local-run-and-debug.md)를 참조하세요.

## <a name="additional-features"></a>추가 기능

VS Code에 대 한 데이터 레이크 도구 hello 같은 기능을 지원 합니다.

-   IntelliSense 자동 완성: 키워드, 메서드 및 변수와 같은 제안이 항목 주위의 팝업 창에 표시됩니다. 서로 다른 아이콘이 다양 한 유형의 hello 개체를 나타냅니다.

    - Scala 데이터 형식
    - 복합 데이터 형식
    - 기본 제공 UDT
    - .NET 컬렉션 및 클래스
    - C# 식
    - 기본 제공 C# UDF, UDO 및 UDAAG 
    - U-SQL 함수
    - U-SQL 창 작업 함수
 
    ![Data Lake Tools for Visual Studio Code IntelliSense 개체 형식](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   데이터 레이크 분석 메타 데이터에 자동 완성 IntelliSense: 데이터 레이크 도구 hello Data Lake 분석 메타 데이터 정보를 로컬로 다운로드 합니다. hello IntelliSense 기능은 자동으로 hello 데이터베이스, 스키마, 테이블, 뷰, 테이블 반환 함수, 프로시저 및 hello Data Lake 분석 메타 데이터에서 C# 어셈블리를 포함 하 여 개체를 채웁니다.
 
    ![Data Lake Tools for Visual Studio Code IntelliSense 메타데이터](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   IntelliSense 오류 표식: 데이터 레이크 도구 U-SQL 및 C#에 대 한 오류를 편집 하는 hello에 밑줄을 표시 합니다. 
-   구문 강조 표시: 변수, 키워드, 데이터 형식 및 함수 등의 서로 다른 색 toodifferentiate 항목을 사용 하 여 데이터 레이크 도구입니다. 

    ![Data Lake Tools for Visual Studio Code 구문 강조 표시](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>다음 단계

- Visual Studio Code로 U-SQL 로컬 실행 및 로컬 디버그는 [Visual Studio Code로 U-SQL 로컬 실행 및 로컬 디버그](data-lake-tools-for-vscode-local-run-and-debug.md)를 참조하세요.
- Data Lake Analytics 시작 정보는 [자습서: Azure Data Lake Analytics 시작](data-lake-analytics-get-started-portal.md)을 참조하세요.
- Data Lake Tools for Visual Studio에 대한 자세한 내용은 [자습서: Data Lake Tools for Visual Studio를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 참조하세요.
- 어셈블리를 개발에 대한 정보는 [Azure Data Lake Analytics 작업에 U-SQL 어셈블리 개발](data-lake-analytics-u-sql-develop-assemblies.md)을 참조하세요.



