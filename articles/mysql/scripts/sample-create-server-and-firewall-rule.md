---
title: "aaa \"Azure CLI 스크립팅-MySQL에 대 한 Azure 데이터베이스 만들기 | \"Microsoft Docs"
description: "이 샘플 CLI 스크립트는 MySQL 서버용 Azure Database를 만들고 서버 수준 방화벽 규칙을 구성합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 1d619ee0547efd8275eaf7c1347b6c3427025c3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="8b5d3-103">MySQL 서버를 만들고 hello Azure CLI를 사용 하는 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="8b5d3-103">Create a MySQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="8b5d3-104">이 샘플 CLI 스크립트는 MySQL 서버용 Azure Database를 만들고 서버 수준 방화벽 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="8b5d3-105">Hello 스크립트 성공적으로 실행 되 면 hello MySQL 서버는 모든 Azure 서비스에서 액세스할 수 및 hello IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-105">Once hello script runs successfully, hello MySQL server is accessible by all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8b5d3-106">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8b5d3-107">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8b5d3-108">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8b5d3-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="8b5d3-109">Sample script</span></span>
<span data-ttu-id="8b5d3-110">이 샘플 스크립트를 강조 표시 하는 hello 줄 toocustomize hello 관리자 사용자 이름 및 암호를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8b5d3-111">배포 정리</span><span class="sxs-lookup"><span data-stu-id="8b5d3-111">Clean up deployment</span></span>
<span data-ttu-id="8b5d3-112">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="8b5d3-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="8b5d3-113">Script explanation</span></span>
<span data-ttu-id="8b5d3-114">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-114">This script uses hello following commands.</span></span> <span data-ttu-id="8b5d3-115">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8b5d3-116">**명령**</span><span class="sxs-lookup"><span data-stu-id="8b5d3-116">**Command**</span></span> | <span data-ttu-id="8b5d3-117">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="8b5d3-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="8b5d3-118">az group create</span><span class="sxs-lookup"><span data-stu-id="8b5d3-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="8b5d3-119">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8b5d3-120">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="8b5d3-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="8b5d3-121">Hello 데이터베이스를 호스팅하는 MySQL 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="8b5d3-122">az mysql server firewall create</span><span class="sxs-lookup"><span data-stu-id="8b5d3-122">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#create) | <span data-ttu-id="8b5d3-123">Hello 입력 한 IP 주소 범위의 방화벽 규칙 tooallow 액세스 toohello 서버 및 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="8b5d3-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="8b5d3-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="8b5d3-125">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8b5d3-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b5d3-126">Next steps</span></span>
- <span data-ttu-id="8b5d3-127">Azure CLI hello에 대 한 자세한 정보를 확인할: [Azure CLI 설명서](/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5d3-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="8b5d3-128">추가 스크립트 시도: [MySQL용 Azure 데이터베이스 대한 Azure CLI 샘플](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="8b5d3-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
