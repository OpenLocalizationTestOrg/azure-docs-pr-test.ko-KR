---
title: "aaaRed Hat 업데이트 인프라 (RHUI) | Microsoft Docs"
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
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="898e1-103">Azure의 주문형 Red Hat Enterprise Linux Vm에 대한 RHUI(Red Hat Update Infrastructure)</span><span class="sxs-lookup"><span data-stu-id="898e1-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="898e1-104">Hello 주문형 Red Hat Enterprise Linux (RHEL) 이미지에서 사용할 수 있는 Azure Marketplace에서 만든 가상 컴퓨터는 등록 된 tooaccess hello Red Hat 업데이트 인프라 (RHUI)이 Azure에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-104">Virtual machines created from hello on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered tooaccess hello Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="898e1-105">hello 주문형 RHEL 인스턴스 액세스 tooa 국가별 yum 리포지토리와 수 tooreceive 증분 업데이트를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-105">hello on-demand RHEL instances have access tooa regional yum repository and able tooreceive incremental updates.</span></span>

<span data-ttu-id="898e1-106">RHUI 하 여 관리 되는 hello yum 리포지토리 목록 RHEL 인스턴스 프로 비전 하는 동안 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-106">hello yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="898e1-107">Toodo 실행-추가 구성 필요 하지 않습니다 `yum update` RHEL 인스턴스 준비 tooget hello에 대 한 최신 업데이트 된 후입니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-107">You don't need toodo any additional configuration - run `yum update` after your RHEL instance is ready tooget hello latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="898e1-108">2016 년 9 월 업데이트는 Azure RHUI 배포 및 hello의 단계적된 종료를 시작 했습니다. 2017 년 1 월에에서 Azure RHUI 이전 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of hello older Azure RHUI.</span></span> <span data-ttu-id="898e1-109">사용 된 hello RHEL 이미지 (또는 해당 스냅숏) 2016 년 9 월에서에서 이상-가능성이 경우 동작은 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-109">If you have been using hello RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="898e1-110">그러나 오래 된 스냅숏을/Vm 있다면, 해당 구성을 toobe 중단 없이 액세스할 toohello Azure RHUI에 대해 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-110">If, however, you have older snapshots/VMs, their configuration needs toobe updated for uninterrupted access toohello Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="898e1-111">RHUI Azure 인프라 업데이트</span><span class="sxs-lookup"><span data-stu-id="898e1-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="898e1-112">2016년 9월을 기준으로 Azure는 새로운 RHUI(Red Hat 업데이트 인프라) 서버 모음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="898e1-113">이러한 서버는 모든 VM에서 하위 지역에 관계없이 단일 끝점(rhui-1.micrsoft.com)을 사용할 수 있도록 [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/)를 통해 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="898e1-114">hello Azure 마켓플레이스 (2016 년 9 월 이상 버전) 지점 toohello 새 Azure RHUI 서버에서 새 RHEL 종 량 제 (PAYG) 이미지 hello 하 고 추가 조치는 필요 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="898e1-114">hello new RHEL Pay-As-You-Go (PAYG) images in hello Azure Marketplace (versions dated September 2016 or later) point toohello new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="898e1-115">작업이 필요한지 확인</span><span class="sxs-lookup"><span data-stu-id="898e1-115">Determine if action is required</span></span>
<span data-ttu-id="898e1-116">TooAzure RHUI RHEL PAYG Azure VM에서 연결할 때 문제가 발생 하는 경우 다음이 단계를 수행</span><span class="sxs-lookup"><span data-stu-id="898e1-116">If you are experiencing problems connecting tooAzure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="898e1-117">Azure RHUI 끝점에 대한 VM 구성 검사</span><span class="sxs-lookup"><span data-stu-id="898e1-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="898e1-118">확인 `/etc/yum.repos.d/rh-cloud.repo` 파일 참조가 너무`rhui-[1-3].microsoft.com` 의 baseurl에 `[rhui-microsoft-azure-rhel*]` hello 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference too`rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of hello file.</span></span> <span data-ttu-id="898e1-119">사용 하는 경우 새 Azure RHUI hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-119">If it is - you are using hello new Azure RHUI.</span></span>

    <span data-ttu-id="898e1-120">하는 경우 패턴을 따르는 hello로 tooa 위치를 가리키는 `mirrorlist.*cds[1-4].cloudapp.net` -hello 구성 업데이트 작업이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-120">If it pointing tooa location with hello following pattern `mirrorlist.*cds[1-4].cloudapp.net` - hello configuration update is required.</span></span>

    <span data-ttu-id="898e1-121">Hello 새 구성을 사용 하는 경우 여전히 tooAzure RHUI-연결할 수 없는 Microsoft 소프트웨어 또는 Red Hat를 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-121">If you are using hello new configuration and still cannot connect tooAzure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="898e1-122">TooAzure 호스팅되지 RHUI 액세스는 제한 된 toohello Vm 내에서 [Microsoft Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-122">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="898e1-123">Hello 이전 Azure RHUI 여전히 사용할 수 있는 경우이 검사를 수행 하 고 원하는 tooautomatically hello 구성 업데이트를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-123">If hello old Azure RHUI is still available when you do this check and you would like tooautomatically update hello configuration, execute hello following command:</span></span>

    <span data-ttu-id="898e1-124">`sudo yum update RHEL6`또는 `sudo yum update RHEL7` hello RHEL 패밀리 버전에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on hello RHEL family version.</span></span>

