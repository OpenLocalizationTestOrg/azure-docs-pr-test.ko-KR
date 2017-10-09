---
title: "첫 번째 Windows VM에는 IIS aaaInstall | Microsoft Docs"
description: "첫 번째 시험해 IIS를 설치 하 고 포트 80을 사용 하 여 Windows 가상 컴퓨터는 Azure 포털 hello 합니다."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a>Windows VM에서 역할을 설치하여 실험
첫 번째 가상 컴퓨터 (VM)를 구성 및 실행 되 고 있으면 tooinstalling 소프트웨어 및 서비스에서 이동할 수 있습니다. 이 자습서에서는 하겠습니다 toouse 서버 관리자에서 Windows Server VM tooinstall hello IIS 합니다. 그런 다음 네트워크 보안 그룹 (NSG) hello Azure 포털 tooopen 포트 80 tooIIS 트래픽을 사용 하 여 만듭니다. 

첫 번째 VM을 아직 만들지 않은 경우 해야 다시가 서 너무[hello Azure 포털에서에서 첫 번째 Windows 가상 컴퓨터를 만들](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 이 자습서를 계속 합니다.

## <a name="make-sure-hello-vm-is-running"></a>VM이 실행 되 고 있는지 hello를 확인 합니다.
1. 열기 hello [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **가상 컴퓨터**합니다. Hello 목록에서 hello 가상 컴퓨터를 선택 합니다.
3. Hello 상태가 **중지 (할당 취소)**, hello 클릭 **시작** hello 단추 **Essentials** hello VM의 블레이드에서 합니다. Hello 상태가 **실행**, toohello 다음 단계로 이동할 수 있습니다.

## <a name="connect-toohello-virtual-machine-and-sign-in"></a>Toohello 가상 컴퓨터에 연결 하 고 로그인
1. Hello 허브 메뉴에서 클릭 **가상 컴퓨터**합니다. Hello 목록에서 hello 가상 컴퓨터를 선택 합니다.
2. Hello 가상 컴퓨터에 대 한 hello 블레이드에서 클릭 **연결**합니다. 그러면 만들어지고 바로 가기 tooconnect tooyour 컴퓨터과 같은 원격 데스크톱 프로토콜 파일 (.rdp 파일)을 다운로드 합니다. Toosave hello 파일 tooyour 데스크톱 편리 하 게 할 수 있습니다. **열기** 파일 tooconnect tooyour VM이 있습니다.
   
    ![Hello Azure 포털 보여 주는 스크린샷 어떻게 tooconnect tooyour VM](./media/hero-role/connect.png)
3. 경고가 나타나면 해당 hello.rdp 알 수 없는 게시자에서 시작 됩니다. 이것은 정상입니다. Hello 원격 데스크톱 창에서 클릭 **연결** toocontinue 합니다.
   
    ![알 수 없는 게시자에 대한 경고 스크린샷](./media/hero-role/rdp-warn.png)
4. Hello Windows 보안 창 형식 hello 사용자 이름 및 암호를 만들 때 만든 hello 로컬 계정에 대 한 VM을 hello 합니다. hello 사용자 이름을으로 입력 됩니다 *vmname*&#92; *사용자 이름*, 클릭 **확인**합니다.
   
    ![Hello VM 이름, 사용자 이름 및 암호를 입력 하는 스크린 샷](./media/hero-role/credentials.png)
5. 경고가 나타나면 해당 hello 인증서를 확인할 수 없습니다. 이것은 정상입니다. 클릭 **예** tooverify hello 가상 컴퓨터의 id를 hello 및 로그온을 완료 합니다.
   
   ![메시지를 보여 주는 스크린샷 hello VM의 hello id를 확인 한 섹션인](./media/hero-role/cert-warning.png)

Tooconnect 려 할 때 tootrouble에서 실행 하면 참조 [Windows 기반 Azure 가상 컴퓨터 문제를 해결 하는 원격 데스크톱 연결 tooa](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

## <a name="install-iis-on-your-vm"></a>VM에 IIS 설치
Toohello VM에에서 로그인 해야 했으므로 더 작업할 수 있도록 서버 역할을 설치 합니다.

1. 아직 열려 있지 않은 경우 **서버 관리자** 를 엽니다. Hello 클릭 **시작** 메뉴를 차례로 클릭 **서버 관리자**합니다.
2. **서버 관리자**선택, **로컬 서버** hello 왼쪽된 창에서. 
3. Hello 메뉴에서 선택 **관리** > **역할 및 기능 추가**합니다.
4. Hello 추가 역할 및 기능 마법사 hello **설치 유형을** 페이지에서 선택 **역할 기반 또는 기능 기반 설치**, 클릭 하 고 **다음**합니다.
   
    ![스크린 샷 보여 주는 hello 추가 역할 및 기능 마법사에 대 한 탭 설치 유형](./media/hero-role/role-wizard.png)
5. Hello 서버 풀의 hello VM을 선택 하 고 클릭 **다음**합니다.
6. Hello에 **서버 역할** 페이지에서 **웹 서버 (IIS)**합니다.
   
    ![스크린 샷 보여 주는 hello 추가 역할 및 기능 마법사에 대 한 탭 서버 역할](./media/hero-role/add-iis.png)
7. IIS에 필요한 기능을 추가 하는 방법에 대 한 팝업 hello, 되는지 확인 **관리 도구 포함** 을 선택 하 고 클릭 **기능 추가**합니다. 클릭 하 여 hello 팝업을 닫으면 **다음** hello 마법사에서 합니다.
   
    ![Hello IIS 역할을 추가 하는 팝업 tooconfirm 보여 주는 스크린샷](./media/hero-role/confirm-add-feature.png)
8. Hello 기능 페이지에서 클릭 **다음**합니다.
9. Hello에 **웹 서버 역할 (IIS)** 페이지 **다음**합니다. 
10. Hello에 **역할 서비스** 페이지 **다음**합니다. 
11. Hello에 **확인** 페이지 **설치**합니다. 
12. Hello 설치가 완료 되 면 클릭 **닫기** hello 마법사에 있습니다.

## <a name="open-port-80"></a>포트 80 열기
VM tooaccept 위해에서 포트 80 통한 트래픽 인바운드 tooadd는 인바운드 규칙 toohello 네트워크 보안 그룹을 사용 해야 합니다. 

1. 열기 hello [Azure 포털](https://portal.azure.com)합니다.
2. **가상 컴퓨터** 선택 hello 만든 VM입니다.
3. Hello 가상 컴퓨터 설정에서 선택 **네트워크 인터페이스** 다음 선택 hello 기존 네트워크 인터페이스 하 고 있습니다.
   
    ![Hello에 대 한 가상 컴퓨터 설정을 hello 네트워크 인터페이스를 보여 주는 스크린샷](./media/hero-role/network-interface.png)
4. **Essentials** hello 네트워크 인터페이스에 대 한 클릭 hello **네트워크 보안 그룹**합니다.
   
    ![Hello 네트워크 인터페이스에 대 한 hello Essentials 섹션을 보여 주는 스크린샷](./media/hero-role/select-nsg.png)
5. Hello에 **Essentials** NSG hello에 대 한 블레이드에서 있어야 인바운드 규칙에 대 한 하나의 기존 기본 **기본 허용 rdp** 수 있는 toolog toohello VM에에서 있습니다. 다른 인바운드 규칙 tooallow IIS 트래픽을 추가 합니다. **인바운드 보안 규칙**을 클릭합니다.
   
    ![NSG hello에 대 한 hello Essentials 섹션을 보여 주는 스크린샷](./media/hero-role/inbound.png)
6. **인바운드 보안 규칙**에서 **추가**를 클릭합니다.
   
    ![Hello 단추 tooadd 보안 규칙을 보여 주는 스크린샷](./media/hero-role/add-rule.png)
7. **인바운드 보안 규칙**에서 **추가**를 클릭합니다. 형식 **80** 에서 포트 범위 hello 하 고 있는지 확인 **허용** 을 선택 합니다. 완료되면 **확인**을 클릭합니다.
   
    ![Hello 단추 tooadd 보안 규칙을 보여 주는 스크린샷](./media/hero-role/port-80.png)

Nsg 인바운드 및 아웃 바운드 규칙에 대 한 자세한 내용은 참조 하십시오. [Azure 포털 hello 허용 외부 tooyour VM 사용 하 여 액세스](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="connect-toohello-default-iis-website"></a>Toohello 기본 IIS 웹 사이트를 연결 합니다.
1. Hello Azure 포털에서에서 클릭 **가상 컴퓨터** 한 다음 VM을 선택 합니다.
2. Hello에 **Essentials** 블레이드에서 복사 하면 **공용 IP 주소**합니다.
   
    ![여기서 toofind hello VM의 공용 IP 주소를 보여 주는 스크린샷](./media/hero-role/ipaddress.png)
3. 브라우저를 열고 hello 주소 표시줄에서 다음과 같은 공용 IP 주소 입력: http://<publicIPaddress> 클릭 **Enter** toogo toothat 주소입니다.
4. 브라우저가는 hello 기본 IIS 웹 페이지를 열어야 합니다. 모양은 다음과 같습니다.
   
    ![브라우저에서 다음과 같은 hello 기본 IIS 페이지에 관계를 보여 주는 스크린샷](./media/hero-role/iis-default.png)

## <a name="next-steps"></a>다음 단계
* 또한 실험할 수 [데이터 디스크 연결](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour 가상 컴퓨터. 데이터 디스크는 가상 컴퓨터에 대한 더 많은 저장소를 제공합니다.

