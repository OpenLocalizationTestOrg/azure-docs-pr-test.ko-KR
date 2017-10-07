---
title: "빠른 시작-aaaAzure VM 만듭니다 포털 | Microsoft Docs"
description: "Azure 빠른 시작 - VM 만들기 포털"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 984a400c976e349a59f873210d6e04bcdea39e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-portal"></a>Azure 포털 hello로 Linux 가상 컴퓨터 만들기

Hello Azure 포털을 통해 azure 가상 컴퓨터를 만들 수 있습니다. 이 메서드는 가상 컴퓨터 및 관련된 모든 리소스를 만들고 구성하기 위한 브라우저 기반 사용자 인터페이스를 제공합니다. 이 퀵 스타트 단계별로 실행 가상 컴퓨터를 만들고 hello VM에서 웹 서버를 설치 합니다.

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.

## <a name="create-ssh-key-pair"></a>SSH 키 쌍 만들기

SSH 키 쌍 toocomplete이 빠른 시작을 해야합니다. 기존 SSH 키 쌍을 사용하는 경우 이 단계를 건너뛸 수 있습니다.

Bash 셸의에서이 명령을 실행 하 고 지시를 따른 hello 화면에 표시 합니다. hello 명령 출력에는 hello 공개 키 파일의 hello 파일 이름을 포함합니다. Hello 공개 키 파일 toohello 클립보드의 hello 내용을 복사 합니다.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-tooazure"></a>TooAzure 로그인 

Azure 포털에서 http://portal.azure.com toohello에 로그인 합니다.

## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기

1. Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.

2. **계산**을 선택한 후 **Ubuntu Server 16.04 LTS**를 선택합니다. 

3. Hello 가상 컴퓨터 정보를 입력 합니다. **인증 유형**으로 **SSH 공용 키**를 선택합니다. SSH 공개 키를 붙여 넣는 경우 주의 tooremove 모든 선행 또는 후행 공백은 합니다. 완료되면 **확인**을 클릭합니다.

    ![Hello 포털 블레이드에서 VM에 대 한 기본 정보를 입력 합니다.](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. Hello VM에 대 한 크기를 선택 합니다. toosee 자세한 크기 선택 **모든 보기** hello 변경 또는 **지원 되는 디스크 형식을** 필터입니다. 

    ![VM 크기를 보여 주는 스크린샷](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. Hello 설정 블레이드에서 hello 기본값을 유지 하 고 클릭 **확인**합니다.

6. Hello 요약 페이지에서 클릭 **확인** toostart hello 가상 컴퓨터에 배포 합니다.

7. hello VM에 Azure 포털 대시보드에서 고정 된 toohello 됩니다. Hello 배포 완료 되 면 hello VM 요약 블레이드 자동으로 열립니다.


## <a name="connect-toovirtual-machine"></a>Toovirtual 컴퓨터 연결

Hello 가상 컴퓨터와 SSH 연결을 만듭니다.

1. Hello 클릭 **연결** hello 가상 컴퓨터 블레이드 단추입니다. hello 단추 표시 사용된 tooconnect toohello 가상 컴퓨터 일 수 있는 한 SSH 연결 문자열을 연결 합니다.

    ![포털 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. 실행된 hello 다음 명령은 toocreate SSH 세션입니다. Hello Azure 포털에서에서 복사 하는 hello로 hello 연결 문자열을 대체 합니다.

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a>NGINX 설치

사용 하 여 hello 다음 스크립트 tooupdate 패키지 소스를 이용한 적 하 고 hello 최신 NGINX 패키지를 설치 합니다. 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

을 완료 한 후 hello SSH 세션을 종료 하 고 hello Azure 포털에서에서 hello VM 속성을 반환 합니다.


## <a name="open-port-80-for-web-traffic"></a>웹 트래픽에 대해 포트 80 열기 

NSG(네트워크 보안 그룹)는 인바운드 및 아웃바운드 트래픽의 보안을 유지합니다. VM hello Azure 포털에서에서 만들어지면는 인바운드 규칙 SSH 연결에 대 한 포트 22에 만들어집니다. 이 VM에서 웹 서버를 호스트 하기 때문에 포트 80에 대해 만든 toobe NSG 규칙에 필요 합니다.

1. Hello 가상 컴퓨터의 hello hello 이름을 클릭 **리소스 그룹**합니다.
2. 선택 hello **네트워크 보안 그룹**합니다. hello NSG를 식별할 수 있습니다 hello를 사용 하 여 **형식** 열입니다. 
3. 설정에서 hello 왼쪽 메뉴에서 클릭 **인바운드 보안 규칙**합니다.
4. **추가**를 클릭합니다.
5. **이름**에서 **http**를 입력합니다. 있는지 확인 **포트 범위가** too80 설정 및 **동작** 너무 설정**허용**합니다. 
6. **확인**을 클릭합니다.


## <a name="view-hello-nginx-welcome-page"></a>Hello NGINX 시작 페이지 보기

Hello 웹 서버 hello에서 액세스할 수 있습니다, NGINX 설치 되어 있으며 포트 80 엽니다 tooyour VM 인터넷 합니다. 웹 브라우저를 열고 hello hello VM의 공용 IP 주소를 입력 합니다. hello Azure 포털에서에서 VM 블레이드의 hello hello 공용 IP 주소를 찾을 수 있습니다.

![NGINX 기본 사이트](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>리소스 정리

더 이상 필요 hello 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 삭제 합니다. toodo 따라서 hello 가상 컴퓨터 블레이드에서 hello 리소스 그룹을 선택 하 고 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 간단한 가상 컴퓨터, 네트워크 보안 그룹 규칙을 배포했으며 웹 서버를 설치했습니다. Azure 가상 컴퓨터에 대해 자세히 toolearn Linux Vm에 대 한 toohello 자습서를 계속 합니다.

> [!div class="nextstepaction"]
> [Azure Linux 가상 컴퓨터 자습서](./tutorial-manage-vm.md)
