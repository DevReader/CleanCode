# 4장 주석
## 내용 정리
### 코드만으로 의도를 표현한다
- 주석을 달기 보다는 코드를 개선한다
- 예외: 의미/의도를 명확히 하거나 경고하는 주석

## 사례 적용
### 사례 1
**❓ 어느 쪽이 의도가 명확해 보일까?**
- 인라인으로 작성하기
```
if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem())) { ... }
```

- 변수 만들기
```
ArrayList moduleDependees = smodule.getDependSubsystems();
String outSubSystem = subSysMod.getSubSystem();
if (moduleDependees.contains(outSubSystem)) { ... }
```