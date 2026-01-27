# PlayerPrefs

&#x20;`PlayerPrefs`는 Player Preference의 줄임말이고 적당한 방식으로 어떤 값들을 로컬에 저장하고 불러올 수 있는 메소드를 제공한다. 사이즈가 큰 데이터를 저장하는 자료구조가 그렇듯 key-value의 형태를 띄고 있다.

&#x20;신기하게 `PlayerPrefs.SetFloat(string key, float value)`라는 메소드가 소개되어 있는데 왜 굳이?? 라는 느낌이 든다. 받는 type에 맞게 함수 override가 안되어 있는건가?? 찾을 때도 GetFloat 이런 식이다. 좀 불편한 것 같다.

&#x20;key에 대응되는 value가 있는지 궁금하다면 `bool PlayerPrefs.HasKey(string key)`로 체크하면 된다.

&#x20;
