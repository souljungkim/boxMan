# Event
`OBJ`가 `이동함에 따라 Event`를 발생시킬 수 있습니다. 

#### ※ 표
 종류 | Template속성 | Event Data | 설명
------|--------------|------------|-------
start | data-event-start | {box, obj, boxSize} | box가 생성될때
boxin | data-event-boxin | {boxel, obj, copyObj, boxSize, boxBefore, data} | OBJ가 해당 BOX로 들어올때
boxout | data-event-boxout | {boxel, obj, copyObj, boxSize, boxBefore, data} | OBJ가 해당 BOX에서 나갈때
boxinout | data-event-boxinout | {boxel, obj, copyObj, boxSize, boxBefore, data} | OBJ가 해당 BOX로 들어오거나 나갈때 
beforeboxin | data-event-beforeboxin | {box, obj, boxSize} | OBJ가 해당 BOX로 들어오기 전에
mustdo | data-event-mustdo | null | 무조건 발생.
external | data-event-external | Event | Browser 외부로부터 파일을 끌고 왔을때
afterdetect | data-event-afterdetect | null | 탐지(detect)를 마친 후
swappedin | data-event-swappedin | {boxel, obj, boxBefore} | swap이 발생할때
swappedout | data-event-swappedout | {boxel, obj, boxBefore} | swap이 발생할때

#### ※ 자동적용
- 편의를 위해서 예제에서는 다음 코드가 생략되어 있습니다.
    ```html
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@sj-js/boxman/dist/css/boxman.min.css">
    <script src="https://cdn.jsdelivr.net/npm/@sj-js/crossman/dist/js/crossman.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@sj-js/boxman/dist/js/boxman.min.js"></script>
    <script>
        var boxman = new BoxMan().setTheme('test-1');
    </script>
    ```
    
    *@* *+prefix* *x* *@* 
    ```html
    <link rel="stylesheet" href="../boxman/boxman.css">
    <script src="../crossman/crossman.js"></script>
    <script src="../boxman/boxman.js"></script>
    <script> 
        var boxman = new BoxMan().setTheme('test-1');
    </script>
    ```



## start
- BOX가 생성될 때 발생합니다.
    *@* *!* *@*
    ```html
    <script>
        boxman.detect(function(boxman){
            boxman.newBox({id:'boxA', content:'BOX A'});
            boxman.newBox({id:'boxB', content:'BOX B', start:function(){            
                document.getElementById('tester').innerHTML = 'Do start event!';
            }});
            boxman.newObj({id:'objA', content:'OBJ A'});
        });     
    </script>
    <body> 
        <div id="tester">TEST</div>    
    </body>
    ```
  
    *@* *!* *@*
    ```html
    <script>
        boxman.detect();     
    </script>
    <body>
        <div id="tester">TEST</div>
        <div id="boxA" data-box>BOX A</div>
        <div id="boxB" data-box data-event-start="document.getElementById('tester').innerHTML = 'Do start event!';" >BOX B</div>
        <div data-obj>OBJ A</div>    
    </body>
    ```


 
## boxin
- OBJ가 해당 BOX에 들어올 때
    *@* *!* *@*
    ```html
    <script>
        boxman.detect();     
    </script>
    <body>
        <div id="tester">TEST</div>
        <div id="boxA" data-box data-event-boxin="document.getElementById('tester').innerHTML+='boxin '" >Box A</div>
        <div id="boxB" data-box>Box B</div>
        <div data-obj>Obj A</div>
    </body>
    ```
  
  
  
## boxout
- OBJ가 해당 BOX에서 나갈 때
    *@* *!* *@*
    ```html
    <script>
        boxman.detect();     
    </script>
    <body>
        <div id="tester">TEST</div>
        <div id="boxA" data-box data-event-boxout="document.getElementById('tester').innerHTML+='boxout '" >Box A</div>
        <div id="boxB" data-box>Box B</div>
        <div data-obj>Obj A</div>
    </body>
    ```
    
    

