---
title: "Azure 앱 서비스 웹 앱과 aaaHow toouse io.js"
description: "자세한 내용은 방법 toouse io.js에 Azure 앱 서비스의 웹 앱입니다."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a>방법 및 Azure 앱 서비스 웹 앱 toouse io.js
hello 인기 있는 노드 포크 [io.js] 다양 한 차이 tooJoyent Node.js 프로젝트를 보다 개방적 거 버 넌 스 모델, 더 빠른 릴리스 주기 및 더 빠른 단기간 새 실험적 JavaScript 기능을 포함 하 여 기능 합니다.

[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps에는 많은 Node.js 버전이 미리 설치되어 있지만 사용자가 제공한 Node.js 이진 파일도 허용합니다. 이 문서에서는 앱 서비스 웹 앱에 io.js hello 사용 하도록 설정 하는 두 가지 방법: hello io.js 이진 파일의 수동 업로드에 hello 뿐만 아니라 Azure toouse hello 최신 사용 가능한 io.js 버전을 자동으로 구성 하는 확장된 배포 스크립트의 사용 합니다. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>배포 스크립트 사용
Node.js 응용 프로그램의 배포 시 응용 프로그램 서비스 웹 앱 환경을 hello tooensure가 올바르게 구성 하는 작은 명령의 수를 실행 합니다. 이 프로세스는 배포 스크립트를 사용 하 여 사용자 지정 된 tooinclude hello 다운로드 및 io.js의 구성을 수 있습니다.

hello [io.js 배포 스크립트](https://github.com/felixrieseberg/iojs-azure) GitHub에서 사용할 수 있습니다. 웹 앱에 tooenable io.js 복사 하기만 하면 **.deployment**, **deploy.cmd** 및 **IISNode.yml** 응용 프로그램 폴더의 toohello 루트 tooWeb 앱 및 배포 합니다.  

hello 첫 번째 파일 **.deployment**, 웹 앱 toorun 지시 **deploy.cmd** 배포 시. 이 스크립트는 Node.js 응용 프로그램에 대 한 모든 hello 일반적인 단계를 실행 하지만 또한 hello io.js의 최신 버전을 다운로드 합니다. 마지막으로, **IISNode.yml** 웹 앱 toouse 다운로드 정당한 hello io.js 사전 설치 된 Node.js 이진 대신 이진을 구성 합니다.

> [!NOTE]
> tooupdate hello io.js 이진 파일을 사용 하 고 응용 프로그램을 다시 배포 하면-hello 스크립트 io.js 마다 한 번 hello 응용 프로그램 배포의 새 버전을 다운로드 합니다.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>수동 설치 사용
사용자 지정 io.js 버전의 hello 수동 설치에만 두 단계가 포함 됩니다. 먼저, hello 다운로드 **win x64** hello에서 직접 이진 [io.js 배포]합니다. **iojs.exe** 및 **iojs.lib** 파일이 필요합니다. 모두 저장 웹 응용 프로그램 내의 tooa 폴더 예의 파일 **bin/iojs**합니다.

웹 앱 toouse tooconfigure **iojs.exe** 사전 설치 된 노드 버전을 대신 만듭니다는 **IISNode.yml** 응용 프로그램의 hello 루트에 있는 파일 및 hello 다음 줄을 추가 합니다.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>다음 단계
이 문서에서 toouse io.js 앱 서비스 웹 앱을 모두 사용 하 여 사용 배포 스크립트 뿐 아니라 수동 설치를 제공 하는 방법을 배웠습니다. 

> [!NOTE]
> io.js는 집중적으로 개발되고 있으며, Node.js보다 자주 업데이트됩니다. 여러 Node.js 모듈이 io.js와 함께 작동하지 않을 수 있으므로 문제 해결은 [GitHub의 io.js] 를 참조하세요.
> 
> 

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

[io.js]: https://iojs.org
[io.js 배포]: https://iojs.org/dist/
[GitHub의 io.js]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
