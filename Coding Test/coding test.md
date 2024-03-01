# 완주하지 못한 선수
```python
import collections
def solution(participant, completion): 
	answer = collections.Counter(participant) - collections.Counter(completion) 
	return list(answer.keys())[0]
```
- collections.Counter: 
	- iterable(리스트, 문자열 등)에서 요소의 개수를 세어서, 요소를 키로 하고 해당 요소의 개수를 값으로 하는 딕셔너리 형태의 객체를 생성

