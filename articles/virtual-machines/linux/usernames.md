---
title: "aaaSelecting Linux에 대 한 사용자 이름 | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터에 대 한 tooselect 사용자 이름을 지정 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="cd73f-103">Azure에서 Linux용 사용자 이름 선택</span><span class="sxs-lookup"><span data-stu-id="cd73f-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="cd73f-104">Azure에서 Linux 가상 컴퓨터를 프로 비전 할 때 toolog hello VM에 나중에 사용할 수 있는 루트가 아닌 사용자의 hello 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd73f-104">When you provision a Linux virtual machine on Azure you must specify hello name of a non-root user that you can later use toolog into hello VM.</span></span> <span data-ttu-id="cd73f-105">Hello 새 사용자의 hello 이름을 선택할 수 있습니다 또는 경우 Azure 클래식 포털 hello를 통한 프로비저닝 그대로 hello 기본 이름 "azureuser"입니다.</span><span class="sxs-lookup"><span data-stu-id="cd73f-105">You may choose hello name of hello new user, or if provisioning via hello Azure classic portal you can accept hello default name "azureuser".</span></span>

<span data-ttu-id="cd73f-106">대부분의 경우에서이 사용자 hello 기본 이미지에 존재 하지 않습니다 및 hello를 프로 비전 프로세스 중 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd73f-106">In most cases this user won't exist on hello base image and will be created during hello provisioning process.</span></span> <span data-ttu-id="cd73f-107">Hello 사용자에 있으면 기본 VM 이미지 hello 다음 hello Azure Linux 에이전트 단순히 hello 암호 및/또는 hello VM을 만들 때 지정한 hello 정보에 따라 해당 사용자에 대 한 SSH 키를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd73f-107">If hello user exists on hello base VM image, then hello Azure Linux agent simply configures hello password and/or SSH key for that user based on hello information you specified when creating hello VM.</span></span>

<span data-ttu-id="cd73f-108">**그러나**Linux에서는 사용해서는 안 되는 일련의 사용자 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cd73f-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="cd73f-109">프로세스는 프로 비전 하는 hello **실패** tooprovision UID 0에서 99 있는 사용자로 정의 된 기존 시스템 사용자를 사용 하 여 Linux VM을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd73f-109">hello provisioning process will **fail** if you try tooprovision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="cd73f-110">일반적인 예로 hello `root` UID 0에는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="cd73f-110">A typical example is hello `root` user, which has UID 0.</span></span>

