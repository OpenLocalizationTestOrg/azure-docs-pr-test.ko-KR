---
title: "aaaSpecifying Node.js 버전"
description: "Toospecify 버전의 Node.js Azure 웹 사이트 및 클라우드 서비스에서 사용 하는 hello 하는 방법에 대해 알아봅니다"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a>Azure 응용 프로그램에서 Node.js 버전 지정
Node.js 응용 프로그램을 호스트할 때 응용 프로그램이 특정 버전의 Node.js 사용 하는 tooensure를 수도 있습니다. 있는 경우 여러 가지 방법으로 tooaccomplish이 Azure에서 호스팅되는 응용 프로그램

## <a name="default-versions"></a>기본 버전
Azure에서 제공 하는 hello Node.js 버전 지속적으로 업데이트 합니다. 별도로 지정 하지 않으면 hello hello에 지정 된 기본 버전 `WEBSITE_NODE_DEFAULT_VERSION` 환경 변수가 사용 됩니다. toooverride이 기본값,이 문서의 다음 섹션의 hello 단계 수행

> [!NOTE]
> Azure 클라우드 서비스 (웹 또는 작업자 역할)에서 응용 프로그램을 호스팅하는 것이 hello hello 응용 프로그램을 배포 하는 처음으로 하는 경우 Azure는 toouse를 시도 하는 경우 개발 환경에 설치 하면 동일한 버전의 Node.js hello 것 Azure에서 사용할 수 있는 hello 기본 버전 중 하 나와 일치 합니다.
>
>

## <a name="versioning-with-packagejson"></a>package.json을 사용하여 버전 관리
Node.js toobe hello tooyour 다음을 추가 하 여 사용의 hello 버전을 지정할 수 있습니다 **package.json** 파일:

    "engines":{"node":version}

여기서 *버전* hello 특정 버전 번호 toouse 됩니다. 다음과 같이 버전에 보다 복잡한 조건을 지정할 수 있습니다.

    "engines":{"node": "0.6.22 || 0.8.x"}

0.6.22 이면 hello 호스팅 환경에서에서 사용할 수 있는 hello 버전 이후 hello 가장 높은 버전의 hello 0.8 사용할 수 있는 계열 수 대신 사용-0.8.4 합니다.

## <a name="versioning-websites-with-app-settings"></a>앱 설정을 사용하여 웹 사이트 버전 관리
Hello 응용 프로그램을 웹 사이트에서를 호스팅하는 경우 hello 환경 변수를 설정할 수 있습니다 **WEBSITE_NODE_DEFAULT_VERSION** toohello 원하는 버전.

## <a name="versioning-cloud-services-with-powershell"></a>PowerShell을 사용하여 클라우드 서비스 버전 관리
클라우드 서비스에 hello 응용 프로그램을 호스팅하는 Azure PowerShell을 사용 하 여 hello 응용 프로그램을 배포 하는 경우 hello를 사용 하 여 hello 기본 Node.js 버전을 재정의할 수 있습니다 **집합 AzureServiceProjectRole** PowerShell cmdlet. 예:

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

참고 hello 매개 변수 문 위의 hello에 대/소문자를 구분 하지 않습니다.  Hello를 확인 하 여 hello 올바른 버전의 Node.js가 선택한 확인할 수 있습니다 **엔진** 사용자 역할에 속성 **package.json**합니다.

Hello를 사용할 수도 있습니다 **Get AzureServiceProjectRoleRuntime** tooretrieve Node.js 버전 클라우드 서비스로 호스팅되는 응용 프로그램에 사용할 수 있는 목록입니다.  이 목록에 프로젝트에 의존 하는 Node.js의 hello 버전은 항상 확인 합니다.

## <a name="using-a-custom-version-with-azure-websites"></a>Azure 웹 사이트에서 사용자 지정 버전 사용
Azure에 몇 가지 기본 버전의 Node.js 제공 하며, 기본적으로 제공 하지 않는 버전 toouse를 할 수 있습니다. 응용 프로그램을 Azure 웹 사이트로 호스트 된 경우이 수행할 수 있습니다 hello를 사용 하 여 **iisnode.yml** 파일입니다. hello 다음 단계에 관한 사용자 지정 버전의 Node.Js 사용 하 여 Azure 웹 사이트와의 hello 프로세스를 통해:

1. 만든 다음 새 디렉터리를 만들고는 **server.js** hello 디렉터리 내의 파일입니다. hello **server.js** hello 다음 파일을 포함 해야 합니다.

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    이 hello 웹 사이트를 찾을 때 사용 되는 hello Node.js 버전을 표시 됩니다.
2. 새 웹 사이트와 hello 사이트의 참고 hello 이름을 만듭니다. Hello 다음과 같이 hello를 사용 하는 예를 들어 [Azure 명령줄 도구] toocreate 라는 새 Azure 웹 사이트 **입력 하면 mywebsite**, hello 웹 사이트에 대 한 Git 리포지토리를 사용 하도록 설정 합니다.

        azure site create mywebsite --git
3. 라는 새 디렉터리를 만들고 **bin** hello를 포함 하는 hello 디렉터리의 자식으로 **server.js** 파일입니다.
4. 특정 버전의 hello 다운로드 **node.exe** (hello Windows 버전) 응용 프로그램과 함께 toouse 한다고 합니다. 예를 들어 다음 사용 하 여 hello **curl** toodownload 0.8.1 버전:

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    Hello 저장 **node.exe** hello에 파일을 **bin** 이전에 만든 폴더에 있습니다.
5. 만들기는 **iisnode.yml** hello 동일 파일 hello로 디렉터리 **server.js** 파일을 선택한 다음 다음 콘텐츠 toohello hello 추가 **iisnode.yml** 파일:

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    이 경로 여기서 hello **node.exe** 프로그램 응용 프로그램 toohello Azure 웹 사이트를 게시 한 후 프로젝트 내에서 파일을 찾을 수는 있습니다.
6. 응용 프로그램을 게시합니다. 예를 들어 I 앞에서 만든 새 웹 사이트 hello-git 매개 변수와 함께, 이후 hello 다음 명령을 hello 응용 프로그램 파일 toomy 로컬 Git 리포지토리를 추가 되며 다음 toohello 웹 사이트 리포지토리 푸시:

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    Hello 응용 프로그램에 게시 된 후 브라우저에서 hello 웹 사이트를 엽니다. "Hello from Azure running node version: v0.8.1"이라는 메시지가 표시됩니다.

## <a name="next-steps"></a>다음 단계
Toospecify hello 버전의 Node.js 응용 프로그램에서 사용 하는 방법을 이해 했으므로 너무 방법을 알아보려면[모듈 관련 작업을 수행할], [Node.js 웹 사이트를 배포](app-service-web/app-service-web-get-started-nodejs.md), 및 [toouse Azure hello 하는 방법 Mac 및 Linux 용 명령줄 도구]합니다.

자세한 내용은 참조 hello [Node.js 개발자 센터](https://azure.microsoft.com/develop/nodejs/)합니다.

[toouse Azure hello 하는 방법 Mac 및 Linux 용 명령줄 도구]:cli-install-nodejs.md
[Azure 명령줄 도구]:cli-install-nodejs.md
[모듈 관련 작업을 수행할]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
