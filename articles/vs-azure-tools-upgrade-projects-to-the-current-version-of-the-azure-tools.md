---
title: "aaaHow tooupgrade 프로젝트 toohello 현재 버전의 Azure tools hello | Microsoft Docs"
description: "어떻게 tooupgrade Azure 프로젝트에서 Visual Studio toohello 현재 버전의 hello Azure 도구에 알아봅니다"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1d64070a-078d-468a-87f4-e6715de6475f
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: c89ba43af0f2fd9db46ce0c90f0da3d70dc1510b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupgrade-projects-toohello-current-version-of-hello-azure-tools-for-visual-studio"></a>Tooupgrade는 toohello 현재 버전의 hello Azure Tools for Visual Studio 프로젝션 하는 방법
## <a name="overview"></a>개요
1.6 이전의 릴리스 hello 현재 버전의 hello Azure Tools (또는 1.6 버전인 이전 릴리스)를 설치한 후 Azure 도구를 사용 하 여 만든 모든 프로젝트 열기으로 (2011 년 11 월) 자동으로 업그레이드 됩니다. 사용 하 여 프로젝트를 만든 경우 이러한 도구 1.6 (2011 년 11 월) 릴리스의 hello 및 해당 릴리스가 설치 되어 있는 수 있습니다 hello 이전 릴리스에서 프로젝트를 열고 나중에 있는지 여부를 tooupgrade 해당 합니다.

## <a name="how-your-project-changes-when-you-upgrade-it"></a>업그레이드 시 프로젝트의 변경 내용
프로젝트를 자동으로 업그레이드 하거나 지정 하는 경우 선택 tooupgrade, 프로젝트는 현재 버전 특정 어셈블리의 toowork 수정이 섹션에 설명 된 대로 일부 속성도 변경 됩니다. 프로젝트에 필요한 다른 변경 내용을 toobe hello 최신 버전의 hello 도구와 호환를 경우 해당 변경 내용을 수동으로 해야 합니다.

* 웹 역할에 대 한 hello web.config 파일 및 작업자 역할에 대 한 hello app.config 파일은 업데이트 된 tooreference hello 최신 버전의 Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll 합니다.
* hello Microsoft.WindowsAzure.StorageClient.dll, Microsoft.WindowsAzure.Diagnostics.dll 및 Microsoft.WindowsAzure.ServiceRuntime.dll 어셈블리가 업그레이드 된 toohello 새 버전입니다.
* Hello Azure 프로젝트 파일 (.ccproj)에 저장 된 게시 프로필은 hello에 hello 확장명이.azurePubXml 인 별도 파일에 이동된 tooa **게시** 하위 디렉터리입니다.
* 게시 프로필 hello에서 일부 속성은 업데이트 된 toosupport 새로운 기능과 변경 된 기능입니다. 배포된 클라우드 서비스를 동시에 또는 중분 방식으로 업데이트할 수 있으므로 **AllowUpgrade**는 **DeploymentReplacementMethod**로 대체됩니다.
* 속성을 hello **UseIISExpressByDefault** 추가 되 고 hello 웹 서버 디버깅에 사용 되는 변경 되지 않는 자동으로 인터넷 정보 서비스 (IIS) tooIIS Express에서에서 있도록 toofalse를 설정 합니다. IIS Express는 hello 기본 웹 서버 hello hello tools의 최신 릴리스를 사용 하 여 만든 프로젝트입니다.
* Azure Caching을 하나 이상의 프로젝트 역할에서 호스트 하는 경우 프로젝트를 업그레이드할 때 hello 서비스 구성 (파일.cscfg) 및 서비스 정의 (.csdef 파일)의 일부 속성이 변경 됩니다. Hello 프로젝트 hello Azure 캐싱 NuGet 패키지를 사용 하는 경우 hello 프로젝트는 업그레이드 된 toohello hello 패키지의 최신 버전입니다. Hello web.config 파일을 열고 hello 업그레이드 프로세스 중 해당 hello 클라이언트 구성이 올바르게 유지 되었는지 확인 해야 합니다. Hello NuGet 패키지를 사용 하지 않고 hello 참조 tooAzure Caching 클라이언트 어셈블리를 추가한 경우 이러한 어셈블리는 업데이트 되지 않습니다. 이러한 참조 toohello 새 버전을 수동으로 업데이트 해야 합니다.

> [!IMPORTANT]
> F # 프로젝트의 경우 이러한 어셈블리의 최신 버전 hello 참조할 수 있도록 tooAzure 어셈블리 참조를 수동으로 업데이트 해야 있습니다.
> 
> 

### <a name="how-tooupgrade-an-azure-project-toohello-current-release"></a>어떻게 tooupgrade Azure 프로젝트 toohello 현재 버전
1. 설치 hello 현재 버전의 Visual Studio 설치 hello에 Azure Tools hello hello에 대 한 toouse 되도록 tooupgrade 연 다음 hello 프로젝트 및 프로젝트를 업그레이드 합니다. Azure tools hello 프로젝트를 만든 경우 1.6 이전 릴리스 (2011 년 11 월) hello 프로젝트는 자동으로 업그레이드 된 toohello 현재 버전입니다. 2011 년 11 월 릴리스 hello로 hello 프로젝트를 만든 및 릴리스가 아직 설치 되어 있는 경우 해당 릴리스에서 hello 프로젝트가 열립니다.
2. Hello 프로젝트 노드에 대 한 바로 가기 메뉴를 열고 hello 솔루션 탐색기에서 선택 **속성**, hello 선택 **응용 프로그램** 나타나는 hello 대화 상자의 탭 합니다.
   
    hello **응용 프로그램** 탭 hello 프로젝트와 관련 된 hello 도구 버전을 표시 합니다. 현재 버전의 Azure Tools hello 표시 되 면 hello 프로젝트가 이미 업그레이드 되었습니다. 어떤 hello 탭에 표시 하는 보다 최신 버전의 hello 도구를 설치 했으면는 **업그레이드** 단추가 나타납니다.
3. Hello 선택 **업그레이드** 단추 tooupgrade 프로젝트 toohello 현재 버전의 hello 도구입니다.
4. Hello 프로젝트를 빌드하고 API 변경으로 인해 발생 하는 오류를 해결 합니다. 에 대 한 내용은 toomodify hello 새 버전에 대 한 코드에 대 한 hello 설명서를 참조 하는 방법에 특정 API hello 합니다.

