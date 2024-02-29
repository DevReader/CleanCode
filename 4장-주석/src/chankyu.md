# 4장 주석

```ts
type Nurse = {

/** 간호사 id */
nurseId: number;
/** 계정 id */
accountId: number | null;
/** 간호 팀 아이디 */
shiftTeamId: number | null;
/** 병동 id */
wardId: number;
/** 간호사 이름 */
name: string;
/** 간호사 전화번호 */
phoneNum: string;
/** 간호사 연동 여부 */
isConnected: boolean;
/** 근무 리스트 */
nurseShiftTypes: {
	nurseShiftTypeId: number;
	name: string;
	shortName: string;
	isPossible: boolean;
	isPreferred: boolean;
}[];
/**근무표에 들어가는 사람인가? */
isWorker: boolean;
/**근무표 제작 권한 */
isDutyManager: boolean;
/**병동 관리 권한 */
isWardManager: boolean;
/**성별 */
gender: string;
/**입사날짜 */
employmentDate: string;
memo: string;
isDeleted: boolean;
/** 구분 인덱스 */
divisionNum: number;
/** 구분 내 인덱스 */
priority: number;
};
```
### 같은 이야기를 중복하는 주석
- 이름을 충분히 잘 이해하게 지었음에도 주석이 굳이 한글로 번역해서 남겨져있음.
- 그 중 주석이 필요한 이름들은, 주석이 필요없는 이름으로 바꿔야 함.
- 타입의 모든 속성에 주석을 달아야 한다는 규칙보다는 속성 이름이 길어지더라도 주석을 사용하지 않는 것을 지양하자.

```js
/** GET `/wards/${wardId}/shift-teams/${shiftTeamId}/req-duty` */
const getReqShift = async (wardId: number, shiftTeamId: number, year: number, month: number) =>
(
	await axiosInstance.get<RequestShift>(
`/wards/${wardId}/shift-teams/${shiftTeamId}/req-duty?${qs.stringify({ year, month })}`
	)
).data;
```
### jsdoc을 위해 작성한 주석
- 다른 곳에서 getReqShift를 사용할 때, 그 API의 주소를 알 필요가 있는가?
- 어차피 props만 잘 넘겨주면 알아서 작동한다.
- 굳이 주소를 노출시킬 필요가 없다.

결국 4장의 핵심은 주석을 쓰지말자가 아니라, 주석을 쓰기전에 최대한 코드를 잘 보살펴서 주석을 쓰지 않아도 되는 코드를 만들자이다. 주석이 무조건 필요한 코드를 찾기는 쉽지 않았다. 작성할 때 이 주석이 있으면 이해하기 쉽겠지라는 생각으로 작성했었다.
