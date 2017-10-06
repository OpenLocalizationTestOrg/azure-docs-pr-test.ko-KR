---
title: "Windows VM 확장 오류 aaaTroubleshooting | Microsoft Docs"
description: "Azure Windows VM 확장 오류 문제 해결에 대해 자세히 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a>Azure Windows VM 확장 오류 문제 해결
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>확장 상태 보기
Azure Powershell에서 Azure Resource Manager 템플릿을 실행할 수 있습니다. Hello 템플릿을 실행 하 고 나면 Azure 리소스 탐색기 또는 hello 명령줄 도구에서 hello 확장 상태를 볼 수 있습니다.

다음은 예제입니다.

Azure PowerShell:

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

다음은 hello 샘플 출력이입니다.

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  ]

## <a name="troubleshooting-extension-failures"></a>확장 오류 문제 해결
### <a name="re-running-hello-extension-on-hello-vm"></a>Hello VM에 확장 hello를 다시 실행합니다.
Hello 사용자 지정 스크립트 확장을 사용 하 여 VM에서 스크립트를 실행 하는 경우에 오류가 있는 VM 만들었지만 hello 스크립트는 실패 했을 경우에 따라 실행할 수 있습니다. 이러한 conditons에서이 오류 로부터 방식으로 toorecover 권장 hello는 tooremove hello 확장 한 hello 서식 파일을 다시 실행 합니다.
참고: 앞으로이 기능은 될 향상 된 tooremove hello hello 확장을 제거 하기 위해 필요 합니다.

#### <a name="remove-hello-extension-from-azure-powershell"></a>Azure PowerShell에서 hello 확장 제거
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

Hello 확장 제거 되 면 hello 템플릿을 hello VM에서 다시 실행된 toorun hello 스크립트 수 있습니다.

