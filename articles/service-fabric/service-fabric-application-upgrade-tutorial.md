---
title: "aaaService 패브릭 응용 프로그램 업그레이드 자습서 | Microsoft Docs"
description: "이 문서에서는 서비스 패브릭 응용 프로그램을 배포 하 고, hello 코드를 변경 하 고, Visual Studio를 사용 하 여 업그레이드 롤아웃 hello 환경을 안내 합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a3181a7a-9ab1-4216-b07a-05b79bd826a4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: d069ff0b291018dbac846e65cddff1e9d73d156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-tutorial-using-visual-studio"></a>Visual Studio를 사용하여 서비스 패브릭 응용 프로그램 업그레이드 자습서
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Azure 서비스 패브릭 hello 업그레이드 프로세스에 클라우드 응용 프로그램 변경 된 서비스에만 업그레이드 되 고 hello 업그레이드 프로세스 전체에서 응용 프로그램 상태는 모니터링을 간소화 합니다. 자동으로 롤백합니다 hello 응용 프로그램 toohello 문제 발생 시에 이전 버전입니다. 서비스 패브릭 응용 프로그램 업그레이드는 *가동 중지 시간이 0*이므로 hello 응용 프로그램을 가동 중지 시간 없이으로 업그레이드할 수 있습니다. 이 자습서에서는 어떻게 toocomplete Visual Studio에서 롤링 업그레이드 합니다.

## <a name="step-1-build-and-publish-hello-visual-objects-sample"></a>1 단계: 빌드 및 게시 hello 시각적 개체 샘플
먼저, hello 다운로드 [시각적 개체](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) GitHub에서 응용 프로그램입니다. 그런 다음 빌드하고 hello 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 hello 응용 프로그램을 게시 **VisualObjects**, hello를 선택 하 고 **게시** hello 서비스 패브릭 메뉴 항목에 명령 합니다.

![서비스 패브릭 응용 프로그램의 상황에 맞는 메뉴][image1]

선택 하면 **게시** 는 팝업 표시 되며 hello를 설정할 수 있습니다 **profile을 대상** 너무**PublishProfiles\Local.xml**합니다. hello 창을 보여 hello 클릭 하기 전에 다음 **게시**합니다.

![서비스 패브릭 응용 프로그램 게시][image2]

클릭할 수 있는 이제 **게시** hello 대화 상자에서. 사용할 수 있습니다 [서비스 패브릭 탐색기 tooview hello 클러스터와 hello 응용 프로그램](service-fabric-visualizing-your-cluster.md)합니다. hello 시각적 개체 응용 프로그램에 웹 서비스 입력 tooby 처리할 수 있다고 [http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/) 브라우저의 주소 표시줄 hello에에서 있습니다.  Hello 화면 내에서 이동 10 부동 시각적 개체를 볼 수 있습니다.

**참고:** 너무 배포 경우`Cloud.xml` 프로필 (Azure 서비스 패브릭) hello 응용 프로그램에서 사용할 수 해야 **http://{ServiceFabricName}. { Region}.cloudapp.azure.com:8081/visualobjects/**합니다. 권한이 있는지 확인 `8081/TCP` hello 부하 분산 장치에에서 구성 된 (hello에서 hello 부하 분산 장치를 찾을 hello 서비스 패브릭 인스턴스와 동일한 리소스 그룹).

## <a name="step-2-update-hello-visual-objects-sample"></a>2 단계: 업데이트 hello 시각적 개체 샘플
1 단계에서 배포 된 hello 버전으로 hello 시각적 개체 회전 하지 않습니다 나타날 수 있습니다. 이 응용 프로그램 tooone hello 시각적 개체도 회전 업그레이드 해 보겠습니다.

Hello VisualObjects 솔루션 내에서 hello VisualObjects.ActorService 프로젝트를 선택 하 고 hello 엽니다 **VisualObjectActor.cs** 파일입니다. 해당 파일 내에서 이동 toohello 메서드 `MoveObject`를 주석으로 처리 `visualObject.Move(false)`, 주석 처리를 제거 하 고 `visualObject.Move(true)`합니다. Hello 서비스를 업그레이드 한 후 hello 개체를 회전 하는이 코드를 변경 합니다.  **(재빌드)를 빌드할 수 이제 솔루션 hello**, hello 빌드 프로젝트를 수정 합니다. 선택 하는 경우 *모두 다시 빌드*, 모든 hello 프로젝트에 대 한 tooupdate hello 버전을 보유 합니다.

Tooversion 응용 프로그램도 필요합니다. toomake hello 버전 hello에서 마우스 오른쪽 단추로 클릭 한 후 변경 **VisualObjects** 프로젝트를 Visual Studio hello를 사용할 수 있습니다 **매니페스트 버전 편집** 옵션입니다. 이 옵션을 선택 하면 hello 대화 상자를 엽니다 edition 버전에 대 한 다음과 같습니다.

