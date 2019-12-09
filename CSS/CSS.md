## CSS

참고 : https://caniuse.com/
### CSS 
* style tag
    ```html
    <style> 
        a{ // selector
            color: black;  // Property : Value; 
        }
    </style>
    ```
* inline 속성 
    ```html
    <h1 style="colr:red"> Hello World </h1>

### class, id
tag, class, id 중에서 id를 가장 우선한다. 

* class
    ```html
    <style>
        .class_name{
            color: black;
        }
    </style>
    <body>
        <div class="class_name"></div>
    </body>
    ```
    - 축약
    ``` html
        .class_a, .class_b {

        } 
    ```
* id 
    ```html
    <style>
        #id_name{
            color: black;
        }
    </style>
    <body id="id_name">
    </body>
    ```

### box model
* block level element

* inline elment 

    `display:inline`  
    `display:block` 와 같은 방식으로 기본 display 속성 바꿀 수 있다.
 

### padding, margin
 margin   
 border   
 padding   
 content 


 ### 단위  
* rem
    * em
    ```html
    <style>
        body{
            font-size: 10px;
        },
        div{
            font-size: 1.4em;
        }
    </style>
    <body>
        <div class="test"> Hello  <!-- 10 * 1.4 px -->
        <div class="test"> Hello </div>    
        </div> <!-- 10 * 1.4 * 1.4 px -->
        
    </body>
    ```
    `em ` 의 단위를 사용히게 되면 부모의 폰트 사이즈를 계속 상속을 받아서 하위로 내려갈수록 단위가 커지게 된다. 
    
    - rem 
    ```html
    <style>
        html{
            font-size: 10px;
        },
        div{
            font-size: 1.4rem; /* rem */
        }
    </style>
    <body>
        <div class="test"> Hello  <!-- 10 * 1.4 px -->
        <div class="test"> Hello </div>    
        </div> <!-- 10 * 1.4 px -->
        
    </body>
    ```
    rem을 사용하게 되면 root 속성(일반적으로 html)을 기준으로 하여 단위가 정해진다.

