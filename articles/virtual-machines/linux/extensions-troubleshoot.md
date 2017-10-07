---
title: "Linux VM aaaTroubleshooting 확장 오류 | Microsoft Docs"
description: "Azure Linux VM 확장 오류 문제 해결에 대해 자세히 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>Azure Linux VM 확장 오류 문제 해결
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>확장 상태 보기
Azure 리소스 관리자 템플릿 hello Azure CLI에서에서 실행할 수 있습니다. Hello 템플릿을 실행 하 고 나면 Azure 리소스 탐색기 또는 hello 명령줄 도구에서 hello 확장 상태를 볼 수 있습니다.

다음은 예제입니다.

Azure CLI:

      azure vm get-instance-view


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

## <a name="troubleshooting-extenson-failures"></a>확장 오류 문제 해결:
### <a name="re-running-hello-extension-on-hello-vm"></a>Hello VM에 확장 hello를 다시 실행합니다.
Hello 사용자 지정 스크립트 확장을 사용 하 여 VM에서 스크립트를 실행 하는 경우에 오류가 있는 VM 만들었지만 hello 스크립트는 실패 했을 경우에 따라 실행할 수 있습니다. 이러한 conditons에서이 오류 로부터 방식으로 toorecover 권장 hello는 tooremove hello 확장 한 hello 서식 파일을 다시 실행 합니다.
참고: 앞으로이 기능은 될 향상 된 tooremove hello hello 확장을 제거 하기 위해 필요 합니다.

#### <a name="remove-hello-extension-from-azure-cli"></a>Azure CLI에서 hello 확장 제거
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

여기서 "publsher-name" hello 출력에서 "azure vm get-인스턴스-보기" toohello 확장 형식을 해당 하 고 hello 이름은 hello 템플릿에서 hello 확장 리소스의 이름

Hello 확장 제거 되 면 hello 템플릿을 hello VM에서 다시 실행된 toorun hello 스크립트 수 있습니다.

