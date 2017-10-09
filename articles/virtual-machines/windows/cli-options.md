---
title: windows Azure CLI aaaUsing hello | Microsoft Docs
description: "Windows hello Azure CLI를 사용 하 여"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a>Windows hello Azure CLI를 사용 하 여

Azure 명령줄 인터페이스 (CLI) hello 명령줄 및 스크립팅 환경 만들기 및 Azure 리소스 관리를 제공 합니다. macOS, Linux 및 Windows 운영 체제에 대 한 hello Azure CLI ´ ù. 하지만 이러한 운영 체제에서 hello CLI 명령을 동일 운영 체제 특정 스크립팅 구문 다를 수 있습니다.

이 문서 정보 hello 방식 Azure CLI hello에 설치 하 고 각각에 대 한 구문 고려 사항 창과 세부 정보에서 실행 수입니다. Azure CLI 설명서에 대한 자세한 내용은 [Azure CLI 설명서]( https://docs.microsoft.com/en-us/cli/azure/overview)를 참조하세요.

## <a name="windows-subsystem-for-linux"></a>Linux용 Windows 하위 시스템

hello Windows 하위 시스템 Linux (WSL)는 Windows 10 Anniversary 및 이후 버전에서 Ubuntu Linux 환경을 제공 합니다. WSL를 사용하도록 설정하면 네이티브 Bash 환경을 제공합니다. 이 기능은 Azure CLI 스크립트를 만들고 실행하는 데 사용할 수 있습니다. WSL에서 네이티브 Bash 환경을 제공하기 때문에 Azure CLI 스크립트를 수정하지 않고 macOS, Linux 및 Windows 간에 공유할 수 있습니다.

toouse hello Azure CLI WSL에 hello 다음을 수행 합니다.

|작업 | 지침 |
|---|---|
| WSL 사용 | [WSL 설명서 설치](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| Hello Azure CLI를 설치 합니다. |[WSL/Ubuntu 14.04에 hello CLI를 설치 합니다.](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a>PowerShell

windows에서 hello Azure CLI를 고유 하 게 실행할 수 있습니다. 이 구성에서는 hello Azure CLI 패키지 hello Windows 운영 체제에 설치 되어 및 PowerShell에서 명령을 실행할 수 있습니다. 이 구성에서는 지원되는 버전의 Windows에서 Azure CLI 명령 및 스크립트를 실행할 수 있지만 플랫폼 지정 스크립트 구문이 필요합니다. 이런 이유로 macOS, Linux 및 Windows 스크립트를 모두 수정하지 않고 공유할 수 있는 것은 아닙니다.

이러한 지침을 사용 하 여 hello 패키지를 설치 하는 windows에서 Azure CLI toouse hello [설치 hello Windows에서 CLI](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows)합니다.

## <a name="docker-image"></a>Docker 이미지

Windows 용 Docker를 사용 하 여 hello Azure CLI를 포함 하는 Docker 이미지 수 있습니다. 시작할 수 있습니다. 이 이미지는 Linux에서 기반으로 하며 네이티브 Bash 환경을 포함합니다.  Windows 용 Docker 및 hello Azure CLI 이미지, 스크립트 toobe macOS, Linux 및 Windows에서 공유할을 사용할 때 

Windows 용 Docker에 Azure CLI toouse hello Windows 용 Docker 실행 되 고 hello 다음 명령을 실행을 확인 합니다.

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

완료 되 면 시작 합니다 즉 Bash hello Azure CLI 도구와 함께 미리 로드 합니다.

## <a name="next-steps"></a>다음 단계

[Azure Virtual Machines에 대한 CLI 샘플](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Azure Web Apps에 대한 CLI 샘플](../../app-service-web/app-service-cli-samples.md)

[Azure SQL에 대한 CLI 샘플](../../sql-database/sql-database-cli-samples.md)
