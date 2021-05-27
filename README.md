# my-own-game
//create the ball, playerPaddle and computerPaddle as sprite objects
var ball1 = createSprite(75,200,10,10);
ball1.setAnimation("ball");
var ball2 = createSprite(350,200,10,10);
ball2.setAnimation("ball");

var playerPaddle = createSprite(370,200,10,70);
playerPaddle.setAnimation("player");

var computerPaddle = createSprite(30,200,10,70);
computerPaddle.setAnimation("robot");

//variable to store different state of game
var gameState = "serve";

//variables to keep the score
var compScore = 0;
var playerScore = 0;


function draw() {
  //clear the screen
  background("white");
  
  if(ball1.isTouching(computerPaddle) || ball1.isTouching(playerPaddle)) {
   playSound("hit.mp3");
  }
if (keyWentDown("k")) {
playerPaddle.setAnimation("player_kick");
      
 }
if (keyWentUp("k")) {
playerPaddle.setAnimation("player");
        
  }
    
  
  
  //place info text in the center
  if (gameState === "serve") {
    text("Press Space to Serve",150,180);
  }
   
  //display scores
  text(compScore, 170,20);
  text(playerScore, 230,20);
  if (keyDown("UP_ARROW")) {
    playerPaddle.y=playerPaddle.y-5
  }
  if (keyDown("DOWN_ARROW")) {
    playerPaddle.y=playerPaddle.y+5
  }
  if (keyDown("w")) {
    computerPaddle.y=computerPaddle.y-5
  }
  if (keyDown("s")) {
    computerPaddle.y=computerPaddle.y+5
  }
  //make the player paddle move with the mouse's y position
  
  //AI for the computer paddle
  //make it move with the ball's y position
 
  
  //draw line at the centre
  for (var i = 0; i < 400; i=i+20) {
    line(200,i,200,i+10);
  }
  
  
  //create edge boundaries
  //make the ball bounce with the top and the bottom edges
  createEdgeSprites();
   if(ball1.isTouching(topEdge)||ball1.isTouching(bottomEdge)) {
   playSound("wall_hit.mp3", false);
        
  }
  
  ball1.bounceOff(topEdge);
  ball1.bounceOff(bottomEdge);
  ball1.bounceOff(playerPaddle);
  ball1.bounceOff(computerPaddle);
  ball2.bounceOff(topEdge);
  ball2.bounceOff(bottomEdge);
  ball2.bounceOff(playerPaddle);
  ball2.bounceOff(computerPaddle);
  
  playerPaddle.bounceOff(topEdge);
  playerPaddle.bounceOff(bottomEdge);
  computerPaddle.bounceOff(topEdge);
  computerPaddle.bounceOff(bottomEdge);
  
  
  //serve the ball when space is pressed
  if (keyDown("space") &&  gameState === "serve") {
    serve2();
    serve1();
     playerPaddle.setAnimation("player");
    gameState = "play";
  }
  
 
  //reset the ball to the centre if it crosses the screen
  if(ball1.x > 400 || ball1.x <0||ball2.x > 400 || ball2.x<0 ) {
  playSound("score.mp3", false);
      
    if(ball1.x > 400||ball2.x>400) {
      compScore = compScore + 1;
     
    }
    
    if(ball1.x < 0||ball2.x < 0) {
      playerScore = playerScore + 1;
    }
    
    reset1();
    reset2();
   
    gameState = "serve";
  }
  
  
 
  if (keyDown("r") && gameState === "over") {
    gameState = "serve";
    compScore = 0;
    playerScore = 0;
  }
  
  drawSprites();
}

function serve1() {
  ball1.velocityX = 6;
  ball1.velocityY = 6;
}

function reset1() {
  ball1.x = 75;
  ball1.y = 200;
  ball1.velocityX = 0;
  ball1.velocityY = 0;
  
}
function serve2() {
  ball2.velocityX = -6;
  ball2.velocityY = 6;
}

function reset2() {
  ball2.x = 350;
  ball2.y = 200;
  ball2.velocityX = 0;
  ball2.velocityY = 0;
  
}