![버전 관리 대화 상자][image3]

Hello에 대 한 업데이트 hello 버전 hello 응용 프로그램 tooversion 2.0.0 함께 자신의 코드 패키지 및 프로젝트를 수정 합니다. Hello 매니페스트 hello 다음과 같습니다 hello 변경 된 후 (굵게 표시 된 부분 hello 변경 내용을 표시 하는 데 사용):

![버전 업데이트][image4]

hello Visual Studio tools 버전을 선택 하면 자동 롤업을 수행할 수 있는 **응용 프로그램 및 서비스 버전을 자동으로 업데이트**합니다. 사용 하는 경우 [SemVer](http://www.semver.org), tooupdate hello 코드 해야 및/또는 구성 패키지 버전에 대 한 해당 경우에 옵션을 선택 합니다.

Hello 변경 내용을 저장 하 고 이제 hello 확인 **응용 프로그램 업그레이드 hello** 상자입니다.

## <a name="step-3--upgrade-your-application"></a>3단계: 응용 프로그램 업그레이드
Hello를 숙지 [응용 프로그램 업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md) 및 hello [업그레이드 프로세스](service-fabric-application-upgrade.md) tooget hello 다양 한 업그레이드 매개 변수, 제한 시간, 및 수행할 수 있는 상태 조건 이해 적용할 수 있습니다. 이 연습에 대 한 hello 서비스 상태 평가 조건 (모니터링 되지 않는 모드) toohello 기본을 설정 됩니다. 선택 하 여 이러한 설정을 구성할 수 있습니다 **업그레이드 설정 구성** 다음 원하는 대로 hello 매개 변수를 수정 합니다.

이제 우리는 모든 집합 toostart hello 응용 프로그램을 선택 하 여 업그레이드 **게시**합니다. 이 옵션은 프로그램 응용 프로그램 tooversion hello 개체 회전할 2.0.0를 업그레이드 합니다. 서비스 패브릭 (일부 개체는 업데이트 먼저 다른 사용자가 다음) 한 번에 하나의 업데이트 도메인을 업그레이드 하 고 hello 서비스는 hello 업그레이드 하는 동안 액세스할 수 있는 상태로 유지 합니다. 액세스 toohello 서비스 클라이언트 (브라우저)를 통해 확인할 수 있습니다.  

이제 응용 프로그램 업그레이드 진행 hello,으로 모니터링할 수 있습니다 서비스 패브릭 탐색기로 hello를 사용 하 여 **진행 중인 업그레이드** hello 응용 프로그램에서 탭 합니다.

잠시 후에 (완료) 모든 업데이트 도메인을 업그레이드 해야 하 고 해당 hello 업그레이드가 완료 된 hello Visual Studio 출력 창도 명시 합니다. 발견 하 게 하는 *모든* hello 시각적 개체 브라우저 창에서 이제 회전!

Tootry hello 버전을 변경 하 고 연습으로 버전 2.0.0 tooversion 3.0.0에서에서 이동 하거나 다시 tooversion 1.0.0 버전 2.0.0 에서도 수 있습니다. 사용할 제한 시간 및 상태 정책 toomake 자신을 살펴봅니다. Tooa 쿼럼 응답을 반대로 tooan Azure로 클러스터를 배포 때 사용 되는 hello 매개 toodiffer가 있을 수 있습니다. 신중 hello 제한 시간을 설정 하는 것이 좋습니다.

## <a name="next-steps"></a>다음 단계
[Powershell을 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial-powershell.md) 에서는 PowerShell을 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md)를 사용하여 응용 프로그램 업그레이드 방법을 제어합니다.

응용 프로그램 업그레이드를 학습 하 여 호환 되도록 어떻게 toouse [데이터 직렬화](service-fabric-application-upgrade-data-serialization.md)합니다.

Toouse 너무 참조 하 여 응용 프로그램을 업그레이드 하는 동안 기능에 고급 하는 방법에 대해 알아봅니다[고급 항목](service-fabric-application-upgrade-advanced.md)합니다.

toohello 단계를 참조 하 여 응용 프로그램 업그레이드의 일반적인 문제를 수정 [응용 프로그램 업그레이드 문제 해결](service-fabric-application-upgrade-troubleshooting.md)합니다.

[image1]: media/service-fabric-application-upgrade-tutorial/upgrade7.png
[image2]: media/service-fabric-application-upgrade-tutorial/upgrade1.png
[image3]: media/service-fabric-application-upgrade-tutorial/upgrade5.png
[image4]: media/service-fabric-application-upgrade-tutorial/upgrade6.png
