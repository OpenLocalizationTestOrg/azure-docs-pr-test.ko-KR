---
title: "Azure CLI 스크립트 - MySQL용 Azure 데이터베이스 만들기 | Microsoft Docs"
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
ms.openlocfilehash: 201db294ce362ef3e09cbe62f48bd51c8ea94dbb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="5a521-103">Azure CLI를 사용하여 MySQL 서버 만들기 및 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="5a521-103">Create a MySQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="5a521-104">이 샘플 CLI 스크립트는 MySQL 서버용 Azure Database를 만들고 서버 수준 방화벽 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5a521-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="5a521-105">스크립트가 성공적으로 실행되면 모든 Azure 서비스 및 구성된 IP 주소에서 MySQL 서버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a521-105">Once the script runs successfully, the MySQL server is accessible by all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5a521-106">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a521-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5a521-107">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5a521-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="5a521-108">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a521-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5a521-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="5a521-109">Sample script</span></span>
<span data-ttu-id="5a521-110">이 샘플 스크립트에서 강조 표시된 줄을 편집하여 관리자 사용자 이름 및 암호를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a521-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="5a521-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "MySQL용 Azure 데이터베이스 및 서버 수준 방화벽 규칙을 만듭니다.")]</span><span class="sxs-lookup"><span data-stu-id="5a521-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5a521-112">배포 정리</span><span class="sxs-lookup"><span data-stu-id="5a521-112">Clean up deployment</span></span>
<span data-ttu-id="5a521-113">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a521-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="5a521-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "리소스 그룹을 삭제합니다.")]</span><span class="sxs-lookup"><span data-stu-id="5a521-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="5a521-115">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="5a521-115">Script explanation</span></span>
<span data-ttu-id="5a521-116">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a521-116">This script uses the following commands.</span></span> <span data-ttu-id="5a521-117">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a521-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5a521-118">**명령**</span><span class="sxs-lookup"><span data-stu-id="5a521-118">**Command**</span></span> | <span data-ttu-id="5a521-119">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="5a521-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="5a521-120">az group create</span><span class="sxs-lookup"><span data-stu-id="5a521-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="5a521-121">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a521-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5a521-122">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="5a521-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="5a521-123">데이터베이스를 호스팅하는 MySQL 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a521-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="5a521-124">az mysql server firewall create</span><span class="sxs-lookup"><span data-stu-id="5a521-124">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#create) | <span data-ttu-id="5a521-125">입력한 IP 주소 범위의 서버에서 서버 및 서버의 데이터베이스에 액세스할 수 있도록 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a521-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="5a521-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="5a521-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="5a521-127">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5a521-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5a521-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5a521-128">Next steps</span></span>
- <span data-ttu-id="5a521-129">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a521-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="5a521-130">추가 스크립트 시도: [MySQL용 Azure 데이터베이스 대한 Azure CLI 샘플](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="5a521-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
