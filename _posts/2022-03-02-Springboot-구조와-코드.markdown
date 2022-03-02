---
layout: post
title:  "Springboot 구조와 코드"
categories: springboot
---

    board.xml

    <?xml version="1.0" encoding="UTF-8"?>  
    <!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">  
    <mapper namespace="com.example.springboot_practice.repository.BoardRepository">  
   
     <select id="getUserBoardData" resultType="com.example.springboot_practice.domain.Board">  
     SELECT  
     id, 
     title, 
     regdate, 
     publisher, 
     contents FROM board where publisher = #{userId}  
     </select>  
    </mapper>

repository에서 publisher를 파라미터(userId)로 받아(where publisher = #{userId}), boardData를 select한다.

    user.xml

    <?xml version="1.0" encoding="UTF-8"?>  
    <!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">  
    <mapper namespace="com.example.springboot_practice.repository.UserRepository">  
     <select id="getData" resultType="com.example.springboot_practice.domain.User">  
      SELECT  
     id, 
     name, 
     phone_number, 
     address, 
     birthday, 
     age, 
     type, is_use,
     regdate 
     FROM user WHERE id = #{userId}  
     </select>  
     
    </mapper>

repository에서 id를 파라미터(userId)로 받아(WHERE id = #{userId}), UserData를 select한다.

    Board.java(도메인)

    import com.fasterxml.jackson.annotation.JsonFormat;  
    import lombok.Data;  
      
    import java.time.LocalDate;  
      
    @Data  
    public class Board {  
    private Long id;  
     private String title;  
     private Long publisher;  
     private String contents;  
      @JsonFormat(pattern="yyyy-MM-dd")  
        private LocalDate regDate;  
    }

도메인은 리포지토리와 1대1로 맵핑된다. repository에서 id, title, publisher, contents, regDate를 맵핑한다.

    User.java(도메인)

    import com.fasterxml.jackson.annotation.JsonFormat;  
    import lombok.Data;  
      
    import java.time.LocalDateTime;  
      
    @Data  
    public class User {  
      
        private Long id;  
     private String name;  
     private int age;  
     private String birthday;  
     private String phone_number;  
     private String address;  
     private String type;  
     private int is_use;  
      
      @JsonFormat(pattern="yyyy-MM-dd HH:mm:ss")  
        private LocalDateTime regDate;  
    }
같은 방법으로 User테이블과 1대1 맵핑한다.

    BoardRepository.java

    @Mapper  
    public interface BoardRepository {  
        List<Board> getList();  
      
        List<Board> getUserBoardData(Long userId); //service에서 BoardData를 가져오는 용도로 사용  
    }
    UserRepository.java
    
    @Mapper  
    public interface UserRepository {  
        List<User> getList();  
      
      User getData(Long userId);  
    }

    ApiService.java

    import com.example.springboot_practice.repository.BoardRepository;  
    import com.example.springboot_practice.repository.UserRepository;  
    import lombok.RequiredArgsConstructor;  
    import org.springframework.stereotype.Service;  
      
    @Service  
    @RequiredArgsConstructor  
    public class ApiService {  
        private final BoardRepository boardRepository;  
     private final UserRepository userRepository;  
      
     public UserBoardDataResponseDto getUserBoardData(Long userId) {  
            UserBoardDataResponseDto dto = new UserBoardDataResponseDto();  
      
      User userData = userRepository.getData(userId);  
      
      dto.setUserId(userData.getId()); //userRepository에서 Id를 가져온(get) 후, dto의 userId에 저장(set)한다.  
      dto.setAddress(userData.getAddress()); //userRepository에서 Address를 가져온(get) 후, dto의 Address에 저장(set)한다.  
      dto.setAge(userData.getAge()); //userRepository에서 Age를 가져온(get) 후, dto의 Age에 저장(set)한다.  
      dto.setName(userData.getName()); //userRepository에서 Name을 가져온(get) 후, dto의 Name에 저장(set)한다.  
      dto.setBoardData(boardRepository.getUserBoardData(userData.getId())); //boardRepository의 boardData를 dto에 저장한다.  
      
      return dto; //dto 출력(userId, Address, Age, Name, boardData)  
      }  
    }

    UserBoardDataResponseDto.java(Dto:Data transfer object)
    
    import java.util.List;
    
      
      
    
    @Data
    
    public class UserBoardDataResponseDto {
    
    //Controller로 보낼 양식:
    
    private Long userId;
    
    private String name;
    
    private int age;
    
    private String address;
    
    private List<Board> boardData;
    
    }

    ApiController.java

        @RestController  
        @RequiredArgsConstructor  
        public class ApiController {  
            private final ApiService apiService;  
      
            @GetMapping("/api")  
                public UserBoardDataResponseDto getUserBoardData(@RequestParam Long userId) {  
                    return apiService.getUserBoardData(userId); //apiService에서 dto를 return한다.  
      }  
    }
ApiService에서 getUserBoardData의 리턴이 dto였으므로, 최종적으로 apiService에서 dto를 리턴한다.