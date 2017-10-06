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
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="d1b7f-103">개인 Docker 컨테이너 레지스트리로 인증</span><span class="sxs-lookup"><span data-stu-id="d1b7f-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="d1b7f-104">hello를 사용 하 여 로그인 하면 Azure 컨테이너 레지스트리에 컨테이너 이미지와 toowork, `docker login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-104">toowork with container images in an Azure container registry, you log in using hello `docker login` command.</span></span> <span data-ttu-id="d1b7f-105">**[Azure Active Directory 서비스 주체](../active-directory/active-directory-application-objects.md)** 또는 레지스트리 특정 **관리자 계정**을 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="d1b7f-106">이 문서에서는 이러한 ID에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="d1b7f-107">서비스 주체</span><span class="sxs-lookup"><span data-stu-id="d1b7f-107">Service principal</span></span>

<span data-ttu-id="d1b7f-108">할 수 있습니다 [서비스 사용자를 할당](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour 레지스트리 기본 Docker 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="d1b7f-109">대부분의 시나리오에서는 서비스 주체를 사용하도록 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="d1b7f-110">Hello 서비스 보안 주체 toohello의 hello 응용 프로그램 ID와 암호를 제공 `docker login` hello 다음 예제와 같이 명령:</span><span class="sxs-lookup"><span data-stu-id="d1b7f-110">Provide hello app ID and password of hello service principal toohello `docker login` command, as shown in hello following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="d1b7f-111">로그인 한 Docker tooremember hello 응용 프로그램 id입니다. 필요 하지 hello 자격 증명을 캐시 하는</span><span class="sxs-lookup"><span data-stu-id="d1b7f-111">Once logged in, Docker caches hello credentials, so you don't need tooremember hello app ID.</span></span>

> [!TIP]
> <span data-ttu-id="d1b7f-112">Hello를 실행 하 여 서비스 사용자의 hello 암호를 생성 하려면 원하는 경우 `az ad sp reset-credentials` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-112">If you want, you can regenerate hello password of a service principal by running hello `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="d1b7f-113">서비스 사용자 허용 [역할 기반 액세스](../active-directory/role-based-access-control-configure.md) tooa 레지스트리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) tooa registry.</span></span> <span data-ttu-id="d1b7f-114">사용 가능한 역할은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-114">Available roles are:</span></span>
  * <span data-ttu-id="d1b7f-115">독자(풀 전용 액세스).</span><span class="sxs-lookup"><span data-stu-id="d1b7f-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="d1b7f-116">참가자(풀 및 푸시).</span><span class="sxs-lookup"><span data-stu-id="d1b7f-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="d1b7f-117">소유자 (끌어오기, 푸시 및 할당 역할 tooother 사용자)입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-117">Owner (pull, push, and assign roles tooother users).</span></span>

<span data-ttu-id="d1b7f-118">Azure Container Registry에서는 익명 액세스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="d1b7f-119">공용 이미지에는 [Docker 허브](https://docs.docker.com/docker-hub/)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="d1b7f-120">다른 사용자 또는 응용 프로그램에 대 한 toodefine 액세스 있습니다 tooa 레지스트리 여러 서비스 사용자를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-120">You can assign multiple service principals tooa registry, which allows you toodefine access for different users or applications.</span></span> <span data-ttu-id="d1b7f-121">서비스 사용자는 "헤더 없이" 연결 tooa 레지스트리 개발자 또는 예제 따르는 hello 같은 DevOps 시나리오에도 사용 하도록 설정:</span><span class="sxs-lookup"><span data-stu-id="d1b7f-121">Service principals also enable "headless" connectivity tooa registry in developer or DevOps scenarios such as hello following examples:</span></span>

  * <span data-ttu-id="d1b7f-122">DC/OS, docker는 Docker Swarm Kubernetes 등 레지스트리 tooorchestration 시스템에서 컨테이너 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-122">Container deployments from a registry tooorchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="d1b7f-123">또한 끌어와 컨테이너 레지스트리에 toorelated Azure 서비스와 같은 [컨테이너 서비스](../container-service/index.yml), [앱 서비스](../app-service/index.md), [일괄 처리](../batch/index.md), [서비스 패브릭](/azure/service-fabric/), 등입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-123">You can also pull container registries toorelated Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="d1b7f-124">연속 통합 및 배포 (예: Visual Studio Team Services 또는 Jenkins) 컨테이너 이미지를 작성 하 고 있는 솔루션 푸시 tooa 레지스트리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them tooa registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="d1b7f-125">관리자 계정</span><span class="sxs-lookup"><span data-stu-id="d1b7f-125">Admin account</span></span>
<span data-ttu-id="d1b7f-126">만드는 각 레지스트리에는 관리자 계정이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="d1b7f-127">사용 하도록 설정 하 고 hello 통해 예를 들어 hello 자격 증명을 관리할 수 있지만 기본적으로 hello 계정이 비활성화 된 [포털](container-registry-get-started-portal.md#manage-registry-settings) hello를 사용 하 여 또는 [Azure CLI 2.0 명령은](container-registry-get-started-azure-cli.md#manage-admin-credentials)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-127">By default hello account is disabled, but you can enable it and manage hello credentials, for example through hello [portal](container-registry-get-started-portal.md#manage-registry-settings) or using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="d1b7f-128">각 관리자 계정은 두 개의 암호가 제공되며, 둘 다 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="d1b7f-129">두 개의 암호가 hello를 사용 하 여 하나의 암호 hello를 다시 생성 하는 동안 다른 암호 toomaintain 연결 toohello 레지스트리를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-129">hello two passwords allow you toomaintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="d1b7f-130">Hello 사용자 이름 및 암호 toohello 중 하나를 전달할 수 hello 계정이 사용 되 면 `docker login` 기본 인증 toohello 레지스트리에 대 한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-130">If hello account is enabled, you can pass hello user name and either password toohello `docker login` command for basic authentication toohello registry.</span></span> <span data-ttu-id="d1b7f-131">예:</span><span class="sxs-lookup"><span data-stu-id="d1b7f-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="d1b7f-132">hello 관리자 계정은 주로 테스트를 위해 단일 사용자 tooaccess hello 레지스트리를 위해 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-132">hello admin account is designed for a single user tooaccess hello registry, mainly for test purposes.</span></span> <span data-ttu-id="d1b7f-133">Tooshare hello 관리자 계정 자격 증명 다른 사용자 사이는 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-133">It is not recommended tooshare hello admin account credentials among other users.</span></span> <span data-ttu-id="d1b7f-134">모든 사용자를 단일 사용자 toohello 레지스트리로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-134">All users appear as a single user toohello registry.</span></span> <span data-ttu-id="d1b7f-135">이 계정은 사용 하지 않도록 설정 하거나 변경 hello 자격 증명을 사용 하는 모든 사용자에 대 한 레지스트리 액세스를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-135">Changing or disabling this account disables registry access for all users who use hello credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="d1b7f-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d1b7f-136">Next steps</span></span>
* <span data-ttu-id="d1b7f-137">[Hello Docker CLI를 사용 하 여 첫 번째 이미지 푸시](container-registry-get-started-docker-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-137">[Push your first image using hello Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="d1b7f-138">인증 hello 컨테이너 레지스트리 미리 보기에 대 한 자세한 내용은 참조 hello [블로그 게시물](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b7f-138">For more information about authentication in hello Container Registry preview, see hello [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
