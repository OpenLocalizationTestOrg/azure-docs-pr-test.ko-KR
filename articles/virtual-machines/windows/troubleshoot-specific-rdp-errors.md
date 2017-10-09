---
title: "Azure Vm에 대 한 aaaSpecific RDP 오류 메시지 | Microsoft Docs"
description: "Azure에서 원격 데스크톱 연결 tooa Windows 가상 컴퓨터를 사용 하는 동안 나타날 수 있는 특정 오류 메시지 이해"
keywords: "원격 데스크톱 오류, 원격 데스크톱 연결 오류 tooVM, 연결할 수 없습니다. 원격 데스크톱 문제 해결"
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
ms.openlocfilehash: 8e1551be23e696bd60adbd76c3e1ea86d9dd11aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a>특정 RDP 오류 메시지 tooa Azure에서 Windows VM 문제 해결
Azure에서 원격 데스크톱 연결 tooa Windows 가상 컴퓨터 (VM)를 사용 하는 경우 특정 오류 메시지가 나타날 수 있습니다. 이 문서 세부 정보 중 일부 hello 단계 tooresolve 문제 해결 발생 한 가지 일반적인 오류 메시지에 있습니다. Tooyour VM 연결 문제가 발생 하는 경우 특정 오류 메시지가 발생 하지 없이 RDP를 사용 하, hello 참조 [문제 해결 가이드에 대 한 원격 데스크톱](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

특정 오류 메시지에 대 한 정보를 보려면 hello 다음을 참조 하세요.

* [원격 데스크톱 라이선스 서버 사용 가능한 tooprovide 없습니다 라이선스 있기 때문에 hello 원격 연결이 끊어졌습니다](#rdplicense)합니다.
* [원격 데스크톱 hello 컴퓨터 "이름"에서 찾을 수 없는](#rdpname)합니다.
* [인증 오류가 발생 했습니다. hello 로컬 보안 기관에 연결할 수 없는](#rdpauth)합니다.
* [Windows 보안 오류: 자격 증명이 작동하지 않습니다](#wincred).
* [이 컴퓨터 toohello 원격 컴퓨터에 연결할 수 없는](#rdpconnect)합니다.

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a>hello 원격 세션에는 없는 원격 데스크톱 라이선스 서버 사용 가능한 tooprovide 라이선스 있기 때문에 연결이 해제 되었습니다.
원인: hello 원격 데스크톱 서버 역할에 대 한 hello 120 일 라이선스 유예 기간이 만료 및 tooinstall 라이선스가 필요 합니다.

이 문제를 해결 hello 포털에서 hello RDP 파일의 로컬 복사본을 저장 하 고 PowerShell 명령 프롬프트 tooconnect에서이 명령을 실행 합니다. 이 단계를 따르면 해당 연결에만 라이선스를 사용할 수 없게 됩니다.

        mstsc <File name>.RDP /admin

두 개 이상의 동시 원격 데스크톱 연결 toohello VM을 실제로 필요 하지 않으면, 서버 관리자 tooremove hello 원격 데스크톱 서버 역할을 사용할 수 있습니다.

자세한 내용은 hello 블로그 게시물을 참조 하십시오. ["원격 데스크톱 라이선스 서버가 없는 사용할 수 있는" Azure VM 실패](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/)합니다.

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a>원격 데스크톱 hello 컴퓨터 "name"을 찾을 수 없습니다.
원인: 컴퓨터에 원격 데스크톱 클라이언트 hello hello hello RDP 파일의 hello 설정에서 hello 컴퓨터 이름을 확인할 수 없습니다.

가능한 해결 방법:

* 조직의 인트라넷을 사용 하는 경우 컴퓨터 액세스 toohello 프록시 서버에 HTTPS 트래픽 tooit를 보낼 수 있는지 확인 합니다.
* 로컬에 저장 된 RDP 파일을 사용 하는 경우 hello 포털에서 생성 되는 하나 hello를 사용해 보세요. 이 단계는 hello hello 가상 컴퓨터 또는 hello 클라우드 서비스와의 hello VM hello 끝점 포트에 대 한 올바른 DNS 이름이 있는지 확인 합니다. Hello 포털에서 생성 되는 샘플 RDP 파일 다음과 같습니다.
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

이 RDP 파일의 hello 주소 부분에 있습니다.

* hello는 hello ("tailspin-azdatatier.cloudapp.net"이 예에서) VM을 포함 하는 hello 클라우드 서비스의 도메인 이름을 정규화 합니다.
* hello 외부 TCP 포트의 원격 데스크톱 트래픽 (55919)에 대 한 hello 끝점입니다.

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a>인증 오류가 발생했습니다. hello 로컬 보안 기관에 연결할 수 없습니다.
원인: hello 대상 VM의 자격 증명의 사용자 이름 부분 hello에에서 hello 보안 기관을 찾을 수 없습니다.

Hello 양식에서 사용자 이름이 표시 되는 경우 *SecurityAuthority*\\*UserName* (예: CORP\User1), hello *SecurityAuthority* 부분이 어느 hello VM의 컴퓨터 이름 (로컬 보안 기관 hello) 또는 Active Directory 도메인 이름입니다.

가능한 해결 방법:

* Hello 계정이 로컬 toohello VM 인 경우 해당 hello VM 이름이 올바르게 입력 되어 있는지 확인 합니다.
* Hello 계정이 Active Directory 도메인에 있는 경우 hello hello 도메인 이름이 올바른지를 확인 합니다.
* Active Directory 도메인 계정 인지 hello 도메인 이름의 철자가 정확 하는 경우 해당 도메인의 도메인 컨트롤러를 사용할 수 있는지 확인 합니다. 도메인 컨트롤러가 시작되지 않았기 때문에 사용할 수 없는 것은 도메인 컨트롤러가 포함된 Azure 가상 네트워크에서 일반적인 문제입니다. 해결 방법으로 도메인 계정 대신 로컬 관리자 계정을 사용할 수 있습니다.

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a>Windows 보안 오류: 자격 증명이 작동하지 않습니다.
원인: 계정 이름 및 암호 hello 대상 VM 확인할 수 없습니다.

Windows 기반 컴퓨터의 로컬 계정 또는 도메인 계정을 hello 자격 증명 유효성을 검사할 수 있습니다.

* 로컬 계정에 대 한 hello를 사용 하 여 *ComputerName*\\*UserName* 구문 (예: SQL1\Admin4798).
* 도메인 계정에 대 한 hello를 사용 하 여 *DomainName*\\*UserName* 구문 (예: CONTOSO\peterodman).

새 Active Directory 포리스트에 VM tooa 도메인 컨트롤러 승격 시키고 hello 로컬 관리자 계정으로 로그인 하는 변환 동일 hello로 tooan 해당 계정 hello 새 포리스트 및 도메인 암호입니다. 그러면 hello 로컬 계정이 삭제 됩니다.

다음 가상 컴퓨터 hello hello corp.contoso.com 도메인에 대 한 새 포리스트의 도메인 컨트롤러로 승격을 DC1\DCAdmin, hello 로컬 계정으로 로그인 DC1\DCAdmin 로컬 계정에서 삭제 되 고 새 도메인 계정 (CORP\DCAdmin hello 하는 예를 들어 ) 사용 하 여 만든 hello 동일 암호입니다.

해당 hello 계정 이름 hello 가상 컴퓨터를 올바른 계정으로 확인할 수 및 해당 hello 암호가 올바른지 이름 인지 확인 합니다.

Hello 로컬 관리자 계정의 toochange hello 암호가 필요한 경우 참조 [Windows 가상 컴퓨터에 대 한 서비스 tooreset 암호 또는 원격 데스크톱 hello](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a>이 컴퓨터는 toohello 원격 컴퓨터를 연결할 수 없습니다.
원인: hello 계정 tooconnect 사용 없을 대 한 원격 데스크톱 로그인 합니다.

모든 Windows 컴퓨터에 원격 데스크톱 사용자가 로컬 그룹이 것에 원격으로 로그인 할 수 있는 hello 계정 및 그룹을 포함 합니다. Hello 로컬 관리자 그룹의 구성원도 액세스할 수 있으며, 이러한 계정을 hello 원격 데스크톱 사용자에 대 한 로컬 그룹에 나열 되지 않은 경우에 도메인에 가입 된 컴퓨터에 대 한 hello 로컬 관리자 그룹에는 hello 도메인에 대 한 hello 도메인 관리자가 포함 됩니다.

Tooconnect와 사용 중인는 hello 계정에 대 한 원격 데스크톱 로그인이 있는지 확인 합니다. 문제를 해결할 도메인 또는 로컬 관리자 계정 tooconnect 원격 데스크톱을 통해 사용 합니다. tooadd hello 원하는 계정 toohello 원격 데스크톱 users 로컬 그룹, hello Microsoft Management Console 스냅인을 사용 하 여 (**시스템 도구 > 로컬 사용자 및 그룹 > 그룹 > 원격 데스크톱 사용자**).

## <a name="next-steps"></a>다음 단계
이러한 오류 중에 발생 한 RDP를 사용 하 여 연결 된 알 수 없는 문제가 있는 경우 참조 hello [문제 해결 가이드에 대 한 원격 데스크톱](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

* VM에서 실행 중인 응용 프로그램에 액세스 하는 단계를 문제 해결을 위해 참조 [문제 해결 액세스 tooan 응용 프로그램이 Azure VM에서 실행 중인](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
* Azure에서 SSH (보안 셸) tooconnect tooa Linux VM을 사용 하는 데 문제가 있는 경우 참조 [해결 SSH 연결 tooa Azure에서 Linux VM](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

