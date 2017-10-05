---
title: "Azure Linux VM 에이전트 개요 | Microsoft Docs"
description: "Linux 에이전트(waagent)를 설치 및 구성하여 가상 컴퓨터와 Azure 패브릭 컨트롤러의 상호 작용을 관리하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486ad6bb148583a957fb82b7954ff94f853b12cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-and-using-the-azure-linux-agent"></a><span data-ttu-id="cb6fe-103">Azure Linux 에이전트 이해 및 사용</span><span class="sxs-lookup"><span data-stu-id="cb6fe-103">Understanding and using the Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="cb6fe-104">소개</span><span class="sxs-lookup"><span data-stu-id="cb6fe-104">Introduction</span></span>
<span data-ttu-id="cb6fe-105">Microsoft Azure Linux 에이전트(waagent)는 Linux 및 FreeBSD 프로비저닝, Azure 패브릭 컨트롤러와 VM의 상호 작용을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-105">The Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="cb6fe-106">이 에이전트는 다음과 같은 Linux 및 FreeBSD laaS 배포 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-106">It provides the following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="cb6fe-107">자세한 내용은 Azure Linux 에이전트 [추가 정보](https://github.com/Azure/WALinuxAgent/blob/master/README.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-107">See the Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="cb6fe-108">**이미지 프로비전**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="cb6fe-109">사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="cb6fe-109">Creation of a user account</span></span>
  * <span data-ttu-id="cb6fe-110">SSH 인증 유형 구성</span><span class="sxs-lookup"><span data-stu-id="cb6fe-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="cb6fe-111">SSH 공개 키 및 키 쌍 배포</span><span class="sxs-lookup"><span data-stu-id="cb6fe-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="cb6fe-112">호스트 이름 설정</span><span class="sxs-lookup"><span data-stu-id="cb6fe-112">Setting the host name</span></span>
  * <span data-ttu-id="cb6fe-113">플랫폼 DNS에 호스트 이름 게시</span><span class="sxs-lookup"><span data-stu-id="cb6fe-113">Publishing the host name to the platform DNS</span></span>
  * <span data-ttu-id="cb6fe-114">플랫폼에 SSH 호스트 키 지문 보고</span><span class="sxs-lookup"><span data-stu-id="cb6fe-114">Reporting SSH host key fingerprint to the platform</span></span>
  * <span data-ttu-id="cb6fe-115">리소스 디스크 관리</span><span class="sxs-lookup"><span data-stu-id="cb6fe-115">Resource Disk Management</span></span>
  * <span data-ttu-id="cb6fe-116">리소스 디스크 포맷 및 탑재</span><span class="sxs-lookup"><span data-stu-id="cb6fe-116">Formatting and mounting the resource disk</span></span>
  * <span data-ttu-id="cb6fe-117">스왑 공간 구성</span><span class="sxs-lookup"><span data-stu-id="cb6fe-117">Configuring swap space</span></span>
* <span data-ttu-id="cb6fe-118">**네트워킹**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-118">**Networking**</span></span>
  
  * <span data-ttu-id="cb6fe-119">플랫폼 DHCP 서버와의 호환성을 개선하기 위한 경로 관리</span><span class="sxs-lookup"><span data-stu-id="cb6fe-119">Manages routes to improve compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="cb6fe-120">네트워크 인터페이스 이름의 안정성 확인</span><span class="sxs-lookup"><span data-stu-id="cb6fe-120">Ensures the stability of the network interface name</span></span>
* <span data-ttu-id="cb6fe-121">**커널**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-121">**Kernel**</span></span>
  
  * <span data-ttu-id="cb6fe-122">가상 NUMA 구성(커널에 대해 사용 안 함 <2.6.37)</span><span class="sxs-lookup"><span data-stu-id="cb6fe-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="cb6fe-123">/dev/random의 Hyper-V 엔트로피 이용</span><span class="sxs-lookup"><span data-stu-id="cb6fe-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="cb6fe-124">루트 장치(원격일 수 있음)에 대한 SCSI 시간 제한 구성</span><span class="sxs-lookup"><span data-stu-id="cb6fe-124">Configures SCSI timeouts for the root device (which could be remote)</span></span>
* <span data-ttu-id="cb6fe-125">**진단**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="cb6fe-126">직렬 포트로 콘솔 리디렉션</span><span class="sxs-lookup"><span data-stu-id="cb6fe-126">Console redirection to the serial port</span></span>
* <span data-ttu-id="cb6fe-127">**SCVMM 배포**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="cb6fe-128">System Center Virtual Machine Manager 2012 R2 환경에서 실행되는 경우 Linux용 VMM 에이전트 검색 및 부트스트랩</span><span class="sxs-lookup"><span data-stu-id="cb6fe-128">Detects and bootstraps the VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="cb6fe-129">**VM 확장**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="cb6fe-130">소프트웨어 및 구성 자동화를 사용하도록 Microsoft 및 Partner에서 작성된 구성 요소를 Linux VM(IaaS)에 삽입</span><span class="sxs-lookup"><span data-stu-id="cb6fe-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) to enable software and configuration automation</span></span>
  * <span data-ttu-id="cb6fe-131">[https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="cb6fe-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="cb6fe-132">통신</span><span class="sxs-lookup"><span data-stu-id="cb6fe-132">Communication</span></span>
<span data-ttu-id="cb6fe-133">플랫폼에서 에이전트로의 정보 흐름은 다음 두 채널을 통해 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-133">The information flow from the platform to the agent occurs via two channels:</span></span>

* <span data-ttu-id="cb6fe-134">IaaS 배포를 위해 부팅 시 연결된 DVD.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="cb6fe-135">이 DVD에는 실제 SSH 키 쌍이 아닌 모든 프로비전 정보가 포함된 OVF 규격 구성 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than the actual SSH keypairs.</span></span>
* <span data-ttu-id="cb6fe-136">배포 및 토폴로지 구성을 가져오는 데 사용된 REST API를 공개하는 TCP 끝점</span><span class="sxs-lookup"><span data-stu-id="cb6fe-136">A TCP endpoint exposing a REST API used to obtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="cb6fe-137">요구 사항</span><span class="sxs-lookup"><span data-stu-id="cb6fe-137">Requirements</span></span>
<span data-ttu-id="cb6fe-138">다음 시스템은 테스트를 거쳐 Azure Linux 에이전트와 동작하는 것으로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-138">The following systems have been tested and are known to work with the Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="cb6fe-139">[http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)에서 설명한 대로 Microsoft Azure 플랫폼에서 지원되는 시스템의 공식 목록에서 이 목록은 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-139">This list may differ from the official list of supported systems on the Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="cb6fe-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="cb6fe-140">CoreOS</span></span>
* <span data-ttu-id="cb6fe-141">CentOS 6.3 이상</span><span class="sxs-lookup"><span data-stu-id="cb6fe-141">CentOS 6.3+</span></span>
* <span data-ttu-id="cb6fe-142">Red Hat Enterprise Linux 6.7 이상</span><span class="sxs-lookup"><span data-stu-id="cb6fe-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="cb6fe-143">Debian 7.0 이상</span><span class="sxs-lookup"><span data-stu-id="cb6fe-143">Debian 7.0+</span></span>
* <span data-ttu-id="cb6fe-144">Ubuntu 12.04 이상</span><span class="sxs-lookup"><span data-stu-id="cb6fe-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="cb6fe-145">openSUSE 12.3 이상</span><span class="sxs-lookup"><span data-stu-id="cb6fe-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="cb6fe-146">SLES 11 SP3 이상</span><span class="sxs-lookup"><span data-stu-id="cb6fe-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="cb6fe-147">Oracle Linux 6.4 이상</span><span class="sxs-lookup"><span data-stu-id="cb6fe-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="cb6fe-148">기타 지원되는 시스템:</span><span class="sxs-lookup"><span data-stu-id="cb6fe-148">Other Supported Systems:</span></span>

* <span data-ttu-id="cb6fe-149">FreeBSD 10 이상(Azure Linux 에이전트 v2.0.10 이상)</span><span class="sxs-lookup"><span data-stu-id="cb6fe-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="cb6fe-150">Linux 에이전트는 다음과 같은 일부 시스템 패키지가 있어야 제대로 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-150">The Linux agent depends on some system packages in order to function properly:</span></span>

* <span data-ttu-id="cb6fe-151">Python 2.6 이상</span><span class="sxs-lookup"><span data-stu-id="cb6fe-151">Python 2.6+</span></span>
* <span data-ttu-id="cb6fe-152">OpenSSL 1.0 이상</span><span class="sxs-lookup"><span data-stu-id="cb6fe-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="cb6fe-153">OpenSSH 5.3 이상</span><span class="sxs-lookup"><span data-stu-id="cb6fe-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="cb6fe-154">파일 시스템 유틸리티: sfdisk, fdisk, mkfs, parted</span><span class="sxs-lookup"><span data-stu-id="cb6fe-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="cb6fe-155">암호 도구: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="cb6fe-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="cb6fe-156">텍스트 처리 도구: sed, grep</span><span class="sxs-lookup"><span data-stu-id="cb6fe-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="cb6fe-157">네트워크 도구: ip-route</span><span class="sxs-lookup"><span data-stu-id="cb6fe-157">Network tools: ip-route</span></span>
* <span data-ttu-id="cb6fe-158">UDF 파일 시스템 탑재에 대한 커널 지원</span><span class="sxs-lookup"><span data-stu-id="cb6fe-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="cb6fe-159">설치</span><span class="sxs-lookup"><span data-stu-id="cb6fe-159">Installation</span></span>
<span data-ttu-id="cb6fe-160">배포 패키지에서 리포지토리의 RPM 또는 DEB 패키지를 사용한 설치는 선호하는 Azure Linux Azure 설치 및 업그레이드 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-160">Installation using an RPM or a DEB package from your distribution's package repository is the preferred method of installing and upgrading the Azure Linux Agent.</span></span> <span data-ttu-id="cb6fe-161">모든 [인증 배포 공급자](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)는 이미지 및 리포지토리에 Azure Linux 에이전트 패키지를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-161">All the [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate the Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="cb6fe-162">원본에서 설치 또는 사용자 지정 위치 또는 접두사로의 설치와 같은 고급 설치 옵션에 대한 자세한 내용은 [GitHub의 Azure Linux 에이전트 리포지토리](https://github.com/Azure/WALinuxAgent)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-162">Refer to the documentation in the [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or to custom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="cb6fe-163">명령줄 옵션</span><span class="sxs-lookup"><span data-stu-id="cb6fe-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="cb6fe-164">플래그</span><span class="sxs-lookup"><span data-stu-id="cb6fe-164">Flags</span></span>
* <span data-ttu-id="cb6fe-165">verbose: 지정한 명령의 세부 정보 표시를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="cb6fe-166">force: 일부 명령의 대화형 확인을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="cb6fe-167">명령</span><span class="sxs-lookup"><span data-stu-id="cb6fe-167">Commands</span></span>
* <span data-ttu-id="cb6fe-168">help: 지원되는 명령 및 플래그를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-168">help: Lists the supported commands and flags.</span></span>
* <span data-ttu-id="cb6fe-169">deprovision: 시스템을 정리하여 다시 프로비전하기에 적합하도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-169">deprovision: Attempt to clean the system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="cb6fe-170">이 작업은 다음을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-170">This operation deleted the following:</span></span>
  
  * <span data-ttu-id="cb6fe-171">모든 SSH 호스트 키(구성 파일에서 Provisioning.RegenerateSshHostKeyPair가 'y'인 경우)</span><span class="sxs-lookup"><span data-stu-id="cb6fe-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="cb6fe-172">/etc/resolv.conf의 Nameserver 구성</span><span class="sxs-lookup"><span data-stu-id="cb6fe-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="cb6fe-173">/etc/shadow의 루트 암호(구성 파일에서 Provisioning.DeleteRootPassword가 'y'인 경우)</span><span class="sxs-lookup"><span data-stu-id="cb6fe-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="cb6fe-174">캐시된 DHCP 클라이언트 임대</span><span class="sxs-lookup"><span data-stu-id="cb6fe-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="cb6fe-175">호스트 이름을 localhost.localdomain으로 다시 설정</span><span class="sxs-lookup"><span data-stu-id="cb6fe-175">Resets host name to localhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="cb6fe-176">Deprovision 명령을 사용한다고 해서 이미지에서 중요한 정보를 모두 지우고 다시 배포하기에 적합하게 만든다고 보증할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-176">Deprovisioning does not guarantee that the image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="cb6fe-177">deprovision+user: -deprovision(위 참조) 명령의 모든 작업을 수행하고 마지막으로 프로비전한 사용자 계정(/var/lib/waagent에서 가져온 계정) 및 연결된 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-177">deprovision+user: Performs everything under -deprovision (above) and also deletes the last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="cb6fe-178">Azure에서 이전에 프로비전한 이미지의 프로비전을 해제하여 이미지를 캡처하고 다시 사용할 수 있도록 하는 경우에 이 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="cb6fe-179">version: waagent의 버전을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-179">version: Displays the version of waagent</span></span>
* <span data-ttu-id="cb6fe-180">serialconsole: ttyS0(첫 번째 직렬 포트)을 부팅 콘솔로 표시하도록 GRUB를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-180">serialconsole: Configures GRUB to mark ttyS0 (the first serial port) as the boot console.</span></span> <span data-ttu-id="cb6fe-181">이 매개 변수는 커널 부팅 로그를 직렬 포트로 보내고 디버깅에 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-181">This ensures that kernel bootup logs are sent to the serial port and made available for debugging.</span></span>
* <span data-ttu-id="cb6fe-182">daemon: waagent를 디먼으로 실행하여 플랫폼 조작을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-182">daemon: Run waagent as a daemon to manage interaction with the platform.</span></span> <span data-ttu-id="cb6fe-183">이 인수는 waagent init 스크립트에서 waagent에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-183">This argument is specified to waagent in the waagent init script.</span></span>
* <span data-ttu-id="cb6fe-184">start: waagent를 백그라운드 프로세스로 실행</span><span class="sxs-lookup"><span data-stu-id="cb6fe-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="cb6fe-185">구성</span><span class="sxs-lookup"><span data-stu-id="cb6fe-185">Configuration</span></span>
<span data-ttu-id="cb6fe-186">구성 파일(/etc/waagent.conf)은 waagent의 동작을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-186">A configuration file (/etc/waagent.conf) controls the actions of waagent.</span></span> <span data-ttu-id="cb6fe-187">다음은 샘플 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-187">A sample configuration file is shown below:</span></span>

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

<span data-ttu-id="cb6fe-188">다양한 구성 옵션이 아래에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-188">The various configuration options are described in detail below.</span></span> <span data-ttu-id="cb6fe-189">구성 옵션으로 부울, 문자열 또는 정수의 세 가지 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="cb6fe-190">부울 구성 옵션은 "y" 또는 "n"으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-190">The Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="cb6fe-191">특수 키워드 "None"은 아래에 자세히 설명된 대로 일부 문자열 형식 구성 항목에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-191">The special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="cb6fe-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="cb6fe-193">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb6fe-193">Type: Boolean</span></span>  
<span data-ttu-id="cb6fe-194">기본값: y</span><span class="sxs-lookup"><span data-stu-id="cb6fe-194">Default: y</span></span>

<span data-ttu-id="cb6fe-195">이 옵션을 통해 사용자가 에이전트의 프로비전 기능을 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-195">This allows the user to enable or disable the provisioning functionality in the agent.</span></span> <span data-ttu-id="cb6fe-196">유효한 값은 "y" 또는 "n"입니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="cb6fe-197">프로비전을 사용하지 않도록 설정한 경우 이미지의 SSH 호스트 및 사용자 키는 유지되며 Azure 프로비전 API에서 지정한 모든 구성은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-197">If provisioning is disabled, SSH host and user keys in the image are preserved and any configuration specified in the Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="cb6fe-198">프로비전에 cloud-init를 사용하는 Ubuntu 클라우드 이미지에서 `Provisioning.Enabled` 매개 변수의 기본값은 "n"입니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-198">The `Provisioning.Enabled` parameter defaults to "n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="cb6fe-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="cb6fe-200">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb6fe-200">Type: Boolean</span></span>  
<span data-ttu-id="cb6fe-201">기본값: n</span><span class="sxs-lookup"><span data-stu-id="cb6fe-201">Default: n</span></span>

<span data-ttu-id="cb6fe-202">설정한 경우 /etc/shadow 파일의 루트 암호가 프로비전 프로세스 중 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-202">If set, the root password in the /etc/shadow file is erased during the provisioning process.</span></span>

<span data-ttu-id="cb6fe-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="cb6fe-204">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb6fe-204">Type: Boolean</span></span>  
<span data-ttu-id="cb6fe-205">기본값: y</span><span class="sxs-lookup"><span data-stu-id="cb6fe-205">Default: y</span></span>

<span data-ttu-id="cb6fe-206">설정한 경우 모든 SSH 호스트 키 쌍(ecdsa, dsa 및 rsa)이 프로비전 프로세스 중 /etc/ssh/에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during the provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="cb6fe-207">그리고 새로운 단일 키 쌍이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="cb6fe-208">새로운 키 쌍의 암호화 종류는 Provisioning.SshHostKeyPairType 항목으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-208">The encryption type for the fresh key pair is configurable by the Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="cb6fe-209">일부 배포에서는 SSH 디먼이 다시 시작될 때(예: 다시 부팅될 때) 누락된 모든 암호화 종류에 대해 SSH 키 쌍을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when the SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="cb6fe-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="cb6fe-211">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb6fe-211">Type: String</span></span>  
<span data-ttu-id="cb6fe-212">기본값: rsa</span><span class="sxs-lookup"><span data-stu-id="cb6fe-212">Default: rsa</span></span>

<span data-ttu-id="cb6fe-213">이 옵션은 가상 컴퓨터의 SSH 디먼에서 지원하는 암호화 알고리즘 형식으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-213">This can be set to an encryption algorithm type that is supported by the SSH daemon on the virtual machine.</span></span> <span data-ttu-id="cb6fe-214">일반적으로 지원되는 값은 "rsa", "dsa" 및 "ecdsa"입니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-214">The typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="cb6fe-215">Windows의 "putty.exe"는 "ecdsa"를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="cb6fe-216">따라서 Windows에서 putty.exe를 사용하여 Linux 배포에 연결하려는 경우 "rsa" 또는 "dsa"를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-216">So, if you intend to use putty.exe on Windows to connect to a Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="cb6fe-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="cb6fe-218">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb6fe-218">Type: Boolean</span></span>  
<span data-ttu-id="cb6fe-219">기본값: y</span><span class="sxs-lookup"><span data-stu-id="cb6fe-219">Default: y</span></span>

<span data-ttu-id="cb6fe-220">설정한 경우 waagent가 Linux 가상 컴퓨터에서 호스트 이름("hostname" 명령에서 반환하는 이름)의 변경 여부를 모니터링하고, 이미지의 네트워킹 구성을 자동으로 업데이트하여 변경 내용을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-220">If set, waagent will monitor the Linux virtual machine for hostname changes (as returned by the "hostname" command) and automatically update the networking configuration in the image to reflect the change.</span></span> <span data-ttu-id="cb6fe-221">DNS 서버로 이름 변경을 푸시하기 위해 가상 컴퓨터에서 네트워킹이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-221">In order to push the name change to the DNS servers, networking will be restarted in the virtual machine.</span></span> <span data-ttu-id="cb6fe-222">이 때문에 인터넷 연결이 잠시 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="cb6fe-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="cb6fe-224">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb6fe-224">Type: Boolean</span></span>  
<span data-ttu-id="cb6fe-225">기본값: n</span><span class="sxs-lookup"><span data-stu-id="cb6fe-225">Default: n</span></span>

<span data-ttu-id="cb6fe-226">설정되면 waagent는 Base64에서 CustomData를 디코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="cb6fe-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="cb6fe-228">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb6fe-228">Type: Boolean</span></span>  
<span data-ttu-id="cb6fe-229">기본값: n</span><span class="sxs-lookup"><span data-stu-id="cb6fe-229">Default: n</span></span>

<span data-ttu-id="cb6fe-230">설정되면 waagent는 프로비전 후에 CustomData를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="cb6fe-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="cb6fe-232">형식:String</span><span class="sxs-lookup"><span data-stu-id="cb6fe-232">Type:String</span></span>  
<span data-ttu-id="cb6fe-233">기본값: 6</span><span class="sxs-lookup"><span data-stu-id="cb6fe-233">Default:6</span></span>

<span data-ttu-id="cb6fe-234">암호 해시를 생성할 때 암호화에 사용되는 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="cb6fe-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="cb6fe-235">1 - MD5</span></span>  
 <span data-ttu-id="cb6fe-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="cb6fe-236">2a - Blowfish</span></span>  
 <span data-ttu-id="cb6fe-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="cb6fe-237">5 - SHA-256</span></span>  
 <span data-ttu-id="cb6fe-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="cb6fe-238">6 - SHA-512</span></span>  

<span data-ttu-id="cb6fe-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="cb6fe-240">형식:String</span><span class="sxs-lookup"><span data-stu-id="cb6fe-240">Type:String</span></span>  
<span data-ttu-id="cb6fe-241">기본값: 10</span><span class="sxs-lookup"><span data-stu-id="cb6fe-241">Default:10</span></span>

<span data-ttu-id="cb6fe-242">암호 해시를 생성할 때 사용되는 임의 salt의 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="cb6fe-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="cb6fe-244">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb6fe-244">Type: Boolean</span></span>  
<span data-ttu-id="cb6fe-245">기본값: y</span><span class="sxs-lookup"><span data-stu-id="cb6fe-245">Default: y</span></span>

<span data-ttu-id="cb6fe-246">설정한 경우 "ResourceDisk.Filesystem"에서 사용자가 요청한 파일 시스템 유형이 "ntfs" 이외의 유형이면 플랫폼에서 제공한 리소스 디스크가 waagent로 포맷되어 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-246">If set, the resource disk provided by the platform will be formatted and mounted by waagent if the filesystem type requested by the user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="cb6fe-247">단일 Linux 파티션 유형(83)을 디스크에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-247">A single partition of type Linux (83) will be made available on the disk.</span></span> <span data-ttu-id="cb6fe-248">이 파티션이 탑재될 수 있는 경우에는 포맷되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="cb6fe-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="cb6fe-250">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb6fe-250">Type: String</span></span>  
<span data-ttu-id="cb6fe-251">기본값: ext4</span><span class="sxs-lookup"><span data-stu-id="cb6fe-251">Default: ext4</span></span>

<span data-ttu-id="cb6fe-252">이 옵션은 리소스 디스크의 파일 시스템 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-252">This specifies the filesystem type for the resource disk.</span></span> <span data-ttu-id="cb6fe-253">지원되는 값은 Linux 배포에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="cb6fe-254">문자열이 X이면 mkfs.X가 Linux 이미지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-254">If the string is X, then mkfs.X should be present on the Linux image.</span></span> <span data-ttu-id="cb6fe-255">일반적으로 SLES 11 이미지는 'ext3'을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="cb6fe-256">여기에서 FreeBSD 이미지는 'ufs2'를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="cb6fe-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="cb6fe-258">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb6fe-258">Type: String</span></span>  
<span data-ttu-id="cb6fe-259">기본값: /mnt/resource</span><span class="sxs-lookup"><span data-stu-id="cb6fe-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="cb6fe-260">이 옵션은 리소스 디스크가 탑재되는 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-260">This specifies the path at which the resource disk is mounted.</span></span> <span data-ttu-id="cb6fe-261">리소스 디스크는 *임시* 디스크이며 VM의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-261">Note that the resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span>

<span data-ttu-id="cb6fe-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="cb6fe-263">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb6fe-263">Type: String</span></span>  
<span data-ttu-id="cb6fe-264">기본값: 없음</span><span class="sxs-lookup"><span data-stu-id="cb6fe-264">Default: None</span></span>

<span data-ttu-id="cb6fe-265">mount -o 명령에 전달될 디스크 탑재 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-265">Specifies disk mount options to be passed to the mount -o command.</span></span> <span data-ttu-id="cb6fe-266">쉼표로 구분된 값 목록입니다(예:</span><span class="sxs-lookup"><span data-stu-id="cb6fe-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="cb6fe-267">'nodev,nosuid').</span><span class="sxs-lookup"><span data-stu-id="cb6fe-267">'nodev,nosuid'.</span></span> <span data-ttu-id="cb6fe-268">자세한 내용은 mount(8)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-268">See mount(8) for details.</span></span>

<span data-ttu-id="cb6fe-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="cb6fe-270">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb6fe-270">Type: Boolean</span></span>  
<span data-ttu-id="cb6fe-271">기본값: n</span><span class="sxs-lookup"><span data-stu-id="cb6fe-271">Default: n</span></span>

<span data-ttu-id="cb6fe-272">설정한 경우 스왑 파일(/swapfile)이 리소스 디스크에 만들어져서 시스템 스왑 공간에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-272">If set, a swap file (/swapfile) is created on the resource disk and added to the system swap space.</span></span>

<span data-ttu-id="cb6fe-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="cb6fe-274">형식: Integer</span><span class="sxs-lookup"><span data-stu-id="cb6fe-274">Type: Integer</span></span>  
<span data-ttu-id="cb6fe-275">기본값: 0</span><span class="sxs-lookup"><span data-stu-id="cb6fe-275">Default: 0</span></span>

<span data-ttu-id="cb6fe-276">스왑 파일의 크기(MB)입니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-276">The size of the swap file in megabytes.</span></span>

<span data-ttu-id="cb6fe-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="cb6fe-278">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb6fe-278">Type: Boolean</span></span>  
<span data-ttu-id="cb6fe-279">기본값: n</span><span class="sxs-lookup"><span data-stu-id="cb6fe-279">Default: n</span></span>

<span data-ttu-id="cb6fe-280">설정한 경우 로그에 대한 세부 정보 표시가 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="cb6fe-281">Waagent가 /var/log/waagent.log에 로깅하고 시스템 logrotate 기능을 활용하여 로그를 순환시킵니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-281">Waagent logs to /var/log/waagent.log and leverages the system logrotate functionality to rotate logs.</span></span>

<span data-ttu-id="cb6fe-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="cb6fe-283">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb6fe-283">Type: Boolean</span></span>  
<span data-ttu-id="cb6fe-284">기본값: n</span><span class="sxs-lookup"><span data-stu-id="cb6fe-284">Default: n</span></span>

<span data-ttu-id="cb6fe-285">설정되면 에이전트는 기본 하드웨어의 펌웨어 버전과 일치하는 RDMA 커널 드라이버를 로드한 후 설치하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-285">If set, the agent will attempt to install and then load an RDMA kernel driver that matches the version of the firmware on the underlying hardware.</span></span>

<span data-ttu-id="cb6fe-286">**OS.RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="cb6fe-287">형식: Integer</span><span class="sxs-lookup"><span data-stu-id="cb6fe-287">Type: Integer</span></span>  
<span data-ttu-id="cb6fe-288">기본값: 300</span><span class="sxs-lookup"><span data-stu-id="cb6fe-288">Default: 300</span></span>

<span data-ttu-id="cb6fe-289">이 옵션은 OS 디스크 및 데이터 드라이브에서 SCSI 시간 제한을 초 단위로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-289">This configures the SCSI timeout in seconds on the OS disk and data drives.</span></span> <span data-ttu-id="cb6fe-290">설정하지 않은 경우 시스템 기본값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-290">If not set, the system defaults are used.</span></span>

<span data-ttu-id="cb6fe-291">**OS.OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="cb6fe-292">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb6fe-292">Type: String</span></span>  
<span data-ttu-id="cb6fe-293">기본값: 없음</span><span class="sxs-lookup"><span data-stu-id="cb6fe-293">Default: None</span></span>

<span data-ttu-id="cb6fe-294">이 옵션은 openssl 이진의 대체 경로를 지정하는 데 사용하여 암호화 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-294">This can be used to specify an alternate path for the openssl binary to use for cryptographic operations.</span></span>

<span data-ttu-id="cb6fe-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="cb6fe-296">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb6fe-296">Type: String</span></span>  
<span data-ttu-id="cb6fe-297">기본값: 없음</span><span class="sxs-lookup"><span data-stu-id="cb6fe-297">Default: None</span></span>

<span data-ttu-id="cb6fe-298">설정되면 에이전트는 이 프록시 서버를 사용하여 인터넷에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-298">If set, the agent will use this proxy server to access the internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="cb6fe-299">Ubuntu 클라우드 이미지</span><span class="sxs-lookup"><span data-stu-id="cb6fe-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="cb6fe-300">Ubuntu 클라우드 이미지는 [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) 을 사용하여 Azure Linux 에이전트에 서 관리되는 여러 구성 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) to perform many configuration tasks that would otherwise be managed by the Azure Linux Agent.</span></span>  <span data-ttu-id="cb6fe-301">다음과 같은 차이점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-301">Please note the following differences:</span></span>

* <span data-ttu-id="cb6fe-302">**Provisioning.Enabled** 프로비전 작업을 수행하기 위해 cloud-init을 사용하는 Ubuntu 클라우드 이미지에서 기본값은 "n"입니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-302">**Provisioning.Enabled** defaults to "n" on Ubuntu Cloud Images that use cloud-init to perform provisioning tasks.</span></span>
* <span data-ttu-id="cb6fe-303">다음 구성 매개 변수는 cloud-init을 사용하여 리소스 디스크와 swap 공간을 관리하는 Ubuntu 클라우드 이미지에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-303">The following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init to manage the resource disk and swap space:</span></span>
  
  * <span data-ttu-id="cb6fe-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="cb6fe-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="cb6fe-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="cb6fe-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="cb6fe-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="cb6fe-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="cb6fe-309">프로비전 중 Ubuntu 클라우드 이미지에서 리소스 디스크 탑재 지점 및 swap 공간을 구성하려면 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb6fe-309">Please see the following resources to configure the resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="cb6fe-310">Ubuntu Wiki: Swap 파티션 구성</span><span class="sxs-lookup"><span data-stu-id="cb6fe-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="cb6fe-311">Azure 가상 컴퓨터에 사용자 지정 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="cb6fe-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

