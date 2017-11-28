---
title: "PostgreSQL에 대 한 Azure 데이터베이스에서 aaaUsing PostgreSQL 확장 | Microsoft Docs"
description: "PostgreSQL에 대 한 Azure 데이터베이스에서 확장을 사용 하 여 데이터베이스의 hello 기능 tooextend hello 기능에 설명 합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/29/2017
ms.openlocfilehash: af2462d7a923b934bc0329153be7079ba86e8856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a><span data-ttu-id="d4fbe-103">PostgreSQL용 Azure 데이터베이스의 PostgreSQL 확장</span><span class="sxs-lookup"><span data-stu-id="d4fbe-103">PostgreSQL Extensions in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="d4fbe-104">PostgreSQL 확장을 사용 하 여 데이터베이스의 hello 기능 tooextend hello 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-104">PostgreSQL provides hello ability tooextend hello functionality of your database using extensions.</span></span> <span data-ttu-id="d4fbe-105">확장 관련 된 여러 SQL 개체 toobe 단일 패키지에서 번들에 대 한 허용 로드 또는 단일 명령으로 데이터베이스에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-105">Extensions allow for multiple related SQL objects toobe bundled together in a single package and can be loaded or removed from your database with a single command.</span></span> <span data-ttu-id="d4fbe-106">Hello 데이터베이스에 로드 된 확장에는 기본 제공 기능 마찬가지로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-106">Extensions once loaded into hello database can function just like features that are built in.</span></span> <span data-ttu-id="d4fbe-107">PostgreSQL 확장에 대한 자세한 내용은 [관련 개체를 확장으로 패키지](https://www.postgresql.org/docs/9.6/static/extend-extensions.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-107">For more information on PostgreSQL extensions, see [Packaging Related Objects into an Extension](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).</span></span>

## <a name="how-toouse-postgresql-extensions"></a><span data-ttu-id="d4fbe-108">어떻게 toouse PostgreSQL 확장?</span><span class="sxs-lookup"><span data-stu-id="d4fbe-108">How toouse PostgreSQL extensions?</span></span>
<span data-ttu-id="d4fbe-109">PostgreSQL 확장 toobe를 사용 하기 전에 데이터베이스에 대 한 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-109">PostgreSQL extensions need toobe installed for your database before you can use them.</span></span> <span data-ttu-id="d4fbe-110">실행 tooinstall 특정 확장에는 [확장명 만들기](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) psql 도구 tooload에서 명령을 데이터베이스에 패키지에 포함 된 개체를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-110">tooinstall a particular extension, run the [CREATE EXTENSION](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) command from psql tool tooload hello packaged objects into your database.</span></span>

<span data-ttu-id="d4fbe-111">PostgreSQL용 Azure 데이터베이스는 여기에 나열된 대로 주요 확장의 일부만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-111">Azure Database for PostgreSQL supports a subset of key extensions as listed here.</span></span> <span data-ttu-id="d4fbe-112">목록에 나오지 hello 외에 다른 확장 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-112">Beyond hello ones listed, other extensions are not supported.</span></span> <span data-ttu-id="d4fbe-113">PostgreSQL용 Azure 데이터베이스 서비스로 고유한 확장을 만들 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-113">You cannot create your own extension with Azure Database for PostgreSQL service.</span></span>

## <a name="extensions-supported-by-azure-database-for-postgresql"></a><span data-ttu-id="d4fbe-114">PostgreSQL용 Azure 데이터베이스에서 지원하는 확장</span><span class="sxs-lookup"><span data-stu-id="d4fbe-114">Extensions supported by Azure Database for PostgreSQL</span></span>
<span data-ttu-id="d4fbe-115">hello 다음 표에 hello 표준 PostgreSQL 확장 목록 PostgreSQL에 대 한 Azure 데이터베이스에서 현재 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-115">hello following tables list hello standard PostgreSQL extensions that are currently supported by Azure Database for PostgreSQL.</span></span> <span data-ttu-id="d4fbe-116">pg\_available\_extensions를 쿼리하여 이 정보를 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-116">You can also obtain this information by querying pg\_available\_extensions.</span></span> 

