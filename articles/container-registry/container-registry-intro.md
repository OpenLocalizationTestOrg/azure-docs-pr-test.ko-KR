---
title: "Azure에서 Docker 컨테이너 레지스트리에 aaaPrivate | Microsoft Docs"
description: "소개 toohello Azure 컨테이너 레지스트리 서비스, 클라우드 기반, 관리, 개인 Docker 레지스트리를 제공 합니다."
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f6edcf0bf947b7770ee0a4e4a5cfbf4ef8b7392a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooprivate-docker-container-registries"></a>소개 tooprivate Docker 컨테이너 레지스트리


Azure 컨테이너 레지스트리는 관리 되는 [Docker 레지스트리](https://docs.docker.com/registry/) 에 따라 서비스 hello Docker 레지스트리 2.0 오픈 소스입니다. 만들기 및 Azure 컨테이너 레지스트리에 toostore를 유지 하 고, 개인 관리 [Docker 컨테이너](https://www.docker.com/what-docker) 이미지입니다. 기존 컨테이너 개발 및 배포 파이프라인을 사용 하 여 Azure에서 컨테이너 레지스트리를 사용 하 여 및 Docker 커뮤니티 전문 hello 본문에 그립니다.

Docker 및 컨테이너에 대한 기본 지식은 다음을 참조하세요.

* [Docker 사용자 가이드](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a>사용 사례
레지스트리 toovarious 배포 대상 Azure 컨테이너에서 이미지를 가져올:

* **확장성 있는 오케스트레이션 시스템**: [DC/OS](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/) 및 [Kubernetes](http://kubernetes.io/docs/)를 포함하는 호스트 클러스터에서 컨테이너화된 응용 프로그램을 관리합니다.
* **Azure 서비스**는 [컨테이너 서비스](../container-service/index.yml), [App Service](/app-service/index.md), [Batch](../batch/index.md) 및 [Service Fabric](/azure/service-fabric/)을 포함하는 대규모 응용 프로그램 빌드 및 실행을 지원합니다.

개발자가 컨테이너 개발 워크플로의 일부로 tooa 컨테이너 레지스트리를 푸시할 수 있습니다. 예를 들어 [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) 또는 [Jenkins](https://jenkins.io/)와 같은 배포 도구 및 지속적인 통합의 컨테이너 레지스트리를 대상으로 합니다.





## <a name="key-concepts"></a>주요 개념
* **레지스트리** - Azure 구독 내에서 하나 이상의 컨테이너 레지스트리를 만듭니다. 각 레지스트리는 표준 Azure에서 지원 되며 [저장소 계정](../storage/common/storage-introduction.md) hello에 동일한 위치입니다. Hello에 레지스트리 키를 만들어서 로컬, 네트워크 닫기 저장소 컨테이너 이미지를 활용 하면 배포와 같은 Azure 위치입니다. 정규화 된 레지스트리 이름에는 hello 폼 `myregistry.azurecr.io`합니다.

  하면 [액세스 제어](container-registry-authentication.md) Azure Active Directory 기반을 사용 하 여 tooa 컨테이너 레지스트리 [서비스 사용자](../active-directory/active-directory-application-objects.md) 또는 제공 된 관리자 계정. 표준 실행된 hello `docker login` 는 레지스트리에 tooauthenticate 명령입니다.

* **관리되는 레지스트리** - 세 가지 SKU, 즉 Basic, Standard 및 Premium으로 레지스트리에 대한 추가 기능을 제공하는 계층입니다. 이러한 Sku의 hello 이미지 hello 안정성을 향상 시키고 새 기능을 사용할 수 있는 Azure 컨테이너 레지스트리에 서비스에서 관리 하는 저장소 계정에 저장 됩니다. 새로운 기능에는 웹후크 통합, Azure Active Directory를 사용한 리포지토리 인증 및 삭제 기능 지원이 포함됩니다. 사용자는 관리 되는 레지스트리 또는 toocreate 간의 hello 옵션 toochoose 레지스트리를 만들 때 고유 저장소 계정에서 지 원하는 레지스트리를 있습니다.

* **리포지토리** - 레지스트리는 컨테이너 이미지 그룹인 하나 이상의 리포지토리를 포함합니다. Azure Container Registry는 다단계 리포지토리 네임스페이스를 지원합니다. 이 기능을 통해 이미지 관련된 tooa 특정 앱의 있습니다 toogroup 컬렉션 또는 앱 toospecific 개발 또는 운영 팀의 컬렉션입니다. 예:

  * `myregistry.azurecr.io/aspnetcore:1.0.1`은 회사 차원의 이미지를 나타냅니다.
  * `myregistry.azurecr.io/warrantydept/dotnet-build`나타냅니다 이미지 hello 보증 부서 간에 공유 toobuild.NET 응용 프로그램 사용
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web`hello 보증 부서별로 소유 hello 고객 제출 앱에서 그룹화 웹 이미지를 나타냅니다.

* **이미지** - 리포지토리에 저장되며 각 이미지는 Docker 컨테이너의 읽기 전용 스냅숏입니다. Azure 컨테이너 레지스트리는 Windows 및 Linux 이미지 모두를 포함할 수 있습니다. 모든 컨테이너 배포에 대한 이미지 이름을 제어합니다. 사용 하 여 표준 [Docker 명령을](https://docs.docker.com/engine/reference/commandline/) toopush 이미지, repository 또는 이미지 리포지토리에서 끌어오기를 합니다.

* **컨테이너** - 컨테이너는 소프트웨어 응용 프로그램을 정의하며 코드, 런타임, 시스템 도구 및 라이브러리를 포함하는 완전한 파일 시스템으로 래핑된 종속성을 정의합니다. 컨테이너 레지스트리에서 끌어온 Windows 또는 Linux 이미지를 기반으로 Docker 컨테이너를 실행합니다. 단일 컴퓨터에서 실행 되는 컨테이너 hello 운영 체제 커널을 공유 합니다. Docker 컨테이너 완전히 이식 가능 tooall 주요 Linux 배포판, Mac 및 Windows는입니다.




## <a name="next-steps"></a>다음 단계
* [Hello Azure 포털을 사용 하 여 컨테이너 레지스트리 만들기](container-registry-get-started-portal.md)
* [Hello Azure CLI를 사용 하 여 컨테이너 레지스트리 만들기](container-registry-get-started-azure-cli.md)
* [Hello Docker CLI를 사용 하 여 첫 번째 이미지 강제](container-registry-get-started-docker-cli.md)
* toobuild 연속 통합 및 배포 워크플로 Visual Studio Team Services, Azure 컨테이너 서비스 및 Azure 컨테이너 레지스트리를 사용 하 여 참조 [이 자습서](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md)합니다.
* Tooset (공용 끝점) 없이 Azure에서 직접 Docker 개인 레지스트리를 원하는 경우 참조 [배포 사용자 고유의 개인 Docker 레지스트리 Azure에서](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md)합니다.
