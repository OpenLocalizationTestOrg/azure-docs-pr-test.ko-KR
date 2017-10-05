---
title: "Azure VM에 대한 특정 RDP 오류 메시지 | Microsoft Docs"
description: "Azure에서 Windows 가상 컴퓨터에 원격 데스크톱 연결을 시도할 때 나타날 수 있는 특정 오류 메시지를 이해합니다."
keywords: "원격 데스크톱 오류,원격 데스크톱 연결 오류,VM에 연결할 수 없습니다,원격 데스크톱 문제 해결"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: e7c049106726a15e96d4ebe7c7c0388a29c546c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-to-a-windows-vm-in-azure"></a><span data-ttu-id="fe13f-104">Azure에서 Windows VM에 대한 특정 RDP 오류 메시지 문제 해결</span><span class="sxs-lookup"><span data-stu-id="fe13f-104">Troubleshooting specific RDP error messages to a Windows VM in Azure</span></span>
<span data-ttu-id="fe13f-105">Azure에서 Windows 가상 컴퓨터(VM)에 원격 데스크톱 연결을 사용할 때 특정 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-105">You may receive a specific error message when using Remote Desktop connection to a Windows virtual machine (VM) in Azure.</span></span> <span data-ttu-id="fe13f-106">이 문서에서는 발생할 수 있는 일반적인 일부 오류 메시지와 이 문제를 해결하기 위한 문제 해결 단계에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-106">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span> <span data-ttu-id="fe13f-107">RDP를 사용하여 VM에 연결하는 데 문제가 있지만 특정 오류 메시지가 발생하지 않는다면 [원격 데스크톱에 대한 자세한 문제 해결 가이드](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe13f-107">If you are having issues connecting to your VM using RDP but do not encounter a specific error message, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="fe13f-108">특정 오류 메시지에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe13f-108">For information on specific error messages, see the following:</span></span>

* <span data-ttu-id="fe13f-109">[라이선스를 제공할 수 있는 원격 데스크톱 라이선스 서버가 없으므로 원격 세션이 끊겼습니다](#rdplicense).</span><span class="sxs-lookup"><span data-stu-id="fe13f-109">[The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license](#rdplicense).</span></span>
* <span data-ttu-id="fe13f-110">[원격 데스크톱에서 컴퓨터 "이름"을 찾을 수 없습니다](#rdpname).</span><span class="sxs-lookup"><span data-stu-id="fe13f-110">[Remote Desktop can't find the computer "name"](#rdpname).</span></span>
* <span data-ttu-id="fe13f-111">[인증 오류가 발생했습니다. 로컬 보안 기관에 연결할 수 없습니다.](#rdpauth)</span><span class="sxs-lookup"><span data-stu-id="fe13f-111">[An authentication error has occurred. The Local Security Authority cannot be contacted](#rdpauth).</span></span>
* <span data-ttu-id="fe13f-112">[Windows 보안 오류: 자격 증명이 작동하지 않습니다](#wincred).</span><span class="sxs-lookup"><span data-stu-id="fe13f-112">[Windows Security error: Your credentials did not work](#wincred).</span></span>
* <span data-ttu-id="fe13f-113">[이 컴퓨터에서 원격 컴퓨터에 연결할 수 없습니다](#rdpconnect).</span><span class="sxs-lookup"><span data-stu-id="fe13f-113">[This computer can't connect to the remote computer](#rdpconnect).</span></span>

<a id="rdplicense"></a>

## <a name="the-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-to-provide-a-license"></a><span data-ttu-id="fe13f-114">라이선스를 제공할 수 있는 원격 데스크톱 라이선스 서버가 없으므로 원격 세션이 끊겼습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-114">The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license.</span></span>
<span data-ttu-id="fe13f-115">원인: 원격 데스크톱 서버 역할에 대한 120일 라이선스 유예 기간이 만료되었고 라이선스를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-115">Cause: The 120-day licensing grace period for the Remote Desktop Server role has expired and you need to install licenses.</span></span>

<span data-ttu-id="fe13f-116">대안으로 포털에서 RDP 파일의 로컬 복사본을 저장하고 PowerShell 명령 프롬프트에서 이 명령을 실행하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-116">As a workaround, save a local copy of the RDP file from the portal and run this command at a PowerShell command prompt to connect.</span></span> <span data-ttu-id="fe13f-117">이 단계를 따르면 해당 연결에만 라이선스를 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-117">This step disables licensing for just that connection:</span></span>

        mstsc <File name>.RDP /admin

<span data-ttu-id="fe13f-118">VM에 실제로 두 개 이상의 동시 원격 데스크톱 연결이 필요하지 않을 경우 서버 관리자를 사용하여 원격 데스크톱 서버 역할을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-118">If you don't actually need more than two simultaneous Remote Desktop connections to the VM, you can use Server Manager to remove the Remote Desktop Server role.</span></span>

<span data-ttu-id="fe13f-119">자세한 내용은 ["사용 가능한 원격 데스크톱 라이선스 서버가 없음"과 함께 Azure VM이 실패하는 경우](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/)블로그 게시물을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe13f-119">For more information, see the blog post [Azure VM fails with "No Remote Desktop License Servers available"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span></span>

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-the-computer-name"></a><span data-ttu-id="fe13f-120">원격 데스크톱에서 컴퓨터 "name"을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-120">Remote Desktop can't find the computer "name".</span></span>
<span data-ttu-id="fe13f-121">원인: 컴퓨터의 원격 데스크톱 클라이언트가 RDP 파일의 설정에 있는 컴퓨터의 이름을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-121">Cause: The Remote Desktop client on your computer can't resolve the name of the computer in the settings of the RDP file.</span></span>

<span data-ttu-id="fe13f-122">가능한 해결 방법:</span><span class="sxs-lookup"><span data-stu-id="fe13f-122">Possible solutions:</span></span>

* <span data-ttu-id="fe13f-123">조직 인트라넷을 사용하는 경우 컴퓨터가 프록시 서버에 액세스할 수 있고 HTTPS 트래픽을 보낼 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-123">If you're on an organization's intranet, make sure that your computer has access to the proxy server and can send HTTPS traffic to it.</span></span>
* <span data-ttu-id="fe13f-124">로컬 컴퓨터에 저장된 RDP 파일을 사용하는 경우 포털에서 생성한 파일을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="fe13f-124">If you're using a locally stored RDP file, try using the one that's generated by the portal.</span></span> <span data-ttu-id="fe13f-125">이 단계에서는 가상 컴퓨터 또는 클라우드 서비스 및 VM의 끝점 포트에 대한 올바른 DNS 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-125">This step ensures that you have the correct DNS name for the virtual machine, or the cloud service and the endpoint port of the VM.</span></span> <span data-ttu-id="fe13f-126">포털에서 생성된 RDP 파일의 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-126">Here is a sample RDP file generated by the portal:</span></span>
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

<span data-ttu-id="fe13f-127">이 RDP 파일의 주소 부분에는</span><span class="sxs-lookup"><span data-stu-id="fe13f-127">The address portion of this RDP file has:</span></span>

* <span data-ttu-id="fe13f-128">VM을 포함하는 클라우드 서비스의 정규화된 도메인 이름(이 예제에서는 "tailspin azdatatier.cloudapp.net")이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-128">The fully qualified domain name of the cloud service that contains the VM ("tailspin-azdatatier.cloudapp.net" in this example).</span></span>
* <span data-ttu-id="fe13f-129">원격 데스크톱 트래픽에 대한 끝점의 외부 TCP 포트(55919)</span><span class="sxs-lookup"><span data-stu-id="fe13f-129">The external TCP port of the endpoint for Remote Desktop traffic (55919).</span></span>

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-the-local-security-authority-cannot-be-contacted"></a><span data-ttu-id="fe13f-130">인증 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-130">An authentication error has occurred.</span></span> <span data-ttu-id="fe13f-131">로컬 보안 기관에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-131">The Local Security Authority cannot be contacted.</span></span>
<span data-ttu-id="fe13f-132">원인: 대상 VM이 사용자의 자격 증명의 사용자 이름 부분에서 보안 기관을 찾지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-132">Cause: The target VM can't locate the security authority in the user name portion of your credentials.</span></span>

<span data-ttu-id="fe13f-133">사용자 이름이 *SecurityAuthority*\\*UserName*(예: CORP\User1) 형식인 경우 *SecurityAuthority* 부분은 VM의 컴퓨터 이름(로컬 보안 기관)이거나 Active Directory 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-133">When your user name is in the form *SecurityAuthority*\\*UserName* (example: CORP\User1), the *SecurityAuthority* portion is either the VM's computer name (for the local security authority) or an Active Directory domain name.</span></span>

<span data-ttu-id="fe13f-134">가능한 해결 방법:</span><span class="sxs-lookup"><span data-stu-id="fe13f-134">Possible solutions:</span></span>

* <span data-ttu-id="fe13f-135">계정이 VM의 로컬 계정인 경우 VM 이름의 철자가 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-135">If the account is local to the VM, make sure that the VM name is spelled correctly.</span></span>
* <span data-ttu-id="fe13f-136">계정이 Active Directory 도메인에 있는 경우 도메인 이름의 철자를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-136">If the account is on an Active Directory domain, check the spelling of the domain name.</span></span>
* <span data-ttu-id="fe13f-137">사용자 계정이 Active Directory 도메인 계정이고 해당 도메인 이름 철자가 올바르게 입력된 경우, 해당 도메인에서 도메인 컨트롤러를 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-137">If it is an Active Directory domain account and the domain name is spelled correctly, verify that a domain controller is available in that domain.</span></span> <span data-ttu-id="fe13f-138">도메인 컨트롤러가 시작되지 않았기 때문에 사용할 수 없는 것은 도메인 컨트롤러가 포함된 Azure 가상 네트워크에서 일반적인 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-138">It's a common issue in Azure virtual networks that contain domain controllers that a domain controller is unavailable because it hasn't been started.</span></span> <span data-ttu-id="fe13f-139">해결 방법으로 도메인 계정 대신 로컬 관리자 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-139">As a workaround, you can use a local administrator account instead of a domain account.</span></span>

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a><span data-ttu-id="fe13f-140">Windows 보안 오류: 자격 증명이 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-140">Windows Security error: Your credentials did not work.</span></span>
<span data-ttu-id="fe13f-141">원인: 대상 VM에서 계정 이름 및 암호의 유효성을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-141">Cause: The target VM can't validate your account name and password.</span></span>

<span data-ttu-id="fe13f-142">Windows 기반 컴퓨터는 로컬 계정 또는 도메인 계정 자격 증명의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-142">A Windows-based computer can validate the credentials of either a local account or a domain account.</span></span>

* <span data-ttu-id="fe13f-143">로컬 계정의 경우 *ComputerName*\\*UserName* 구문(예: SQL1\Admin4798)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-143">For local accounts, use the *ComputerName*\\*UserName* syntax (example: SQL1\Admin4798).</span></span>
* <span data-ttu-id="fe13f-144">도메인 계정의 경우 *DomainName*\\*UserName* 구문(예: CONTOSO\peterodman)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-144">For domain accounts, use the *DomainName*\\*UserName* syntax (example: CONTOSO\peterodman).</span></span>

<span data-ttu-id="fe13f-145">VM을 새 Active Directory 포리스트의 도메인 컨트롤러로 승격한 경우 사용자가 로그인할 때 사용한 로컬 관리자 계정이 새 포리스트 및 도메인과 같은 암호를 가진 동일한 계정으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-145">If you have promoted your VM to a domain controller in a new Active Directory forest, the local administrator account that you signed in with is converted to an equivalent account with the same password in the new forest and domain.</span></span> <span data-ttu-id="fe13f-146">그러면 로컬 계정이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-146">The local account is then deleted.</span></span>

<span data-ttu-id="fe13f-147">예를 들어 DC1\DCAdmin 로컬 계정으로 로그인하고 가상 컴퓨터를 corp.contoso.com 도메인에 대한 새 포리스트의 도메인 컨트롤러로 승격하는 경우 DC1\DCAdmin 로컬 계정이 삭제되고 같은 암호를 가진 새 도메인 계정 CORP\DCAdmin이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-147">For example, if you signed in with the local account DC1\DCAdmin, and then promoted the virtual machine as a domain controller in a new forest for the corp.contoso.com domain, the DC1\DCAdmin local account gets deleted and a new domain account (CORP\DCAdmin) is created with the same password.</span></span>

<span data-ttu-id="fe13f-148">계정 이름이 가상 컴퓨터가 유효한 계정으로 확인할 수 있는 이름이고 암호가 올바른지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="fe13f-148">Make sure that the account name is a name that the virtual machine can verify as a valid account, and that the password is correct.</span></span>

<span data-ttu-id="fe13f-149">로컬 관리자 계정의 암호를 변경해야 하는 경우 [Windows 가상 컴퓨터에 대한 원격 데스크톱 서비스 또는 암호를 다시 설정하는 방법](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe13f-149">If you need to change the password of the local administrator account, see [How to reset a password or the Remote Desktop service for Windows virtual machines](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-to-the-remote-computer"></a><span data-ttu-id="fe13f-150">이 컴퓨터에서 원격 컴퓨터에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-150">This computer can't connect to the remote computer.</span></span>
<span data-ttu-id="fe13f-151">원인: 연결에 사용한 계정에 원격 데스크톱 로그인 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-151">Cause: The account that's used to connect does not have Remote Desktop sign-in rights.</span></span>

<span data-ttu-id="fe13f-152">모든 Windows 컴퓨터에는 원격으로 로그인할 수 있는 계정 및 그룹을 포함하는 원격 데스크톱 사용자 로컬 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-152">Every Windows computer has a Remote Desktop users local group, which contains the accounts and groups that can sign into it remotely.</span></span> <span data-ttu-id="fe13f-153">로컬 관리자 그룹의 구성원도 액세스 권한을 갖고 있지만 원격 데스크톱 사용자 로컬 그룹에 표시되지 않은 계정도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-153">Members of the local administrators group also have access, even though those accounts are not listed in the Remote Desktop users local group.</span></span> <span data-ttu-id="fe13f-154">도메인에 가입된 컴퓨터의 경우 해당 도메인의 도메인 관리자도 로컬 관리자 그룹에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-154">For domain-joined machines, the local administrators group also contains the domain administrators for the domain.</span></span>

<span data-ttu-id="fe13f-155">연결하는 데 사용하는 계정에 원격 데스크톱 로그인 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-155">Make sure that the account you're using to connect with has Remote Desktop sign-in rights.</span></span> <span data-ttu-id="fe13f-156">해결 방법으로 도메인 또는 로컬 관리자 계정을 사용하여 원격 데스크톱을 통해 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-156">As a workaround, use a domain or local administrator account to connect over Remote Desktop.</span></span> <span data-ttu-id="fe13f-157">원격 데스크톱 사용자 로컬 그룹에 원하는 계정을 추가하려면 Microsoft Management Console 스냅인(**시스템 도구 > 로컬 사용자 및 그룹 > 그룹 > 원격 데스크톱 사용자**)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe13f-157">To add the desired account to the Remote Desktop users local group, use the Microsoft Management Console snap-in (**System Tools > Local Users and Groups > Groups > Remote Desktop Users**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe13f-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe13f-158">Next steps</span></span>
<span data-ttu-id="fe13f-159">이러한 오류가 발생하지 않고 RDP를 사용한 연결에 대해 알려지지 않은 문제가 있는 경우 [원격 데스크톱에 대한 자세한 문제 해결 가이드](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe13f-159">If none of these errors occurred and you have an unknown issue with connecting using RDP, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="fe13f-160">VM에서 실행 중인 응용 프로그램에 액세스하는 문제 해결 단계는 [Azure VM에서 실행 중인 응용 프로그램에 대한 액세스 문제 해결](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe13f-160">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access to an application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="fe13f-161">SSH(Secure Shell)를 사용하여 Azur에서 Linux VM에 연결하는 데 문제가 있는 경우 [Azure에서 Linux VM에 SSH 연결 문제 해결](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe13f-161">If you are having issues using Secure Shell (SSH) to connect to a Linux VM in Azure, see [Troubleshoot SSH connections to a Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