### <a name="data-types-extensions"></a><span data-ttu-id="d4fbe-117">데이터 형식 확장</span><span class="sxs-lookup"><span data-stu-id="d4fbe-117">Data types extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="d4fbe-118">**확장**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-118">**Extension**</span></span> | <span data-ttu-id="d4fbe-119">**설명**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-119">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="d4fbe-120">citext</span><span class="sxs-lookup"><span data-stu-id="d4fbe-120">citext</span></span>](https://www.postgresql.org/docs/9.6/static/citext.html) | <span data-ttu-id="d4fbe-121">대/소문자 구분 문자 문자열 형식 제공</span><span class="sxs-lookup"><span data-stu-id="d4fbe-121">Provides a case-insensitive character string type</span></span> |
| [<span data-ttu-id="d4fbe-122">hstore</span><span class="sxs-lookup"><span data-stu-id="d4fbe-122">hstore</span></span>](https://www.postgresql.org/docs/9.6/static/hstore.html) | <span data-ttu-id="d4fbe-123">키/값 쌍 집합을 저장하기 위한 데이터 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-123">Provides data type for storing sets of key/value pairs</span></span> |

### <a name="functions-extensions"></a><span data-ttu-id="d4fbe-124">함수 확장</span><span class="sxs-lookup"><span data-stu-id="d4fbe-124">Functions extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="d4fbe-125">**확장**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-125">**Extension**</span></span> | <span data-ttu-id="d4fbe-126">**설명**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-126">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="d4fbe-127">fuzzystrmatch</span><span class="sxs-lookup"><span data-stu-id="d4fbe-127">fuzzystrmatch</span></span>](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | <span data-ttu-id="d4fbe-128">여러 toodetermine 유사성 함수 및 문자열 사이의 거리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-128">Provides several functions toodetermine similarities and distance between strings.</span></span> |
| [<span data-ttu-id="d4fbe-129">intarray</span><span class="sxs-lookup"><span data-stu-id="d4fbe-129">intarray</span></span>](https://www.postgresql.org/docs/9.6/static/intarray.html) | <span data-ttu-id="d4fbe-130">null 없는 정수 배열을 조작하기 위한 함수 및 연산자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-130">Provides functions and operators for manipulating null-free arrays of integers.</span></span> |
| [<span data-ttu-id="d4fbe-131">pgcrypto</span><span class="sxs-lookup"><span data-stu-id="d4fbe-131">pgcrypto</span></span>](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | <span data-ttu-id="d4fbe-132">암호화 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-132">Provides cryptographic functions</span></span> |
| [<span data-ttu-id="d4fbe-133">pg\_partman</span><span class="sxs-lookup"><span data-stu-id="d4fbe-133">pg\_partman</span></span>](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | <span data-ttu-id="d4fbe-134">시간 또는 ID로 분할된 테이블을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-134">Manages partitioned tables by time or ID</span></span> |
| [<span data-ttu-id="d4fbe-135">pg\_trgm</span><span class="sxs-lookup"><span data-stu-id="d4fbe-135">pg\_trgm</span></span>](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | <span data-ttu-id="d4fbe-136">일치 하는 트라이 영숫자 텍스트의 hello 유사성을 확인 하기 위한 함수 및 연산자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-136">Provides functions and operators for determining hello similarity of alphanumeric text based on trigram matching</span></span> |
| [<span data-ttu-id="d4fbe-137">uuid-ossp</span><span class="sxs-lookup"><span data-stu-id="d4fbe-137">uuid-ossp</span></span>](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | <span data-ttu-id="d4fbe-138">UUID(범용 고유 식별자)를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-138">Generate universally unique identifiers (UUIDs)</span></span> |

### <a name="full-text-search-extensions"></a><span data-ttu-id="d4fbe-139">전체 텍스트 검색 확장</span><span class="sxs-lookup"><span data-stu-id="d4fbe-139">Full-text Search extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="d4fbe-140">**확장**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-140">**Extension**</span></span> | <span data-ttu-id="d4fbe-141">**설명**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-141">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="d4fbe-142">unaccent</span><span class="sxs-lookup"><span data-stu-id="d4fbe-142">unaccent</span></span>](https://www.postgresql.org/docs/9.6/static/unaccent.html) | <span data-ttu-id="d4fbe-143">Lexemes에서 악센트(분음 기호)를 제거하는 텍스트 검색 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-143">A text search dictionary that removes accents (diacritic signs) from lexemes.</span></span> |

### <a name="index-types-extensions"></a><span data-ttu-id="d4fbe-144">인덱스 형식 확장</span><span class="sxs-lookup"><span data-stu-id="d4fbe-144">Index Types extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="d4fbe-145">**확장**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-145">**Extension**</span></span> | <span data-ttu-id="d4fbe-146">**설명**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-146">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="d4fbe-147">btree\_gin</span><span class="sxs-lookup"><span data-stu-id="d4fbe-147">btree\_gin</span></span>](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | <span data-ttu-id="d4fbe-148">특정 데이터 형식에 대해 B-트리 유사 동작을 구현하는 샘플 GIN 연산자 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-148">Provides sample GIN operator classes that implement B-tree like behavior for certain data types.</span></span> |
| [<span data-ttu-id="d4fbe-149">btree\_gist</span><span class="sxs-lookup"><span data-stu-id="d4fbe-149">btree\_gist</span></span>](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | <span data-ttu-id="d4fbe-150">B-트리를 구현하는 GiST 인덱스 연산자 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-150">Provides GiST index operator classes that implement B-tree.</span></span> |

### <a name="language-extensions"></a><span data-ttu-id="d4fbe-151">언어 확장</span><span class="sxs-lookup"><span data-stu-id="d4fbe-151">Language extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="d4fbe-152">**확장**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-152">**Extension**</span></span> | <span data-ttu-id="d4fbe-153">**설명**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-153">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="d4fbe-154">plpgsql</span><span class="sxs-lookup"><span data-stu-id="d4fbe-154">plpgsql</span></span>](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | <span data-ttu-id="d4fbe-155">PL/pgSQL 로드 가능 절차 언어</span><span class="sxs-lookup"><span data-stu-id="d4fbe-155">PL/pgSQL loadable procedural language</span></span> |

### <a name="miscellaneous-extensions"></a><span data-ttu-id="d4fbe-156">기타 확장</span><span class="sxs-lookup"><span data-stu-id="d4fbe-156">Miscellaneous extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="d4fbe-157">**확장**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-157">**Extension**</span></span> | <span data-ttu-id="d4fbe-158">**설명**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-158">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="d4fbe-159">pg\_buffercache</span><span class="sxs-lookup"><span data-stu-id="d4fbe-159">pg\_buffercache</span></span>](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | <span data-ttu-id="d4fbe-160">실시간으로 hello 공유 버퍼 캐시에서 일어나는 검사 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-160">Provides a means for examining what's happening in hello shared buffer cache in real time.</span></span> |
| [<span data-ttu-id="d4fbe-161">pg\_prewarm</span><span class="sxs-lookup"><span data-stu-id="d4fbe-161">pg\_prewarm</span></span>](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | <span data-ttu-id="d4fbe-162">Hello 버퍼 캐시로 방법을 tooload 관계 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-162">Provides a way tooload relation data into hello buffer cache.</span></span> |
| [<span data-ttu-id="d4fbe-163">pg\_stat\_statements</span><span class="sxs-lookup"><span data-stu-id="d4fbe-163">pg\_stat\_statements</span></span>](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | <span data-ttu-id="d4fbe-164">서버에서 실행되는 모든 SQL 문의 실행 통계를 추적하는 수단을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-164">Provides a means for tracking execution statistics of all SQL statements executed by a server.</span></span> |
| [<span data-ttu-id="d4fbe-165">postgres\_fdw</span><span class="sxs-lookup"><span data-stu-id="d4fbe-165">postgres\_fdw</span></span>](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | <span data-ttu-id="d4fbe-166">외부 데이터 래퍼 사용 하 여 외부 PostgreSQL 서버에 저장 된 tooaccess 데이터</span><span class="sxs-lookup"><span data-stu-id="d4fbe-166">Foreign-data wrapper used tooaccess data stored in external PostgreSQL servers</span></span> |

### <a name="postgis"></a><span data-ttu-id="d4fbe-167">PostGIS</span><span class="sxs-lookup"><span data-stu-id="d4fbe-167">PostGIS</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="d4fbe-168">**확장**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-168">**Extension**</span></span> | <span data-ttu-id="d4fbe-169">**설명**</span><span class="sxs-lookup"><span data-stu-id="d4fbe-169">**Description**</span></span> |
|---|---|
| <span data-ttu-id="d4fbe-170">[PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal</span><span class="sxs-lookup"><span data-stu-id="d4fbe-170">[PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal</span></span> | <span data-ttu-id="d4fbe-171">PostgreSQL에 대한 공간 및 지리적 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-171">Spatial and geographic objects for PostgreSQL.</span></span> |
| <span data-ttu-id="d4fbe-172">address\_standardizer, address\_standardizer\_data\_us</span><span class="sxs-lookup"><span data-stu-id="d4fbe-172">address\_standardizer, address\_standardizer\_data\_us</span></span> | <span data-ttu-id="d4fbe-173">사용 되는 tooparse 구성 요소에는 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-173">Used tooparse an address into constituent elements.</span></span> <span data-ttu-id="d4fbe-174">Toosupport 지 오 코딩 주소 정규화 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-174">Used toosupport geocoding address normalization step.</span></span> |
| [<span data-ttu-id="d4fbe-175">pgrouting</span><span class="sxs-lookup"><span data-stu-id="d4fbe-175">pgrouting</span></span>](http://pgrouting.org/) | <span data-ttu-id="d4fbe-176">Hello PostGIS 확장 / PostgreSQL 지리 공간 데이터베이스 tooprovide 지리 공간 라우팅 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-176">Extends hello PostGIS / PostgreSQL geospatial database tooprovide geospatial routing functionality.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d4fbe-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4fbe-177">Next steps</span></span>
<span data-ttu-id="d4fbe-178">Toouse 원하는 확장을 보이지 않으세요?</span><span class="sxs-lookup"><span data-stu-id="d4fbe-178">Don't see an extension you'd like toouse?</span></span> <span data-ttu-id="d4fbe-179">저희에게 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-179">Please let us know.</span></span> <span data-ttu-id="d4fbe-180">[고객 사용자 의견 포럼](https://feedback.azure.com/forums/597976-azure-database-for-postgresql)에서 기존 요청에 투표하거나 새 사용자 의견 및 희망 사항을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="d4fbe-180">Vote for existing requests or create new feedback and wishes in our [Customer feedback forum](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).</span></span>
