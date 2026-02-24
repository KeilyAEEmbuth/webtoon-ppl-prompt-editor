# Image Attributes Example - Mountain Stairway Scene (One Character)

![Rural Market Scene with Overhead View](../images/one_man_scene_example.png)

## 이미지 설명

산악 계단길에서 한 명의 인물이 지팡이를 짚고 열심히 올라가는 긴장감 있는 액션 장면입니다.

---

## JSON 구조화 데이터

```json
{
  "schema_version": "1.0",
  "scene": {
    "scene_type": "exterior",
    "location": "mountain_path_stairway",
    "tone": "tense_action",
    "narrative_perspective": "character_focus",
    "context_summary": "A single character hurriedly climbs a steep outdoor stairway using a walking stick, showing signs of exertion and urgency."
  },
  "objects": [
    {
      "object_id": "human_01",
      "object_type": "human",
      "role": "traveler",
      "position": "center_foreground",
      "orientation": "upward",
      "facial_visibility": "hidden",
      "emotional_state": "strained",
      "gesture": "leaning_forward",
      "action": "running_up_stairs",
      "clothing": {
        "outerwear_type": "robe",
        "primary_color": "light_brown"
      },
      "tool_used": "object_01"
    },
    {
      "object_id": "object_01",
      "object_type": "object",
      "sub_type": "tool",
      "position": "center_foreground",
      "associated_with": "human_01",
      "function": "walking_support",
      "state": "in_use"
    }
  ],
  "environment_objects": [
    {
      "object_id": "env_01",
      "object_type": "object",
      "sub_type": "stairway",
      "position": "foreground",
      "semantic_role": "movement_path"
    },
    {
      "object_id": "env_02",
      "object_type": "object",
      "sub_type": "rope",
      "position": "foreground",
      "semantic_role": "safety_support"
    },
    {
      "object_id": "env_03",
      "object_type": "object",
      "sub_type": "rock_cliff",
      "position": "background",
      "semantic_role": "terrain_boundary"
    }
  ],
  "text_elements": [
    {
      "text_id": "text_01",
      "text": "후우!",
      "language": "ko",
      "text_type": "sound_effect",
      "position": "center_foreground",
      "semantic_function": "exertion"
    },
    {
      "text_id": "text_02",
      "text": "후우!",
      "language": "ko",
      "text_type": "sound_effect",
      "position": "upper_midground",
      "semantic_function": "exertion"
    },
    {
      "text_id": "text_03",
      "text": "타박",
      "language": "ko",
      "text_type": "sound_effect",
      "position": "lower_foreground",
      "semantic_function": "footstep"
    }
  ],
  "relationships": [
    {
      "source": "human_01",
      "target": "object_01",
      "relationship_type": "using_tool"
    },
    {
      "source": "human_01",
      "target": "env_01",
      "relationship_type": "moving_through",
      "direction": "upward"
    }
  ],
  "implicit_information": {
    "social_context": "journey_or_escape",
    "power_dynamic": "environment_over_character",
    "shared_experience": "physical_exertion",
    "ppl_potential": "low",
    "ppl_reason": "Action-focused scene with no consumer-facing product exposure"
  }
}
```

---

## Schema Compliance Report (스키마 적합성 검사)

### ✓ 통과 항목

| 항목 | 상태 | 설명 |
|------|------|------|
| `schema_version` | ✓ PASS | "1.0" 올바르게 지정 |
| `scene.scene_type` | ✓ PASS | "exterior" - 정의된 enum 값 |
| `scene.narrative_perspective` | ✓ PASS | "character_focus" - 정의된 enum 값 |
| `objects[]` 구조 | ✓ PASS | object_id, object_type 필수 필드 모두 포함 |
| Object 타입 분류 | ✓ PASS | human, object 올바르게 사용 |
| Human 속성 | ✓ PASS | role, position, facial_visibility, emotional_state, gesture, action, clothing, tool_used 모두 포함 |
| Object 속성 | ✓ PASS | sub_type, position, associated_with, function, state 적절히 포함 |
| `environment_objects[]` 구조 | ✓ PASS | object_id, object_type, sub_type 필수 필드 포함 |
| `text_elements[]` | ✓ PASS | 모든 필수 필드(text_id, text, language, text_type) 포함, 3개 요소 적절 |
| `relationships[]` | ✓ PASS | source, target, relationship_type 필수 필드 포함, 2개 관계 정의 |
| `implicit_information` | ✓ PASS | 주요 필드(social_context, power_dynamic, ppl_potential) 포함 |
| Clothing 구조 | ✓ PASS | outerwear_type, primary_color 정상 정의 |

### ⚠ 주의 항목

