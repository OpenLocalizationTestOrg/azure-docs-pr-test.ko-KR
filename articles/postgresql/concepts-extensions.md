---
title: "PostgreSQL용 Azure 데이터베이스에서 PostgreSQL 확장 사용 | Microsoft Docs"
description: "PostgreSQL용 Azure 데이터베이스에서 확장을 사용하여 데이터베이스의 기능을 확장하는 방법을 설명합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/29/2017
ms.openlocfilehash: 755d1cf1a921f6be8f28a4a8ae515db08d904fcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a><span data-ttu-id="1e37c-103">PostgreSQL용 Azure 데이터베이스의 PostgreSQL 확장</span><span class="sxs-lookup"><span data-stu-id="1e37c-103">PostgreSQL Extensions in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="1e37c-104">PostgreSQL은 확장을 사용하여 데이터베이스의 기능을 확장하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-104">PostgreSQL provides the ability to extend the functionality of your database using extensions.</span></span> <span data-ttu-id="1e37c-105">확장을 통해 관련된 여러 SQL 개체를 단일 패키지에 번들로 묶을 수 있으며 단일 명령을 사용해서 데이터베이스에서 로드하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-105">Extensions allow for multiple related SQL objects to be bundled together in a single package and can be loaded or removed from your database with a single command.</span></span> <span data-ttu-id="1e37c-106">데이터베이스에 로드된 확장은 기본 제공된 기능처럼 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-106">Extensions once loaded into the database can function just like features that are built in.</span></span> <span data-ttu-id="1e37c-107">PostgreSQL 확장에 대한 자세한 내용은 [관련 개체를 확장으로 패키지](https://www.postgresql.org/docs/9.6/static/extend-extensions.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e37c-107">For more information on PostgreSQL extensions, see [Packaging Related Objects into an Extension](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).</span></span>

## <a name="how-to-use-postgresql-extensions"></a><span data-ttu-id="1e37c-108">PostgreSQL 확장을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="1e37c-108">How to use PostgreSQL extensions?</span></span>
<span data-ttu-id="1e37c-109">PostgreSQL 확장을 사용하려면 먼저 데이터베이스에 대해 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-109">PostgreSQL extensions need to be installed for your database before you can use them.</span></span> <span data-ttu-id="1e37c-110">특정 확장을 설치하려면 psql 도구에서 [CREATE EXTENSION](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) 명령을 실행하여 패키지 개체를 데이터베이스에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-110">To install a particular extension, run the [CREATE EXTENSION](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) command from psql tool to load the packaged objects into your database.</span></span>

<span data-ttu-id="1e37c-111">PostgreSQL용 Azure 데이터베이스는 여기에 나열된 대로 주요 확장의 일부만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-111">Azure Database for PostgreSQL supports a subset of key extensions as listed here.</span></span> <span data-ttu-id="1e37c-112">나열된 확장 이외의 다른 확장은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-112">Beyond the ones listed, other extensions are not supported.</span></span> <span data-ttu-id="1e37c-113">PostgreSQL용 Azure 데이터베이스 서비스로 고유한 확장을 만들 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-113">You cannot create your own extension with Azure Database for PostgreSQL service.</span></span>

## <a name="extensions-supported-by-azure-database-for-postgresql"></a><span data-ttu-id="1e37c-114">PostgreSQL용 Azure 데이터베이스에서 지원하는 확장</span><span class="sxs-lookup"><span data-stu-id="1e37c-114">Extensions supported by Azure Database for PostgreSQL</span></span>
<span data-ttu-id="1e37c-115">다음 표에는 PostgreSQL용 Azure 데이터베이스에서 현재 지원하는 표준 PostgreSQL 확장이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-115">The following tables list the standard PostgreSQL extensions that are currently supported by Azure Database for PostgreSQL.</span></span> <span data-ttu-id="1e37c-116">pg\_available\_extensions를 쿼리하여 이 정보를 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-116">You can also obtain this information by querying pg\_available\_extensions.</span></span> 

