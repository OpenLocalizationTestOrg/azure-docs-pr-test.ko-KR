---
title: "Linux용 사용자 이름 선택 | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터의 사용자 이름을 선택하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 1874d72e5f88816036667932371ff28704d186c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="8a828-103">Azure에서 Linux용 사용자 이름 선택</span><span class="sxs-lookup"><span data-stu-id="8a828-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="8a828-104">Azure에서 Linux 가상 컴퓨터를 프로비전할 때는 나중에 VM 로그인에 사용할 수 있는 루트가 아닌 사용자의 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a828-104">When you provision a Linux virtual machine on Azure you must specify the name of a non-root user that you can later use to log into the VM.</span></span> <span data-ttu-id="8a828-105">새 사용자의 이름을 선택할 수 있습니다. 또는 Azure 클래식 포털을 통해 프로비전하는 경우 기본 이름인 "azureuser"를 사용할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="8a828-105">You may choose the name of the new user, or if provisioning via the Azure classic portal you can accept the default name "azureuser".</span></span>

<span data-ttu-id="8a828-106">대부분의 경우 이러한 사용자는 기본 이미지에 존재하지 않으며 프로비전 프로세스 중에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a828-106">In most cases this user won't exist on the base image and will be created during the provisioning process.</span></span> <span data-ttu-id="8a828-107">사용자가 이미 기본 VM 이미지에 존재하는 경우 Azure Linux 에이전트가 VM을 만들 때 사용자가 지정한 정보를 토대로 해당 사용자에 대한 암호 및/또는 SSH 키를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8a828-107">If the user exists on the base VM image, then the Azure Linux agent simply configures the password and/or SSH key for that user based on the information you specified when creating the VM.</span></span>

<span data-ttu-id="8a828-108">**그러나**Linux에서는 사용해서는 안 되는 일련의 사용자 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8a828-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="8a828-109">UID가 0-99인 사용자로 정의된 기존 시스템 사용자를 사용하여 Linux VM을 프로비전하려고 하면 프로비전 프로세스가 **실패** 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a828-109">The provisioning process will **fail** if you try to provision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="8a828-110">전형적인 예로는 UID가 0인 `root` 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a828-110">A typical example is the `root` user, which has UID 0.</span></span>

