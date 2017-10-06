---
title: "Azure 컨테이너 레지스트리에 aaaAuthenticate | Microsoft Docs"
description: "주 서버 또는 관리자 계정을 Azure Active Directory를 사용 하 여 tooan Azure 컨테이너 레지스트리에 toolog 서비스 하는 방법"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>개인 Docker 컨테이너 레지스트리로 인증
hello를 사용 하 여 로그인 하면 Azure 컨테이너 레지스트리에 컨테이너 이미지와 toowork, `docker login` 명령입니다. **[Azure Active Directory 서비스 주체](../active-directory/active-directory-application-objects.md)** 또는 레지스트리 특정 **관리자 계정**을 사용하여 로그인할 수 있습니다. 이 문서에서는 이러한 ID에 대해 자세히 설명합니다.



## <a name="service-principal"></a>서비스 주체

할 수 있습니다 [서비스 사용자를 할당](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour 레지스트리 기본 Docker 인증을 사용 합니다. 대부분의 시나리오에서는 서비스 주체를 사용하도록 권장됩니다. Hello 서비스 보안 주체 toohello의 hello 응용 프로그램 ID와 암호를 제공 `docker login` hello 다음 예제와 같이 명령:

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

로그인 한 Docker tooremember hello 응용 프로그램 id입니다. 필요 하지 hello 자격 증명을 캐시 하는

> [!TIP]
> Hello를 실행 하 여 서비스 사용자의 hello 암호를 생성 하려면 원하는 경우 `az ad sp reset-credentials` 명령입니다.
>


서비스 사용자 허용 [역할 기반 액세스](../active-directory/role-based-access-control-configure.md) tooa 레지스트리 합니다. 사용 가능한 역할은 다음과 같습니다.
  * 독자(풀 전용 액세스).
  * 참가자(풀 및 푸시).
  * 소유자 (끌어오기, 푸시 및 할당 역할 tooother 사용자)입니다.

Azure Container Registry에서는 익명 액세스를 사용할 수 없습니다. 공용 이미지에는 [Docker 허브](https://docs.docker.com/docker-hub/)를 사용할 수 있습니다.

다른 사용자 또는 응용 프로그램에 대 한 toodefine 액세스 있습니다 tooa 레지스트리 여러 서비스 사용자를 할당할 수 있습니다. 서비스 사용자는 "헤더 없이" 연결 tooa 레지스트리 개발자 또는 예제 따르는 hello 같은 DevOps 시나리오에도 사용 하도록 설정:

  * DC/OS, docker는 Docker Swarm Kubernetes 등 레지스트리 tooorchestration 시스템에서 컨테이너 배포 합니다. 또한 끌어와 컨테이너 레지스트리에 toorelated Azure 서비스와 같은 [컨테이너 서비스](../container-service/index.yml), [앱 서비스](../app-service/index.md), [일괄 처리](../batch/index.md), [서비스 패브릭](/azure/service-fabric/), 등입니다.

  * 연속 통합 및 배포 (예: Visual Studio Team Services 또는 Jenkins) 컨테이너 이미지를 작성 하 고 있는 솔루션 푸시 tooa 레지스트리 합니다.





## <a name="admin-account"></a>관리자 계정
만드는 각 레지스트리에는 관리자 계정이 자동으로 만들어집니다. 사용 하도록 설정 하 고 hello 통해 예를 들어 hello 자격 증명을 관리할 수 있지만 기본적으로 hello 계정이 비활성화 된 [포털](container-registry-get-started-portal.md#manage-registry-settings) hello를 사용 하 여 또는 [Azure CLI 2.0 명령은](container-registry-get-started-azure-cli.md#manage-admin-credentials)합니다. 각 관리자 계정은 두 개의 암호가 제공되며, 둘 다 다시 생성할 수 있습니다. 두 개의 암호가 hello를 사용 하 여 하나의 암호 hello를 다시 생성 하는 동안 다른 암호 toomaintain 연결 toohello 레지스트리를 허용 합니다. Hello 사용자 이름 및 암호 toohello 중 하나를 전달할 수 hello 계정이 사용 되 면 `docker login` 기본 인증 toohello 레지스트리에 대 한 명령입니다. 예:

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> hello 관리자 계정은 주로 테스트를 위해 단일 사용자 tooaccess hello 레지스트리를 위해 설계 되었습니다. Tooshare hello 관리자 계정 자격 증명 다른 사용자 사이는 권장 되지 않습니다. 모든 사용자를 단일 사용자 toohello 레지스트리로 표시 됩니다. 이 계정은 사용 하지 않도록 설정 하거나 변경 hello 자격 증명을 사용 하는 모든 사용자에 대 한 레지스트리 액세스를 사용 하지 않습니다.
>


### <a name="next-steps"></a>다음 단계
* [Hello Docker CLI를 사용 하 여 첫 번째 이미지 푸시](container-registry-get-started-docker-cli.md)합니다.
* 인증 hello 컨테이너 레지스트리 미리 보기에 대 한 자세한 내용은 참조 hello [블로그 게시물](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/)합니다.
