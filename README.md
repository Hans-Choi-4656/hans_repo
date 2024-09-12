2024년 9월 26일, [PostgreSQL 글로벌 개발 그룹](https://www.postgresql.org)
은 오늘 세계에서 가장 진보된 오픈 소스 데이터베이스의 최신 버전인 [PostgreSQL 17](https://www.postgresql.org/docs/17/release-17.html)의 출시를 발표했습니다.

수십 년에 걸친 오픈 소스 개발을 기반으로 구축된 PostgreSQL 17은 성능과 확장성을 개선하는 동시에 새로운 데이터 액세스 및 저장 패턴에 적응할 수 있도록 지원합니다. 이번 PostgreSQL 릴리스에는 Vacuum 상태를 위한 메모리 관리 구현, 스토리지 액세스 최적화 및 동시성이 높은 워크로드에 대한 개선, 대량 로딩 및 내보내기 속도 향상, 인덱스 쿼리 실행 개선 등 전반적인 성능이 크게 향상되었습니다. 새로운 워크로드와 중요 시스템 모두에 도움이 되는 기능, 예를 들어 SQL/JSON JSON_TABLE 명령에 대한 개발자 환경 추가, 고가용성 워크로드 및 주요 버전 업그레이드의 관리를 간소화하는 논리적 복제 기능 개선 등이 PostgreSQL 17에 포함되어 있습니다.

“PostgreSQL 17은 PostgreSQL 개발을 주도하는 글로벌 오픈 소스 커뮤니티가 데이터베이스 여정의 모든 단계에서 사용자에게 도움이 되는 개선 사항을 구축하는 방법을 강조합니다."라고 PostgreSQL 핵심 팀원 Jonathan Katz는 말합니다. “대규모 데이터베이스 운영을 위한 개선 사항이든, 즐거운 개발자 경험을 기반으로 하는 새로운 기능이든, PostgreSQL 17은 데이터 관리 경험을 향상시킬 것입니다.”

안정성, 견고성, 확장성으로 잘 알려진 혁신적인 데이터 관리 시스템인 PostgreSQL은 글로벌 개발자 커뮤니티에서 25년 이상 오픈 소스를 개발해 온 결과, 모든 규모의 조직에서 선호하는 오픈 소스 관계형 데이터베이스로 자리 잡았습니다.

### 시스템 전반의 성능 향상

PostgreSQL [VACUUM](https://www.postgresql.org/docs/17/routine-vacuuming.html)프로세스는 정상적인 운영을 위해 매우 중요하며, 서버 인스턴스 리소스를 필요로 합니다.
PostgreSQL 17은 VACUUM 프로세스를 위한 최대 20배 적은 메모리를 소비하는 새로운 내부 메모리 구조를 도입했습니다. 이를 통해 VACUUM 속도가 향상되고 공유 리소스 사용량이 줄어들어 워크로드에 더 많은 가용성을 확보할 수 있습니다.

PostgreSQL 17은 I/O 계층의 성능을 지속적으로 개선하고 있습니다. 동시성이 높은 워크로드의 경우, [WAL](https://www.postgresql.org/docs/17/wal-intro.html)처리의 개선으로 쓰기 처리량이 최대 2배까지 향상될 수 있습니다.([WAL]
또한, 새로운 스트리밍 I/O 인터페이스는 순차 스캔(테이블에서 모든 데이터 읽기) 속도와 [분석]](https://www.postgresql.org/docs/17/sql-analyze.html)에서 플래너 통계를 업데이트하는 속도를 높여줍니다.

PostgreSQL 17은 또한 쿼리 실행에도 성능 향상을 확장합니다.
PostgreSQL 17은 `IN` 절을 사용하는 쿼리의 성능을 개선합니다.
[B-tree](https://www.postgresql.org/docs/17/indexes-types.html#INDEXES-TYPES-BTREE)
인덱스를 사용하는 `IN` 절로 쿼리 성능을 개선합니다. 또한
[BRIN](https://www.postgresql.org/docs/17/brin.html) 인덱스는 이제
병렬 빌드를 지원합니다. PostgreSQL 17에는 쿼리 계획에 대한 몇 가지 개선 사항이 포함되어 있습니다,
NULL` 제약 조건에 대한 최적화를 비롯하여 쿼리 계획에 대한 몇 가지 개선 사항이 포함되어 있습니다.
일반 테이블 표현식] 처리(https://www.postgresql.org/docs/17/queries-with.html)
([`WITH` 쿼리](https://www.postgresql.org/docs/17/queries-with.html)). 이
릴리스에는 더 많은 SIMD(단일 명령어/복수 데이터) 지원이 추가되었습니다.
계산 가속화를 위한 SIMD(단일 명령어/다중 데이터) 지원이 추가되었습니다.
[`bit_count`](https://www.postgresql.org/docs/17/functions-bitstring.html)
함수.

### 강력한 개발자 환경의 추가 확장

PostgreSQL은 [JSON 지원을 추가한 최초의 관계형 데이터베이스(2012년)]였습니다(https://www.postgresql.org/about/news/postgresql-92-released-1415/),
그리고 PostgreSQL 17은 SQL/JSON 표준 구현을 추가했습니다.
[`json_table`](https://www.postgresql.org/docs/17/functions-json.html#FUNCTIONS-SQLJSON-TABLE)
은 이제 PostgreSQL 17에서 사용할 수 있으므로 개발자가 JSON 데이터를
표준 PostgreSQL 테이블로 변환할 수 있습니다. PostgreSQL 17은 이제 [SQL/JSON 생성자](https://www.postgresql.org/docs/17/functions-json.html#FUNCTIONS-JSON-CREATION-TABLE)를 지원합니다.
(`JSON`, `JSON_SCALAR`, `JSON_SERIALIZE`) 및
[쿼리 함수](https://www.postgresql.org/docs/17/functions-json.html#SQLJSON-QUERY-FUNCTIONS)
(`JSON_EXISTS`, `JSON_QUERY`, `JSON_VALUE`), 개발자에게 다른 방법으로 [...]를 제공합니다.
다른 방법을 제공합니다. 이번 릴리스에는 다음이 추가되었습니다.
[`jsonpath` 표현식](https://www.postgresql.org/docs/17/functions-json.html#FUNCTIONS-SQLJSON-PATH-OPERATORS),
JSON 데이터를 네이티브 PostgreSQL 데이터 유형으로 변환하는 데 중점을 두고 있습니다,
숫자, 부울, 문자열 및 날짜/시간 유형을 포함합니다.

PostgreSQL 17은 [`MERGE`](https://www.postgresql.org/docs/17/sql-merge.html)에 더 많은 기능을 추가합니다,
조건부 업데이트에 사용되는 `RETURNING` 절 및
보기](https://www.postgresql.org/docs/17/sql-createview.html)를 업데이트할 수 있는 기능이 추가되었습니다.
또한 PostgreSQL 17에는 대량 로딩 및 데이터 내보내기를 위한 새로운 기능이 있습니다.
내보내기, 대용량 행 내보내기 시 최대 2배의 성능 향상 포함
COPY`](https://www.postgresql.org/docs/17/sql-copy.html) 명령을 사용하여 큰 행을 내보낼 때 최대 2배의 성능 향상을 포함합니다.
원본과 대상이 일치하는 경우 `COPY` 성능도 개선되었습니다.
인코딩이 일치하는 경우에도 성능이 향상되었으며, 새로운 옵션인 `ON_ERROR`가 추가되어 삽입 오류가 있는 경우에도 가져오기를
가져오기를 계속할 수 있는 새로운 옵션이 포함되어 있습니다.

이번 릴리스에서는 파티션의 데이터 관리 기능과 원격 Postgreasearch에 분산된 데이터
파티션의 데이터와 원격 PostgreSQL 인스턴스에 분산된 데이터를 관리하는 기능이 확장되었습니다. PostgreSQL 17은 다음을 지원합니다.
ID 열 및 제외 제약 조건 사용
[파티션된 테이블](https://www.postgresql.org/docs/17/ddl-partitioning.html).
PostgreSQL 외부 데이터 래퍼](https://www.postgresql.org/docs/17/postgres-fdw.html)
([`postgres_fdw`](https://www.postgresql.org/docs/17/postgres-fdw.html)), 사용됨.
는 이제 원격 PostgreSQL 인스턴스에서 쿼리를 실행하기 위해 `EXISTS` 및
IN` 하위 쿼리를 원격 서버로 푸시하여 보다 효율적으로 처리할 수 있습니다.

또한, PostgreSQL 17에는 플랫폼에 독립적이고 변경이 불가능한
콜레이션 제공자가 내장되어 있으며, 이는 불변성을 보장하고 ``유사한 정렬 의미론``을 제공합니다.
C` 콜레이션과 유사한 정렬 시맨틱을 제공하지만, 인코딩 방식은
SQL_ASCII`를 사용한다는 점을 제외하면 말입니다. 이 새로운 콜레이션 제공자를 사용하면 텍스트 기반 쿼리에서
쿼리가 실행하는 위치에 관계없이 동일한 정렬된 결과를 반환하도록 보장합니다.
PostgreSQL.

### 고가용성 및 주요 버전 업그레이드를 위한 논리적 복제 기능 향상

[논리적 복제](https://www.postgresql.org/docs/17/logical-replication.html)
은 많은 사용 사례에서 데이터를 실시간으로 스트리밍하는 데 사용됩니다. 하지만 이번 릴리스 이전에는
이 릴리스 이전에는 주요 버전 업그레이드를 수행하려는 사용자는 다음을 수행해야 했습니다.
데이터를 다시 동기화해야 하는 [논리적 복제 슬롯](https://www.postgresql.org/docs/17/logical-replication-subscription.html#LOGICAL-REPLICATION-SUBSCRIPTION-SLOT)을 삭제해야 했습니다.
를 재동기화해야 했습니다. PostgreSQL 17부터 업그레이드하는 경우,
사용자는 논리적 복제 슬롯을 삭제할 필요가 없으므로 논리적 복제를 사용할 때 업그레이드
프로세스를 간소화할 수 있습니다.

이제 PostgreSQL 17에는 논리적 복제를 위한 장애 조치 제어 기능이 포함되어 있습니다.
고가용성 환경에 배포할 때 더욱 탄력적으로 사용할 수 있습니다. 또한,
PostgreSQL 17은
[`pg_createsubscriber`](https://www.postgresql.org/docs/17/app-pgcreatesubscriber.html)
명령줄 도구를 도입하여 물리적 복제본을 새로운 논리적 복제본으로 변환할 수 있습니다.

### 보안 및 운영 관리를 위한 더 많은 옵션 제공

PostgreSQL 17은 사용자가 데이터베이스 시스템의 전체 수명 주기를 관리할 수 있는
관리할 수 있는 방법이 더욱 확장되었습니다. PostgreSQL에는 새로운 TLS 옵션인 `sslnegotiation`이 있습니다.
를 사용할 때 사용자가 직접 TLS 핸드셰이크를 수행할 수 있습니다.
[ALPN](https://en.wikipedia.org/wiki/Application-Layer_Protocol_Negotiation)
(ALPN 디렉터리에 `postgresql`로 등록됨). PostgreSQL 17은 또한
미리 정의된 역할](https://www.postgresql.org/docs/17/predefined-roles.html),
사용자에게 유지 관리 작업을 수행할 수 있는 권한을 부여합니다.

[`pg_basebackup`](https://www.postgresql.org/docs/17/app-pgbasebackup.html), 포스트그레SQL에 포함된
백업 유틸리티가 이제 증분 백업을 지원하고
전체 백업을 재구성하는 [`pg_combinebackup`](https://www.postgresql.org/docs/17/app-pgcombinebackup.html) 
유틸리티를 추가하여 전체 백업을 재구성할 수 있습니다. 또한
[`pg_dump`](https://www.postgresql.org/docs/17/app-pgdump.html)에는 `--필터`라는 새로운
필터`라는 새로운 옵션이 포함되어 있어 덤프 파일을 생성할 때 포함할 개체를 선택할 수 있습니다.
덤프 파일을 생성할 때 포함할 개체를 선택할 수 있습니다.

PostgreSQL 17에는 모니터링 및 분석 기능에 대한 개선 사항도 포함되어 있습니다.
이제 [`EXPLAIN`](https://www.postgresql.org/docs/17/sql-explain.html)에 로컬 I/O 블록 읽기에 소요된
로컬 I/O 블록 읽기 및 쓰기에 소요된 시간을 표시하며, 두 가지 새로운 옵션을 포함합니다:
네트워크 전송을 위해 데이터 변환에 소요된 시간과
및 사용된 메모리 양을 확인하는 데 유용합니다. 이제 PostgreSQL 17은
은 [인덱스 진공 청소 진행 상황]을 보고합니다(https://www.postgresql.org/docs/17/progress-reporting.html#VACUUM-PROGRESS-REPORTING),
그리고 [`pg_wait_events`](https://www.postgresql.org/docs/17/view-pg-wait-events.html)
시스템 뷰가 추가되어 [`pg_stat_activity`](https://www.postgresql.org/docs/17/monitoring-stats.html#MONITORING-PG-STAT-ACTIVITY-VIEW)와 결합하면
활성 세션이 대기 중인 이유에 대한 더 많은 인사이트를 제공합니다.

### 추가 기능

그 외 많은 새로운 기능과 개선 사항이 PostgreSQL 17에 추가되었습니다.
사용 사례에 도움이 될 수 있습니다. 자세한 내용은
[릴리스 노트](https://www.postgresql.org/docs/17/release-17.html)를 참조하세요.
신규 및 변경된 기능의 전체 목록을 확인하세요.

### PostgreSQL 소개

[PostgreSQL](https://www.postgresql.org)은 세계에서 가장 진보된 오픈 소스 데이터베이스입니다.
수천 명의 사용자, 기여자로 구성된 글로벌 커뮤니티가 있는 세계에서 가장 진보된 오픈 소스 데이터베이스입니다,
회사 및 조직. 캘리포니아 버클리 대학교에서 시작된 35년 이상의 엔지니어링을 기반으로 구축되었습니다.
캘리포니아 버클리 대학교에서 시작된 PostgreSQL은 타의 추종을 불허하는
타의 추종을 불허하는 개발 속도를 이어가고 있습니다. PostgreSQL의 성숙한 기능 세트는
최고의 독점 데이터베이스 시스템과 일치할 뿐만 아니라 고급 데이터베이스에서는 이를 능가합니다.
기능, 확장성, 보안 및 안정성 면에서 최고를 능가합니다.

### 링크

* [다운로드](https://www.postgresql.org/download/)
* [릴리즈 노트](https://www.postgresql.org/docs/17/release-17.html)
* [프레스 키트](https://www.postgresql.org/about/press/)
* [보안 페이지](https://www.postgresql.org/support/security/)
* 버전 관리 정책](https://www.postgresql.org/support/versioning/)
* 팔로우](https://twitter.com/postgresql)
* 기부](https://www.postgresql.org/about/donate/)

## 기능에 대해 자세히 알아보기

위의 기능 및 기타 기능에 대한 설명은 다음을 참조하세요.
리소스를 참조하세요:

* [릴리즈 노트](https://www.postgresql.org/docs/17/release-17.html)
* [기능 매트릭스](https://www.postgresql.org/about/featurematrix/)

## 다운로드 위치

다음과 같은 여러 가지 방법으로 PostgreSQL 17을 다운로드할 수 있습니다:

* 공식 다운로드](https://www.postgresql.org/download/) 페이지에서 [Windows](https://www.postgresql.org/download/windows/), [Linux](https://www.postgresql.org/download/linux/), [macOS](https://www.postgresql.org/download/macosx/) 등을 위한 설치 프로그램 및 도구를 다운로드할 수 있습니다.
* [소스 코드](https://www.postgresql.org/ftp/source/v17.0)

다른 도구와 확장 프로그램은
[PostgreSQL 확장 네트워크](http://pgxn.org/).

## 문서

PostgreSQL 17은 매뉴얼 페이지뿐만 아니라 HTML 문서도 함께 제공되며, [HTML](https://www.postgresql.org/docs/17/) 및 [PDF](https://www.postgresql.org/files/documentation/pdf/17/postgresql-17-US.pdf) 형식의 문서를 온라인에서 찾아볼 수도 있습니다.

## 라이선스

PostgreSQL은 [PostgreSQL 라이선스](https://www.postgresql.org/about/licence/)를 사용합니다,
BSD와 유사한 “허용적” 라이선스를 사용합니다. 이
[OSI 인증 라이선스](http://www.opensource.org/licenses/postgresql/)는
유연하고 비즈니스 친화적인 것으로 널리 인정받고 있습니다.
유연하고 비즈니스 친화적이라는 평가를 받고 있습니다. 함께
여러 회사의 지원과 코드에 대한 공개 소유권을 갖춘 이 라이선스는
자체 제품에 데이터베이스를 내장하고자 하는 공급업체에게 매우 인기 있는 PostgreSQL은
수수료, 공급업체 종속 또는 라이선스 조건 변경에 대한 걱정 없이 자사 제품에 데이터베이스를 내장하려는 공급업체에게 인기가 높습니다.

## 연락처

웹사이트

* [https://www.postgresql.org/](https://www.postgresql.org/)

이메일

* [press@postgresql.org](mailto:press@postgresql.org)

## 이미지 및 로고

Postgres, PostgreSQL 및 코끼리 로고(Slonik)는 모두 등록된
상표입니다(https://www.postgres.ca).
이러한 마크를 사용하려면 [상표 정책](https://www.postgresql.org/about/policies/trademarks/)을 준수해야 합니다.

## 기업 지원 및 기부

PostgreSQL은 개발자를 후원하는 수많은 기업의 지원을 받고 있습니다,
호스팅 리소스를 제공하고 재정적 지원을 제공합니다. 다음을 참조하십시오.
[스폰서](https://www.postgresql.org/about/sponsors/) 페이지를 참조하십시오.
프로젝트 서포터.

또한 다음과 같은 대규모 커뮤니티도 있습니다.
[PostgreSQL 지원을 제공하는 회사](https://www.postgresql.org/support/professional_support/),
개인 컨설턴트부터 다국적 기업에 이르기까지 다양합니다.

PostgreSQL 글로벌 개발 그룹에 재정적 기여를 하고 싶다면
개발 그룹 또는 공인된 커뮤니티 비영리 단체 중 하나에 재정적 기부를 하고 싶으신 경우,
기부](https://www.postgresql.org/about/donate/) 페이지를 방문하세요.