* <span data-ttu-id="cd73f-111">참고 항목: [Linux 표준 기반 - 사용자 ID 범위](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="cd73f-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="cd73f-112">hello 다음은 일반적인 기본 제공 시스템에 대 한 사용자 CentOS 및을 사용 하면 안 Azure에서 Linux 가상 컴퓨터를 프로 비전 할 때 Ubuntu 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cd73f-112">hello following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="cd73f-113">이 목록은 예 시일 뿐에 toohello 설명서를 참조 배포 tooensure 해당 hello 사용자 이름을 기존 시스템 사용자와 충돌 하지 않는지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd73f-113">This list is just an example, please refer toohello documentation for your distribution tooensure that hello username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="cd73f-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="cd73f-114">CentOS</span></span>
* <span data-ttu-id="cd73f-115">abrt</span><span class="sxs-lookup"><span data-stu-id="cd73f-115">abrt</span></span>
* <span data-ttu-id="cd73f-116">adm</span><span class="sxs-lookup"><span data-stu-id="cd73f-116">adm</span></span>
* <span data-ttu-id="cd73f-117">audio</span><span class="sxs-lookup"><span data-stu-id="cd73f-117">audio</span></span>
* <span data-ttu-id="cd73f-118">bin</span><span class="sxs-lookup"><span data-stu-id="cd73f-118">bin</span></span>
* <span data-ttu-id="cd73f-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="cd73f-119">cdrom</span></span>
* <span data-ttu-id="cd73f-120">cgred</span><span class="sxs-lookup"><span data-stu-id="cd73f-120">cgred</span></span>
* <span data-ttu-id="cd73f-121">daemon</span><span class="sxs-lookup"><span data-stu-id="cd73f-121">daemon</span></span>
* <span data-ttu-id="cd73f-122">dbus</span><span class="sxs-lookup"><span data-stu-id="cd73f-122">dbus</span></span>
* <span data-ttu-id="cd73f-123">dialout</span><span class="sxs-lookup"><span data-stu-id="cd73f-123">dialout</span></span>
* <span data-ttu-id="cd73f-124">dip</span><span class="sxs-lookup"><span data-stu-id="cd73f-124">dip</span></span>
* <span data-ttu-id="cd73f-125">disk</span><span class="sxs-lookup"><span data-stu-id="cd73f-125">disk</span></span>
* <span data-ttu-id="cd73f-126">floppy</span><span class="sxs-lookup"><span data-stu-id="cd73f-126">floppy</span></span>
* <span data-ttu-id="cd73f-127">ftp</span><span class="sxs-lookup"><span data-stu-id="cd73f-127">ftp</span></span>
* <span data-ttu-id="cd73f-128">ftp</span><span class="sxs-lookup"><span data-stu-id="cd73f-128">ftp</span></span>
* <span data-ttu-id="cd73f-129">games</span><span class="sxs-lookup"><span data-stu-id="cd73f-129">games</span></span>
* <span data-ttu-id="cd73f-130">gopher</span><span class="sxs-lookup"><span data-stu-id="cd73f-130">gopher</span></span>
* <span data-ttu-id="cd73f-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="cd73f-131">haldaemon</span></span>
* <span data-ttu-id="cd73f-132">halt</span><span class="sxs-lookup"><span data-stu-id="cd73f-132">halt</span></span>
* <span data-ttu-id="cd73f-133">kmem</span><span class="sxs-lookup"><span data-stu-id="cd73f-133">kmem</span></span>
* <span data-ttu-id="cd73f-134">lock</span><span class="sxs-lookup"><span data-stu-id="cd73f-134">lock</span></span>
* <span data-ttu-id="cd73f-135">lp</span><span class="sxs-lookup"><span data-stu-id="cd73f-135">lp</span></span>
* <span data-ttu-id="cd73f-136">mail</span><span class="sxs-lookup"><span data-stu-id="cd73f-136">mail</span></span>
* <span data-ttu-id="cd73f-137">man</span><span class="sxs-lookup"><span data-stu-id="cd73f-137">man</span></span>
* <span data-ttu-id="cd73f-138">mem</span><span class="sxs-lookup"><span data-stu-id="cd73f-138">mem</span></span>
* <span data-ttu-id="cd73f-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="cd73f-139">nfsnobody</span></span>
* <span data-ttu-id="cd73f-140">nobody</span><span class="sxs-lookup"><span data-stu-id="cd73f-140">nobody</span></span>
* <span data-ttu-id="cd73f-141">ntp</span><span class="sxs-lookup"><span data-stu-id="cd73f-141">ntp</span></span>
* <span data-ttu-id="cd73f-142">operator</span><span class="sxs-lookup"><span data-stu-id="cd73f-142">operator</span></span>
* <span data-ttu-id="cd73f-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="cd73f-143">oprofile</span></span>
* <span data-ttu-id="cd73f-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="cd73f-144">postdrop</span></span>
* <span data-ttu-id="cd73f-145">postfix</span><span class="sxs-lookup"><span data-stu-id="cd73f-145">postfix</span></span>
* <span data-ttu-id="cd73f-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="cd73f-146">qpidd</span></span>
* <span data-ttu-id="cd73f-147">root</span><span class="sxs-lookup"><span data-stu-id="cd73f-147">root</span></span>
* <span data-ttu-id="cd73f-148">rpc</span><span class="sxs-lookup"><span data-stu-id="cd73f-148">rpc</span></span>
* <span data-ttu-id="cd73f-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="cd73f-149">rpcuser</span></span>
* <span data-ttu-id="cd73f-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="cd73f-150">saslauth</span></span>
* <span data-ttu-id="cd73f-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="cd73f-151">shutdown</span></span>
* <span data-ttu-id="cd73f-152">slocate</span><span class="sxs-lookup"><span data-stu-id="cd73f-152">slocate</span></span>
* <span data-ttu-id="cd73f-153">sshd</span><span class="sxs-lookup"><span data-stu-id="cd73f-153">sshd</span></span>
* <span data-ttu-id="cd73f-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="cd73f-154">stapdev</span></span>
* <span data-ttu-id="cd73f-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="cd73f-155">stapusr</span></span>
* <span data-ttu-id="cd73f-156">sync</span><span class="sxs-lookup"><span data-stu-id="cd73f-156">sync</span></span>
* <span data-ttu-id="cd73f-157">sys</span><span class="sxs-lookup"><span data-stu-id="cd73f-157">sys</span></span>
* <span data-ttu-id="cd73f-158">tape</span><span class="sxs-lookup"><span data-stu-id="cd73f-158">tape</span></span>
* <span data-ttu-id="cd73f-159">test</span><span class="sxs-lookup"><span data-stu-id="cd73f-159">test</span></span>
* <span data-ttu-id="cd73f-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="cd73f-160">tcpdump</span></span>
* <span data-ttu-id="cd73f-161">tty</span><span class="sxs-lookup"><span data-stu-id="cd73f-161">tty</span></span>
* <span data-ttu-id="cd73f-162">users</span><span class="sxs-lookup"><span data-stu-id="cd73f-162">users</span></span>
* <span data-ttu-id="cd73f-163">utempter</span><span class="sxs-lookup"><span data-stu-id="cd73f-163">utempter</span></span>
* <span data-ttu-id="cd73f-164">utmp</span><span class="sxs-lookup"><span data-stu-id="cd73f-164">utmp</span></span>
* <span data-ttu-id="cd73f-165">uucp</span><span class="sxs-lookup"><span data-stu-id="cd73f-165">uucp</span></span>
* <span data-ttu-id="cd73f-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="cd73f-166">vcsa</span></span>
* <span data-ttu-id="cd73f-167">video</span><span class="sxs-lookup"><span data-stu-id="cd73f-167">video</span></span>
* <span data-ttu-id="cd73f-168">wheel</span><span class="sxs-lookup"><span data-stu-id="cd73f-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="cd73f-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cd73f-169">Ubuntu</span></span>
* <span data-ttu-id="cd73f-170">adm</span><span class="sxs-lookup"><span data-stu-id="cd73f-170">adm</span></span>
* <span data-ttu-id="cd73f-171">admin</span><span class="sxs-lookup"><span data-stu-id="cd73f-171">admin</span></span>
* <span data-ttu-id="cd73f-172">audio</span><span class="sxs-lookup"><span data-stu-id="cd73f-172">audio</span></span>
* <span data-ttu-id="cd73f-173">backup</span><span class="sxs-lookup"><span data-stu-id="cd73f-173">backup</span></span>
* <span data-ttu-id="cd73f-174">bin</span><span class="sxs-lookup"><span data-stu-id="cd73f-174">bin</span></span>
* <span data-ttu-id="cd73f-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="cd73f-175">cdrom</span></span>
* <span data-ttu-id="cd73f-176">crontab</span><span class="sxs-lookup"><span data-stu-id="cd73f-176">crontab</span></span>
* <span data-ttu-id="cd73f-177">daemon</span><span class="sxs-lookup"><span data-stu-id="cd73f-177">daemon</span></span>
* <span data-ttu-id="cd73f-178">dialout</span><span class="sxs-lookup"><span data-stu-id="cd73f-178">dialout</span></span>
* <span data-ttu-id="cd73f-179">dip</span><span class="sxs-lookup"><span data-stu-id="cd73f-179">dip</span></span>
* <span data-ttu-id="cd73f-180">disk</span><span class="sxs-lookup"><span data-stu-id="cd73f-180">disk</span></span>
* <span data-ttu-id="cd73f-181">fax</span><span class="sxs-lookup"><span data-stu-id="cd73f-181">fax</span></span>
* <span data-ttu-id="cd73f-182">floppy</span><span class="sxs-lookup"><span data-stu-id="cd73f-182">floppy</span></span>
* <span data-ttu-id="cd73f-183">fuse</span><span class="sxs-lookup"><span data-stu-id="cd73f-183">fuse</span></span>
* <span data-ttu-id="cd73f-184">games</span><span class="sxs-lookup"><span data-stu-id="cd73f-184">games</span></span>
* <span data-ttu-id="cd73f-185">gnats</span><span class="sxs-lookup"><span data-stu-id="cd73f-185">gnats</span></span>
* <span data-ttu-id="cd73f-186">irc</span><span class="sxs-lookup"><span data-stu-id="cd73f-186">irc</span></span>
* <span data-ttu-id="cd73f-187">kmem</span><span class="sxs-lookup"><span data-stu-id="cd73f-187">kmem</span></span>
* <span data-ttu-id="cd73f-188">landscape</span><span class="sxs-lookup"><span data-stu-id="cd73f-188">landscape</span></span>
* <span data-ttu-id="cd73f-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="cd73f-189">libuuid</span></span>
* <span data-ttu-id="cd73f-190">list</span><span class="sxs-lookup"><span data-stu-id="cd73f-190">list</span></span>
* <span data-ttu-id="cd73f-191">lp</span><span class="sxs-lookup"><span data-stu-id="cd73f-191">lp</span></span>
* <span data-ttu-id="cd73f-192">mail</span><span class="sxs-lookup"><span data-stu-id="cd73f-192">mail</span></span>
* <span data-ttu-id="cd73f-193">man</span><span class="sxs-lookup"><span data-stu-id="cd73f-193">man</span></span>
* <span data-ttu-id="cd73f-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="cd73f-194">messagebus</span></span>
* <span data-ttu-id="cd73f-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="cd73f-195">mlocate</span></span>
* <span data-ttu-id="cd73f-196">netdev</span><span class="sxs-lookup"><span data-stu-id="cd73f-196">netdev</span></span>
* <span data-ttu-id="cd73f-197">news</span><span class="sxs-lookup"><span data-stu-id="cd73f-197">news</span></span>
* <span data-ttu-id="cd73f-198">nobody</span><span class="sxs-lookup"><span data-stu-id="cd73f-198">nobody</span></span>
* <span data-ttu-id="cd73f-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="cd73f-199">nogroup</span></span>
* <span data-ttu-id="cd73f-200">operator</span><span class="sxs-lookup"><span data-stu-id="cd73f-200">operator</span></span>
* <span data-ttu-id="cd73f-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="cd73f-201">plugdev</span></span>
* <span data-ttu-id="cd73f-202">proxy</span><span class="sxs-lookup"><span data-stu-id="cd73f-202">proxy</span></span>
* <span data-ttu-id="cd73f-203">root</span><span class="sxs-lookup"><span data-stu-id="cd73f-203">root</span></span>
* <span data-ttu-id="cd73f-204">sasl</span><span class="sxs-lookup"><span data-stu-id="cd73f-204">sasl</span></span>
* <span data-ttu-id="cd73f-205">shadow</span><span class="sxs-lookup"><span data-stu-id="cd73f-205">shadow</span></span>
* <span data-ttu-id="cd73f-206">src</span><span class="sxs-lookup"><span data-stu-id="cd73f-206">src</span></span>
* <span data-ttu-id="cd73f-207">ssh</span><span class="sxs-lookup"><span data-stu-id="cd73f-207">ssh</span></span>
* <span data-ttu-id="cd73f-208">sshd</span><span class="sxs-lookup"><span data-stu-id="cd73f-208">sshd</span></span>
* <span data-ttu-id="cd73f-209">staff</span><span class="sxs-lookup"><span data-stu-id="cd73f-209">staff</span></span>
* <span data-ttu-id="cd73f-210">sudo</span><span class="sxs-lookup"><span data-stu-id="cd73f-210">sudo</span></span>
* <span data-ttu-id="cd73f-211">sync</span><span class="sxs-lookup"><span data-stu-id="cd73f-211">sync</span></span>
* <span data-ttu-id="cd73f-212">sys</span><span class="sxs-lookup"><span data-stu-id="cd73f-212">sys</span></span>
* <span data-ttu-id="cd73f-213">syslog</span><span class="sxs-lookup"><span data-stu-id="cd73f-213">syslog</span></span>
* <span data-ttu-id="cd73f-214">tape</span><span class="sxs-lookup"><span data-stu-id="cd73f-214">tape</span></span>
* <span data-ttu-id="cd73f-215">tty</span><span class="sxs-lookup"><span data-stu-id="cd73f-215">tty</span></span>
* <span data-ttu-id="cd73f-216">users</span><span class="sxs-lookup"><span data-stu-id="cd73f-216">users</span></span>
* <span data-ttu-id="cd73f-217">utmp</span><span class="sxs-lookup"><span data-stu-id="cd73f-217">utmp</span></span>
* <span data-ttu-id="cd73f-218">uucp</span><span class="sxs-lookup"><span data-stu-id="cd73f-218">uucp</span></span>
* <span data-ttu-id="cd73f-219">video</span><span class="sxs-lookup"><span data-stu-id="cd73f-219">video</span></span>
* <span data-ttu-id="cd73f-220">voice</span><span class="sxs-lookup"><span data-stu-id="cd73f-220">voice</span></span>
* <span data-ttu-id="cd73f-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="cd73f-221">whoopsie</span></span>
* <span data-ttu-id="cd73f-222">www-data</span><span class="sxs-lookup"><span data-stu-id="cd73f-222">www-data</span></span>

