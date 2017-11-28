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
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="c87f7-103">Azure Windows VM 확장 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c87f7-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="c87f7-104">확장 상태 보기</span><span class="sxs-lookup"><span data-stu-id="c87f7-104">Viewing extension status</span></span>
<span data-ttu-id="c87f7-105">Azure Powershell에서 Azure Resource Manager 템플릿을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c87f7-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="c87f7-106">Hello 템플릿을 실행 하 고 나면 Azure 리소스 탐색기 또는 hello 명령줄 도구에서 hello 확장 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c87f7-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="c87f7-107">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="c87f7-107">Here is an example:</span></span>

<span data-ttu-id="c87f7-108">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c87f7-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="c87f7-109">다음은 hello 샘플 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="c87f7-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="c87f7-110">]</span><span class="sxs-lookup"><span data-stu-id="c87f7-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="c87f7-111">확장 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c87f7-111">Troubleshooting extension failures</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="c87f7-112">Hello VM에 확장 hello를 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c87f7-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="c87f7-113">Hello 사용자 지정 스크립트 확장을 사용 하 여 VM에서 스크립트를 실행 하는 경우에 오류가 있는 VM 만들었지만 hello 스크립트는 실패 했을 경우에 따라 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c87f7-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="c87f7-114">이러한 conditons에서이 오류 로부터 방식으로 toorecover 권장 hello는 tooremove hello 확장 한 hello 서식 파일을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c87f7-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="c87f7-115">참고: 앞으로이 기능은 될 향상 된 tooremove hello hello 확장을 제거 하기 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c87f7-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-powershell"></a><span data-ttu-id="c87f7-116">Azure PowerShell에서 hello 확장 제거</span><span class="sxs-lookup"><span data-stu-id="c87f7-116">Remove hello extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="c87f7-117">Hello 확장 제거 되 면 hello 템플릿을 hello VM에서 다시 실행된 toorun hello 스크립트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c87f7-117">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

