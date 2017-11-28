---
title: "DevTest Labs VM에 대 한 사용자 지정 아티팩트 aaaCreate | Microsoft Docs"
description: "Tooauthor 사용자 고유의 아티팩트에 대 한 포함 된 사용 방법을 DevTest Labs에 알아봅니다"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="628d0-103">DevTest Lab VM에 대한 사용자 지정 아티팩트 만들기</span><span class="sxs-lookup"><span data-stu-id="628d0-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="628d0-104">개요</span><span class="sxs-lookup"><span data-stu-id="628d0-104">Overview</span></span>
<span data-ttu-id="628d0-105">**아티팩트** 사용 되는 toodeploy 되며 VM 프로 비전 된 후 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-105">**Artifacts** are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="628d0-106">아티팩트는 Git 리포지토리의 폴더에 저장되어 있는 아티팩트 정의 파일 및 다른 스크립트 파일로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="628d0-107">JSON 및 식을 사용할 수 있는 toospecify 수행할 아티팩트 정의 파일 구성 VM에서 tooinstall 합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-107">Artifact definition files consist of JSON and expressions that you can use toospecify what you want tooinstall on a VM.</span></span> <span data-ttu-id="628d0-108">예를 들어 hello 이름 아티팩트, 명령 toorun 및 hello 명령을 실행할 때 사용할 수 있는 매개 변수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-108">For example, you can define hello name of an artifact, command toorun, and parameters that are made available when hello command is run.</span></span> <span data-ttu-id="628d0-109">이름으로 hello 아티팩트 정의 파일 내에서 tooother 스크립트 파일을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-109">You can refer tooother script files within hello artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="628d0-110">아티팩트 정의 파일 형식</span><span class="sxs-lookup"><span data-stu-id="628d0-110">Artifact definition file format</span></span>
<span data-ttu-id="628d0-111">hello 다음 예제는 hello 정의 파일의 기본 구조를 구성 하는 hello 섹션.</span><span class="sxs-lookup"><span data-stu-id="628d0-111">hello following example shows hello sections that make up hello basic structure of a definition file:</span></span>

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| <span data-ttu-id="628d0-112">요소 이름</span><span class="sxs-lookup"><span data-stu-id="628d0-112">Element name</span></span> | <span data-ttu-id="628d0-113">Required?</span><span class="sxs-lookup"><span data-stu-id="628d0-113">Required?</span></span> | <span data-ttu-id="628d0-114">설명</span><span class="sxs-lookup"><span data-stu-id="628d0-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="628d0-115">$schema</span><span class="sxs-lookup"><span data-stu-id="628d0-115">$schema</span></span> |<span data-ttu-id="628d0-116">아니요</span><span class="sxs-lookup"><span data-stu-id="628d0-116">No</span></span> |<span data-ttu-id="628d0-117">Hello 정의 파일의 hello 유효성 테스트에 도움이 되는 hello JSON 스키마 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-117">Location of hello JSON schema file that helps in testing hello validity of hello definition file.</span></span> |
| <span data-ttu-id="628d0-118">title</span><span class="sxs-lookup"><span data-stu-id="628d0-118">title</span></span> |<span data-ttu-id="628d0-119">예</span><span class="sxs-lookup"><span data-stu-id="628d0-119">Yes</span></span> |<span data-ttu-id="628d0-120">Hello 랩에 표시 된 hello 아티팩트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-120">Name of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="628d0-121">설명</span><span class="sxs-lookup"><span data-stu-id="628d0-121">description</span></span> |<span data-ttu-id="628d0-122">예</span><span class="sxs-lookup"><span data-stu-id="628d0-122">Yes</span></span> |<span data-ttu-id="628d0-123">Hello 랩에 표시 된 hello 아티팩트에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-123">Description of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="628d0-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="628d0-124">iconUri</span></span> |<span data-ttu-id="628d0-125">아니요</span><span class="sxs-lookup"><span data-stu-id="628d0-125">No</span></span> |<span data-ttu-id="628d0-126">Hello 랩에 표시 된 hello 아이콘의 Uri입니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-126">Uri of hello icon displayed in hello lab.</span></span> |
| <span data-ttu-id="628d0-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="628d0-127">targetOsType</span></span> |<span data-ttu-id="628d0-128">예</span><span class="sxs-lookup"><span data-stu-id="628d0-128">Yes</span></span> |<span data-ttu-id="628d0-129">Hello 아티팩트를 설치한 VM의 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-129">Operating system of hello VM where artifact is installed.</span></span> <span data-ttu-id="628d0-130">지원되는 옵션은 Windows 및 Linux입니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="628d0-131">매개 변수</span><span class="sxs-lookup"><span data-stu-id="628d0-131">parameters</span></span> |<span data-ttu-id="628d0-132">아니요</span><span class="sxs-lookup"><span data-stu-id="628d0-132">No</span></span> |<span data-ttu-id="628d0-133">아티팩트 설치 명령이 컴퓨터에서 실행될 때 제공되는 값으로</span><span class="sxs-lookup"><span data-stu-id="628d0-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="628d0-134">아티팩트를 사용자 지정하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="628d0-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="628d0-135">runCommand</span></span> |<span data-ttu-id="628d0-136">예</span><span class="sxs-lookup"><span data-stu-id="628d0-136">Yes</span></span> |<span data-ttu-id="628d0-137">VM에서 실행되는 아티팩트 설치 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="628d0-138">아티팩트 매개 변수</span><span class="sxs-lookup"><span data-stu-id="628d0-138">Artifact parameters</span></span>
<span data-ttu-id="628d0-139">Hello hello 정의 파일의 매개 변수 섹션에서 아티팩트를 설치 하는 경우는 사용자가 입력할 수 있는 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-139">In hello parameters section of hello definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="628d0-140">Hello 아티팩트 설치 명령에 toothese 값을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-140">You can refer toothese values in hello artifact install command.</span></span>

