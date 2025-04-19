---
title: "Repo"
weight: 7
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
bookComments: false
# bookSearchExclude: false
---

## 4세대 VCS

### Monorepo vs Multirepo

모노레포(Monorepo)와 멀티레포(Multirepo)는 현대 소프트웨어 개발에서 가장 중요한 버전 관리 전략입니다.

#### 모노레포 (Monorepo)
- **정의**: 여러 프로젝트의 코드를 단일 저장소에서 관리하는 방식
- **장점**:
  - 코드 공유와 재사용이 용이
  - 원자적 커밋으로 cross-project 변경 관리 가능
  - 통합된 CI/CD 파이프라인 구성 가능
  - 일관된 개발 환경과 도구 사용
- **단점**:
  - 저장소 크기가 커져 성능 이슈 발생 가능
  - 접근 권한 관리가 복잡
  - 빌드 시간이 길어질 수 있음

#### 멀티레포 (Multirepo)
- **정의**: 각 프로젝트를 독립된 저장소에서 관리하는 방식
- **장점**:
  - 프로젝트별 독립적인 버전 관리
  - 더 명확한 접근 권한 관리
  - 저장소별 가벼운 크기 유지
- **단점**:
  - 코드 재사용이 어려움
  - 프로젝트 간 종속성 관리가 복잡
  - 여러 프로젝트에 걸친 변경사항 관리가 어려움

### 대규모 기업의 VCS 솔루션

#### VFSforGit
- Microsoft가 개발한 가상 파일 시스템 기반 Git 확장
- 대규모 Git 저장소를 효율적으로 관리
- 필요한 파일만 선택적으로 다운로드하여 작업 가능

#### Google Piper
- Google의 자체 개발 중앙집중식 VCS
- 수백만 커밋과 페타바이트 규모의 코드 관리
- 강력한 코드 검색과 분석 기능 제공

### 현대적 VCS 트렌드
1. **하이브리드 접근**
   - 모노레포와 멀티레포의 장점을 결합
   - 메인 프로젝트는 모노레포로, 독립적인 서비스는 멀티레포로 관리

2. **확장성 중심 도구**
   - Git의 한계를 극복하는 새로운 도구들 등장
   - 클라우드 네이티브 VCS 솔루션 증가

3. **자동화 통합**
   - CI/CD 파이프라인과의 긴밀한 통합
   - 자동화된 코드 리뷰와 품질 관리

[^vfsforgit]: [VFS for Git - Microsoft](https://vfsforgit.org/)
[^piper]: [Google's Piper Version Control System](https://research.google/pubs/pub45424/)