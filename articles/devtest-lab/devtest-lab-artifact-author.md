---
title: "DevTest Labs VM에 대한 사용자 지정 아티팩트 만들기 | Microsoft 문서"
description: "DevTest 랩과 함께 사용할 사용자 고유의 아티팩트를 저작하는 방법 알아보기"
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
ms.openlocfilehash: 2412033daa1d97860dd9f380178622b1ddc590c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="eed63-103">DevTest Lab VM에 대한 사용자 지정 아티팩트 만들기</span><span class="sxs-lookup"><span data-stu-id="eed63-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="eed63-104">개요</span><span class="sxs-lookup"><span data-stu-id="eed63-104">Overview</span></span>
<span data-ttu-id="eed63-105">**아티팩트** 가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-105">**Artifacts** are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="eed63-106">아티팩트는 Git 리포지토리의 폴더에 저장되어 있는 아티팩트 정의 파일 및 다른 스크립트 파일로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="eed63-107">아티팩트 정의 파일은 VM에 설치하려는 아티팩트를 지정하는 데 사용할 수 있는 JSON과 식으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-107">Artifact definition files consist of JSON and expressions that you can use to specify what you want to install on a VM.</span></span> <span data-ttu-id="eed63-108">예를 들어 아티팩트의 이름, 실행할 명령, 명령이 실행되는 경우 사용할 수 있는 매개 변수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-108">For example, you can define the name of an artifact, command to run, and parameters that are made available when the command is run.</span></span> <span data-ttu-id="eed63-109">이름으로 아티팩트 정의 파일 내의 다른 스크립트 파일을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-109">You can refer to other script files within the artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="eed63-110">아티팩트 정의 파일 형식</span><span class="sxs-lookup"><span data-stu-id="eed63-110">Artifact definition file format</span></span>
<span data-ttu-id="eed63-111">다음 예제에서는 정의 파일의 기본 구조를 구성하는 섹션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-111">The following example shows the sections that make up the basic structure of a definition file:</span></span>

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

| <span data-ttu-id="eed63-112">요소 이름</span><span class="sxs-lookup"><span data-stu-id="eed63-112">Element name</span></span> | <span data-ttu-id="eed63-113">Required?</span><span class="sxs-lookup"><span data-stu-id="eed63-113">Required?</span></span> | <span data-ttu-id="eed63-114">설명</span><span class="sxs-lookup"><span data-stu-id="eed63-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eed63-115">$schema</span><span class="sxs-lookup"><span data-stu-id="eed63-115">$schema</span></span> |<span data-ttu-id="eed63-116">아니요</span><span class="sxs-lookup"><span data-stu-id="eed63-116">No</span></span> |<span data-ttu-id="eed63-117">정의 파일의 유효성을 테스트하는 데 도움이 되는 JSON 스키마 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-117">Location of the JSON schema file that helps in testing the validity of the definition file.</span></span> |
| <span data-ttu-id="eed63-118">title</span><span class="sxs-lookup"><span data-stu-id="eed63-118">title</span></span> |<span data-ttu-id="eed63-119">예</span><span class="sxs-lookup"><span data-stu-id="eed63-119">Yes</span></span> |<span data-ttu-id="eed63-120">랩에 표시되는 아티팩트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-120">Name of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="eed63-121">설명</span><span class="sxs-lookup"><span data-stu-id="eed63-121">description</span></span> |<span data-ttu-id="eed63-122">예</span><span class="sxs-lookup"><span data-stu-id="eed63-122">Yes</span></span> |<span data-ttu-id="eed63-123">랩에 표시되는 아티팩트에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-123">Description of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="eed63-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="eed63-124">iconUri</span></span> |<span data-ttu-id="eed63-125">아니요</span><span class="sxs-lookup"><span data-stu-id="eed63-125">No</span></span> |<span data-ttu-id="eed63-126">랩에 표시되는 아이콘의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-126">Uri of the icon displayed in the lab.</span></span> |
| <span data-ttu-id="eed63-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="eed63-127">targetOsType</span></span> |<span data-ttu-id="eed63-128">예</span><span class="sxs-lookup"><span data-stu-id="eed63-128">Yes</span></span> |<span data-ttu-id="eed63-129">아티팩트가 설치되는 VM의 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-129">Operating system of the VM where artifact is installed.</span></span> <span data-ttu-id="eed63-130">지원되는 옵션은 Windows 및 Linux입니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="eed63-131">매개 변수</span><span class="sxs-lookup"><span data-stu-id="eed63-131">parameters</span></span> |<span data-ttu-id="eed63-132">아니요</span><span class="sxs-lookup"><span data-stu-id="eed63-132">No</span></span> |<span data-ttu-id="eed63-133">아티팩트 설치 명령이 컴퓨터에서 실행될 때 제공되는 값으로</span><span class="sxs-lookup"><span data-stu-id="eed63-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="eed63-134">아티팩트를 사용자 지정하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="eed63-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="eed63-135">runCommand</span></span> |<span data-ttu-id="eed63-136">예</span><span class="sxs-lookup"><span data-stu-id="eed63-136">Yes</span></span> |<span data-ttu-id="eed63-137">VM에서 실행되는 아티팩트 설치 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="eed63-138">아티팩트 매개 변수</span><span class="sxs-lookup"><span data-stu-id="eed63-138">Artifact parameters</span></span>
<span data-ttu-id="eed63-139">정의 파일의 매개 변수 섹션에서 아티팩트를 설치할 때 사용자가 입력할 수 있는 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-139">In the parameters section of the definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="eed63-140">아티팩트 설치 명령에서 다음 값을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-140">You can refer to these values in the artifact install command.</span></span>