| 항목 | 심각도 | 설명 |
|------|--------|------|
| `scene.tone` | ⚠ WARN | "tense_action"은 스키마의 정의된 enum에 없음 |
| | | 권장값: `warm_casual`, `comedic_tension`, `serious`, `romantic`, `neutral` |
| | | → 수정 권장: `"serious"` 또는 `"tense"` 개념 추가 검토 필요 |
| `human_01.orientation` | ⚠ WARN | "upward"는 스키마의 정의된 enum에 없음 |
| | | 권장값: `front`, `back`, `left`, `right`, `side`, `unknown` |
| | | → 수정 권장: 신체 방향으로 해석 시 `"front"` 또는 `"back"` 사용 |
| `environment_objects[].sub_type` | ⚠ WARN | "stairway", "rope", "rock_cliff" - 모두 스키마 예시에 미포함 |
| | | 권장값: `furniture`, `signage`, `device`, `vehicle`, `other` |
| | | → 수정 권장: `"furniture"` (계단), `"other"` (로프, 바위) 또는 더 일반화된 분류 |
| `text_elements[2].position` | ⚠️ INFO | "lower_foreground"는 스키마 position enum에 정의되지 않음 |
| | | 권장값: `left_foreground`, `center_foreground`, `right_foreground`, `foreground` 등 |
| | | → 수정 권장: `"center_foreground"` 사용 |

### ✓ 데이터 일관성 검증

| 검증 항목 | 결과 | 상세 |
|----------|------|------|
| 고유 ID | ✓ PASS | 모든 object_id, text_id 중복 없음 (human_01, object_01, env_01~03, text_01~03) |
| ID 참조 일관성 | ✓ PASS | tool_used: "object_01" → objects[]에 존재 ✓ |
| | ✓ PASS | relationships source/target → 모두 존재하는 ID 참조 ✓ |
| 타입별 속성 사용 | ✓ PASS | human의 선택적 속성만 human_01에 사용됨 ✓ |
| | ✓ PASS | object의 선택적 속성만 object_01에 사용됨 ✓ |
| Enum 값 | ⚠ WARN | scene.tone, human_01.orientation, environment_objects sub_type, text_elements position 미정의 값 사용 |

### 📋 최종 평가

**적합성 점수: 78/100**

**판정:** ⚠️ **조건부 통과** - 구조적 적합성은 우수하나 enum 값 표준화 필요

#### 주요 문제점 분석

1. **scene.tone** (높은 우선순위)
   - 현재: `"tense_action"`
   - 원인: 웹툰 액션 장면의 톤을 나타내려 했으나 스키마 enum 누락
   - 영향: 장면의 감정 톤 분류 일관성 저해
   - 권장: `"serious"` 또는 스키마에 `"tense"` enum 추가

2. **human_01.orientation** (중간 우선순위)
   - 현재: `"upward"`
   - 원인: 캐릭터가 위쪽을 바라본다는 뜻이지만, 스키마의 orientation은 신체 방향을 의미
   - 영향: 신체 방향 메타데이터 혼동
   - 권장: 신체 방향으로 재해석하여 `"front"` 또는 `"back"` 사용

3. **environment_objects sub_type들** (중간 우선순위)
   - 현재: `"stairway"`, `"rope"`, `"rock_cliff"`
   - 원인: 장면의 구체적인 환경 요소를 최대한 정확히 표현하려는 의도
   - 영향: 환경 객체 분류 일관성 저해
   - 권장: 
     ```json
     "stairway" → "furniture" 또는 "architectural_element"
     "rope" → "other" 또는 "safety_equipment"
     "rock_cliff" → "other" 또는 "natural_feature"
     ```

4. **text_elements[2].position** (낮은 우선순위)
   - 현재: `"lower_foreground"`
   - 원인: 세부 위치 표현
   - 권장: `"center_foreground"` 또는 `"foreground"`

#### 권장 수정사항

**버전 1 - 기존 스키마 준수:**
```json
{
  "scene": {
    "tone": "serious"  // 기존: "tense_action"
  },
  "objects": [{
    "orientation": "front"  // 기존: "upward"
  }],
  "environment_objects": [
    {"sub_type": "furniture"},      // 기존: "stairway"
    {"sub_type": "other"},          // 기존: "rope"
    {"sub_type": "other"}           // 기존: "rock_cliff"
  ],
  "text_elements": [{
    "position": "center_foreground" // 기존: "lower_foreground"
  }]
}
```

#### 스키마 개선 제안 (v1.1 업데이트)

`orientation` enum 확장 제안:
- 현재: `front`, `back`, `left`, `right`, `side`, `unknown`
- 제안: `upward`, `downward` 추가 (특히 계단 장면에 유용)

`scene.tone` enum 확장 제안:
- 현재: `warm_casual`, `comedic_tension`, `serious`, `romantic`, `neutral`
- 제안: `tense_action`, `dramatic`, `suspenseful` 추가

`environment_objects.sub_type` 확장 제안:
- 현재: `furniture`, `signage`, `device`, `vehicle`, `other` (예시)
- 제안: `architectural_element`, `natural_feature`, `safety_equipment`, `structural_support` 추가

---

## 종합 의견

이 JSON은 **액션 씬의 긴장감과 움직임을 매우 잘 표현**하고 있습니다:

✓ **강점:**
- 캐릭터의 감정 상태(`strained`), 제스처(`leaning_forward`), 행동(`running_up_stairs`)의 일관성
- 효과음 3개로 행동의 역동성 표현 (`후우!`, `후우!`, `타박`)
- 환경과 캐릭터의 관계 정의 (moving_through, using_tool)
- 암묵적 정보가 장면의 서사적 맥락을 잘 담음

⚠️ **개선점:**
- 스키마 정의 enum 값 준수로 데이터 표준화 필요
- 향후 스키마 확장 시 이러한 값들이 추가될 가능성 높음

