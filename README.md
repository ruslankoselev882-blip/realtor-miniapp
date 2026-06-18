<!doctype html>
<html lang="ru">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<title>КвартираБот — подборки для риелторов</title>
<script src="https://telegram.org/js/telegram-web-app.js"></script>
<style>
:root{
  --bg: var(--tg-theme-bg-color, #ffffff);
  --secbg: var(--tg-theme-secondary-bg-color, #f1f1f4);
  --text: var(--tg-theme-text-color, #1c1c1e);
  --hint: var(--tg-theme-hint-color, #8a8a8e);
  --link: var(--tg-theme-link-color, #2f80ed);
  --button: var(--tg-theme-button-color, #2f80ed);
  --button-text: var(--tg-theme-button-text-color, #ffffff);
  --border: rgba(128,128,128,.22);
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{margin:0;padding:0;background:var(--secbg);color:var(--text);font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,Helvetica,Arial,sans-serif;font-size:16px}
#root{max-width:480px;margin:0 auto;min-height:100vh;background:var(--bg);display:flex;flex-direction:column;position:relative}
#topbar{position:sticky;top:0;z-index:10;background:var(--bg);border-bottom:1px solid var(--border);padding:10px 14px;display:flex;align-items:center;justify-content:space-between;gap:10px}
.brand{font-weight:600;font-size:15px;white-space:nowrap}
.proto{font-weight:400;font-size:11px;color:var(--hint);background:var(--secbg);padding:2px 6px;border-radius:6px;margin-left:4px}
.seg{display:flex;background:var(--secbg);border-radius:9px;padding:2px}
.seg button{border:0;background:transparent;color:var(--hint);font-size:13px;padding:6px 12px;border-radius:7px;cursor:pointer}
.seg button.on{background:var(--bg);color:var(--text);box-shadow:0 1px 3px rgba(0,0,0,.12);font-weight:600}
#screen{flex:1;overflow-y:auto;padding-bottom:84px}
#tabbar{position:sticky;bottom:0;background:var(--bg);border-top:1px solid var(--border);display:flex;z-index:10}
#tabbar button{flex:1;border:0;background:transparent;color:var(--hint);padding:12px;font-size:13px;cursor:pointer}
#tabbar button.on{color:var(--link);font-weight:600}
.pad{padding:14px}
.h1{font-size:20px;font-weight:700;margin:6px 0}
.hint{color:var(--hint);font-size:13px;margin:4px 0 12px;line-height:1.5}
.rowtop{display:flex;align-items:center;justify-content:space-between;margin-bottom:8px}
.card{background:var(--bg);border:1px solid var(--border);border-radius:14px;padding:12px;margin-bottom:10px}
.card.tap{cursor:pointer}
.row{display:flex;align-items:center;gap:10px}
.grow{flex:1;min-width:0}
.grow>div{overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.sub{color:var(--hint);font-size:13px}
.sub2{font-size:13px;color:var(--hint);margin:18px 0 8px}
.mini{width:42px;height:42px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:20px;flex:none}
.src{font-size:11px;color:var(--hint);background:var(--secbg);padding:3px 7px;border-radius:7px;white-space:nowrap}
.chev{color:var(--hint);font-size:20px}
.btn{border:1px solid var(--border);background:var(--bg);color:var(--text);border-radius:10px;padding:10px 14px;font-size:14px;cursor:pointer;font-weight:500}
.btn.sm{padding:7px 12px;font-size:13px}
.btn.full{width:100%;margin-top:14px}
.btn.ghost{background:var(--secbg);border-color:transparent}
.btn.primary{background:var(--button);color:var(--button-text);border-color:var(--button)}
.lbl{display:block;font-size:12px;color:var(--hint);margin:14px 0 5px}
input{width:100%;border:1px solid var(--border);background:var(--bg);color:var(--text);border-radius:10px;padding:11px;font-size:15px;outline:none}
input:focus{border-color:var(--link)}
.linkrow{display:flex;gap:8px}
.linkrow input{flex:1;min-width:0}
.orline{display:flex;align-items:center;justify-content:center;margin:16px 0;color:var(--hint);font-size:12px}
.orline:before,.orline:after{content:'';flex:1;height:1px;background:var(--border)}
.orline span{padding:0 10px}
.two{display:flex;gap:10px}
.two>div{flex:1}
.pickrow{display:flex;align-items:center;gap:10px;border:1px solid var(--border);border-radius:12px;padding:10px;margin-bottom:8px;cursor:pointer}
.pickrow input{width:20px;height:20px;flex:none}
.empty{color:var(--hint);text-align:center;padding:30px 10px}
.back{background:none;border:0;color:var(--link);font-size:14px;padding:6px 0;cursor:pointer}
.b{font-size:12px;padding:4px 9px;border-radius:8px;white-space:nowrap;font-weight:500}
.b-like{background:#e3f6ea;color:#1d8a4e}
.b-show{background:#e5f0ff;color:#2f6fd0}
.b-no{background:var(--secbg);color:var(--hint)}
.b-wait{background:var(--secbg);color:var(--hint)}
.share{background:var(--secbg);border-radius:14px;padding:12px;margin:12px 0}
.stats{display:flex;gap:8px;margin:12px 0}
.stat{flex:1;background:var(--secbg);border-radius:12px;padding:12px;text-align:center}
.stat b{display:block;font-size:22px}
.stat span{font-size:12px;color:var(--hint)}
.stat.hot{background:#e5f0ff}
.stat.hot b{color:#2f6fd0}
.notif{background:#e5f0ff;color:#2f6fd0;border-radius:12px;padding:12px;font-size:13px;margin:6px 0 4px;line-height:1.5}
.clienthead{padding:14px 14px 0;text-align:center}
.prog{font-size:13px;color:var(--hint)}
.dots{display:flex;gap:5px;justify-content:center;margin-top:8px}
.dots span{width:7px;height:7px;border-radius:50%;background:var(--border)}
.dots span.on{background:var(--link)}
.ccard{margin:14px;border:1px solid var(--border);border-radius:18px;overflow:hidden}
.photo{height:190px;position:relative;display:flex;align-items:center;justify-content:center}
.photo .house{font-size:56px;opacity:.55}
.pill{position:absolute;top:10px;font-size:11px;background:rgba(255,255,255,.92);color:#333;padding:4px 9px;border-radius:8px}
.pill.left{left:10px}
.pill.right{right:10px}
.cbody{padding:14px}
.price{font-size:24px;font-weight:700}
.params{color:var(--hint);font-size:14px;margin-top:3px}
.addr{font-size:14px;margin-top:10px}
.tags{display:flex;gap:6px;flex-wrap:wrap;margin-top:10px}
.tag{font-size:12px;background:var(--secbg);color:var(--hint);padding:4px 9px;border-radius:8px}
.chips{display:flex;flex-wrap:wrap;gap:8px;margin-top:4px}
.chip{border:1px solid var(--border);background:var(--bg);color:var(--text);border-radius:10px;padding:9px 14px;font-size:14px;cursor:pointer}
.chip.on{background:var(--button);color:var(--button-text);border-color:var(--button)}
.chip.busy{background:var(--secbg);color:var(--hint);border-color:transparent;opacity:.65;cursor:default}
.slot{display:flex;align-items:center;gap:10px;padding:10px 12px;border:1px solid var(--border);border-radius:10px;margin-bottom:8px}
.slot .t{font-weight:600;width:46px;flex:none}
.slot .s{flex:1;font-size:13px;color:var(--hint)}
.slot.book{background:#e5f0ff;border-color:transparent}
.slot.book .s{color:#2f6fd0}
.slot.blk{background:var(--secbg);border-color:transparent}
.b-new{background:var(--secbg);color:var(--hint)}
.b-search{background:#e5f0ff;color:#2f6fd0}
.b-showing{background:#fbeede;color:#b5760f}
.b-offer{background:#fbe9e0;color:#c2521e}
.b-deal{background:#e3f6ea;color:#1d8a4e}
.funnel{display:flex;gap:6px;margin:10px 0}
.fcell{flex:1;min-width:0;background:var(--secbg);border-radius:10px;padding:8px 4px;text-align:center}
.fcell b{display:block;font-size:18px}
.fcell span{font-size:11px;color:var(--hint)}
.result{background:var(--secbg);border-radius:12px;padding:14px;margin:12px 0}
.result .big{font-size:26px;font-weight:700;margin:2px 0 0}
.kv{display:flex;justify-content:space-between;font-size:14px;margin-top:8px}
.kv span:first-child{color:var(--hint)}
.react{display:flex;gap:10px;padding:0 14px 18px}
.rb{flex:1;border:0;border-radius:14px;padding:16px 8px;font-size:15px;font-weight:600;cursor:pointer}
.rb.no{flex:0 0 56px;background:var(--secbg);color:var(--hint);font-size:20px}
.rb.like{background:#e3f6ea;color:#1d8a4e}
.rb.show{background:var(--button);color:var(--button-text)}
.center{text-align:center;padding-top:40px}
.big{font-size:54px;margin-bottom:6px}
#toast{position:fixed;left:50%;bottom:96px;transform:translateX(-50%) translateY(20px);background:#222;color:#fff;padding:10px 16px;border-radius:10px;font-size:13px;opacity:0;pointer-events:none;transition:.25s;z-index:50;max-width:90%;text-align:center}
#toast.show{opacity:1;transform:translateX(-50%) translateY(0)}
</style>
</head>
<body>
<div id="root">
  <header id="topbar"></header>
  <main id="screen"></main>
  <nav id="tabbar"></nav>
</div>
<script>
var KEY = 'kvartirabot_mvp_v3';
var SEED = {
  objects: [
    {id:'o1', price:7900000, rooms:2, area:54, floor:'6/12', address:'ул. Артёма, 12', district:'Калининский', tags:['Новостройка','Свежий ремонт'], photo:1, source:'Авито'},
    {id:'o2', price:6200000, rooms:2, area:48, floor:'3/9', address:'пр. Мира, 5', district:'Ворошиловский', tags:['Кирпич','Закрытый двор'], photo:2, source:'Циан'},
    {id:'o3', price:5400000, rooms:1, area:38, floor:'8/10', address:'ул. Шевченко, 30', district:'Калининский', tags:['Распашонка'], photo:3, source:'вручную'},
    {id:'o4', price:9300000, rooms:3, area:72, floor:'4/5', address:'бул. Пушкина, 8', district:'Ворошиловский', tags:['Сталинка','Высокие потолки'], photo:4, source:'Авито'},
    {id:'o5', price:4100000, rooms:1, area:32, floor:'2/9', address:'ул. Университетская, 41', district:'Киевский', tags:['Под ремонт'], photo:5, source:'Домклик'},
    {id:'o6', price:11800000, rooms:3, area:88, floor:'9/16', address:'пр. Ильича, 100', district:'Будённовский', tags:['Новостройка','Панорама'], photo:6, source:'Авито'}
  ],
  podborki: [
    {id:'p1', client:'Иван Петров', criteria:'2-комн до 8 млн, Калининский', objectIds:['o1','o2','o3'], createdAt: Date.now()-86400000}
  ],
  reactions: { p1: { o2:'like', o1:'show' } },
  showings: [ {id:'s1', podId:'p1', objectId:'o1', when:'Завтра, 18:00', day:'Завтра', time:'18:00', comment:'', status:'new'} ],
  blocks: {'Завтра|12:00': true},
  clients: [
    {id:'c1', name:'Иван Петров', phone:'+7 949 123-45-67', budget:'до 8 млн', criteria:'2-комн, Калининский', status:'showing', source:'Авито', note:''},
    {id:'c2', name:'Мария Лукьяненко', phone:'+7 949 765-43-21', budget:'до 5 млн', criteria:'1-комн, центр', status:'search', source:'Рекомендация', note:''}
  ]
};

function load(){
  try{ var r = localStorage.getItem(KEY); if(r) return JSON.parse(r); }catch(e){}
  var s = JSON.parse(JSON.stringify(SEED));
  try{ localStorage.setItem(KEY, JSON.stringify(s)); }catch(e){}
  return s;
}
function save(){ try{ localStorage.setItem(KEY, JSON.stringify(state)); }catch(e){} }
function resetAll(){ try{ localStorage.removeItem(KEY); }catch(e){} state = load(); ui = {role:'agent',screen:'objects',podborka:null,client:null,ci:0}; render(); toast('Данные сброшены'); }

var state = load();
if(!state.showings) state.showings = [];
if(!state.reactions) state.reactions = {};
if(!state.blocks) state.blocks = {};
if(!state.clients) state.clients = [];
state.showings.forEach(function(sh){ if(!sh.time && sh.when){ var pp=sh.when.split(', '); sh.day=pp[0]; sh.time=pp[1]||''; } });
var ui = { role:'agent', screen:'objects', podborka:null, client:null, ci:0, booking:null, bDayLabel:null, bTime:null, schedDay:null, crmClient:null, calc:false, ownerView:null, _calcPrice:0 };

function money(n){ return (n||0).toLocaleString('ru-RU') + ' ₽'; }
function esc(s){ return String(s==null?'':s).replace(/[&<>"]/g, function(c){ return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]; }); }
function uid(p){ return p + Math.random().toString(36).slice(2,7); }
function obj(id){ for(var i=0;i<state.objects.length;i++){ if(state.objects[i].id===id) return state.objects[i]; } return null; }
function pod(id){ for(var i=0;i<state.podborki.length;i++){ if(state.podborki[i].id===id) return state.podborki[i]; } return null; }
function photoBg(n){ var c=['#dce8fb','#e7e0fb','#fbe3e0','#dff7ec','#fbf3d6','#e1eefb']; return c[((n||1)-1)%c.length]; }
function firstName(s){ return String(s||'').split(' ')[0] || 'Клиент'; }
function haptic(t){ try{ window.Telegram && window.Telegram.WebApp && window.Telegram.WebApp.HapticFeedback && window.Telegram.WebApp.HapticFeedback.impactOccurred(t||'light'); }catch(e){} }
var MON = ['янв','фев','мар','апр','мая','июн','июл','авг','сен','окт','ноя','дек'];
var TIMES = ['10:00','11:00','12:00','13:00','14:00','15:00','16:00','17:00','18:00','19:00','20:00'];
function dayChips(){
  var arr = [];
  for(var i=0;i<5;i++){ var d=new Date(); d.setDate(d.getDate()+i);
    var label = i===0?'Сегодня' : i===1?'Завтра' : (d.getDate()+' '+MON[d.getMonth()]);
    arr.push({id:'d'+i, label:label});
  }
  return arr;
}
function findShowing(podId, objId){ for(var i=0;i<state.showings.length;i++){ var s=state.showings[i]; if(s.podId===podId && s.objectId===objId) return s; } return null; }
function slotKey(day, time){ return day + '|' + time; }
function slotStatus(day, time, exclId){
  for(var i=0;i<state.showings.length;i++){ var s=state.showings[i]; if(s.day===day && s.time===time && s.id!==exclId) return {type:'booking', showing:s}; }
  if(state.blocks[slotKey(day, time)]) return {type:'blocked'};
  return null;
}
var STATUSES = [['new','Новый'],['search','Подбор'],['showing','Показы'],['offer','Торг'],['deal','Сделка']];
function statusLabel(s){ for(var i=0;i<STATUSES.length;i++){ if(STATUSES[i][0]===s) return STATUSES[i][1]; } return s; }
function statusBadge(s){ return '<span class="b b-'+s+'">'+esc(statusLabel(s))+'</span>'; }
function crmClient(id){ for(var i=0;i<state.clients.length;i++){ if(state.clients[i].id===id) return state.clients[i]; } return null; }
function num(id){ var el=document.getElementById(id); return el ? (parseInt((el.value||'').replace(/\D/g,''),10)||0) : 0; }
function objStats(objId){
  var inPods=0, likes=0, shows=0, viewers=0;
  state.podborki.forEach(function(p){
    if(p.objectIds.indexOf(objId)>=0){ inPods++; var r=state.reactions[p.id]||{}; if(r[objId]){ viewers++; if(r[objId]==='like') likes++; if(r[objId]==='show') shows++; } }
  });
  var sh=0; state.showings.forEach(function(x){ if(x.objectId===objId) sh++; });
  return {inPods:inPods, likes:likes, shows:shows, viewers:viewers, showings:sh};
}

function counts(podId){
  var r = state.reactions[podId] || {}, like=0, show=0, no=0;
  for(var k in r){ if(r[k]==='like') like++; else if(r[k]==='show') show++; else if(r[k]==='dislike') no++; }
  return {like:like, show:show, no:no};
}
function badge(t){
  if(t==='like') return '<span class="b b-like">Нравится</span>';
  if(t==='show') return '<span class="b b-show">Хочет показ</span>';
  if(t==='dislike') return '<span class="b b-no">Не то</span>';
  return '<span class="b b-wait">Ждём реакции</span>';
}
function react(podId, objId, type){
  if(!state.reactions[podId]) state.reactions[podId] = {};
  state.reactions[podId][objId] = type;
  save();
  haptic(type==='show'?'medium':'light');
}

function toast(msg){
  var t = document.getElementById('toast');
  if(!t){ t = document.createElement('div'); t.id='toast'; document.body.appendChild(t); }
  t.textContent = msg; t.className='show';
  clearTimeout(window.__tt); window.__tt = setTimeout(function(){ t.className=''; }, 1800);
}

/* ----- agent: objects ----- */
function screenObjects(){
  var s = document.getElementById('screen');
  s.innerHTML = '<div class="pad">'
    + '<div class="rowtop"><div class="h1">Объекты</div><button class="btn sm" onclick="go(\'addObject\')">+ Добавить</button></div>'
    + state.objects.map(function(o){
        return '<div class="card"><div class="row">'
          + '<div class="mini" style="background:'+photoBg(o.photo)+'">🏢</div>'
          + '<div class="grow"><div><b>'+money(o.price)+'</b></div><div class="sub">'+o.rooms+'-комн · '+o.area+' м² · '+esc(o.address)+'</div></div>'
          + '<span class="src">'+esc(o.source)+'</span></div>'
          + '<button class="btn sm" style="margin-top:10px" onclick="openOwner(\''+o.id+'\')">📊 Отчёт собственнику</button></div>';
      }).join('')
    + '</div>';
}

function screenAddObject(){
  var s = document.getElementById('screen');
  s.innerHTML = '<div class="pad">'
    + '<button class="back" onclick="go(\'objects\')">‹ Объекты</button>'
    + '<div class="h1">Добавить объект</div>'
    + '<label class="lbl">Ссылка на объявление</label>'
    + '<div class="linkrow"><input id="f_link" placeholder="avito.ru/... · cian.ru/..."><button class="btn sm" onclick="pullLink()">Подтянуть</button></div>'
    + '<div class="hint" id="f_note">Возьмём фото, цену и параметры — ты проверишь и сохранишь</div>'
    + '<div class="orline"><span>или</span></div>'
    + '<button class="btn ghost full" style="margin-top:0" onclick="uploadTable()">⬆ Загрузить таблицу (Excel/CSV) — демо</button>'
    + '<div class="orline"><span>заполнить вручную</span></div>'
    + '<label class="lbl">Цена</label><input id="f_price" placeholder="7 900 000">'
    + '<div class="two"><div><label class="lbl">Комнат</label><input id="f_rooms" placeholder="2"></div><div><label class="lbl">Площадь, м²</label><input id="f_area" placeholder="54"></div></div>'
    + '<div class="two"><div><label class="lbl">Этаж</label><input id="f_floor" placeholder="6/12"></div><div><label class="lbl">Район</label><input id="f_district" placeholder="Калининский"></div></div>'
    + '<label class="lbl">Адрес</label><input id="f_addr" placeholder="ул. Артёма, 12">'
    + '<button class="btn full primary" onclick="saveObject()">Сохранить в базу</button>'
    + '</div>';
}
function pullLink(){
  var link = (document.getElementById('f_link').value||'').trim();
  document.getElementById('f_price').value = '8 500 000';
  document.getElementById('f_rooms').value = '2';
  document.getElementById('f_area').value = '56';
  document.getElementById('f_floor').value = '5/14';
  document.getElementById('f_addr').value = 'ул. Стратонавтов, 7';
  document.getElementById('f_district').value = 'Киевский';
  document.getElementById('f_note').textContent = link ? 'Подтянуто из ссылки — проверь и сохрани' : 'Это демо-заполнение. Проверь и сохрани';
  toast('Данные подтянуты');
}
function saveObject(){
  var price = parseInt((document.getElementById('f_price').value||'').replace(/\D/g,''),10) || 0;
  var addr = (document.getElementById('f_addr').value||'').trim();
  if(!price && !addr){ toast('Заполни хотя бы цену и адрес'); return; }
  var o = {
    id: uid('o'), price: price,
    rooms: parseInt(document.getElementById('f_rooms').value,10) || 0,
    area: parseInt(document.getElementById('f_area').value,10) || 0,
    floor: (document.getElementById('f_floor').value||'').trim(),
    address: addr || 'Без адреса',
    district: (document.getElementById('f_district').value||'').trim(),
    tags: [], photo: Math.floor(Math.random()*6)+1, source: 'добавлен'
  };
  state.objects.unshift(o); save(); ui.screen='objects'; render(); toast('Объект добавлен');
}
function uploadTable(){
  var sample = [
    {price:6800000, rooms:2, area:51, floor:'7/10', address:'ул. Кобозева, 22', district:'Ворошиловский'},
    {price:3900000, rooms:1, area:34, floor:'1/5', address:'ул. Левобережная, 3', district:'Пролетарский'},
    {price:14500000, rooms:4, area:110, floor:'5/9', address:'пр. Театральный, 17', district:'Ворошиловский'}
  ];
  sample.forEach(function(x){
    state.objects.unshift({id:uid('o'), price:x.price, rooms:x.rooms, area:x.area, floor:x.floor, address:x.address, district:x.district, tags:[], photo:Math.floor(Math.random()*6)+1, source:'из таблицы'});
  });
  save(); ui.screen='objects'; render(); toast('Загружено 3 объекта из таблицы');
}

/* ----- agent: podborki ----- */
function screenPodborki(){
  var s = document.getElementById('screen');
  var list = state.podborki.length
    ? state.podborki.map(function(p){
        var c = counts(p.id);
        return '<div class="card tap" onclick="openDash(\''+p.id+'\')">'
          + '<div class="row"><div class="grow"><b>'+esc(p.client)+'</b></div><span class="chev">›</span></div>'
          + '<div class="sub">'+p.objectIds.length+' объектов · '+c.like+' нравится'+(c.show?' · '+c.show+' на показ':'')+'</div></div>';
      }).join('')
    : '<div class="empty">Пока нет подборок. Создай первую.</div>';
  s.innerHTML = '<div class="pad"><div class="rowtop"><div class="h1">Подборки</div><button class="btn sm" onclick="go(\'newPodborka\')">+ Создать</button></div>'+list+'</div>';
}
function openDash(id){ ui.podborka=id; ui.screen='dashboard'; render(); }

function screenNewPodborka(){
  var s = document.getElementById('screen');
  s.innerHTML = '<div class="pad">'
    + '<button class="back" onclick="go(\'podborki\')">‹ Назад</button>'
    + '<div class="h1">Новая подборка</div>'
    + '<label class="lbl">Клиент</label><input id="f_client" placeholder="Имя клиента">'
    + '<label class="lbl">Что ищет (необязательно)</label><input id="f_crit" placeholder="2-комн до 8 млн, Калининский">'
    + '<label class="lbl">Объекты в подборку</label>'
    + state.objects.map(function(o){
        return '<label class="pickrow"><input type="checkbox" class="objpick" value="'+o.id+'">'
          + '<div class="mini" style="background:'+photoBg(o.photo)+'">🏢</div>'
          + '<div class="grow"><div>'+esc(o.address)+'</div><div class="sub">'+money(o.price)+' · '+o.rooms+'-комн</div></div></label>';
      }).join('')
    + '<button class="btn full primary" onclick="createPodborka()">Создать подборку</button>'
    + '</div>';
}
function createPodborka(){
  var client = (document.getElementById('f_client').value||'').trim() || 'Клиент';
  var crit = (document.getElementById('f_crit').value||'').trim();
  var checks = document.querySelectorAll('.objpick:checked');
  var ids = []; for(var i=0;i<checks.length;i++) ids.push(checks[i].value);
  if(!ids.length){ toast('Выбери хотя бы один объект'); return; }
  var p = {id:uid('p'), client:client, criteria:crit, objectIds:ids, createdAt:Date.now()};
  state.podborki.unshift(p); save(); ui.podborka=p.id; ui.screen='dashboard'; render(); toast('Подборка создана');
}

function screenDashboard(){
  var s = document.getElementById('screen'); var p = pod(ui.podborka);
  if(!p){ ui.screen='podborki'; return screenPodborki(); }
  var c = counts(p.id); var r = state.reactions[p.id] || {};
  var url = location.origin + location.pathname + '?p=' + p.id;
  var shows = p.objectIds.filter(function(id){ return r[id]==='show'; });
  s.innerHTML = '<div class="pad">'
    + '<button class="back" onclick="go(\'podborki\')">‹ Подборки</button>'
    + '<div class="h1">'+esc(p.client)+'</div>'
    + '<div class="hint">'+(p.criteria?esc(p.criteria):'без критериев')+'</div>'
    + '<div class="share"><div class="sub">Ссылка для клиента</div>'
      + '<div class="linkrow" style="margin:6px 0 10px"><input readonly value="'+esc(url)+'"><button class="btn sm" onclick="copyLink(\''+p.id+'\')">Копировать</button></div>'
      + '<button class="btn ghost full" style="margin-top:0" onclick="openAsClient(\''+p.id+'\')">▶ Открыть как клиент (демо)</button></div>'
    + '<div class="stats">'
      + '<div class="stat"><b>'+p.objectIds.length+'</b><span>объектов</span></div>'
      + '<div class="stat"><b>'+c.like+'</b><span>нравится</span></div>'
      + '<div class="stat'+(c.show?' hot':'')+'"><b>'+c.show+'</b><span>на показ</span></div></div>'
    + (shows.length ? '<div class="notif">🔔 <b>'+esc(firstName(p.client))+'</b> записался на показ: '+shows.map(function(id){var sh=findShowing(p.id,id);return esc(obj(id).address)+(sh?' — '+esc(sh.when):'');}).join('; ')+'</div>' : '')
    + '<div class="sub2">Реакции по объектам</div>'
    + p.objectIds.map(function(id){ var o=obj(id); if(!o) return '';
        var sh = findShowing(p.id, id);
        var right = (r[id]==='show' && sh) ? '<span class="b b-show">📅 '+esc(sh.when)+'</span>' : badge(r[id]);
        return '<div class="card"><div class="row">'
          + '<div class="mini" style="background:'+photoBg(o.photo)+'">🏢</div>'
          + '<div class="grow"><div>'+esc(o.address)+'</div><div class="sub">'+money(o.price)+'</div></div>'
          + right+'</div></div>';
      }).join('')
    + '</div>';
}
function copyLink(id){
  var url = location.origin + location.pathname + '?p=' + id;
  if(navigator.clipboard && navigator.clipboard.writeText){
    navigator.clipboard.writeText(url).then(function(){ toast('Ссылка скопирована'); }, function(){ toast('Скопируй вручную: '+url); });
  } else { toast('Скопируй вручную: '+url); }
}

/* ----- client ----- */
function openAsClient(id){ ui.role='client'; ui.client=id; ui.ci=0; render(); }
function clientReact(type){
  var p = pod(ui.client); if(!p) return;
  react(p.id, p.objectIds[ui.ci], type); ui.ci++; render();
}
function screenClient(){
  var s = document.getElementById('screen');
  if(!ui.client){
    s.innerHTML = '<div class="pad"><div class="h1">Открыть подборку</div>'
      + '<div class="hint">В реальном продукте клиент открывает её по ссылке от риелтора. Для демо выбери подборку:</div>'
      + '<div class="card tap" onclick="openCalc()"><div class="row"><div class="grow"><b>🧮 Ипотечный калькулятор</b><div class="sub">Посчитать платёж и оставить заявку</div></div><span class="chev">›</span></div></div>'
      + state.podborki.map(function(p){
          return '<div class="card tap" onclick="openAsClient(\''+p.id+'\')"><div class="row"><div class="grow"><b>'+esc(p.client)+'</b></div><span class="chev">›</span></div><div class="sub">'+p.objectIds.length+' объектов'+(p.criteria?' · '+esc(p.criteria):'')+'</div></div>';
        }).join('')
      + '</div>';
    return;
  }
  var p = pod(ui.client);
  if(!p){ ui.client=null; return screenClient(); }
  if(ui.booking){ return screenBooking(); }
  if(ui.ci >= p.objectIds.length){
    var c = counts(p.id);
    s.innerHTML = '<div class="pad center"><div class="big">🎉</div><div class="h1">Готово!</div>'
      + '<div class="hint">Спасибо! Риелтор уже видит, что вам понравилось'+(c.show?', и какие квартиры показать':'')+'.</div>'
      + '<button class="btn ghost full" onclick="ui.ci=0;render()">Посмотреть заново</button>'
      + '<button class="btn full" onclick="setRole(\'agent\')">Я риелтор — открыть реакции</button></div>';
    return;
  }
  var o = obj(p.objectIds[ui.ci]);
  s.innerHTML = '<div class="clienthead"><div class="prog">'+(ui.ci+1)+' / '+p.objectIds.length+'</div>'
    + '<div class="dots">'+p.objectIds.map(function(_,i){ return '<span class="'+(i<=ui.ci?'on':'')+'"></span>'; }).join('')+'</div></div>'
    + '<div class="ccard"><div class="photo" style="background:'+photoBg(o.photo)+'">'
      + '<span class="pill left">'+esc(o.district)+'</span><span class="pill right">фото скоро</span><span class="house">🏢</span></div>'
    + '<div class="cbody"><div class="price">'+money(o.price)+'</div>'
      + '<div class="params">'+o.rooms+'-комн · '+o.area+' м² · '+esc(o.floor)+' этаж</div>'
      + '<div class="addr">📍 '+esc(o.address)+'</div>'
      + '<div class="tags">'+(o.tags||[]).map(function(t){ return '<span class="tag">'+esc(t)+'</span>'; }).join('')+'</div></div></div>'
    + '<div class="react">'
      + '<button class="rb no" onclick="clientReact(\'dislike\')" aria-label="Не то">✕</button>'
      + '<button class="rb like" onclick="clientReact(\'like\')">♡ Нравится</button>'
      + '<button class="rb show" onclick="openBooking()">📅 На показ</button></div>';
}

/* ----- booking / showings ----- */
function openBooking(){ ui.booking = pod(ui.client).objectIds[ui.ci]; ui.bDayLabel=null; ui.bTime=null; render(); }
function pickDay(label){ ui.bDayLabel=label; ui.bTime=null; render(); }
function pickTime(t){ ui.bTime=t; render(); }
function cancelBooking(){ ui.booking=null; render(); }
function confirmBooking(){
  if(!ui.bDayLabel || !ui.bTime){ toast('Выбери день и время'); return; }
  var p = pod(ui.client); var objId = ui.booking;
  var ex = findShowing(p.id, objId);
  if(slotStatus(ui.bDayLabel, ui.bTime, ex?ex.id:null)){ toast('Это время уже занято — выбери другое'); return; }
  var when = ui.bDayLabel + ', ' + ui.bTime;
  var cEl = document.getElementById('b_comment');
  var comment = (cEl && cEl.value || '').trim();
  if(ex){ ex.when=when; ex.day=ui.bDayLabel; ex.time=ui.bTime; ex.comment=comment; ex.status='new'; }
  else { state.showings.unshift({id:uid('s'), podId:p.id, objectId:objId, when:when, day:ui.bDayLabel, time:ui.bTime, comment:comment, status:'new'}); }
  react(p.id, objId, 'show');
  ui.booking=null; ui.ci++; render(); haptic('medium'); toast('Вы записаны на показ');
}
function bookingTimes(){
  if(!ui.bDayLabel) return '<div class="hint">Сначала выбери день</div>';
  var p = pod(ui.client); var ex = findShowing(p.id, ui.booking); var exId = ex?ex.id:null;
  return '<div class="chips">' + TIMES.map(function(t){
    if(slotStatus(ui.bDayLabel, t, exId)) return '<button class="chip busy" disabled>'+t+' · занято</button>';
    return '<button class="chip'+(ui.bTime===t?' on':'')+'" onclick="pickTime(\''+t+'\')">'+t+'</button>';
  }).join('') + '</div>';
}
function screenBooking(){
  var s = document.getElementById('screen');
  var o = obj(ui.booking); var days = dayChips();
  s.innerHTML = '<div class="pad">'
    + '<button class="back" onclick="cancelBooking()">‹ Назад к квартире</button>'
    + '<div class="h1">Запись на показ</div>'
    + '<div class="card"><div class="row"><div class="mini" style="background:'+photoBg(o.photo)+'">🏢</div>'
      + '<div class="grow"><div><b>'+money(o.price)+'</b></div><div class="sub">'+esc(o.address)+'</div></div></div></div>'
    + '<label class="lbl">Удобный день</label><div class="chips">'
    + days.map(function(d){ return '<button class="chip'+(ui.bDayLabel===d.label?' on':'')+'" onclick="pickDay(\''+d.label+'\')">'+esc(d.label)+'</button>'; }).join('')
    + '</div>'
    + '<label class="lbl">Время</label>' + bookingTimes()
    + '<label class="lbl">Комментарий риелтору (необязательно)</label><input id="b_comment" placeholder="Например: после 18:00 удобнее">'
    + '<button class="btn full primary" onclick="confirmBooking()">📅 Записаться на показ</button>'
    + '<button class="btn ghost full" onclick="cancelBooking()">Отмена</button>'
    + '</div>';
}
function pickSchedDay(label){ ui.schedDay=label; render(); }
function blockSlot(day, time){ state.blocks[slotKey(day, time)] = true; save(); render(); haptic('light'); }
function freeSlot(day, time){ delete state.blocks[slotKey(day, time)]; save(); render(); }
function screenShowings(){
  var s = document.getElementById('screen');
  var days = dayChips(); var selDay = ui.schedDay || days[0].label;
  var dayrow = '<div class="chips">' + days.map(function(d){ return '<button class="chip'+(selDay===d.label?' on':'')+'" onclick="pickSchedDay(\''+esc(d.label)+'\')">'+esc(d.label)+'</button>'; }).join('') + '</div>';
  var grid = TIMES.map(function(t){
    var st = slotStatus(selDay, t);
    if(st && st.type==='booking'){
      var o=obj(st.showing.objectId), pp=pod(st.showing.podId);
      return '<div class="slot book"><span class="t">'+t+'</span><span class="s">Запись: '+esc(pp?firstName(pp.client):'')+(o?' · '+esc(o.address):'')+'</span><span class="b b-show">показ</span></div>';
    }
    if(st && st.type==='blocked'){
      return '<div class="slot blk"><span class="t">'+t+'</span><span class="s">Занято вами</span><button class="btn sm" onclick="freeSlot(\''+esc(selDay)+'\',\''+t+'\')">Освободить</button></div>';
    }
    return '<div class="slot"><span class="t">'+t+'</span><span class="s">свободно</span><button class="btn sm" onclick="blockSlot(\''+esc(selDay)+'\',\''+t+'\')">Занять</button></div>';
  }).join('');
  var list = state.showings.length
    ? state.showings.map(function(sh){
        var o = obj(sh.objectId); var p = pod(sh.podId);
        var st = sh.status==='confirmed' ? '<span class="b b-like">Подтверждён</span>' : '<span class="b b-show">Новый</span>';
        return '<div class="card">'
          + '<div class="row"><div class="grow"><b>'+esc(o?o.address:'—')+'</b></div>'+st+'</div>'
          + '<div class="sub" style="margin-top:4px">📅 '+esc(sh.when)+' · '+esc(p?p.client:'')+'</div>'
          + (sh.comment ? '<div class="sub" style="margin-top:4px">💬 '+esc(sh.comment)+'</div>' : '')
          + (sh.status==='confirmed' ? '' : '<button class="btn sm" style="margin-top:10px" onclick="confirmShowing(\''+sh.id+'\')">Подтвердить показ</button>')
          + '</div>';
      }).join('')
    : '<div class="empty">Пока никто не записался на показ.</div>';
  s.innerHTML = '<div class="pad"><div class="h1">Показы</div>'
    + '<div class="sub2">Моя занятость</div>'
    + '<div class="hint">Выбери день и займи слоты, когда ты недоступен — клиент их выбрать не сможет. Записи клиентов появляются тут же.</div>'
    + dayrow + '<div style="margin-top:10px">' + grid + '</div>'
    + '<div class="sub2">Записи клиентов</div>' + list + '</div>';
}
function confirmShowing(id){
  for(var i=0;i<state.showings.length;i++){ if(state.showings[i].id===id){ state.showings[i].status='confirmed'; break; } }
  save(); render(); toast('Показ подтверждён');
}

/* ----- CRM ----- */
function screenClients(){
  var s = document.getElementById('screen');
  var f = {}; STATUSES.forEach(function(x){ f[x[0]]=0; });
  state.clients.forEach(function(c){ if(f[c.status]!=null) f[c.status]++; });
  var funnel = '<div class="funnel">' + STATUSES.map(function(x){ return '<div class="fcell"><b>'+f[x[0]]+'</b><span>'+esc(x[1])+'</span></div>'; }).join('') + '</div>';
  var list = state.clients.length
    ? state.clients.map(function(c){
        return '<div class="card tap" onclick="openClient(\''+c.id+'\')">'
          + '<div class="row"><div class="grow"><b>'+esc(c.name)+'</b><div class="sub">'+esc(c.budget||'')+(c.criteria?' · '+esc(c.criteria):'')+'</div></div>'+statusBadge(c.status)+'</div>'
          + '<div class="sub" style="margin-top:6px">📞 '+esc(c.phone||'—')+' · источник: '+esc(c.source||'—')+'</div></div>';
      }).join('')
    : '<div class="empty">Пока нет клиентов. Добавь вручную или они придут с калькулятора.</div>';
  s.innerHTML = '<div class="pad"><div class="rowtop"><div class="h1">Клиенты</div><button class="btn sm" onclick="addClientManual()">+ Клиент</button></div>'
    + funnel + list
    + '<button class="btn ghost full" onclick="openCalc()">🧮 Открыть калькулятор (лид-магнит)</button></div>';
}
function openClient(id){ ui.crmClient=id; ui.screen='clientDetail'; render(); }
function addClientManual(){ var c={id:uid('c'), name:'Новый клиент', phone:'', budget:'', criteria:'', status:'new', source:'вручную', note:''}; state.clients.unshift(c); save(); openClient(c.id); }
function screenClientDetail(){
  var s = document.getElementById('screen'); var c = crmClient(ui.crmClient);
  if(!c){ ui.screen='clients'; return screenClients(); }
  s.innerHTML = '<div class="pad"><button class="back" onclick="go(\'clients\')">‹ Клиенты</button>'
    + '<div class="h1">'+esc(c.name)+'</div>'
    + '<div class="hint">источник: '+esc(c.source||'—')+'</div>'
    + '<label class="lbl">Имя</label><input id="cl_name" value="'+esc(c.name)+'">'
    + '<label class="lbl">Телефон</label><input id="cl_phone" value="'+esc(c.phone||'')+'" inputmode="tel">'
    + '<div class="two"><div><label class="lbl">Бюджет</label><input id="cl_budget" value="'+esc(c.budget||'')+'"></div>'
      + '<div><label class="lbl">Что ищет</label><input id="cl_crit" value="'+esc(c.criteria||'')+'"></div></div>'
    + '<label class="lbl">Стадия сделки</label><div class="chips">'
    + STATUSES.map(function(x){ return '<button class="chip'+(c.status===x[0]?' on':'')+'" onclick="setClientStatus(\''+c.id+'\',\''+x[0]+'\')">'+esc(x[1])+'</button>'; }).join('')
    + '</div>'
    + '<label class="lbl">Заметка / напоминание</label><textarea id="cl_note" rows="3" style="width:100%;border:1px solid var(--border);background:var(--bg);color:var(--text);border-radius:10px;padding:11px;font-size:15px;font-family:inherit">'+esc(c.note||'')+'</textarea>'
    + '<button class="btn full primary" onclick="saveClient(\''+c.id+'\')">Сохранить</button>'
    + '<button class="btn ghost full" onclick="deleteClient(\''+c.id+'\')">Удалить клиента</button></div>';
}
function setClientStatus(id, st){ var c=crmClient(id); if(c){ c.status=st; save(); render(); haptic('light'); } }
function saveClient(id){ var c=crmClient(id); if(!c) return;
  var g=function(x){ var e=document.getElementById(x); return e?e.value.trim():undefined; };
  var nm=g('cl_name'); if(nm) c.name=nm; c.phone=g('cl_phone')||''; c.budget=g('cl_budget')||''; c.criteria=g('cl_crit')||''; c.note=g('cl_note')||'';
  save(); toast('Сохранено');
}
function deleteClient(id){ state.clients = state.clients.filter(function(c){ return c.id!==id; }); save(); ui.screen='clients'; render(); toast('Клиент удалён'); }

/* ----- калькулятор (лид-магнит) ----- */
function openCalc(price){ ui.calc=true; ui._calcPrice = price||0; render(); }
function closeCalc(){ ui.calc=false; render(); }
function screenCalc(){
  var s = document.getElementById('screen');
  var pp = ui._calcPrice || 6000000;
  s.innerHTML = '<div class="pad"><button class="back" onclick="closeCalc()">‹ Назад</button>'
    + '<div class="h1">🧮 Ипотечный калькулятор</div>'
    + '<div class="hint">Прикинь платёж по квартире. Это же — лид-магнит: клиент считает и оставляет заявку, она падает тебе в «Клиенты».</div>'
    + '<label class="lbl">Стоимость, ₽</label><input id="c_price" value="'+pp.toLocaleString('ru-RU')+'" inputmode="numeric">'
    + '<div class="two"><div><label class="lbl">Первый взнос, ₽</label><input id="c_dp" value="'+Math.round(pp*0.2).toLocaleString('ru-RU')+'" inputmode="numeric"></div>'
      + '<div><label class="lbl">Срок, лет</label><input id="c_years" value="20" inputmode="numeric"></div></div>'
    + '<label class="lbl">Ставка, % годовых</label><input id="c_rate" value="18" inputmode="decimal">'
    + '<button class="btn full primary" onclick="calcCompute()">Рассчитать</button>'
    + '<div id="calc_result"></div>'
    + '<div class="card" style="margin-top:16px"><div class="sub2" style="margin-top:0">Оставить заявку риелтору</div>'
      + '<input id="lead_name" placeholder="Имя"><div style="height:8px"></div>'
      + '<input id="lead_phone" placeholder="Телефон" inputmode="tel">'
      + '<button class="btn full primary" onclick="addLead()">Оставить заявку</button></div></div>';
  calcCompute();
}
function calcCompute(){
  var price=num('c_price'), dp=num('c_dp'), years=num('c_years')||1;
  var rate=parseFloat((document.getElementById('c_rate').value||'').replace(',','.'))||0;
  var loan=Math.max(0, price-dp), r=rate/12/100, n=years*12;
  var pay = (r>0) ? loan*r/(1-Math.pow(1+r,-n)) : (n>0?loan/n:0);
  var over=pay*n-loan;
  var ded=Math.min(Math.min(price,2000000)*0.13, 260000);
  var el=document.getElementById('calc_result'); if(!el) return;
  el.innerHTML = '<div class="result"><div class="sub">Ежемесячный платёж</div><p class="big">'+Math.round(pay).toLocaleString('ru-RU')+' ₽</p>'
    + '<div class="kv"><span>Сумма кредита</span><span>'+Math.round(loan).toLocaleString('ru-RU')+' ₽</span></div>'
    + '<div class="kv"><span>Переплата за '+years+' лет</span><span>'+Math.round(over).toLocaleString('ru-RU')+' ₽</span></div>'
    + '<div class="kv"><span>Налоговый вычет до</span><span>'+Math.round(ded).toLocaleString('ru-RU')+' ₽</span></div></div>';
}
function addLead(){
  var nm=(document.getElementById('lead_name').value||'').trim();
  var ph=(document.getElementById('lead_phone').value||'').trim();
  if(!ph){ toast('Укажи телефон'); return; }
  state.clients.unshift({id:uid('c'), name:nm||'Заявка с калькулятора', phone:ph, budget:'', criteria:'ипотека / расчёт', status:'new', source:'калькулятор', note:''});
  save(); haptic('medium'); toast('Заявка отправлена риелтору ✓');
  document.getElementById('lead_name').value=''; document.getElementById('lead_phone').value='';
}

/* ----- отчёт собственнику ----- */
function openOwner(objId){ ui.ownerView=objId; render(); }
function closeOwner(){ ui.ownerView=null; ui.role='agent'; ui.screen='objects'; render(); }
function screenOwner(){
  var s = document.getElementById('screen'); var o=obj(ui.ownerView);
  if(!o){ ui.ownerView=null; return render(); }
  var st=objStats(o.id); var url=location.origin+location.pathname+'?owner='+o.id;
  var interest = st.viewers ? Math.round(st.likes/st.viewers*100) : 0;
  s.innerHTML = '<div class="pad"><button class="back" onclick="closeOwner()">‹ Назад (это видит собственник)</button>'
    + '<div class="h1">Отчёт по вашей квартире</div>'
    + '<div class="card"><div class="row"><div class="mini" style="background:'+photoBg(o.photo)+'">🏢</div><div class="grow"><div><b>'+esc(o.address)+'</b></div><div class="sub">'+money(o.price)+'</div></div></div></div>'
    + '<div class="stats"><div class="stat"><b>'+st.inPods+'</b><span>в подборках</span></div>'
      + '<div class="stat"><b>'+st.viewers+'</b><span>смотрели</span></div>'
      + '<div class="stat"><b>'+interest+'%</b><span>интерес</span></div></div>'
    + '<div class="stats"><div class="stat"><b>'+st.likes+'</b><span>понравилось</span></div>'
      + '<div class="stat'+(st.shows?' hot':'')+'"><b>'+st.shows+'</b><span>хотят показ</span></div>'
      + '<div class="stat"><b>'+st.showings+'</b><span>показов</span></div></div>'
    + '<div class="notif" style="margin-top:14px">📈 '+(st.shows? 'Есть запросы на просмотр — ведём к сделке.' : (st.likes? 'Есть заинтересованные — двигаемся к показам.' : 'Расширяем охват, ждём первые отклики.'))+'</div>'
    + '<div class="share"><div class="sub">Ссылка для собственника</div><div class="linkrow" style="margin-top:6px"><input readonly value="'+esc(url)+'"><button class="btn sm" onclick="copyOwnerLink(\''+o.id+'\')">Копировать</button></div></div></div>';
}
function copyOwnerLink(id){ var url=location.origin+location.pathname+'?owner='+id; if(navigator.clipboard&&navigator.clipboard.writeText){ navigator.clipboard.writeText(url).then(function(){toast('Ссылка скопирована');},function(){toast('Скопируй вручную: '+url);}); } else toast('Скопируй вручную: '+url); }

/* ----- shell ----- */
function go(screen){ ui.calc=false; ui.ownerView=null; ui.screen=screen; if(screen!=='dashboard') ui.podborka=null; render(); }
function setRole(r){ ui.role=r; ui.calc=false; ui.ownerView=null; if(r==='agent' && !ui.screen) ui.screen='objects'; render(); }
function render(){
  document.getElementById('topbar').innerHTML =
    '<div class="brand">🏠 КвартираБот<span class="proto">прототип</span></div>'
    + '<div class="seg"><button class="'+(ui.role==='agent'?'on':'')+'" onclick="setRole(\'agent\')">Риелтор</button>'
    + '<button class="'+(ui.role==='client'?'on':'')+'" onclick="setRole(\'client\')">Клиент</button></div>';
  var tab = document.getElementById('tabbar');
  if(ui.ownerView){ tab.style.display='none'; return screenOwner(); }
  if(ui.calc){ tab.style.display='none'; return screenCalc(); }
  if(ui.role==='agent'){
    tab.style.display='flex';
    var onObj = (ui.screen==='objects' || ui.screen==='addObject');
    var onCli = (ui.screen==='clients' || ui.screen==='clientDetail');
    var onShow = (ui.screen==='showings');
    var onPod = (!onObj && !onCli && !onShow);
    tab.innerHTML = '<button class="'+(onObj?'on':'')+'" onclick="go(\'objects\')">🏢 Объекты</button>'
      + '<button class="'+(onCli?'on':'')+'" onclick="go(\'clients\')">👥 Клиенты</button>'
      + '<button class="'+(onPod?'on':'')+'" onclick="go(\'podborki\')">📋 Подборки</button>'
      + '<button class="'+(onShow?'on':'')+'" onclick="go(\'showings\')">📅 Показы</button>';
    if(ui.screen==='addObject') screenAddObject();
    else if(ui.screen==='clients') screenClients();
    else if(ui.screen==='clientDetail') screenClientDetail();
    else if(ui.screen==='podborki') screenPodborki();
    else if(ui.screen==='newPodborka') screenNewPodborka();
    else if(ui.screen==='dashboard') screenDashboard();
    else if(ui.screen==='showings') screenShowings();
    else screenObjects();
  } else {
    tab.style.display='none';
    screenClient();
  }
}

var tg = window.Telegram && window.Telegram.WebApp;
if(tg){ try{ tg.ready(); tg.expand(); }catch(e){} }
try{
  var q = new URLSearchParams(location.search);
  var pp = q.get('p');
  if(pp && pod(pp)){ ui.role='client'; ui.client=pp; ui.ci=0; }
  if(q.get('calc')){ ui.calc=true; }
  var ow = q.get('owner');
  if(ow && obj(ow)){ ui.ownerView=ow; }
}catch(e){}
render();
</script>
</body>
</html>
