## 정의

객체(Object)는 COS의 기본 유닛이며 사진을 앨범에 저장된 것처럼 객체는 버킷에 저장됩니다. 사용자는 Tencent Cloud 콘솔, API 및 SDK와 같은 다양한 방법을 통해 객체를 관리할 수 있습니다. API와 SDK의 예시에서 객체의 명명 형식은 `<ObjectKey>`입니다.

>!간편 업로드와 멀티파트 업로드 두 가지 방벙을 통해 객체를 업로드할 수 있습니다.
>- 간편 업로드를 사용할 때에 객체의 크기가 5GB 이하로 제한됩니다.
>- 멀티파트 업로드는 각각 파트에 5GB로 제한하여 10000개 및 48.82TB의 최대 객체 크기로 제한됩니다.

각 객체는 객체 키(ObjectKey), 값(Value) 및 객체 메타데이터(Metadata)로 구성됩니다.

- 객체 키: 객체 키는 객체가 버킷에 있는 유일한 식별자입니다.
- 값(Value): 업로드된 객체의 크기입니다.
- 객체 메타데이터(Metadata): 객체를 업로드할 때 설정할 수 있는 이름 값 쌍입니다.

사용자는 콘솔에서 객체를 조작할 수 있습니다. 자세한 내용은 다음을 참조하십시오.

