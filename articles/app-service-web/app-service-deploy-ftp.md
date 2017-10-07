---
title: "aaaDeploy 사용자 앱 tooAzure FTP/S를 사용 하 여 응용 프로그램 서비스 | Microsoft Docs"
description: "자세한 방법을 toodeploy 앱 서비스를 사용 하 여 FTP 또는 FTPS 앱 tooAzure 프로그램."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a>사용자 응용 프로그램 tooAzure FTP/S를 사용 하 여 응용 프로그램 서비스를 배포 합니다.

이 문서에서는 어떻게 toouse FTP toodeploy를 웹 앱, 모바일 앱 백 엔드, 또는 API 앱 너무 FTPS 또는[Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.

응용 프로그램에 대 한 hello FTP/S 끝점 이미 활성화 되었습니다. 구성이 필요한 tooenable FTP/S 배포 합니다.

> [!IMPORTANT]
> 단계 tooimprove Microsoft Azure 플랫폼 보안 수행 하 고 계속 합니다. 이러한 지속적인 노력의 일환으로 독일 중부 및 독일 북동부 하위 지역에 대해 웹 응용 프로그램 업그레이드가 예정되어 있습니다. 이 프로세스 동안 웹 응용 프로그램 배포에 대 한 일반 텍스트 FTP 프로토콜의 hello 사용할을 해제 합니다. 권장 사항 tooour 고객 배포에 대 한 tooswitch tooFTPS입니다. 이 업그레이드/9/5에 대 한 계획 되어 있는 동안 모든 중단 tooyour 서비스를 예상 되지 않는 했습니다. 여러분의 지원에 감사 드립니다.

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a>1단계: 배포 자격 증명 설정

앱에 대 한 tooaccess hello FTP 서버를 먼저 배포 자격 증명이 필요 합니다. 

배포 자격 증명 참조 tooset 또는 리셋 [Azure 앱 서비스 배포 자격 증명](app-service-deployment-credentials.md)합니다. 이 자습서의 사용자 자격 증명 hello 사용을 보여 줍니다.

## <a name="step-2-get-ftp-connection-information"></a>2단계: FTP 연결 정보 가져오기

1. Hello에 [Azure 포털](https://portal.azure.com), 응용 프로그램을 열고 [리소스 블레이드](../azure-resource-manager/resource-group-portal.md#manage-resources)합니다.
2. 선택 **개요** hello 왼쪽된 메뉴에 대 한 hello 값을 확인 한 다음 **P/배포 사용자**, **FTP 호스트 이름**, 및 **FTPS 호스트 이름**합니다. 

    ![FTP 연결 정보](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > hello **P/배포 사용자** 사용자가 값으로 표시 된 대로 hello 순서 tooprovide hello FTP 서버에 대 한 적절 한 컨텍스트에 hello 응용 프로그램 이름을 포함 하는 Azure 포털입니다.
    > 찾을 수 선택 하면 동일한 정보를 hello **속성** hello 왼쪽된 메뉴에 있습니다. 
    >
    > 또한 hello 배포 암호 표시 하지 않습니다. 배포 암호를 잊은 경우 돌아가서 너무[1 단계](#step1) 배포 암호를 다시 설정 합니다.
    >
    >

## <a name="step-3-deploy-files-tooazure"></a>3 단계: 파일 tooAzure 배포

1. FTP 클라이언트에서 ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client)등), tooconnect tooyour 앱 수집한 hello 연결 정보를 사용 합니다.
3. 파일 및 해당 해당 디렉터리 구조 toohello 복사 [ **/사이트/wwwroot** 디렉터리](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) Azure에서 (또는 hello **/사이트/wwwroot/App_Data/작업/** 에 대 한 디렉터리 WebJobs)입니다.
4. 찾아보기 tooyour 앱의 URL tooverify hello 앱은 제대로 실행 중입니다. 

> [!NOTE] 
> 와 달리 [Git 기반 배포](app-service-deploy-local-git.md), FTP 배포 배포 자동화를 수행 하는 hello를 지원 하지 않습니다. 
>
> - 종속성 복원(예: NuGet, NPM, PIP 및 Composer Automation)
> - .NET 이진 파일 컴파일
> - web.config 생성([Node.js 예제](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps) 참조)
> 
> 로컬 컴퓨터에서 이러한 필요한 파일을 수동으로 복원, 빌드 및 생성한 후 앱과 함께 배포해야 합니다.
>
>

## <a name="next-steps"></a>다음 단계

고급 배포 시나리오에 대 한 시도 [tooAzure Git가 포함 된 배포](app-service-deploy-local-git.md)합니다. Git 기반 배포 tooAzure 버전 제어, 패키지를 복원, MSBuild, 등 수 있습니다.

## <a name="more-resources"></a>추가 리소스

* [PHP-MySQL 웹 앱을 만들고 FTP를 사용하여 배포합니다.](web-sites-php-mysql-deploy-use-ftp.md)
* [Azure App Service 배포 자격 증명](app-service-deploy-ftp.md)
