---
title: "MySQL에 대 한 Azure 데이터베이스에 대 한 응용 프로그램 개발 개요 aaaDatabase | Microsoft Docs"
description: "개발자는 MySQL에 대 한 응용 프로그램 코드 tooconnect tooAzure 데이터베이스를 작성할 때 따라야 하는 디자인 고려 사항을 소개합니다"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="0077f-103">MySQL용 Azure 데이터베이스에 대한 응용 프로그램 개발 개요</span><span class="sxs-lookup"><span data-stu-id="0077f-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="0077f-104">이 문서에서는 개발자 MySQL에 대 한 응용 프로그램 코드 tooconnect tooAzure 데이터베이스를 작성할 때 따라야 하는 설계 고려 사항</span><span class="sxs-lookup"><span data-stu-id="0077f-104">This article discusses design considerations that a developer should follow when writing application code tooconnect tooAzure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="0077f-105">방법 toocreate는 서버에서 서버 기반 방화벽 만듭니다 서버 속성 보기, 데이터베이스 만들기, 연결 하 mysql.exe 및 워크 벤치를 사용 하 여 쿼리 표시는 자습서를 참조 하세요. [첫 번째 Azure의 MySQL 데이터베이스 디자인](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0077f-105">For a tutorial showing you how toocreate a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="0077f-106">언어 및 플랫폼</span><span class="sxs-lookup"><span data-stu-id="0077f-106">Language and platform</span></span>
<span data-ttu-id="0077f-107">다양한 프로그래밍 언어 및 플랫폼에 대한 코드 샘플을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0077f-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="0077f-108">Toohello 코드 샘플에서 링크를 찾을 수 있습니다: [MySQL 용 tooconnect tooAzure 데이터베이스를 사용 하는 연결 라이브러리](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="0077f-108">You can find links toohello code samples at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="0077f-109">도구</span><span class="sxs-lookup"><span data-stu-id="0077f-109">Tools</span></span>
<span data-ttu-id="0077f-110">MySQL에 대 한 azure 데이터베이스 사용 hello MySQL community 버전, MySQL, mysql.exe 같은 워크 벤치 또는 MySQL 유틸리티와 같은 일반 관리 도구와 호환 [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), 등입니다.</span><span class="sxs-lookup"><span data-stu-id="0077f-110">Azure Database for MySQL uses hello MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="0077f-111">또한 hello Azure 포털, Azure CLI 및 REST Api toointeract hello 데이터베이스 서비스와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0077f-111">You can also use hello Azure portal, Azure CLI, and REST APIs toointeract with hello database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="0077f-112">리소스 제한</span><span class="sxs-lookup"><span data-stu-id="0077f-112">Resource limitations</span></span>
<span data-ttu-id="0077f-113">Azure의 MySQL 데이터베이스 다른 두 가지 메커니즘을 사용 하 여 hello 리소스 tooa 사용할 수 있는 서버를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0077f-113">Azure MySQL Database manages hello resources available tooa server using two different mechanisms:</span></span> 
- <span data-ttu-id="0077f-114">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="0077f-114">Resources Governance</span></span> 
- <span data-ttu-id="0077f-115">제한 적용</span><span class="sxs-lookup"><span data-stu-id="0077f-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="0077f-116">보안</span><span class="sxs-lookup"><span data-stu-id="0077f-116">Security</span></span>
<span data-ttu-id="0077f-117">Azure MySQL Database는 액세스를 제한하고, 데이터를 보호하고, 사용자 및 역할을 구성하고, MySQL Database에 대한 활동을 모니터링하기 위한 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0077f-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="0077f-118">인증</span><span class="sxs-lookup"><span data-stu-id="0077f-118">Authentication</span></span>
<span data-ttu-id="0077f-119">Azure MySQL Database는 사용자 및 로그인의 서버 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0077f-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="0077f-120">복원력</span><span class="sxs-lookup"><span data-stu-id="0077f-120">Resiliency</span></span>
<span data-ttu-id="0077f-121">일시적인 오류가 발생 하는 tooMySQL 데이터베이스를 연결 하는 동안 코드 hello 호출을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0077f-121">When a transient error occurs while connecting tooMySQL Database, your code should retry hello call.</span></span> <span data-ttu-id="0077f-122">동시에 다시 시도 하는 여러 클라이언트가 포함 된 SQL 데이터베이스 hello 부담이 되지 않는 있도록 논리에 백오프 hello 재시도 논리가 사용을 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0077f-122">We recommend hello retry logic use back off logic, so that it does not overwhelm hello SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="0077f-123">코드 샘플: 보여주는 코드 샘플에 다시 시도 논리를 hello에서 선택한 언어에 대 한 예제 참조: [MySQL 용 tooconnect tooAzure 데이터베이스를 사용 하는 연결 라이브러리](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="0077f-123">Code samples: For code samples that illustrate retry logic, see samples for hello language of your choice at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="0077f-124">연결 관리</span><span class="sxs-lookup"><span data-stu-id="0077f-124">Managing Connections</span></span>
<span data-ttu-id="0077f-125">데이터베이스 연결 제한 된 리소스 되므로 권장 연결을 통해 구분이 가능한 사용할 MySQL 데이터베이스에 액세스할 때 tooachieve 성능 향상.</span><span class="sxs-lookup"><span data-stu-id="0077f-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database tooachieve better performance.</span></span>
- <span data-ttu-id="0077f-126">Hello 데이터베이스 연결 풀링을 또는 영구 연결을 사용 하 여 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="0077f-126">Access hello database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="0077f-127">짧은 연결 수명 범위를 사용 하 여 hello 데이터베이스를 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="0077f-127">Access hello database by using short connection life span.</span></span> 
- <span data-ttu-id="0077f-128">Hello hello 연결 시도, tooconcurrent 연결 인해 toocatch 실패 시점에서 응용 프로그램에서 재시도 논리를 사용 하 여 허용 되는 hello 최대값에 도달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0077f-128">Use retry logic in your application at hello point of hello connection attempt, toocatch failures due tooconcurrent connections have reached hello maximum allowed.</span></span> <span data-ttu-id="0077f-129">Hello에서 재시도 논리 짧은 지연 간격을 설정 하 고 hello 추가 연결 시도 하기 전에 임의의 시간이 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="0077f-129">In hello retry logic, set a short delay, and then wait for a random time before hello additional connection attempts.</span></span>