- [객체 검색](https://cloud.tencent.com/document/product/436/13325)
- [객체 정보 조회](https://cloud.tencent.com/document/product/436/13326)
- [객체 접근 권한 설정](https://cloud.tencent.com/document/product/436/13327)
- [사용자 지정 헤더 설정](https://cloud.tencent.com/document/product/436/13361)

## 객체 키

### 정의

Tencent Cloud COS의 객체에는 유효한 객체 키가 있어야 합니다. 객체 키는 버킷에서 객체의 유일한 식별자입니다.
예를 들어, 객체의 접근 주소인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com / folder / picture.jpg`에서 객체 키는`folder / picture.jpg`입니다.

### 명명 규칙

- 키 이름에 UTF-8 문자를 사용할 수 있습니다. 키 이름은 다른 응용프로그램과의 호환성을 최대화하려면 대문자와 소문자 및 숫자(즉, [az, A-Z, 0-9]), 특수 문자(`-`,`!`,`_`, `.`,`*`) 및 이들의 조합을 권장합니다.
- 최대 인코딩 길이는 850바이트입니다.
- 객체 키는 ASCII 컨드롤 문자 중의 위쪽 화살표(↑), 아래쪽 화살표(↓), 오른쪽 화살표(→), 왼쪽 화살표(←)는 각각 CAN(24), EM(25), SUB(26), ESC(27)에 해당하여 지원되지 않습니다.
- 업로드된 파일 또는 폴더의 이름에 중국어 문자가 포함되어 있으면 해당 파일 또는 폴더에 접근하거나 요청할 때 중국어 문자는 URL 인코딩 규칙에 따라 백분율로 인코딩됩니다.
예를 들어,`문서 .doc`에 접근할 때, 객체 키는 `문서 .doc`입니다. 실제로 URL 인코딩 규칙에 따라 읽는 백분율로 인코딩된 문자열은 `% e6 % 96 % 87 % e6 % a1 % a3.doc`입니다.

유효한 객체 키 이름의 예시는 다음과 같습니다.

- my-organization
- my.great_photos-2016/01/me.jpg
- videos/2016/birthday/video.wmv

#### 특수 문자

일부 문자는 겍체 키 중에서 16진수 형식으로 URL에 인코딩되거나 참조될 수 있습니다. 일부는 인쇄할 수 없는 문자이며 브라우저가 해당 문자를 처리하지 못할 수도 있습니다. 특별한 처리가 필요한 문자가 다음과 같습니다.

|  ,  |                              :                               |    ;     |  =   |
| :--: | :----------------------------------------------------------: | :------: | :--: |
|  &   |                              $                               |    @     |  +   |
|  ?   | ASCII 문자 범위: 00-1F 16진수(0-31, 10진수)<br /> 및 7F(127, 10진수) | (스페이스) |      |

또한 모든 응용프로그램에서 일관성을 유지하려면 상당한 특수 처리가 필요한 문자가 있으므로 다음과 같은 문자를 직접 사용하지 않는 것이 좋습니다.

|  `   |  ^   |             "              |  \|
| :--: | :--: | :------------------------: | :--: |
|  {   |  }   |             [              |  ]   |
|  ~   |  %   |             #              |  \   |
|  >   |  <   | ASCII <br />128-255 10진수 |

### 관련 설명

#### 접근 주소

객체의 접근 주소는 버킷 접근 주소와 객체 키로 구성되며, `[버킷 도메인 이름]/[객체 키]`의 형식입니다.

예를 들어 `exampleobject.txt`를 광저우(화남 지역)의 `examplebucket-1250000000` 버킷에 업로드하면 `exampleobject.txt`의 접근 주소는 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject.txt`입니다.

#### 폴더 및 디렉터리

COS에 폴더와 디렉터리라는 게 없으며 COS는 객체 `project/a.txt`가 업로드되기 때문에 `project` 폴더를 생성하지 않습니다. 사용자의 사용 습관을 충족시키기 위해 COS는 콘솔이나 COS browser와 같은 그래픽 도구에 [폴더] 또는 [디렉터리] 표시 방식을 시뮬레이션합니다. 이는 키 값이 `project/`이고 내용이 비어 있는 객체를 생성하여 구현하며, 표시 방식은 기존 폴더와 유사합니다.

예: API, SDK 를 통해 객체 `project/doc/a.txt`를 업로드합니다. 구분 문자`/`는 "폴더"의 디스플레이 방식을 시뮬레이션하게 되기 때문에 콘솔에 "폴더"`project`와`doc`가 나타나게 됩니다. 그 중 `doc`는 `project`의 하위 "폴더"이며 `a.txt`를 포함합니다.

>!버킷의 객체는 분산형 클러스터 사이에 균등하게 분산됩니다. 따라서 지정된 객체 키 접두사 용량의 크기를 직접적으로 가져올 수는 없습니다. 각 객체의 크기를 누적해서 얻을 수 있습니다.

폴더와 디렉터리를 삭제하는 것은 아래와 같이 비교적 복잡합니다.

| 방법 | 삭제                              | 결과                                                         |
| -------- | --------------------------------- | ------------------------------------------------------------ |
| 콘솔   | 폴더 `project`                  | 객체 키 접두사가 `project/`인 모든 객체가 삭제됩니다 |
| 콘솔   | 객체 `project / doc / a.txt`          | `project`와`doc` 폴더가 유지됩니다                            |
| API 및 SDK | 객체 `project /` 또는 `project / doc /` | 객체 `project / doc / *. txt`는 유지됩니다. 폴더의 객체를 함께 삭제하려면 코드 순회를 사용해야 합니다. |

## COS 유형

접근 빈도에 따라 표준 스토리지, 저빈도 스토리지, 보관 스토리지를 제공합니다.

>!스토리지 클래스의 기본값은 표준 스토리지입니다.

### 표준 스토리지

표준 스토리지는 사용자에게 신뢰성, 가용성 및 성능이 뛰어난 COS 서비스를 제공합니다.

표준 스토리지는 낮은 액세스 지연과 높은 처리량을 갖추고 있기 때문에 인기 파일이 많아 데이터에 빈번하게 액세스해야 하는 시나리오에 적합합니다.

· 적용 시나리오: 인기 동영상, 소셜 이미지, 모바일 앱, 게임 프로그램, 동적 웹사이트

### 저빈도 스토리지

저빈도 스토리지는 사용자에게 높은 신뢰성, 비교적 낮은 스토리지 비용과 짧은 액세스 지연의 COS 서비스를 제공합니다.

밀리초 단위로 첫 번째 바이트에 계속 액세스하면서 스토리지 비용을 최소화하고 데이터를 검색하는 동안 대기하지 않고 빠르게 읽을 수 있습니다. 그러나 데이터 읽는 비용이 부과됩니다. 주로 액세스 빈도가 상대적으로 낯은 시나리오에 적합합니다.

**적용 시나리오**: 네트워크 디스크 데이터, 빅 데이터 분석, 정부 및 기업 비즈니스 데이터, 저빈도 파일, 모니터링 데이터

### 보관 스토리지

보관 스토리지는 사용자에게 높은 신뢰성, 매우 낮은 스토리지 비용과 오래동안 스토리지 가능한 COS 서비스를 제공합니다.

가장 낮은 스토리지 단가를 제공하지만 데이터를 읽는 데 시간이 오래 걸린 특징으로 하는 보관 스토리지는 오랜동안 보관해야 할 데이터에 적합합니다.

**적용 시나리오**: 아카이브 데이터, 의학 이미지, 과학 데이터, 필름 및 비디오 자료.

### 스토리지 클래스 비교

|              | 표준 스토리지 | 저빈도 스토리지 | 보관 스토리지
| ------------ | -------- | -------- | ------------------- |
| 응답         | 밀리초   | 밀리초   | 사전에 복구 신청      |
| 최단 요금 계산 시간 | -        | 30일    | 90일               |
| 지원 지역     | 모든 지역 | 모든 지역 | 중국 대륙 지역만  |
| 스토리지 비용     | 표준     | 상대적 낮음     | 매우 낮음                |
| 데이터 검색 비용 | -        | 상대적 낮음     | 상대적 높음                |
| 읽기/쓰기 요청 비용 | 매우 낮음     | 상대적 낮음     | 매우 낮음(복구 후에야 신청 가능) |


## 객체 메타데이터

### 정의

객체 중에서 이름 값 쌍인 객체 메타데이터는 서버에서 HTTP 프로토콜로 HTML 데이터를 발송하기 전에 보내는 문자열이고 HTTP 헤더라고도 합니다. 객체를 업로드할 때 HTTP 헤더를 수정하여 페이지의 응답 양식을 변경하거나 캐시 시간 수정과 같은 구성 정보를 전달할 수 있습니다.

객체 메타데이터에는 시스템 메타데이터와 사용자 지정 메타데이터가 있습니다.

>!객체의 HTTP 헤더를 수정해도 객체 자체는 수정되지 않습니다.

### 시스템 메타데이터

업로드/수정 시간과 같은 객체의 속성 정보를 가리킵니다.

| 이름             | 설명                                                         |
| ---------------- | ------------------------------------------------------------ |
| Date             | 현재 날짜와 시간.                                             |
| Content-Length             | RFC 2616에서 정의한 HTTP 요청 내용 길이(바이트)로 일반적으로 PUT 유형의 API 작업에 사용됩니다. |
| Last-Modified     | 객체 생성 날짜 또는 마지막 수정 날짜(나중에 발생한 날짜를 기준으로).                  |
| Content-MD5      | RFC 1864에서 정의한 Base64로 인코딩돈 128-bit 내용 MD5 검증값입니다. 이 헤더는 파일 내용에 변화 발생 여부를 검사하는 데 사용됩니다. |
| Authorization    | 인증 정보를 지침하며 요청의 유효성 검증에 사용하는 서명 정보입니다. 공유 읽기 파일의 경우, 이 헤더를 가질 필요가 없습니다. |
| x-cos-version-id | 객체 버전. 버킷에 버전 컨트롤을 활성화할 때 반환한 객체 번전 ID입니다.      |
| ETag          | PUT Object에 의해 업로드된 객체인 경우 업로드된 파일 내용의 MD5 값을 나타냅니다. 객체가 멀티파트 업로드 또는 이전 버전의 API로 업로드된 경우에는 업로드된 파일의 유일한 ID를 나타냅니다. 검사 기능을 수행할 수 없습니다     |
| Expect           | RFC 2616에서 정의한 HTTP 요청 내용 길이(바이트)입니다                  |
| Connection       | 클라이언트와 서버간의 통신 상태입니다. 열거형 값: keep-alive, close |

### 사용자 지정 메타데이터

Content-Type, Cache-Control, Expires 및 x-cos-meta-와 같은 객체의 사용자 지정 매개변수를 가르킵니다. 자세한 내용은 [사용자 지정 객체 헤더](https://cloud.tencent.com/document/product/436/13361)를 참조하십시오.

| 이름                              | 설명                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| Cache-Control                     |	RFC 2616 에서 정의한 캐시 정책으로 Object 메타데이터로 저장됩니다          |
| Content-Disposition/Encoding/Type | RFC 2616 에서 정의한 파일 이름/인코딩 형식/내용 유형(MIME)이 Object 메타데이터로 저장됩니다.|
| Expires                           | RFC 2616 에서 정의한 파일 이름이 객체 메타데이터로 저장됩니다          |
| x-cos-acl                         | Object의 ACL 속성을 정의합니다. 유효값: private, public-read-write, public-read. 기본값: private |
| x-cos-grant-*                     | 권한 부여받은 자에게 어떤 권한을 부여합니다                                         |
| x-cos-storage-class               |객체의 스토리지 클래스를 설정합니다. 열거형 값: STANDARD, STANDARD_IA, 기본값: STANDARD |
| x-cos-server-side-encryption      | 객체를 위해 서버 암호화를 활성화하는지를 지정합니다. COS 마스터 키를 암호화하여 AES256를 입력하고 사용합니다. |

## 객체 하위 리소스

COS에는 버킷 및 객체와 관련된 하위 리소스가 있습니다. 하위 리소스는 객체에 의존됩니다. 즉, 하위 리소스는 자체적으로 존재하지 않으며 다른 엔터티(예: 객체 또는 버킷)와 항상 연결됩니다. ACL은 특정 객체에 대한 접근 컨트롤 정보 리스트로, COS에서 객체의 하위 리소스입니다.

ACL에는 권한 부여받은 사용자와 권한 부여된 라이센싱 리스트를 식별함으로써 객채에 대해 접근을 제어할 수 있습니다. 객체를 생성할 때 ACL은 객체를 완전히 컨트롤할 수있는 객체 소유자를 식별합니다. 사용자는 객체 ACL을 검색하거나 이를 새 권한 라이센싱 리스트로 바꿀 수 있습니다.

>!ACL에 대한 모든 업데이트 사항을 기존 ACL로 대체해야 합니다.

## 접근 권한 유형

COS는 객체에 대한 **공용 권한** 및 **사용자 권한**을 설정할 수 있도록 지원합니다.
**공개 권한**: 계승 권한, 비공개 읽기/쓰기 및 공개 읽기 및 비공개 쓰기가 포함됩니다.
- 계승 권한: 객체가 계승한 버킷 권한은 버킷 접근 권한과 일치합니다. 객체를 접근할 때 COS에서 읽을 수 있는 객체 권한은 계승 버킷 권한이며 버킷 권한과 매칭합니다. 새 객체가 추가된 경우에 기본적으로 해당 버킷의 권한을 계승합니다.
- 비공개 읽기/쓰기: COS에서 객체의 권한은 비공개 읽기/쓰기로 읽을 경우 버킷 권한에 관계없이 [서명 인증](/document/product/436/6054)을 통과해야 객체에 접근할 수 있습니다.
- 공개 읽기 및 비공개 쓰기: COS에서 객체의 권한은 공개 읽기로 읽을 경우 버킷 권한에 관계없이 객체는 모두 직접적으로 다운로드할 수 있습니다.

**사용자 권한**: 루트 계정은 기본적으로 객체의 모든 권한 (예:완전 제어)이 있습니다. COS에서 서브 계정은 데이터 읽기, 데이터 쓰기, 권한 읽기,권한 쓰기를 지원하여 심지어 완전 제어의 권한을 갖습니다.

### 적용 시나리오
비공개 읽기/쓰기 버킷에서 특정한 객체에게 공용 접근을 설정하거나 공개 읽기/비공개 쓰기 버킷에서 특정한 객체에 대해 권한을 설정한 후 접근할 수 있습니다.
