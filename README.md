∥bloxd.io world code
var ticksElapsed=0;
var mod = 10000 //Define Variables.
var time = 0;

function onPlayerJoin(playerId){
	n = api.getEntityName(playerId);
	if(n=="hermionegranger59") {api.kickPlayer(playerId,"I'm Sorry, I Hate Taking Blame For Things I Didn't Do"); }
}

const DAY_NIGHT_CYCLE_MS = mod * 1000;
const Start = Date.now();
const SKYBOX_DAY = { type: "earth", inclination: 0, turbidity: 5, luminance: 1.0 };
const SKYBOX_NIGHT = { type: "earth", inclination: 180, turbidity: 15, luminance: 0.1 };
function tick(dt){
	time = (time+1)%mod;
	if(time % 100 == 0){api.log(time); }
    const elapsed = Date.now() - Start, cycleProgress = (elapsed % DAY_NIGHT_CYCLE_MS) / DAY_NIGHT_CYCLE_MS;
    if (cycleProgress < 0.5) { setDynamicSkybox(cycleProgress * 2); } else { setDynamicSkybox(1 - (cycleProgress - 0.5) * 2); }
};
function setDynamicSkybox(darkness) {
    const currentSkybox = { type: "earth", inclination: lerp(0, 180, darkness), turbidity: lerp(5, 15, darkness), luminance: lerp(1.0, 0.1, darkness) };
    for (const playerId of api.getPlayerIds()) { api.setClientOption(playerId, "skyBox", currentSkybox); }
}
function lerp(start, end, t) { return start + (end - start) * t; }

function cd(pid,time,ab){
	let now=Date.now();
	let remaining=now-time;
	if(remaining<=0){
		cooldowns[ability][pId]=now;
		return true;
	}  
	let secondsLeft=Math.ceil(remaining/1000);
	api.sendMessage(pId,`${ab} is on cooldown! ${secondsLeft}s remaining.`);			return false;
}

function fire(pId,rmb){
	it=api.getHeldItem(pId)
	if(it=="Red PaintBall"&&rmb==true){
		api.giveItem(pId,"Fireball",1)
		api.removeItemName(pId,"Red PaintBall",1)
	}
}

