<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body style="margin: 0">
<canvas id="canvas">Upload Browser!</canvas>
<script>
  const canvas = document.getElementById('canvas');
  const ctx = canvas.getContext('2d');

  canvas.width = innerWidth;
  canvas.height = innerHeight;

  let bool = true;
  let mode;
  let dir;
  let dir2 = 0;
  let rpx = 100;
  let l = 10;
  let r = 2;
  let score = 0;
  let scoreBot = 0;
  let neironball;
  let neironballI;
  let touchPosition = null;
  let posY = canvas.height / 2.3;
  let posYBot = canvas.height / 2.3;
  let posYBotC = posYBot;
  //posYBotC -= (canvas.height/(l*2));
  let posYBotCI;
  let posYI;
  let end;
  let game;
  let rect1 = new Path2D();
  let rect2 = new Path2D();
  let rect3 = new Path2D();
  let arc = [];
    arc[0] = {
      x: canvas.width / 2,
      y: canvas.height / 2,
    };
  let rectN = [];
  let grad = ctx.createLinearGradient(0,0,innerWidth,innerHeight/2);
  grad.addColorStop('0','#b2ffe7');
  grad.addColorStop('1', '#00cbba')
  //game = setInterval(drawBackGround , 500);



   function ballMovement(event){
    if(event.keyCode == 13) {
      dir2 = 3;
    }
    }

    function ballMovement2(event) {
      if (dir2 == 0) {
        dir2 = 3;
        console.log(dir2);
      }
    }

  function stickMovement(event){
    ctx.fillStyle = '#00b7d7';
    ctx.fillRect(canvas.width - canvas.width/20, event.clientY, canvas.width/50, canvas.height/l);
    posY = event.clientY;
  }

  function touchStickMovement(event){
    //touchPosition = { x: event.changedTouches[0].clientX, y: event.changedTouches[0].clientY };
    ctx.fillStyle = '#00b7d7';
    ctx.fillRect(canvas.width - canvas.width/20, event.changedTouches[0].clientY, canvas.width/50, canvas.height/l);
    posY = event.changedTouches[0].clientY;
  }

  //end = setInterval(start_end , 3000);
  start_end();
  function start_end() {
    while (bool == true) {
      ctx.clearRect(0, 0, innerWidth, innerHeight);
      canvas.width = innerWidth;
      canvas.height = innerHeight;
      ctx.fillStyle = grad;
      ctx.fillRect(0, 0, innerWidth, innerHeight);
      ctx.fillStyle = '#fff17d';
      //ctx.font = '84px Comic Sans MS';
      ctx.font = '960% Trebuchet MS';
      ctx.fillText('< AIR HOCKEY >', canvas.width / 10, canvas.height / 7);
      ctx.fillStyle = '#ffffff';
      ctx.font = '640% Trebuchet MS';
      ctx.fillText('MENU', canvas.width / 2.5, canvas.height / 3);
      ctx.fillStyle = '#00b7d7';
      rect1.rect(canvas.width / 3.4, canvas.height / 2.5, canvas.width / 2.5, canvas.height / 10);
      ctx.fill(rect1);
      ctx.fillStyle = '#00b7d7';
      rect2.rect(canvas.width / 3.4, (canvas.height / 2.5) + (canvas.height / 7), canvas.width / 2.5, canvas.height / 10);
      ctx.fill(rect2);
      ctx.fillStyle = '#00b7d7';
      rect3.rect(canvas.width / 3.4, (canvas.height / 2.5) + ((canvas.height / 7) * 2), canvas.width / 2.5, canvas.height / 10);
      ctx.fill(rect3);
      ctx.fillStyle = '#ffffff';
      ctx.font = '400% Trebuchet MS';
      ctx.fillText('PLAYER/PLAYER', canvas.width / 3.15, canvas.height / 2.15);
      ctx.fillText('BOT/PLAYER', canvas.width / 2.8, canvas.height / 2.15 + (canvas.height / 7));
      ctx.fillText('BOT/BOT', canvas.width / 2.55, canvas.height / 2.15 + ((canvas.height / 7) * 2));
      canvas.addEventListener('mousedown', direction2);

      function direction2(event) {
        if (ctx.isPointInPath(rect1, event.offsetX, event.offsetY)) {
          mode = 1;
          ctx.clearRect(0, 0, innerWidth, innerHeight);
          bool = false;
          //clearInterval(end);
          //game = setInterval(drawBackGround, 500);
        }
        if (ctx.isPointInPath(rect2, event.offsetX, event.offsetY)) {
          mode = 2;
          ctx.clearRect(0, 0, innerWidth, innerHeight);
          bool = false;
          //clearInterval(end);
          //game = setInterval(drawBackGround, 500);
        }
        if (ctx.isPointInPath(rect3, event.offsetX, event.offsetY)) {
          mode = 3;
          ctx.clearRect(0, 0, innerWidth, innerHeight);
          bool = false;
          //clearInterval(end);
          //game = setInterval(drawBackGround, 500);
        }
        //if(r == 1) {
        //ctx.clearRect(0, 0, innerWidth, innerHeight);
        //clearInterval(end);
        //console.log(r);
        //location.reload();
        //}
      }

      //requestAnimationFrame(start_end);
    }
    drawBackGround();
  }

  //function draw(){
    //drawBackGround();
  //}
  function drawBackGround() {
    canvas.width = innerWidth;
    canvas.height = innerHeight;
    ctx.fillStyle = grad;
    //(canvas.height/(l*3))*1.6
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    if(mode == 2 || mode == 3 ) {
      console.log("mode: " + mode);
      for (let i = 0; i < (l * r); i++) {
        //ctx.fillStyle = '#ffffff';
        //ctx.font = '320% Trebuchet MS';
        rectN[i] = {
          //t: ctx.fillText(i, 0, (canvas.height / (l*1))*i),
          //n: ctx.fillStyle = '#133fff',
          //s: ctx.strokeRect(0, (canvas.height / (l*1))*i, canvas.width, (canvas.height / (l*1))*(i+1)),
          //n2: ctx.fillStyle = '#1fffff',
          r: ctx.fillRect(0, (canvas.height / (l * r)) * i, canvas.width, (canvas.height / (l * r)) * (i + 1)),
          k: 1
        }
      }
    }
    //if(mode == 2) {
      ctx.fillStyle = '#00b7d7';
      ctx.fillRect(canvas.width / 20, posYBotC - (canvas.height / (l * 2)), canvas.width / 50, canvas.height / l);
      ctx.fillStyle = '#00b7d7';
      ctx.fillRect(canvas.width - canvas.width / 20, posY, canvas.width / 50, canvas.height / l);
   // }
    for (let i = 0; i < arc.length; i++) {
      ctx.fillRect(arc[i].x, arc[i].y, canvas.width / 50, canvas.width / 50);
      ctx.fill();
    }

    if (score >= 7 || scoreBot >= 7) {
      clearInterval(drawBackGround);
      location.reload();
    }

      let ballX = arc[0].x;
      let ballY = arc[0].y;
      if(ballX > canvas.width){
       dir2 = 0;
       ballX = canvas.width / 2;
       ballY = canvas.height / 2;
       scoreBot++;
       //window.navigator.vibrate([5000, 1000, 5000]);
      }
      if(ballX < 0){
       dir2 = 0;
       ballX = canvas.width / 2;
       ballY = canvas.height / 2;
       score++;

      }
      //posYBotC = (canvas.height/(l*3))*1.6;
      if(mode == 2 || mode == 3) {
        console.log("mode: " + mode);
        for (let i = 0; i < (l * r); i++) {

          if (ballY >= (canvas.height / (l * r)) * i && ballY <= (canvas.height / (l * r)) * (i + 1)) {
            rectN[i].k = 0;
            neironball = rectN[i].k;
            neironballI = i;
          }
          if (posYBotC >= (canvas.height / (l * r)) * i && posYBotC < (canvas.height / (l * r)) * (i + 1)) {
            posYBotCI = i;
          }
        }
        console.log(posYBotCI + ' posYBotCI');
        console.log(neironballI + ' neironballI');
        if (posYBotCI == neironballI) {
          //console.log(posYBotCI + ' posYBotCI');
          //console.log(neironballI + ' neironballI');
        } else if (posYBotCI > neironballI) {
          posYBotC -= canvas.height / (rpx * 0.5);
          console.log(posYBotC + ' posYBotC');
          console.log(posYBotCI + ' 126');
          //console.log(neironballI + ' neironballI');
        } else if (posYBotCI < neironballI) {
          posYBotC += canvas.width / (rpx * 0.5);
          console.log(posYBotC + ' posYBotC');
          console.log(posYBotCI + '130');
          //console.log(neironballI + ' neironballI');
        }
        if(mode == 3){
          console.log("mode: " + mode);
        for (let i = 0; i < (l * r); i++) {

          if (ballY >= (canvas.height / (l * r)) * i && ballY <= (canvas.height / (l * r)) * (i + 1)) {
            rectN[i].k = 0;
            neironball = rectN[i].k;
            neironballI = i;
          }
          if (posY >= (canvas.height / (l * r)) * i && posY < (canvas.height / (l * r)) * (i + 1)) {
            posYI = i;
          }
        }
        console.log(posYBotCI + ' posYBotCI');
        console.log(neironballI + ' neironballI');
        if (posYBotCI == neironballI) {
          //console.log(posYBotCI + ' posYBotCI');
          //console.log(neironballI + ' neironballI');
        } else if (posYI > neironballI) {
          posY -= canvas.height / (rpx * 0.5);
          console.log(posY + ' posYBotC');
          console.log(posYI + ' 126');
          //console.log(neironballI + ' neironballI');
        } else if (posYBotCI < neironballI) {
          posY += canvas.width / (rpx * 0.5);
          console.log(posY + ' posYBotC');
          console.log(posYI + '130');
          //console.log(neironballI + ' neironballI');
        }
        }
      }

      //posYBotC = (canvas.height/(l*3))*1.6;
      //ballY -
      ctx.fillStyle = '#ffffff';
      ctx.font = '320% Trebuchet MS';
      ctx.fillText(scoreBot + ' : ' + score, canvas.width / 2.1, canvas.height / 13 );
      if (score >= 7) {
        ctx.fillStyle = '#ffffff';
      ctx.font = '320% Trebuchet MS';
      ctx.fillText('You win!!!', canvas.width / 2.4, canvas.height / 5 );
      }
      if (scoreBot >= 7) {
        ctx.fillStyle = '#ffffff';
      ctx.font = '320% Trebuchet MS';
      ctx.fillText('Game Over!!!', canvas.width / 2.5, canvas.height / 5 );
      }

      if(ballY <= 0 && dir2 == 5){
       dir2 = 6;
       //window.navigator.vibrate([500, 100, 500]);
      }
      if(ballY <= 0 && dir2 == 1){
       dir2 = 2;
       //window.navigator.vibrate([500, 100, 500]);
      }
      if(ballY >= canvas.height && dir2 == 6){
       dir2 = 5;
       //window.navigator.vibrate([500, 100, 500]);
      }
      if(ballY >= canvas.height && dir2 == 2){
       dir2 = 1;
       //window.navigator.vibrate([500, 100, 500]);
      }
      if(mode == 1) {
        console.log("mode: " + mode);
        if (ballX >= canvas.width - canvas.width / 20 - canvas.width / 50 && ballX <= canvas.width && ballY + canvas.width / 50 >= posY && ballY <= posY + canvas.height / (l * 3)) {
          dir2 = 5;
        }
        if (ballX >= canvas.width - canvas.width / 20 - canvas.width / 50 && ballX <= canvas.width && ballY + canvas.width / 50 >= posY + canvas.height / (l * 3) && ballY <= posY + (canvas.height / (l * 3)) * 2) {
          dir2 = 4;
        }
        if (ballX >= canvas.width - canvas.width / 20 - canvas.width / 50 && ballX <= canvas.width && ballY + canvas.width / 50 >= posY + (canvas.height / (l * 3)) * 2 && ballY <= posY + (canvas.height / (l * 3)) * 3) {
          dir2 = 6;
        }
        if (ballX <= canvas.width / 20 + canvas.width / 50 && ballX >= 0 && ballY + canvas.width / 50 >= posYBotC && ballY <= posYBotC + (canvas.height / (l * 3))) {
          dir2 = 1;
        }
        if (ballX <= canvas.width / 20 + canvas.width / 50 && ballX >= 0 && ballY + canvas.width / 50 >= posYBotC + (canvas.height / (l * 3)) && ballY <= posYBotC + (canvas.height / (l * 3)) * 2) {
          dir2 = 3;
        }
        if (ballX >= canvas.width - canvas.width / 20 - canvas.width / 50 && ballX <= canvas.width && ballY + canvas.width / 50 >= posYBotC + (canvas.height / (l * 3) * 2) && ballY <= posYBotC + (canvas.height / (l * 3)) * 3) {
          dir2 = 2;
        }
      }
      if(mode == 2) {
        console.log("mode: " + mode);
        if (ballX >= canvas.width - canvas.width / 20 - canvas.width / 50 && ballX <= canvas.width && ballY + canvas.width / 50 >= posY && ballY <= posY + canvas.height / (l * 3)) {
          dir2 = 5;
          console.log(dir2);
        }
        if (ballX >= canvas.width - canvas.width / 20 - canvas.width / 50 && ballX <= canvas.width && ballY + canvas.width / 50 >= posY + canvas.height / (l * 3) && ballY <= posY + (canvas.height / (l * 3)) * 2) {
          dir2 = 4;
          console.log(dir2);
        }
        if (ballX >= canvas.width - canvas.width / 20 - canvas.width / 50 && ballX <= canvas.width && ballY + canvas.width / 50 >= posY + (canvas.height / (l * 3)) * 2 && ballY <= posY + (canvas.height / (l * 3)) * 3) {
          dir2 = 6;
          console.log(dir2);
        }
        if (ballX <= canvas.width / 20 + canvas.width / 50) {
          if (ballX >= 0) {
            if (ballY + canvas.width / 50 >= posYBotC - (canvas.height / (l * 2))) {
              if (ballY <= posYBotC + (canvas.height / l)) {
                dir2 = Math.floor(Math.random() * 3 + 1);
              }
            }
          }
        }
      }
      if(mode == 3) {
        console.log("mode: " + mode);
        if (ballX >= canvas.width - canvas.width / 20 - canvas.width / 50 && ballX <= canvas.width && ballY + canvas.width / 50 >= posY && ballY <= posY + canvas.height / (l * 3)) {
          dir2 = 5;
        }
        if (ballX >= canvas.width - canvas.width / 20 - canvas.width / 50 && ballX <= canvas.width && ballY + canvas.width / 50 >= posY + canvas.height / (l * 3) && ballY <= posY + (canvas.height / (l * 3)) * 2) {
          dir2 = 4;
        }
        if (ballX >= canvas.width - canvas.width / 20 - canvas.width / 50 && ballX <= canvas.width && ballY + canvas.width / 50 >= posY + (canvas.height / (l * 3)) * 2 && ballY <= posY + (canvas.height / (l * 3)) * 3) {
          dir2 = 6;
        }
        if (ballX <= canvas.width / 20 + canvas.width / 50) {
          if (ballX >= 0) {
            if (ballY + canvas.width / 50 >= posYBotC - (canvas.height / (l * 2))) {
              if (ballY <= posYBotC + (canvas.height / l)) {
                dir2 = Math.floor(Math.random() * 3 + 1);
              }
            }
          }
        }
      }

      //posYBotC = ballY - (canvas.height/(l*3))*1.6;

     arc.pop();
     if(dir2 == 5){
       console.log(dir2);
       ballX -= canvas.width/rpx;
       ballY -= canvas.height/rpx;
     }
     if(dir2 == 6){
       console.log(dir2);
       ballX -= canvas.width/rpx;
       ballY += canvas.height/rpx;
     }
     if(dir2 == 4){
       console.log(dir2);
       ballX -= canvas.width/rpx;
     }
     if(dir2 == 1 ){
       console.log(dir2);
       ballX += canvas.width/rpx;
       ballY -= canvas.height/rpx;
     }
     if(dir2 == 2 ){
       console.log(dir2);
       ballX += canvas.width/rpx;
       ballY += canvas.height/rpx;
     }
     if(dir2 == 3 ){
       console.log(dir2);
       ballX += canvas.width/rpx;
     }
     let newball = {
        x: ballX,
        y: ballY,
      }
      arc.unshift(newball);
    document.addEventListener('keydown', ballMovement);
    document.addEventListener('mousedown', ballMovement2);
    canvas.addEventListener('mousemove', stickMovement);
    canvas.addEventListener('touchmove', touchStickMovement);
    window.addEventListener("gamepadconnected", function(e) {
  console.log("Gamepad connected at index %d: %s. %d buttons, %d axes.",
  e.gamepad.index, e.gamepad.id,
  e.gamepad.buttons.length, e.gamepad.axes.length);
  console.log('');
  console.log(e);
});
    window.addEventListener("gamepaddisconnected", function(e) {
  console.log("Gamepad disconnected from index %d: %s",
  e.gamepad.index, e.gamepad.id);
});
    requestAnimationFrame(drawBackGround);
  }
  //drawBackGround();
</script>
</body>
</html>
