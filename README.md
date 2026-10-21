# Magnetic Chess

보드 위에 자석 공을 놓아 상대의 공을 끌어당기고, 자기 조각을 먼저 0으로 만드는 쪽이 이기는 2인 턴제 보드게임입니다.
Google Play에 출시해 운영 중이며, 1인 개발했습니다.

**[🎮 Google Play에서 플레이하기](https://play.google.com/store/apps/details?id=com.developerjw.magenticchess.mobile)**
· [📄 개발 기록 (포트폴리오 페이지)](https://developer-jiwookim.github.io/Magnetic-Chess/)
· [▶ 플레이 영상](https://youtu.be/SnjKNFRUPV0)

포트폴리오 페이지에는 자석 물리(길버트 힘) 계산, 오브젝트 풀링, 턴 상태 관리 구현과
Unity 2022 → Unity 6 마이그레이션 과정에서 찾아낸 버그들을 정리해 두었습니다.

---

## 이 저장소에 대해

이 저장소는 **코드 열람용**입니다. 직접 작성한 C# 스크립트와 개발 문서만 담았고,
씬·프리팹·모델·텍스처·사운드 등 리소스는 포함하지 않았습니다.
게임에 사용한 외부 에셋은 라이선스상 원본을 공개 저장소에 재배포할 수 없기 때문입니다.
따라서 이 저장소만으로는 Unity 프로젝트를 열거나 빌드할 수 없으며, 플레이는 Google Play 출시 버전으로 할 수 있습니다.

| 항목 | 내용 |
|---|---|
| 엔진 | Unity 6 (6000.5.3f1) · URP 17.5 |
| 플랫폼 | Android (IL2CPP · ARM64) |
| 최신 버전 | 1.1.0 (versionCode 20) |
| 스크립트 | C# 50개 · 2,967 lines |
| 모드 | AI 대전 · 오프라인 2인 대전 |

## 저장소 구성

```
Assets/MyAssets/Scripts/
├── Core/       데이터 저장, 게임 설정, 사운드, 씬 전환, Singleton<T>   (7)
├── Magnet/     길버트 힘 계산, 자석볼 스폰·풀링, 충돌 판정             (5)
├── Match/      경기 진행, TurnStateMachine, MatchTimer, 인게임 UI      (12)
├── MainMenu/   타이틀, 모드 선택, 게임 설정 패널                      (14)
├── UI/         공용 패널(UIPanel 기반), 메뉴바, 옵션                  (11)
└── AI/         빈 자리 탐색 후 배치 지점 결정                         (1)
docs/              포트폴리오 페이지 (GitHub Pages)
REFACTORING_LOG.md Unity 6 이식 과정의 리팩토링 기록
```

먼저 보면 좋은 파일:

- [`Magnet/MagnetWorld.cs`](Assets/MyAssets/Scripts/Magnet/MagnetWorld.cs) — 매 물리 프레임 O(n²) 자력 계산, 네이티브 호출 캐싱
- [`Magnet/MagnetBallSpawner.cs`](Assets/MyAssets/Scripts/Magnet/MagnetBallSpawner.cs) — `ObjectPool<T>` 기반 풀링과 사전 생성
- [`Match/TurnStateMachine.cs`](Assets/MyAssets/Scripts/Match/TurnStateMachine.cs) · [`Match/MatchTimer.cs`](Assets/MyAssets/Scripts/Match/MatchTimer.cs) — Unity API에 의존하지 않는 순수 C# 규칙 클래스
- [`AI/AI_FSM.cs`](Assets/MyAssets/Scripts/AI/AI_FSM.cs) — 안전 반경을 좁혀 가며 배치 지점을 찾는 AI

---

## 외부 에셋 / 라이선스

### 외부 에셋

게임의 3D 배경·캐릭터·일부 UI와 사운드는 Unity Asset Store에서 구매하거나 무료로 받은 에셋을 사용했습니다.
에셋 원본은 공개 저장소에 재배포할 수 없어 이 저장소에는 포함하지 않았습니다.

### 아이콘 (Flaticon)

게임 UI 아이콘은 [Flaticon](https://www.flaticon.com/)의 무료 아이콘을 출처 표기 조건으로 사용했습니다.

| 아이콘 | 제작자 |
|---|---|
| [AI 대전](https://www.flaticon.com/kr/free-icons/ai-) · [메뉴](https://www.flaticon.com/kr/free-icons/) · [분쟁](https://www.flaticon.com/kr/free-icons/) · [종료(resume)](https://www.flaticon.com/free-icons/end) · [선택](https://www.flaticon.com/kr/free-icons/) · [좌우 이동](https://www.flaticon.com/kr/free-icons/) | Freepik |
| [로그아웃(exit)](https://www.flaticon.com/kr/free-icons/-) | Ardiansyah |
| [설정](https://www.flaticon.com/kr/free-icons/) | Gregor Cresnar |
| [온라인](https://www.flaticon.com/kr/free-icons/) | Muhammad_Usman |
| [다시 하기](https://www.flaticon.com/kr/free-icons/) | Debi Alpa Nugraha |
| [계속하기](https://www.flaticon.com/kr/free-icons/) | Catalin Fertu |
| [도움말](https://www.flaticon.com/free-icons/help) | susannanovaIDR |

### 폰트

| 폰트 | 용도 | 라이선스 |
|---|---|---|
| [SUITE](https://sun.fo/suite/) | 게임 UI | SIL Open Font License 1.1 |
| Diphylleia | 게임 UI | SIL Open Font License 1.1 |
| [둘기마요](https://blog.naver.com/dovemayo_/223003707589) | 개발자 로고 | 무료 사용 허용 (제작자 고지) |

### 이 저장소의 코드

이 저장소의 C# 코드와 문서는 [MIT License](LICENSE)로 공개합니다.
MIT License는 이 저장소에 포함된 파일에만 적용되며, 위에 적은 외부 에셋·아이콘·폰트에는 각 제작자의 라이선스가 적용됩니다.