<span data-ttu-id="628d0-141">구조를 다음 hello로 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-141">You define parameters with hello following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="628d0-142">요소 이름</span><span class="sxs-lookup"><span data-stu-id="628d0-142">Element name</span></span> | <span data-ttu-id="628d0-143">Required?</span><span class="sxs-lookup"><span data-stu-id="628d0-143">Required?</span></span> | <span data-ttu-id="628d0-144">설명</span><span class="sxs-lookup"><span data-stu-id="628d0-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="628d0-145">type</span><span class="sxs-lookup"><span data-stu-id="628d0-145">type</span></span> |<span data-ttu-id="628d0-146">예</span><span class="sxs-lookup"><span data-stu-id="628d0-146">Yes</span></span> |<span data-ttu-id="628d0-147">매개 변수 값의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-147">Type of parameter value.</span></span> <span data-ttu-id="628d0-148">Hello hello 허용 되는 형식에 대 한 목록을 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="628d0-148">See hello following list for hello allowed types:</span></span> |
| <span data-ttu-id="628d0-149">displayName</span><span class="sxs-lookup"><span data-stu-id="628d0-149">displayName</span></span> |<span data-ttu-id="628d0-150">예</span><span class="sxs-lookup"><span data-stu-id="628d0-150">Yes</span></span> |<span data-ttu-id="628d0-151">Hello 매개 변수 hello 랩의 표시 된 tooa 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-151">Name of hello parameter that is displayed tooa user in hello lab.</span></span> | |
| <span data-ttu-id="628d0-152">설명</span><span class="sxs-lookup"><span data-stu-id="628d0-152">description</span></span> |<span data-ttu-id="628d0-153">예</span><span class="sxs-lookup"><span data-stu-id="628d0-153">Yes</span></span> |<span data-ttu-id="628d0-154">설명 hello 랩에 표시 되는 hello 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-154">Description of hello parameter that is displayed in hello lab.</span></span> |

<span data-ttu-id="628d0-155">hello 유형은 허용:</span><span class="sxs-lookup"><span data-stu-id="628d0-155">hello allowed types are:</span></span>

