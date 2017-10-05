---
title: "Azure CLI를 사용하여 Linux VM 이미지 선택 | Microsoft Docs"
description: "Azure CLI를 사용하여 Marketplace VM 이미지의 게시자, 제품, SKU 및 버전을 확인하는 방법을 알아봅니다."
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
ms.openlocfilehash: e0c27a7ee9e9a7ab1a3b004e070fa556b56a36a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-find-linux-vm-images-in-the-azure-marketplace-with-the-azure-cli"></a><span data-ttu-id="8bf96-103">Azure CLI를 사용하여 Azure Marketplace에서 Linux VM 이미지를 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="8bf96-103">How to find Linux VM images in the Azure Marketplace with the Azure CLI</span></span>
<span data-ttu-id="8bf96-104">이 항목에서는 Azure CLI 2.0을 사용하여 Azure Marketplace에서 VM 이미지를 찾는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-104">This topic describes how to use the Azure CLI 2.0 to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="8bf96-105">이 정보를 사용하여 Linux VM을 만들 때 Marketplace 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-105">Use this information to specify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="8bf96-106">최신 Azure CLI 2.0을 [설치](/cli/azure/install-az-cli2)하고 Azure 계정(`az login`)에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-106">Make sure that you installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in to an Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="8bf96-107">용어</span><span class="sxs-lookup"><span data-stu-id="8bf96-107">Terminology</span></span>

<span data-ttu-id="8bf96-108">Marketplace 이미지는 CLI 및 다른 Azure 도구에서 계층 구조에 따라 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-108">Marketplace images are identified in the CLI and other Azure tools according to a hierarchy:</span></span>

* <span data-ttu-id="8bf96-109">**Publisher** - 이미지를 만든 조직입니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-109">**Publisher** - The organization that created the image.</span></span> <span data-ttu-id="8bf96-110">예제: Canonical</span><span class="sxs-lookup"><span data-stu-id="8bf96-110">Example: Canonical</span></span>
* <span data-ttu-id="8bf96-111">**Offer** - 게시자에 의해 생성 되는 관련 이미지 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="8bf96-112">예제: Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="8bf96-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="8bf96-113">**SKU** - 제공의 인스턴스(예: 배포의 주 릴리스)입니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="8bf96-114">예제: 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="8bf96-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="8bf96-115">**Version** - 이미지 SKU의 버전 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-115">**Version** - The version number of an image SKU.</span></span> <span data-ttu-id="8bf96-116">이미지를 지정하면 버전 번호를 “최신”으로 바꿀 수 있습니다. 그러면 배포의 최신 버전이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-116">When specifying the image, you can replace the version number with "latest", which selects the latest version of the distribution.</span></span>

<span data-ttu-id="8bf96-117">Marketplace 이미지를 지정하려면 일반적으로 이미지 *URN*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-117">To specify a Marketplace image, you typically use the image *URN*.</span></span> <span data-ttu-id="8bf96-118">URN은 다음 값을 콜론(:) 문자로 구분해서 조합합니다. *Publisher*:*Offer*:*Sku*:*Version*</span><span class="sxs-lookup"><span data-stu-id="8bf96-118">The URN combines these values, separated by the colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="8bf96-119">인기 있는 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="8bf96-119">List popular images</span></span>

