# 🔴 MACRO CRISIS EARLY WARNING SYSTEM
> 안녕하세요. figvermouth입니다.
> **비밀지표 12가지 + 네프콘인사이트 릴레이 10 + SRF + Securities Lending**  
> 종합해서 보면 좋을 것 같아 대시보드를 만들었어요.
>
> 전문가 아닙니다. 윌리엄의 네프콘 내용을 교과서로 삼고, 공부하며 찾은 분석기준을 보완하여 직접 만든 도구입니다.  
> 공들여 오랜 기간 만들었는데, 코딩 전문가도 아니며, 투자에서도 경험이 부족해 여러모로 책 잡힐 것도 많을 거예요
> 하지만, 순수한 선의로 공유하는 것이니 이해해주세요. 🙏

---

## 🗺️ 대시보드 전체 구조

| 탭 |  데이터 방식 |
|----|-------------|
| ① | FRED 자동 |
| ② | FRED 자동 |
| ③ | 부분 수동 |
| ④ | FRED 자동 |
| ⑤ | FRED 자동 |
| ⑥ | FRED 자동 |
| ⑦ | 엑셀 업로드 |
| ⑧ | FRED 자동 |
| ⑨ | CSV 업로드 |
| ⑩ | FRED + 파일 업로드 |
| ⑪ | CSV 업로드 |
| ⑫ | 엑셀 업로드 |
| ⑬ | FRED 자동 |
| ⑭ | NY Fed 자동 |
| ⑮ | NY Fed 자동 |

---

## 🚀 처음 시작하기 (5분 완성)

### Step 1 — 파일 열기

HTML 파일을 **크롬(Chrome)** 또는 **엣지(Edge)** 브라우저로 엽니다.  
설치 불필요. 서버 불필요. 파일 하나면 됩니다.

> 🔒 **비밀번호 화면이 뜨면:** '부동산과 금융패권 완결시리즈' 댓글 수 + '금융부자가 되는 삶의 본질' 댓글 수 연이어 기재한 6자리 입력 후 Enter

---

### Step 2 — FRED API 키 발급 (핵심, 무료)

FRED는 미국 세인트루이스 연방준비은행이 운영하는 경제 데이터 서비스입니다.  
이 대시보드 지표의 80%가 여기서 자동으로 데이터를 가져옵니다.

**발급 방법:**
1. https://fredaccount.stlouisfed.org/login/secure/ 접속
2. 계정 생성 (이메일만 있으면 됩니다)
3. 로그인 → My Account → API Keys → **Request API Key**
4. 발급된 32자리 키 복사

**입력 방법:**
- 대시보드 우측 상단 **⚙ API SETTINGS** 클릭
- ① FRED API KEY 란에 붙여넣기
- **SAVE & REFRESH** 클릭 → 데이터 자동 로드

---

### Step 3 — 선택적 API 키 (없어도 됩니다)

| 키 | 용도 | 발급처 |
|----|------|--------|
| 한국은행 ECOS | ③탭 KRW CD금리 실데이터 | https://ecos.bok.or.kr/api/ |
| WTO API | ⑪탭 교역량 자동 조회 | https://apiportal.wto.org/signup |

> ECOS 미설정 시 OECD 데이터로 자동 대체됩니다 (오차 ±25bps).

---

## 📂 탭별 데이터 연동 가이드

### ① ② ④ ⑤ ⑥ ⑧ ⑬ — FRED 자동 연동

FRED API 키 입력 후 자동 로드. **별도 작업 없음.**

---

### ③

**EUR/USD만 수동 입력**이 필요하고, 나머지 통화는 CIP 산식에 따라 자동 계산됩니다.

**EUR/USD 베이시스 확인:**
- CME 사이트에서 EUR/USD xccy basis 최신 값 확인
- https://www.cmegroup.com/reports/cme-xccy-basis-historical-data.csv
- 탭③ EUR/USD 수동 입력 필드에 값 입력 (단위: bps)

---

### ⑦

ICI 엑셀 파일 업로드 → Government / Prime / Tax-Exempt 구성요소별 자동 분석

**다운로드:**
1. https://www.ici.org/research/stats/money-market 접속
2. **Weekly Money Market Fund Assets** 엑셀 다운로드
3. 탭⑦ 업로드 영역에 드래그앤드롭

---

### ⑨ 

