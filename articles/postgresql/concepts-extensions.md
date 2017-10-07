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
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a>PostgreSQL용 Azure 데이터베이스의 PostgreSQL 확장
PostgreSQL 확장을 사용 하 여 데이터베이스의 hello 기능 tooextend hello 기능을 제공 합니다. 확장 관련 된 여러 SQL 개체 toobe 단일 패키지에서 번들에 대 한 허용 로드 또는 단일 명령으로 데이터베이스에서 제거할 수 있습니다. Hello 데이터베이스에 로드 된 확장에는 기본 제공 기능 마찬가지로 작동할 수 있습니다. PostgreSQL 확장에 대한 자세한 내용은 [관련 개체를 확장으로 패키지](https://www.postgresql.org/docs/9.6/static/extend-extensions.html)를 참조하세요.

## <a name="how-toouse-postgresql-extensions"></a>어떻게 toouse PostgreSQL 확장?
PostgreSQL 확장 toobe를 사용 하기 전에 데이터베이스에 대 한 설치 합니다. 실행 tooinstall 특정 확장에는 [확장명 만들기](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) psql 도구 tooload에서 명령을 데이터베이스에 패키지에 포함 된 개체를 hello 합니다.

PostgreSQL용 Azure 데이터베이스는 여기에 나열된 대로 주요 확장의 일부만 지원합니다. 목록에 나오지 hello 외에 다른 확장 지원 되지 않습니다. PostgreSQL용 Azure 데이터베이스 서비스로 고유한 확장을 만들 수는 없습니다.

## <a name="extensions-supported-by-azure-database-for-postgresql"></a>PostgreSQL용 Azure 데이터베이스에서 지원하는 확장
hello 다음 표에 hello 표준 PostgreSQL 확장 목록 PostgreSQL에 대 한 Azure 데이터베이스에서 현재 지원 됩니다. pg\_available\_extensions를 쿼리하여 이 정보를 얻을 수도 있습니다. 

### <a name="data-types-extensions"></a>데이터 형식 확장

> [!div class="mx-tableFixed"]
| **확장** | **설명** |
|---|---|
| [citext](https://www.postgresql.org/docs/9.6/static/citext.html) | 대/소문자 구분 문자 문자열 형식 제공 |
| [hstore](https://www.postgresql.org/docs/9.6/static/hstore.html) | 키/값 쌍 집합을 저장하기 위한 데이터 형식을 제공합니다. |

### <a name="functions-extensions"></a>함수 확장

> [!div class="mx-tableFixed"]
| **확장** | **설명** |
|---|---|
| [fuzzystrmatch](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | 여러 toodetermine 유사성 함수 및 문자열 사이의 거리를 제공 합니다. |
| [intarray](https://www.postgresql.org/docs/9.6/static/intarray.html) | null 없는 정수 배열을 조작하기 위한 함수 및 연산자를 제공합니다. |
| [pgcrypto](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | 암호화 함수를 제공합니다. |
| [pg\_partman](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | 시간 또는 ID로 분할된 테이블을 관리합니다. |
| [pg\_trgm](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | 일치 하는 트라이 영숫자 텍스트의 hello 유사성을 확인 하기 위한 함수 및 연산자를 제공 합니다. |
| [uuid-ossp](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | UUID(범용 고유 식별자)를 생성합니다. |

### <a name="full-text-search-extensions"></a>전체 텍스트 검색 확장

> [!div class="mx-tableFixed"]
| **확장** | **설명** |
|---|---|
| [unaccent](https://www.postgresql.org/docs/9.6/static/unaccent.html) | Lexemes에서 악센트(분음 기호)를 제거하는 텍스트 검색 사전입니다. |

### <a name="index-types-extensions"></a>인덱스 형식 확장

> [!div class="mx-tableFixed"]
| **확장** | **설명** |
|---|---|
| [btree\_gin](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | 특정 데이터 형식에 대해 B-트리 유사 동작을 구현하는 샘플 GIN 연산자 클래스를 제공합니다. |
| [btree\_gist](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | B-트리를 구현하는 GiST 인덱스 연산자 클래스를 제공합니다. |

### <a name="language-extensions"></a>언어 확장

> [!div class="mx-tableFixed"]
| **확장** | **설명** |
|---|---|
| [plpgsql](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | PL/pgSQL 로드 가능 절차 언어 |

### <a name="miscellaneous-extensions"></a>기타 확장

> [!div class="mx-tableFixed"]
| **확장** | **설명** |
|---|---|
| [pg\_buffercache](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | 실시간으로 hello 공유 버퍼 캐시에서 일어나는 검사 하는 방법을 제공 합니다. |
| [pg\_prewarm](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | Hello 버퍼 캐시로 방법을 tooload 관계 데이터를 제공합니다. |
| [pg\_stat\_statements](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | 서버에서 실행되는 모든 SQL 문의 실행 통계를 추적하는 수단을 제공합니다. |
| [postgres\_fdw](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | 외부 데이터 래퍼 사용 하 여 외부 PostgreSQL 서버에 저장 된 tooaccess 데이터 |

### <a name="postgis"></a>PostGIS

> [!div class="mx-tableFixed"]
| **확장** | **설명** |
|---|---|
| [PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal | PostgreSQL에 대한 공간 및 지리적 개체입니다. |
| address\_standardizer, address\_standardizer\_data\_us | 사용 되는 tooparse 구성 요소에는 주소입니다. Toosupport 지 오 코딩 주소 정규화 단계를 사용합니다. |
| [pgrouting](http://pgrouting.org/) | Hello PostGIS 확장 / PostgreSQL 지리 공간 데이터베이스 tooprovide 지리 공간 라우팅 기능을 제공 합니다. |

## <a name="next-steps"></a>다음 단계
Toouse 원하는 확장을 보이지 않으세요? 저희에게 알려주세요. [고객 사용자 의견 포럼](https://feedback.azure.com/forums/597976-azure-database-for-postgresql)에서 기존 요청에 투표하거나 새 사용자 의견 및 희망 사항을 만드세요.
