# HydroPulse 프로젝트 정의 / Project Scope

## 한국어

**목표** — 운동 시간, 운동 중 평균 심박수, 평소 체중으로 운동 종료 시점의 수분 손실량을 추정하고, 이를 기준으로 운동 후 수분 보충량을 mL 단위로 안내한다.

| 항목 | 한 줄 정의 | 단위·데이터 |
|---|---|---|
| 운동 시간 | 한 번의 운동을 시작해서 마칠 때까지의 경과 시간이다. | 분 · `Session_Duration (hours)` × 60 |
| 평균 심박수 | 해당 운동 세션에서 측정한 분당 심박수의 평균이다. | bpm · `Avg_BPM` |
| 평소 체중 | 사용자 프로필에 등록해 운동 세션마다 재사용하는 기준 체중이다. | kg · `Weight (kg)` |
| 운동 후 추정 수분 보충량 | 운동 종료 시점의 추정 순수분 손실량을 바탕으로 사용자에게 안내하는 보충량이다. | mL · 시스템 출력 |

첫 버전은 위 세 가지 입력을 사용한다. 사용자가 운동 유형이나 이전 수분 섭취량을 입력할 필요는 없다.

**학습 및 검증 기준** — `Water_Intake (liters)`의 측정 시점과 정의는 확인이 필요하다. 실제로 마신 양을 기록한 값이라면 보충 필요량의 정답으로 사용하지 않는다. 검증용 세션에서는 운동 전후 체중 차이로 순수분 손실량을 추정하고 모델의 손실량 예측과 비교한다. 이 값은 수분 보충 안내의 근거이며 개인의 정확한 섭취 필요량을 직접 측정한 값은 아니다. 평균 절대 오차(MAE)는 세션별 예측값과 기준값 차이의 절댓값을 평균해 mL로 보고한다. 운동 전후 체중 측정은 검증에만 사용한다.

## English

**Objective** — Estimate fluid loss at the end of exercise from session duration, average exercise heart rate, and usual body weight. Use that estimate to suggest a post-exercise fluid intake in mL.

| Item | One-line definition | Unit and data |
|---|---|---|
| Exercise duration | The elapsed time from the start to the end of one exercise session. | Minutes · `Session_Duration (hours)` × 60 |
| Average heart rate | The mean heart rate, in beats per minute, measured during that session. | bpm · `Avg_BPM` |
| Usual body weight | The baseline weight stored in the user's profile and reused across sessions. | kg · `Weight (kg)` |
| Estimated post-exercise fluid intake | The amount of fluid suggested to the user based on estimated net fluid loss at the end of the session. | mL · system output |

The first version uses the three inputs above. Users do not need to enter their workout type or previous fluid intake.

**Training and validation reference** — The timing and definition of `Water_Intake (liters)` still need to be confirmed. If it records actual consumption, do not use it as the ground truth for fluid replacement needs. For validation sessions, estimate net fluid loss from the change in body weight before and after exercise, then compare it with the model's fluid-loss prediction. This reference informs the suggested intake and does not directly measure an individual's exact intake requirement. Report mean absolute error (MAE) in mL by averaging the absolute differences between predictions and reference values across sessions. Weigh-ins before and after exercise are for validation only.
