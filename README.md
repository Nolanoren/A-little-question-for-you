    <p>What sounds food="Pizza" onclick="selectFood(this)"><span class="emoji">🍕</span><span class="label">Pizza</span></div>
      <div class="choice" data-food="Burgers" onclick="selectFood(this)"><span class="emoji">🍔</span><span class="label">Burgers</span></div>
      <div class="choice" data-food="Mexican" onclick="selectFood(this)"><span class="emoji">🌮</span><span class="label">Mexican</span></div>
      <div class="choice" data-food="Ice Cream" onclick="selectFood(this)"><span class="emoji">🍦</span><span class="label">Ice Cream</span></div>
      <div class="choice" data-food="Mini Golf" onclick="selectFood(this)"><span class="emoji">⛳</span><span class="label">Mini Golf</span></div>
      <div class="choice" data-food="Bowling" onclick="selectFood(this)"><span class="emoji">🎳</span><span class="label">Bowling</span></div>
      <div class="choice" data-food="Movie" onclick="selectFood(this)"><span class="emoji">🎬</span><span class="label">Movie</span></div>
      <div class="choice" data-food="Arcade" onclick="selectFood(this)"><span class="emoji">🕹️</span><span class="label">Arcade</span></div>
      <div class="choice" data-food="Pickleball" onclick="selectFood(this)"><span class="emoji">🏓</span><span class="label">Pickleball</span></div>
      <div class="choice" data-food="Italian" onclick="selectFood(this)"><span class="emoji">🍝</span><span class="label">Italian</span></div>
      <div class="choice" data-food="Something casual" onclick="selectFood(this)"><span class="emoji">🍿</span><span class="label">Something casual</span></div>
      <div class="choice" data-food="Other" onclick="selectOther()"><span class="emoji">✨</span><span class="label">Other</span></div>
    </div>
    <button class="primary" onclick="nextFromFood()">Next →</button>
    <div class="dots"><i class="dot on"></i><i class="dot"></i><i class="dot"></i></div>
  </section>

  <section class="screen" id="s3other">
    <div class="top"><button class="back" onclick="go(2)">← Back</button><span>3 / 5</span></div>
    <h2>Something else? 💕</h2>
    <p>Tell me what you'd like to do!</p>
    <div class="field" style="margin-top:35px">
      <label for="otherIdea">YOUR DATE IDEA</label>
      <textarea id="otherIdea" rows="5" placeholder="Type your idea here..."></textarea>
    </div>
    <button class="primary" onclick="saveOtherIdea()">Next →</button>
    <div class="dots"><i class="dot on"></i><i class="dot on"></i><i class="dot"></i></div>
  </section>

  <section class="screen" id="s3">
    <div class="top"><button class="back" onclick="backFromDate()">← Back</button><span>4 / 5</span></div>
    <h2>Pick a date & time.</h2>
    <p>Choose whatever works best for you.</p>
    <div class="field"><label for="date">DATE</label><input id="date" type="date"></div>
    <div class="field"><label for="time">TIME</label><input id="time" type="time"></div>
    <div class="field"><label for="note">ANYTHING ELSE? <span style="font-weight:400;color:#aaa">(optional)</span></label><textarea id="note" rows="3" placeholder="Maybe a place you want to go..."></textarea></div>
    <button class="primary" onclick="finish()">Looks good →</button>
    <div class="dots"><i class="dot on"></i><i class="dot on"></i><i class="dot"></i></div>
  </section>

  <section class="screen" id="s4">
    <div class="top"><span class="brand">it's a plan ✨</span><span>5 / 5</span></div>
    <div class="hero" style="justify-content:flex-start;padding-top:55px">
      <div class="thank" style="color:#ff4f82;text-shadow:0 10px 30px rgba(255,79,130,.22)">♥</div>
      <h1>Thank you!</h1>
      <p>I can't wait. Here's what we picked:</p>
      <div class="summary" style="width:100%;text-align:left">
        <div class="row"><span class="icon">💡</span><div><small>Date idea</small><strong id="sumFood">—</strong></div></div>
        <div class="row"><span class="icon">📅</span><div><small>Date</small><strong id="sumDate">—</strong></div></div>
        <div class="row"><span class="icon">🕐</span><div><small>Time</small><strong id="sumTime">—</strong></div></div>
      </div>
      <p id="sumNote" style="font-size:14px"></p>
      <div style="font-size:15px;font-weight:600;margin-top:4px">See you then :)</div>
    </div>
    <div class="dots"><i class="dot on"></i><i class="dot on"></i><i class="dot on"></i></div>
  </section>
</div>

<script>
let food = "";

function go(n){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById('s'+n).classList.add('active');
  window.scrollTo(0,0);
}
function noThanks(){
  document.querySelector('#s1 .hero').innerHTML = `
    <div class="smallheart" style="color:#ff4f82;text-shadow:0 8px 25px rgba(255,79,130,.2)">♥</div>
    <h1>No worries :)</h1>
    <p>Thanks for being honest. Have a great day!</p>
    <button class="no" style="width:100%;max-width:350px" onclick="location.reload()">Back</button>`;
}
function selectFood(el){
  document.querySelectorAll('.choice').forEach(c=>c.classList.remove('selected'));
  el.classList.add('selected'); food=el.dataset.food;
}
function nextFromFood(){
  if(!food){alert("Pick a date idea first 😊");return;}
  go(3);
}
function selectOther(){
  document.querySelectorAll('.choice').forEach(c=>c.classList.remove('selected'));
  food="Other";
  go('3other');
}
function saveOtherIdea(){
  const idea=document.getElementById('otherIdea').value.trim();
  if(!idea){alert("Type your date idea first 😊");return;}
  food=idea;
  go(3);
}
function backFromDate(){
  if(food && !["Pizza","Burgers","Mexican","Ice Cream","Mini Golf","Bowling","Movie","Arcade","Pickleball","Italian","Something casual"].includes(food)){
    go('3other');
  } else {
    go(2);
  }
}
function finish(){
  const date=document.getElementById('date').value;
  const time=document.getElementById('time').value;
  if(!date || !time){alert("Pick a date and time first 😊");return;}
  const d=new Date(date+"T00:00:00");
  document.getElementById('sumFood').textContent=food;
  document.getElementById('sumDate').textContent=d.toLocaleDateString(undefined,{weekday:'short',month:'long',day:'numeric',year:'numeric'});
  const [h,m]=time.split(':'); const t=new Date(); t.setHours(h,m);
  document.getElementById('sumTime').textContent=t.toLocaleTimeString(undefined,{hour:'numeric',minute:'2-digit'});
  const note=document.getElementById('note').value.trim();
  document.getElementById('sumNote').textContent=note ? "Note: "+note : "";
  go(4);
}
const today=new Date();
const iso=new Date(today.getTime()-today.getTimezoneOffset()*60000).toISOString().split('T')[0];
document.getElementById('date').min=iso;
</script>
</body>
</html>
