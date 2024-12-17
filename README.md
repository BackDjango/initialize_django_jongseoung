# initialize_django

</br>
</br>
</br>
<div align="center">
<img width="340" alt="image" src="https://github.com/user-attachments/assets/b9265f32-8dac-49c1-9a1a-5b034f6d7704">
</div>
</br>
</br>
</br>

> **이 프로젝트는 Django와 Django REST Framework (DRF)를 커스터마이징하여 자신만의 설정을 구성하는 것을 목표로 합니다.**  
> **개발 기간: 2024.04 ~ 2024.05**

</br>

## 사용 기술 스택

| **분야**       | **기술 스택**                           |
| -------------- | --------------------------------------- |
| **백엔드**     | Django, Django Rest Framework           |
| **데이터베이스** | PostgreSQL                              |

</br>

## 진행 방식  
프로젝트 진행 과정은 다음과 같이 구성됩니다:
1. **개별 레포지토리 생성 및 작업**  
2. **설정 변경 사항마다 커밋 후 코드 리뷰**  
3. **주간 회의 진행**  


### 주간 회의  

- **시간**: 저녁 9시 ~ 10시 30분  
- **형식**: 전체 회의  
- **진행 순서**:  
   1. 짝과 코드 리뷰한 내용을 바탕으로 발표  
   2. 팀원들과 리뷰 및 토론 진행  

</br>

## 프로젝트 목표

1. **커스터마이징된 Django 설정 구현**  
   - 공식 문서나 블로그에서 제공하는 설정을 참고하되, 장단점을 비교하고 자신만의 설정을 적용  
   - 설정을 재사용 가능하게 만들어 이후 프로젝트에서 포크를 활용할 수 있도록 최적화  

2. **GitHub 기능 습득**  
   - 깃 이슈, Pull Request (PR), Actions 등의 기능을 활용하여 효율적인 협업 프로세스 적용  

</br>

## 기대 효과  
- 자신만의 Django 설정을 구축해 프로젝트의 확장성과 생산성을 높임  
- GitHub 활용 능력을 강화하여 협업 프로젝트에 유연하게 대응  

</br>

## 구현 기능

