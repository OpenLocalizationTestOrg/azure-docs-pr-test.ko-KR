---
title: "Linux VM 에이전트 개요 aaaAzure | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall 및 Linux 에이전트 (waagent) toomanage Azure 패브릭 컨트롤러와 가상 컴퓨터의 상호 작용을 구성 합니다."
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
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a><span data-ttu-id="2e1ca-103">이해 및 hello Azure Linux 에이전트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-103">Understanding and using hello Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="2e1ca-104">소개</span><span class="sxs-lookup"><span data-stu-id="2e1ca-104">Introduction</span></span>
<span data-ttu-id="2e1ca-105">hello Microsoft Azure Linux 에이전트 (waagent) Linux 및 FreeBSD 프로비저닝, 및 hello Azure 패브릭 컨트롤러와 VM의 상호 작용을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-105">hello Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="2e1ca-106">Linux 및 FreeBSD IaaS 배포에 대 한 기능을 수행 하는 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-106">It provides hello following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="2e1ca-107">Hello Azure Linux 에이전트 참조 [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) 추가 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-107">See hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="2e1ca-108">**이미지 프로비전**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="2e1ca-109">사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2e1ca-109">Creation of a user account</span></span>
  * <span data-ttu-id="2e1ca-110">SSH 인증 유형 구성</span><span class="sxs-lookup"><span data-stu-id="2e1ca-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="2e1ca-111">SSH 공개 키 및 키 쌍 배포</span><span class="sxs-lookup"><span data-stu-id="2e1ca-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="2e1ca-112">설정 hello 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="2e1ca-112">Setting hello host name</span></span>
  * <span data-ttu-id="2e1ca-113">게시 hello 호스트 이름 toohello 플랫폼 DNS</span><span class="sxs-lookup"><span data-stu-id="2e1ca-113">Publishing hello host name toohello platform DNS</span></span>
  * <span data-ttu-id="2e1ca-114">보고 SSH 호스트 키 지문 toohello 플랫폼</span><span class="sxs-lookup"><span data-stu-id="2e1ca-114">Reporting SSH host key fingerprint toohello platform</span></span>
  * <span data-ttu-id="2e1ca-115">리소스 디스크 관리</span><span class="sxs-lookup"><span data-stu-id="2e1ca-115">Resource Disk Management</span></span>
  * <span data-ttu-id="2e1ca-116">서식 지정 및 hello 리소스 디스크를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-116">Formatting and mounting hello resource disk</span></span>
  * <span data-ttu-id="2e1ca-117">스왑 공간 구성</span><span class="sxs-lookup"><span data-stu-id="2e1ca-117">Configuring swap space</span></span>
* <span data-ttu-id="2e1ca-118">**네트워킹**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-118">**Networking**</span></span>
  
  * <span data-ttu-id="2e1ca-119">경로 tooimprove 호환 플랫폼 DHCP 서버 관리</span><span class="sxs-lookup"><span data-stu-id="2e1ca-119">Manages routes tooimprove compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="2e1ca-120">Hello 네트워크 인터페이스 이름의 hello 안정성 보장</span><span class="sxs-lookup"><span data-stu-id="2e1ca-120">Ensures hello stability of hello network interface name</span></span>
* <span data-ttu-id="2e1ca-121">**커널**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-121">**Kernel**</span></span>
  
  * <span data-ttu-id="2e1ca-122">가상 NUMA 구성(커널에 대해 사용 안 함 <2.6.37)</span><span class="sxs-lookup"><span data-stu-id="2e1ca-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="2e1ca-123">/dev/random의 Hyper-V 엔트로피 이용</span><span class="sxs-lookup"><span data-stu-id="2e1ca-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="2e1ca-124">Hello 루트 장치 (원격 일 수도 있음)에 대 한 SCSI 제한 구성</span><span class="sxs-lookup"><span data-stu-id="2e1ca-124">Configures SCSI timeouts for hello root device (which could be remote)</span></span>
