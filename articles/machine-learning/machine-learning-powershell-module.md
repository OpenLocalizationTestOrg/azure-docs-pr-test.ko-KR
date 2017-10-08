---
title: "기계 학습 모듈 aaaPowerShell | Microsoft Docs"
description: "Azure 기계 학습에 대 한 hello PowerShell 모듈은 공개 미리 보기 모드에서 사용할 수 있습니다. PowerShell toocreate를 사용 하 고 작업 영역, 실험, 웹 서비스 등을 관리 합니다."
keywords: "실험, 선형 회귀, 기계 학습 알고리즘, 기계 학습 자습서, 예측 모델링 기술, 데이터 과학 실험"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: a9001cc2-3aa0-47e1-b175-1f76408ba1d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: garye;haining
ms.openlocfilehash: 59362027356b86bf286b7c07380db677ae1d71c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a>Microsoft Azure 기계 학습용 PowerShell 모듈
Azure 기계 학습에 대 한 PowerShell 모듈 hello는 toouse Windows PowerShell toomanage 작업 영역, 실험, 데이터 집합, 기본 웹 서비스 등 수 있는 강력한 도구입니다.

Hello 설명서를 볼 수 있으며에서 hello 전체 소스 코드와 함께 hello 모듈을 다운로드 [https://aka.ms/amlps](https://aka.ms/amlps)합니다. 

> [!NOTE]
> hello Azure 컴퓨터 학습 PowerShell 모듈은 현재 미리 보기 모드입니다. hello 모듈 toobe를 개선 하 고이 미리 보기 기간 중에 확장을 계속 합니다. Hello 예의 주시 [Cortana 인텔리전스 및 기계 학습 블로그](https://blogs.technet.microsoft.com/machinelearning/) 뉴스 및 정보에 대 한 합니다.

## <a name="what-is-hello-machine-learning-powershell-module"></a>Hello 컴퓨터 학습 PowerShell 모듈 이란?
hello 컴퓨터 학습 PowerShell 모듈은는 합니다. .NET 기반 DLL 모듈을 toofully 수 있는 Windows PowerShell에서 Azure 기계 학습 작업 영역, 실험, 데이터 집합, 기본 웹 서비스 및 기본 웹 서비스 끝점을 관리 합니다. 

Hello 모듈과 함께 완전히 분리 된 포함 된 hello 전체 소스 코드를 다운로드할 수 있습니다 [C# API 계층](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs)합니다. 고유한 .NET 프로젝트에서 이 DLL을 참조하고 .NET 코드를 통해 Azure Machine Learning을 관리할 수 있습니다. 또한 hello DLL 자주 사용 하는 클라이언트에서 직접 사용할 수 있는 기본 REST Api에 따라 달라 집니다.

## <a name="what-can-i-do-with-hello-powershell-module"></a>Hello PowerShell 모듈과 함께 어떻게 해야 합니까?
다음은이 PowerShell 모듈 수행할 수 있는 hello 작업의 일부입니다. 체크 아웃 hello [설명서 전체](https://aka.ms/amlps) 이 함수 및 더 많은 기능입니다.

* 관리 인증서를 사용한 새 작업 영역 프로비전([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))
* 실험 그래프를 나타내는 JSON 파일을 내보내기 및 가져오기([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) 및 [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))
* 실험 실행([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))
* 예측 실험에서 웹 서비스 만들기([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))
* 게시된 웹 서비스에 끝점 만들기([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))
* RRS 또는 BES 웹 서비스 끝점 호출([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) 및 [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))

다음은 PowerShell toorun 기존 실험을 사용 하는 빠른 예제가입니다.

        #Find hello first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run hello Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

자세한 사용 사례에 대 한 hello PowerShell 모듈 tooautomate 일반적으로 요청 되는 작업을 사용 하 여에이 문서를 참조: [PowerShell을 사용 하 여 하나의 실험에서 많은 기계 학습 모델 및 웹 서비스 엔드포인트를 만들](machine-learning-create-models-and-endpoints-with-powershell.md)합니다.

## <a name="how-do-i-get-started"></a>어떻게 시작하나요?
tooget 컴퓨터 학습 PowerShell을 시작, hello 다운로드 [릴리스 패키지](https://github.com/hning86/azuremlps/releases) GitHub 및 따라 hello에서 [설치에 대 한 지침](https://github.com/hning86/azuremlps/blob/master/README.md)합니다. hello 명령은 방법을 toounblock hello 다운로드/압축을 푼 DLL에 설명 하 고 PowerShell 환경으로 가져옵니다. 대부분의 cmdlet에서는 hello 작업 영역 ID, hello 작업 영역 인증 토큰을 제공 하 고 작업 영역을 hello Azure 지역 hello hello는 합니다. hello 가장 간단한 방법은 tooprovide hello 값 기본 config.json 파일을 통해 수행 됩니다. hello 지침 또한 설명 어떻게 tooconfigure이이 파일입니다. 

및를 hello git 트리 복제, hello 코드를 수정 하 고 컴파일할 수 Visual Studio를 사용 하 여 로컬로 합니다.

## <a name="next-steps"></a>다음 단계
Hello에 hello PowerShell 모듈에 대 한 전체 설명서를 찾을 수 있습니다 [https://aka.ms/amlps](https://aka.ms/amlps)합니다. 

체크 아웃 hello 심층 분석 방법을 toouse hello 실제 시나리오에서 모듈의 확장된 된 예제에 대 한 사용 사례를 [PowerShell을 사용 하 여 하나의 실험에서 많은 기계 학습 모델 및 웹 서비스 엔드포인트를 만들](machine-learning-create-models-and-endpoints-with-powershell.md)합니다.
