<html>
<head>
<style type="text/css">

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  
    font: bold 14px Arial, sans-serif;
}

html {
    height: 100%;
    background: white;
    background: radial-gradient(circle, #E6E6FA 20%, #ccc);
    background-size: cover;
}

#calculator {
    width: 325px;
    height: auto;
  
    margin: 10px auto;
    padding: 20px 20px 9px;
  
    background: #008000;
    background: linear-gradient(#008000, #ADFF2F);
    border-radius: 3px;
    box-shadow: 0px 4px #808080, 0px 10px 15px rgba(0, 0, 0, 0.2);
}

.top span.clear {
    float: left;
}

.top .screen {
    height: 40px;
    width: 212px;  
    float: right;  
    padding: 0 10px;  
    background: rgba(0, 0, 0, 0.2);
    border-radius: 3px;
    box-shadow: inset 0px 4px rgba(0, 0, 0, 0.2);
    font-size: 17px;
    line-height: 40px;
    color: white;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
    text-align: right;
    letter-spacing: 1px;
}

.keys, .top {overflow: hidden;}
.keys span, .top span.clear {
    float: left;
    position: relative;
    top: 0;
  
    cursor: pointer;
  
    width: 66px;
    height: 36px;
  
    background: Lightseagreen;
    border-radius: 3px;
    box-shadow: 0px 4px rgba(0, 0, 0, 0.2);
  
    margin: 0 7px 11px 0;
  
    color: #888;
    line-height: 36px;
    text-align: center;
  
    user-select: none;
    transition: all 0.2s ease;
}
.keys span.operator {
    background: #87CEEB;
    margin-right: 0;
}

.keys span.eval {
    background: #00FF7F;
    box-shadow: 0px 4px #9da853;

    color: #888e5f;
}

.top span.clear {
    background: #40E0D0;
    box-shadow: 0px 4px #708090;
    color: white;
}

/* Some hover effects */
.keys span:hover {
    background: #9c89f6;
    box-shadow: 0px 4px #6b54d3;
    color: white;
}

.keys span.eval:hover {
    background: #abb850;
    box-shadow: 0px 4px #717a33;
    color: #ffffff;
}

.top span.clear:hover {
    background: #f68991;
    box-shadow: 0px 4px #d3545d;
    color: white;
}

.keys span:active {
    box-shadow: 0px 0px #6b54d3;
    top: 4px;
}

.keys span.eval:active {
    box-shadow: 0px 0px #717a33;
    top: 4px;
}

.top span.clear:active {
    top: 4px;
    box-shadow: 0px 0px #d3545d;
}
</style>
</head>
<body>
<p><center>Calculator : Moch Fajar Hikmatulloh</center></p>
<div id="calculator">
    <!-- Screen and clear key -->
    <div class="top">
        <span class="clear">C</span>
        <div class="screen"></div>
    </div>
  
    <div class="keys">
        <!-- operators and other keys -->
        <span>7</span>
        <span>8</span>
        <span>9</span>
        <span class="operator">+</span>
        <span>4</span>
        <span>5</span>
        <span>6</span>
        <span class="operator">-</span>
        <span>1</span>
        <span>2</span>
        <span>3</span>
        <span class="operator">÷</span>
        <span>0</span>
        <span>.</span>
        <span class="eval">=</span>
        <span class="operator">x</span>
    </div>
</div>

<!-- PrefixFree -->
<script type="text/javascript">
var keys = document.querySelectorAll('#calculator span');
var operators = ['+', '-', 'x', '÷'];
var decimalAdded = false;

for(var i = 0; i < keys.length; i++) {
    keys[i].onclick = function(e) {
        var input = document.querySelector('.screen');
        var inputVal = input.innerHTML;
        var btnVal = this.innerHTML;
      
        if(btnVal == 'C') {
            input.innerHTML = '';
            decimalAdded = false;
        }
      
        else if(btnVal == '=') {
            var equation = inputVal;
            var lastChar = equation[equation.length - 1];
            equation = equation.replace(/x/g, '*').replace(/÷/g, '/');
            if(operators.indexOf(lastChar) > -1 || lastChar == '.')
                equation = equation.replace(/.$/, '');
          
            if(equation)
                input.innerHTML = eval(equation);
              
            decimalAdded = false;
        }
      
        else if(operators.indexOf(btnVal) > -1) {
            var lastChar = inputVal[inputVal.length - 1];
            if(inputVal != '' && operators.indexOf(lastChar) == -1)
                input.innerHTML += btnVal;          
            else if(inputVal == '' && btnVal == '-')
                input.innerHTML += btnVal;
            if(operators.indexOf(lastChar) > -1 && inputVal.length > 1) {
                input.innerHTML = inputVal.replace(/.$/, btnVal);
            }          
            decimalAdded =false;
        }      
        else if(btnVal == '.') {
            if(!decimalAdded) {
                input.innerHTML += btnVal;
                decimalAdded = true;
            }
        }
        else {
            input.innerHTML += btnVal;
        }
        e.preventDefault();
    }
}
</script>
</body>
</html>
