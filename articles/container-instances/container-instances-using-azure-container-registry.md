---
title: "Azure 컨테이너 레지스트리 hello에서 컨테이너 인스턴스 aaaDeploy tooAzure | Azure 문서"
description: "Azure 컨테이너 레지스트리 hello에서 tooAzure 컨테이너 인스턴스를 배포"
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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a><span data-ttu-id="f5aa6-103">Azure 컨테이너 레지스트리 hello에서 tooAzure 컨테이너 인스턴스를 배포</span><span class="sxs-lookup"><span data-stu-id="f5aa6-103">Deploy tooAzure Container Instances from hello Azure Container Registry</span></span>

<span data-ttu-id="f5aa6-104">Azure 컨테이너 레지스트리 hello Docker 컨테이너 이미지에 대 한 Azure 기반, 사설 레지스트리입니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-104">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="f5aa6-105">이 문서에서는 어떻게 toodeploy 컨테이너 이미지에에서 저장 된 Azure 컨테이너 레지스트리 hello tooAzure 컨테이너 인스턴스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-105">This article covers how toodeploy container images stored in hello Azure Container Registry tooAzure Container Instances.</span></span>

## <a name="using-hello-azure-cli"></a><span data-ttu-id="f5aa6-106">Hello Azure CLI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f5aa6-106">Using hello Azure CLI</span></span>

<span data-ttu-id="f5aa6-107">hello Azure CLI 만들고 컨테이너 인스턴스를 Azure에서 컨테이너를 관리 하기 위한 명령이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-107">hello Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="f5aa6-108">Hello에 대 한 개인 이미지를 지정 하면 `create` 명령을 hello 컨테이너 레지스트리에 hello 이미지 레지스트리는 데 필요한 암호 tooauthenticate을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-108">If you specify a private image in hello `create` command, you can also specify hello image registry password required tooauthenticate with hello container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="f5aa6-109">hello `create` hello를 지정 하는 지원도 명령을 `registry-login-server` 및 `registry-username`합니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-109">hello `create` command also supports specifying hello `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="f5aa6-110">그러나 Azure 컨테이너 레지스트리 hello에 대 한 hello 로그인 서버는 항상 *registryname*. azurecr.io 및 hello 기본 사용자 이름은 *registryname*이므로 이러한 값 hello 이미지 이름에서 유추 하는 경우 명시적으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-110">However, hello login server for hello Azure Container Registry is always *registryname*.azurecr.io and hello default username is *registryname*, so these values are inferred from hello image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="f5aa6-111">Azure Resource Manager 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="f5aa6-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="f5aa6-112">Hello를 포함 하 여 Azure 리소스 관리자 템플릿을의 Azure 컨테이너 레지스트리 hello 속성을 지정할 수 있습니다 `imageRegistryCredentials` hello 컨테이너 그룹 정의 속성:</span><span class="sxs-lookup"><span data-stu-id="f5aa6-112">You can specify hello properties of your Azure Container Registry in an Azure Resource Manager template by including hello `imageRegistryCredentials` property in hello container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="f5aa6-113">컨테이너 레지스트리 암호 hello 서식 파일에 직접 저장 tooavoid에 암호로 저장 하는 것이 좋습니다 [Azure 키 자격 증명 모음](../key-vault/key-vault-manage-with-cli2.md) hello를 사용 하 여 hello 템플릿을에서 참조 하 고 [간의 네이티브 통합 Azure 리소스 관리자 및 주요 자격 증명 모음 hello](../azure-resource-manager/resource-manager-keyvault-parameter.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-113">tooavoid storing your container registry password directly in hello template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in hello template using hello [native integration between hello Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="f5aa6-114">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f5aa6-114">Using hello Azure portal</span></span>

<span data-ttu-id="f5aa6-115">Azure 컨테이너 레지스트리 hello에서 컨테이너 이미지를 유지 하는 경우 hello Azure 포털을 사용 하 여 Azure 컨테이너 인스턴스에서 컨테이너를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-115">If you maintain container images in hello Azure Container Registry, you can easily create a container in Azure Container Instances using hello Azure portal.</span></span>

1. <span data-ttu-id="f5aa6-116">Azure 포털 hello tooyour 컨테이너 레지스트리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-116">In hello Azure portal, navigate tooyour container registry.</span></span>

2. <span data-ttu-id="f5aa6-117">리포지토리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-117">Choose Repositories.</span></span>

    ![hello Azure 포털의에서 hello Azure 컨테이너 레지스트리 메뉴][acr-menu]

3. <span data-ttu-id="f5aa6-119">toodeploy 원하는 hello 리포지토리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-119">Choose hello repository that you want toodeploy from.</span></span>

4. <span data-ttu-id="f5aa6-120">Hello 태그를 마우스 오른쪽 단추로 클릭 하려는 toodeploy hello 컨테이너 이미지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-120">Right-click hello tag for hello container image you want toodeploy.</span></span>

    ![Azure Container Instances를 사용하여 컨테이너를 시작하기 위한 상황에 맞는 메뉴][acr-runinstance-contextmenu]

5. <span data-ttu-id="f5aa6-122">Hello 컨테이너에 대 한 이름 및 hello 리소스 그룹에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-122">Enter a name for hello container and a name for hello resource group.</span></span> <span data-ttu-id="f5aa6-123">원하는 경우에 hello 기본값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-123">You can also change hello default values if you wish.</span></span>

    ![Azure Container Instances의 만들기 메뉴][acr-create-deeplink]

6. <span data-ttu-id="f5aa6-125">Hello 배포 완료 되 면 해당 IP 주소 및 기타 속성 hello 알림 창 toofind에서 toohello 컨테이너 그룹을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-125">Once hello deployment completes, you can navigate toohello container group from hello notifications pane toofind its IP address and other properties.</span></span>

    ![Azure Container Instances 컨테이너 그룹의 세부 정보 보기][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="f5aa6-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5aa6-127">Next steps</span></span>

<span data-ttu-id="f5aa6-128">Toobuild 컨테이너 tooa 개인 컨테이너 레지스트리, 푸시 및 여 tooAzure 컨테이너 인스턴스를 배포 방법에 대해 알아봅니다 [hello 자습서 완료](container-instances-tutorial-prepare-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5aa6-128">Learn how toobuild containers, push them tooa private container registry, and deploy them tooAzure Container Instances by [completing hello tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