* <span data-ttu-id="628d0-156">문자열 - 유효한 모든 JSON 문자열</span><span class="sxs-lookup"><span data-stu-id="628d0-156">string – any valid JSON string</span></span>
* <span data-ttu-id="628d0-157">int - 유효한 모든 JSON 정수</span><span class="sxs-lookup"><span data-stu-id="628d0-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="628d0-158">bool - 유효한 모든 JSON 부울</span><span class="sxs-lookup"><span data-stu-id="628d0-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="628d0-159">array - 유효한 모든 JSON 배열</span><span class="sxs-lookup"><span data-stu-id="628d0-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="628d0-160">아티팩트 식 및 함수</span><span class="sxs-lookup"><span data-stu-id="628d0-160">Artifact expressions and functions</span></span>
<span data-ttu-id="628d0-161">식을 사용할 수 있습니다 및 함수 tooconstruct hello 아티팩트 명령을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-161">You can use expression and functions tooconstruct hello artifact install command.</span></span>
<span data-ttu-id="628d0-162">식은 대괄호로 묶여 ([및]), hello 아티팩트 설치 될 때 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when hello artifact is installed.</span></span> <span data-ttu-id="628d0-163">식은 JSON 문자열 값에서 어느 위치에나 나타날 수 있으며 항상 다른 JSON 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="628d0-164">Toouse 대괄호가로 시작 하는 리터럴 문자열을 필요한 경우 [, 두 개의 대괄호를 사용 해야 합니다 [[합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-164">If you need toouse a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="628d0-165">일반적으로 식을 함수 tooconstruct 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-165">Typically, you use expressions with functions tooconstruct a value.</span></span> <span data-ttu-id="628d0-166">JavaScript에서와 마찬가지로 함수 호출은 functionName(arg1,arg2,arg3)으로 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="628d0-167">hello 다음은 일반 함수.</span><span class="sxs-lookup"><span data-stu-id="628d0-167">hello following list shows common functions:</span></span>

* <span data-ttu-id="628d0-168">parameters(parameterName)-hello 아티팩트 명령이 실행 될 때 제공 되는 매개 변수 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-168">parameters(parameterName) - Returns a parameter value that is provided when hello artifact command is run.</span></span>
* <span data-ttu-id="628d0-169">concat(arg1,arg2,arg3, …..) - 여러 문자열 값을 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="628d0-170">이 함수는 임의의 수의 인수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="628d0-171">hello 방법을 예제와 다음 toouse 식과 함수 tooconstruct 값:</span><span class="sxs-lookup"><span data-stu-id="628d0-171">hello following example shows how toouse expression and functions tooconstruct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="628d0-172">사용자 지정 아티팩트 만들기</span><span class="sxs-lookup"><span data-stu-id="628d0-172">Create a custom artifact</span></span>
<span data-ttu-id="628d0-173">다음 단계를 수행하여 사용자 지정 아티팩트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="628d0-174">JSON 편집기를 설치 하-JSON 편집기 toowork 아티팩트 정의 파일을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-174">Install a JSON editor - You need a JSON editor toowork with artifact definition files.</span></span> <span data-ttu-id="628d0-175">Windows, Linux 및 OS X에 사용할 수 있는 [Visual Studio Code](https://code.visualstudio.com/)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="628d0-176">Get에서 DevTest Labs Azure 팀에서 만든 샘플 artifactfile.json-체크 아웃 hello 아티팩트 우리의 [GitHub 리포지토리](https://github.com/Azure/azure-devtestlab)풍부한 라이브러리 만들어졌습니다. 여기서 아티팩트 수 있는 사용자 고유의 아티팩트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-176">Get a sample artifactfile.json - Check out hello artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="628d0-177">아티팩트 정의 파일을 다운로드 하 고 변경 내용을 tooit toocreate 사용자 고유의 아티팩트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-177">Download an artifact definition file and make changes tooit toocreate your own artifacts.</span></span>
3. <span data-ttu-id="628d0-178">아티팩트 정의 파일에는 intellisense-tooconstruct 사용된 될 수 있는 활용 IntelliSense toosee 유효한 요소 사용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-178">Make use of IntelliSense - Leverage IntelliSense toosee valid elements that can be used tooconstruct an artifact definition file.</span></span> <span data-ttu-id="628d0-179">Hello 다양 한 옵션 값에 대 한 요소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-179">You can also see hello different options for values of an element.</span></span> <span data-ttu-id="628d0-180">예를 들어 IntelliSense 표시 hello를 편집 하는 경우 Windows 또는 Linux의 두 가지 선택 hello **targetOsType** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-180">For example, IntelliSense show you hello two choices of Windows or Linux when editing hello **targetOsType** element.</span></span>
4. <span data-ttu-id="628d0-181">저장소 hello 아티팩트는 [git 리포지토리](devtest-lab-add-artifact-repo.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-181">Store hello artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="628d0-182">여기서 hello 디렉터리 이름을 hello 동일 hello 아티팩트 이름으로 각 아티팩트에 대 한 별도 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-182">Create a separate directory for each artifact where hello directory name is hello same as hello artifact name.</span></span>
   2. <span data-ttu-id="628d0-183">Hello 아티팩트 정의 파일 (artifactfile.json) 만든 hello 디렉터리에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-183">Store hello artifact definition file (artifactfile.json) in hello directory you created.</span></span>
   3. <span data-ttu-id="628d0-184">Hello 아티팩트에서 참조 되는 저장소 hello 스크립트 명령을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-184">Store hello scripts that are referenced from hello artifact install command.</span></span>
      
      <span data-ttu-id="628d0-185">다음은 아티팩트 폴더가 표시되는 모습의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![아티팩트 Git 리포지토리 예](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="628d0-187">Hello 아티팩트 저장소 toohello 랩 추가-toohello 문서 참조 [아티팩트 및 템플릿에 대 한 Git 리포지토리를 추가](devtest-lab-add-artifact-repo.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-187">Add hello artifacts repository toohello lab - Refer toohello article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="628d0-188">관련 문서</span><span class="sxs-lookup"><span data-stu-id="628d0-188">Related articles</span></span>
* [<span data-ttu-id="628d0-189">어떻게 DevTest Labs의 toodiagnose 아티팩트 오류</span><span class="sxs-lookup"><span data-stu-id="628d0-189">How toodiagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="628d0-190">VM tooexisting Azure DevTest Labs에서 리소스 관리자 템플릿을 사용 하는 AD 도메인 가입</span><span class="sxs-lookup"><span data-stu-id="628d0-190">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="628d0-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="628d0-191">Next steps</span></span>
* <span data-ttu-id="628d0-192">너무 방법에 대해 알아봅니다[Git 아티팩트 저장소 tooa 랩 추가](devtest-lab-add-artifact-repo.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="628d0-192">Learn how too[add a Git artifact repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