<span data-ttu-id="eed63-141">다음과 같은 구조를 사용하여 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-141">You define parameters with the following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="eed63-142">요소 이름</span><span class="sxs-lookup"><span data-stu-id="eed63-142">Element name</span></span> | <span data-ttu-id="eed63-143">Required?</span><span class="sxs-lookup"><span data-stu-id="eed63-143">Required?</span></span> | <span data-ttu-id="eed63-144">설명</span><span class="sxs-lookup"><span data-stu-id="eed63-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eed63-145">type</span><span class="sxs-lookup"><span data-stu-id="eed63-145">type</span></span> |<span data-ttu-id="eed63-146">예</span><span class="sxs-lookup"><span data-stu-id="eed63-146">Yes</span></span> |<span data-ttu-id="eed63-147">매개 변수 값의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-147">Type of parameter value.</span></span> <span data-ttu-id="eed63-148">허용되는 형식에 대해 다음 목록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eed63-148">See the following list for the allowed types:</span></span> |
| <span data-ttu-id="eed63-149">displayName</span><span class="sxs-lookup"><span data-stu-id="eed63-149">displayName</span></span> |<span data-ttu-id="eed63-150">예</span><span class="sxs-lookup"><span data-stu-id="eed63-150">Yes</span></span> |<span data-ttu-id="eed63-151">랩에서 사용자에게 표시되는 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-151">Name of the parameter that is displayed to a user in the lab.</span></span> | |
| <span data-ttu-id="eed63-152">설명</span><span class="sxs-lookup"><span data-stu-id="eed63-152">description</span></span> |<span data-ttu-id="eed63-153">예</span><span class="sxs-lookup"><span data-stu-id="eed63-153">Yes</span></span> |<span data-ttu-id="eed63-154">랩에 표시되는 매개 변수의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-154">Description of the parameter that is displayed in the lab.</span></span> |

<span data-ttu-id="eed63-155">허용 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-155">The allowed types are:</span></span>

