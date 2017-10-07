---
title: "hello Azure CLI로 aaaSelect Linux VM 이미지 | Microsoft Docs"
description: "Azure CLI toodetermine hello 게시자, 제품, SKU 및 마켓플레이스 VM 이미지에 대 한 버전 toouse hello 하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a><span data-ttu-id="d7164-103">Linux VM toofind hello Azure CLI로 hello Azure 마켓플레이스 이미지 방법</span><span class="sxs-lookup"><span data-stu-id="d7164-103">How toofind Linux VM images in hello Azure Marketplace with hello Azure CLI</span></span>
<span data-ttu-id="d7164-104">이 항목에서는 toouse hello Azure Marketplace에서에서 Azure CLI 2.0 toofind VM 이미지를 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-104">This topic describes how toouse hello Azure CLI 2.0 toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="d7164-105">Linux VM을 만들 때이 정보 toospecify 마켓플레이스 이미지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-105">Use this information toospecify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="d7164-106">Hello를 최신 버전 설치 되었는지 확인 [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정에에서 기록 됩니다 (`az login`).</span><span class="sxs-lookup"><span data-stu-id="d7164-106">Make sure that you installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in tooan Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="d7164-107">용어</span><span class="sxs-lookup"><span data-stu-id="d7164-107">Terminology</span></span>

<span data-ttu-id="d7164-108">마켓플레이스 이미지 hello CLI 및 tooa 계층 구조에 따라 다른 Azure 도구에서 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-108">Marketplace images are identified in hello CLI and other Azure tools according tooa hierarchy:</span></span>

* <span data-ttu-id="d7164-109">**게시자** -hello hello 이미지를 만든 조직입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-109">**Publisher** - hello organization that created hello image.</span></span> <span data-ttu-id="d7164-110">예제: Canonical</span><span class="sxs-lookup"><span data-stu-id="d7164-110">Example: Canonical</span></span>
* <span data-ttu-id="d7164-111">**Offer** - 게시자에 의해 생성 되는 관련 이미지 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="d7164-112">예제: Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="d7164-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="d7164-113">**SKU** - 제공의 인스턴스(예: 배포의 주 릴리스)입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="d7164-114">예제: 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="d7164-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="d7164-115">**버전** -hello SKU 이미지의 버전 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-115">**Version** - hello version number of an image SKU.</span></span> <span data-ttu-id="d7164-116">Hello 이미지를 지정할 때는 바꿀 수 있습니다 hello 버전 번호 "최신" hello hello 분포의 최신 버전을 선택 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-116">When specifying hello image, you can replace hello version number with "latest", which selects hello latest version of hello distribution.</span></span>

<span data-ttu-id="d7164-117">마켓플레이스 이미지 toospecify 일반적으로 사용 hello 이미지 *URN*합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-117">toospecify a Marketplace image, you typically use hello image *URN*.</span></span> <span data-ttu-id="d7164-118">hello 콜론 (:) 문자로 구분 된 이러한 값을 결합 하는 hello URN: *게시자*:*제공*:*Sku*:*버전*합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-118">hello URN combines these values, separated by hello colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="d7164-119">인기 있는 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="d7164-119">List popular images</span></span>

<span data-ttu-id="d7164-120">Hello 실행 [az vm 이미지 목록을](/cli/azure/vm/image#list) hello 없이 명령을 `--all` 옵션, toosee hello Azure 마켓플레이스 이미지 인기 있는 VM의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-120">Run hello [az vm image list](/cli/azure/vm/image#list) command, without hello `--all` option, toosee a list of popular VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="d7164-121">예를 들어 실행 hello 명령 toodisplay 다음 캐시 된 인기 있는 이미지 목록을 표 형태로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-121">For example, run hello following command toodisplay a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="d7164-122">hello 출력 hello URN을 포함 (hello에 대 한 값을 hello *Urn* 열)과 toospecify hello 이미지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-122">hello output includes hello URN (hello value in hello *Urn* column), which you use toospecify hello image.</span></span> <span data-ttu-id="d7164-123">이러한 인기 있는 마켓플레이스 이미지 중 하나가 지정 된 VM을 만들 때 지정할 수 있습니다 hello URN 별칭 같은 *UbuntuLTS*합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify hello URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a><span data-ttu-id="d7164-124">특정 이미지 찾기</span><span class="sxs-lookup"><span data-stu-id="d7164-124">Find specific images</span></span>

<span data-ttu-id="d7164-125">toofind hello Marketplace에서에서 특정 VM 이미지를 사용 하 여 hello `az vm image list` hello로 명령을 `--all` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-125">toofind a specific VM image in hello Marketplace, use hello `az vm image list` command with hello `--all` option.</span></span> <span data-ttu-id="d7164-126">이 버전의 hello 명령 일부 시간 toocomplete 걸리고 긴 출력을 반환할 수 있으므로 하면 일반적으로 hello 목록 필터 기준 `--publisher` 또는 다른 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-126">This version of hello command takes some time toocomplete and can return lengthy output, so you usually filter hello list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="d7164-127">예를 들어 다음 명령을 hello 표시 모든 Debian 제안 (hello 없이 사항에 유의 `--all` 스위치와 공용 이미지의 로컬 캐시 hello 데이터만 검색):</span><span class="sxs-lookup"><span data-stu-id="d7164-127">For example, hello following command displays all Debian offers (remember that without hello `--all` switch, it only searches hello local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="d7164-128">부분 출력:</span><span class="sxs-lookup"><span data-stu-id="d7164-128">Partial output:</span></span> 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

<span data-ttu-id="d7164-129">Hello 사용 하 여 비슷한 필터 적용 `--location`, `--publisher`, 및 `--sku` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-129">Apply similar filters with hello `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="d7164-130">에 대 한 검색 하는 등의 필터에서 부분적으로 일치도 수행할 수 있습니다 `--offer Deb` toofind 모든 Debian 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` toofind all Debian images.</span></span>

<span data-ttu-id="d7164-131">Hello로 특정 위치를 지정 하지 않으면 `--location` 옵션에 대 한 hello 값 `westus` 기본적으로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-131">If you don't specify a particular location with hello `--location` option, hello values for `westus` are returned by default.</span></span> <span data-ttu-id="d7164-132">(`az configure --defaults location=<location>`을 실행하여 다른 기본 위치를 설정합니다.)</span><span class="sxs-lookup"><span data-stu-id="d7164-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="d7164-133">다음 명령을 hello에서 모든 Debian 8 Sku를 나열 하는 예를 들어 `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="d7164-133">For example, hello following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="d7164-134">부분 출력:</span><span class="sxs-lookup"><span data-stu-id="d7164-134">Partial output:</span></span>

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-hello-images"></a><span data-ttu-id="d7164-135">Hello 이미지를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-135">Navigate hello images</span></span> 
<span data-ttu-id="d7164-136">또 다른 방법은 toofind 위치에 이미지는 toorun hello [az vm 이미지 목록을 게시자](/cli/azure/vm/image#list-publishers), [az vm 이미지 목록을 제공](/cli/azure/vm/image#list-offers), 및 [az vm 이미지 목록을 sku](/cli/azure/vm/image#list-skus) 순서로 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-136">Another way toofind an image in a location is toorun hello [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="d7164-137">이러한 명령을 사용하여 값을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="d7164-138">Hello 이미지 게시자 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-138">List hello image publishers.</span></span>
2. <span data-ttu-id="d7164-139">지정된 게시자에 제안을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="d7164-140">지정된 제안에 SKU를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="d7164-141">예를 들어 hello 다음 명령은 나열 hello West US 위치의에서 hello 이미지 게시자.</span><span class="sxs-lookup"><span data-stu-id="d7164-141">For example, hello following command lists hello image publishers in hello West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="d7164-142">부분 출력:</span><span class="sxs-lookup"><span data-stu-id="d7164-142">Partial output:</span></span>

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
<span data-ttu-id="d7164-143">이 정보 toofind 특정 게시자에서 제공 하는 데 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-143">Use this information toofind offers from a specific publisher.</span></span> <span data-ttu-id="d7164-144">예를 들어 Canonical가 hello West US 위치에서에서 이미지 게시자를 찾을 해당 서비스를 실행 하 여 `azure vm image list-offers`합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-144">For example, if Canonical is an image publisher in hello West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="d7164-145">Hello 위치와 hello 다음 예제와 같이 hello 게시자를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-145">Pass hello location and hello publisher as in hello following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="d7164-146">출력:</span><span class="sxs-lookup"><span data-stu-id="d7164-146">Output:</span></span>

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
<span data-ttu-id="d7164-147">미국 서 부 지역 hello에 Canonical 게시 hello 참조 **UbuntuServer** Azure에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-147">You see that in hello West US region, Canonical publishes hello **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="d7164-148">하지만 어떤 Sku? 이러한 값을 실행 하는 tooget `azure vm image list-skus` hello 위치, 게시자 및 검색 한 제안 설정:</span><span class="sxs-lookup"><span data-stu-id="d7164-148">But what SKUs? tooget those values, run `azure vm image list-skus` and set hello location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="d7164-149">출력:</span><span class="sxs-lookup"><span data-stu-id="d7164-149">Output:</span></span>

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

<span data-ttu-id="d7164-150">마지막으로 hello를 사용 하 여 `az vm image list` 명령 toofind hello 예를 들어 원하는 SKU의 특정 버전 **16.04 LTS**:</span><span class="sxs-lookup"><span data-stu-id="d7164-150">Finally, use hello `az vm image list` command toofind a specific version of hello SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="d7164-151">출력:</span><span class="sxs-lookup"><span data-stu-id="d7164-151">Output:</span></span>

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a><span data-ttu-id="d7164-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7164-152">Next steps</span></span>
<span data-ttu-id="d7164-153">이제 hello 이미지 정확 하 게 선택할 수 있습니다 toouse 하 여 원하는 hello URN 값을 기록 라인으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-153">Now you can choose precisely hello image you want toouse by taking note of hello URN value.</span></span> <span data-ttu-id="d7164-154">Hello로이 값을 전달 `--image` hello로 VM을 만들 때 매개 변수 [az vm 만들기](/cli/azure/vm#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-154">Pass this value with hello `--image` parameter when you create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="d7164-155">"최신"으로 hello URN에서에서 hello 버전 번호를 바꿀 필요에 따라 수를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-155">Remember that you can optionally replace hello version number in hello URN with "latest".</span></span> <span data-ttu-id="d7164-156">이 버전은 항상 hello hello 분포의 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-156">This version is always hello latest version of hello distribution.</span></span> <span data-ttu-id="d7164-157">hello URN 정보를 사용 하 여 신속 하 게 가상 컴퓨터 toocreate 참조 [만들기 및 Azure CLI hello로 Linux Vm 관리](tutorial-manage-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7164-157">toocreate a virtual machine quickly by using hello URN information, see [Create and Manage Linux VMs with hello Azure CLI](tutorial-manage-vm.md).</span></span>
