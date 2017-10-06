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
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a>DevTest Lab VM에 대한 사용자 지정 아티팩트 만들기
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a>개요
**아티팩트** 사용 되는 toodeploy 되며 VM 프로 비전 된 후 응용 프로그램을 구성 합니다. 아티팩트는 Git 리포지토리의 폴더에 저장되어 있는 아티팩트 정의 파일 및 다른 스크립트 파일로 구성됩니다. JSON 및 식을 사용할 수 있는 toospecify 수행할 아티팩트 정의 파일 구성 VM에서 tooinstall 합니다. 예를 들어 hello 이름 아티팩트, 명령 toorun 및 hello 명령을 실행할 때 사용할 수 있는 매개 변수를 정의할 수 있습니다. 이름으로 hello 아티팩트 정의 파일 내에서 tooother 스크립트 파일을 참조할 수 있습니다.

## <a name="artifact-definition-file-format"></a>아티팩트 정의 파일 형식
hello 다음 예제는 hello 정의 파일의 기본 구조를 구성 하는 hello 섹션.

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

| 요소 이름 | Required? | 설명 |
| --- | --- | --- |
| $schema |아니요 |Hello 정의 파일의 hello 유효성 테스트에 도움이 되는 hello JSON 스키마 파일의 위치입니다. |
| title |예 |Hello 랩에 표시 된 hello 아티팩트의 이름입니다. |
| 설명 |예 |Hello 랩에 표시 된 hello 아티팩트에 대 한 설명입니다. |
| iconUri |아니요 |Hello 랩에 표시 된 hello 아이콘의 Uri입니다. |
| targetOsType |예 |Hello 아티팩트를 설치한 VM의 운영 체제입니다. 지원되는 옵션은 Windows 및 Linux입니다. |
| 매개 변수 |아니요 |아티팩트 설치 명령이 컴퓨터에서 실행될 때 제공되는 값으로 아티팩트를 사용자 지정하는 데 도움이 됩니다. |
| runCommand |예 |VM에서 실행되는 아티팩트 설치 명령입니다. |

### <a name="artifact-parameters"></a>아티팩트 매개 변수
Hello hello 정의 파일의 매개 변수 섹션에서 아티팩트를 설치 하는 경우는 사용자가 입력할 수 있는 값을 지정 합니다. Hello 아티팩트 설치 명령에 toothese 값을 참조할 수 있습니다.

구조를 다음 hello로 매개 변수를 정의 합니다.

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| 요소 이름 | Required? | 설명 |
| --- | --- | --- |
| type |예 |매개 변수 값의 형식입니다. Hello hello 허용 되는 형식에 대 한 목록을 다음을 참조 하십시오. |
| displayName |예 |Hello 매개 변수 hello 랩의 표시 된 tooa 사용자의 이름입니다. | |
| 설명 |예 |설명 hello 랩에 표시 되는 hello 매개 변수입니다. |

hello 유형은 허용:

* 문자열 - 유효한 모든 JSON 문자열
* int - 유효한 모든 JSON 정수
* bool - 유효한 모든 JSON 부울
* array - 유효한 모든 JSON 배열

## <a name="artifact-expressions-and-functions"></a>아티팩트 식 및 함수
식을 사용할 수 있습니다 및 함수 tooconstruct hello 아티팩트 명령을 설치 합니다.
식은 대괄호로 묶여 ([및]), hello 아티팩트 설치 될 때 평가 됩니다. 식은 JSON 문자열 값에서 어느 위치에나 나타날 수 있으며 항상 다른 JSON 값을 반환합니다. Toouse 대괄호가로 시작 하는 리터럴 문자열을 필요한 경우 [, 두 개의 대괄호를 사용 해야 합니다 [[합니다.
일반적으로 식을 함수 tooconstruct 값을 사용 합니다. JavaScript에서와 마찬가지로 함수 호출은 functionName(arg1,arg2,arg3)으로 형식이 지정됩니다.

hello 다음은 일반 함수.

* parameters(parameterName)-hello 아티팩트 명령이 실행 될 때 제공 되는 매개 변수 값을 반환 합니다.
* concat(arg1,arg2,arg3, …..) - 여러 문자열 값을 결합합니다. 이 함수는 임의의 수의 인수를 사용할 수 있습니다.

hello 방법을 예제와 다음 toouse 식과 함수 tooconstruct 값:

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a>사용자 지정 아티팩트 만들기
다음 단계를 수행하여 사용자 지정 아티팩트를 만듭니다.

1. JSON 편집기를 설치 하-JSON 편집기 toowork 아티팩트 정의 파일을 사용 해야 합니다. Windows, Linux 및 OS X에 사용할 수 있는 [Visual Studio Code](https://code.visualstudio.com/)를 사용하는 것이 좋습니다.
2. Get에서 DevTest Labs Azure 팀에서 만든 샘플 artifactfile.json-체크 아웃 hello 아티팩트 우리의 [GitHub 리포지토리](https://github.com/Azure/azure-devtestlab)풍부한 라이브러리 만들어졌습니다. 여기서 아티팩트 수 있는 사용자 고유의 아티팩트를 만듭니다. 아티팩트 정의 파일을 다운로드 하 고 변경 내용을 tooit toocreate 사용자 고유의 아티팩트를 확인 합니다.
3. 아티팩트 정의 파일에는 intellisense-tooconstruct 사용된 될 수 있는 활용 IntelliSense toosee 유효한 요소 사용을 확인 합니다. Hello 다양 한 옵션 값에 대 한 요소를 볼 수 있습니다. 예를 들어 IntelliSense 표시 hello를 편집 하는 경우 Windows 또는 Linux의 두 가지 선택 hello **targetOsType** 요소입니다.
4. 저장소 hello 아티팩트는 [git 리포지토리](devtest-lab-add-artifact-repo.md)합니다.
   
   1. 여기서 hello 디렉터리 이름을 hello 동일 hello 아티팩트 이름으로 각 아티팩트에 대 한 별도 디렉터리를 만듭니다.
   2. Hello 아티팩트 정의 파일 (artifactfile.json) 만든 hello 디렉터리에 저장 합니다.
   3. Hello 아티팩트에서 참조 되는 저장소 hello 스크립트 명령을 설치 합니다.
      
      다음은 아티팩트 폴더가 표시되는 모습의 예입니다.
      
      ![아티팩트 Git 리포지토리 예](./media/devtest-lab-artifact-author/git-repo.png)
5. Hello 아티팩트 저장소 toohello 랩 추가-toohello 문서 참조 [아티팩트 및 템플릿에 대 한 Git 리포지토리를 추가](devtest-lab-add-artifact-repo.md)합니다.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a>관련 문서
* [어떻게 DevTest Labs의 toodiagnose 아티팩트 오류](devtest-lab-troubleshoot-artifact-failure.md)
* [VM tooexisting Azure DevTest Labs에서 리소스 관리자 템플릿을 사용 하는 AD 도메인 가입](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[Git 아티팩트 저장소 tooa 랩 추가](devtest-lab-add-artifact-repo.md)합니다.