* <span data-ttu-id="eed63-156">문자열 - 유효한 모든 JSON 문자열</span><span class="sxs-lookup"><span data-stu-id="eed63-156">string – any valid JSON string</span></span>
* <span data-ttu-id="eed63-157">int - 유효한 모든 JSON 정수</span><span class="sxs-lookup"><span data-stu-id="eed63-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="eed63-158">bool - 유효한 모든 JSON 부울</span><span class="sxs-lookup"><span data-stu-id="eed63-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="eed63-159">array - 유효한 모든 JSON 배열</span><span class="sxs-lookup"><span data-stu-id="eed63-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="eed63-160">아티팩트 식 및 함수</span><span class="sxs-lookup"><span data-stu-id="eed63-160">Artifact expressions and functions</span></span>
<span data-ttu-id="eed63-161">식과 함수를 사용하여 아티팩트 설치 명령을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-161">You can use expression and functions to construct the artifact install command.</span></span>
<span data-ttu-id="eed63-162">식은 대괄호([ 및 ]) 안에 들어 있고 아티팩트를 설치할 때 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when the artifact is installed.</span></span> <span data-ttu-id="eed63-163">식은 JSON 문자열 값에서 어느 위치에나 나타날 수 있으며 항상 다른 JSON 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="eed63-164">대괄호([)로 시작하는 리터럴 문자열을 사용해야 하는 경우 대괄호를 두 개([[) 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-164">If you need to use a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="eed63-165">일반적으로 함수가 포함된 식을 사용하여 값을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-165">Typically, you use expressions with functions to construct a value.</span></span> <span data-ttu-id="eed63-166">JavaScript에서와 마찬가지로 함수 호출은 functionName(arg1,arg2,arg3)으로 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="eed63-167">다음 목록에는 일반 함수가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-167">The following list shows common functions:</span></span>

* <span data-ttu-id="eed63-168">매개 변수(parameterName) - 아티팩트 명령이 실행될 때 제공되는 매개 변수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-168">parameters(parameterName) - Returns a parameter value that is provided when the artifact command is run.</span></span>
* <span data-ttu-id="eed63-169">concat(arg1,arg2,arg3, …..) - 여러 문자열 값을 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="eed63-170">이 함수는 임의의 수의 인수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="eed63-171">다음 예제에서는 값을 구성하기 위해 식과 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-171">The following example shows how to use expression and functions to construct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="eed63-172">사용자 지정 아티팩트 만들기</span><span class="sxs-lookup"><span data-stu-id="eed63-172">Create a custom artifact</span></span>
<span data-ttu-id="eed63-173">다음 단계를 수행하여 사용자 지정 아티팩트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="eed63-174">JSON 편집기 설치 - 아티팩트 정의 파일 작업을 수행하려면 JSON 편집기가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-174">Install a JSON editor - You need a JSON editor to work with artifact definition files.</span></span> <span data-ttu-id="eed63-175">Windows, Linux 및 OS X에 사용할 수 있는 [Visual Studio Code](https://code.visualstudio.com/)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="eed63-176">artifactfile.json 샘플 가져오기 - 사용자 고유 아티팩트를 만드는 데 도움이 되는 풍부한 아티팩트 라이브러리를 만들어 놓은 [GitHub 리포지토리](https://github.com/Azure/azure-devtestlab)에서 Azure DevTest Labs 팀이 만든 아티팩트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-176">Get a sample artifactfile.json - Check out the artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="eed63-177">아티팩트 정의 파일을 다운로드하고 변경하여 사용자 고유 아티팩트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-177">Download an artifact definition file and make changes to it to create your own artifacts.</span></span>
3. <span data-ttu-id="eed63-178">IntelliSense 사용 - 아티팩트 정의 파일을 구성하는 데 사용할 수 있는 유효한 요소를 보려면 IntelliSense를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-178">Make use of IntelliSense - Leverage IntelliSense to see valid elements that can be used to construct an artifact definition file.</span></span> <span data-ttu-id="eed63-179">또한 요소 값에 대한 다양한 옵션을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-179">You can also see the different options for values of an element.</span></span> <span data-ttu-id="eed63-180">예를 들어 IntelliSense에 **targetOsType** 요소를 편집할 때 두 가지 선택 항목인 Windows 또는 Linux가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-180">For example, IntelliSense show you the two choices of Windows or Linux when editing the **targetOsType** element.</span></span>
4. <span data-ttu-id="eed63-181">[git 리포지토리](devtest-lab-add-artifact-repo.md)에 아티팩트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-181">Store the artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="eed63-182">디렉터리 이름이 아티팩트 이름과 동일한 경우 각 아티팩트에 대해 별도의 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-182">Create a separate directory for each artifact where the directory name is the same as the artifact name.</span></span>
   2. <span data-ttu-id="eed63-183">만든 디렉터리에 아티팩트 정의 파일(artifactfile.json)을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-183">Store the artifact definition file (artifactfile.json) in the directory you created.</span></span>
   3. <span data-ttu-id="eed63-184">아티팩트 설치 명령에서 참조된 스크립트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-184">Store the scripts that are referenced from the artifact install command.</span></span>
      
      <span data-ttu-id="eed63-185">다음은 아티팩트 폴더가 표시되는 모습의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![아티팩트 Git 리포지토리 예](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="eed63-187">랩에 아티팩트 리포지토리 추가 - [아티팩트 및 템플릿에 Git 리포지토리 추가](devtest-lab-add-artifact-repo.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eed63-187">Add the artifacts repository to the lab - Refer to the article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="eed63-188">관련 문서</span><span class="sxs-lookup"><span data-stu-id="eed63-188">Related articles</span></span>
* [<span data-ttu-id="eed63-189">DevTest Labs에서 아티팩트 실패를 진단하는 방법</span><span class="sxs-lookup"><span data-stu-id="eed63-189">How to diagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="eed63-190">Azure DevTest Labs에서 리소스 관리자 템플릿을 사용하여 기존 AD 도메인에 VM 가입</span><span class="sxs-lookup"><span data-stu-id="eed63-190">Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="eed63-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eed63-191">Next steps</span></span>
* <span data-ttu-id="eed63-192">[랩에 Git 아티팩트 리포지토리를 추가](devtest-lab-add-artifact-repo.md)하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="eed63-192">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