* <span data-ttu-id="2e1ca-125">**진단**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="2e1ca-126">콘솔 리디렉션 toohello 직렬 포트</span><span class="sxs-lookup"><span data-stu-id="2e1ca-126">Console redirection toohello serial port</span></span>
* <span data-ttu-id="2e1ca-127">**SCVMM 배포**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="2e1ca-128">검색 하 고 System Center Virtual Machine Manager 2012 R2 환경에서 실행 하는 경우 Linux 용 hello VMM 에이전트를 시작 되도록</span><span class="sxs-lookup"><span data-stu-id="2e1ca-128">Detects and bootstraps hello VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="2e1ca-129">**VM 확장**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="2e1ca-130">Linux VM (IaaS) tooenable 소프트웨어 및 구성 자동화로 Microsoft 및 협력 업체에서 작성 된 구성 요소를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) tooenable software and configuration automation</span></span>
  * <span data-ttu-id="2e1ca-131">[https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="2e1ca-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="2e1ca-132">통신</span><span class="sxs-lookup"><span data-stu-id="2e1ca-132">Communication</span></span>
<span data-ttu-id="2e1ca-133">두 개의 채널을 통해 hello 정보 흐름 hello 플랫폼 toohello 에이전트에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-133">hello information flow from hello platform toohello agent occurs via two channels:</span></span>

* <span data-ttu-id="2e1ca-134">IaaS 배포를 위해 부팅 시 연결된 DVD.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="2e1ca-135">이 DVD hello 실제 SSH 키 쌍 이외의 모든 프로 비전 정보를 포함 하는 규격 OVF 구성 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than hello actual SSH keypairs.</span></span>
* <span data-ttu-id="2e1ca-136">REST API를 노출 하는 TCP 끝점 tooobtain 배포 및 토폴로지 구성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-136">A TCP endpoint exposing a REST API used tooobtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="2e1ca-137">요구 사항</span><span class="sxs-lookup"><span data-stu-id="2e1ca-137">Requirements</span></span>
<span data-ttu-id="2e1ca-138">hello 다음과 같은 시스템 테스트를 거쳐 Azure Linux 에이전트 hello로 toowork 알려진:</span><span class="sxs-lookup"><span data-stu-id="2e1ca-138">hello following systems have been tested and are known toowork with hello Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="2e1ca-139">이 목록은 여기에서 설명한 대로 hello 공식 목록 hello Microsoft Azure 플랫폼에서 지원 되는 시스템에서 달라질 수 있습니다: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="2e1ca-139">This list may differ from hello official list of supported systems on hello Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="2e1ca-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2e1ca-140">CoreOS</span></span>
* <span data-ttu-id="2e1ca-141">CentOS 6.3 이상</span><span class="sxs-lookup"><span data-stu-id="2e1ca-141">CentOS 6.3+</span></span>
* <span data-ttu-id="2e1ca-142">Red Hat Enterprise Linux 6.7 이상</span><span class="sxs-lookup"><span data-stu-id="2e1ca-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="2e1ca-143">Debian 7.0 이상</span><span class="sxs-lookup"><span data-stu-id="2e1ca-143">Debian 7.0+</span></span>
* <span data-ttu-id="2e1ca-144">Ubuntu 12.04 이상</span><span class="sxs-lookup"><span data-stu-id="2e1ca-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="2e1ca-145">openSUSE 12.3 이상</span><span class="sxs-lookup"><span data-stu-id="2e1ca-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="2e1ca-146">SLES 11 SP3 이상</span><span class="sxs-lookup"><span data-stu-id="2e1ca-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="2e1ca-147">Oracle Linux 6.4 이상</span><span class="sxs-lookup"><span data-stu-id="2e1ca-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="2e1ca-148">기타 지원되는 시스템:</span><span class="sxs-lookup"><span data-stu-id="2e1ca-148">Other Supported Systems:</span></span>

* <span data-ttu-id="2e1ca-149">FreeBSD 10 이상(Azure Linux 에이전트 v2.0.10 이상)</span><span class="sxs-lookup"><span data-stu-id="2e1ca-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="2e1ca-150">hello Linux 에이전트 제대로 순서 toofunction에 일부 시스템 패키지에 따라 다릅니다.:</span><span class="sxs-lookup"><span data-stu-id="2e1ca-150">hello Linux agent depends on some system packages in order toofunction properly:</span></span>

* <span data-ttu-id="2e1ca-151">Python 2.6 이상</span><span class="sxs-lookup"><span data-stu-id="2e1ca-151">Python 2.6+</span></span>
* <span data-ttu-id="2e1ca-152">OpenSSL 1.0 이상</span><span class="sxs-lookup"><span data-stu-id="2e1ca-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="2e1ca-153">OpenSSH 5.3 이상</span><span class="sxs-lookup"><span data-stu-id="2e1ca-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="2e1ca-154">파일 시스템 유틸리티: sfdisk, fdisk, mkfs, parted</span><span class="sxs-lookup"><span data-stu-id="2e1ca-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="2e1ca-155">암호 도구: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="2e1ca-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="2e1ca-156">텍스트 처리 도구: sed, grep</span><span class="sxs-lookup"><span data-stu-id="2e1ca-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="2e1ca-157">네트워크 도구: ip-route</span><span class="sxs-lookup"><span data-stu-id="2e1ca-157">Network tools: ip-route</span></span>
* <span data-ttu-id="2e1ca-158">UDF 파일 시스템 탑재에 대한 커널 지원</span><span class="sxs-lookup"><span data-stu-id="2e1ca-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="2e1ca-159">설치</span><span class="sxs-lookup"><span data-stu-id="2e1ca-159">Installation</span></span>
<span data-ttu-id="2e1ca-160">분포의 패키지 저장소는 RPM 또는 DEB 패키지를 사용 하 여 설치는 설치 및 hello Azure Linux 에이전트 업그레이드의 기본 설정 하는 hello 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-160">Installation using an RPM or a DEB package from your distribution's package repository is hello preferred method of installing and upgrading hello Azure Linux Agent.</span></span> <span data-ttu-id="2e1ca-161">모든 hello [배포 공급자 보증](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello Azure Linux 에이전트 패키지를 해당 이미지 및 저장소에 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-161">All hello [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate hello Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="2e1ca-162">Hello에 toohello 문서를 참조 하십시오 [GitHub의 Azure Linux 에이전트 리포지토리](https://github.com/Azure/WALinuxAgent) 소스 또는 toocustom 위치나 접두사에서 설치 하는 등의 고급 설치 옵션에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-162">Refer toohello documentation in hello [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or toocustom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="2e1ca-163">명령줄 옵션</span><span class="sxs-lookup"><span data-stu-id="2e1ca-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="2e1ca-164">플래그</span><span class="sxs-lookup"><span data-stu-id="2e1ca-164">Flags</span></span>
* <span data-ttu-id="2e1ca-165">verbose: 지정한 명령의 세부 정보 표시를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="2e1ca-166">force: 일부 명령의 대화형 확인을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="2e1ca-167">명령</span><span class="sxs-lookup"><span data-stu-id="2e1ca-167">Commands</span></span>
* <span data-ttu-id="2e1ca-168">도움말: hello 지원 명령 및 플래그를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-168">help: Lists hello supported commands and flags.</span></span>
* <span data-ttu-id="2e1ca-169">프로 비전 해제: tooclean hello 시스템을 시도 하 고 다시 프로 비전에 맞게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-169">deprovision: Attempt tooclean hello system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="2e1ca-170">이 작업 hello 다음을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-170">This operation deleted hello following:</span></span>
  
  * <span data-ttu-id="2e1ca-171">모든 SSH 호스트 키 (Provisioning.RegenerateSshHostKeyPair 'y' hello 구성 파일의 경우)</span><span class="sxs-lookup"><span data-stu-id="2e1ca-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="2e1ca-172">/etc/resolv.conf의 Nameserver 구성</span><span class="sxs-lookup"><span data-stu-id="2e1ca-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="2e1ca-173">/Etc/shadow (Provisioning.DeleteRootPassword 'y' hello 구성 파일의 경우)의 루트 암호</span><span class="sxs-lookup"><span data-stu-id="2e1ca-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="2e1ca-174">캐시된 DHCP 클라이언트 임대</span><span class="sxs-lookup"><span data-stu-id="2e1ca-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="2e1ca-175">다시 설정 합니다. 호스트 이름 toolocalhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="2e1ca-175">Resets host name toolocalhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="2e1ca-176">프로 비전 해제 해당 hello 이미지는 중요 한 정보를 모두 선택 취소 하 고 재배포를 위해 적합 한 보장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-176">Deprovisioning does not guarantee that hello image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="2e1ca-177">프로 비전 해제 + 사용자:-프로 비전 해제 (위) 아래에 있는 모든 수행 하 고도 (/var/lib/waagent에서 가져온) hello 마지막 프로 비전 된 사용자 계정을 삭제 하 고 연결 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-177">deprovision+user: Performs everything under -deprovision (above) and also deletes hello last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="2e1ca-178">Azure에서 이전에 프로비전한 이미지의 프로비전을 해제하여 이미지를 캡처하고 다시 사용할 수 있도록 하는 경우에 이 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="2e1ca-179">버전: waagent의 hello 버전을 표시 합니다</span><span class="sxs-lookup"><span data-stu-id="2e1ca-179">version: Displays hello version of waagent</span></span>
* <span data-ttu-id="2e1ca-180">serialconsole: GRUB toomark ttyS0 구성 (첫 번째 직렬 포트 hello) hello 부팅 콘솔로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-180">serialconsole: Configures GRUB toomark ttyS0 (hello first serial port) as hello boot console.</span></span> <span data-ttu-id="2e1ca-181">이렇게 하면 커널 부팅 로그 디버깅에 사용할 수 있는 전송 toothe 직렬 포트를 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-181">This ensures that kernel bootup logs are sent toothe serial port and made available for debugging.</span></span>
* <span data-ttu-id="2e1ca-182">디먼: waagent hello 플랫폼과 상호 작용을 데몬 toomanage로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-182">daemon: Run waagent as a daemon toomanage interaction with hello platform.</span></span> <span data-ttu-id="2e1ca-183">이 인수는 hello waagent init 스크립트에 지정 된 toowaagent입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-183">This argument is specified toowaagent in hello waagent init script.</span></span>
* <span data-ttu-id="2e1ca-184">start: waagent를 백그라운드 프로세스로 실행</span><span class="sxs-lookup"><span data-stu-id="2e1ca-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="2e1ca-185">구성</span><span class="sxs-lookup"><span data-stu-id="2e1ca-185">Configuration</span></span>
<span data-ttu-id="2e1ca-186">구성 파일 (/ etc/waagent.conf) 컨트롤 hello waagent의 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-186">A configuration file (/etc/waagent.conf) controls hello actions of waagent.</span></span> <span data-ttu-id="2e1ca-187">다음은 샘플 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-187">A sample configuration file is shown below:</span></span>

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

<span data-ttu-id="2e1ca-188">hello 다양 한 구성 옵션은 아래에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-188">hello various configuration options are described in detail below.</span></span> <span data-ttu-id="2e1ca-189">구성 옵션으로 부울, 문자열 또는 정수의 세 가지 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="2e1ca-190">"y" 또는 "n"으로 hello 부울 구성 옵션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-190">hello Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="2e1ca-191">안녕 특별 한 키워드 "None" 일부 문자열 형식 구성 항목에 설명 된 대로 아래에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-191">hello special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="2e1ca-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="2e1ca-193">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="2e1ca-193">Type: Boolean</span></span>  
<span data-ttu-id="2e1ca-194">기본값: y</span><span class="sxs-lookup"><span data-stu-id="2e1ca-194">Default: y</span></span>

<span data-ttu-id="2e1ca-195">이 사용자 tooenable hello를 허용 하거나 hello hello 에이전트의 기능을 프로 비전을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-195">This allows hello user tooenable or disable hello provisioning functionality in hello agent.</span></span> <span data-ttu-id="2e1ca-196">유효한 값은 "y" 또는 "n"입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="2e1ca-197">프로 비전을 해제 하면 SSH 호스트 및 사용자 키 hello 이미지에는 유지 하 고 hello Azure 프로 비전 API에에서 지정 된 모든 구성 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-197">If provisioning is disabled, SSH host and user keys in hello image are preserved and any configuration specified in hello Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="2e1ca-198">hello `Provisioning.Enabled` 프로 비전에 대 한 클라우드 초기화를 사용 하는 클라우드 이미지와 Ubuntu 너무 "n" 매개 변수 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-198">hello `Provisioning.Enabled` parameter defaults too"n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="2e1ca-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="2e1ca-200">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="2e1ca-200">Type: Boolean</span></span>  
<span data-ttu-id="2e1ca-201">기본값: n</span><span class="sxs-lookup"><span data-stu-id="2e1ca-201">Default: n</span></span>

<span data-ttu-id="2e1ca-202">Hello/등/섀도 파일에 hello 루트 암호를 설정 하는 동안 지워진 경우 hello 프로 비전 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-202">If set, hello root password in hello /etc/shadow file is erased during hello provisioning process.</span></span>

<span data-ttu-id="2e1ca-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="2e1ca-204">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="2e1ca-204">Type: Boolean</span></span>  
<span data-ttu-id="2e1ca-205">기본값: y</span><span class="sxs-lookup"><span data-stu-id="2e1ca-205">Default: y</span></span>

<span data-ttu-id="2e1ca-206">집합에 모든 SSH 호스트 키 쌍 (예: ecdsa, dsa 및 rsa) 하는 동안 삭제 되 면 hello /etc/ssh/에서 프로 비전 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during hello provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="2e1ca-207">그리고 새로운 단일 키 쌍이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="2e1ca-208">hello 새로운 키 쌍에 대 한 암호화 유형 적용 hello가 hello Provisioning.SshHostKeyPairType 항목 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-208">hello encryption type for hello fresh key pair is configurable by hello Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="2e1ca-209">일부 배포를 다시 만듭니다 누락 된 모든 암호화 종류에 대 한 SSH 키 쌍 (예: 다시 부팅) 시 hello SSH 디먼이 다시 시작 되 면 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when hello SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="2e1ca-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="2e1ca-211">형식: String</span><span class="sxs-lookup"><span data-stu-id="2e1ca-211">Type: String</span></span>  
<span data-ttu-id="2e1ca-212">기본값: rsa</span><span class="sxs-lookup"><span data-stu-id="2e1ca-212">Default: rsa</span></span>

<span data-ttu-id="2e1ca-213">Tooan hello SSH 디먼이 hello 가상 컴퓨터에서 지원 되는 암호화 알고리즘 유형을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-213">This can be set tooan encryption algorithm type that is supported by hello SSH daemon on hello virtual machine.</span></span> <span data-ttu-id="2e1ca-214">일반적으로 지원 되는 hello 값은 "rsa", "dsa" 및 "ecdsa"입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-214">hello typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="2e1ca-215">Windows의 "putty.exe"는 "ecdsa"를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="2e1ca-216">따라서 Windows tooconnect tooa Linux 배포에서 toouse putty.exe 하려는 경우에 사용 하십시오 "rsa" 또는 "dsa".</span><span class="sxs-lookup"><span data-stu-id="2e1ca-216">So, if you intend toouse putty.exe on Windows tooconnect tooa Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="2e1ca-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="2e1ca-218">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="2e1ca-218">Type: Boolean</span></span>  
<span data-ttu-id="2e1ca-219">기본값: y</span><span class="sxs-lookup"><span data-stu-id="2e1ca-219">Default: y</span></span>

<span data-ttu-id="2e1ca-220">집합 경우 waagent 됩니다 (hello "hostname" 명령에서 반환 된)을 호스트 이름 변경에 대 한 hello Linux 가상 컴퓨터를 모니터링할 고 hello 이미지 tooreflect hello 변경에서 네트워킹 구성 hello를 자동으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-220">If set, waagent will monitor hello Linux virtual machine for hostname changes (as returned by hello "hostname" command) and automatically update hello networking configuration in hello image tooreflect hello change.</span></span> <span data-ttu-id="2e1ca-221">순서 toopush hello 이름에서 toohello DNS 서버를 변경, 네트워킹 hello 가상 컴퓨터 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-221">In order toopush hello name change toohello DNS servers, networking will be restarted in hello virtual machine.</span></span> <span data-ttu-id="2e1ca-222">이 때문에 인터넷 연결이 잠시 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="2e1ca-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="2e1ca-224">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="2e1ca-224">Type: Boolean</span></span>  
<span data-ttu-id="2e1ca-225">기본값: n</span><span class="sxs-lookup"><span data-stu-id="2e1ca-225">Default: n</span></span>

<span data-ttu-id="2e1ca-226">설정되면 waagent는 Base64에서 CustomData를 디코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="2e1ca-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="2e1ca-228">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="2e1ca-228">Type: Boolean</span></span>  
<span data-ttu-id="2e1ca-229">기본값: n</span><span class="sxs-lookup"><span data-stu-id="2e1ca-229">Default: n</span></span>

<span data-ttu-id="2e1ca-230">설정되면 waagent는 프로비전 후에 CustomData를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="2e1ca-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="2e1ca-232">형식:String</span><span class="sxs-lookup"><span data-stu-id="2e1ca-232">Type:String</span></span>  
<span data-ttu-id="2e1ca-233">기본값: 6</span><span class="sxs-lookup"><span data-stu-id="2e1ca-233">Default:6</span></span>

<span data-ttu-id="2e1ca-234">암호 해시를 생성할 때 암호화에 사용되는 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="2e1ca-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="2e1ca-235">1 - MD5</span></span>  
 <span data-ttu-id="2e1ca-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="2e1ca-236">2a - Blowfish</span></span>  
 <span data-ttu-id="2e1ca-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="2e1ca-237">5 - SHA-256</span></span>  
 <span data-ttu-id="2e1ca-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="2e1ca-238">6 - SHA-512</span></span>  

<span data-ttu-id="2e1ca-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="2e1ca-240">형식:String</span><span class="sxs-lookup"><span data-stu-id="2e1ca-240">Type:String</span></span>  
<span data-ttu-id="2e1ca-241">기본값: 10</span><span class="sxs-lookup"><span data-stu-id="2e1ca-241">Default:10</span></span>

<span data-ttu-id="2e1ca-242">암호 해시를 생성할 때 사용되는 임의 salt의 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="2e1ca-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="2e1ca-244">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="2e1ca-244">Type: Boolean</span></span>  
<span data-ttu-id="2e1ca-245">기본값: y</span><span class="sxs-lookup"><span data-stu-id="2e1ca-245">Default: y</span></span>

<span data-ttu-id="2e1ca-246">설정, hello 플랫폼에서 제공 하는 hello 리소스 디스크 포맷 하 고 됩니다 "ResourceDisk.Filesystem"에서 hello 사용자가 요청한 hello 파일 시스템 형식 "ntfs" 이외의 값 이면 waagent을 통해 탑재 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-246">If set, hello resource disk provided by hello platform will be formatted and mounted by waagent if hello filesystem type requested by hello user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="2e1ca-247">Linux (83) 형식의 단일 파티션은 사용 가능 하 게 hello 디스크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-247">A single partition of type Linux (83) will be made available on hello disk.</span></span> <span data-ttu-id="2e1ca-248">이 파티션이 탑재될 수 있는 경우에는 포맷되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="2e1ca-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="2e1ca-250">형식: String</span><span class="sxs-lookup"><span data-stu-id="2e1ca-250">Type: String</span></span>  
<span data-ttu-id="2e1ca-251">기본값: ext4</span><span class="sxs-lookup"><span data-stu-id="2e1ca-251">Default: ext4</span></span>

<span data-ttu-id="2e1ca-252">Hello 리소스 디스크에 대 한 hello 파일 시스템 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-252">This specifies hello filesystem type for hello resource disk.</span></span> <span data-ttu-id="2e1ca-253">지원되는 값은 Linux 배포에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="2e1ca-254">Hello 문자열 X, 다음 mkfs 경우. X는 hello Linux 이미지에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-254">If hello string is X, then mkfs.X should be present on hello Linux image.</span></span> <span data-ttu-id="2e1ca-255">일반적으로 SLES 11 이미지는 'ext3'을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="2e1ca-256">여기에서 FreeBSD 이미지는 'ufs2'를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="2e1ca-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="2e1ca-258">형식: String</span><span class="sxs-lookup"><span data-stu-id="2e1ca-258">Type: String</span></span>  
<span data-ttu-id="2e1ca-259">기본값: /mnt/resource</span><span class="sxs-lookup"><span data-stu-id="2e1ca-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="2e1ca-260">Hello 리소스 디스크 탑재 hello 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-260">This specifies hello path at which hello resource disk is mounted.</span></span> <span data-ttu-id="2e1ca-261">해당 하는 hello 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-261">Note that hello resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span>

<span data-ttu-id="2e1ca-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="2e1ca-263">형식: String</span><span class="sxs-lookup"><span data-stu-id="2e1ca-263">Type: String</span></span>  
<span data-ttu-id="2e1ca-264">기본값: 없음</span><span class="sxs-lookup"><span data-stu-id="2e1ca-264">Default: None</span></span>

<span data-ttu-id="2e1ca-265">디스크 탑재 옵션 전달 toobe toohello 탑재-o 명령을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-265">Specifies disk mount options toobe passed toohello mount -o command.</span></span> <span data-ttu-id="2e1ca-266">쉼표로 구분된 값 목록입니다(예:</span><span class="sxs-lookup"><span data-stu-id="2e1ca-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="2e1ca-267">'nodev,nosuid').</span><span class="sxs-lookup"><span data-stu-id="2e1ca-267">'nodev,nosuid'.</span></span> <span data-ttu-id="2e1ca-268">자세한 내용은 mount(8)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-268">See mount(8) for details.</span></span>

<span data-ttu-id="2e1ca-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="2e1ca-270">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="2e1ca-270">Type: Boolean</span></span>  
<span data-ttu-id="2e1ca-271">기본값: n</span><span class="sxs-lookup"><span data-stu-id="2e1ca-271">Default: n</span></span>

<span data-ttu-id="2e1ca-272">경우 설정, 스왑 파일 (/ 스왑 파일) hello 리소스 디스크에 생성 되 고 toohello 시스템 스왑 공간을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-272">If set, a swap file (/swapfile) is created on hello resource disk and added toohello system swap space.</span></span>

<span data-ttu-id="2e1ca-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="2e1ca-274">형식: Integer</span><span class="sxs-lookup"><span data-stu-id="2e1ca-274">Type: Integer</span></span>  
<span data-ttu-id="2e1ca-275">기본값: 0</span><span class="sxs-lookup"><span data-stu-id="2e1ca-275">Default: 0</span></span>

<span data-ttu-id="2e1ca-276">hello 크기 (메가바이트)에서 hello 스왑 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-276">hello size of hello swap file in megabytes.</span></span>

<span data-ttu-id="2e1ca-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="2e1ca-278">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="2e1ca-278">Type: Boolean</span></span>  
<span data-ttu-id="2e1ca-279">기본값: n</span><span class="sxs-lookup"><span data-stu-id="2e1ca-279">Default: n</span></span>

<span data-ttu-id="2e1ca-280">설정한 경우 로그에 대한 세부 정보 표시가 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="2e1ca-281">Waagent은 too/var/log/waagent.log를 로그 및 hello 시스템 logrotate 기능 toorotate 로그를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-281">Waagent logs too/var/log/waagent.log and leverages hello system logrotate functionality toorotate logs.</span></span>

<span data-ttu-id="2e1ca-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="2e1ca-283">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="2e1ca-283">Type: Boolean</span></span>  
<span data-ttu-id="2e1ca-284">기본값: n</span><span class="sxs-lookup"><span data-stu-id="2e1ca-284">Default: n</span></span>

<span data-ttu-id="2e1ca-285">설정, hello 에이전트는 시도 tooinstall 하 고 다음 기반 하드웨어 hello hello 펌웨어 hello 버전과 일치 하는 RDMA 커널 드라이버를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-285">If set, hello agent will attempt tooinstall and then load an RDMA kernel driver that matches hello version of hello firmware on hello underlying hardware.</span></span>

<span data-ttu-id="2e1ca-286">**OS.RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="2e1ca-287">형식: Integer</span><span class="sxs-lookup"><span data-stu-id="2e1ca-287">Type: Integer</span></span>  
<span data-ttu-id="2e1ca-288">기본값: 300</span><span class="sxs-lookup"><span data-stu-id="2e1ca-288">Default: 300</span></span>

<span data-ttu-id="2e1ca-289">Hello SCSI 제한 시간 (초) hello OS 디스크 및 데이터 드라이브에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-289">This configures hello SCSI timeout in seconds on hello OS disk and data drives.</span></span> <span data-ttu-id="2e1ca-290">설정 하지 않으면 hello 시스템 기본값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-290">If not set, hello system defaults are used.</span></span>

<span data-ttu-id="2e1ca-291">**OS.OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="2e1ca-292">형식: String</span><span class="sxs-lookup"><span data-stu-id="2e1ca-292">Type: String</span></span>  
<span data-ttu-id="2e1ca-293">기본값: 없음</span><span class="sxs-lookup"><span data-stu-id="2e1ca-293">Default: None</span></span>

<span data-ttu-id="2e1ca-294">이 사용 되는 toospecify 암호화 작업에 대 한 openssl 이진 toouse hello에 대 한 대체 경로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-294">This can be used toospecify an alternate path for hello openssl binary toouse for cryptographic operations.</span></span>

<span data-ttu-id="2e1ca-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="2e1ca-296">형식: String</span><span class="sxs-lookup"><span data-stu-id="2e1ca-296">Type: String</span></span>  
<span data-ttu-id="2e1ca-297">기본값: 없음</span><span class="sxs-lookup"><span data-stu-id="2e1ca-297">Default: None</span></span>

<span data-ttu-id="2e1ca-298">설정 하면, hello 에이전트는 사용이 프록시 서버 tooaccess hello 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-298">If set, hello agent will use this proxy server tooaccess hello internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="2e1ca-299">Ubuntu 클라우드 이미지</span><span class="sxs-lookup"><span data-stu-id="2e1ca-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="2e1ca-300">Ubuntu 클라우드 이미지를 활용 하는 참고 [클라우드 init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform 그렇지 않으면으로 하 여 관리할 수 있는 많은 구성 작업 hello Azure Linux 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform many configuration tasks that would otherwise be managed by hello Azure Linux Agent.</span></span>  <span data-ttu-id="2e1ca-301">다음 차이점 hello를 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-301">Please note hello following differences:</span></span>

* <span data-ttu-id="2e1ca-302">**Provisioning.Enabled** Ubuntu 클라우드 이미지와 클라우드 init tooperform 작업 프로 비전을 사용 하는 "n" 너무 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-302">**Provisioning.Enabled** defaults too"n" on Ubuntu Cloud Images that use cloud-init tooperform provisioning tasks.</span></span>
* <span data-ttu-id="2e1ca-303">구성 매개 변수 뒤 hello 클라우드 init는 toomanage hello 리소스 디스크 및 스왑 공간을 사용 하는 Ubuntu 클라우드 이미지에 영향을 미치지:</span><span class="sxs-lookup"><span data-stu-id="2e1ca-303">hello following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init toomanage hello resource disk and swap space:</span></span>
  
  * <span data-ttu-id="2e1ca-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="2e1ca-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="2e1ca-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="2e1ca-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="2e1ca-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="2e1ca-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="2e1ca-309">프로 비전 시 스왑 Ubuntu 클라우드 이미지에는 공간 및 hello 리소스 tooconfigure hello 리소스 디스크 탑재 지점를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2e1ca-309">Please see hello following resources tooconfigure hello resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="2e1ca-310">Ubuntu Wiki: Swap 파티션 구성</span><span class="sxs-lookup"><span data-stu-id="2e1ca-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="2e1ca-311">Azure 가상 컴퓨터에 사용자 지정 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="2e1ca-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