**다운로드:**
1. https://www.newyorkfed.org/markets/counterparties/primary-dealers-statistics 접속
2. time-series-data에서 표가 나올 수 있는 하단(세부범주)까지 클릭 후 상단 두번째 **EXPORT** 버튼 클릭
3. **All time series data** 선택 → CSV 다운로드
4. 탭⑨ 업로드 영역에 드래그앤드롭

> 매주 목요일 전주 데이터 발표됩니다.

---

### ⑩ 

#### A) FRED 데이터
탭⑩ 화면 내 FRED API 패널에서 같은 키를 한 번 더 입력하고 **⬇ FRED 로드** 클릭.

#### B) COT 파일 — CFTC 직접 다운로드 (권장)

> Nasdaq Data Link 무료 계정은 접근 제한 가능 → CFTC 직접 다운로드 권장

**단계별 방법:**
1. https://www.cftc.gov/MarketReports/CommitmentsofTraders/HistoricalCompressed/index.htm 접속
2. **"Traders in Financial Futures ; Futures Only Reports"** 섹션 찾기
3. 원하는 연도 ZIP 파일 클릭 (예: 2024, 2025)
4. ZIP 압축 해제
5. **`FinFut24.txt`**, **`FinFut25.txt`** 등 파일 확인
6. 탭⑩에 **복수 파일 동시 업로드** (자동 병합)

> 2009년 9월부터 연도별 전체 데이터 제공. 최근 2~3년치면 충분합니다.

---

### ⑪ 

**BDI (발틱 드라이 인덱스) CSV:**
1. https://www.investing.com/indices/baltic-dry-historical-data 접속
2. **Historical Data** 탭 클릭
3. 날짜 범위 설정
4. **[Download Data]** 버튼 → CSV 저장
5. 탭⑪ BDI 업로드 영역에 업로드

> Cass Freight Index는 FRED API 연동 시 자동 로드됩니다.

---

### ⑫

**CDS 데이터:**
1. https://www.worldgovernmentbonds.com/sovereign-cds/ 접속
2. CDS 데이터 표 전체 선택 → Ctrl+C 복사
3. 엑셀 새 시트에 Ctrl+V 붙여넣기 → 파일 저장
4. 탭⑫에 업로드

---

### ⑭ SRF / ⑮ Securities Lending

NY Fed 데이터 자동 연동 — 탭 진입 시 자동 로드.  
로컬 파일 환경(`file://`)에서는 각 탭의 파일 업로드 기능 사용.

---

## 📊 신호 판독 기준

```
🟢 GREEN  (0~8점)   → 시스템 안정. 정상 관찰
🟡 YELLOW (9~16점)  → 경계. 유동성 흐름 집중 모니터링
🔴 RED    (17~24점) → 구조적 위기 신호. 방어 검토
```

**핵심 원칙:**
- 가격이 아닌 **조건의 변화**를 본다
- 유동성은 **항상 가격보다 먼저** 움직인다
- 복수 영역 동시 악화 → 변동성 급증
- 수익보다 **탈락하지 않는 것**이 우선

---

## ⚠ 알아두세요

**콘솔 메시지 중 무시해도 되는 것:**

| 메시지 | 설명 |
|--------|------|
| `[KRW] FRED 폴백 성공` | 정상 동작 (OECD→FRED 자동 전환) |
| `Unsafe attempt to load URL file://` | 브라우저 보안 정책, 기능 영향 없음 |
| `Tracking Prevention blocked` | Edge 설정, 기능 영향 없음 |

**API 키 보안:**
- 모든 키는 **이 브라우저 로컬에만 저장** (localStorage)
- 외부 서버로 전송되지 않음
- 공용 컴퓨터 사용 후 브라우저 데이터 삭제 권장

---

## 📅 업데이트 권장 주기

| 탭 | 주기 | 방법 |
|----|------|------|
| ①②④⑤⑥⑧⑬ | 자동 | FRED API |
| ⑦ | 주 1회 (목) | 엑셀 수동 |
| ⑨ | 주 1회 (목) | NY Fed CSV 수동 |
| ⑩ | 주 1회 (금) | CFTC 수동 |
| ⑪ | 필요 시 | CSV 수동 |
| ⑫ | 월 1~2회 | 엑셀 수동 |

---

*부족하지만 선의로 공유합니다. @figvermouth🙏*
