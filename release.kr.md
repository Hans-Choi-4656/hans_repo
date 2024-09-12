2024년 9월 26일, 오늘 [PostgreSQL 글로벌 개발 그룹](https://www.postgresql.org)
은 세계에서 가장 진보된 오픈 소스 데이터베이스의 최신 버전인 [PostgreSQL 17](https://www.postgresql.org/docs/17/release-17.html)의 출시를 발표했습니다.

수십 년에 걸친 오픈 소스 개발을 기반으로 구축된 PostgreSQL 17은 성능과 확장성을 개선하는 동시에 새로운 데이터 액세스 및 저장 패턴에 적응할 수 있도록 지원합니다. 이번 PostgreSQL 릴리스에는 Vacuum 상태를 위한 메모리 관리 구현, 스토리지 액세스 최적화 및 동시성이 높은 워크로드에 대한 개선, 대량 로딩 및 내보내기 속도 향상, 인덱스 쿼리 실행 개선 등 전반적인 성능이 크게 향상되었습니다. 새로운 워크로드와 중요 시스템 모두에 도움이 되는 기능, 예를 들어 SQL/JSON JSON_TABLE 명령에 대한 개발자 환경 추가, 고가용성 워크로드 및 주요 버전 업그레이드의 관리를 간소화하는 논리적 복제 기능 개선 등이 PostgreSQL 17에 포함되어 있습니다.

“PostgreSQL 17은 PostgreSQL 개발을 주도하는 글로벌 오픈 소스 커뮤니티가 데이터베이스 여정의 모든 단계에서 사용자에게 도움이 되는 개선 사항을 구축하는 방법을 강조합니다."라고 PostgreSQL 핵심 팀원 Jonathan Katz는 말합니다. “대규모 데이터베이스 운영을 위한 개선 사항이든, 즐거운 개발자 경험을 기반으로 하는 새로운 기능이든, PostgreSQL 17은 데이터 관리 경험을 향상시킬 것입니다.”

안정성, 견고성, 확장성으로 잘 알려진 혁신적인 데이터 관리 시스템인 PostgreSQL은 글로벌 개발자 커뮤니티에서 25년 이상 오픈 소스를 개발해 온 결과, 모든 규모의 조직에서 선호하는 오픈 소스 관계형 데이터베이스로 자리 잡았습니다.

### 시스템 전반의 성능 향상

PostgreSQL [VACUUM](https://www.postgresql.org/docs/17/routine-vacuuming.html)프로세스는 정상적인 운영을 위해 매우 중요하며, 서버 인스턴스 리소스를 필요로 합니다.
PostgreSQL 17은 VACUUM 프로세스를 위한 최대 20배 적은 메모리를 소비하는 새로운 내부 메모리 구조를 도입했습니다. 이를 통해 VACUUM 속도가 향상되고 공유 리소스 사용량이 줄어들어 워크로드에 더 많은 가용성을 확보할 수 있습니다.

PostgreSQL 17은 I/O 계층의 성능을 지속적으로 개선하고 있습니다. 동시성이 높은 워크로드의 경우, [Write Ahead Log](https://www.postgresql.org/docs/17/wal-intro.html)(WAL)처리의 개선으로 쓰기 처리량이 최대 2배까지 향상될 수 있습니다.
또한, 새로운 스트리밍 I/O 인터페이스는 순차 스캔(테이블에서 모든 데이터 읽기) 속도와 [ANALYZE](https://www.postgresql.org/docs/17/sql-analyze.html)에서 플래너 통계를 업데이트하는 속도를 높여줍니다.

PostgreSQL 17은 쿼리 실행에 대한 성능을 향상시켰습니다. 
PostgreSQL 17은 기본 인덱스 방식인 [B-tree](https://www.postgresql.org/docs/17/indexes-types.html#INDEXES-TYPES-BTREE) 인덱스를 사용하는 `IN` 절의 쿼리 성능을 개선합니다.
또한 [BRIN](https://www.postgresql.org/docs/17/brin.html) 인덱스는 이제 병렬 빌드를 지원합니다.
PostgreSQL 17에는 NOT NULL 제약 조건에 대한 최적화, [일반적인 테이블 표현식](https://www.postgresql.org/docs/17/queries-with.html) ([`WITH` 쿼리](https://www.postgresql.org/docs/17/queries-with.html)) 처리 개선 등 쿼리 계획에 대한 몇 가지 개선 사항이 포함되어 있습니다. 이번 릴리스에는 [`bit_count`](https://www.postgresql.org/docs/17/functions-bitstring.html) 함수에 AVX-512를 사용하는 등 계산 가속화를 위한 SIMD(단일 명령어/복수 데이터) 지원이 추가되었습니다.

### 더욱 향상된 개발자 환경

PostgreSQL는 [JSON 지원이 추가된 최초의 관계형 데이터베이스(2012)](https://www.postgresql.org/about/news/postgresql-92-released-1415/)였으며, PostgreSQL 17에서는 SQL/JSON 표준에 대한 구현을 더욱 강화했습니다. 이제 PostgreSQL 17에서는 [`JSON_TABLE`](https://www.postgresql.org/docs/17/functions-json.html#FUNCTIONS-SQLJSON-TABLE) 기능이 추가되어, 개발자들이 JSON 데이터를 표준 PostgreSQL 테이블로 변환할 수 있습니다. 또한 PostgreSQL 17은 [SQL/JSON 생성자](https://www.postgresql.org/docs/17/functions-json.html#FUNCTIONS-JSON-CREATION-TABLE)(`JSON`, `JSON_SCALAR`, `JSON_SERIALIZE`)와 [쿼리 함수](https://www.postgresql.org/docs/17/functions-json.html#SQLJSON-QUERY-FUNCTIONS) (`JSON_EXISTS`, `JSON_QUERY`, `JSON_VALUE`)를 지원하여, 개발자들이 JSON 데이터를 보다 다양한 방식으로 상호작용할 수 있도록 기능을 강화했습니다. 이번 릴리즈에서는 JSON 데이터를 기본 PostgreSQL 데이터 유형으로 변환하는 데 중점을 두고, 숫자, 불리언(boolean), 문자열, 날짜/시간 유형을 포함한 더 많은 [`jsonpath` 표현식](https://www.postgresql.org/docs/17/functions-json.html#FUNCTIONS-SQLJSON-PATH-OPERATORS)이 추가되었습니다.

또한 PostgreSQL 17은 조건부 업데이트에 사용되는 [`MERGE`](https://www.postgresql.org/docs/17/sql-merge.html) 기능을 더욱 강화하여, `RETURNING`절과 [뷰](https://www.postgresql.org/docs/17/sql-createview.html) 업데이트 기능을 추가했습니다. 이와 함께 PostgreSQL 17은 대량 데이터 로드 및 데이터 내보내기를 위한 새로운 기능도 도입했으며, 여기에는 [`COPY`](https://www.postgresql.org/docs/17/sql-copy.html) 명령어를 사용하여 큰 사이즈의 행을 내보낼 경우 성능이 최대 2배 향상되는 것도 포함됩니다. 또한 소스와 목적지 인코딩이 일치하는 경우 `COPY`의 성능이 개선되었고, 새롭게 추가된 옵션인 `ON_ERROR` 옵션을 통해 가져오기(import) 과정에서 삽입 오류가 발생하더라도 계속 진행할 수 있게 되었습니다.

이번 릴리즈는 파티션 내 데이터 관리와 원격 PostgreSQL 인스턴스에서 분산된 데이터 관리 기능이 확장되었습니다. PostgreSQL 17은 [partitioned tables](https://www.postgresql.org/docs/17/ddl-partitioning.html)에서 아이덴티티 열과 배제 제약 조건을 지원합니다. 원격 PostgreSQL 인스턴스에서 쿼리를 실행하는 데 사용되는 [PostgreSQL foreign data wrapper](https://www.postgresql.org/docs/17/postgres-fdw.html)([`postgres_fdw`](https://www.postgresql.org/docs/17/postgres-fdw.html))는 이제 EXISTS 및 IN 서브쿼리를 원격 서버로 푸시할 수 있어, 더 효율적인 처리 작업이 가능해졌습니다.

PostgreSQL 17에는 내장형(built-in)이며, 플랫폼에 독립적이고, 불변한, 정렬(collation) 프로바이더가 추가되었습니다. 이 프로바이더는 불변성을 보장하며, C 정렬 규칙과 유사한 정렬 의미론을 제공하지만, SQL_ASCII 대신 UTF-8 인코딩을 사용합니다. 이 새로운 정렬 프로바이더를 사용하면 PostgreSQL을 실행하는 환경에 관계없이 텍스트 기반 쿼리가 항상 동일한 정렬 결과를 반환하도록 보장됩니다.

### 고가용성과 주요 버전 업그레이드를 위한 논리적 복제의 향상된 기능들

[논리적 복제](https://www.postgresql.org/docs/17/logical-replication.html)는 다양한 사용 사례에서 데이터를 실시간으로 스트리밍하는 데 사용됩니다. 그러나 이번 릴리즈 이전에는, 주요 버전 업그레이드를 수행하려는 사용자들이 [logical replication slots](https://www.postgresql.org/docs/17/logical-replication-subscription.html#LOGICAL-REPLICATION-SUBSCRIPTION-SLOT)을 삭제해야 했고, 이로 인해 업그레이드 후 구독자들에게 데이터를 다시 동기화해야 하는 번거로움이 있었습니다. 하지만 PostgreSQL 17부터는 주요 버전 업그레이드 시 logical replication slots을 삭제할 필요가 없어졌습니다. 이로 인해 논리적 복제를 사용할 때 업그레이드 프로세스가 간소화되었습니다.

PostgreSQL 17은 논리적 복제를 위한 장애 조치(failover) 제어 기능을 포함하여, 고가용성 환경에서 배포될 때 더욱 탄력적으로 운영될 수 있도록 개선되었습니다. 또한, PostgreSQL 17에서는 물리적 복제본(physical replica)을 새로운 논리적 복제본(logical replica)으로 변환하는 [`pg_createsubscriber`](https://www.postgresql.org/docs/17/app-pgcreatesubscriber.html) 명령어 도구도 도입되었습니다.

### 보안 및 운영 관리를 위한 다양한 옵션

PostgreSQL 17은 사용자가 데이터베이스 시스템의 전체 라이프사이클을 관리할 수 있는 방법을 더욱 확장시켰습니다. PostgreSQL에는 새로운 TLS 옵션인 sslnegotiation이 있습니다. 이 옵션을 통해 [ALPN](https://en.wikipedia.org/wiki/Application-Layer_Protocol_Negotiation) (ALPN 디렉토리에 postgresql로 등록되어있음)을 사용할 때 사용자가 직접 TLS 핸드셰이크를 수행할 수 있습니다. 또한 PostgreSQL 17은 사용자가 데이터베이스의 유지 관리 작업을 수행할 수 있는 권한을 가진 `pg_maintain`이라는 [predefined role](https://www.postgresql.org/docs/17/predefined-roles.html)을 새로 추가했습니다.

PostgreSQL에 포함된 백업 유틸리티인 [`pg_basebackup`](https://www.postgresql.org/docs/17/app-pgbasebackup.html)은 이제 증분 백업을 지원하며, 전체 백업을 재구성할 수 있는 [`pg_combinebackup`](https://www.postgresql.org/docs/17/app-pgcombinebackup.html) 유틸리티가 추가되었습니다. 또한 [`pg_dump`](https://www.postgresql.org/docs/17/app-pgdump.html)에는 덤프 파일을 생성할 때 포함할 객체를 선택할 수 있는 `--filter` 라는 새로운 옵션이 추가되었습니다.

PostgreSQL 17은 모니터링 및 분석 기능이 개선되었습니다. 이제 [`EXPLAIN`](https://www.postgresql.org/docs/17/sql-explain.html)은 로컬 I/O 블록 읽기 및 쓰기에 소요된 시간을 보여주며, 데이터 변환시 네트워크 전송에 소요된 시간과 사용된 메모리 양을 확인할 수 있는 두 가지 새로운 옵션인 `SERIALIZE`와 `MEMORY`를 추가했습니다.또한 PostgreSQL 17은 [인덱스 VACUUM 진행상황](https://www.postgresql.org/docs/17/progress-reporting.html#VACUUM-PROGRESS-REPORTING)을 보고하며, 액티브 세션이 대기 상태인 이유에 대한 더 많은 인사이트를 제공하는 [`pg_wait_events`](https://www.postgresql.org/docs/17/view-pg-wait-events.html) 시스템 뷰를 추가하여 [`pg_stat_activity`](https://www.postgresql.org/docs/17/monitoring-stats.html#MONITORING-PG-STAT-ACTIVITY-VIEW)와 함께 사용할 수 있습니다.

### 추가 기능

그 외에도 사용 사례에 도움이 될 수 있는 많은 새로운 기능과 개선 사항이 PostgreSQL 17에 추가되었습니다. 새로 추가되거나 변경된 기능의 전체 목록은 [출시 소식](https://www.postgresql.org/docs/17/release-17.html)을 참조하세요.

### PostgreSQL 소개

[PostgreSQL](https://www.postgresql.org)은 수천 명의 사용자, 기여자, 기업 및 조직으로 구성된 글로벌 커뮤니티가 있는 세계에서 가장 진보된 오픈 소스 데이터베이스입니다. 캘리포니아 버클리 대학교에서 시작된 35년 이상의 엔지니어링을 기반으로 구축된 PostgreSQL은 타의 추종을 불허하는 발전 속도를 이어가고 있습니다. PostgreSQL의 우수한 기능들은 최고의 상용 데이터베이스 시스템에 필적할 뿐만 아니라 고급 데이터베이스 기능, 확장성, 보안 및 안정성 면에서 이를 뛰어넘습니다.

### 링크

* [다운로드](https://www.postgresql.org/download/)
* [출시 소식](https://www.postgresql.org/docs/17/release-17.html)
* [홍보글](https://www.postgresql.org/about/press/)
* [보안 정보](https://www.postgresql.org/support/security/)
* [버전 정책](https://www.postgresql.org/support/versioning/)
* [트위터 팔로우 @postgresql](https://twitter.com/postgresql)
* [기부](https://www.postgresql.org/about/donate/)

## 기능에 대해 자세히 알아보기

위의 기능 및 기타 기능에 대한 설명은 다음 리소스를 참조하시기 바랍니다:

* [출시 소식](https://www.postgresql.org/docs/17/release-17.html)
* [기능 매트릭스](https://www.postgresql.org/about/featurematrix/)

## 다운로드 위치

다음과 같은 여러 가지 방법으로 PostgreSQL 17을 다운로드할 수 있습니다:

* [공식 다운로드](https://www.postgresql.org/download/) 페이지에서 [Windows](https://www.postgresql.org/download/windows/), [Linux](https://www.postgresql.org/download/linux/), [macOS](https://www.postgresql.org/download/macosx/) 등을 위한 설치 프로그램 및 도구를 다운로드할 수 있습니다.
* [소스 코드](https://www.postgresql.org/ftp/source/v17.0)

다른 도구와 확장 프로그램은 [PostgreSQL Extension Network](http://pgxn.org/)에서 확인할 수 있습니다.

## 문서

PostgreSQL 17은 man 페이지뿐만 아니라 HTML 문서도 함께 제공되며, [HTML](https://www.postgresql.org/docs/17/) 및 [PDF](https://www.postgresql.org/files/documentation/pdf/17/postgresql-17-US.pdf) 형식의 문서를 온라인에서 찾아볼 수도 있습니다.

## 라이센스

PostgreSQL은 BSD와 유사한 “허용” 라이센스인 [PostgreSQL 라이센스](https://www.postgresql.org/about/licence/)를 사용합니다.
[OSI 인증 라이센스](http://www.opensource.org/licenses/postgresql/)는 상용 및 독점 응용 프로그램에서 PostgreSQL의 사용을 제한하지 않기 때문에 유연하고 비즈니스 친화적인 것으로 널리 인정받고 있습니다. 
여러 회사의 지원 및 코드의 공개 소유권과 함께, 이 라이센스는 수수료, 공급업체 종속 또는 라이센스 조건 변경에 대한 우려 없이 자체 제품에 데이터베이스를 내장하고자 하는 공급업체에게 매우 인기가 있습니다.

## 연락처

웹사이트
* [https://www.postgresql.org/](https://www.postgresql.org/)

이메일
* [press@postgresql.org](mailto:press@postgresql.org)

## 이미지와 로고

Postgres, PostgreSQL 및 코끼리 로고(Slonik)는 모두 [PostgreSQL 커뮤니티 협회](https://www.postgres.ca)의 등록된 상표입니다.
이러한 마크를 사용하려면 [상표 정책](https://www.postgresql.org/about/policies/trademarks/)을 준수해야 합니다.

## 기업 지원 및 기부

PostgreSQL은 개발자를 후원하고, 호스팅 리소스를 제공하고, 재정적 지원을 제공하는 수많은 회사의 지원을 받고 있습니다. 
이러한 프로젝트 후원자 중 일부는 페이지를 참조하십시오.[sponsors](https://www.postgresql.org/about/sponsors/)

또한 개인 컨설턴트부터 다국적 기업에 이르기까지 PostgreSQL 지원을 제공하는 커뮤니티가 있습니다.[companies offering PostgreSQL Support](https://www.postgresql.org/support/professional_support/)

PostgreSQL 글로벌 개발 그룹 또는 공인된 커뮤니티 비영리 단체 중 하나에 재정적 기부를 하고 싶으시면 페이지를 방문하세요.[donations](https://www.postgresql.org/about/donate/)