## boxinout
- OBJ가 해당 BOX로 들어오거나 나갈때
    *@* *!* *@*
    ```html
    <script>
        boxman.detect();     
    </script>
    <body>
        <div id="tester">TEST</div>
        <div id="boxA" data-box data-event-boxinout="document.getElementById('tester').innerHTML+='boxinout '" >Box A</div>
        <div id="boxB" data-box>Box B</div>
        <div data-obj>Obj A</div>
    </body>
    ```   
  
  
  
## beforeboxin
- OBJ가 해당 BOX에 들어오기 전에
    *@* *!* *@*
    ```html
    <script>
        boxman.detect();     
    </script>
    <body>
        <div id="tester">TEST</div>
        <div id="boxA" data-box data-event-beforeboxin="document.getElementById('tester').innerHTML+='(A) '; return false;">Box A</div>
        <div id="boxB" data-box data-event-beforeboxin="document.getElementById('tester').innerHTML+='(B) '; return true;">Box B</div>
        <div data-box>
            Box C
            <div data-obj>Obj A</div>
        </div>
        
    </body>
    ```
  
  
  
## mustdo
- 무조건
    *@* *!* *@*
    ```html
    <script>
        boxman.detect();     
    </script>
    <body>
        <div id="tester">TEST</div>
        <div id="boxA" data-box data-event-mustdo="document.getElementById('tester').innerHTML+='(A)'">Box A</div>
        <div id="boxB" data-box data-event-mustdo="document.getElementById('tester').innerHTML+='(B)'">Box B</div>
        <div data-obj>Obj A</div>
    </body>
    ```
  
  
  
## external
- Browser 외부로부터 파일을 끌고 왔을때
    *@* *!* *@*
    ```html
    <script>
        boxman.detect();     
    </script>
    <body>
        <div id="tester">TEST</div>
        <div data-box data-event-external="document.getElementById('tester').innerHTML+='(external)'" >Box A</div>
        <div data-box>Box B</div>
        <div data-obj>Obj A</div>
    </body>
    ```
    
    
    
## afterdetect
- 탐지(detect)를 마친 후
    *@* *!* *@*
    ```html
    <script>      
        boxman.detect();
        boxman.afterDetect(function(){
            document.getElementById('tester').innerHTML = '__APPLE';          
        });  
    </script>
    <body>
        <div id="tester">TEST</div>
        <div id="boxA" data-box data-event-mustdo="tester.innerHTML+='♡'" >Box A</div>
        <div id="boxB" data-box>Box B</div>
        <div data-obj>Obj A</div>
    </body>
    ```
    
    
## swappedin
- Swap되어 들어왔을 때
    *@* *!* *@*
    ```html
    <script>      
        boxman.setup({appendType: BoxMan.APPEND_TYPE_SWAP}).detect();
    </script>
    <body>
        <div id="tester">TEST</div>
        <div id="boxA" data-box data-event-swappedin="tester.innerHTML+='♡'" >
            Box A
            <div data-obj>Obj A</div>
            <div data-obj>Obj B</div>
            <div data-obj>Obj C</div>
        </div>
        <div id="boxB" data-box>
            Box B
            <div data-obj>Obj D</div>
            <div data-obj>Obj E</div>
        </div>        
    </body>
    ```


## swappedout
- Swap되어 나갔을 때
    *@* *!* *@*
    ```html
    <script>      
        boxman.setup({appendType: BoxMan.APPEND_TYPE_SWAP}).detect();
    </script>
    <body>
        <div id="tester">TEST</div>
        <div id="boxA" data-box data-event-swappedout="tester.innerHTML+='♥'" >
            Box A
            <div data-obj>Obj A</div>
            <div data-obj>Obj B</div>
            <div data-obj>Obj C</div>
        </div>
        <div id="boxB" data-box>
            Box B
            <div data-obj>Obj D</div>
            <div data-obj>Obj E</div>
        </div>
    </body>
    ```
