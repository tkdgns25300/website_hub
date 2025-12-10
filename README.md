# 🌐 Website Hub (Web App Store)

> **"목적 없어도 즐길 수 있는 웹 탐색·발견 플랫폼"**  
> 웹에는 숨겨진 보석 같은 사이트가 많습니다. 구글 검색으로 찾기 힘든 유용한 사이트를 큐레이션하여 '우연한 발견(Serendipity)'을 선물합니다.

---

## 📖 목차 (Table of Contents)
1. [프로젝트 개요](#-프로젝트-개요-overview)
2. [기술 스택](#-기술-스택-tech-stack)
3. [메뉴 및 기능](#-메뉴-및-기능-features)
4. [데이터 구조](#-데이터-구조-data-taxonomy)
5. [데이터베이스 스키마](#-데이터베이스-스키마-schema)
6. [설치 및 실행](#-설치-및-실행-getting-started)

---

## 📌 프로젝트 개요 (Overview)

### 1.1 서비스 정의
- **컨셉**: 웹사이트를 위한 앱스토어 (App Store for Websites)
- **목표**: 파편화된 웹사이트 정보를 31개 카테고리와 태그 시스템으로 분류하여 제공

### 1.2 타겟 유저
- **🕵️ 디스커버러 (Explorer)**: 심심할 때 새로운 게임, 심리테스트 등 킬링타임용 사이트를 찾는 유저
- **⚡️ 메이커/워커 (Maker/Worker)**: 업무 효율을 높여줄 유용한 도구나 디자인 소스를 찾는 실용주의 유저

---

## 🛠 기술 스택 (Tech Stack)

이 프로젝트는 **Next.js**를 기반으로 하며, 별도의 외부 데이터베이스 서버(RDS 등) 없이 **로컬 파일 기반 데이터베이스(SQLite)**를 사용하여 비용 효율성을 극대화합니다.

- **Framework**: [Next.js](https://nextjs.org/) (App Router, SSR)
- **Language**: TypeScript / JavaScript
- **Styling**: Vanilla CSS (Premium & Dynamic Design)
- **Database**: SQLite (In-project file storage for cost efficiency)
- **Deployment**: AWS Amplify
- **ORM**: Prisma (Recommended for schema management with SQLite)

---

## 🚀 메뉴 및 기능 (Features)

### 1. Discovery (추천)
운영자가 직접 큐레이션한 보석 같은 사이트들을 소개합니다.
- **Editor’s Choice**: 퀄리티 검증 완료된 추천 사이트 배너
- **Curated Collections**: 테마별 모음 (예: *No-Code Tools*, *Cozy Vibes*)

### 2. Trending (인기)
트래픽 데이터를 기반으로 신뢰할 수 있는 인기 순위를 제공합니다.
- **Top 10**: 이번 주 클릭 랭킹
- **Rising (Hot)**: 급상승 트래픽 사이트

### 3. Essentials (메이저)
일상적으로 사용하는 필수 사이트로 즉시 이동 가능한 '스피드 다이얼' 기능을 제공합니다.
- **Speed Dial**: Google, MS Copilot, Naver, YouTube, Netflix 등 로고 그리드 제공
- *특징*: 상세 페이지 없이 바로 Outlink 이동

### 4. Categories (카테고리)
명확한 목적이 있는 사용자를 위해 전 세계 웹사이트를 **31개 카테고리**로 분류했습니다.

---

## 🗂 데이터 구조 (Data Taxonomy)

### 카테고리 그룹 (Hierarchy)
- **A-E**: Art & Design, Business, Entertainment...
- **F-L**: Finance, Food & Drink, Games, Health, Lifestyle...
- **M-P**: Music, News, Productivity, Parenting...
- **S-W**: Shopping, Social, Sports, Tools, Travel, Weather...

### 태그 시스템 (Tagging)
- **Pricing**: `#Free`, `#Freemium`, `#Subscription`, `#Ad-Supported`
- **Access**: `#No Sign-up`, `#Mobile Friendly`, `#No Install`
- **Category Specific**: 
    - 개발: `#JSON`, `#Regex`
    - 디자인: `#Color`, `#Fonts`
    - 게임: `#Web Game`, `#IO Game`

---

## 💾 데이터베이스 스키마 (Schema)

데이터는 프로젝트 내부의 **SQLite** 파일에 저장됩니다.

### 1. `websites` (메인 테이블)
웹사이트의 핵심 정보를 담습니다.

| Field | Type | Description |
|-------|------|-------------|
| `id` | BigInt (PK) | 고유 ID |
| `url` | Varchar | 사이트 주소 (중복 체크) |
| `title` | Varchar | 사이트 이름 |
| `short_description` | Varchar | 한 줄 소개 |
| `detail_description` | Text | 상세 설명 |
| `thumbnail_url` | Varchar | 썸네일 경로 |
| `category` | Varchar | 카테고리 (Enum) |
| `monthly_traffic` | BigInt | 월간 트래픽 (정렬 기준) |
| `total_traffic` | BigInt | 누적 트래픽 |
| `is_featured` | Boolean | '추천' 노출 여부 |
| `is_essential` | Boolean | '메이저' 포함 여부 |
| `status` | Varchar | 상태 (ACTIVE, PENDING 등) |

### 2. `tags` (태그 정의)
| Field | Type | Description |
|-------|------|-------------|
| `id` | BigInt (PK) | 고유 ID |
| `name` | Varchar | 태그명 (예: #Free) |
| `type` | Varchar | 태그 그룹 (COST, TECH 등) |

### 3. `website_tags` (매핑)
`websites`와 `tags`의 N:M 연결 테이블입니다.

---

## 🏁 설치 및 실행 (Getting Started)

### 1. 프로젝트 클론 및 의존성 설치
```bash
npm install
```

### 2. 개발 서버 실행
```bash
npm run dev
```

### 3. 데이터베이스 설정 (Prisma 사용 시)
```bash
# 스키마 적용
npx prisma db push

# 프리즈마 스튜디오 실행 (데이터 관리)
npx prisma studio
```

### 4. 프로덕션 빌드
```bash
npm run build
npm start
```
