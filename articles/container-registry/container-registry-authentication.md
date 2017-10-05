---
title: "Azure 컨테이너 레지스트리로 인증 | Microsoft 문서"
description: "Azure Active Directory 서비스 주체 또는 관리자 계정을 사용하여 Azure 컨테이너 레지스트리에 로그인하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: aa2a6bf3d7d9ec22020036851fc0f2bca37e31bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="62c84-103">개인 Docker 컨테이너 레지스트리로 인증</span><span class="sxs-lookup"><span data-stu-id="62c84-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="62c84-104">Azure 컨테이너 레지스트리에서 컨테이너 이미지를 사용하려면 `docker login` 명령을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-104">To work with container images in an Azure container registry, you log in using the `docker login` command.</span></span> <span data-ttu-id="62c84-105">**[Azure Active Directory 서비스 주체](../active-directory/active-directory-application-objects.md)** 또는 레지스트리 특정 **관리자 계정**을 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="62c84-106">이 문서에서는 이러한 ID에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="62c84-107">서비스 주체</span><span class="sxs-lookup"><span data-stu-id="62c84-107">Service principal</span></span>

<span data-ttu-id="62c84-108">레지스트리에 [서비스 주체를 할당](container-registry-get-started-azure-cli.md#assign-a-service-principal)하고 기본 Docker 인증에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) to your registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="62c84-109">대부분의 시나리오에서는 서비스 주체를 사용하도록 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="62c84-110">다음 예제와 같이 서비스 주체의 앱 ID와 암호를 `docker login` 명령에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-110">Provide the app ID and password of the service principal to the `docker login` command, as shown in the following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="62c84-111">로그인하면 Docker에서 자격 증명을 캐시하므로 앱 ID를 기억할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-111">Once logged in, Docker caches the credentials, so you don't need to remember the app ID.</span></span>

> [!TIP]
> <span data-ttu-id="62c84-112">원하는 경우 `az ad sp reset-credentials` 명령을 실행하여 서비스 주체의 암호를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-112">If you want, you can regenerate the password of a service principal by running the `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="62c84-113">서비스 주체는 [역할 기반 액세스](../active-directory/role-based-access-control-configure.md)를 레지스트리에 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) to a registry.</span></span> <span data-ttu-id="62c84-114">사용 가능한 역할은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-114">Available roles are:</span></span>
  * <span data-ttu-id="62c84-115">독자(풀 전용 액세스).</span><span class="sxs-lookup"><span data-stu-id="62c84-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="62c84-116">참가자(풀 및 푸시).</span><span class="sxs-lookup"><span data-stu-id="62c84-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="62c84-117">소유자(풀, 푸시, 다른 사용자에게 역할 할당).</span><span class="sxs-lookup"><span data-stu-id="62c84-117">Owner (pull, push, and assign roles to other users).</span></span>

<span data-ttu-id="62c84-118">Azure Container Registry에서는 익명 액세스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="62c84-119">공용 이미지에는 [Docker 허브](https://docs.docker.com/docker-hub/)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="62c84-120">여러 서비스 주체를 레지스트리에 할당할 수 있으므로 여러 사용자 또는 응용 프로그램에 대한 액세스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-120">You can assign multiple service principals to a registry, which allows you to define access for different users or applications.</span></span> <span data-ttu-id="62c84-121">또한 서비스 주체는 다음 예제와 같은 개발자 또는 DevOps 시나리오에서 레지스트리에 대한 "헤드리스" 연결을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-121">Service principals also enable "headless" connectivity to a registry in developer or DevOps scenarios such as the following examples:</span></span>

  * <span data-ttu-id="62c84-122">레지스트리에서 DC/OS, Docker Swarm 및 Kubernetes를 포함한 오케스트레이션 시스템으로 컨테이너 배포 -</span><span class="sxs-lookup"><span data-stu-id="62c84-122">Container deployments from a registry to orchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="62c84-123">컨테이너 레지스트리를 관련 Azure 서비스(예: [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/) 등)로 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-123">You can also pull container registries to related Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="62c84-124">컨테이너 이미지를 작성하고 레지스트리로 푸시하는 지속적인 통합 및 배포 솔루션(예: Visual Studio Team Services 또는 Jenkins)</span><span class="sxs-lookup"><span data-stu-id="62c84-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them to a registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="62c84-125">관리자 계정</span><span class="sxs-lookup"><span data-stu-id="62c84-125">Admin account</span></span>
<span data-ttu-id="62c84-126">만드는 각 레지스트리에는 관리자 계정이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="62c84-127">기본적으로 계정은 사용할 수 없지만 [포털](container-registry-get-started-portal.md#manage-registry-settings) 또는 [Azure CLI 2.0 명령](container-registry-get-started-azure-cli.md#manage-admin-credentials)을 통해 계정을 사용하도록 설정하고 자격 증명을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-127">By default the account is disabled, but you can enable it and manage the credentials, for example through the [portal](container-registry-get-started-portal.md#manage-registry-settings) or using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="62c84-128">각 관리자 계정은 두 개의 암호가 제공되며, 둘 다 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="62c84-129">두 개의 암호를 사용하면 다른 암호를 다시 생성하는 동안에 하나의 암호를 사용하여 레지스트리에 대한 연결을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-129">The two passwords allow you to maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="62c84-130">계정을 사용할 수 있으면 레지스트리에 대한 기본 인증을 위해 사용자 이름과 둘 중 한 가지 암호를 `docker login` 명령에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-130">If the account is enabled, you can pass the user name and either password to the `docker login` command for basic authentication to the registry.</span></span> <span data-ttu-id="62c84-131">예:</span><span class="sxs-lookup"><span data-stu-id="62c84-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="62c84-132">관리자 계정은 주로 테스트 용도로 단일 사용자가 레지스트리에 액세스하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-132">The admin account is designed for a single user to access the registry, mainly for test purposes.</span></span> <span data-ttu-id="62c84-133">관리자 계정 자격 증명을 다른 사용자와 공유하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-133">It is not recommended to share the admin account credentials among other users.</span></span> <span data-ttu-id="62c84-134">모든 사용자는 레지스트리에서 단일 사용자로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-134">All users appear as a single user to the registry.</span></span> <span data-ttu-id="62c84-135">이 계정을 변경하거나 사용하지 않도록 설정하면 자격 증명을 사용하는 모든 사용자의 레지스트리 액세스는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62c84-135">Changing or disabling this account disables registry access for all users who use the credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="62c84-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="62c84-136">Next steps</span></span>
* <span data-ttu-id="62c84-137">[Docker CLI를 사용하여 첫 번째 이미지 푸시](container-registry-get-started-docker-cli.md)</span><span class="sxs-lookup"><span data-stu-id="62c84-137">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="62c84-138">컨테이너 레지스트리 미리 보기의 인증에 대한 자세한 내용은 [블로그 게시물](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62c84-138">For more information about authentication in the Container Registry preview, see the [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
