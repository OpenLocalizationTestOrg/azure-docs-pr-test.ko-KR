---
title: "컨테이너 인스턴스 자습서-aaaAzure 앱 준비 | Azure 문서"
description: "응용 프로그램 배포 tooAzure 컨테이너 인스턴스 준비"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a>컨테이너에 대 한 배포 tooAzure 컨테이너 인스턴스 만들기

Azure Container Instances를 통해 어떠한 가상 컴퓨터를 프로비전하지 않고 또 더 높은 수준의 서비스를 채택하지 않고도 Azure로 Docker 컨테이너를 배포할 수 있습니다. 이 자습서에서는 Node.js에서 간단한 웹 응용 프로그램을 빌드하고 Azure Container Instances를 사용하여 실행할 수 있는 컨테이너로 패키지합니다. 다음 내용을 설명합니다.

> [!div class="checklist"]
> * GitHub에서 응용 프로그램 소스 복제  
> * 응용 프로그램 소스에서 컨테이너 이미지 만들기
> * Hello 이미지 로컬 Docker 환경에서 테스트

후속 자습서에서는 사용자 이미지 tooan Azure 컨테이너 레지스트리 업로드 한 후에 tooAzure 컨테이너 인스턴스를 배포 합니다.

## <a name="before-you-begin"></a>시작하기 전에

이 자습서에서는 컨테이너, 컨테이너 이미지 및 기본 Docker 명령과 같은 핵심 Docker 개념에 대한 기본적인 지식이 있다고 가정합니다. 필요한 경우 컨테이너 기본 사항에 대한 입문서는 [Get started with Docker(Docker 시작)]( https://docs.docker.com/get-started/)를 참조하세요. 

toocomplete이이 자습서에서는 Docker 개발 환경이 필요 합니다. Docker는 모든 [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) 또는 [Linux](https://docs.docker.com/engine/installation/#supported-platforms) 시스템에서 쉽게 Docker를 구성하는 패키지를 제공합니다.

## <a name="get-application-code"></a>응용 프로그램 코드 가져오기

이 자습서에서는 hello 샘플에서 기본적으로 제공 하는 간단한 웹 응용 프로그램에 포함 되어 [Node.js](http://nodejs.org)합니다. hello 앱 정적 HTML 페이지를 사용 되 고는 다음과 같습니다.

![브라우저에 표시된 자습서 앱][aci-tutorial-app]

Git toodownload hello 샘플을 사용 합니다.

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a>Hello 컨테이너 이미지 만들기

Dockerfile hello 샘플 리포지토리에 제공 된 hello hello 컨테이너 빌드되는 방식을 보여 줍니다. 시작 되는 [공식 Node.js 이미지] [ dockerhub-nodeimage] 기반 [Alpine Linux](https://alpinelinux.org/), 컨테이너와 적합된 toouse 있는 소규모 배포 합니다. 그런 다음 hello 컨테이너로 hello 응용 프로그램 파일을 복사, hello Node Package Manager를 사용 하 여 종속성을 설치 및 마지막으로 hello 응용 프로그램을 시작 합니다.

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

사용 하 여 hello `docker build` 명령 toocreate hello 컨테이너 이미지를로 태그 지정 *aci 자습서 앱*:

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

사용 하 여 hello `docker images` toosee hello 빌드된 이미지:

```bash
docker images
```

출력:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a>Hello 컨테이너를 로컬로 실행

Hello 컨테이너 tooAzure 컨테이너 인스턴스 배포를 시도 하기 전에 로컬로 실행 작동 tooconfirm 합니다. hello `-d` 스위치를 통해 hello 컨테이너 hello 백그라운드에서 실행 하는 동안 `-p` toomap 프로그램 계산 tooport hello 컨테이너에는 80에는 임의의 포트가 있습니다.

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

컨테이너 hello open hello 브라우저 toohttp://localhost:8080 tooconfirm ï ´ ù.

![Hello 브라우저에서 로컬로 실행 중인 hello 응용 프로그램][aci-tutorial-app-local]

## <a name="next-steps"></a>다음 단계

이 자습서에서는 배포 된 tooAzure 컨테이너 인스턴스 수 있는 컨테이너 이미지를 만들었습니다. 단계를 수행 하는 hello 완료 되었습니다.

> [!div class="checklist"]
> * GitHub에서 응용 프로그램 소스 hello 복제  
> * 응용 프로그램 소스에서 컨테이너 이미지 만들기
> * Hello 컨테이너 로컬로 테스트

Azure 컨테이너 레지스트리에 컨테이너 이미지를 저장 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
> [푸시 이미지 tooAzure 컨테이너 레지스트리](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png