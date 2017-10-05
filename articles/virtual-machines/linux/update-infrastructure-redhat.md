---
title: RHUI(Red Hat Update Infrastructure) | Microsoft Docs
description: "Microsoft Azure의 주문형 Red Hat Enterprise Linux 인스턴스에 대한 RHUI(Red Hat Update Infrastructure)에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: 07815d691ffe57f0349f7a90ced4a2fcc1ab834f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="a919f-103">Azure의 주문형 Red Hat Enterprise Linux Vm에 대한 RHUI(Red Hat Update Infrastructure)</span><span class="sxs-lookup"><span data-stu-id="a919f-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="a919f-104">Azure 마켓플레이스에서 사용할 수 있는 RHEL(주문형 Red Hat Enterprise Linux)이미지에서 만든 가상 컴퓨터는 Azure에 배포된 RHUI(Red Hat Update Infrastructure)에 액세스하도록 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-104">Virtual machines created from the on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered to access the Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="a919f-105">주문형 RHEL 인스턴스는 국가별 yum 리포지토리에 액세스하며 증분 업데이트를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-105">The on-demand RHEL instances have access to a regional yum repository and able to receive incremental updates.</span></span>

<span data-ttu-id="a919f-106">RHUI에서 관리되는 yum 리포지토리 목록은 프로비전 중 RHEL 인스턴스에 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-106">The yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="a919f-107">따라서 추가 구성을 할 필요가 없습니다. RHEL 인스턴스가 최신 업데이트를 적용할 준비가 되면 `yum update`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-107">You don't need to do any additional configuration - run `yum update` after your RHEL instance is ready to get the latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="a919f-108">2016년 9월에 업데이트된 Azure RHUI를 배포했고 2017년 1월에 이전 Azure RHUI를 단계적으로 종료하기 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of the older Azure RHUI.</span></span> <span data-ttu-id="a919f-109">2016년 9월 이후부터 RHEL 이미지(또는 해당 스냅숏)을 사용하고 있었다면 조치가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-109">If you have been using the RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="a919f-110">그러나 오래된 스냅숏/VM을 있다면 Azure RHUI에 중단 없이 액세스하기 위해 해당 구성을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-110">If, however, you have older snapshots/VMs, their configuration needs to be updated for uninterrupted access to the Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="a919f-111">RHUI Azure 인프라 업데이트</span><span class="sxs-lookup"><span data-stu-id="a919f-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="a919f-112">2016년 9월을 기준으로 Azure는 새로운 RHUI(Red Hat 업데이트 인프라) 서버 모음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="a919f-113">이러한 서버는 모든 VM에서 하위 지역에 관계없이 단일 끝점(rhui-1.micrsoft.com)을 사용할 수 있도록 [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/)를 통해 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="a919f-114">Azure Marketplace에서 새로운 RHEL PAYG(종량제) 이미지(버전 날짜 2016년 9월 이상)는 새 Azure RHUI 서버를 가리키며 추가 작업이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-114">The new RHEL Pay-As-You-Go (PAYG) images in the Azure Marketplace (versions dated September 2016 or later) point to the new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="a919f-115">작업이 필요한지 확인</span><span class="sxs-lookup"><span data-stu-id="a919f-115">Determine if action is required</span></span>
<span data-ttu-id="a919f-116">RHEL PAYG Azure VM에서 Azure RHUI에 연결할 때 문제가 발생하는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-116">If you are experiencing problems connecting to Azure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="a919f-117">Azure RHUI 끝점에 대한 VM 구성 검사</span><span class="sxs-lookup"><span data-stu-id="a919f-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="a919f-118">`/etc/yum.repos.d/rh-cloud.repo` 파일이 해당 파일에 있는 `[rhui-microsoft-azure-rhel*]` 섹션의 baseurl에서 `rhui-[1-3].microsoft.com`에 대한 참조를 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference to `rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of the file.</span></span> <span data-ttu-id="a919f-119">그렇다면 새 Azure RHUI를 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-119">If it is - you are using the new Azure RHUI.</span></span>

    <span data-ttu-id="a919f-120">다음 `mirrorlist.*cds[1-4].cloudapp.net` 패턴으로 위치를 가리키는 경우 구성 업데이트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-120">If it pointing to a location with the following pattern `mirrorlist.*cds[1-4].cloudapp.net` - the configuration update is required.</span></span>

    <span data-ttu-id="a919f-121">새 구성을 사용하고 Azure RHUI에 연결할 수 없으면 Microsoft 또는 Red Hat을 사용하여 지원 사례를 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-121">If you are using the new configuration and still cannot connect to Azure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a919f-122">Azure 호스티드 RHUI에 대한 액세스는 [Microsoft Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)내의 Vm에 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-122">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="a919f-123">이 검사를 수행하고 구성을 자동으로 업데이트할 때 이전 Azure RHUI 여전히 사용할 수 있는 경우 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-123">If the old Azure RHUI is still available when you do this check and you would like to automatically update the configuration, execute the following command:</span></span>

    <span data-ttu-id="a919f-124">RHEL 제품군 버전에 따라 `sudo yum update RHEL6` 또는 `sudo yum update RHEL7`입니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on the RHEL family version.</span></span>

3. <span data-ttu-id="a919f-125">이전 Azure RHUI에 더 이상 연결할 수 없는 경우 다음 섹션에서 설명한 수동 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-125">If you can no longer connect to the old Azure RHUI, follow the manual steps described in the next section.</span></span>

4. <span data-ttu-id="a919f-126">영향을 받는 VM이 프로비전되는 원본 이미지/스냅숏에서 구성을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-126">Make sure to update the configuration on the source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-the-old-azure-rhui"></a><span data-ttu-id="a919f-127">이전 Azure RHUI의 단계적인 종료</span><span class="sxs-lookup"><span data-stu-id="a919f-127">Phased shutdown of the old Azure RHUI</span></span>
<span data-ttu-id="a919f-128">이전 Azure RHUI를 종료하는 동안에는 다음과 같이 액세스를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-128">During the shutdown of the old Azure RHUI we restrict access to it as follows:</span></span>

1. <span data-ttu-id="a919f-129">이미 연결 중인 일련의 IP 주소에 추가 액세스(ACL)를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-129">Further restrict access (ACL) to set of IP addresses that are already connecting to it.</span></span> <span data-ttu-id="a919f-130">가능한 부작용: 이전 Azure RHUI를 계속해서 사용하는 경우 새 VM에 연결하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-130">Possible side-effects: if you continue using the old Azure RHUI - your new VMs may not be able to connect to it.</span></span> <span data-ttu-id="a919f-131">종료/할당 취소/시작 시퀀스를 수행하는 동적 IP를 가진 RHEL VM은 새 IP를 수신할 수 있으므로 이전 Azure RHUI에 연결하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing to connect to the old Azure RHUI</span></span>

2. <span data-ttu-id="a919f-132">미러 콘텐츠 배달 서버 종료</span><span class="sxs-lookup"><span data-stu-id="a919f-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="a919f-133">가능한 부작용: 추가 CDSes를 종료했기 때문에 `yum update` 서비스 시간이 길어진 만큼 이전 Azure RHUI에 연결할 수 없을 지점까지의 제한 시간이 길어집니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until the point when you can no longer connect to the old Azure RHUI.</span></span>

### <a name="the-ips-for-the-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="a919f-134">새 RHUI 콘텐츠 배달 서버에 대한 IP</span><span class="sxs-lookup"><span data-stu-id="a919f-134">The IPs for the new RHUI content delivery servers are</span></span>
<span data-ttu-id="a919f-135">네트워크 구성을 사용하여 RHEL PAYG VM에서 추가 액세스를 제한하려는 경우 사용자의 환경에 따라 작동하도록 다음 IP를 `yum update`에 대해 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-135">If you are using network configuration to further restrict access from RHEL PAYG VMs, make sure the following IPs are allowed for `yum update` to work depending on the environment you are in.</span></span> 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-to-use-the-new-azure-rhui-servers"></a><span data-ttu-id="a919f-136">새 Azure RHUI 서버를 사용하기 위한 수동 업데이트 절차</span><span class="sxs-lookup"><span data-stu-id="a919f-136">Manual update procedure to use the new Azure RHUI servers</span></span>
<span data-ttu-id="a919f-137">공개 키 서명 다운로드(curl을 통해)</span><span class="sxs-lookup"><span data-stu-id="a919f-137">Download (via curl) the public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="a919f-138">다운로드한 키 확인</span><span class="sxs-lookup"><span data-stu-id="a919f-138">Verify the downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="a919f-139">출력을 확인하고 `keyid` 및 `user ID packet` 확인</span><span class="sxs-lookup"><span data-stu-id="a919f-139">Check the output, verify `keyid` and `user ID packet`:</span></span>

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

<span data-ttu-id="a919f-140">공개 키 설치</span><span class="sxs-lookup"><span data-stu-id="a919f-140">Install the public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="a919f-141">클라이언트 RPM 다운로드, 확인 및 설치</span><span class="sxs-lookup"><span data-stu-id="a919f-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="a919f-142">다운로드: RHEL 6의 경우</span><span class="sxs-lookup"><span data-stu-id="a919f-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="a919f-143">RHEL 7의 경우</span><span class="sxs-lookup"><span data-stu-id="a919f-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="a919f-144">다음 확인</span><span class="sxs-lookup"><span data-stu-id="a919f-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="a919f-145">출력에서 패키지 서명이 정상인지 확인</span><span class="sxs-lookup"><span data-stu-id="a919f-145">Check in output that signature of the package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="a919f-146">RPM 설치</span><span class="sxs-lookup"><span data-stu-id="a919f-146">Install the RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="a919f-147">완료되면 VM에서 Azure RHUI에 액세스할 수 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="a919f-147">Upon completion, verify that you can access Azure RHUI form the VM</span></span>

### <a name="all-in-one-script-for-automating-the-preceding-task"></a><span data-ttu-id="a919f-148">이전 태스크를 자동화하는 일체형 스크립트</span><span class="sxs-lookup"><span data-stu-id="a919f-148">All-in-one script for automating the preceding task</span></span>
<span data-ttu-id="a919f-149">영향을 받는 VM을 새 Azure RHUI 서버에 업데이트하는 작업을 자동화하기 위해 필요에 따라 다음 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-149">Use the following script as needed to automate the task of updating affected VMs to the new Azure RHUI servers.</span></span>

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a><span data-ttu-id="a919f-150">RHUI 개요</span><span class="sxs-lookup"><span data-stu-id="a919f-150">RHUI overview</span></span>
<span data-ttu-id="a919f-151">[Red Hat 업데이트 인프라](https://access.redhat.com/products/red-hat-update-infrastructure)는 Red Hat 인증 클라우드 공급자가 호스트하는 Red Hat Enterprise Linux 클라우드 인스턴스의 yum 리포지토리 콘텐츠를 관리할 수 있는 확장성이 뛰어난 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution to manage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="a919f-152">업스트림 Pulp 프로젝트를 기반으로, RHUI는 클라우드 공급자가 Red Hat 호스트되는 리포지토리 콘텐츠를 로컬로 미러링하고, 고유한 콘텐츠로 사용자 지정 리포지토리를 만들고, 부하 분산된 콘텐츠 배달 시스템을 통해 이러한 리포지토리를 대규모 최종 사용자 그룹에 제공하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-152">Based on the upstream Pulp project, RHUI allows cloud providers to locally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available to a large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="a919f-153">RHUI 사용 가능한 지역</span><span class="sxs-lookup"><span data-stu-id="a919f-153">Regions where RHUI is available</span></span>
<span data-ttu-id="a919f-154">RHUI는 RHEL 주문형 이미지를 사용할 수 있는 모든 지역에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="a919f-155">RHUI는 현재 [Azure 상태 대시보드](https://azure.microsoft.com/status/) 페이지, Azure 미국 정부 및 Azure 독일 지역에 나열된 모든 공용 지역을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-155">It currently includes all public regions listed on the [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="a919f-156">RHEL 주문형 이미지에서 프로비전된 VM에 대한 RHUI 액세스 권한은 해당 가격에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="a919f-157">추가 지역/국가 클라우드 가용성은 향후 RHEL 주문형 가용성을 확장할 때 업데이트될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="a919f-158">Azure 호스티드 RHUI에 대한 액세스는 [Microsoft Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)내의 Vm에 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-158">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="a919f-159">다른 업데이트 리파지토리에서 업데이트 받기</span><span class="sxs-lookup"><span data-stu-id="a919f-159">Get updates from another update repository</span></span>
<span data-ttu-id="a919f-160">Azure 호스티드 RHUI가 아닌 다른 업데이트 리포지토리에서 업데이트를 가져와야 하는 경우 먼저 RHUI에서 인스턴스의 등록을 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-160">If you need to get updates from a different update repository (instead of Azure-hosted RHUI), first you need to unregister your instances from RHUI.</span></span> <span data-ttu-id="a919f-161">그런 다음 원하는 업데이트 인프라(예: Red Hat 위성 또는 Red Hat 고객 포털 CDN)에 다시 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-161">Then you need to re-register them with the desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="a919f-162">이러한 서비스에 대한 적합한 Red Hat 구독 및 [Azure에서 Red Hat 클라우드 액세스](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure)에 대한 등록이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="a919f-163">RHUI 등록을 취소하고 업데이트 인프라에 재등록하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-163">To unregister RHUI and reregister to your update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="a919f-164">/etc/yum.repos.d/rh-cloud.repo를 편집하고 모든 `enabled=1`을 `enabled=0`으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` to `enabled=0`.</span></span> <span data-ttu-id="a919f-165">예:</span><span class="sxs-lookup"><span data-stu-id="a919f-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="a919f-166">/etc/yum/pluginconf.d/rhnplugin.conf를 편집하고 `enabled=0`을 `enabled=1`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` to `enabled=1`.</span></span>
3. <span data-ttu-id="a919f-167">그런 다음 Red Hat 고객 포털과 같은 원하는 인프라에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-167">Then register with the desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="a919f-168">[시스템을 Red Hat 고객 포털에 등록 및 구독하는 방법](https://access.redhat.com/solutions/253273)에 나오는 Red Hat 솔루션 가이드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-168">Follow Red Hat solution guide on [how to register and subscribe a system to the Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="a919f-169">Azure 호스티드 RHUI에 대한 액세스는 RHEL 종량제(PAYG) 이미지 가격에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-169">Access to the Azure-hosted RHUI is included in the RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="a919f-170">Azure 호스티드 RHUI에서 PAYG RHEL VM의 등록을 취소하더라도 가상 컴퓨터를 사용자 라이선스 필요(BYOL) 형식 VM으로 변환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-170">Unregistering a PAYG RHEL VM from the Azure-hosted RHUI does not convert the virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="a919f-171">업데이트의 다른 원본에 동일한 VM을 등록하는 경우 Azure RHEL 소프트웨어 요금에 한 번, Red Hat 구독에 대한 한 번 등 두 배의 요금이 부과될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-171">If you register the same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and the second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="a919f-172">Azure 호스티드 RHUI 이외의 업데이트 인프라를 지속적으로 사용해야 한다면 [Azure용 Red Hat 기반 가상 컴퓨터 만들기 및 업데이트](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 문서에서 설명된 대로 사용자 고유의 (BYOL 유형) 이미지를 만들어 배포하는 것을 고려해 보도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-172">If you consistently need to use an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="a919f-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a919f-173">Next steps</span></span>
<span data-ttu-id="a919f-174">Azure Marketplace 종량제 이미지에서 Red Hat Enterprise Linux VM을 만들고 Azure 호스티드 RHUI를 활용하려면 [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/)로 갑니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-174">To create a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="a919f-175">아무런 추가 설치도 없이 RHEL 인스턴스에서 `yum update`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a919f-175">You will be able to use `yum update` in your RHEL instance without any additional setup.</span></span>