3. <span data-ttu-id="898e1-125">Toohello 더 이상 연결할 수 있는 경우 이전 Azure RHUI, hello 수동 단계 수행 hello 다음 섹션에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-125">If you can no longer connect toohello old Azure RHUI, follow hello manual steps described in hello next section.</span></span>

4. <span data-ttu-id="898e1-126">VM을 영향을 받는 hello 원본 이미지/스냅숏 tooupdate hello 구성 되었는지 확인에서 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-126">Make sure tooupdate hello configuration on hello source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a><span data-ttu-id="898e1-127">단계적된 종료 hello 이전 Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="898e1-127">Phased shutdown of hello old Azure RHUI</span></span>
<span data-ttu-id="898e1-128">Hello의 hello 종료 하는 동안 tooit는 다음과 같이 액세스를 제한할 이전 Azure RHUI:</span><span class="sxs-lookup"><span data-stu-id="898e1-128">During hello shutdown of hello old Azure RHUI we restrict access tooit as follows:</span></span>

1. <span data-ttu-id="898e1-129">연결 하는 이미 tooit IP 주소의 액세스 (ACL) tooset을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-129">Further restrict access (ACL) tooset of IP addresses that are already connecting tooit.</span></span> <span data-ttu-id="898e1-130">가능한 부작용:를 사용 하 여 계속 진행 하면 기존 Azure RHUI hello-새 Vm 수 tooconnect tooit 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-130">Possible side-effects: if you continue using hello old Azure RHUI - your new VMs may not be able tooconnect tooit.</span></span> <span data-ttu-id="898e1-131">동적 Ip와 RHEL Vm 종료/할당 취소/시작 순서를 통해 이동 하는 새 IP를 받을 수 있습니다 및 따라서도 시작할 수 tooconnect toohello 실패 이전 Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="898e1-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing tooconnect toohello old Azure RHUI</span></span>

