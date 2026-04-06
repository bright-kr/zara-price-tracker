# Zara 가격 추적기

[![Bright Data](https://img.shields.io/badge/Powered%20by-Bright%20Data-blue?style=flat-square)](https://brightdata.co.kr)
[![Zara Price Tracker](https://img.shields.io/badge/Zara%20Price%20Tracker-Managed%20Solution-orange?style=flat-square)](https://brightdata.co.kr/products/insights/price-tracker/zara)
[![Python](https://img.shields.io/badge/Python-3.9%2B-yellow?style=flat-square)](https://python.org)

[![Bright Insights Price Tracker](https://raw.githubusercontent.com/danielshashko/bright-insights-assets/main/price-tracker-hero-v2.png)](https://brightdata.co.kr/products/insights/price-tracker/zara)

실시간 Zara 가격 추적 - Inditex의 대표적인 패스트 패션 브랜드입니다. 시작하는 방법은 두 가지입니다: **완전 관리형** 인텔리전스 플랫폼 또는 자체 파이프라인을 구축할 수 있는 **셀프서비스 API**.

---

## 옵션 1: Bright Insights - AI 기반 가격 추적 (권장)

**[Bright Insights](https://brightdata.co.kr/products/insights/price-tracker/zara)**는 Bright Data의 완전 관리형 리테일 인텔리전스 플랫폼입니다. scraper를 구축할 필요도, 인프라를 유지할 필요도 없습니다. 구조화되고 분석 준비가 완료된 가격 데이터가 대시보드, 데이터 피드 또는 BI 도구로 바로 전달됩니다.

**팀이 Bright Insights를 선택하는 이유:**
- 🚀 **설정 불필요** - 바로 사용할 수 있는 대시보드와 데이터 피드로 몇 분 안에 운영 시작
- 🤖 **AI 기반 추천** - 대화형 AI 어시스턴트가 수백만 개의 데이터 포인트를 즉시 실행 가능한 인사이트로 전환
- ⚡ **실시간 모니터링** - 시간 단위부터 일 단위까지의 refresh 주기와 즉시 알림(email, Slack, webhook)
- 🌍 **무제한 확장성** - 모든 웹사이트, 모든 지역, 모든 refresh 빈도 지원
- 🔗 **즉시 연동 가능한 integrations** - AWS, GCP, Databricks, Snowflake 등
- 🛡️ **완전 관리형** - Bright Data가 schema 변경, 사이트 업데이트, 데이터 품질을 자동으로 처리

**주요 사용 사례:**
- ✅ Zara의 **시즌별 할인** 및 세일 이벤트 추적
- ✅ **경쟁사 가격 모니터링** 및 트렌드 식별
- ✅ 상품 가격이 목표 가격 아래로 내려가면 **가격 알림 자동화**
- ✅ MAP 정책 준수 모니터링 및 가격 위반 감지
- ✅ 경쟁사 프로모션 및 프로모션 동향 추적
- ✅ 정제되고 표준화된 데이터를 동적 가격 책정 알고리즘 또는 AI 모델에 직접 제공

> **월 $250부터 - [맞춤 견적 받기 →](https://brightdata.co.kr/products/insights/price-tracker/zara)**

---

## 옵션 2: Web Scraper API를 통한 셀프서비스

직접 파이프라인을 구축하고 싶으신가요? Bright Data의 **Web Scraper API**는 프록시나 scraping 인프라를 관리하지 않고도 가격, 재고 여부, 리뷰 등 Zara 상품 데이터에 programmatic access를 제공합니다.

### 사전 요구 사항

- Python 3.9 이상
- [Bright Data account](https://brightdata.co.kr) (무료 체험 가능)
- Bright Data **API token** ([발급 방법](https://docs.brightdata.co.kr/general/account/account-settings#api-token))
- Zara 상품용 Bright Data **Web Scraper ID** ([Web Scrapers control panel에서 확인](https://brightdata.co.kr/cp/scrapers))

### 설정

1. **이 repository 복제**

   ```bash
   git clone https://github.com/bright-kr/zara-price-tracker.git
   cd zara-price-tracker
   ```

2. **dependencies 설치**

   ```bash
   pip install -r requirements.txt
   ```

3. **자격 증명 구성**

   `.env.example`을 `.env`로 복사한 뒤 값을 입력하세요:

   ```bash
   cp .env.example .env
   ```

   ```env
   BRIGHTDATA_API_TOKEN=your_api_token_here
   BRIGHTDATA_DATASET_ID=your_dataset_id_here
   ```

   > **Web Scraper ID 찾기**
   > [Bright Data Control Panel](https://brightdata.co.kr/cp/scrapers)에 로그인한 후 **Web Scrapers**로 이동하여
   > "Zara"를 검색하고 Web Scraper ID를 복사하세요 (형식: `gd_xxxxxxxxxxxx`).

---

## 사용법

### 1. URL로 특정 상품 추적

구조화된 가격 데이터를 가져오기 위해 Zara 상품 URL 목록을 전달합니다:

```python
from price_tracker import track_prices

urls = [
    "https://www.zara.com/us/en/sample-product-p12345678.html",
    # Add more product URLs here
]

results = track_prices(urls)
for item in results:
    print(f"{item.get('title')} - {item.get('final_price', item.get('price'))} {item.get('currency', '')}")
```

또는 직접 실행:

```bash
python price_tracker.py
```

### 2. 키워드로 상품 검색

키워드 검색과 일치하는 상품을 찾습니다:

```python
from price_tracker import discover_by_keyword

results = discover_by_keyword("laptop", limit=50)
```

### 3. 카테고리 URL로 상품 탐색

Zara 카테고리 페이지의 모든 상품을 수집합니다:

```python
from price_tracker import discover_by_category

results = discover_by_category(
    "https://zara.com/category/example",
    limit=100,
)
```

---

## 출력 필드

각 결과 레코드에는 다음 필드가 포함됩니다:

| Field | Description |
|-------|-------------|
| `url` | 상품 페이지 URL |
| `title` | 상품명 |
| `brand` | 브랜드 |
| `initial_price` | 원래 가격 |
| `final_price` | 세일가 / 현재 가격 |
| `currency` | 통화 코드 |
| `discount` | 할인율 |
| `in_stock` | 재고 여부 |
| `color` | 사용 가능한 색상 |
| `size` | 사용 가능한 사이즈 |
| `category` | 상품 카테고리 / 부서 |
| `images` | 상품 이미지 URL |
| `description` | 상품 설명 |
| `timestamp` | 수집 타임스탬프 |

### 샘플 출력

```json
[
  {
    "url": "https://www.zara.com/us/en/sample-product-p12345678.html",
    "title": "Example Product Name",
    "brand": "Example Brand",
    "initial_price": 59.99,
    "final_price": 44.99,
    "currency": "USD",
    "discount": "25%",
    "in_stock": true,
    "rating": 4.5,
    "reviews_count": 1234,
    "images": ["https://zara.com/images/product1.jpg"],
    "description": "Product description text...",
    "timestamp": "2025-01-15T10:30:00Z"
  }
]
```

---

## 고급 옵션

`trigger_collection()` 함수는 데이터 수집을 제어하기 위한 선택적 파라미터를 지원합니다:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | integer | - | 반환할 최대 레코드 수 |
| `include_errors` | boolean | `true` | 결과에 오류 보고 포함 |
| `notify` | string (URL) | - | 스냅샷 준비 완료 시 호출할 webhook URL |
| `format` | string | `json` | 출력 형식: `json`, `csv` 또는 `ndjson` |

옵션 사용 예시:

```python
from price_tracker import trigger_collection, get_results

inputs = [{"url": "https://www.zara.com/us/en/sample-product-p12345678.html"}]
snapshot_id = trigger_collection(inputs, limit=200, notify="https://your-webhook.com/hook")
results = get_results(snapshot_id)
```

---

## 리소스

- 🌟 [Zara Price Tracker - Bright Insights (Managed)](https://brightdata.co.kr/products/insights/price-tracker/zara)
- 🔧 [Zara Scraper API](https://brightdata.co.kr/products/web-scraper/zara)
- 📖 [Bright Data Web Scraper API Documentation](https://docs.brightdata.co.kr/scraping-automation/web-scraper-api/overview)
- 🗄️ [Web Scrapers Control Panel](https://brightdata.co.kr/cp/scrapers)
- 🔑 [API token 발급 방법](https://docs.brightdata.co.kr/general/account/account-settings#api-token)
- 🌐 [Bright Data 홈페이지](https://brightdata.co.kr)

---

*[Bright Data](https://brightdata.co.kr)로 구축 - 업계를 선도하는 웹 데이터 플랫폼.*