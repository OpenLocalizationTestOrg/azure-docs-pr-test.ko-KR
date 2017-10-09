---
title: "Azure VM에 대 한 aaaDownload hello 템플릿을 | Microsoft Docs"
description: "Hello 만들기 hello 리소스 관리자 배포 모델에서 배포를 자동화 된 VM toohelp 다운로드"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a>VM에 대 한 hello 템플릿을 다운로드합니다
Azure에서 VM을 만들 때 hello 포털 또는 PowerShell을 리소스 관리자를 사용 하 여 서식 파일은 자동으로 생성 합니다. 이 템플릿 tooquickly 중복 배포를 사용할 수 있습니다. hello 서식 파일의 모든 리소스 그룹의 hello 리소스에 대 한 정보를 포함합니다. 가상 컴퓨터에 대 한 hello ´ ï ´ hello 네트워킹 리소스를 포함 하 여 해당 리소스 그룹에 VM hello 지원 하기 위해 만든 모든 것을 의미 합니다.

## <a name="download-hello-template-using-hello-portal"></a>Hello 포털을 사용 하 여 hello 템플릿을 다운로드합니다
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 하나의 hello 허브 메뉴에서 선택 **가상 컴퓨터**합니다.
3. Hello 목록에서 hello 가상 컴퓨터를 선택 합니다.
4. **Automation 스크립트**를 선택합니다.
5. 선택 **다운로드** hello.zip 파일 tooyour 로컬 컴퓨터를 저장 합니다.
6. Hello.zip 파일을 열고 hello 파일 tooa 폴더에 추출 합니다. hello.zip 파일에 포함 됩니다.
   
   * deploy.ps1
   * deploy.sh 
   * deployer.rb
   * DeploymentHelper.cs
   * parameters.json
   * template.json

hello template.json 파일은 hello 템플릿입니다.

## <a name="download-hello-template-using-powershell"></a>PowerShell을 사용 하 여 hello 템플릿을 다운로드합니다
Hello를 사용 하 여 hello.json 템플릿 파일을 다운로드할 수 있습니다 [내보내기 AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet. Hello를 사용할 수 있습니다 `-path` 매개 변수 tooprovide hello 파일 이름 및 hello.json 파일에 대 한 경로입니다. Hello 리소스 그룹에 대 한 toodownload hello 서식 파일 이름이 지정 하는 방법을 보여 주는이 예제 **myResourceGroup** toohello **C:\users\public\downloads** 로컬 컴퓨터의 폴더에 있습니다.

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a>다음 단계
서식 파일을 사용 하 여 리소스를 배포에 대 한 더 toolearn 참조 [리소스 관리자 템플릿 연습](../../azure-resource-manager/resource-manager-template-walkthrough.md)합니다.

