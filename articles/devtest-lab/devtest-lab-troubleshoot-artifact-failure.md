---
title: "DevTest Labs Azure VM의 aaaDiagnose 아티팩트 오류 | Microsoft Docs"
description: "자세한 내용은 방법에서 DevTest Labs tootroubleshoot 아티팩트 오류"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a><span data-ttu-id="4aa5b-103">Hello 랩에서 아티팩트 오류를 진단</span><span class="sxs-lookup"><span data-stu-id="4aa5b-103">Diagnose artifact failures in hello lab</span></span> 
<span data-ttu-id="4aa5b-104">아티팩트를 만든 후에 성공 또는 실패 하는 경우 toosee를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-104">After you have created an artifact, you can check toosee if it succeeded or failed.</span></span> <span data-ttu-id="4aa5b-105">DevTest Labs에서 아티팩트 로그 toodiagnose 아티팩트 오류를 사용할 수 있는 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-105">Artifact logs in DevTest Labs provide information you can use toodiagnose an artifact failure.</span></span> <span data-ttu-id="4aa5b-106">Windows VM에 대 한 hello 아티팩트 로그 정보를 볼 수는 몇 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-106">There are a couple different ways you can view hello artifact log information for a Windows VM.</span></span>

> [!NOTE]
> <span data-ttu-id="4aa5b-107">tooensure 실패는 올바르게 식별 및 설명,이 hello 아티팩트 제대로 구성 되어 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-107">tooensure that failures are correctly identified and explained, it is important that hello artifact is properly structured.</span></span> <span data-ttu-id="4aa5b-108">Toocorrectly 아티팩트를 생성 하는 방법에 대 한 정보를 참조 하십시오. [사용자 지정 아티팩트를 만들](devtest-lab-artifact-author.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-108">For information about how toocorrectly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="4aa5b-109">하 고 올바르게 구조화 된 아티팩트의 예로 toosee이 [테스트 매개 변수 형식](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) 아티팩트입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-109">And toosee an example of a properly structured artifact, check out this [Test Parameter Types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a><span data-ttu-id="4aa5b-110">Hello Azure 포털을 사용 하 여 아티팩트 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4aa5b-110">Troubleshoot artifact failures using hello Azure portal</span></span>
<span data-ttu-id="4aa5b-111">다음이 단계를 수행 하는 아티팩트를 만드는 동안 toouse hello Azure 포털 toodiagnose 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-111">toouse hello Azure portal toodiagnose failures during artifact creation, follow these steps:</span></span>

1. <span data-ttu-id="4aa5b-112">리소스의 hello 목록에서 랩을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-112">From hello list of resources, select your lab.</span></span>

2. <span data-ttu-id="4aa5b-113">Hello tooinvestigate 원하는 hello 아티팩트를 포함 하는 Windows VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-113">Choose hello Windows VM that includes hello artifact you want tooinvestigate.</span></span>

3. <span data-ttu-id="4aa5b-114">아래에 hello 왼쪽된 패널에 **일반**, 선택 **아티팩트**합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-114">In hello left panel under **GENERAL**, choose **Artifacts**.</span></span> <span data-ttu-id="4aa5b-115">해당 VM과 연결 된 아티팩트 목록이 표시를 나타내는 hello 이름 hello 아티팩트 및 서버 인스턴스의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-115">A list of artifacts associated with that VM appears, indicating hello name of hello artifact and its status.</span></span>

   ![아티팩트 Git 리포지토리 예](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="4aa5b-117">**실패**의 상태를 보여 주는 아티팩트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-117">Choose an artifact that shows a status of **Failed**.</span></span> <span data-ttu-id="4aa5b-118">hello 아티팩트가 열리고 hello 아티팩트 hello 실패에 대 한 세부 정보가 포함 된 확장 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-118">hello artifact opens and shows an extension message that includes details about hello failure of hello artifact.</span></span>

   ![아티팩트 Git 리포지토리 예](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a><span data-ttu-id="4aa5b-120">Hello VM 내에서 아티팩트 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4aa5b-120">Troubleshoot artifact failures from within hello VM</span></span>
<span data-ttu-id="4aa5b-121">hello 가상 컴퓨터 내에서 tooview hello 아티팩트 로그에서 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-121">tooview hello artifact logs from within hello virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="4aa5b-122">Toohello toodiagnose 원하는 hello 아티팩트를 포함 하는 VM에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-122">Log in toohello VM that contains hello artifact you want toodiagnose.</span></span>

2. <span data-ttu-id="4aa5b-123">여기서 "1.9는 hello CSE 버전 번호 tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status 이동입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-123">Navigate tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status where "1.9 is hello CSE version number.</span></span>

   ![아티팩트 Git 리포지토리 예](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="4aa5b-125">열기 hello **상태** 파일 tooview 정보 해당 VM에 대 한 아티팩트 실패를 진단 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-125">Open hello **status** file tooview information that helps diagnose artifact failures for that VM.</span></span>




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="4aa5b-126">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="4aa5b-126">Related blog posts</span></span>
* [<span data-ttu-id="4aa5b-127">VM tooexisting Azure DevTest Labs에서 리소스 관리자 템플릿을 사용 하는 AD 도메인 가입</span><span class="sxs-lookup"><span data-stu-id="4aa5b-127">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="4aa5b-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4aa5b-128">Next steps</span></span>
* <span data-ttu-id="4aa5b-129">너무 방법에 대해 알아봅니다[Git 리포지토리 tooa 랩 추가](devtest-lab-add-artifact-repo.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa5b-129">Learn how too[add a Git repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

