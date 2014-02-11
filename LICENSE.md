char.stop();

//variables...
var wspeed:Number=0; // The speed our character will move
var vy:Number=0; // Y axis speed
var gv:Number=1; // Gravity
var jumped:Boolean=false; // jump variable, false means not jumping

// Event Listeners...
stage.addEventListener (KeyboardEvent.KEY_DOWN,keydown); // this one listens when a key is pressed
stage.addEventListener (KeyboardEvent.KEY_UP,keyup); // this one listens when we let of go a key
stage.addEventListener (Event.ENTER_FRAME,gameloop); // this fires every frame

function keydown(e:KeyboardEvent) {
	if (e.keyCode==Keyboard.LEFT)  {
		wspeed=-10;
		char.gotoAndStop(2);
	}
	if (e.keyCode==Keyboard.RIGHT)  {
	    wspeed=10;
		char.gotoAndStop(1);
	}
	if (e.keyCode==Keyboard.SPACE) {
		if (!jumped) {
			vy=-14;
			jumped=true;
			
		}
	}	
}

function keyup(e:KeyboardEvent) {
	if (e.keyCode==Keyboard.LEFT) {
		wspeed=-0;
	}
	if (e.keyCode==Keyboard.RIGHT) {
		wspeed=0;
	}
}

function gameloop(e:Event) {
	
	char.x+=wspeed;
	
	
	if (char.x<0) {
		char.x=0;
	}
	if (char.x>550) {
		char.x=550;
	}
	
	vy+=gv;
	if (!platforms.hitTestPoint(char.x,char.y,true)) {
		char.y+=vy;
	}
	if (!platforms2.hitTestPoint(char.x,char.y,true)) {
		char.y+=vy;
	}
	
	for (var i=0;i<10;i++) {
		if (platforms.hitTestPoint(char.x,char.y,true)) {
			char.y--;
			vy=0;
			jumped=false;
		}
		for (var a=0;i<10;i++) {
		if (platforms2.hitTestPoint(char.x,char.y,true)) {
			char.y--;
			vy=0;
			jumped=false;
		}
	}
	
}
}


