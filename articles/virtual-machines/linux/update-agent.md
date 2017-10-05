---
title: "GitHub에서 Azure Linux 에이전트 업데이트 | Microsoft Docs"
description: "Azure Linux VM의 Azure Linux 에이전트를 GitHub의 최신 버전으로 업데이트하는 방법을 알아봅니다."
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
ms.openlocfilehash: c79e37976a58ae5384b5856e0f7f258a773ef0fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-update-the-azure-linux-agent-on-a-vm"></a><span data-ttu-id="db1ae-103">VM에서 Azure Linux 에이전트를 업데이트하는 방법</span><span class="sxs-lookup"><span data-stu-id="db1ae-103">How to update the Azure Linux Agent on a VM</span></span>

<span data-ttu-id="db1ae-104">Azure Linux VM에서 [Azure Linux 에이전트](https://github.com/Azure/WALinuxAgent) 를 업데이트하려면 다음 항목이 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-104">To update your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="db1ae-105">Azure에서 실행 중인 Linux VM</span><span class="sxs-lookup"><span data-stu-id="db1ae-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="db1ae-106">SSH를 사용하여 해당 Linux VM에 연결</span><span class="sxs-lookup"><span data-stu-id="db1ae-106">A connection to that Linux VM using SSH.</span></span>

<span data-ttu-id="db1ae-107">항상 Linux 배포판 리포지토리의 패키지에 대해 먼저 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-107">You should always check for a package in the Linux distro repository first.</span></span> <span data-ttu-id="db1ae-108">사용 가능한 패키지는 최신 버전이 아닐 수도 있지만 자동 업데이트를 사용하면 Linux 에이전트에서 항상 최신 업데이트를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-108">It is possible the package available may not be the latest version, however, enabling autoupdate will ensure the Linux Agent will always get the latest update.</span></span> <span data-ttu-id="db1ae-109">패키지 관리자에서 설치 문제가 있는 경우 배포판 공급 업체에서 지원을 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-109">Should you have issues installing from the package managers, you should seek support from the distro vendor.</span></span>

## <a name="updating-the-azure-linux-agent"></a><span data-ttu-id="db1ae-110">Azure Linux 에이전트 업데이트</span><span class="sxs-lookup"><span data-stu-id="db1ae-110">Updating the Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="db1ae-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="db1ae-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db1ae-112">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="db1ae-113">패키지 캐시 업데이트</span><span class="sxs-lookup"><span data-stu-id="db1ae-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db1ae-114">최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="db1ae-114">Install the latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db1ae-115">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="db1ae-116">먼저 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-116">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db1ae-117">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db1ae-118">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db1ae-119">실행을 활성화하려면:</span><span class="sxs-lookup"><span data-stu-id="db1ae-119">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="db1ae-120">waagent 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="db1ae-120">Restart the waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="db1ae-121">14.04에 대한 에이전트 다시 시작</span><span class="sxs-lookup"><span data-stu-id="db1ae-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="db1ae-122">16.04 / 17.04에 대한 에이전트 다시 시작</span><span class="sxs-lookup"><span data-stu-id="db1ae-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="db1ae-123">Debian</span><span class="sxs-lookup"><span data-stu-id="db1ae-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="db1ae-124">Debian 7 “Wheezy”</span><span class="sxs-lookup"><span data-stu-id="db1ae-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db1ae-125">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="db1ae-126">패키지 캐시 업데이트</span><span class="sxs-lookup"><span data-stu-id="db1ae-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db1ae-127">최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="db1ae-127">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="db1ae-128">에이전트 자동 업데이트 활성화</span><span class="sxs-lookup"><span data-stu-id="db1ae-128">Enable agent auto update</span></span>
<span data-ttu-id="db1ae-129">이 버전의 Debian이 2.0.16 이상의 버전을 포함하지 않으므로 AutoUpdate를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="db1ae-130">위 명령의 출력에서 패키지가 최신 상태인지 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-130">The output from the above command will show you if the package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="db1ae-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span><span class="sxs-lookup"><span data-stu-id="db1ae-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db1ae-132">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="db1ae-133">패키지 캐시 업데이트</span><span class="sxs-lookup"><span data-stu-id="db1ae-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db1ae-134">최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="db1ae-134">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db1ae-135">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="db1ae-136">먼저 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-136">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db1ae-137">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db1ae-138">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db1ae-139">실행을 활성화하려면:</span><span class="sxs-lookup"><span data-stu-id="db1ae-139">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="db1ae-140">waagent 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="db1ae-140">Restart the waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="db1ae-141">Redhat / CentOS</span><span class="sxs-lookup"><span data-stu-id="db1ae-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="db1ae-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="db1ae-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db1ae-143">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="db1ae-144">사용 가능한 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db1ae-145">최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="db1ae-145">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db1ae-146">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="db1ae-147">먼저 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-147">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db1ae-148">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db1ae-149">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db1ae-150">실행을 활성화하려면:</span><span class="sxs-lookup"><span data-stu-id="db1ae-150">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="db1ae-151">waagent 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="db1ae-151">Restart the waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="db1ae-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="db1ae-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db1ae-153">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="db1ae-154">사용 가능한 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db1ae-155">최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="db1ae-155">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db1ae-156">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="db1ae-157">먼저 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-157">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db1ae-158">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db1ae-159">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db1ae-160">실행을 활성화하려면:</span><span class="sxs-lookup"><span data-stu-id="db1ae-160">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="db1ae-161">waagent 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="db1ae-161">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="db1ae-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="db1ae-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="db1ae-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="db1ae-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db1ae-164">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="db1ae-165">사용 가능한 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-165">Check available updates</span></span>

<span data-ttu-id="db1ae-166">위의 출력에서 패키지가 최신 상태인지 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-166">The above output will show you if the package is up to date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db1ae-167">최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="db1ae-167">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db1ae-168">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="db1ae-169">먼저 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-169">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db1ae-170">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db1ae-171">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db1ae-172">실행을 활성화하려면:</span><span class="sxs-lookup"><span data-stu-id="db1ae-172">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="db1ae-173">waagent 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="db1ae-173">Restart the waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="db1ae-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="db1ae-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="db1ae-175">현재 패키지 버전 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="db1ae-176">사용 가능한 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-176">Check available updates</span></span>

<span data-ttu-id="db1ae-177">위의 출력에서 패키지가 최신 상태인지 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-177">In the output from the above, this will show you if the package is upto date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="db1ae-178">최신 패키지 버전 설치</span><span class="sxs-lookup"><span data-stu-id="db1ae-178">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db1ae-179">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="db1ae-180">먼저 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-180">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db1ae-181">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db1ae-182">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db1ae-183">실행을 활성화하려면:</span><span class="sxs-lookup"><span data-stu-id="db1ae-183">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="db1ae-184">waagent 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="db1ae-184">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="db1ae-185">Oracle 6 및 7</span><span class="sxs-lookup"><span data-stu-id="db1ae-185">Oracle 6 and 7</span></span>

<span data-ttu-id="db1ae-186">Oracle Linux의 경우 `Addons` 리포지토리가 사용되도록 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-186">For Oracle Linux, make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="db1ae-187">파일 `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) 또는 파일 `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux)를 편집하고 이 파일의 **[ol6_addons]** 또는 **[ol7_addons]** 아래에서 줄 `enabled=0`을 `enabled=1`로 변경하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-187">Choose to edit the file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="db1ae-188">그런 다음 최신 버전의 Azure Linux 에이전트를 설치하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-188">Then, to install the latest version of the Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="db1ae-189">추가 기능 리포지토리를 찾을 수 없는 경우 Oracle Linux 릴리스에 따라 .repo 파일의 맨 뒤에 다음 줄을 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-189">If you don't find the add-on repository you can simply add these lines at the end of your .repo file according to your Oracle Linux release:</span></span>

<span data-ttu-id="db1ae-190">Oracle Linux 6 가상 컴퓨터의 경우:</span><span class="sxs-lookup"><span data-stu-id="db1ae-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="db1ae-191">Oracle Linux 7 가상 컴퓨터의 경우:</span><span class="sxs-lookup"><span data-stu-id="db1ae-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="db1ae-192">그런 다음 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="db1ae-193">일반적으로는 이렇게만 하면 되지만 어떤 이유로든 https://github.com에서 직접 설치해야 하는 경우 다음 단계를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="db1ae-193">Typically this is all you need, but if for some reason you need to install it from https://github.com directly, use the following steps.</span></span>


## <a name="update-the-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="db1ae-194">배포에 대해 에이전트 패키지가 없는 경우 Linux 에이전트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-194">Update the Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="db1ae-195">명령줄에 `sudo yum install wget`를 입력하여 wget를 설치합니다. Redhat, CentOS, Oracle Linux 버전 6.4 및 6.5와 같이 기본적으로 이 방법으로 설치되지 않는 몇 가지 배포판이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on the command line.</span></span>

### <a name="1-download-the-latest-version"></a><span data-ttu-id="db1ae-196">1. 최신 버전 다운로드</span><span class="sxs-lookup"><span data-stu-id="db1ae-196">1. Download the latest version</span></span>
<span data-ttu-id="db1ae-197">웹 페이지에서 [GitHub의 Azure Linux 에이전트 릴리스](https://github.com/Azure/WALinuxAgent/releases) 를 열고 최신 버전 번호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-197">Open [the release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out the latest version number.</span></span> <span data-ttu-id="db1ae-198">`waagent --version`을 입력하면 현재 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="db1ae-199">2.2.x 이상 버전의 경우 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="db1ae-200">예를 들어 다음 줄에서는 버전 2.2.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-200">The following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-the-azure-linux-agent"></a><span data-ttu-id="db1ae-201">2. Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-201">2. Install the Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="db1ae-202">버전 2.2.x의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="db1ae-203">`setuptools` 패키지를 먼저 설치해야 할 수도 있습니다. [여기](https://pypi.python.org/pypi/setuptools)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db1ae-203">You may need to install the package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="db1ae-204">그런 후 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="db1ae-205">자동 업데이트가 활성화되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="db1ae-206">먼저 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-206">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="db1ae-207">'AutoUpdate.Enabled'를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="db1ae-208">이 출력이 표시되는 경우 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="db1ae-209">실행을 활성화하려면:</span><span class="sxs-lookup"><span data-stu-id="db1ae-209">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-the-waagent-service"></a><span data-ttu-id="db1ae-210">3. waagent 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="db1ae-210">3. Restart the waagent service</span></span>
<span data-ttu-id="db1ae-211">대부분의 Linux 배포판:</span><span class="sxs-lookup"><span data-stu-id="db1ae-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="db1ae-212">Ubuntu의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="db1ae-213">CoreOS의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-the-azure-linux-agent-version"></a><span data-ttu-id="db1ae-214">4. Azure Linux 에이전트 버전 확인</span><span class="sxs-lookup"><span data-stu-id="db1ae-214">4. Confirm the Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="db1ae-215">CoreOS에서는 위의 명령이 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-215">For CoreOS, the above command may not work.</span></span>

<span data-ttu-id="db1ae-216">Azure Linux 에이전트 버전이 새 버전으로 업데이트된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db1ae-216">You will see that the Azure Linux Agent version has been updated to the new version.</span></span>

<span data-ttu-id="db1ae-217">Azure Linux 에이전트에 대한 자세한 내용은 [Azure Linux 에이전트 추가 정보](https://github.com/Azure/WALinuxAgent)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db1ae-217">For more information regarding the Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>