[블로그 정리](https://jongseoung.tistory.com/tag/initialize_django)

### AUTH
> JWT를 이용하여 인증 및 권한 관리

### BOARD
> 기본적인 CRUD 구현

### 환경 변수 관리
> 보안적인 요소를 고려하여 환경 변수를 효율적으로 관리
</br>민감한 정보(예: 데이터베이스 비밀번호, API 키, 시크릿 키 등)를 소스 코드에 직접 포함시키지 않고, 환경 변수 파일을 사용하여 관리
</br>Django-environ 사용

### LOGGING
[LoggerMixin](https://github.com/BackDjango/initialize_django_jongseoung/blob/e076cb98e8b9ccecdb045e6a24854cb299cb825e/core/mixins.py#L20)

> HTTP 요청/응답을 효과적으로 로깅하여 디버깅 및 문제 해결을 용이하게 기능 구현
</br> 요청의 헤더, 바디와 응답 데이터를 통일된 포맷으로 기록해 추적 및 분석에 활용
</br> View마다 중복되는 코드를 Mixin으로 구현함으로써 중복 제거

> 개발환경: 콘솔에 DEBUG 레벨 출력, ERROR이상은 errors.log에 기록
</br> 배포환경: 파일에 DEBUG 레벨 출력, ERROR이상은 errors.log에 기록

### CUSTOM PAGINATION
[CustomPagination](https://github.com/BackDjango/initialize_django_jongseoung/blob/e076cb98e8b9ccecdb045e6a24854cb299cb825e/core/paginations.py#L9)
> 데이터를 페이지 단위로 나누어 제공하며, 사용자가 페이지 크기와 페이지 번호를 조절할 수 있는 기능을 제공
</br> 응답에 페이지 정보(현재 페이지, 페이지 크기, 전체 데이터 수)와 이전/다음 페이지 링크를 포함하여 사용자에게 명확한 정보를 제공
</br> 페이지네이션된 데이터를 통일된 응답 구조로 반환하여 일관성을 유지

### CUSTOM EXCEPTION
[예외처리 코드](https://github.com/BackDjango/initialize_django_jongseoung/blob/main/core/exceptions/__init__.py)
</br>
[예외처리 목록](https://github.com/BackDjango/initialize_django_jongseoung/blob/main/core/exceptions/service_exceptions.py)
</br>
[적용 예시](https://github.com/BackDjango/initialize_django_jongseoung/blob/e076cb98e8b9ccecdb045e6a24854cb299cb825e/api/versions/v1/users/serializers.py#L21)

> 프로젝트의 특성과 요구사항에 맞게 커스텀 예외 처리를 구현
</br> service_exceptions(예외 처리 목록)에 클래스를 정의함으로써 간편하게 예시 추가 가능 
</br> 특정한 상황에서 발생할 수 있는 예외들을 정의하고, 이를 효과적으로 핸들링하여 사용자에게 적절한 에러 메시지를 제공하는 기능을 구현

### CUSTOM RESPONSE
[CustomResponse](https://github.com/BackDjango/initialize_django_jongseoung/blob/e076cb98e8b9ccecdb045e6a24854cb299cb825e/core/responses.py#L4)
> 통일된 응답 구조를 제공하는 Custom Response 클래스를 구현
</br> 응답 데이터에 상태코드, 메시지, 사용자 정의 코드, 데이터를 포함하여 일관된 형식으로 변환
</br> 불필요한 코드 중복을 줄이고, 에러 처리 및 성공 응답 시 명확한 구조를 유지

### CUSTOM RENDER
[CustomRenderer](https://github.com/BackDjango/initialize_django_jongseoung/blob/e076cb98e8b9ccecdb045e6a24854cb299cb825e/core/renderers.py#L4)
> 데이터의 렌더링 방식을 커스터마이징하여 클라이언트에게 최적화된 포맷으로 데이터를 제공
</br> DRF의 기본 JSONRenderer를 확장하여 HTTP 상태코드, 상태 텍스트, 데이터를 포함한 구조화된 JSON응답을 반환
</br> RESPONSE를 사용중이므로 현재 비활성화 상태 -> 설정에서 비활성화 하였습니다.

### CUSTOM JWT TOKEN
[미들 웨어](https://github.com/jong-seoung/initialize_DRF/blob/a32bb1fab9457ae1288b2c09d0b3fe0f4eb6cee1/core/middlewares.py#L9)
</br>
[백엔드](https://github.com/jong-seoung/initialize_DRF/blob/a32bb1fab9457ae1288b2c09d0b3fe0f4eb6cee1/core/backends.py#L14)
</br>
[토큰 발급 및 블랙리스트 등록](https://github.com/jong-seoung/initialize_DRF/blob/main/core/serializers.py)
> 기본적인 JWT 토큰 외에, 프로젝트 요구사항에 맞는 커스텀 JWT 토큰 기능을 구현
</br> 토큰의 유효 기간, 클레임, 시크릿 키 등을 설정하고, 토큰 갱신 기능
</br> 인증 백엔드, 미들웨어, 토큰 발급, 블랙리스트 구현

### SWAGGER
[Swagger Settings](https://github.com/BackDjango/initialize_django_jongseoung/tree/main/config/settings/swagger)
> API 문서화를 위해 drf-yasg를 사용하여 Swagger 설정을 구성
</br>API 엔드포인트를 시각화하고, 인터랙티브 문서를 제공

### GITHUB
[이슈](https://github.com/BackDjango/initialize_django_jongseoung/issues?q=is%3Aissue+is%3Aclosed)
</br>
[PR](https://github.com/BackDjango/initialize_django_jongseoung/pulls?q=is%3Apr+is%3Aclosed)
> Pre-commit 설정
</br>Issues 관리
</br>PR (Pull Request) 관리
</br>Labels 설정

<br>

## 설치 및 설정

### 필수 조건
- Python 3.11
- Django 5.0.4
- Django REST Framework 3.15.1

### 설치 방법
1. 저장소를 클론합니다.
   ```bash
   git clone <저장소 URL>
   cd <프로젝트 디렉토리>

2. 가상환경 만들기
   ```bash
    python -m venv venv

3. 가상환경을 활성화 시켜줍니다.
- Windows
    ```bash
    venv\Scripts\activate

- MacOS/Linux
    ```bash
    source venv/bin/activate

4. requirements.txt에 있는 의존성 파일 설치
   ```bash
    pip install -r requirements.txt

4. .env 파일 설정

5. Django의 데이터 베이스를 마이그레이션 & 마이그레이트
   ```bash
    make makemigrations
    make migrate

6. 실행
   ```bash
    make run
