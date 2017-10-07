---
title: "aaaAzure 함수 런타임 설치 | Microsoft Docs"
description: "TooInstall은 Azure 함수 런타임 hello 하는 방법"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a>Hello Azure 함수 런타임 미리 보기 설치

Tooinstall hello Azure 함수 런타임 미리 보기를 원하는 경우 이러한 단계를 수행 해야 합니다.

1. 컴퓨터 전달 hello 최소 요구 사항을 확인 하십시오.
1. Hello 다운로드 [Azure 함수 런타임 Preview 설치 관리자](https://aka.ms/azafr)합니다. 
1. Hello Azure 함수 런타임 미리 보기 설치
1. Hello Azure 함수 런타임 미리 보기의 전체 hello 구성

## <a name="prerequisites"></a>필수 조건

Hello Azure 함수 런타임 미리 보기를 설치 하기 전에 hello 다음이 있어야 합니다.

1. Microsoft Windows Server 2016 또는 Microsoft Windows 10 작성자 업데이트(Professional 또는 Enterprise Edition)를 실행하는 컴퓨터
1. 네트워크 내에서 실행되는 SQL Server 인스턴스.  최소 버전 요구 사항은 SQL Server Express입니다.

## <a name="install-hello-azure-functions-runtime-preview"></a>Hello Azure 함수 런타임 미리 보기 설치

hello Azure 함수 런타임 preview 설치 관리자 hello Azure 함수 런타임 미리 보기 관리 및 작업자 역할의 hello 설치 과정을 안내합니다.  가능한 tooinstall hello 관리 되며 작업자 역할 hello에 동일한 컴퓨터.  그러나 다른 함수를 추가 하면 배포한 toobe 수 tooscale 추가 컴퓨터에 더 많은 작업자 역할에 여러 worker 함수.

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a>Hello에 hello 관리 및 작업자 역할을 설치 동일한 컴퓨터

1. Hello Azure 함수 런타임 Preview 설치 관리자를 실행 합니다.

    ![Azure Functions 런타임 미리 보기 설치 관리자][1]

1. **다음을 클릭** hello 설치 관리자의 첫 번째 단계 hello 지난 사전
1. Hello hello 약관을 읽은 후 **EULA**, **hello 확인란** tooaccept hello 용어 및 **다음 클릭** tooadvance 합니다.
1. 이 컴퓨터에 tooinstall 원하는 선택 hello 역할 이제 **함수 관리 역할** 및/또는 **함수 작업자 역할** 및 **"다음" 클릭**

    ![Azure Functions 런타임 미리 보기 설치 관리자 - 역할 선택][3]

    > [!NOTE]
    > Hello를 설치할 수 있습니다 **함수 작업자 역할** 다른 많은 컴퓨터 toodo에서, 다음이 지침에 따라 한만 선택 **함수 작업자 역할** hello 설치 관리자에서 합니다.

1. **다음을 클릭** toohave hello **Azure 함수에 대 한 런타임 설치 관리자** 컴퓨터에 설치 합니다.
1. 전체 hello 설치 관리자가 hello 시작 되 면 **Azure 함수 런타임 구성 도구**합니다.

    ![Azure Functions 런타임 미리 보기 설치 관리자 완료][5]

    > [!NOTE]
    > 에 설치 하는 경우 **Windows 10** 및 hello **컨테이너** 기능이 활성화 되지 않은 이전에, hello **Azure 함수 런타임** 설치 관리자 묻는 tooreboot 컴퓨터 toocomplete hello를 설치 합니다.

## <a name="configure-hello-azure-functions-runtime"></a>Hello Azure 함수 런타임 구성

toocomplete hello Azure 함수 런타임 설치 hello 구성을 완료 해야 합니다.

1. hello **Azure 함수 런타임 구성 도구** 컴퓨터에 설치 된 역할을 보여 줍니다.

    ![Azure Functions 런타임 미리 보기 구성 도구][6]

1. Hello 클릭 **데이터베이스** 탭을 hello 입력 **SQL Server 인스턴스에 대 한 연결 세부 정보** 및 **적용을 클릭**합니다.  이 순서 toohello Azure 함수 런타임 toocreate 데이터베이스 toosupport hello 런타임 필요 합니다.
    
    ![Azure Functions 런타임 미리 보기 데이터베이스 구성][7]

1. Hello 클릭 **자격 증명** 탭 합니다.  이 화면에서 모든 Azure Functions를 호스트하기 위해 FileShare에서 사용할 2개의 새 자격 증명을 만들어야 합니다.  **사용자 이름 및 암호 지정** hello에 대 한 조합을 **파일 공유 소유자** 및 hello에 대 한 **파일 공유 사용자** 클릭 **적용**합니다.

    ![Azure Functions 런타임 미리 보기 자격 증명][8]

1. Hello 클릭 **파일 공유** 탭 합니다.  이 화면에서의 hello hello 세부 정보를 지정 해야 **파일 공유 위치**합니다.  이 위치가 자동으로 생성될 수도 있고 기존 파일 공유를 사용하고 **적용**을 클릭할 수도 있습니다.  새 파일 공유 위치를 선택 하는 경우에 hello Azure 함수 런타임 하 여 사용에 대 한 디렉터리를 지정 해야 합니다.
    
    ![Azure Functions 런타임 미리 보기 파일 공유][9]

1. Hello 클릭 **IIS** 탭 합니다.  이 탭에는 Azure 함수 런타임 설치 만듭니다 해당 hello IIS에서 hello 웹 사이트의 hello 세부 정보 표시 합니다.  **적용을 클릭** toocomplete 합니다.

    ![Azure Functions 런타임 미리 보기 IIS][10]

1. Hello 클릭 **서비스** 탭 합니다.  이 탭 Azure 함수 런타임 설치에서 hello 서비스의 hello 상태를 표시 합니다.  초기 구성 hello after **Azure 함수 호스트 정품 인증 서비스** 클릭을 실행 하지 않는 **서비스 시작**

    ![Azure Functions 런타임 미리 보기 구성 완료][11]

1. 마지막으로 toohello 찾아보기 **Azure 함수 런타임 포털** 으로`https://<machinename>/`

    ![Azure Functions 런타임 미리 보기 포털][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png