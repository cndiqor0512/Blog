---
layout: post
title:  "boardData 가져오기"
categories: springboot
--- 

``` java
컨트롤러:
@GetMapping("api/boardData/{boardId}")
    public Board getBoardData(@PathVariable Long boardId){ return boardService.getBoardData(boardId);}
``` 
boardId를 parameter로 받아서 getBoardData를 boardId로 입력하여 받아온다.

``` java
서비스:
public Board getBoardData(Long boardId) {
        return boardRepository.getBoardData(boardId);
    }
```
boardId를 파라미터로 받고 boardRepository에서 boardData를 리턴하는 메소드

``` java
리포지토리:
Board getBoardData(Long id);
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

board List 가져오기:

``` java
boardController:

@RestController
@RequiredArgsConstructor
public class BoardController {
    private final BoardService boardService;

    @GetMapping("/board")
    public List<Board> getList() {
        return boardService.getList();

    }
}
```
boardService의 getList메소드를 리턴한다.
``` java
boardService:
@Service
@RequiredArgsConstructor
public class BoardService {
    private final BoardRepository boardRepository;

    public List<Board> getList() {
        return boardRepository.getList();
    }
}
```
getList메소드: boardRepository에서의 List를 리턴한다.
``` java
boardRepository:
@Mapper
public interface BoardRepository {
    List<Board> getList(); //Board의 List
}
```
```java
board:
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
<select id="getList" resultType="com.example.springboot_practice.domain.Board">
        SELECT
            id,
            title,
            regdate,
            publisher,
            contents
        FROM board
    </select>
```
board테이블에서 조건 없이 모든 column의 id, title, regdate, publisher, contents의 데이터를 선택한다.