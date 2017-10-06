---
title: "Visual Studio에서 서버가 없는 앱 aaaBuild | Microsoft Docs"
description: "첫 번째 서버가 없는 응용 프로그램을 작성, 배포, 및 Visual Studio에서 hello 앱 관리에이 가이드를 시작 하세요."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a>Logic Apps 및 함수를 사용하여 Visual Studio에서 서버를 사용하지 않는 앱 빌드

Azure에서 서버를 사용하지 않는 도구 및 기능은 클라우드 응용 프로그램의 신속한 개발 및 배포를 허용합니다.  이 문서는 방법에 중점을 두고 tooget 서버가 없는 응용 프로그램을 작성 하는 Visual Studio에서 시작 합니다.  Azure에서 서버를 사용하지 않음 개요는 [이 문서에서 찾을 수 있습니다](logic-apps-serverless-overview.md).

## <a name="getting-everything-ready"></a>모든 항목 준비

Visual Studio에서 서버가 없는 응용 hello 필요한 필수 구성 요소 toobuild 키를 같습니다.

* [Visual Studio 2017](https://www.visualstudio.com/vs/) 또는 Visual Studio 2015 - Community, Professional 또는 Enterprise
* [Visual Studio용 Logic Apps 도구](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* [최신 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 이상)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* [Azure 함수 핵심 도구](https://www.npmjs.com/package/azure-functions-core-tools) toodebug 로컬로 함수
* Hello를 사용 하는 경우 액세스 toohello 웹 포함 논리 응용 프로그램 디자이너

## <a name="getting-started-with-a-deployment-template"></a>배포 템플릿 시작

Azure의 리소스 관리는 리소스 그룹 내에서 수행됩니다.  리소스 그룹은 리소스의 논리적 그룹화입니다.  리소스 그룹은 리소스의 컬렉션의 배포 및 관리를 허용합니다.  Azure에서 서버를 사용하지 않는 응용 프로그램의 경우 리소스 그룹에는 Azure Logic Apps 및 Azure Functions 모두가 포함되어 있습니다.  Visual Studio 내에서 리소스 그룹 프로젝트 hello를 사용 하 여 수 toodevelop 하는, 관리 및 단일 자산으로 hello 전체 응용 프로그램을 배포 합니다.

### <a name="create-a-resource-group-project-in-visual-studio"></a>Visual Studio에서 리소스 그룹 프로젝트 만들기

1. Visual Studio에서 tooadd 클릭는 **새 프로젝트**
1. Hello에 **클라우드** 범주를 선택 toocreate Azure **리소스 그룹** 프로젝트  
 * Hello 범주 또는 나열 된 프로젝트 표시 되지 않으면 되어 있는지 확인 hello Azure SDK for Visual Studio 설치
1. 이름 및 위치를 hello 프로젝트를 지정 하 고 선택 **확인** toocreate Visual Studio 템플릿을 tooselect 라는 메시지를 표시 합니다.  공백, 논리 앱 시작 또는 다른 리소스에서 toostart를 선택할 수 있습니다.  그러나이 경우 사용 서버가 없는 앱 시작 우리는 Azure 빠른 시작 템플릿 tooget 합니다.
1. tooshow 템플릿을 선택 **Azure 빠른 시작** ![Azure 빠른 시작을 선택 하면 템플릿][1]
1. 서버 빠른 시작 템플릿 선택 hello: **101-logic-app-and-function-app** 클릭 **확인**

hello 퀵 스타트 템플릿은 리소스 그룹 프로젝트의 배포 템플릿을 만듭니다.  hello 템플릿은 Azure 함수를 호출 하 고 hello 결과 반환 하는 간단한 논리 앱을 포함 합니다.  Hello를 열면 `azuredeploy.json` 파일에 hello 솔루션 탐색기, hello 서버가 없는 응용 프로그램에 대 한 hello 리소스를 확인할 수 있습니다.

## <a name="deploying-hello-serverless-application"></a>Hello 서버가 없는 응용 프로그램 배포

Visual Studio에서 hello 논리 앱에 대 한 비주얼 디자이너를 열 수 있습니다, 전에 미리 배포할된 Azure 리소스 그룹 toobe가 필요 합니다.  그러면 디자이너 toocreate hello 및 사용 하 여 연결 tooresources 및 서비스를 hello 논리 앱 있습니다.  시작 tooget, 단순히 필요 toodeploy hello 솔루션을 생성 합니다.

1. Visual studio에서는 선택 hello 프로젝트를 마우스 오른쪽 단추로 클릭 **배포**, 만들고는 **새로** 배포 ![새 리소스 배포를 선택 하면][2]
1. 유효한 Azure 구독 및 리소스 그룹을 선택합니다.
1. 너무 선택**배포** hello 솔루션
1. 논리 앱 hello에 대 한 hello 이름과 hello Azure 함수 앱에 입력 합니다.  hello Azure 함수 이름은 필요 toobe 전역적으로 고유

hello 서버가 없는 솔루션 hello 지정 된 리소스 그룹으로 배포합니다.  Hello 보면 **출력** Visual Studio에서 hello 배포의 hello 상태를 볼 수 있습니다.

## <a name="editing-hello-logic-app-in-visual-studio"></a>Visual Studio에서 편집 hello 논리 앱

모든 리소스 그룹에 배포 된 hello 솔루션, hello 비주얼 디자이너 사용된 tooedit 수 있으며 변경 내용을 toohello 논리 앱 확인 됩니다.

1. 마우스 오른쪽 단추로 클릭 hello `azuredeploy.json` hello 솔루션 탐색기에서에서 파일을 선택 **와 논리 앱 디자이너 열기**
1. 선택 hello **리소스 그룹** 및 **위치** hello 솔루션 되었습니다 tooand 선택 배포 **확인**

hello 논리 앱에 대 한 비주얼 디자이너 이제 Visual Studio와 함께 표시 됩니다.  Tooadd 단계를 계속 지정, hello 워크플로 수정 및 변경 내용을 저장 합니다.  또한 Visual Studio에서 논리 앱을 만들 수도 있습니다.  Hello를 마우스 오른쪽 단추로 클릭 하는 경우 **리소스** tooadd hello 템플릿 탐색기에서 선택할 수 있습니다는 **논리 앱** toohello 프로젝트.  빈 논리 앱을 로드 하지 않고 hello 비주얼 디자이너는 미리 리소스 그룹으로 배포 합니다.

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a>배포된 논리 앱에 대한 실행 기록 관리 및 보기

또한 관리 하 고 Azure에 배포 된 논리 앱에 대 한 hello 실행 기록을 볼 수 있습니다.  Hello를 열면 **클라우드 탐색기** 도구 실행 기록 보기 또는 Visual Studio, 모든 논리 앱을 마우스 오른쪽 단추로 클릭 하 고 수 tooedit, 사용 안 함, 속성 보기를 선택 합니다.  편집을 클릭 하면 수도 있습니다를 Visual Studio 리소스 그룹 프로젝트에 게시 된 논리 앱 toodownload를.  즉, Azure 포털 hello 사용 하 여 논리 앱 빌드를 시작 하는 경우에 수 여전히 가져와야 하는 Visual Studio에서 관리 합니다.

## <a name="developing-an-azure-function-in-visual-studio"></a>Visual Studio에서 Azure 함수 개발

hello 배포 템플릿 배포 hello에 지정 된 hello git 리포지토리에 대 한 hello 솔루션에 포함 된 모든 Azure 함수 `azuredeploy.json` 변수입니다.  Hello 솔루션 내에 함수 개체를 작성 하는 경우 소스 제어 (GitHub, Visual Studio Team Services 등)로 확인 하 고 hello 업데이트 `repo` 변수인 hello 템플릿 배포 hello Azure 함수입니다.

### <a name="creating-an-azure-function-project"></a>Azure 함수 프로젝트 만들기

JavaScript, Python, F #, Bash, 일괄 처리 또는 PowerShell을 사용 하 여 hello 수행 [hello 함수 CLI의에서 단계를](../azure-functions/functions-run-local.md) toocreate 프로젝트입니다.  C#의 기능을 개발 하는 경우 사용할 수 있습니다는 [C# 클래스 라이브러리](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) hello Azure 함수 hello에 대 한 현재 솔루션의 합니다.

## <a name="next-steps"></a>다음 단계

* [자세한 내용은 방법 toobuild 서버가 없는 소셜 대시보드](logic-apps-scenario-social-serverless.md)
* [Visual Studio 클라우드 탐색기에서 논리 앱 관리](logic-apps-manage-from-vs.md)
* [논리 앱 워크플로 정의 언어](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
