# GitHub Pages 커스텀 도메인 설정 가이드

## 개요
GitHub Pages에 커스텀 도메인을 연결하여 `https://rockme999.github.io/suparain` 대신 자신의 도메인(예: `www.suparain.com` 또는 `suparain.com`)으로 웹사이트에 접속할 수 있도록 설정합니다.

---

## 설정 방법

### 1단계: GitHub Pages 설정

1. GitHub 저장소로 이동: https://github.com/rockme999/suparain
2. **Settings** 탭 클릭
3. 왼쪽 메뉴에서 **Pages** 클릭
4. **Custom domain** 섹션에서 도메인 입력
   - 예: `www.suparain.com` 또는 `suparain.com`
5. **Save** 클릭
6. **Enforce HTTPS** 옵션 활성화 (권장)

### 2단계: DNS 레코드 설정

도메인 제공업체(예: GoDaddy, Namecheap, Cloudflare 등)의 DNS 관리 페이지에서 다음 설정을 추가합니다.

#### 옵션 A: 서브도메인 사용 (www.suparain.com) - 권장

**CNAME 레코드 추가:**
- **Type**: CNAME
- **Name/Host**: `www`
- **Value/Target**: `rockme999.github.io`
- **TTL**: 3600 (또는 기본값)

#### 옵션 B: 루트 도메인 사용 (suparain.com)

**A 레코드 추가 (4개 모두 추가):**
- **Type**: A
- **Name/Host**: `@` 또는 `suparain.com`
- **Value/Target**: 다음 IP 주소들을 각각 추가:
  - `185.199.108.153`
  - `185.199.109.153`
  - `185.199.110.153`
  - `185.199.111.153`
- **TTL**: 3600 (또는 기본값)

**또는 CNAME 레코드 (일부 DNS 제공업체만 지원):**
- **Type**: CNAME
- **Name/Host**: `@` 또는 `suparain.com`
- **Value/Target**: `rockme999.github.io`
- **TTL**: 3600

#### 옵션 C: 둘 다 사용 (www와 루트 도메인)

1. 루트 도메인에 A 레코드 4개 추가 (옵션 B 참고)
2. www 서브도메인에 CNAME 레코드 추가 (옵션 A 참고)

### 3단계: CNAME 파일 생성 (서브도메인 사용 시)

서브도메인(`www.suparain.com`)을 사용하는 경우, 저장소 루트에 `CNAME` 파일을 생성해야 합니다.

**CNAME 파일 내용:**
```
www.suparain.com
```

**참고:** 루트 도메인만 사용하는 경우 CNAME 파일이 필요 없습니다. GitHub에서 자동으로 처리합니다.

---

## 주요 DNS 제공업체별 설정 방법

### GoDaddy
1. 도메인 관리 → DNS 관리
2. 레코드 추가 → CNAME 또는 A 레코드 선택
3. 위의 값 입력 후 저장

### Namecheap
1. Domain List → Manage → Advanced DNS
2. Add New Record → CNAME 또는 A 레코드 선택
3. 위의 값 입력 후 저장

### Cloudflare
1. DNS → Records
2. Add record → CNAME 또는 A 레코드 선택
3. 위의 값 입력 후 저장
4. **Proxy status**: DNS only (주황색 구름 비활성화)로 설정

### Google Domains
1. DNS → Custom resource records
2. Add → CNAME 또는 A 레코드 선택
3. 위의 값 입력 후 저장

---

## 확인 및 문제 해결

### DNS 전파 확인
DNS 변경사항이 전 세계에 전파되는 데 최대 48시간이 걸릴 수 있습니다. 다음 도구로 확인:
- https://dnschecker.org
- https://www.whatsmydns.net

### GitHub Pages 확인
1. 저장소 Settings → Pages
2. **Custom domain** 섹션에 녹색 체크 표시가 나타나면 설정 완료
3. **Enforce HTTPS** 옵션이 활성화되면 SSL 인증서가 자동으로 발급됨

### 일반적인 문제

**문제**: "Domain's DNS record could not be verified"
- **해결**: DNS 레코드가 올바르게 설정되었는지 확인하고, 24-48시간 대기

**문제**: HTTPS가 활성화되지 않음
- **해결**: DNS 전파 완료 후 몇 시간 더 대기. GitHub가 SSL 인증서를 발급하는 데 시간이 필요

**문제**: www와 루트 도메인 모두 작동하지 않음
- **해결**: 루트 도메인에는 A 레코드, www에는 CNAME 레코드 사용

---

## 보안 권장사항

1. **Enforce HTTPS** 항상 활성화
2. CNAME 파일이 저장소에 포함되어 있는지 확인 (서브도메인 사용 시)
3. DNS 레코드의 TTL 값을 적절히 설정 (3600초 권장)

---

## 📝 Document Information

**Created**: 2025-01-27  
**Last Updated**: 2025-01-27  
**Author**: Development Team

### Update History

#### 2025-01-27 (Initial Creation)
- GitHub Pages 커스텀 도메인 설정 가이드 작성
- DNS 레코드 설정 방법 추가
- 주요 DNS 제공업체별 가이드 추가

---

**Note**: This document is managed according to documentation rules.

