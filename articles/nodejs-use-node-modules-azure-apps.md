---
title: "aaaWorking Node.js 모듈"
description: "자세한 방법을 toowork 클라우드 서비스 또는 Azure 앱 서비스를 사용 하는 경우 Node.js 모듈입니다."
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c0e6cd3d-932d-433e-b72d-e513e23b4eb6
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 926358b7eb80a659dbc1015686b06a30d8c9b8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-nodejs-modules-with-azure-applications"></a>Azure 응용 프로그램에 Node.js 모듈 사용
이 문서에서는 Azure에서 호스트되는 응용 프로그램에 Node.js 모듈을 사용하는 방법에 대해 안내합니다. 응용 프로그램에서 특정 버전의 모듈을 사용하고 Azure 네이티브 모듈을 사용하도록 하는 방법을 설명합니다.

Node.js 모듈을 사용 하 여 이미 익숙한 경우 **package.json** 및 **npm shrinkwrap.json** 파일 hello 다음 정보는이 문서에 대해서는 설명의 빠른 요약을 제공 합니다.

* Azure 앱 서비스는 **package.json** 및 **npm-shrinkwrap.json** 파일을 인식하며 이 파일의 항목을 기반으로 모듈을 설치할 수 있습니다.

* Azure 클라우드 서비스는 hello 개발 환경 및 hello에 설치 된 모든 모듈 toobe 예상 **노드\_모듈** 디렉터리 toobe hello 배포 패키지의 일부로 포함 합니다. 하지만 사용 하 여 모듈을 설치 하기 위한 가능한 tooenable 지원 되었기 **package.json** 또는 **npm shrinkwrap.json** 파일 클라우드 서비스에이 구성의 hello 기본 사용자 지정에 필요 클라우드 서비스 프로젝트에서 사용 되는 스크립트입니다. 방법의 예에 대 한 tooconfigure이이 환경 참조 [Azure 시작 작업 toorun npm 설치 tooavoid 노드 모듈 배포](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)

> [!NOTE]
> Azure 가상 컴퓨터 처럼 VM에 배포 환경을 hello hello 가상 컴퓨터에서 호스팅하는 hello 운영 체제에 따라 달라 집니다.이 문서에서 다루지 않습니다.
> 
> 

## <a name="nodejs-modules"></a>Node.js 모듈
모듈은 응용 프로그램의 특정 기능을 제공하는 로드 가능한 JavaScript 패키지입니다. 하지만 모듈은 일반적으로 설치 하 여 hello를 사용 하 여 **npm** 명령줄 도구를 일부 모듈 (예: hello http 모듈)은 hello 핵심 Node.js 패키지의 일부로 있습니다.

Hello에 저장 된 모듈을 설치 하면 **노드\_모듈** hello 루트 응용 프로그램 디렉터리 구조에 디렉터리입니다. Hello 내에서 각 모듈이 **노드\_모듈** 디렉터리 유지 자체 **노드\_모듈** 의존 하 고이 동작을 반복 하는 모든 모듈에 포함 된 디렉터리 종속성 체인 hello 모든 hello 방식으로 모든 모듈에 대해 하지만이 환경의 각 모듈을 설치 toohave 매우 큰 디렉터리 구조에서 발생할 수 있습니다에 종속 hello 모듈에 대 한 자체 버전 요구를 수 있습니다.

배포 hello **노드\_모듈** 응용 프로그램의 일부 hello 배포 비교 했을 때의 hello 크기 증가 하면 디렉터리 toousing는 **package.json** 또는  **하지만 npm shrinkwrap.json** ; 파일을 프로덕션 환경에서 사용 되는 hello 모듈의 hello 버전은 hello 동일 개발에 사용 되는 hello 모듈로 보장지 않습니다 합니다.

### <a name="native-modules"></a>네이티브 모듈
대부분의 모듈이 단순히 일반 텍스트 JavaScript 파일인 반면, 일부 모듈은 플랫폼별 이진 이미지입니다. 이 모듈은 설치 시간에 대개 Python 및 node-gyp를 사용하여 컴파일됩니다. Azure 클라우드 서비스는 hello 사용 하므로 **노드\_모듈** hello 응용 프로그램을 당시의 hello 설치 된 모듈의 일부는 클라우드 서비스에서 작동 해야 하는 대로 포함 된 모든 네이티브 모듈의 일부로 배포 되는 폴더 설치 하 고 Windows 개발 시스템에서 컴파일된 합니다.

Azure App Service는 일부 네이티브 모듈을 지원하지 않으며 특정 필수 구성 요소가 필요한 모듈을 컴파일할 때는 오류가 발생할 수 있습니다. MongoDB와 같은 일부 일반적인 모듈에는 선택적 네이티브 종속성이 있으며 이러한 종속성 없이도 정상적으로 작동하지만 다음 두 가지 해결 방법은 현재 사용 가능한 거의 모든 네이티브 모듈에 효과적인 것으로 입증되었습니다.

* 실행 **npm 설치** 모든 hello 네이티브 모듈의 필수 구성 요소가 설치 되어 있는 Windows 컴퓨터. 그런 다음 만든 hello 배포할 **노드\_모듈** hello 응용 프로그램 tooAzure 앱 서비스의 일부로 폴더입니다.

  * 를 컴파일하기 전에 로컬 Node.js 설치는 일치 하는 인프라를 갖추고 및 hello 버전은 Azure에서 사용 되는 가능한 toohello 가깝도록 확인 (속성에서 런타임에 hello 현재 값을 확인할 수 있습니다 **process.arch**및 **process.version**).

