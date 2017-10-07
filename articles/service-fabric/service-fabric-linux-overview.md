---
title: "Linux에서 서비스 패브릭 aaaAzure | Microsoft Docs"
description: "서비스 패브릭 클러스터 Linux와 수 toodeploy 및 Linux에서 Java 및 C#에서 작성 하는 호스트 서비스 패브릭 응용 프로그램 수는 Java를 지원 합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a>Linux의 서비스 패브릭
Linux에서 서비스 패브릭의 hello 미리 보기를 사용 하면 toobuild, 배포 및 Windows에서와 마찬가지로 Linux에서 고가용성, 확장성이 높은 응용 프로그램을 관리 합니다. hello 서비스 패브릭 프레임 워크 (신뢰할 수 있는 서비스 및 Reliable Actors)는 Linux에서 java에서 더하기 tooC # (.NET Core)에서 사용할 수 있습니다.  어떤 언어 또는 프레임워크에서도 [게스트 실행 서비스](service-fabric-deploy-existing-app.md) 를 빌드할 수 있습니다. 또한 hello 미리 보기는 오케스트레이션 Docker 컨테이너도 지원합니다. Docker 컨테이너 게스트 실행 파일 또는 hello 서비스 패브릭 프레임 워크를 사용 하는 기본 서비스 패브릭 서비스를 실행할 수 있습니다.

Linux에서 서비스 패브릭은 운영 체제 구체적인 정보 및 프로그래밍 언어 지원) (제외 것과 개념상 동일 tooService windows Fabric를입니다. 따라서 대부분의 우리의 [기존 설명서](http://aka.ms/servicefabricdocs) hello 기술 개념을 익혀야 하는 데 유용한에 적용 됩니다.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a>지원되는 운영 체제 및 프로그래밍 언어
제한 된 hello 미리 보기 만드는 기능을 지원 hello 하나 상자 개발 또한 toomulti 컴퓨터로 Ubuntu Server 16.04를 실행 하는 Azure에서 구성 된 클러스터를 클러스터링 합니다. hello 미리 보기에서는 Reliable Actors hello 및 추가 tooguest 실행 파일 및 Docker 컨테이너 조정에서 Java 및 C#에서 신뢰할 수 있는 상태 비저장 서비스 프레임 워크 hello 합니다.  

> [!NOTE]
> 신뢰할 수 있는 컬렉션은 Linux에서 아직 지원되지 않습니다. 독립 실행형 클러스터 지원 되지 않습니다 하나만 상자 및 Azure Linux 다중 컴퓨터 클러스터 중-hello 미리 보기에서 지원 됩니다.
>
>


## <a name="supported-tooling"></a>지원되는 도구
hello 미리 보기 서비스 패브릭 CLI를 통해 hello 클러스터와의 상호 작용을 지원합니다. Java 개발자를 위해 Linux 및 OSX에서 지원되는 Eclipse에 Eclipse 및 Yeoman과의 통합이 제공됩니다. hello OSX 통합 vagrant 통해 hello 내부적 Linux VM을 사용합니다. C# 개발자를 위한 Yeoman와의 통합 toogenerate 응용 프로그램 템플릿이 제공 됩니다.

## <a name="next-steps"></a>다음 단계

* 익숙해질 목적으로 hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) 및 [신뢰할 수 있는 서비스](service-fabric-reliable-services-introduction.md) 프로그래밍 프레임 워크
* [Linux에서 개발 환경 준비](service-fabric-get-started-linux.md)
* [OSX에서 개발 환경 준비](service-fabric-get-started-mac.md)
* [Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기](service-fabric-create-your-first-linux-application-with-java.md)
* [Jenkins 및 GitHub로 Setup Service Fabric 연속 통합 및 배포 설정](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [Service Fabric Windows/Linux 간 차이점](service-fabric-linux-windows-differences.md)
