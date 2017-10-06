---
title: "Azure Data Lake Tools: Visual Studio Code를 사용한 U-SQL 로컬 실행 및 로컬 디버그 | Microsoft Docs"
description: "Visual Studio Code toolocal 및 로컬 실행에 대 한 Azure 데이터 레이크 도구 toouse 디버깅 하는 방법에 대해 알아봅니다."
Keywords: "VScode, Azure 데이터 레이크 도구, 로컬 실행 로컬 디버그, 디버깅, 로컬 미리 보기 저장소 파일 업로드 toostorage 경로"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a>Visual Studio Code로 U-SQL 로컬 실행 및 로컬 디버그

## <a name="prerequisites"></a>필수 조건
이러한 절차를 시작 하기 전에 필수 구성 요소가 충족 다음 hello 있는지 확인 합니다.
- Azure Data Lake Tool for Visual Studio Code. 자세한 내용은 [Azure Data Lake Tools for Visual Studio Code 사용](data-lake-analytics-data-lake-tools-for-vscode.md)을 참조하세요.
- C# Visual Studio Code (tooperform U SQL 로컬 디버그 경우)에 대 한 합니다.

   ![Data Lake Tools for Visual Studio Code에 C# 설치](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > hello U-SQL 로컬 실행 및 디버그 기능 현재만 지원 Windows 사용자입니다. 


## <a name="set-up-hello-u-sql-local-run-environment"></a>Hello U-SQL 로컬 실행된 환경 설정

1. Ctrl + Shift + P tooopen hello 명령 팔레트를 선택한 다음 입력 **ADL: LocalRun 종속성 다운로드** toodownload hello 패키지 합니다.  

   ![Hello ADL LocalRun 종속성 패키지를 다운로드 합니다.](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. Hello 종속성 패키지가 hello에 표시 된 hello 경로에서 찾은 **출력** 창에서 한 다음 BuildTools 및 Win10SDK 10240 설치 합니다. 다음은 예제 경로입니다.  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  ![Hello 종속성 패키지 찾기](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)

   a. tooinstall BuildTools, hello 마법사의 지시를 따릅니다.   

  ![BuildTools 설치](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   b. tooinstall Win10SDK 10240 hello 마법사의 지시를 따릅니다.  

  ![Win10SDK 10240 설치](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. Hello 환경 변수를 설정 합니다. 집합 hello **SCOPE_CPP_SDK** 환경 변수를:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. Hello OS toomake hello 환경 변수 설정이 적용 되었는지 다시 시작 합니다.  

   ![Hello SCOPE_CPP_SDK 환경 변수에서 설치 되어 있는지 확인](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a>Hello 로컬 실행된 서비스를 시작 하 고 hello tooa 로컬 계정 U-SQL 작업 제출 
Hello 처음 사용자에 대 한 증명된 toodownload hello ADL 중인: LocalRun 종속성 다운로드를 아직 설치 되지 않은 경우 패키지 합니다.
1. Ctrl + Shift + P tooopen hello 명령 팔레트를 선택한 다음 입력 **ADL: 로컬 실행 서비스 시작**합니다.
2. 선택 **Accept** tooaccept hello 처음으로 hello에 대 한 Microsoft 소프트웨어 사용 조건. 

   ![Hello Microsoft 소프트웨어 사용 조건에 동의](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. hello cmd 콘솔이 열립니다. 신규 사용자 tooenter 필요 **3**, 입력 및 출력 데이터에 대 한 hello 로컬 폴더 경로 찾습니다. 다른 옵션에 대 한 hello 기본값을 사용할 수 있습니다. 

   ![Data Lake Tools for Visual Studio Code가 cmd 로컬 실행](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. Ctrl + Shift + P tooopen hello 명령 색상표를 선택, 입력 **ADL: 작업 제출**를 선택한 후 **로컬** toosubmit hello 작업 tooyour 로컬 계정.

   ![Data Lake Tools for Visual Studio Code 로컬 선택](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. Hello 작업을 제출 하면 hello 제출 세부 정보를 볼 수 있습니다. 선택 tooview hello 전송에 자세히 설명 **jobUrl** hello에 **출력** 창. Hello cmd 콘솔에서 hello 작업 전송 상태를 볼 수 있습니다. 입력 **7** hello cmd 콘솔에서 tooknow 하려는 경우 자세한 작업 정보입니다.

   ![Data Lake Tools for Visual Studio Code 로컬 실행 출력](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake Tools for Visual Studio Code 로컬 실행 cmd 상태](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png) 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a>Hello U-SQL 작업에 대 한 로컬 디버그를 시작 합니다.  
Hello 처음 사용자에 대 한 증명된 toodownload hello ADL 중인: LocalRun 종속성 다운로드를 아직 설치 되지 않은 경우 패키지 합니다.
  
1. Ctrl + Shift + P tooopen hello 명령 팔레트를 선택한 다음 입력 **ADL: 로컬 실행 서비스 시작**합니다. hello cmd 콘솔이 열립니다. 해당 hello 있는지 확인 **DataRoot** 설정 됩니다.
3. C# 코드 숨김에서 중단점을 설정합니다.
4. Hello 스크립트 편집기에서 다시 Ctrl + Shift + P tooopen hello 명령 콘솔을 선택 하 고 다음을 입력 **로컬 디버그** toostart 로컬 디버그 서비스입니다.

![Data Lake Tools for Visual Studio Code 로컬 디버그 결과](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a>다음 단계
- Azure Data Lake Tools for Visual Studio Code 사용에 대해서는 [Azure Data Lake Tools for Visual Studio Code 사용](data-lake-analytics-data-lake-tools-for-vscode.md)을 참조하세요.
- Data Lake Analytics 시작 정보는 [자습서: Azure Data Lake Analytics 시작](data-lake-analytics-get-started-portal.md)을 참조하세요.
- Data Lake Tools for Visual Studio에 대한 자세한 내용은 [자습서: Data Lake Tools for Visual Studio를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 참조하세요.
- Hello에 대 한 내용은 어셈블리를 개발, [Azure 데이터 레이크 분석 작업에 대 한 개발 U-SQL 어셈블리](data-lake-analytics-u-sql-develop-assemblies.md)합니다.