* <span data-ttu-id="8a828-111">참고 항목: [Linux 표준 기반 - 사용자 ID 범위](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="8a828-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="8a828-112">다음은 Azure에서 Linux 가상 컴퓨터를 프로비전할 때 사용하지 말아야 할 Ubuntu 및 CentOS에 대한 일반적인 기본 제공 시스템 사용자 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="8a828-112">The following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="8a828-113">이 목록은 예로 든 것일 뿐입니다. 선택한 사용자 이름이 기존 시스템 사용자와 충돌하지 않는지 확인하기 위해 배포에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a828-113">This list is just an example, please refer to the documentation for your distribution to ensure that the username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="8a828-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="8a828-114">CentOS</span></span>
* <span data-ttu-id="8a828-115">abrt</span><span class="sxs-lookup"><span data-stu-id="8a828-115">abrt</span></span>
* <span data-ttu-id="8a828-116">adm</span><span class="sxs-lookup"><span data-stu-id="8a828-116">adm</span></span>
* <span data-ttu-id="8a828-117">audio</span><span class="sxs-lookup"><span data-stu-id="8a828-117">audio</span></span>
* <span data-ttu-id="8a828-118">bin</span><span class="sxs-lookup"><span data-stu-id="8a828-118">bin</span></span>
* <span data-ttu-id="8a828-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="8a828-119">cdrom</span></span>
* <span data-ttu-id="8a828-120">cgred</span><span class="sxs-lookup"><span data-stu-id="8a828-120">cgred</span></span>
* <span data-ttu-id="8a828-121">daemon</span><span class="sxs-lookup"><span data-stu-id="8a828-121">daemon</span></span>
* <span data-ttu-id="8a828-122">dbus</span><span class="sxs-lookup"><span data-stu-id="8a828-122">dbus</span></span>
* <span data-ttu-id="8a828-123">dialout</span><span class="sxs-lookup"><span data-stu-id="8a828-123">dialout</span></span>
* <span data-ttu-id="8a828-124">dip</span><span class="sxs-lookup"><span data-stu-id="8a828-124">dip</span></span>
* <span data-ttu-id="8a828-125">disk</span><span class="sxs-lookup"><span data-stu-id="8a828-125">disk</span></span>
* <span data-ttu-id="8a828-126">floppy</span><span class="sxs-lookup"><span data-stu-id="8a828-126">floppy</span></span>
* <span data-ttu-id="8a828-127">ftp</span><span class="sxs-lookup"><span data-stu-id="8a828-127">ftp</span></span>
* <span data-ttu-id="8a828-128">ftp</span><span class="sxs-lookup"><span data-stu-id="8a828-128">ftp</span></span>
* <span data-ttu-id="8a828-129">games</span><span class="sxs-lookup"><span data-stu-id="8a828-129">games</span></span>
* <span data-ttu-id="8a828-130">gopher</span><span class="sxs-lookup"><span data-stu-id="8a828-130">gopher</span></span>
* <span data-ttu-id="8a828-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="8a828-131">haldaemon</span></span>
* <span data-ttu-id="8a828-132">halt</span><span class="sxs-lookup"><span data-stu-id="8a828-132">halt</span></span>
* <span data-ttu-id="8a828-133">kmem</span><span class="sxs-lookup"><span data-stu-id="8a828-133">kmem</span></span>
* <span data-ttu-id="8a828-134">lock</span><span class="sxs-lookup"><span data-stu-id="8a828-134">lock</span></span>
* <span data-ttu-id="8a828-135">lp</span><span class="sxs-lookup"><span data-stu-id="8a828-135">lp</span></span>
* <span data-ttu-id="8a828-136">mail</span><span class="sxs-lookup"><span data-stu-id="8a828-136">mail</span></span>
* <span data-ttu-id="8a828-137">man</span><span class="sxs-lookup"><span data-stu-id="8a828-137">man</span></span>
* <span data-ttu-id="8a828-138">mem</span><span class="sxs-lookup"><span data-stu-id="8a828-138">mem</span></span>
* <span data-ttu-id="8a828-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="8a828-139">nfsnobody</span></span>
* <span data-ttu-id="8a828-140">nobody</span><span class="sxs-lookup"><span data-stu-id="8a828-140">nobody</span></span>
* <span data-ttu-id="8a828-141">ntp</span><span class="sxs-lookup"><span data-stu-id="8a828-141">ntp</span></span>
* <span data-ttu-id="8a828-142">operator</span><span class="sxs-lookup"><span data-stu-id="8a828-142">operator</span></span>
* <span data-ttu-id="8a828-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="8a828-143">oprofile</span></span>
* <span data-ttu-id="8a828-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="8a828-144">postdrop</span></span>
* <span data-ttu-id="8a828-145">postfix</span><span class="sxs-lookup"><span data-stu-id="8a828-145">postfix</span></span>
* <span data-ttu-id="8a828-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="8a828-146">qpidd</span></span>
* <span data-ttu-id="8a828-147">root</span><span class="sxs-lookup"><span data-stu-id="8a828-147">root</span></span>
* <span data-ttu-id="8a828-148">rpc</span><span class="sxs-lookup"><span data-stu-id="8a828-148">rpc</span></span>
* <span data-ttu-id="8a828-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="8a828-149">rpcuser</span></span>
* <span data-ttu-id="8a828-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="8a828-150">saslauth</span></span>
* <span data-ttu-id="8a828-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="8a828-151">shutdown</span></span>
* <span data-ttu-id="8a828-152">slocate</span><span class="sxs-lookup"><span data-stu-id="8a828-152">slocate</span></span>
* <span data-ttu-id="8a828-153">sshd</span><span class="sxs-lookup"><span data-stu-id="8a828-153">sshd</span></span>
* <span data-ttu-id="8a828-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="8a828-154">stapdev</span></span>
* <span data-ttu-id="8a828-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="8a828-155">stapusr</span></span>
* <span data-ttu-id="8a828-156">sync</span><span class="sxs-lookup"><span data-stu-id="8a828-156">sync</span></span>
* <span data-ttu-id="8a828-157">sys</span><span class="sxs-lookup"><span data-stu-id="8a828-157">sys</span></span>
* <span data-ttu-id="8a828-158">tape</span><span class="sxs-lookup"><span data-stu-id="8a828-158">tape</span></span>
* <span data-ttu-id="8a828-159">test</span><span class="sxs-lookup"><span data-stu-id="8a828-159">test</span></span>
* <span data-ttu-id="8a828-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="8a828-160">tcpdump</span></span>
* <span data-ttu-id="8a828-161">tty</span><span class="sxs-lookup"><span data-stu-id="8a828-161">tty</span></span>
* <span data-ttu-id="8a828-162">users</span><span class="sxs-lookup"><span data-stu-id="8a828-162">users</span></span>
* <span data-ttu-id="8a828-163">utempter</span><span class="sxs-lookup"><span data-stu-id="8a828-163">utempter</span></span>
* <span data-ttu-id="8a828-164">utmp</span><span class="sxs-lookup"><span data-stu-id="8a828-164">utmp</span></span>
* <span data-ttu-id="8a828-165">uucp</span><span class="sxs-lookup"><span data-stu-id="8a828-165">uucp</span></span>
* <span data-ttu-id="8a828-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="8a828-166">vcsa</span></span>
* <span data-ttu-id="8a828-167">video</span><span class="sxs-lookup"><span data-stu-id="8a828-167">video</span></span>
* <span data-ttu-id="8a828-168">wheel</span><span class="sxs-lookup"><span data-stu-id="8a828-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="8a828-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8a828-169">Ubuntu</span></span>
* <span data-ttu-id="8a828-170">adm</span><span class="sxs-lookup"><span data-stu-id="8a828-170">adm</span></span>
* <span data-ttu-id="8a828-171">admin</span><span class="sxs-lookup"><span data-stu-id="8a828-171">admin</span></span>
* <span data-ttu-id="8a828-172">audio</span><span class="sxs-lookup"><span data-stu-id="8a828-172">audio</span></span>
* <span data-ttu-id="8a828-173">backup</span><span class="sxs-lookup"><span data-stu-id="8a828-173">backup</span></span>
* <span data-ttu-id="8a828-174">bin</span><span class="sxs-lookup"><span data-stu-id="8a828-174">bin</span></span>
* <span data-ttu-id="8a828-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="8a828-175">cdrom</span></span>
* <span data-ttu-id="8a828-176">crontab</span><span class="sxs-lookup"><span data-stu-id="8a828-176">crontab</span></span>
* <span data-ttu-id="8a828-177">daemon</span><span class="sxs-lookup"><span data-stu-id="8a828-177">daemon</span></span>
* <span data-ttu-id="8a828-178">dialout</span><span class="sxs-lookup"><span data-stu-id="8a828-178">dialout</span></span>
* <span data-ttu-id="8a828-179">dip</span><span class="sxs-lookup"><span data-stu-id="8a828-179">dip</span></span>
* <span data-ttu-id="8a828-180">disk</span><span class="sxs-lookup"><span data-stu-id="8a828-180">disk</span></span>
* <span data-ttu-id="8a828-181">fax</span><span class="sxs-lookup"><span data-stu-id="8a828-181">fax</span></span>
* <span data-ttu-id="8a828-182">floppy</span><span class="sxs-lookup"><span data-stu-id="8a828-182">floppy</span></span>
* <span data-ttu-id="8a828-183">fuse</span><span class="sxs-lookup"><span data-stu-id="8a828-183">fuse</span></span>
* <span data-ttu-id="8a828-184">games</span><span class="sxs-lookup"><span data-stu-id="8a828-184">games</span></span>
* <span data-ttu-id="8a828-185">gnats</span><span class="sxs-lookup"><span data-stu-id="8a828-185">gnats</span></span>
* <span data-ttu-id="8a828-186">irc</span><span class="sxs-lookup"><span data-stu-id="8a828-186">irc</span></span>
* <span data-ttu-id="8a828-187">kmem</span><span class="sxs-lookup"><span data-stu-id="8a828-187">kmem</span></span>
* <span data-ttu-id="8a828-188">landscape</span><span class="sxs-lookup"><span data-stu-id="8a828-188">landscape</span></span>
* <span data-ttu-id="8a828-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="8a828-189">libuuid</span></span>
* <span data-ttu-id="8a828-190">list</span><span class="sxs-lookup"><span data-stu-id="8a828-190">list</span></span>
* <span data-ttu-id="8a828-191">lp</span><span class="sxs-lookup"><span data-stu-id="8a828-191">lp</span></span>
* <span data-ttu-id="8a828-192">mail</span><span class="sxs-lookup"><span data-stu-id="8a828-192">mail</span></span>
* <span data-ttu-id="8a828-193">man</span><span class="sxs-lookup"><span data-stu-id="8a828-193">man</span></span>
* <span data-ttu-id="8a828-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="8a828-194">messagebus</span></span>
* <span data-ttu-id="8a828-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="8a828-195">mlocate</span></span>
* <span data-ttu-id="8a828-196">netdev</span><span class="sxs-lookup"><span data-stu-id="8a828-196">netdev</span></span>
* <span data-ttu-id="8a828-197">news</span><span class="sxs-lookup"><span data-stu-id="8a828-197">news</span></span>
* <span data-ttu-id="8a828-198">nobody</span><span class="sxs-lookup"><span data-stu-id="8a828-198">nobody</span></span>
* <span data-ttu-id="8a828-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="8a828-199">nogroup</span></span>
* <span data-ttu-id="8a828-200">operator</span><span class="sxs-lookup"><span data-stu-id="8a828-200">operator</span></span>
* <span data-ttu-id="8a828-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="8a828-201">plugdev</span></span>
* <span data-ttu-id="8a828-202">proxy</span><span class="sxs-lookup"><span data-stu-id="8a828-202">proxy</span></span>
* <span data-ttu-id="8a828-203">root</span><span class="sxs-lookup"><span data-stu-id="8a828-203">root</span></span>
* <span data-ttu-id="8a828-204">sasl</span><span class="sxs-lookup"><span data-stu-id="8a828-204">sasl</span></span>
* <span data-ttu-id="8a828-205">shadow</span><span class="sxs-lookup"><span data-stu-id="8a828-205">shadow</span></span>
* <span data-ttu-id="8a828-206">src</span><span class="sxs-lookup"><span data-stu-id="8a828-206">src</span></span>
* <span data-ttu-id="8a828-207">ssh</span><span class="sxs-lookup"><span data-stu-id="8a828-207">ssh</span></span>
* <span data-ttu-id="8a828-208">sshd</span><span class="sxs-lookup"><span data-stu-id="8a828-208">sshd</span></span>
* <span data-ttu-id="8a828-209">staff</span><span class="sxs-lookup"><span data-stu-id="8a828-209">staff</span></span>
* <span data-ttu-id="8a828-210">sudo</span><span class="sxs-lookup"><span data-stu-id="8a828-210">sudo</span></span>
* <span data-ttu-id="8a828-211">sync</span><span class="sxs-lookup"><span data-stu-id="8a828-211">sync</span></span>
* <span data-ttu-id="8a828-212">sys</span><span class="sxs-lookup"><span data-stu-id="8a828-212">sys</span></span>
* <span data-ttu-id="8a828-213">syslog</span><span class="sxs-lookup"><span data-stu-id="8a828-213">syslog</span></span>
* <span data-ttu-id="8a828-214">tape</span><span class="sxs-lookup"><span data-stu-id="8a828-214">tape</span></span>
* <span data-ttu-id="8a828-215">tty</span><span class="sxs-lookup"><span data-stu-id="8a828-215">tty</span></span>
* <span data-ttu-id="8a828-216">users</span><span class="sxs-lookup"><span data-stu-id="8a828-216">users</span></span>
* <span data-ttu-id="8a828-217">utmp</span><span class="sxs-lookup"><span data-stu-id="8a828-217">utmp</span></span>
* <span data-ttu-id="8a828-218">uucp</span><span class="sxs-lookup"><span data-stu-id="8a828-218">uucp</span></span>
* <span data-ttu-id="8a828-219">video</span><span class="sxs-lookup"><span data-stu-id="8a828-219">video</span></span>
* <span data-ttu-id="8a828-220">voice</span><span class="sxs-lookup"><span data-stu-id="8a828-220">voice</span></span>
* <span data-ttu-id="8a828-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="8a828-221">whoopsie</span></span>
* <span data-ttu-id="8a828-222">www-data</span><span class="sxs-lookup"><span data-stu-id="8a828-222">www-data</span></span>