2. <span data-ttu-id="898e1-132">미러 콘텐츠 배달 서버 종료</span><span class="sxs-lookup"><span data-stu-id="898e1-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="898e1-133">가능한 부작용: 자세한 CDSes 종료으로 표시 될 수 없습니다 더 이상 `yum update` toohello를 연결할 수 없을 때 hello까지 더 많은 시간 제한을 지점 시간을 제공 하는 이전 Azure RHUI 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until hello point when you can no longer connect toohello old Azure RHUI.</span></span>

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="898e1-134">새 RHUI 콘텐츠 배달 서버 hello에 대 한 Ip hello는</span><span class="sxs-lookup"><span data-stu-id="898e1-134">hello IPs for hello new RHUI content delivery servers are</span></span>
<span data-ttu-id="898e1-135">네트워크 구성 toofurther를 사용 하는 경우 RHEL PAYG Vm에서 액세스를 제한, Ip 다음 hello에 사용할 수 있는지 확인 `yum update` 있는 hello 환경에 따라 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-135">If you are using network configuration toofurther restrict access from RHEL PAYG VMs, make sure hello following IPs are allowed for `yum update` toowork depending on hello environment you are in.</span></span> 

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

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a><span data-ttu-id="898e1-136">수동 업데이트 프로시저 toouse hello 새 Azure RHUI 서버</span><span class="sxs-lookup"><span data-stu-id="898e1-136">Manual update procedure toouse hello new Azure RHUI servers</span></span>
<span data-ttu-id="898e1-137">(Curl)를 통해 다운로드 hello 공개 키 서명</span><span class="sxs-lookup"><span data-stu-id="898e1-137">Download (via curl) hello public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="898e1-138">다운로드 한 hello 키 확인</span><span class="sxs-lookup"><span data-stu-id="898e1-138">Verify hello downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="898e1-139">Hello 출력을 확인, 확인 `keyid` 및 `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="898e1-139">Check hello output, verify `keyid` and `user ID packet`:</span></span>

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

<span data-ttu-id="898e1-140">Hello 공개 키를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-140">Install hello public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="898e1-141">클라이언트 RPM 다운로드, 확인 및 설치</span><span class="sxs-lookup"><span data-stu-id="898e1-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="898e1-142">다운로드: RHEL 6의 경우</span><span class="sxs-lookup"><span data-stu-id="898e1-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="898e1-143">RHEL 7의 경우</span><span class="sxs-lookup"><span data-stu-id="898e1-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="898e1-144">다음 확인</span><span class="sxs-lookup"><span data-stu-id="898e1-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="898e1-145">출력에 해당 서명을 확인 hello의 패키지는 확인</span><span class="sxs-lookup"><span data-stu-id="898e1-145">Check in output that signature of hello package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="898e1-146">Hello RPM을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-146">Install hello RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="898e1-147">완료 되 면 Azure RHUI 양식 hello VM에 액세스할 수 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="898e1-147">Upon completion, verify that you can access Azure RHUI form hello VM</span></span>

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a><span data-ttu-id="898e1-148">Hello 앞에 태스크를 자동화 하기 위한 내부에서 올인원 스크립트</span><span class="sxs-lookup"><span data-stu-id="898e1-148">All-in-one script for automating hello preceding task</span></span>
<span data-ttu-id="898e1-149">영향을 받는 Vm toohello 새 Azure RHUI 서버를 업데이트 하는 필요한 tooautomate hello 작업으로 스크립트를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-149">Use hello following script as needed tooautomate hello task of updating affected VMs toohello new Azure RHUI servers.</span></span>

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

## <a name="rhui-overview"></a><span data-ttu-id="898e1-150">RHUI 개요</span><span class="sxs-lookup"><span data-stu-id="898e1-150">RHUI overview</span></span>
<span data-ttu-id="898e1-151">[Red Hat 업데이트 인프라](https://access.redhat.com/products/red-hat-update-infrastructure) Red Hat 인증 클라우드 공급자에 의해 호스트 되는 Red Hat Enterprise Linux 클라우드 인스턴스에 대 한 확장성이 뛰어난 솔루션 toomanage yum 리포지토리 콘텐츠를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution toomanage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="898e1-152">Hello 업스트림 Pulp 프로젝트에 따라, RHUI 허용 클라우드 공급자 toolocally 미러 Red Hat 호스팅되지 리포지토리 콘텐츠, 사용자 지정 저장소도 콘텐츠를 만들고을 부하 분산을 통해 최종 사용자가 해당 저장소 사용 가능한 tooa 큰 그룹 콘텐츠 배달 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-152">Based on hello upstream Pulp project, RHUI allows cloud providers toolocally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available tooa large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="898e1-153">RHUI 사용 가능한 지역</span><span class="sxs-lookup"><span data-stu-id="898e1-153">Regions where RHUI is available</span></span>
<span data-ttu-id="898e1-154">RHUI는 RHEL 주문형 이미지를 사용할 수 있는 모든 지역에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="898e1-155">Hello에 나열 된 모든 public 지역에서는 현재 [Azure 상태 대시보드](https://azure.microsoft.com/status/) 페이지, Azure 미국 정부 및 Azure 독일 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-155">It currently includes all public regions listed on hello [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="898e1-156">RHEL 주문형 이미지에서 프로비전된 VM에 대한 RHUI 액세스 권한은 해당 가격에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="898e1-157">Hello 나중에 요청 시 가용성 RHEL 확장 추가 지역/국가별 클라우드 가용성 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="898e1-158">TooAzure 호스팅되지 RHUI 액세스는 제한 된 toohello Vm 내에서 [Microsoft Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-158">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="898e1-159">다른 업데이트 리파지토리에서 업데이트 받기</span><span class="sxs-lookup"><span data-stu-id="898e1-159">Get updates from another update repository</span></span>
<span data-ttu-id="898e1-160">(Azure 호스팅 RHUI) 하는 대신 다른 업데이트 저장소에서 tooget 업데이트 해야 할 경우 먼저 toounregister RHUI에서 사용자 인스턴스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-160">If you need tooget updates from a different update repository (instead of Azure-hosted RHUI), first you need toounregister your instances from RHUI.</span></span> <span data-ttu-id="898e1-161">Toore 등록 해야 합니다 (예: Red Hat 위성 또는 Red Hat 고객 포털 CDN) hello 원하는 업데이트 인프라를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-161">Then you need toore-register them with hello desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="898e1-162">이러한 서비스에 대한 적합한 Red Hat 구독 및 [Azure에서 Red Hat 클라우드 액세스](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure)에 대한 등록이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="898e1-163">toounregister RHUI tooyour 업데이트 인프라를 다시 등록 하 고 다음이 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-163">toounregister RHUI and reregister tooyour update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="898e1-164">/Etc/yum.repos.d/rh-cloud.repo를 편집 하 고 모든 변경 `enabled=1` 너무`enabled=0`합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` too`enabled=0`.</span></span> <span data-ttu-id="898e1-165">예:</span><span class="sxs-lookup"><span data-stu-id="898e1-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="898e1-166">/Etc/yum/pluginconf.d/rhnplugin.conf를 편집 하 고 변경 `enabled=0` 너무`enabled=1`합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` too`enabled=1`.</span></span>
3. <span data-ttu-id="898e1-167">Red Hat 고객 포털 등 hello 원하는 인프라와를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-167">Then register with hello desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="898e1-168">Red Hat 솔루션 가이드에 따라 [어떻게 tooregister 시스템 toohello Red Hat 고객 포털 구독할](https://access.redhat.com/solutions/253273)합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-168">Follow Red Hat solution guide on [how tooregister and subscribe a system toohello Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="898e1-169">Azure 호스팅 RHUI 액세스 toohello hello RHEL 종 량 제 (PAYG) 이미지 가격에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-169">Access toohello Azure-hosted RHUI is included in hello RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="898e1-170">Azure 호스팅 RHUI hello에서 PAYG RHEL VM의 등록을 취소 해도 VM Bring Your-소유-라이선스 (BYOL) 형식으로 hello 가상 컴퓨터 변환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-170">Unregistering a PAYG RHEL VM from hello Azure-hosted RHUI does not convert hello virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="898e1-171">등록 하는 경우 동일한 VM hello 업데이트의 다른 소스와 있습니다 수 수 비용이 발생 하지 이중: Red Hat 구독에 대 한 두 번째로 Azure RHEL 소프트웨어 요금 및 hello에 대 한 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-171">If you register hello same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and hello second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="898e1-172">Azure 호스팅 RHUI 이외의 업데이트 인프라를 만들고에 설명 된 대로 사용자 고유의 (BYOL 유형) 이미지를 배포 고려 toouse를 일관 되 게 해야 할 경우 [만들기 및 업로드 Red Hat 기반 가상 컴퓨터는 azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 문서.</span><span class="sxs-lookup"><span data-stu-id="898e1-172">If you consistently need toouse an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="898e1-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="898e1-173">Next steps</span></span>
<span data-ttu-id="898e1-174">Red Hat Enterprise Linux VM에서 Azure 마켓플레이스 종 량 제 이미지와 Azure 호스팅 RHUI 활용 toocreate 너무 이동[Azure 마켓플레이스](https://azure.microsoft.com/marketplace/partners/redhat/)합니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-174">toocreate a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="898e1-175">수 toouse 됩니다 `yum update` 추가 설정 없이 RHEL 인스턴스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="898e1-175">You will be able toouse `yum update` in your RHEL instance without any additional setup.</span></span>

