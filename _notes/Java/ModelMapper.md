#변환 

**ModelMapper**는 **DTO(Data Transfer Object)와 엔티티(Entity) 간의 매핑을 자동화**하는 Java 라이브러리

객체 간 변환을 간편하게 할 수 있어서 **중복 코드 감소, 유지보수성 향상** 등의 장점이 있다.

---

**ModelMapper의 주요 기능**

✔️ 필드명이 같으면 자동 매핑

✔️ DTO ↔ Entity 변환을 간편하게 처리

✔️ 복잡한 객체 구조도 매핑 가능

✔️ 커스텀 매핑 가능


**ModelMapper 사용법**
```Java
implementation 'org.modelmapper:modelmapper:3.1.1' // 의존성 추가
```


**ModelMapper 설정 (Bean 등록)**
```Java
@Configuration
public class ModelMapperConfig {

    @Bean
    public ModelMapper modelMapper() {
        return new ModelMapper();
    }
    
}
```


**ModelMapper 사용 예제**
```Java
@Getter
@Setter
public class UserDto {

    private Long id;
    private String name;
    private String email;

}


@Entity
@Getter
@Setter
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;
}
```


***엔티티 → DTO 변환***
```Java
@Service
public class UserService {

    private final ModelMapper modelMapper;

    public UserService(ModelMapper modelMapper) {
        this.modelMapper = modelMapper;
    }

    public UserDto convertToDto(User user) {
        return modelMapper.map(user, UserDto.class);
    }
}

```


**DTO → 엔티티 변환**
```Java
public User convertToEntity(UserDto userDto) {
    return modelMapper.map(userDto, User.class);
}
```

---
**ModelMapper의 장점**

✅ **코드 중복 감소** → setId(), setName() 같은 매핑 코드를 일일이 작성할 필요 없음

✅ **유지보수성 향상** → 필드가 추가되더라도 수정이 적음

✅ **객체 변환 로직 단순화** → map() 메서드 한 줄로 변환

==**ModelMapper 사용 시 주의할 점**==

**필드명이 다르면 매핑이 안 됨**
→ modelMapper.addMappings()를 사용해 매핑 설정 가능
```Java
modelMapper.typeMap(User.class, UserDto.class)
    .addMapping(User::getName, UserDto::setName);
```

**성능 이슈**
→ 내부적으로 리플렉션(Reflection)을 사용하기 때문에 대량(갯수) 데이터 변환 시 속도가 느려질 수 있음.
[[리플렉션]]

대량 데이터 변환이 필요하면 
1. 직접 매핑하는 방법
2. [[MapStruct]]사용 (컴파일 타임 변환)
