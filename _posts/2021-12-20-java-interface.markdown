---
layout: post
title:  "자바 인터페이스"
date:  2021-12-22 14:44:59
categories: java
---


  # **자바 인터페이스**

 - 인터페이스(Interface)란? 

사물과 사물 또는 사물과 인간 사이의 소통의 매개체.

- 인터페이스의 필요성: 코드의 단순화
- 인터페이스의 선언: implements를 통해 클래스에서 선언함

인터페이스 예제:
# library 패키지:
- 인터페이스 Book
- Main클래스
- Les miserables
- LittlePrince
- Remeo and Juliet

    public interface Book {
    
    String getAuthor();
    
    String getName();
    
    }

인터페이스 Book에 추상메소드 getAuthor과 getName을 추가하였다. 각각의 메소드는 이름 그대로 작가와 작품명을 가져오는 역할을 한다.


     public class LesMiserables implements Book {  
        @Override  
      public String getAuthor() {  
            return "Victor Hugo";  
      }  
        @Override  
      public String getName() {  
            return "Les Miserables";  
      }  
    }
레미제라블 클래스이다. 전에 말했듯이, implements를 통해서 인터페이스 Book을 선언하였고, 추상메소드 2개를 오버라이드하여 작가명은 빅토르 휴고, 작품명은 레미제라블을 리턴하는 모습이다.

같은 방법으로 다른 2개의 책들도 클래스를 만들어주면,

    public class LittlePrince implements Book   {  
        @Override  
      public String getAuthor() {  
            return "SaintExupery";  
      }  
        @Override  
      public String getName() {  
            return "LittlePrince";  
      }  
    }


    public class RomeoandJuliet implements Book{  
        @Override  
      public String getAuthor() {  
            return "Shakespeare";  
      }  
        @Override  
      public String getName() {  
            return "Romeo and Juliet";  
      }  
    }

이렇게 된다.

다음은 Main 메소드이다.

    public class Main {  
        public void findAuthor(Book book){  
            System.out.println("The Author of "+book.getName()+" is "+book.getAuthor());  
      }  
        public static void main(String[] args) {  
            Book book = new LesMiserables();  
      Main main = new Main();  
      main.findAuthor(book);  
      book = new LittlePrince();  
      main.findAuthor(book);  
      book = new RomeoandJuliet();  
      main.findAuthor(book);  
      }  
    }

메인 메소드에서 findAuthor메소드, 즉 작가를 찾는 메소드를 만들었다. 매개변수는, 객체를 통해서 받을 수 있고, 출력은 없는 메소드(void)임을 알 수 있다.

출력내용은, 인터페이스의 book의 getName, getAuthor 메소드를 통해 가져오는 작가명과 작품명이다.

메인 메소드를 보면, 레미제라블에서 생성된 book 객체를 만든것을 볼 수 있다.(다형성, 이것이 가능한 이유는 LesMiserables 클래스가 인터페이스 Book을 상속받았기 때문) main 객체를 만들어 위의 메소드를 사용해 작가명과 작품명을 출력한다. 다른 클래스들 또한 마찬가지로 출력을 하게되면,

    The Author of Les Miserables is Victor Hugo
    The Author of LittlePrince is SaintExupery
    The Author of Romeo and Juliet is Shakespeare

이러한 내용의 출력을 받을 수 있게된다. 

내용을 정리하자면, 인터페이스를 통해 코드를 단순화할 수 있고, 그것에 대한 예제로 도서관에서 책의 작가와 작품명을 불러오는 기능을 만들었다.

