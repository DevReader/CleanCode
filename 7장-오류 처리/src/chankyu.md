# 7장 오류처리

## 수정 전
```ts
function useCreateShift() {
  ...

  const autoCompleteShift = async () => {
    if (!shift || !wardShiftTypeMap || !wardId) return;
    if (shift?.divisionShiftNurses.flatMap((x) => x).length < 10) {
      toast.error('자동완성 기능을 사용하시려면 최소 10명의 간호사가 필요합니다');
      return;
    }
    if (
      !confirm(
        '근무표를 자동으로 채우시겠습니까?\n신청 근무를 최대한 반영한 채 채워집니다.\n약 1분~2분이 소요됩니다!'
      )
    )
      return;
    setLoading(true);
    
    ...
}
```

## 수정 후
```ts
function useCreateShift() {
  
  ...

  const validateShift = () => {
    if (!shift || !wardShiftTypeMap || !wardId) throw new Error('근무 혹은 병동 ID가 없ㅅ브니다');
    if (shift.divisionShiftNurses.flatMap(x => x).length < 10) throw new Error('자동완성 기능을 사용하시려면 최소 10명의 간호사가 필요합니다');
  };

  ...
}

```

### 명백한 예외처리
- 필수 데이터 누락, 필수 조건 누락에 대해 예외를 던지게 변경하였다