* Azure 앱 서비스는 사용자 지정 구성된 tooexecute bash 수 또는 셸 스크립트 배포를 제공 하는 동안 기회 tooexecute 사용자 지정 명령을 hello 및 hello를 정확 하 게 구성 방법은 **npm 설치** 실행 되 고 있습니다. 비디오 표시 하기 위한 방법을 tooconfigure 해당 환경 참조 [Kudu 사용 하 여 사용자 지정 웹 사이트 배포 스크립트]합니다.

### <a name="using-a-packagejson-file"></a>package.json 파일 사용
hello **package.json** 파일은 한 방식으로 toospecify hello 최상위 응용 프로그램에 필요한 종속성 hello 호스팅 플랫폼 설치할 수 있도록 hello 종속성 tooinclude hello를 요구 하는 대신 **노드 \_패키지** hello 배포의 일부로 폴더입니다. Hello 응용 프로그램을 배포한 후 hello **npm 설치** 명령은 사용 되는 tooparse hello **package.json** 파일을 나열 하는 모든 hello 종속성을 설치 합니다.

개발 하는 동안 hello를 사용할 수 있습니다 **-저장**, **-저장 dev**, 또는 **-저장 선택적** 모듈 tooadd hello 모듈 tooyour 에대한항목을설치하는경우매개변수**package.json** 자동으로 파일입니다. 자세한 내용은 [npm-install](https://docs.npmjs.com/cli/install)(영문)을 참조하십시오.

문제가 발생할 hello로 **package.json** 파일은 최상위 종속성에 대 한 hello 버전만 지정 하는지 합니다. 각 모듈을 설치 되었거나 의존 하는 hello 모듈의 hello 버전을 지정 하지 않을 수 있습니다 및 수도 hello 개발에 사용 된 것 보다 다른 종속성 체인으로 끝날 수도 있습니다.

> [!NOTE]
> TooAzure 앱 서비스를 배포할 때 사용자 <b>package.json</b> 파일에서 참조 하는 네이티브 모듈 Git를 사용 하 여 hello 응용 프로그램을 게시 하는 경우 다음 예제에서는 오류 유사한 toohello 표시 될 수 있습니다.
> 
> npm ERR! module-name@0.6.0 설치: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp configure build"' failed with 1
> 
> 

### <a name="using-a-npm-shrinkwrapjson-file"></a>npm-shrinkwrap.json 파일 사용
hello **npm shrinkwrap.json** 파일은의 hello는 시도 tooaddress hello 모듈 버전 관리 제한 **package.json** 파일입니다. Hello 동안 **package.json** 파일 포함 hello 최상위 모듈에 대 한 버전 hello **npm shrinkwrap.json** 파일 hello 전체 모듈 종속성 체인에 대 한 hello 버전 요구 사항에 포함 되어 있습니다.

응용 프로그램을 프로덕션에 대 한 준비 되 면이 버전 요구 사항 잠글를 만들 수 있습니다는 **npm shrinkwrap.json** hello를 사용 하 여 파일 **npm shrinkwrap** 명령입니다. 이 명령은 현재 hello에 설치 된 hello 버전을 사용 합니다 **노드\_모듈** 폴더, 이러한 버전 toohello 기록 **npm shrinkwrap.json** 파일입니다. Hello 응용 프로그램에 대 한 호스팅 환경으로 배포 된 toohello를 수행한 후 hello **npm 설치** 명령은 사용 되는 tooparse hello **npm shrinkwrap.json** 파일을 나열 하는 모든 hello 종속성을 설치 합니다. 자세한 내용은 [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap)을 참조하세요.

> [!NOTE]
> TooAzure 앱 서비스를 배포할 때 사용자 <b>npm shrinkwrap.json</b> 파일에서 참조 하는 네이티브 모듈 Git를 사용 하 여 hello 응용 프로그램을 게시 하는 경우 다음 예제에서는 오류 유사한 toohello 표시 될 수 있습니다.
> 
> npm ERR! module-name@0.6.0 설치: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp configure build"' failed with 1
> 
> 

## <a name="next-steps"></a>다음 단계
이해 했으므로 Azure 사용 하 여 toouse Node.js 모듈 너무 방법을 알아보려면 어떻게[hello Node.js 버전을 지정], [빌드 및 Node.js 웹 응용 프로그램 배포](app-service-web/app-service-web-get-started-nodejs.md), 및 [toouse 명령줄 Azure hello 하는 방법 Mac 및 Linux 용 인터페이스]합니다.

자세한 내용은 참조 hello [Node.js 개발자 센터](/nodejs/azure/)합니다.

[hello Node.js 버전을 지정]: nodejs-specify-node-version-azure-apps.md
[toouse 명령줄 Azure hello 하는 방법 Mac 및 Linux 용 인터페이스]:cli-install-nodejs.md
[Kudu 사용 하 여 사용자 지정 웹 사이트 배포 스크립트]: https://channel9.msdn.com/Shows/Azure-Friday/Custom-Web-Site-Deployment-Scripts-with-Kudu-with-David-Ebbo
