---
title: "GitHub에서 Azure 스택 도구를 다운로드 합니다. | Microsoft Docs"
description: "Azure 스택을 사용 하는 데 필요한 도구를 다운로드 하는 방법에 알아봅니다."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: 28F360AD-789A-488D-965F-FC6E6CCF3329
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: mabrigg
ms.openlocfilehash: d4f8a8d73f8e2ea321cb6cc1deda2301033b249d
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2017
---
# <a name="download-azure-stack-tools-from-github"></a>GitHub에서 Azure 스택 도구 다운로드

AzureStack 도구는 관리 및 Azure 스택에 리소스를 배포 하는 데 사용할 수 있는 PowerShell 모듈을 호스팅하는 GitHub 리포지토리입니다. 다운로드 및 VPN 연결을 설정 하려는 경우 Azure 스택 개발 키트를 또는 windows 기반 외부 클라이언트에 이러한 PowerShell 모듈을 사용할 수 있습니다. 이러한 도구를 얻으려면 GitHub 리포지토리 복제 하거나 AzureStack 도구 폴더에서 다음 스크립트를 실행 하 여 다운로드 합니다.

```PowerShell
# Change directory to the root directory 
cd \

# Download the tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand the downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change to the tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-the-modules"></a>모듈에서 제공 되는 기능

AzureStack 도구 저장소 Azure 스택에 대 한 다음과 같은 기능을 지 원하는 PowerShell 모듈이 포함 되어 있습니다.  

| 기능 | 설명 | 이 모듈을 사용할 수 있는? |
| --- | --- | --- |
| [클라우드 기능](azure-stack-validate-templates.md) | 이 모듈을 사용 하 여 클라우드의 클라우드 기능을 얻으려고 합니다. 예를 들어 Azure 스택 및이 모듈을 사용 하 여 Azure 클라우드에 대 한 API 버전, Azure 리소스 관리자 리소스, VM 확장 등과 같은 클라우드 기능을 얻을 수 있습니다. | 클라우드 관리자와 사용자입니다. |
| [리소스 관리자 정책에 대 한 Azure 스택](azure-stack-policy-module.md) | Azure 스택 동일한 버전 관리 및 서비스 가용성과 함께 Azure 구독 또는 Azure 리소스 그룹을 구성 하려면이 모듈을 사용 합니다. | 클라우드 관리자 및 사용자 |
| [Azure 스택에 연결](azure-stack-connect-azure-stack.md) | 이 모듈을 사용 하 여 PowerShell 통해 Azure 스택 인스턴스에 연결 하 고 Azure 스택에 VPN 연결을 구성 합니다. | 클라우드 관리자 및 사용자 |
| [서식 파일 유효성 검사기](azure-stack-validate-templates.md) | 이 모듈 Azure 스택에 기존 또는 새 템플릿을 배포 하는 경우 확인을 사용 합니다. | 클라우드 관리자 및 사용자 |


## <a name="next-steps"></a>다음 단계
* [Azure 스택 사용자의 PowerShell 환경 구성](azure-stack-powershell-configure-user.md)   
* [VPN을 통해 Azure 스택 개발 키트를 연결 합니다.](azure-stack-connect-azure-stack.md)  
