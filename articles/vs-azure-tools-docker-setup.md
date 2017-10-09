---
title: "Docker 호스트를 VirtualBox aaaConfigure | Microsoft Docs"
description: "단계별 지침은 tooconfigure 기본 Docker는 Docker 컴퓨터 및 VirtualBox 사용 하 여 인스턴스"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a>VirtualBox 및 Docker 호스트 구성
## <a name="overview"></a>개요
이 문서에서는 Docker 컴퓨터 및 VirtualBox를 사용하여 기본 Docker 인스턴스를 구성하는 과정을 안내합니다. Hello를 사용 하 여 [Windows 용 Docker beta](http://beta.docker.com/),이 구성은 필요 하지 않습니다.

## <a name="prerequisites"></a>필수 조건
hello 다음과 같은 도구가 필요 toobe 설치 합니다.

* [Docker 도구 상자](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a>Windows PowerShell을 사용 하 여 hello Docker 클라이언트 구성
tooconfigure Docker 클라이언트 하기만 하면 Windows PowerShell을 열고 hello 다음 단계를 수행 합니다.

1. 기본 docker 호스트 인스턴스를 만듭니다.
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. Hello 기본 인스턴스는 구성 하 고 실행을 확인 합니다. ('기본'이라는 인스턴스가 실행되는 것이 표시됩니다.
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker-machine ls output][0]
3. Hello 현재 호스트와 기본값을 설정 하 고 셸에서 구성 합니다.
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. Hello 활성 Docker 컨테이너를 표시 합니다. hello 목록 비어 있어야 합니다.
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps output][1]

> [!NOTE]
> 개발 컴퓨터를 다시 부팅 될 때마다 해야 toorestart 로컬 docker 호스트 합니다.
> toodo 다음 명령을 명령 프롬프트에서이, 문제 hello: `docker-machine start default`합니다.
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
