---
title: "Azure microservices 위한 개발 환경을 aaaSet | Microsoft Docs"
description: "Hello 런타임, SDK 및 도구를 설치 하 고 로컬 개발 클러스터를 만듭니다. 이 설치를 완료 한 후 응용 프로그램 준비 toobuild 됩니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a>개발 환경 준비
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 toobuild 실행 [Azure 서비스 패브릭 응용 프로그램] [ 1] 하려면 개발 컴퓨터에 hello 런타임, SDK 및 도구를 설치 합니다. Tooenable hello SDK에에서 포함 된 hello Windows PowerShell 스크립트를 실행을 해야 합니다.

## <a name="prerequisites"></a>필수 조건
### <a name="supported-operating-system-versions"></a>지원되는 운영 체제 버전
운영 체제 버전에 따라 hello 개발을 위해 지원 됩니다.

* Windows 7
* Windows 8/Windows 8.1
* Windows Server 2012 R2
* Windows Server 2016
* 윈도우 10

> [!NOTE]
> Windows 7은 기본적으로 Windows PowerShell 2.0만을 포함합니다. 서비스 패브릭 PowerShell cmdlet에는 PowerShell 3.0 이상이 필요합니다. 있습니다 수 [Windows PowerShell 5.0 다운로드] [ powershell5-download] hello Microsoft 다운로드 센터에서에서.
> 
> 

## <a name="install-hello-sdk-and-tools"></a>Hello SDK 및 도구 설치
### <a name="toouse-visual-studio-2017"></a>Visual Studio 2017 toouse
서비스 패브릭 도구는 Visual Studio 2017 hello Azure 개발 및 관리 작업 부하의 일부입니다. 이 워크로드를 Visual Studio 설치의 일부로 사용하도록 설정해야 합니다.
또한 Microsoft Azure 서비스 패브릭 SDK에서 웹 플랫폼 설치 관리자를 사용 하 여 tooinstall hello를 해야 합니다.

* [Hello Microsoft Azure Service Fabric SDK 설치][core-sdk]

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a>toouse Visual Studio 2015 (Visual Studio 2015 업데이트 2 이상 필요)
서비스 패브릭 도구는 Visual Studio 2015에 대 한 hello hello 웹 플랫폼 설치 관리자를 사용 하 여 SDK와 함께 설치 됩니다.

* [Microsoft Azure Service Fabric SDK hello 및 도구 설치][full-bundle-vs2015]

### <a name="sdk-installation-only"></a>SDK 설치만
Hello SDK 하기만 하면,이 패키지를 설치할 수 있습니다.
* [Hello Microsoft Azure Service Fabric SDK 설치][core-sdk]

hello 현재 버전이 됩니다.
* Service Fabric SDK 2.7.198
* Service Fabric 런타임 5.7.198
* Visual Studio 2015 1.7.50721용 Service Fabric 도구
* Visual Studio 2017 업데이트 2에는 Visual Studio 1.6.20170504용 Service Fabric 도구가 포함됩니다.
* Visual Studio 2017 업데이트 3 미리 보기 7(15.3.0 미리 보기 7.0)에는 Visual Studio 1.7.20170721용 Service Fabric 도구가 포함됩니다.

지원되는 버전 목록은 [Service Fabric 지원](service-fabric-support.md)을 참조하세요.

## <a name="enable-powershell-script-execution"></a>PowerShell 스크립트 실행 활성화
서비스 패브릭은 로컬 개발 클러스터를 만들고 Visual Studio에서 응용 프로그램을 배포하기 위해 Windows PowerShell 스크립트를 사용합니다. 기본적으로 Windows에서는 이러한 스크립트의 실행을 차단합니다. tooenable PowerShell 실행 정책 수정 해야 합니다. 관리자 권한으로 PowerShell을 열고 다음 명령을 hello를 입력 합니다.

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>다음 단계
개발 환경의 설정을 마쳤으므로 앱을 빌드하고 실행하기 시작할 수 있습니다.

* [Visual Studio에서 서비스 패브릭 응용 프로그램 처음 만들기](service-fabric-create-your-first-application-in-visual-studio.md)
* [자세한 내용은 방법 toodeploy 로컬 클러스터에 응용 프로그램 및 관리](service-fabric-get-started-with-a-local-cluster.md)
* [Hello 프로그래밍 모델에 대 한 자세한 내용은: 신뢰할 수 있는 서비스 및 Reliable Actors](service-fabric-choose-framework.md)
* [서비스 패브릭 hello GitHub의 코드 샘플 확인](https://aka.ms/servicefabricsamples)
* [서비스 패브릭 탐색기를 사용하여 클러스터 시각화](service-fabric-visualizing-your-cluster.md)
* [서비스 패브릭 경로 tooget 광범위 한 소개 toohello 플랫폼 학습 hello를 수행 합니다.](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* [Service Fabric 지원 옵션](service-fabric-support.md) 알아보기

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric 캠페인 페이지"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI 링크"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI 링크"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI 링크"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
