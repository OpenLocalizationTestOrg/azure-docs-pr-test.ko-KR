---
title: "Visual studio는 앱 tooa 원격 클러스터 aaaPublish | Microsoft Docs"
description: "Visual Studio를 사용 하 여 toopublish 응용 프로그램 tooa 원격 서비스 패브릭 클러스터 하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: d0f06f120cc7e22f3f8e73ce0970e1da5823e647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a>Visual Studio를 사용하여 응용 프로그램 배포 및 제거
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient API](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Visual Studio 용 Azure 서비스 패브릭 확장 hello 간편 하 고 스크립트 가능한 반복 가능 하며, toopublish는 응용 프로그램 tooa 서비스 패브릭 클러스터를 제공합니다.

## <a name="hello-artifacts-required-for-publishing"></a>게시에 필요한 hello 아티팩트
### <a name="deploy-fabricapplicationps1"></a>Deploy-FabricApplication.ps1
서비스 패브릭 응용 프로그램 게시를 위한 매개 변수로 게시 프로필 경로를 사용하는 PowerShell 스크립트입니다. 시작 toomodify는이 스크립트는 응용 프로그램의 일부에 응용 프로그램에 필요할 것입니다.

### <a name="publish-profiles"></a>게시 프로필
Hello 서비스 패브릭 응용 프로그램 프로젝트에서 폴더의 이름은 **PublishProfiles** 와 같은 응용 프로그램을 게시 하기 위한 중요 한 정보를 저장 하는 XML 파일을 포함 합니다.

* 서비스 패브릭 클러스터 연결 매개 변수
* 경로 tooan 응용 프로그램 매개 변수 파일
* 업그레이드 설정

기본적으로 응용 프로그램은 Local.1Node.xml, Local.5Node.xml 및 Cloud.xml의 세 가지 게시 프로필을 포함하게 됩니다. 복사 하 여 붙여 hello 기본 파일 중 하나 이상의 프로 파일을 추가할 수 있습니다.

### <a name="application-parameter-files"></a>응용 프로그램 매개 변수 파일
Hello 서비스 패브릭 응용 프로그램 프로젝트에서 폴더의 이름은 **ApplicationParameters** XML 파일 사용자 지정 응용 프로그램 매니페스트 매개 변수 값을 포함 합니다. 배포 설정에 다른 값을 사용할 수 잇게 응용 프로그램 매니페스트 파일을 매개 변수화할 수 있습니다. 응용 프로그램을 매개 변수화에 대 한 자세한 toolearn 참조 [서비스 패브릭에서 여러 환경을 관리할](service-fabric-manage-multiple-environment-app-configuration.md)합니다.

> [!NOTE]
> 행위자 서비스에 대 한 hello 프로젝트 빌드되어야 먼저 편집기에서 또는 hello 통해 tooedit hello 파일을 시도 하기 전에 게시 대화 상자. 즉, hello 매니페스트 파일의 부분 hello 빌드 시 생성 됩니다.

## <a name="toopublish-an-application-using-hello-publish-service-fabric-application-dialog-box"></a>toopublish hello 서비스 패브릭 응용 프로그램 게시 대화 상자를 사용 하 여 응용 프로그램
hello 대신 다음 단계 설명 방법을 사용 하면 응용 프로그램 toopublish hello **서비스 패브릭 응용 프로그램 게시** hello Visual Studio 서비스 패브릭 도구에서 제공 하는 대화 상자.

1. Hello hello 서비스 패브릭 응용 프로그램 프로젝트의 바로 가기 메뉴에서 선택 **게시...** tooview hello **서비스 패브릭 응용 프로그램 게시** 대화 상자.
   
    ![hello * * 게시 서비스 패브릭 응용 프로그램 * * 대화 상자][0]
   
    hello에서 선택한 hello 파일 **profile을 대상** 드롭다운 목록 상자에는 모든 hello 설정을 제외 하 고 **매니페스트 버전**, 저장 됩니다. 기존 프로필을 다시 사용 하거나 선택 하 여 새로 만들 **< 프로필 관리... >** hello에 **profile을 대상** 드롭다운 목록 상자입니다. 게시 프로필을 선택 하면 해당 내용이 hello hello 대화 상자의 해당 필드에 표시 됩니다. toosave 언제 든 지 변경 내용을 선택 hello **프로필 저장** 링크 합니다.    
2. Hello에 **연결 끝점** 섹션에서 로컬 또는 원격 서비스 패브릭 클러스터의 게시 끝점을 지정 합니다. 연결 끝점 hello tooadd 또는 변경, hello 클릭 **연결 끝점** 드롭다운 목록입니다. hello 목록은 Azure 구독에 따라 hello 사용할 수 있는 서비스 패브릭 클러스터 연결 끝점 toowhich 게시할 수 있습니다. 이미 tooVisual Studio에에서 기록 되지 않습니다 하면 된다는 것 증명된 toodo 하므로 note 합니다.
   
    Hello 클러스터 선택 대화 상자 toochoose hello 집합이 사용 가능한 구독 및 클러스터에서 사용 합니다.
   
    ![hello * * 선택 서비스 패브릭 클러스터 * * 대화 상자][1]
   
   > [!NOTE]
   > Toopublish tooan 임의의 끝점 (예: 파티 클러스터)를 원하는 경우 참조 hello **tooan 임의의 클러스터 끝점을 게시** 아래 섹션.
   > 
   > 
   
    끝점을 선택 하면 Visual Studio hello 연결 toohello 선택한 서비스 패브릭 클러스터의 유효성을 검사 합니다. Hello 클러스터 보안 없으면 Visual Studio tooit 즉시 연결할 수 있습니다. 그러나 hello 클러스터가 안전한 경우 해야 tooinstall 인증서를 계속 하기 전에 로컬 컴퓨터에 합니다. 참조 [tooconfigure 연결의 보안을 어떻게](service-fabric-visualstudio-configure-secure-connections.md) 자세한 정보에 대 한 합니다. 완료 되 면 선택 hello **확인** 단추입니다. hello에 hello 선택한 클러스터 표시 **서비스 패브릭 응용 프로그램 게시** 대화 상자.
3. Hello에 **응용 프로그램 매개 변수 파일** 드롭다운 목록 상자에서 tooan 응용 프로그램 매개 변수 파일을 이동 합니다. 응용 프로그램 매개 변수 파일 hello 응용 프로그램 매니페스트 파일에서 매개 변수에 대 한 사용자가 지정한 값을 보유합니다. 매개 변수를 변경 하거나 tooadd 선택 hello **편집** 단추입니다. 입력 hello hello 매개 변수 값을 변경 하거나 **매개 변수** 눈금. 완료 되 면 선택 hello **저장** 단추입니다.
   
    ![hello * * 매개 변수 * * 편집 대화 상자][2]
4. 사용 하 여 hello **응용 프로그램 업그레이드 hello** 확인란 toospecify이 게시 작업 인지 업그레이드 합니다. 업그레이드 게시 작업은 일반적인 게시 작업과 다릅니다. 차이점 목록은 [서비스 패브릭 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)를 참조하세요. tooconfigure 업그레이드 설정 선택 hello **업그레이드 설정 구성** 링크 합니다. hello 업그레이드 매개 변수 편집기가 나타납니다. 참조 [서비스 패브릭 응용 프로그램의 hello 업그레이드를 구성](service-fabric-visualstudio-configure-upgrade.md) toolearn 업그레이드 매개 변수에 대 한 자세한 합니다.
5. Hello 선택 **매니페스트 버전 중...** 단추 tooview hello **편집 버전** 대화 상자. 업그레이드 tootake 위 tooupdate 응용 프로그램 및 서비스 버전 필요 합니다. 참조 [서비스 패브릭 응용 프로그램 업그레이드 자습서](service-fabric-application-upgrade-tutorial.md) toolearn 응용 프로그램 및 서비스 매니페스트 버전 업그레이드 프로세스에 영향을 줄 합니다.
   
    ![hello * * 버전 * * 편집 대화 상자][3]
   
    Hello 응용 프로그램 및 서비스 버전 1.0.0 또는 숫자 값과 같은 의미 체계 버전 관리의 1.0.0.0 hello 형식에서를 사용 하는 경우 선택 hello **응용 프로그램 및 서비스 버전을 자동으로 업데이트** 옵션입니다. 경우이 옵션을 hello 서비스를 선택 및 코드, 구성, 때마다 응용 프로그램 버전 번호가 자동으로 업데이트 또는 데이터 패키지 버전이 업데이트 됩니다. Tooedit hello 버전을 수동으로 선호 하는 경우이 기능은 hello 확인란 toodisable의 선택을 취소 합니다.
   
   > [!NOTE]
   > 행위자 프로젝트에 대 한 모든 패키지 항목 tooappear를 먼저 작성 hello 프로젝트 toogenerate hello 서비스 매니페스트 파일의 hello 항목.
   > 
   > 
6. 완료 하면 hello 선택 모든 hello 필요한 설정을 지정 **게시** 단추를 선택 하 여 응용 프로그램 toohello toopublish 서비스 패브릭 클러스터입니다. 지정한 hello 설정이 적용 될 toohello 프로세스를 게시 합니다.

## <a name="publish-tooan-arbitrary-cluster-endpoint-including-party-clusters"></a>(파티 클러스터 포함) tooan 임의의 클러스터 끝점을 게시
Visual Studio 게시 환경을 hello tooremote 클러스터에 연결 된 Azure 구독 중 하나를 게시 하기 위한 최적화 됩니다. 그러나 것이 가능한 toopublish tooarbitrary 끝점 (예: 서비스 패브릭 파티 클러스터) 하 여 직접 프로필 XML 게시 hello를 편집 합니다. 위에서 설명한 대로 세 개의 게시 프로필-기본적으로 제공 되**Local.1Node.xml**, **Local.5Node.xml**, 및 **Cloud.xml**-시작 toocreate 않은 상태 다양 한 환경에 대 한 프로필을 추가 합니다. 예를 들어, 라는 tooparty 클러스터를 게시 하기 위한 toocreate 프로 파일을 할 수 있습니다 **Party.xml**합니다.

와 같은 있으면 hello 클러스터 연결 끝점은 클러스터를 보안 되지 않은 tooan 연결 하는 경우 `partycluster1.eastus.cloudapp.azure.com:19000`합니다. 경우 hello에 hello 연결 끝점 게시 한다는 점에서 프로필 유사할 것이:

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  Tooa 보안된 클러스터를 연결 하는 경우 hello 클라이언트 인증서 인증에 사용 되는 hello 로컬 저장소 toobe에서의 tooprovide hello 세부 할 수 있습니다. 자세한 내용은 참조 하십시오. [구성 보안 연결 tooa 서비스 패브릭 클러스터](service-fabric-visualstudio-configure-secure-connections.md)합니다.

  게시 프로필 설정 되 고 나면 hello에서 참조할 수 있습니다 아래와 같이 게시 대화 상자.

  ![게시 대화 상자에서 새 게시 프로필][4]

  참고 새 hello 프로필 게시이 경우 tooone hello 기본 응용 프로그램 매개 변수 파일을 가리킵니다. 이 toopublish hello 환경 수 tooa 동일한 응용 프로그램 구성 하려는 경우 적합 합니다. 이와 반대로 toohave toopublish를 원하는 각 환경에 대해 서로 다른 구성 하려는 경우 하기가 의미 toocreate 해당 응용 프로그램 매개 변수 파일.

## <a name="next-steps"></a>다음 단계
연속 통합 환경에서 tooautomate hello 게시 프로세스를 확인 하려면 어떻게 toolearn [서비스 패브릭 연속 통합을 설정할](service-fabric-set-up-continuous-integration.md)합니다.

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