### <a name="data-types-extensions"></a><span data-ttu-id="1e37c-117">데이터 형식 확장</span><span class="sxs-lookup"><span data-stu-id="1e37c-117">Data types extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="1e37c-118">**확장**</span><span class="sxs-lookup"><span data-stu-id="1e37c-118">**Extension**</span></span> | <span data-ttu-id="1e37c-119">**설명**</span><span class="sxs-lookup"><span data-stu-id="1e37c-119">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="1e37c-120">citext</span><span class="sxs-lookup"><span data-stu-id="1e37c-120">citext</span></span>](https://www.postgresql.org/docs/9.6/static/citext.html) | <span data-ttu-id="1e37c-121">대/소문자 구분 문자 문자열 형식 제공</span><span class="sxs-lookup"><span data-stu-id="1e37c-121">Provides a case-insensitive character string type</span></span> |
| [<span data-ttu-id="1e37c-122">hstore</span><span class="sxs-lookup"><span data-stu-id="1e37c-122">hstore</span></span>](https://www.postgresql.org/docs/9.6/static/hstore.html) | <span data-ttu-id="1e37c-123">키/값 쌍 집합을 저장하기 위한 데이터 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-123">Provides data type for storing sets of key/value pairs</span></span> |

### <a name="functions-extensions"></a><span data-ttu-id="1e37c-124">함수 확장</span><span class="sxs-lookup"><span data-stu-id="1e37c-124">Functions extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="1e37c-125">**확장**</span><span class="sxs-lookup"><span data-stu-id="1e37c-125">**Extension**</span></span> | <span data-ttu-id="1e37c-126">**설명**</span><span class="sxs-lookup"><span data-stu-id="1e37c-126">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="1e37c-127">fuzzystrmatch</span><span class="sxs-lookup"><span data-stu-id="1e37c-127">fuzzystrmatch</span></span>](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | <span data-ttu-id="1e37c-128">문자열 간 유사성 및 거리를 확인하기 위한 몇 가지 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-128">Provides several functions to determine similarities and distance between strings.</span></span> |
| [<span data-ttu-id="1e37c-129">intarray</span><span class="sxs-lookup"><span data-stu-id="1e37c-129">intarray</span></span>](https://www.postgresql.org/docs/9.6/static/intarray.html) | <span data-ttu-id="1e37c-130">null 없는 정수 배열을 조작하기 위한 함수 및 연산자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-130">Provides functions and operators for manipulating null-free arrays of integers.</span></span> |
| [<span data-ttu-id="1e37c-131">pgcrypto</span><span class="sxs-lookup"><span data-stu-id="1e37c-131">pgcrypto</span></span>](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | <span data-ttu-id="1e37c-132">암호화 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-132">Provides cryptographic functions</span></span> |
| [<span data-ttu-id="1e37c-133">pg\_partman</span><span class="sxs-lookup"><span data-stu-id="1e37c-133">pg\_partman</span></span>](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | <span data-ttu-id="1e37c-134">시간 또는 ID로 분할된 테이블을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-134">Manages partitioned tables by time or ID</span></span> |
| [<span data-ttu-id="1e37c-135">pg\_trgm</span><span class="sxs-lookup"><span data-stu-id="1e37c-135">pg\_trgm</span></span>](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | <span data-ttu-id="1e37c-136">trigram 일치를 기준으로 영숫자 텍스트의 유사성을 확인하기 위한 함수 및 연산자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-136">Provides functions and operators for determining the similarity of alphanumeric text based on trigram matching</span></span> |
| [<span data-ttu-id="1e37c-137">uuid-ossp</span><span class="sxs-lookup"><span data-stu-id="1e37c-137">uuid-ossp</span></span>](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | <span data-ttu-id="1e37c-138">UUID(범용 고유 식별자)를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-138">Generate universally unique identifiers (UUIDs)</span></span> |

### <a name="full-text-search-extensions"></a><span data-ttu-id="1e37c-139">전체 텍스트 검색 확장</span><span class="sxs-lookup"><span data-stu-id="1e37c-139">Full-text Search extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="1e37c-140">**확장**</span><span class="sxs-lookup"><span data-stu-id="1e37c-140">**Extension**</span></span> | <span data-ttu-id="1e37c-141">**설명**</span><span class="sxs-lookup"><span data-stu-id="1e37c-141">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="1e37c-142">unaccent</span><span class="sxs-lookup"><span data-stu-id="1e37c-142">unaccent</span></span>](https://www.postgresql.org/docs/9.6/static/unaccent.html) | <span data-ttu-id="1e37c-143">Lexemes에서 악센트(분음 기호)를 제거하는 텍스트 검색 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-143">A text search dictionary that removes accents (diacritic signs) from lexemes.</span></span> |

### <a name="index-types-extensions"></a><span data-ttu-id="1e37c-144">인덱스 형식 확장</span><span class="sxs-lookup"><span data-stu-id="1e37c-144">Index Types extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="1e37c-145">**확장**</span><span class="sxs-lookup"><span data-stu-id="1e37c-145">**Extension**</span></span> | <span data-ttu-id="1e37c-146">**설명**</span><span class="sxs-lookup"><span data-stu-id="1e37c-146">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="1e37c-147">btree\_gin</span><span class="sxs-lookup"><span data-stu-id="1e37c-147">btree\_gin</span></span>](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | <span data-ttu-id="1e37c-148">특정 데이터 형식에 대해 B-트리 유사 동작을 구현하는 샘플 GIN 연산자 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-148">Provides sample GIN operator classes that implement B-tree like behavior for certain data types.</span></span> |
| [<span data-ttu-id="1e37c-149">btree\_gist</span><span class="sxs-lookup"><span data-stu-id="1e37c-149">btree\_gist</span></span>](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | <span data-ttu-id="1e37c-150">B-트리를 구현하는 GiST 인덱스 연산자 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-150">Provides GiST index operator classes that implement B-tree.</span></span> |

### <a name="language-extensions"></a><span data-ttu-id="1e37c-151">언어 확장</span><span class="sxs-lookup"><span data-stu-id="1e37c-151">Language extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="1e37c-152">**확장**</span><span class="sxs-lookup"><span data-stu-id="1e37c-152">**Extension**</span></span> | <span data-ttu-id="1e37c-153">**설명**</span><span class="sxs-lookup"><span data-stu-id="1e37c-153">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="1e37c-154">plpgsql</span><span class="sxs-lookup"><span data-stu-id="1e37c-154">plpgsql</span></span>](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | <span data-ttu-id="1e37c-155">PL/pgSQL 로드 가능 절차 언어</span><span class="sxs-lookup"><span data-stu-id="1e37c-155">PL/pgSQL loadable procedural language</span></span> |

### <a name="miscellaneous-extensions"></a><span data-ttu-id="1e37c-156">기타 확장</span><span class="sxs-lookup"><span data-stu-id="1e37c-156">Miscellaneous extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="1e37c-157">**확장**</span><span class="sxs-lookup"><span data-stu-id="1e37c-157">**Extension**</span></span> | <span data-ttu-id="1e37c-158">**설명**</span><span class="sxs-lookup"><span data-stu-id="1e37c-158">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="1e37c-159">pg\_buffercache</span><span class="sxs-lookup"><span data-stu-id="1e37c-159">pg\_buffercache</span></span>](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | <span data-ttu-id="1e37c-160">공유 버퍼 캐시에서 일어나는 작업을 실시간으로 검사하기 위한 수단을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-160">Provides a means for examining what's happening in the shared buffer cache in real time.</span></span> |
| [<span data-ttu-id="1e37c-161">pg\_prewarm</span><span class="sxs-lookup"><span data-stu-id="1e37c-161">pg\_prewarm</span></span>](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | <span data-ttu-id="1e37c-162">관계 데이터를 버퍼 캐시에 로드하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-162">Provides a way to load relation data into the buffer cache.</span></span> |
| [<span data-ttu-id="1e37c-163">pg\_stat\_statements</span><span class="sxs-lookup"><span data-stu-id="1e37c-163">pg\_stat\_statements</span></span>](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | <span data-ttu-id="1e37c-164">서버에서 실행되는 모든 SQL 문의 실행 통계를 추적하는 수단을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-164">Provides a means for tracking execution statistics of all SQL statements executed by a server.</span></span> |
| [<span data-ttu-id="1e37c-165">postgres\_fdw</span><span class="sxs-lookup"><span data-stu-id="1e37c-165">postgres\_fdw</span></span>](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | <span data-ttu-id="1e37c-166">외부 PostgreSQL 서버에 저장된 데이터에 액세스하는 데 사용되는 외부 데이터 래퍼</span><span class="sxs-lookup"><span data-stu-id="1e37c-166">Foreign-data wrapper used to access data stored in external PostgreSQL servers</span></span> |

### <a name="postgis"></a><span data-ttu-id="1e37c-167">PostGIS</span><span class="sxs-lookup"><span data-stu-id="1e37c-167">PostGIS</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="1e37c-168">**확장**</span><span class="sxs-lookup"><span data-stu-id="1e37c-168">**Extension**</span></span> | <span data-ttu-id="1e37c-169">**설명**</span><span class="sxs-lookup"><span data-stu-id="1e37c-169">**Description**</span></span> |
|---|---|
| <span data-ttu-id="1e37c-170">[PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal</span><span class="sxs-lookup"><span data-stu-id="1e37c-170">[PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal</span></span> | <span data-ttu-id="1e37c-171">PostgreSQL에 대한 공간 및 지리적 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-171">Spatial and geographic objects for PostgreSQL.</span></span> |
| <span data-ttu-id="1e37c-172">address\_standardizer, address\_standardizer\_data\_us</span><span class="sxs-lookup"><span data-stu-id="1e37c-172">address\_standardizer, address\_standardizer\_data\_us</span></span> | <span data-ttu-id="1e37c-173">주소를 구성 요소로 구문 분석하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-173">Used to parse an address into constituent elements.</span></span> <span data-ttu-id="1e37c-174">지오코딩 주소 정규화 단계를 지원하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-174">Used to support geocoding address normalization step.</span></span> |
| [<span data-ttu-id="1e37c-175">pgrouting</span><span class="sxs-lookup"><span data-stu-id="1e37c-175">pgrouting</span></span>](http://pgrouting.org/) | <span data-ttu-id="1e37c-176">지리 공간적 라우팅 기능을 제공하기 위해 PostGIS / PostgreSQL 지리 공간적 데이터베이스를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="1e37c-176">Extends the PostGIS / PostgreSQL geospatial database to provide geospatial routing functionality.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1e37c-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e37c-177">Next steps</span></span>
<span data-ttu-id="1e37c-178">사용하려는 확장이 표시되지 않나요?</span><span class="sxs-lookup"><span data-stu-id="1e37c-178">Don't see an extension you'd like to use?</span></span> <span data-ttu-id="1e37c-179">저희에게 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="1e37c-179">Please let us know.</span></span> <span data-ttu-id="1e37c-180">[고객 사용자 의견 포럼](https://feedback.azure.com/forums/597976-azure-database-for-postgresql)에서 기존 요청에 투표하거나 새 사용자 의견 및 희망 사항을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="1e37c-180">Vote for existing requests or create new feedback and wishes in our [Customer feedback forum](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).</span></span>
