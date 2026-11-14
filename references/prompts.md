# 생성 프롬프트와 작은 시험

근거: 원문 p.61–76, 99–100, 112–118.

프롬프트는 사건·인물 → 장소·상태 → 구도·이동 → 빛·물리·소리 순으로 정리한다. 추상적 미사여구 대신 실제 보일 정보와 유지 조건을 쓴다. 영어 입력문을 쓰더라도 대사는 원래 언어·문구 그대로 유지한다. 플랫폼 미정이면 모델 중립 초안이며 바로 실행했다고 말하지 않는다.

## 단일 숏 입력 골격

필요한 항목만 채우고 불필요한 항목은 제거한다. 확인하지 못한 fps·길이·오디오 기능을 API 파라미터로 만들지 않는다.

```text
Create a {duration}-second {style} shot.
Target framing: {aspect_ratio}. {Verified supported format constraints only.}
STORY: {visible event and audience information; intended emotional change}
CHARACTER: {ID plus actual visible appearance, wardrobe, distinguishing details}
LOCATION / PROPS: {time, spatial relations, prop shape, position, held hand}
REFERENCES: {each input's exact role and priority}
CAMERA: {shot size, height, location, direction; start framing -> movement -> end framing}
START: {character, gaze, hands, feet, prop and environment state}
ACTION: {one core action or a necessary short causal sequence; performance and response}
END: {actual target pose, gaze, held objects, next-shot link}
LIGHT: {source location, direction, visible contrast and color}
PHYSICS: {contact -> force/weight shift -> reaction; story-specific exception if any}
AUDIO IF SUPPORTED: {verbatim dialogue; relevant ambience, foley, effects, music}
KEEP: {necessary continuity constraints}
AVOID: {few highest-impact observable errors}
```

`AVOID`는 자연어 검토 항목이며 별도 네거티브 프롬프트 필드 지원을 뜻하지 않는다. 참조 없이 코드만 적지 않는다. 색·앵글의 감정 효과를 보장하지 않는다. 하나의 숏에 상충하는 고정/회전/이동을 넣지 않는다.

## 멀티컷

숏 시간표와 실제 생성 클립 대응을 먼저 만든다. 요청된 클립 전체 구간 안에서 각 컷의 시작/끝을 이어 놓고 의도하지 않은 시간 겹침과 빈칸을 검사한다. 통합 프롬프트에는 컷별 구도·행동·이동·인물·시선·의상·소품·차량·광원의 연결을 쓴다. 동일 사건을 개별 생성할 분할 대안도 제공한다.

컷 시간은 생성 목표이며 정확한 프레임 제어의 보장이 아니다. 20초는 안내서의 예시이지 고정 단위가 아니다. 멀티컷 미지원이면 단일 숏 클립과 편집 계획으로 전환한다. 전환 겹침은 생성 목표표와 편집 타임라인에서 구분한다.

## 시험과 실패 진단

1. 가장 위험한 핵심 동작을 확인 가능한 구도로 시험한다. 손 접촉을 먼 구도로 시험해 통과시키지 않는다.
2. 원문 사건, 동일성, 소품, 동작, 구도의 관찰 가능한 성공 조건을 미리 쓴다.
3. 프롬프트·참조·설정·시도 ID·출력·사용량을 묶어 기록한다. 실제로 지원되거나 사용한 설정만 기록한다.
4. 오류를 위치와 현상으로 쓴다. 예: 접촉 전에 봉투가 이동함. 원인을 단정하지 말고 이야기/외형/카메라/물리/편집 가설을 구분한다.
5. 주요 변수 하나부터 바꾸고 같은 재생 속도·화면 크기로 비교한다. 확률적 출력이므로 한 결과만으로 인과를 확정하지 않는다. 잘됐던 조건의 회귀도 본다.
6. 반복 실패 또는 승인된 시도·비용 한도에 도달하면 필요한 동작만 분할하거나 반응 숏·소품 클로즈업·실사/합성을 제안한다. 끝없는 자동 재시도는 하지 않는다.

분할 후 손·소품 방향과 속도, 시작/끝, 편집 여유와 소리 연결을 검사한다. 수정 때문에 원문 사건을 바꾸지 않는다. 최종 채택 파일과 버전, 실제 시작/끝, 후반 수정 항목을 인계한다.
