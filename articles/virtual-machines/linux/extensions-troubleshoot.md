---
title: "Linux VM 확장 오류 문제 해결 | Microsoft Docs"
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
ms.openlocfilehash: 589890de379d0b729de1f1ba9e604e0ec0496f50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="9abe4-103">Azure Linux VM 확장 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9abe4-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="9abe4-104">확장 상태 보기</span><span class="sxs-lookup"><span data-stu-id="9abe4-104">Viewing extension status</span></span>
<span data-ttu-id="9abe4-105">Azure CLI에서 Azure Resource Manager 템플릿을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9abe4-105">Azure Resource Manager templates can be executed from the  Azure CLI.</span></span> <span data-ttu-id="9abe4-106">템플릿을 실행한 후 Azure 리소스 탐색기 또는 명령줄 도구에서 확장 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9abe4-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="9abe4-107">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="9abe4-107">Here is an example:</span></span>

<span data-ttu-id="9abe4-108">Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="9abe4-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="9abe4-109">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9abe4-109">Here is the sample output:</span></span>

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
  <span data-ttu-id="9abe4-110">]</span><span class="sxs-lookup"><span data-stu-id="9abe4-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="9abe4-111">확장 오류 문제 해결:</span><span class="sxs-lookup"><span data-stu-id="9abe4-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="9abe4-112">VM에서 확장 다시 실행</span><span class="sxs-lookup"><span data-stu-id="9abe4-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="9abe4-113">사용자 지정 스크립트 확장을 사용하여 VM에서 스크립트를 실행하는 경우 때때로 VM이 성공적으로 만들어졌지만 스크립트가 실패하는 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9abe4-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="9abe4-114">이러한 조건에서 이 오류를 복구하는 권장 방법은 확장을 제거하고 템플릿을 다시 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9abe4-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="9abe4-115">참고: 이후에는 확장을 제거할 필요가 없도록 이 기능이 향상될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="9abe4-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-cli"></a><span data-ttu-id="9abe4-116">Azure CLI에서 확장 제거</span><span class="sxs-lookup"><span data-stu-id="9abe4-116">Remove the extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="9abe4-117">여기서 "publsher-name"은 "azure vm get-instance-view" 출력의 확장 형식에 해당하고 name은 템플릿의 확장 리소스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9abe4-117">Where "publsher-name" corresponds to the extension type from the output of "azure vm get-instance-view" and name is the name of the extension resource from the template</span></span>

<span data-ttu-id="9abe4-118">확장이 제거되면 템플릿을 다시 실행하여 VM에서 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9abe4-118">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

