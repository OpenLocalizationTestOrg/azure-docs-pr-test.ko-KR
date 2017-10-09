---
title: "aaaUse Azure 일괄 처리 Api와 도구 toodevelop 대규모 병렬 처리 솔루션 | Microsoft Docs"
description: "Hello Api 및 hello Azure 배치 서비스를 사용 하 여 솔루션을 개발 하는 데 사용할 수 있는 도구에 알아봅니다."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: tamram
ms.openlocfilehash: ca75a1a63b3e7e6b0805e79a63685bc49aaaca8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-batch-apis-and-tools"></a>Batch API 및 도구 개요

Azure 일괄 처리를 사용 하 여 병렬 작업 처리는 일반적으로 수행 프로그래밍 방식으로 hello 중 하나를 사용 하 여 [일괄 처리 Api](#batch-development-apis)합니다. 클라이언트 응용 프로그램 또는 서비스 일괄 처리 서비스 hello로 hello 일괄 처리 Api toocommunicate를 사용할 수 있습니다. 일괄 처리 Api hello로 만들어 하 풀 계산 노드 관리 가상 컴퓨터 또는 클라우드 서비스 중 하나입니다. 그런 다음 이러한 노드에서 toorun 작업 및 작업을 예약할 수 있습니다. 

효율적으로 조직에 대 한 대규모 작업 부하를 처리 하거나 서비스 프런트 엔드 tooyour 고객은 실행 될 수 있도록 작업 및 작업-요청 시 또는 일정에 따라-하나, 수백 또는 수천 개의 노드에 제공 합니다. 또한 [Azure Data Factory](../data-factory/data-factory-data-processing-using-batch.md?toc=%2fazure%2fbatch%2ftoc.json)와 같은 도구에서 관리하는 대규모 워크플로의 일부로 Azure 배치를 사용할 수도 있습니다.

> [!TIP]
> 준비가 끝나면 toohello 배치 API에서에서 toodig hello에 대 한 더 자세히 이해 기능에 대 한, 제공 hello를 확인해 보세요 [개발자를 위한 일괄 처리 기능 개요](batch-api-basics.md)합니다.
> 
> 

## <a name="azure-accounts-for-batch-development"></a>Batch 개발을 위한 Azure 계정
일괄 처리 솔루션을 개발할 때 다음 계정을 Microsoft Azure의 hello를 사용 합니다.

* **Azure 계정 및 구독** - Azure 구독이 없는 경우 [MSDN 구독자 혜택][msdn_benefits]을 활성화하거나 [무료 Azure 계정][free_account]을 등록할 수 있습니다. 계정을 만들면 기본 구독이 생성됩니다.
* **배치 계정** - 풀, 계산 노드, 작업 및 태스크를 포함하여 Azure 배치 리소스는 Azure 배치 계정과 연결됩니다. 응용 프로그램에서 일괄 처리 서비스 hello에 대 한 요청을 hello 요청 hello Azure 배치 계정 이름, hello 계정의 hello URL 및 액세스 키를 사용 하 여 인증 합니다. 있습니다 수 [일괄 처리 계정 만들기](batch-account-create-portal.md) hello Azure 포털의에서.
* **저장소 계정** - 배치는 [Azure Storage][azure_storage]에 있는 파일에 대한 작업을 기본적으로 지원합니다. 작업을 실행 하는 hello 프로그램 및 처리 하는 hello 데이터를 준비 하 고 hello 생성 하는 출력 데이터를 저장 하기 위한 거의 모든 일괄 처리 시나리오에서 Azure Blob 저장소를 사용 합니다. 저장소 계정 toocreate 참조 [에 대 한 Azure 저장소 계정](../storage/common/storage-create-storage-account.md)합니다.

## <a name="batch-service-apis"></a>Batch 서비스 API

응용 프로그램 및 서비스 수 직접 REST API 호출을 실행 하거나 hello 클라이언트 라이브러리 toorun 다음 중 하나 이상을 사용 하 여 고 Azure 일괄 처리 작업을 관리 합니다.

| API | API 참조 | 다운로드 | 자습서 | 코드 샘플 | 자세한 정보 |
| --- | --- | --- | --- | --- | --- |
| **Batch REST** |[MSDN][batch_rest] |해당 없음 |- |- | [지원되는 버전](https://docs.microsoft.com/rest/api/batchservice/batch-service-rest-api-versioning) |
| **Batch .NET** |[docs.microsoft.com][api_net] |[NuGet ][api_net_nuget] |[자습서](batch-dotnet-get-started.md) |[GitHub][api_sample_net] | [릴리스 정보](http://aka.ms/batch-net-dataplane-changelog) |
| **배치 Python** |[readthedocs.io][api_python] |[PyPI][api_python_pypi] |[자습서](batch-python-tutorial.md)|[GitHub][api_sample_python] | [추가 정보](https://github.com/Azure/azure-sdk-for-python/blob/master/doc/batch.rst) |
| **Batch Node.js** |[github.io][api_nodejs] |[npm][api_nodejs_npm] |- |- | [추가 정보](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/batch) |
| **Batch Java** |[github.io][api_java] |[Maven][api_java_jar] |- |[추가 정보][api_sample_java] | [추가 정보](https://github.com/Azure/azure-batch-sdk-for-java)|

## <a name="batch-management-apis"></a>Batch 관리 API

일괄 처리에 대 한 Azure 리소스 관리자 Api hello tooBatch 계정을 프로그래밍 방식의 액세스를 제공 합니다. 이러한 API를 사용하면 배치 계정, 할당량 및 응용 프로그램 패키지를 프로그래밍 방식으로 관리할 수 있습니다.  

| API | API 참조 | 다운로드 | 자습서 | 코드 샘플 |
| --- | --- | --- | --- | --- |
| **배치 Resource Manager REST** |[docs.microsoft.com][api_rest_mgmt] |해당 없음 |- |[GitHub](https://github.com/Azure-Samples/batch-dotnet-manage-batch-accounts) |
| **배치 Resource Manager .NET** |[docs.microsoft.com][api_net_mgmt] |[NuGet ][api_net_mgmt_nuget] | [자습서](batch-management-dotnet.md) |[GitHub][api_sample_net] |

## <a name="batch-command-line-tools"></a>Batch 명령줄 도구

이 명령줄 도구를 제공 일괄 처리 서비스 및 일괄 처리 관리 Api hello 처럼 동일한 기능을 hello: 

* [PowerShell cmdlet을 일괄 처리][batch_ps]: hello의 Azure 배치 cmdlet hello [Azure PowerShell](/powershell/azure/overview) 모듈 PowerShell 사용 하 여 toomanage 일괄 처리 리소스를 사용 합니다.
* [Azure CLI](/cli/azure/overview): hello Azure CLI (명령줄 인터페이스 Azure) hello 일괄 처리 서비스 및 일괄 처리 관리 서비스를 포함 하 여 여러 Azure 서비스와 상호 작용 하기 위한 셸 명령을 제공 하는 플랫폼 도구 집합입니다. 참조 [Azure CLI를 사용 하 여 일괄 처리 관리 리소스](batch-cli-get-started.md) hello Azure CLI를 사용 하 여 일괄 처리 하는 방법에 대 한 자세한 내용은 합니다.

## <a name="other-tools-for-application-development"></a>응용 프로그램 개발을 위한 기타 도구

Batch 응용 프로그램 및 서비스를 빌드 및 디버깅하는 데 도움이 될 수 있는 추가 도구는 다음과 같습니다.

* [Azure 포털][portal]: 만들기, 모니터링 및 일괄 처리 풀, 작업, 및 hello Azure에서에서 작업을 삭제 합니다. 포털의 일괄 처리 블레이드입니다. 작업을 실행 하 고도 풀에 hello 계산 노드에서 파일을 다운로드 하는 동안 이러한 오류 코드 및 기타 리소스에 대 한 hello 상태 정보를 볼 수 있습니다. 예를 들어 문제를 해결하는 동안 실패한 작업의 `stderr.txt`를 다운로드할 수 있습니다. 또한 toolog toocompute 노드에서 사용할 수 있는 원격 데스크톱 (RDP) 파일을 다운로드할 수 있습니다.
* [Azure 일괄 처리 탐색기][batch_explorer]: 일괄 처리 탐색기는 Azure 포털 hello 하지만 독립 실행형 Windows Presentation Foundation (WPF) 클라이언트 응용 프로그램에서에서 비슷한 일괄 처리 리소스 관리 기능을 제공 합니다. Hello 일괄 처리.NET 예제 응용 프로그램 중 하나에서 사용할 수 있는 [GitHub][github_samples], Visual Studio 2015와 함께 또는 최신 빌드 및 toobrowse 사용 하 고 개발 하는 동안 일괄 처리 계정에 hello 리소스를 관리할 수 있습니다 고 일괄 처리 솔루션을 디버깅 합니다. 작업 보기, 풀 및 작업 세부 정보 계산 노드에서 파일을 다운로드 하 고 일괄 처리 탐색기와 RDP (원격 데스크톱) 파일을 다운로드할 수 있습니다를 사용 하 여 toonodes를 원격으로 연결 합니다.
* [Microsoft Azure 저장소 탐색기][storage_explorer]: Azure 배치 도구 하지 엄격 하 게 하는 동안 hello 저장소 탐색기는 또 다른 중요 한 도구 toohave 개발 하 고 일괄 처리 솔루션을 디버깅 하는 동안 합니다.

## <a name="additional-resources"></a>추가 리소스

- 일괄 처리 응용 프로그램에서 이벤트를 기록 하는 방법에 대 한 toolearn 참조 [진단 평가 및 일괄 처리 솔루션의 모니터링에 대 한 이벤트 로그](batch-diagnostics.md)합니다. Hello 일괄 처리 서비스에서 발생 한 이벤트에 대 한 참조를 참조 하십시오. [일괄 처리 분석](batch-analytics.md)합니다.
- 계산 노드의 환경 변수에 대한 정보는 [Azure Batch 계산 노드 환경 변수](batch-compute-node-environment-variables.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

* 읽기 hello [개발자를 위한 일괄 처리 기능 개요](batch-api-basics.md), toouse 일괄 처리를 준비 하 고 모든 사용자에 대 한 필수 정보입니다. hello 문서 풀, 노드, 작업 및 작업, 및 hello와 같은 일괄 처리 서비스 리소스에 대 한 자세한 내용은 일괄 처리 응용 프로그램을 작성 하는 동안 사용할 수 있는 많은 API 기능을 포함 합니다.
* [.NET 용 hello Azure 배치 라이브러리 시작](batch-dotnet-get-started.md) toolearn 어떻게 toouse C# hello 일괄 처리.NET 라이브러리 tooexecute 단순 작업 일반 일괄 처리 워크플로 사용 하 고 있습니다. 이 문서를 사용 하면 첫 번째 중단할 toouse 일괄 처리 서비스 hello 하는 방법을 학습 하는 동안 중 하나 여야 합니다. 또한 한 [Python 버전](batch-python-tutorial.md) hello 자습서입니다.
* Hello 다운로드 [코드 샘플 GitHub에서] [ github_samples] toosee C# 및 Python 일괄 처리 tooschedule 및 프로세스 샘플 작업 부하와 상호 작용할 수 있는 방법입니다.
* 체크 아웃 hello [일괄 학습 경로] [ learning_path] 일괄 처리와 toowork tooget hello 때 사용할 수 있는 tooyou 리소스의 개념에 알아봅니다.


[azure_storage]: https://azure.microsoft.com/services/storage/
[api_java]: http://azure.github.io/azure-sdk-for-java/
[api_java_jar]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-batch%22
[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_nuget]: https://www.nuget.org/packages/Azure.Batch/
[api_rest_mgmt]: https://docs.microsoft.com/\rest/api/batchmanagement/
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_net_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[api_nodejs]: http://azure.github.io/azure-sdk-for-node/azure-batch/latest/
[api_nodejs_npm]: https://www.npmjs.com/package/azure-batch
[api_python]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html
[api_python_pypi]: https://pypi.python.org/pypi/azure-batch
[api_sample_net]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp
[api_sample_python]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[api_sample_java]: https://github.com/Azure/azure-batch-samples/tree/master/Java/
[batch_ps]: /powershell/resourcemanager/azurerm.batch/v2.7.0/azurerm.batch
[batch_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[free_account]: https://azure.microsoft.com/free/
[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[msdn_benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[storage_explorer]: http://storageexplorer.com/
[portal]: https://portal.azure.com
