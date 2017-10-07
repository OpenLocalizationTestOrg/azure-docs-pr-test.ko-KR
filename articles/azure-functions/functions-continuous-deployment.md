---
title: "Azure 기능에 대 한 aaaContinuous 배포 | Microsoft Docs"
description: "Azure 앱 서비스 toopublish의 연속 배포 기능이 Azure 기능을 사용 합니다."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a>Azure Functions에 대한 연속 배포
Azure 기능 사용 하면 쉽게 toodeploy 앱 서비스 연속 통합을 사용 하 여 함수 앱. Functions는 BitBucket, Dropbox, GitHub 및 VSTS(Visual Studio Team Services)와 통합됩니다. 이렇게 하면 이러한 통합된 서비스 트리거 배포 tooAzure 중 하나를 사용 하 여 워크플로 함수의 코드를 업데이트 합니다. 로 시작 하는 새로운 tooAzure 함수 인 경우 [Azure 함수 개요](functions-overview.md)합니다.

연속 배포는 여러 개의 빈번한 작성자가 통합되는 프로젝트에 적합한 옵션입니다. 또한 함수 코드에서 소스 제어를 유지 관리할 수 있습니다. 배포 원본 hello는 현재 지원 됩니다.

* [Bitbucket](https://bitbucket.org/)
* [Dropbox](https://www.dropbox.com/)
* 외부 리포지토리(Git 또는 Mercurial)
* [Git 로컬 리포지토리](../app-service-web/app-service-deploy-local-git.md)
* [GitHub](https://github.com)
* [OneDrive](https://onedrive.live.com/)
* [Visual Studio Team Services](https://www.visualstudio.com/team-services/)

배포는 함수 앱별로 구성됩니다. Hello 포털에 액세스 toofunction 코드 너무 설정 연속 배포를 사용 하도록 설정한 후*읽기 전용*합니다.

## <a name="continuous-deployment-requirements"></a>연속 배포 요구 사항

연속 배포를 설정 하기 전에 hello 배포 원본에 구성 된 배포 소스와 함수 코드 있어야 합니다. 지정 된 함수 앱 배포의 각 함수 hello 디렉터리 이름을 hello 함수 hello 이름을 인 명명 된 하위 디렉터리에서 실행 됩니다.  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a>연속 배포 설정
이 절차 tooconfigure 연속 배포를 사용 하 여 기존 함수 앱에 대 한 합니다. 다음 단계에서는 GitHub 리포지토리와의 통합을 보여 주지만 Visual Studio Team Services 또는 기타 배포 서비스에도 유사한 단계가 적용됩니다.

1. Hello 함수 앱에서 [Azure 포털](https://portal.azure.com), 클릭 **플랫폼 기능** 및 **배포 옵션**합니다. 
   
    ![연속 배포 설정](./media/functions-continuous-deployment/setup-deployment.png)
 
2. 그런 다음 hello **배포** 블레이드 클릭 **설치**합니다.
 
    ![연속 배포 설정](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. Hello에 **배포 원본을** 블레이드에서 클릭 **선택 소스**선택한 배포 원본에 대 한 hello 정보를 입력 한 다음을 클릭 **확인**합니다.
   
    ![배포 원본 선택](./media/functions-continuous-deployment/choose-deployment-source.png)

연속 배포를 구성한 후에 모든 파일 변경 내용 배포 원본에는 복사 toohello 함수 앱을 전체 사이트 배포 트리거됩니다. hello 원본 파일을 업데이트할 때 hello 사이트를 다시 배포 합니다.

## <a name="deployment-options"></a>배포 옵션

hello 다음은 몇 가지 일반적인 배포 시나리오입니다.

- [스테이징 배포 만들기](#staging)
- [기존 함수 toocontinuous 배포 이동](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a>스테이징 배포 만들기

함수 앱은 배포 슬롯을 지원하지 않습니다. 그러나 연속 통합을 사용하여 별도 스테이징 및 프로덕션 배포를 계속 관리할 수 있습니다.

프로세스 tooconfigure hello 및 스테이징 배포를 다루는 일반적으로 다음과 같습니다.

1. Hello 프로덕션 코드 및 준비에 대 한 구독에서 두 개의 기능 앱을 만듭니다. 

2. 아직 없는 경우 배포 원본을 만듭니다. 이 예제에서는 [GitHub]를 사용합니다.

3. 단계를 완료 하는 hello 이전 프로덕션 함수 앱에 대 한 **연속 배포 설정** 및 집합 hello 배포 분기 toohello 마스터 분기 GitHub 리포지토리에 합니다.
   
    ![배포 분기 선택](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. 함수 앱을 준비 하는 hello에 대 한이 단계를 반복 하지만 GitHub 리포지토리에 있는 대신 분기를 준비 하는 hello를 선택 합니다. 배포 원본이 분기를 지원하지 않는 경우 다른 폴더를 사용합니다.
    
5. 분기 또는 폴더를 준비 하는 hello에 업데이트 tooyour 코드를 확인 한 후 hello 스테이징 배포에에서 이러한 변경 내용이 반영 되었는지 확인 합니다.

6. 테스트를 마친 후 hello 마스터 분기에 병합 hello 준비 분기에서 변경 합니다. 이 병합 toohello 프로덕션 함수 응용 프로그램을 배포를 트리거합니다. 배포 소스 분기를 지원 하지 않으면 hello 준비 폴더의에서 hello 파일로 hello 프로덕션 폴더에 hello 파일을 덮어씁니다.

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a>기존 함수 toocontinuous 배포 이동
기존 함수를 만들고 필요한 toodownload hello 포털에서 유지 관리 하는 경우 위에서 설명한 것 처럼 연속 배포를 설정 하려면 먼저 FTP 또는 hello 로컬 Git 리포지토리를 사용 하 여 코드 파일 함수 기존 합니다. 이렇게 하려면 hello에 응용 프로그램 서비스 설정을 함수 앱에 대 한 합니다. 파일을 다운로드 한 후 선택한 tooyour 연속 배포 원본을 업로드할 수 있습니다.

> [!NOTE]
> 연속 통합을 구성 하면 더 이상 됩니다 수 tooedit hello 함수 포털에서 소스 파일.

- [방법: 배포 자격 증명 구성](#credentials)
- [방법: FTP를 사용하여 파일 다운로드](#downftp)
- [방법: hello 로컬 Git 리포지토리를 사용 하 여 파일 다운로드](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a>방법: 배포 자격 증명 구성
FTP 또는 로컬 Git 리포지토리를 사용 하 여 함수 앱에서 파일을 다운로드할 수 있습니다, 전에 자격 증명 tooaccess hello 사이트를 구성 해야 합니다. 자격 증명 hello 함수 앱 수준에서 설정 됩니다. Hello Azure 포털에서에서 tooset 배포 자격 증명 단계를 수행 하는 hello를 사용 합니다.

1. Hello 함수 앱에서 [Azure 포털](https://portal.azure.com), 클릭 **플랫폼 기능** 및 **배포 자격 증명**합니다.
   
    ![로컬 배포 자격 증명 설정](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. 사용자 이름 및 암호를 입력한 다음 **저장**을 클릭합니다. 이제 이러한 자격 증명 tooaccess 함수 앱 FTP 또는 hello의 기본 제공 Git 리포지토리에서 사용할 수 있습니다.

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a>방법: FTP를 사용하여 파일 다운로드

1. Hello 함수 앱에서 [Azure 포털](https://portal.azure.com), 클릭 **플랫폼 기능** 및 **속성**, 다음에 대 한 hello 값을 복사 **P/배포 사용자**, **FTP 호스트 이름**, 및 **FTPS 호스트 이름**합니다.  

    **P/배포 사용자** hello 응용 프로그램 이름, tooprovide hello FTP 서버에 대 한 적절 한 컨텍스트를 포함 하 여 hello 포털에 표시 된 대로 입력 해야 합니다.
   
    ![배포 정보 가져오기](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. FTP 클라이언트에서 수집한 tooconnect tooyour 앱 hello 연결 정보를 사용 하 고 함수에 대 한 hello 소스 파일을 다운로드 합니다.

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a>방법: 로컬 Git 리포지토리를 사용하여 파일 다운로드

1. Hello 함수 앱에서 [Azure 포털](https://portal.azure.com), 클릭 **플랫폼 기능** 및 **배포 옵션**합니다. 
   
    ![연속 배포 설정](./media/functions-continuous-deployment/setup-deployment.png)
 
2. 그런 다음 hello **배포** 블레이드 클릭 **설치**합니다.
 
    ![연속 배포 설정](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. Hello에 **배포 원본을** 블레이드에서 클릭 **로컬 Git 리포지토리** 클릭 하 고 **확인**합니다.

3. **플랫폼 기능**, 클릭 **속성** Git URL의 hello 값을 확인 합니다. 
   
    ![연속 배포 설정](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. 인식 Git 명령 프롬프트 또는 임의의 Git 도구를 사용 하 여 로컬 컴퓨터의 hello 리포지토리를 복제 합니다. hello Git 복제 명령은 다음과 같습니다.
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. 다음 예제는 hello와 같이 로컬 컴퓨터에 함수 앱 toohello 복제본에서 파일을 인출:
   
        git pull origin master
   
    요청된 경우 [구성된 배포 자격 증명](#credentials)을 제공합니다.  

[GitHub]: https://github.com/
