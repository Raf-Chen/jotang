先介绍css ！   

做完html的内容然后开始调整各个box的大小颜色字体大小颜色，虽然难度不大，但也搞了一段时间，因为要不断尝试颜色跟大小，而所以做的不快（也可能是因为我太菜了），但也刚好之前看的css的引用标签的方法复习了一遍，不像自我介绍里一样全是.classname(doge)。总之好在搞出来颜色大小搭配自己也算满意。







<!DOCTYPE html>

<html>



<head>

​    

    <meta charset="UTF-8">

​    

    <meta http-equiv="X-UA-Compatible" content="IE=edge">

​    

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

​    <title>My todolist</title>

        <style>

​    .center {

​      width: 1000px;

​      background-color: rgb(131, 166, 231);

​      font-size: 40px;

​      margin: 0 *auto*;

​    }



​    ul{

​      list-style: *none*;



​    }

​    li{

​      height: 50px;

​      border: 1px *solid* #ddd;



​    }



​    li:hover{

​      background-color: rgb(166, 238, 212);

​    }



​    .centertodobox {

​      width: 1000px;

​      background-color: rgb(171, 201, 190);

​      margin: 0 *auto*;

​    }



​    \#input {

​      width: 400px;



​      height: 30px;

​    }



​    .title {

​      font-weight: 900;

​    }



​    .check{

​      width: 20px;

​      height: 20px;

​    }



​    .delete {

​      float: *right*;

​      height: 40px;

​      width: 80px;

​      background-color: *blanchedalmond*;

​    }



​    .light {

​      margin-top: 100px;

​      margin-left: 1000px;

​      width: 140px;

​      height: 65px;

​    }







​    footer {

​      margin-left: 600px;

​    }

  </style>

​     





</head>





然后是html！

其实上面style前面那些应该归到这儿来说，还记得第一次看html的教程的时候看到！+tab然后变出很多东西的震撼。这没啥太多说的，根据要求先打几个box出来就成，然后也看了不少别的源代码，看到了别人布局的优势，然后改进了自己的布局，让css能操作且更方便。







body>

​    <header>

                <div class="center">

​            <span class="title">Todolist</span>

​            <input type="text" placeholder="快来规划自己的todo吧！" id="input">

​          </div>

​      </header>

    <div class="centertodobox">

​      <h2>进行中</h2>

​      <ul class="todo">

​          <li>

​              <input type="checkbox" class="check">

​              <span>todo的内容</span>

​              <button class="delete">删除</button>

​            </li>

​        </ul>



​      <h2>已完成</h2>

​      <ul class="done">

​          <li>

​              <input type="checkbox">

​              <span>done的内容</span>

​              <button class="delete">删除</button>

​            </li>

​        </ul>



​     <button class="light">黑夜模式</button>



  </div>



下面是js！！！！！！

这位更是重量级，属实是让我戴了一波痛苦面具，由于没基础，时间也不够（国庆节出去玩了）。学的内容跟熟练度都不太够，所以真的是问遍了能问的人，查了很多csdn，才能找到实现功能的方法，代码的功能实现之间也没啥联系，雀实是一个要求一个要求的解决，甚至单独创一个.html实现一个功能之后再加到源代码里，因为我的菜，有时候还会在实现下一个功能的过程中把不小心上一个功能废掉（无大语），所以又要返回去检查代码，标签名，classname啥的，开始自己检查不出来的时候是真的折磨。也有确实是因为自己了解不够的时候，所以这个时候也会让别人帮忙看看问题出在哪儿，然后再去修改。数组，render函数，append函数这些，我能够理解（当然可能也不是特别理解，大佬别骂了）并且使用之后，都让我觉得我很高端（bushi），总之，虽然看了很多源代码，csdn的帖子，问了别人很多问题，但是最后能够完成这一段代码，做出这些功能还是让我觉得有成就感。





总而言之，写这个代码真的花了很多很多心思跟时间，属于是呕心沥血了，真的很希望可以进焦糖。





script src="http://libs.baidu.com/jquery/2.1.4/jquery.min.js"></script>

    <script>  

​    var todolist = localStorage.getItem("todolist");

​    if (todolist) {

​      todolist = *JSON*.parse(todolist);

​      render();

​    } else {

​      todolist = [];

​    }



​    $("#input").on("change", function () {

​      todolist.push({

​        content: *this*.value,

​        done: false,

​        id: todolist.length,

​      })



​      console.log(todolist);

​      *this*.value = "";

​      render();

​    })



  function changeDone(x){

​    todolist[x].done=event.target.checked;

​    render();

  }





​    $(".centertodobox").on("click", ".delete", function () {

​      console.log(*this*.dataset.index)

​      todolist.splice(*this*.dataset.index, 1);

​      render();

​    })



​    





​    function render() {

​      $(".done").html("");

​      $(".todo").html("");



​      for (var i = 0; i < todolist.length; i++) {

​        if (todolist[i].done) {

​          $(".done").append(

​            ` <li>

​      <input type="checkbox" class="check"  checked onchange="changeDone(${i})">

​      <span>${todolist[i].content}</span>

​      <button data-index="${i}" class="delete">删除</button>

​    </li>`);

​        } else {

​          $(".todo").append(

​            ` <li>

​      <input type="checkbox" class="check" onchange="changeDone(${i})">

​      <span>${todolist[i].content}</span>

​      <button data-index="${i}" class="delete">删除</button>

​    </li>`);



​        }

​      }

​    }



​    window.onbeforeunload = function () {

​      localStorage.setItem("todolist", *JSON*.stringify(todolist));

​    }





​    var light = 1

​    $(".light").click(function () {

​      if (light == 1) {

​        light = 0

​        document.getElementsByClassName("light")[0].innerHTML = "白天模式"

​        $(".centertodobox").css("background-color", "rgb(62, 63, 62)")

​        $(".centertodobox").css("color", "white")

​        $("body").css("background-color", "black")

​        $(".delete").css("background-color", "rgb(82, 80, 77)")

​        $(".delete").css("color", "white")





​      } else {

​        light = 1

​        document.getElementsByClassName("light")[0].innerHTML = "黑夜模式"

​        $(".centertodobox").css("background-color", "rgb(171, 201, 190")

​        $(".centertodobox").css("color", "black")

​        $("body").css("background-color", "white")

​        $(".delete").css("background-color", "blanchedalmond")

​        $(".delete").css("color", "black")



​      }

​    })

​     







  </script>

​    

</body>



</html>