---
layout: post
title:  "springboot에서 controller, service, repository 역할"
date:  2022-02-15 21:51:36
categories: springboot
---

<img src="https://cndiqor0512.github.io/img/Springboot각역할.png">

 위 그림은 springboot가 작동하는 과정을 나타낸 것이다.

 Controller에서 사용자의 요청을 받고 Service로 전송하면, Service에서는 전송받은 요청을 바탕으로 로직을 실행한다. 로직을 실행하는 과정에서 DB의 사용은 Repository에서 담당하며, 로직을 실행한 뒤 리턴을 Controller로 보내면, Controller에서는 로직 결과를 출력한다.

예제:
     
    Controller
    
    import com.example.springboot_practice.domain.User;  
    import com.example.springboot_practice.service.UserService;  
    import lombok.Getter;  
    import lombok.RequiredArgsConstructor;  
    import org.springframework.web.bind.annotation.GetMapping;  
    import org.springframework.web.bind.annotation.RestController;  
    import java.util.List;  
      
    @RestController  
    @RequiredArgsConstructor  
      
    public class UserController {  
        private final UserService userService;  
      
      @GetMapping("/user")  
        public List<User> getList() {  
            return userService.getList();  
      }


    Service
    
    import com.example.springboot_practice.domain.User;  
    import com.example.springboot_practice.repository.UserRepository;  
    import lombok.RequiredArgsConstructor;  
    import org.springframework.stereotype.Service;  
    import java.util.List;  
      
    @Service  
    @RequiredArgsConstructor  
    public class UserService {  
        private final UserRepository userRepository;  
      
     public List<User> getList() {  
            return userRepository.getList();  
      }  
    }


    Repository
    
    import com.example.springboot_practice.domain.User;  
    import org.apache.ibatis.annotations.Mapper;  
      
      
    import java.util.List;  
      
    @Mapper  
    public interface UserRepository {  
        List<User> getList();  
    }


