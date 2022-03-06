---
layout: post
title:  "boardData 가져오기"
categories: springboot
--- 

``` java
컨트롤러:
@GetMapping("api/boardData/{boardId}")
    public List<Board> getBoardData(@PathVariable Long boardId){ return boardService.getBoardData(boardId);}
``` 
boardId를 parameter로 받아서 getBoardData를 boardId로 입력하여 받아온다.

``` java
서비스:
public List<Board> getBoardData(Long boardId) {
        return boardRepository.getBoardData(boardId);
    }
```
boardId를 파라미터로 받고 boardRepository에서 boardData를 리턴하는 메소드

``` java
리포지토리:
List<Board> getBoardData(Long id);
```
Board(도메인, 테이블과 1대1 맵핑)을 가져온다.

```java
Board:
@Data
public class Board {
    private Long id;
    private String title;
    private Long publisher;
    private String contents;
    @JsonFormat(pattern="yyyy-MM-dd")
    private LocalDate regDate;
}
```
board의 데이터 구조
``` html
board.xml:
<select id="getBoardData" resultType="com.example.springboot_practice.domain.Board">
        SELECT
            id,
            title,
            regdate,
            publisher,
            contents
        FROM board where id = #{boardId}
    </select>
```
boardId를 파라미터로 id가 boardId인 board 컬럼의 데이터만을 가져온다.