---
title: "GitHub에서 Azure Linux 에이전트 aaaUpdate hello | Microsoft Docs"
description: "자세한 내용은 방법 tooupdate Azure toohello GitHub에서 최신 버전의 Linux VM에 대 한 Azure Linux 에이전트"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a><span data-ttu-id="95cde-103">Tooupdate VM에 Azure Linux 에이전트를 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95cde-103">How tooupdate hello Azure Linux Agent on a VM</span></span>

<span data-ttu-id="95cde-104">tooupdate 프로그램 [Azure Linux 에이전트](https://github.com/Azure/WALinuxAgent) Azure에서 Linux VM에서 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-104">tooupdate your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="95cde-105">Azure에서 실행 중인 Linux VM</span><span class="sxs-lookup"><span data-stu-id="95cde-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="95cde-106">연결 toothat Linux VM SSH를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-106">A connection toothat Linux VM using SSH.</span></span>

<span data-ttu-id="95cde-107">항상 확인 해야 hello Linux 배포판 저장소의 패키지에 대해 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-107">You should always check for a package in hello Linux distro repository first.</span></span> <span data-ttu-id="95cde-108">그러나 있습니다 사용할 수 있는 hello 패키지 hello 최신 버전을 사용 하지 못할 자동 업데이트를 사용 하도록 설정 하면 hello Linux 에이전트는 항상 hello 최신 업데이트 받습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-108">It is possible hello package available may not be hello latest version, however, enabling autoupdate will ensure hello Linux Agent will always get hello latest update.</span></span> <span data-ttu-id="95cde-109">Hello 패키지 관리자에서 설치 문제가 있는 해야 hello distro 공급 업체에서 지원을 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-109">Should you have issues installing from hello package managers, you should seek support from hello distro vendor.</span></span>

## <a name="updating-hello-azure-linux-agent"></a><span data-ttu-id="95cde-110">Hello Azure Linux 에이전트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-110">Updating hello Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="95cde-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="95cde-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="95cde-112">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="95cde-113">패키지 캐시 업데이트</span><span class="sxs-lookup"><span data-stu-id="95cde-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="95cde-114">Hello 최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="95cde-114">Install hello latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="95cde-115">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="95cde-116">사용 하는 경우 먼저 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-116">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="95cde-117">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="95cde-118">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="95cde-119">tooenable 실행:</span><span class="sxs-lookup"><span data-stu-id="95cde-119">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="95cde-120">Hello waagent 서비스를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="95cde-120">Restart hello waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="95cde-121">14.04에 대한 에이전트 다시 시작</span><span class="sxs-lookup"><span data-stu-id="95cde-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="95cde-122">16.04 / 17.04에 대한 에이전트 다시 시작</span><span class="sxs-lookup"><span data-stu-id="95cde-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="95cde-123">Debian</span><span class="sxs-lookup"><span data-stu-id="95cde-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="95cde-124">Debian 7 “Wheezy”</span><span class="sxs-lookup"><span data-stu-id="95cde-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="95cde-125">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="95cde-126">패키지 캐시 업데이트</span><span class="sxs-lookup"><span data-stu-id="95cde-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="95cde-127">Hello 최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="95cde-127">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="95cde-128">에이전트 자동 업데이트 활성화</span><span class="sxs-lookup"><span data-stu-id="95cde-128">Enable agent auto update</span></span>
<span data-ttu-id="95cde-129">이 버전의 Debian이 2.0.16 이상의 버전을 포함하지 않으므로 AutoUpdate를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="95cde-130">hello 패키지가 최신 상태 인지 표시 명령 위에 hello hello 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-130">hello output from hello above command will show you if hello package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="95cde-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span><span class="sxs-lookup"><span data-stu-id="95cde-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="95cde-132">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="95cde-133">패키지 캐시 업데이트</span><span class="sxs-lookup"><span data-stu-id="95cde-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="95cde-134">Hello 최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="95cde-134">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="95cde-135">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="95cde-136">사용 하는 경우 먼저 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-136">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="95cde-137">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="95cde-138">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="95cde-139">tooenable 실행:</span><span class="sxs-lookup"><span data-stu-id="95cde-139">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="95cde-140">Hello waagent 서비스를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="95cde-140">Restart hello waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="95cde-141">Redhat / CentOS</span><span class="sxs-lookup"><span data-stu-id="95cde-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="95cde-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="95cde-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="95cde-143">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="95cde-144">사용 가능한 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="95cde-145">Hello 최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="95cde-145">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="95cde-146">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="95cde-147">사용 하는 경우 먼저 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-147">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="95cde-148">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="95cde-149">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="95cde-150">tooenable 실행:</span><span class="sxs-lookup"><span data-stu-id="95cde-150">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="95cde-151">Hello waagent 서비스를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="95cde-151">Restart hello waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="95cde-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="95cde-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="95cde-153">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="95cde-154">사용 가능한 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="95cde-155">Hello 최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="95cde-155">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="95cde-156">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="95cde-157">사용 하는 경우 먼저 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-157">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="95cde-158">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="95cde-159">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="95cde-160">tooenable 실행:</span><span class="sxs-lookup"><span data-stu-id="95cde-160">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="95cde-161">Hello waagent 서비스를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="95cde-161">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="95cde-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="95cde-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="95cde-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="95cde-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="95cde-164">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="95cde-165">사용 가능한 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-165">Check available updates</span></span>

<span data-ttu-id="95cde-166">위의 출력 hello hello 패키지 toodate 중일 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-166">hello above output will show you if hello package is up toodate.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="95cde-167">Hello 최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="95cde-167">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="95cde-168">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="95cde-169">사용 하는 경우 먼저 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-169">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="95cde-170">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="95cde-171">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="95cde-172">tooenable 실행:</span><span class="sxs-lookup"><span data-stu-id="95cde-172">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="95cde-173">Hello waagent 서비스를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="95cde-173">Restart hello waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="95cde-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="95cde-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="95cde-175">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="95cde-176">사용 가능한 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-176">Check available updates</span></span>

<span data-ttu-id="95cde-177">위의 hello hello 출력을이 hello 패키지 키는 최신 인지 하면 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-177">In hello output from hello above, this will show you if hello package is upto date.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="95cde-178">Hello 최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="95cde-178">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="95cde-179">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="95cde-180">사용 하는 경우 먼저 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-180">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="95cde-181">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="95cde-182">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="95cde-183">tooenable 실행:</span><span class="sxs-lookup"><span data-stu-id="95cde-183">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="95cde-184">Hello waagent 서비스를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="95cde-184">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="95cde-185">Oracle 6 및 7</span><span class="sxs-lookup"><span data-stu-id="95cde-185">Oracle 6 and 7</span></span>

<span data-ttu-id="95cde-186">Oracle Linux에 대 한 확인 해당 hello `Addons` 리포지토리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-186">For Oracle Linux, make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="95cde-187">Tooedit hello 파일 선택 `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) 또는 `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), hello 줄을 변경 하 고 `enabled=0` 너무`enabled=1` 아래 **[ol6_addons]** 또는 **[ol7_addons]** 이 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-187">Choose tooedit hello file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="95cde-188">그런 다음 tooinstall hello 최신 버전의 hello Azure Linux 에이전트 유형:</span><span class="sxs-lookup"><span data-stu-id="95cde-188">Then, tooinstall hello latest version of hello Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="95cde-189">Hello 추가 기능 저장소를 찾을 수 없는 경우 tooyour Oracle Linux 버전에 따라.repo 파일의 hello 끝에이 줄을 간단히 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-189">If you don't find hello add-on repository you can simply add these lines at hello end of your .repo file according tooyour Oracle Linux release:</span></span>

<span data-ttu-id="95cde-190">Oracle Linux 6 가상 컴퓨터의 경우:</span><span class="sxs-lookup"><span data-stu-id="95cde-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="95cde-191">Oracle Linux 7 가상 컴퓨터의 경우:</span><span class="sxs-lookup"><span data-stu-id="95cde-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="95cde-192">그런 다음 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="95cde-193">일반적으로 필요한 경우 tooinstall 필요한 몇 가지 이유로 https://github.com를 직접 사용 하 여 hello 뒤에서 단계를 제외한 모든입니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-193">Typically this is all you need, but if for some reason you need tooinstall it from https://github.com directly, use hello following steps.</span></span>


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="95cde-194">배포에 대 한 에이전트 패키지가 있는 hello Linux 에이전트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-194">Update hello Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="95cde-195">Wget (Redhat, CentOS 및 Oracle Linux 버전 6.4 및 6.5 같이 기본적으로 설치 하지 않는 일부 배포판은) 입력 하 여 설치 `sudo yum install wget` hello 명령줄에서.</span><span class="sxs-lookup"><span data-stu-id="95cde-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on hello command line.</span></span>

### <a name="1-download-hello-latest-version"></a><span data-ttu-id="95cde-196">1. Hello 최신 버전 다운로드</span><span class="sxs-lookup"><span data-stu-id="95cde-196">1. Download hello latest version</span></span>
<span data-ttu-id="95cde-197">열기 [GitHub의 Azure Linux 에이전트의 릴리스 hello](https://github.com/Azure/WALinuxAgent/releases) 웹 페이지 및 hello 최신 버전 번호에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-197">Open [hello release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out hello latest version number.</span></span> <span data-ttu-id="95cde-198">`waagent --version`을 입력하면 현재 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="95cde-199">2.2.x 이상 버전의 경우 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="95cde-200">hello에 다음 줄에서는 2.2.0 버전을 예로:</span><span class="sxs-lookup"><span data-stu-id="95cde-200">hello following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a><span data-ttu-id="95cde-201">2. Hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-201">2. Install hello Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="95cde-202">버전 2.2.x의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="95cde-203">Tooinstall hello 패키지 해야 `setuptools` 처음- [여기](https://pypi.python.org/pypi/setuptools)합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-203">You may need tooinstall hello package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="95cde-204">그런 후 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="95cde-205">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="95cde-206">사용 하는 경우 먼저 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-206">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="95cde-207">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="95cde-208">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="95cde-209">tooenable 실행:</span><span class="sxs-lookup"><span data-stu-id="95cde-209">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a><span data-ttu-id="95cde-210">3. Hello waagent 서비스를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="95cde-210">3. Restart hello waagent service</span></span>
<span data-ttu-id="95cde-211">대부분의 Linux 배포판:</span><span class="sxs-lookup"><span data-stu-id="95cde-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="95cde-212">Ubuntu의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="95cde-213">CoreOS의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a><span data-ttu-id="95cde-214">4. Hello Azure Linux 에이전트 버전 확인</span><span class="sxs-lookup"><span data-stu-id="95cde-214">4. Confirm hello Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="95cde-215">CoreOS, 명령 위에 hello 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-215">For CoreOS, hello above command may not work.</span></span>

<span data-ttu-id="95cde-216">해당 hello Azure Linux 에이전트 버전 되었습니다 toohello 새 버전을 업데이트 하는 것이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-216">You will see that hello Azure Linux Agent version has been updated toohello new version.</span></span>

<span data-ttu-id="95cde-217">Hello Azure Linux 에이전트에 대 한 자세한 내용은 참조 [Azure Linux 에이전트 README](https://github.com/Azure/WALinuxAgent)합니다.</span><span class="sxs-lookup"><span data-stu-id="95cde-217">For more information regarding hello Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>
