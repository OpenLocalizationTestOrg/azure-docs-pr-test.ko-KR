---
title: "aaaIntroduction tooAzure Kubernetes에 대 한 컨테이너 서비스 | Microsoft Docs"
description: "Kubernetes에 대 한 컨테이너 서비스를 azure 간단한 toodeploy 있고 Azure에서 컨테이너 기반 응용 프로그램을 관리 합니다."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes, Docker, 컨테이너, 마이크로 서비스, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a>소개 tooAzure Kubernetes에 대 한 컨테이너 서비스
간단한 toocreate Kubernetes에 대 한 azure 컨테이너 서비스를 통해 구성 하 고 미리 구성 된 toorun 컨테이너 화 가능한 응용 프로그램이 있는 가상 컴퓨터의 클러스터를 관리 합니다. Toouse 있습니다를 통해 기존 기술을 사용 하면이 커뮤니티 전문, toodeploy 크기가 크고 점점 본문에 대해 하 고 Microsoft Azure에서 컨테이너 기반 응용 프로그램을 관리 합니다.

Azure 컨테이너 서비스를 사용 하면 활용 hello Azure의 엔터프라이즈급 기능 Kubernetes 통해 응용 프로그램 이식성을 유지 하면서 수 있으며 Docker 이미지 형식 hello 수 있습니다.

## <a name="using-azure-container-service-for-kubernetes"></a>Kubernetes용 Azure Container Service 사용
Azure 컨테이너 서비스와 이러한 목표는 오픈 소스 도구와 기술을 담아 고객 사이에서 인기 오늘을 통해 tooprovide 컨테이너 호스팅 환경입니다. toothis 끝 hello 표준 Kubernetes API 끝점을 공개 했습니다. 이러한 표준 끝점을 사용 하 여 tooa Kubernetes 클러스터 통신의 대상이 될 수 있는 모든 소프트웨어를 활용할 수 있습니다. 예를 들어 [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) 또는 [draft](https://github.com/Azure/draft)를 선택할 수 있습니다.

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a>Azure Container Service를 사용하여 Kubernetes 클러스터 만들기
Azure 컨테이너 서비스를 사용 하 여 toobegin hello로 Azure 컨테이너 서비스 클러스터를 배포할 [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) 또는 hello 포털을 통해 (마켓플레이스 검색 hello에 대 한 **Azure 컨테이너 서비스**). Hello Azure 리소스 관리자 템플릿을 통해 더 많은 제어를 필요로 하는 고급 사용자 인 경우 hello 오픈 소스를 사용할 수 있습니다 [acs 엔진](https://github.com/Azure/acs-engine) 프로젝트 toobuild 사용자 고유의 사용자 지정 Kubernetes 클러스터링 하 고 hello를 통해 배포 `az` CLI 합니다.

### <a name="using-kubernetes"></a>Kubernetes 사용
Kubernetes는 컨테이너화된 응용 프로그램의 배포, 크기 조정 및 관리를 자동화합니다. 여기에는 다음과 같이 풍부한 기능들이 포함되어 있습니다.
* 자동 저장소 적재
* 자동 복구
* 수평적 크기 조정
* 서비스 검색 및 부하 분산
* 자동화된 롤아웃 및 롤백
* 비밀 및 구성 관리
* 저장소 오케스트레이션
* 일괄 처리 실행

Azure Container Service를 통해 배포된 Kubernetes의 아키텍처 다이어그램:

![Azure 컨테이너 서비스 toouse Kubernetes를 구성합니다.](media/acs-intro/kubernetes.png)

## <a name="videos"></a>비디오

Azure Container Services의 Kubernetes 지원(Azure Friday, 2017년 1월):

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

Kubernetes에서 응용 프로그램을 개발 및 배포하기 위한 도구(Azure OpenDev, 2017년 6월):

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a>다음 단계

Hello 탐색 [Kubernetes 퀵 스타트](container-service-kubernetes-walkthrough.md) toobegin 오늘날 Azure 컨테이너 서비스를 탐색 합니다.