<span data-ttu-id="8bf96-120">`--all` 옵션을 사용하지 않고 [az vm image list](/cli/azure/vm/image#list) 명령을 실행하여 Azure Marketplace에서 인기있는 VM 이미지의 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-120">Run the [az vm image list](/cli/azure/vm/image#list) command, without the `--all` option, to see a list of popular VM images in the Azure Marketplace.</span></span> <span data-ttu-id="8bf96-121">예를 들어, 다음 명령을 실행하여 테이블 형식으로 캐시된 인기있는 이미지 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-121">For example, run the following command to display a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="8bf96-122">출력에는 이미지를 지정하는 데 사용할 수 있는 URN(*Urn* 열의 값)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-122">The output includes the URN (the value in the *Urn* column), which you use to specify the image.</span></span> <span data-ttu-id="8bf96-123">또한 인기있는 마켓플레이스 이미지 중 하나를 사용하여 VM을 만드는 경우 *UbuntuLTS*와 같은 URN 별칭을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify the URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
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

## <a name="find-specific-images"></a><span data-ttu-id="8bf96-124">특정 이미지 찾기</span><span class="sxs-lookup"><span data-stu-id="8bf96-124">Find specific images</span></span>

<span data-ttu-id="8bf96-125">Marketplace에서 특정 VM 이미지를 찾으려면 `az vm image list` 명령에 `--all` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-125">To find a specific VM image in the Marketplace, use the `az vm image list` command with the `--all` option.</span></span> <span data-ttu-id="8bf96-126">명령의 이 버전은 완료하는 데 다소 시간이 걸리며 긴 출력을 생성할 수 있으므로 일반적으로 `--publisher` 또는 다른 매개 변수를 기준으로 목록을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-126">This version of the command takes some time to complete and can return lengthy output, so you usually filter the list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="8bf96-127">예를 들어, 다음 명령은 모든 Debian 제품을 표시합니다(`--all` 스위치 없이는 공용 이미지의 로컬 캐시만을 검색함).</span><span class="sxs-lookup"><span data-stu-id="8bf96-127">For example, the following command displays all Debian offers (remember that without the `--all` switch, it only searches the local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="8bf96-128">부분 출력:</span><span class="sxs-lookup"><span data-stu-id="8bf96-128">Partial output:</span></span> 
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

<span data-ttu-id="8bf96-129">`--location`, `--publisher` 및 `--sku` 옵션을 사용하여 비슷한 필터를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-129">Apply similar filters with the `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="8bf96-130">모든 Debian 이미지를 찾는 `--offer Deb`을 검색하는 등 필터에서 부분적 일치도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` to find all Debian images.</span></span>

<span data-ttu-id="8bf96-131">`--location` 옵션을 사용하여 특정 위치를 지정하지 않는 경우 기본적으로 `westus`에 대한 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-131">If you don't specify a particular location with the `--location` option, the values for `westus` are returned by default.</span></span> <span data-ttu-id="8bf96-132">(`az configure --defaults location=<location>`을 실행하여 다른 기본 위치를 설정합니다.)</span><span class="sxs-lookup"><span data-stu-id="8bf96-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="8bf96-133">예를 들어 다음 명령은 `westeurope`에 있는 모든 Debian 8개의 SKU를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-133">For example, the following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="8bf96-134">부분 출력:</span><span class="sxs-lookup"><span data-stu-id="8bf96-134">Partial output:</span></span>

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

## <a name="navigate-the-images"></a><span data-ttu-id="8bf96-135">이미지 이동</span><span class="sxs-lookup"><span data-stu-id="8bf96-135">Navigate the images</span></span> 
<span data-ttu-id="8bf96-136">위치에서 이미지를 찾는 또 다른 방법은 [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers) 및 [az vm image list-skus](/cli/azure/vm/image#list-skus)의 순서로 명령을 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-136">Another way to find an image in a location is to run the [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="8bf96-137">이러한 명령을 사용하여 값을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="8bf96-138">이미지 게시자를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-138">List the image publishers.</span></span>
2. <span data-ttu-id="8bf96-139">지정된 게시자에 제안을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="8bf96-140">지정된 제안에 SKU를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="8bf96-141">예를 들어 다음 명령은 미국 서부에 있는 이미지 게시자를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-141">For example, the following command lists the image publishers in the West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="8bf96-142">부분 출력:</span><span class="sxs-lookup"><span data-stu-id="8bf96-142">Partial output:</span></span>

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
<span data-ttu-id="8bf96-143">이 정보를 사용하여 특정 게시자의 제안을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-143">Use this information to find offers from a specific publisher.</span></span> <span data-ttu-id="8bf96-144">예를 들어 Canonical이 미국 서부에 있는 이미지 게시자인 경우 `azure vm image list-offers`을 실행하여 해당 제품을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-144">For example, if Canonical is an image publisher in the West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="8bf96-145">다음 예제와 같이 위치 및 게시자를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-145">Pass the location and the publisher as in the following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="8bf96-146">출력:</span><span class="sxs-lookup"><span data-stu-id="8bf96-146">Output:</span></span>

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
<span data-ttu-id="8bf96-147">미국 서부 지역에서 Canonical이 Azure에 **UbuntuServer** 제품을 게시한다는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-147">You see that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="8bf96-148">하지만 SKU는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="8bf96-148">But what SKUs?</span></span> <span data-ttu-id="8bf96-149">이런 값을 가져오려면 `azure vm image list-skus`을 실행하고 검색한 위치, 게시자 및 제품을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-149">To get those values, run `azure vm image list-skus` and set the location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="8bf96-150">출력:</span><span class="sxs-lookup"><span data-stu-id="8bf96-150">Output:</span></span>

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

<span data-ttu-id="8bf96-151">마지막으로 `az vm image list` 명령을 사용하여 원하는 SKU의 특정 버전을 찾습니다(예: **16.04-LTS**).</span><span class="sxs-lookup"><span data-stu-id="8bf96-151">Finally, use the `az vm image list` command to find a specific version of the SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="8bf96-152">출력:</span><span class="sxs-lookup"><span data-stu-id="8bf96-152">Output:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="8bf96-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8bf96-153">Next steps</span></span>
<span data-ttu-id="8bf96-154">이제 URN 값을 기록하여 사용할 이미지를 정밀하게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-154">Now you can choose precisely the image you want to use by taking note of the URN value.</span></span> <span data-ttu-id="8bf96-155">[az vm create](/cli/azure/vm#create) 명령을 사용하여 VM을 만들 때 이 값을 `--image` 매개 변수와 함께 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-155">Pass this value with the `--image` parameter when you create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="8bf96-156">필요에 따라 "최신"을 사용하여 URN에서 버전 번호를 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-156">Remember that you can optionally replace the version number in the URN with "latest".</span></span> <span data-ttu-id="8bf96-157">이 버전은 항상 최신 버전의 배포입니다.</span><span class="sxs-lookup"><span data-stu-id="8bf96-157">This version is always the latest version of the distribution.</span></span> <span data-ttu-id="8bf96-158">URN 정보를 사용하여 가상 컴퓨터를 빠르게 만들려면 [Azure CLI로 Linux VM 만들기 및 관리](tutorial-manage-vm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8bf96-158">To create a virtual machine quickly by using the URN information, see [Create and Manage Linux VMs with the Azure CLI](tutorial-manage-vm.md).</span></span>
