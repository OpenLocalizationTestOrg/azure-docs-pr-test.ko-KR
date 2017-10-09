---
title: "일괄 처리에 대 한 Azure CLI aaaGet 시작 | Microsoft Docs"
description: "간략 한 소개 toohello 일괄 처리의에서 명령을 가져오려면 Azure CLI Azure 배치 서비스 리소스를 관리 하기 위한"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a>Azure CLI를 사용하여 Batch 리소스 관리

hello Azure CLI 2.0은 Azure 리소스 관리를 위해 Azure의 새로운 명령줄 환경입니다. macOS, Linux 및 Windows에서 사용할 수 있습니다. Azure CLI 2.0 hello 명령줄에서 Azure 리소스를 관리 및 관리 하기 위한 최적화 됩니다. Azure 배치 계정 및 toomanage 리소스 풀, 작업, 작업 등 hello Azure CLI toomanage를 사용할 수 있습니다. Azure CLI hello로 다양 한 hello 스크립팅할 수 있습니다 일괄 처리 Api, Azure 포털 및 일괄 처리 PowerShell cmdlet를 실행 하는 동일한 작업 hello 합니다.

이 문서에서는 Batch와 함께 [Azure CLI 버전 2.0](https://docs.microsoft.com/cli/azure/overview)을 사용하는 방법에 대해 간략히 설명합니다. 참조 [Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) hello CLI를 사용 하 여 azure에 대 한 개요입니다.

Hello hello Azure CLI 버전 2.0의 최신 버전을 사용 하는 것이 좋습니다. 버전 2.0에 대한 자세한 내용은 [현재 일반적으로 사용할 수 있는 Azure CLI 2.0](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/)을 참조하세요.

## <a name="set-up-hello-azure-cli"></a>Hello Azure CLI 설정

에 설명 된 hello 단계를 수행 하는 tooinstall hello Azure CLI [설치 hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md)합니다.

> [!TIP]
> Azure CLI 설치를 업데이트 하는 것이 좋습니다 자주 tootake 활용 해도 서비스 업데이트 및 향상 된 기능입니다.
> 
> 

## <a name="command-help"></a>명령 도움말

추가 하 여 hello Azure CLI에에서는 모든 명령에 대 한 도움말 텍스트를 표시할 수 있습니다 `-h` toohello 명령입니다. 다른 모든 옵션은 생략합니다. 예:

* hello에 대 한 도움말 tooget `az` 명령 입력 합니다.`az -h`
* tooget CLI hello에서 모든 일괄 처리 명령의 목록을 사용 합니다.`az batch -h`
* 일괄 처리 계정을 만드는 방법에 대 한 tooget 도움말을 입력 합니다.`az batch account create -h`

의심에서 hello를 사용 하 여 `-h` 모든 Azure CLI 명령에 대 한 명령줄 옵션 tooget 도움말입니다.

> [!NOTE]
> 이전 버전의 hello 사용 되는 Azure CLI `azure` toopreface CLI 명령입니다. 버전 2.0에서는 이제 모든 명령 앞에 `az`를 사용하여 시작합니다. 있는지 tooupdate 버전 2.0과 스크립트 toouse hello 새 구문을 수 있습니다.
>
>  

또한에 대 한 자세한 내용은 toohello Azure CLI 참조 설명서를 참조할 [일괄 처리에 대 한 Azure CLI 명령을](https://docs.microsoft.com/cli/azure/batch)합니다. 

## <a name="log-in-and-authenticate"></a>로그인 및 인증

toouse hello Azure CLI, 일괄 처리에서 toolog 필요 하 고이 인증 합니다. 두 가지 간단한 단계만 거치면 toofollow 가지가 있습니다.

1. **Azure에 로그인합니다.** 포함 하 여 리소스 관리자 tooAzure 명령을 액세스 제공 Azure에 로그인 할 [일괄 처리 관리 서비스](batch-management-dotnet.md) 명령입니다.  
2. **배치 계정에 로그인합니다.** 일괄 처리 계정 제공에 로그인 할 tooBatch 서비스 명령 액세스할 수 있습니다.   

### <a name="log-in-tooazure"></a>TooAzure 로그인

에 자세하게 설명 Azure에 몇 가지 방법으로 toolog 가지 [Azure CLI 2.0 로그인](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):

1. [대화형으로 로그인합니다](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in). 로그인 대화형으로 실행 하는 경우 Azure CLI 명령을 직접 hello 명령줄에서.
2. [서비스 주체를 사용하여 로그인합니다](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal). 스크립트 또는 응용 프로그램에서 Azure CLI 명령을 실행할 때 서비스 주체를 사용하여 로그인합니다.

이 문서의 hello 위해 보여줍니다 어떻게 toolog Azure에 대화형으로 합니다. 형식 [az 로그인](https://docs.microsoft.com/cli/azure/#login) hello 명령줄에서:

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

hello `az login` 명령은 다음과 같이 tooauthenticate를 사용할 수 있는 토큰을 반환 합니다. Hello 제공 된 지침 tooopen 웹 페이지를 따르고 hello 토큰 tooAzure 제출:

![TooAzure 로그인](./media/batch-cli-get-started/az-login.png)

hello에 나열 된 hello 예제 [셸 스크립트 샘플](#sample-shell-scripts) 표시 방법을 섹션도 toostart 대화형으로 Azure에 로그인 하 여 Azure CLI 세션입니다. 로그인 하면 일괄 처리 계정, 키, 응용 프로그램 패키지 및 할당량을 포함 하 여 일괄 처리 관리 리소스와 toowork 명령을 호출할 수 있습니다.  

### <a name="log-in-tooyour-batch-account"></a>일괄 처리 계정 tooyour에 로그인

toouse hello Azure CLI toomanage 일괄 처리와 같은 리소스 풀, 작업, 작업, 일괄 처리 계정에 toolog 필요 하 고 인증 합니다. toolog toohello 일괄 처리 서비스에서에서 사용 하 여 hello [az 일괄 처리 계정 로그인](https://docs.microsoft.com/cli/azure/batch/account#login) 명령입니다. 

배치 계정에 대한 인증에는 다음 두 가지 옵션이 있습니다.

- **Azure AD(Azure Active Directory) 인증 사용** 

    Azure AD를 사용 하 여 인증 hello 기본 hello Azure CLI를 사용 하 여 일괄 처리를 사용 하는 경우 이며 대부분의 시나리오에 대 한 것이 좋습니다. 
    
    TooAzure를 대화형으로 hello 이전 섹션에 설명 된 대로 로그인 할 때 하므로 hello Azure CLI tooyour 동일한 자격 증명을 사용 하 여 일괄 처리 계정 로그인 자격 증명 캐시 됩니다. 서비스 사용자를 사용 하 여 tooAzure 로그인 하면 해당 자격 증명 tooyour 일괄 처리 계정에에서 사용 되는 toolog도 됩니다.

    Azure AD의 이점은 RBAC(역할 기반 액세스 제어)를 제공한다는 것입니다. RBAC는 사용자의 액세스에 따라 달라 집니다 할당된 된 역할 보다 hello 계정 키 소유 해야 할지 여부는 합니다. 계정 키를 관리하는 대신 RBAC 역할을 관리하고 Azure AD에서 액세스와 인증을 처리하도록 할 수 있습니다.  

    Azure AD를 사용 하 여 인증 필수가 만든 경우 해당 풀 할당 모드를 사용 하 여 Azure 배치 계정 설정 too'User 구독 '. 

    Azure AD를 사용 하 여 계정, hello 호출이 tooyour 일괄 처리에서에서 toolog [az 일괄 처리 계정 로그인](https://docs.microsoft.com/cli/azure/batch/account#login) 명령: 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- **공유 키 인증 사용**

    [공유 키 인증](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) 계정 액세스 키 hello에 대 한 tooauthenticate Azure CLI 명령을 사용 하 여 서비스를 배치 합니다.

    스크립트를 만드는 Azure CLI tooautomate 호출 일괄 처리 명령, 공유 키 인증 또는 Azure AD 서비스 사용자를 사용할 수 있습니다. 일부 시나리오에서는 공유 키 인증을 사용하는 것이 서비스 주체를 만드는 것보다 더 간단할 수 있습니다.  

    공유 키 인증을 사용 하 여 toolog 포함 hello `--shared-key-auth` hello 명령줄 옵션에:

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

hello에 나열 된 hello 예제 [셸 스크립트 샘플](#sample-shell-scripts) 섹션 toolog 일괄 처리 계정에 모두 사용 하 여 Azure CLI hello 하는 방법을 보여 줍니다. Azure AD와 공유 키입니다.

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Azure Batch CLI 템플릿 및 파일 전송 사용(미리 보기)

Hello Azure CLI toorun 일괄 처리 작업에 종단 간 코드를 작성 하지 않고도 사용할 수 있습니다. 일괄 처리 템플릿 파일 만드는 풀, 작업, 및 hello Azure CLI를 사용 하 여 작업을 지원합니다. Hello Azure CLI tooupload 작업 입력된 파일을 사용할 수도 있습니다 toohello Azure 저장소 계정을 hello와 연결 된 일괄 처리 계정을, 및에서 작업 출력 파일을 다운로드 합니다. 자세한 내용은 [Azure Batch CLI 템플릿 및 파일 전송 사용(미리 보기)](batch-cli-templates.md)을 참조하세요.

## <a name="sample-shell-scripts"></a>샘플 셸 스크립트

hello 일괄 처리 서비스 및 일괄 처리 관리 서비스 tooaccomplish 일반적인 작업으로 toouse Azure CLI 명령을 하는 방법을 hello 테이블 표시 뒤에 나열 된 hello 예제 스크립트. 이 샘플 스크립트 다양 한 일괄 처리에 대 한 Azure CLI hello에서 사용할 수 있는 hello 명령을 설명합니다. 

| 스크립트 | 참고 사항 |
|---|---|
| [배치 계정 만들기](./scripts/batch-cli-sample-create-account.md) | 배치 계정을 만들고 저장소 계정과 연결합니다. |
| [응용 프로그램 추가](./scripts/batch-cli-sample-add-application.md) | 응용 프로그램을 추가하고 패키지된 이진 파일을 업로드합니다.|
| [Batch 풀 관리](./scripts/batch-cli-sample-manage-pool.md) | 풀을 만들고, 크기 조정하며, 관리하는 방법을 보여 줍니다. |
| [Batch로 작업 및 태스크 실행](./scripts/batch-cli-sample-run-job.md) | 작업 실행 및 태스크 추가를 보여 줍니다. |

## <a name="json-files-for-resource-creation"></a>리소스를 만들기 위한 JSON 파일

풀 및 작업 같은 일괄 처리 리소스를 만들 때에 명령줄 옵션으로 해당 매개 변수를 전달 하는 대신 hello 새 리소스의 구성이 포함 된 JSON 파일을 지정할 수 있습니다. 예:

```azurecli
az batch pool create my_batch_pool.json
```

명령줄 옵션에만 사용 하 여 대부분의 일괄 처리 리소스를 만들 수 있지만 hello 리소스 세부 정보를 포함 하는 JSON 형식의 파일을 지정 하는 일부 기능이 필요 합니다. 예를 들어 시작 작업에 대 한 리소스 파일 toospecify JSON 파일을 사용 해야 합니다.

JSON 구문 toosee hello 필수 toocreate 리소스, toohello 참조 [배치 REST API 참조] [ rest_api] 설명서입니다. 각 "추가 *리소스 종류*" hello REST API 참조의에서 항목을 해당 리소스를 만들기 위한 샘플 JSON 스크립트를 포함 합니다. JSON 파일 toouse hello Azure CLI로에 대 한 템플릿으로 이러한 샘플 JSON 스크립트를 사용할 수 있습니다. 예를 들어 너무 toosee hello 풀 만들기에 대 한 JSON 구문을 참조[풀 tooan 계정 추가][rest_add_pool]합니다.

JSON 파일을 지정하는 샘플 스크립트는 [Batch로 작업 및 태스크 실행](./scripts/batch-cli-sample-run-job.md)을 참조하세요.

> [!NOTE]
> 리소스를 만들 때 JSON 파일을 지정 하는 경우 해당 리소스에 대 한 hello 명령줄에서 지정 하는 다른 매개 변수는 무시 됩니다.
> 
> 

## <a name="efficient-queries-for-batch-resources"></a>Batch 리소스에 대한 효율적 쿼리

각 Batch 리소스 유형은 배치 계정을 쿼리하고 해당 형식의 리소스를 나열하는 `list` 명령을 지원합니다. 예를 들어 hello 풀에서 작업 계정 및 hello 작업에 나열할 수 있습니다.

```azurecli
az batch pool list
az batch task list --job-id job001
```

Hello 일괄 처리 서비스를 쿼리할 때는 `list` 작업에서 반환 된 데이터는 OData 절 toolimit hello 양을 지정할 수 있습니다. 모든 필터링 서버 쪽 나타나므로 요청 hello 데이터만 hello 와이어를 교차 합니다. 이러한 절 toosave 대역폭을 사용 하 여 (및 따라서 시간) 목록 작업을 수행 하는 경우.

hello 다음 표에서 설명 hello 일괄 처리 서비스에서 지 원하는 hello OData 절:

| 절 | 설명 |
|---|---|
| `--select-clause [select-clause]` | 각 엔터티에 대한 속성의 하위 집합을 반환합니다. |
| `--filter-clause [filter-clause]` | Hello와 일치 하는 엔터티만 반환 OData 식 지정. |
| `--expand-clause [expand-clause]` | 단일 기본 REST 호출의 hello 엔터티 정보를 가져옵니다. hello 확장 지원만 hello 현재을 절 `stats` 속성입니다. |

샘플 toouse OData 절을 참조 하는 방법을 보여 줍니다 해당 스크립트에 대 한 [일괄 처리 작업 및 작업을 실행](./scripts/batch-cli-sample-run-job.md)합니다.

OData 절과 함께 효율적인 목록 쿼리 수행에 대 한 자세한 내용은 참조 하십시오. [hello Azure 배치 서비스를 효율적으로 쿼리](batch-efficient-list-queries.md)합니다.

## <a name="troubleshooting-tips"></a>문제 해결 팁

hello 다음 사항을 참고 Azure CLI 문제를 해결 하는 경우:

* 사용 하 여 `-h` tooget **도움말 텍스트** 모든 CLI 명령에 대 한
* 사용 하 여 `-v` 및 `-vv` toodisplay **verbose** 출력 명령입니다. Hello 때 `-vv` 플래그를 포함 hello Azure CLI hello 실제 REST 요청 및 응답이 표시 됩니다. 이러한 스위치는 전체 오류 출력을 표시하는 데 유용합니다.
* 볼 수 있습니다 **JSON으로 출력 명령** hello로 `--json` 옵션입니다. 예를 들어 `az batch pool show pool001 --json` 은 JSON 형식으로 pool001의 속성을 표시합니다. 그런 다음 복사 하 고 수정할 수에서이 출력 toouse는 `--json-file` (참조 [JSON 파일](#json-files) 이 문서의 앞부분에).
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* hello [배치 포럼] [ batch_forum] 일괄 처리 팀 구성원이 모니터링 됩니다. 문제가 발생하거나 특정 작업에 도움이 필요한 경우 질문을 여기에 게시할 수 있습니다.

## <a name="next-steps"></a>다음 단계

* Azure CLI hello에 대 한 자세한 내용은 참조 hello [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.
* Batch 리소스에 대한 자세한 내용은 [개발자를 위한 Azure Batch 개요](batch-api-basics.md)를 참조하세요.
* 일괄 처리 템플릿 toocreate 풀, 작업 및 작업을 사용 하 여 코드를 작성 하지 않고도 하는 방법에 대 한 자세한 내용은 참조 [Azure 일괄 처리 CLI 템플릿 및 파일 전송 (미리 보기)](batch-cli-templates.md)합니다.

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
