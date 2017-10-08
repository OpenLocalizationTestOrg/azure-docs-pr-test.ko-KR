---
title: "Azure SQL 데이터베이스 aaaCLI 예제-만들기 | Microsoft Docs"
description: "Azure CLI 예제 스크립트 toocreate SQL 데이터베이스"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 0d54e284e19f16387813e24d7beb7ab048a39263
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="586b9-103">CLI toocreate 단일 Azure SQL 데이터베이스를 사용 하 고 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="586b9-103">Use CLI toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="586b9-104">이 Azure CLI 스크립트 예제는 Azure SQL Database를 만들고 서버 수준 방화벽 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="586b9-105">Hello 스크립트 성공적으로 실행 되 면 모든 Azure 서비스에서 SQL 데이터베이스에 액세스할 수는 hello 및 hello IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="586b9-106">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="586b9-107">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="586b9-108">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="586b9-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="586b9-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="586b9-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="586b9-110">Clean up deployment</span></span>

<span data-ttu-id="586b9-111">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-111">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="586b9-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="586b9-112">Script explanation</span></span>

<span data-ttu-id="586b9-113">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-113">This script uses hello following commands.</span></span> <span data-ttu-id="586b9-114">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="586b9-115">명령</span><span class="sxs-lookup"><span data-stu-id="586b9-115">Command</span></span> | <span data-ttu-id="586b9-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="586b9-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="586b9-117">az group create</span><span class="sxs-lookup"><span data-stu-id="586b9-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="586b9-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="586b9-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="586b9-119">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="586b9-120">Hello SQL 데이터베이스를 호스트 하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-120">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="586b9-121">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="586b9-121">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="586b9-122">Hello 입력 한 IP 주소 범위에서 hello 서버의 방화벽 규칙 tooallow 액세스 tooall SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-122">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="586b9-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="586b9-123">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="586b9-124">논리 서버 hello에에서 hello SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-124">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="586b9-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="586b9-125">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="586b9-126">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="586b9-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="586b9-127">Next steps</span></span>

<span data-ttu-id="586b9-128">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="586b9-129">추가 SQL 데이터베이스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 설명서](../sql-database-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="586b9-129">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

