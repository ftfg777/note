#변환 

**MapStruct**는 **DTO ↔ Entity 변환을 자동으로 처리하는 Java 라이브러리**
다만 ModelMapper와 다르게 **컴파일 타임에 변환 코드를 생성**해서 **성능이 빠름**

**즉, 리플렉션을 사용하지 않아서 ModelMapper보다 성능이 좋고, 안정적인 변환이 가능**

---

**MapStruct의 특징**

✅ 컴파일 타임에 변환 코드 생성 → 성능이 빠름

✅ 리플렉션 없이 변환 → 런타임 성능 저하 없음

✅ 코드 자동 생성 → DTO ↔ Entity 변환 코드 줄어듦

✅ 커스텀 매핑 가능 → 복잡한 변환도 지원


**MapStruct 설정**

```Java
dependencies {
    implementation 'org.mapstruct:mapstruct:1.5.5.Final'
    annotationProcessor 'org.mapstruct:mapstruct-processor:1.5.5.Final'
}
```
 annotationProcessor는 MapStruct가 변환 코드를 **컴파일 시 자동 생성**하는데 필요


**MapStruct 사용법**
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

**Mapper 인터페이스 작성**
```Java
import org.mapstruct.Mapper;
import org.mapstruct.Mapping;
import org.mapstruct.factory.Mappers;

@Mapper
public interface UserMapper {
    UserMapper INSTANCE = Mappers.getMapper(UserMapper.class);

    UserDto toDto(User user);  // Entity → DTO 변환
    User toEntity(UserDto userDto);  // DTO → Entity 변환
}
```
UserMapper.INSTANCE.toDto(user) 이렇게 사용하면 User → UserDto 변환 가능
MapStruct는 **컴파일 시 UserMapperImpl이라는 변환 클래스를 자동으로 생성**


**Mapper 사용법**
```Java
UserDto userDto = UserMapper.INSTANCE.toDto(user);
User userEntity = UserMapper.INSTANCE.toEntity(userDto);
```
**ModelMapper처럼 map()을 쓰는 게 아니라, toDto()나 toEntity() 메서드를 직접 호출**
ModelMapper보다 **성능이 빠르고 안정적**

---

**MapStruct 커스텀 매핑**

**필드명이 다를 때**
```Java
@Mapper
public interface UserMapper {
					// email → userEmail 로 매핑
    @Mapping(source = "email", target = "userEmail")  
    UserDto toDto(User user);
}
```

**특정 필드 제외하기**
```Java
@Mapper
public interface UserMapper {
    @Mapping(target = "email", ignore = true)  // email 필드 제외
    UserDto toDto(User user);
}
```


**MapStruct vs ModelMapper**

| **비교 항목**    | **MapStruct**    | **ModelMapper**      |
| ------------ | ---------------- | -------------------- |
| **매핑 방식**    | 컴파일 타임 코드 생성     | 런타임 리플렉션             |
| **성능**       | 빠름               | 상대적으로 느림             |
| **설정 필요 여부** | @Mapper 인터페이스 작성 | modelMapper.map() 호출 |
| **유지보수성**    | 명확한 코드           | 필드 변경 시 오류 발생 가능     |
| **추천 사용 경우** | **대량 데이터 변환**    | **소규모 변환 & 빠른 개발**   |
