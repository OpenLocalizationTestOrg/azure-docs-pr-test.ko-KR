---
title: "앱 서비스 aaaAzure CLI 샘플-| Microsoft Docs"
description: "Azure CLI 샘플 - App Service"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: a943ccffb59c5d30a44cf1ce513fd2eac46101f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples"></a>Azure CLI 샘플

hello 다음 표는 hello Azure CLI를 사용 하 여 빌드된 링크 toobash 스크립트.

| | |
|-|-|
|**앱 만들기**||
| [웹앱 만들기 및 GitHub에서 코드 배포](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| Azure 웹앱을 만들고 공용 GitHub 리포지토리에서 코드를 배포합니다. |
| [GitHub의 연속 배포를 사용하여 웹앱 만들기](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| 사용자가 소유한 GitHub 리포지토리에서 연속 게시를 통해 Azure 웹앱을 만듭니다. |
| [웹앱 만들기 및 로컬 Git 리포지토리의 코드 배포](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | Azure 웹앱을 만들고 로컬 Git 리포지토리의 코드 푸시를 구성합니다. |
| [웹 앱을 만들고 코드 tooa 스테이징 환경 배포](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | 코드 변경 내용을 준비하기 위해 배포 슬롯을 사용하여 Azure 웹앱을 만듭니다. |
| [Docker 컨테이너에서 ASP.NET Core 웹앱 만들기](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| Linux에서 Azure 웹앱을 만들고 Docker Hub의 Docker 이미지를 로드합니다. |
|**앱 구성**||
| [사용자 지정 도메인 tooa 웹 응용 프로그램 맵](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| Azure 웹 앱을 만들고 사용자 지정 도메인 이름을 tooit를 매핑합니다. |
| [사용자 지정 SSL 인증서 tooa 웹 응용 프로그램 바인딩](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| Azure 웹 앱을 만들고 사용자 지정 도메인 이름 tooit의 hello SSL 인증서를 바인딩합니다. |
|**앱 크기 조정**||
| [수동 웹앱 크기 조정](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | Azure 웹앱을 만들고 2개의 인스턴스로 확장합니다. |
| [고가용성 아키텍처로 전 세계 웹앱 크기 조정](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | 두 개의 지역에 두 개의 Azure 웹앱을 만들고 Azure Traffic Manager를 사용하여 단일 끝점을 통해 사용할 수 있습니다. |
|**응용 프로그램 tooresources 연결**||
| [웹 앱 tooa SQL 데이터베이스 연결](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| Azure 웹 앱을 만들고 SQL 데이터베이스를 다음 hello 데이터베이스 연결 문자열 toohello 응용 프로그램 설정을 추가 합니다. |
| [웹 앱 tooa 저장소 계정을 연결 하세요.](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| Azure 웹 앱 및 저장소 계정을 만듭니다 다음 hello 저장소 연결 문자열 toohello 응용 프로그램 설정을 추가 합니다. |
| [웹 앱 tooa redis 캐시를 연결 합니다.](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | Azure 웹 앱 및 redis 캐시를 만든 다음 hello redis 연결 세부 정보 toohello 응용 프로그램 설정을 추가 합니다.) |
| [웹 앱 tooCosmos DB에 연결](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | Azure 웹 앱 및 Cosmos DB 만듭니다 다음 hello Cosmos DB 연결 세부 정보 toohello 응용 프로그램 설정을 추가 합니다. |
|**앱 모니터링**||
| [웹 서버 로그로 웹앱 모니터링](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | Azure 웹 앱을 만들고,에 대해 로깅을 사용 hello 로그 tooyour 로컬 컴퓨터에 다운로드 합니다. |
| | |