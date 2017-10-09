---
title: "aaaAzure 컨테이너 서비스 자습서-앱 준비 | Microsoft Docs"
description: "Azure Container Service 자습서 - 앱 준비"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a>Azure 컨테이너 서비스와 함께 사용할 컨테이너 이미지 toobe 만들기

7개 중 1단계인 이 자습서에서는 Kubernetes에서 사용할 수 있도록 다중 컨테이너 응용 프로그램을 준비하는 과정입니다. 완료되는 단계는 다음과 같습니다.  

> [!div class="checklist"]
> * GitHub에서 응용 프로그램 소스 복제  
> * Hello 응용 프로그램 소스에서 컨테이너 이미지 만들기
> * 로컬 Docker 환경에서 hello 응용 프로그램 테스트

완료 되 면 hello 다음 응용 프로그램은 로컬 개발 환경에서 액세스할 수 있습니다.

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/azure-vote.png)

이후 자습서 hello 컨테이너 이미지는 업로드 된 tooan Azure 컨테이너 레지스트리 하 고 Azure에서 실행 Kubernetes 클러스터를 호스트 하는 다음 합니다.

## <a name="before-you-begin"></a>시작하기 전에

이 자습서에서는 컨테이너, 컨테이너 이미지 및 기본 Docker 명령과 같은 핵심 Docker 개념에 대한 기본적인 지식이 있다고 가정합니다. 필요한 경우 컨테이너 기본 사항에 대한 입문서는 [Get started with Docker(Docker 시작)]( https://docs.docker.com/get-started/)를 참조하세요. 

toocomplete이이 자습서에서는 Docker 개발 환경이 필요 합니다. Docker는 모든 [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) 또는 [Linux](https://docs.docker.com/engine/installation/#supported-platforms) 시스템에서 쉽게 Docker를 구성하는 패키지를 제공합니다.

## <a name="get-application-code"></a>응용 프로그램 코드 가져오기

이 자습서에 사용 된 hello 샘플 응용 프로그램은 기본 투표 앱입니다. hello 응용 프로그램 웹 프런트 엔드 구성 요소 및 백 엔드 Redis 인스턴스에서 구성 됩니다. hello 웹 구성 요소는 사용자 지정 컨테이너 이미지에 패키지 됩니다. hello Redis 인스턴스 Docker 허브에서 수정 되지 않은 이미지를 사용합니다.  

Git toodownload hello 응용 프로그램 tooyour 개발 환경의 복사본을 사용 합니다.

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

내부 hello에 대 한 복제 된 디렉터리는 hello 응용 프로그램 소스 코드, 미리 생성된 된 Docker 파일과 Kubernetes 매니페스트 파일을 작성 합니다. 이러한 파일은 hello 자습서 집합에서 사용 되는 toocreate 자산입니다. 

## <a name="create-container-images"></a>컨테이너 이미지 만들기

[Docker Compose](https://docs.docker.com/compose/) 수 tooautomate hello 빌드 컨테이너 이미지와 hello 다중 컨테이너 응용 프로그램 배포를 사용 합니다.

Hello docker compose.yml 파일 toocreate hello 컨테이너 이미지를 실행 다운로드 hello 이미지, Redis 하 고 hello 응용 프로그램을 시작 합니다.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

완료 되 면 hello를 사용 하 여 [docker 이미지](https://docs.docker.com/engine/reference/commandline/images/) toosee hello 만든 이미지 명령입니다.

```bash
docker images
```

세 개의 이미지가 다운로드되거나 생성되었는지 확인합니다. hello *azure 투표 프런트* 이미지 hello 응용 프로그램에 포함 되어 있습니다. Hello에서 파생 된 *nginx 플라스* 이미지입니다. Docker 허브에서 hello Redis 이미지 다운로드 되었습니다.

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

Hello 실행 [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) 명령 toosee hello 컨테이너를 실행 합니다.

```bash
docker ps
```

출력:

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a>로컬에서 응용 프로그램 테스트

응용 프로그램을 실행 하는 toohttp://localhost:8080 toosee hello를 찾습니다.

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a>리소스 정리

응용 프로그램의 기능을 확인 했으므로 hello 실행 중인 컨테이너를 중지 하 고 제거할 수 있습니다. Hello 컨테이너 이미지를 삭제 하지 마십시오. hello *azure 투표 프런트* 이미지가 업로드 된 tooan Azure 컨테이너 레지스트리 인스턴스 hello 다음 자습서입니다.

실행 중인 컨테이너 toostop hello 다음 hello를 실행 합니다.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

다음 명령을 hello로 중지 hello 컨테이너를 삭제 합니다.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

작업이 완료 되 면 언제 hello Azure 투표 응용 프로그램을 포함 하는 컨테이너 이미지를 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 응용 프로그램 테스트 및 hello 응용 프로그램에 대 한 컨테이너 이미지를 생성 합니다. 단계를 수행 하는 hello 완료 되었습니다.

> [!div class="checklist"]
> * GitHub에서 응용 프로그램 소스 hello 복제  
> * 응용 프로그램 원본에서 컨테이너 이미지 만들기
> * 로컬 Docker 환경에서 테스트 된 hello 응용 프로그램

Azure 컨테이너 레지스트리에 컨테이너 이미지를 저장 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
> [푸시 이미지 tooAzure 컨테이너 레지스트리](./container-service-tutorial-kubernetes-prepare-acr.md)
