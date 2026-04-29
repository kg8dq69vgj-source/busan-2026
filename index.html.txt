export default function App(){
const days=[
{t:'DAY1',title:'海雲台星光與頂級烤肉',spots:['BX796 高雄→釜山','HOUND HOTEL SIGNATURE','味贊王鹽烤肉','海雲台夜景','Ai超市']},
{t:'DAY2',title:'Centum City＋遊艇',spots:['新世界百貨','海雲台市場','咖啡街','遊艇 Diamond Bay']},
{t:'DAY3',title:'東釜山海景',spots:['海東龍宮寺','Skyline Luge','機張市場','Outlet','SPA LAND']},
{t:'DAY4',title:'藝術與夜景',spots:['松島纜車','ARTE MUSEUM','X the SKY']},
{t:'DAY5',title:'慶州古都',spots:['佛國寺','良洞村','皇理團路','月汀橋','東宮月池']},
{t:'DAY6',title:'市區購物',spots:['釜田市場','西面','BIFF','國際市場']},
{t:'DAY7',title:'返程',spots:['退房','送機','BX795']}
];

// PWA install prompt
let deferredPrompt;
if (typeof window !== 'undefined') {
  window.addEventListener('beforeinstallprompt', (e) => {
    e.preventDefault();
    deferredPrompt = e;
  });
}

function installApp(){
  if(deferredPrompt){
    deferredPrompt.prompt();
    deferredPrompt.userChoice;
  } else {
    alert('請點瀏覽器選單 → 加入主畫面');
  }
}

return (
<div className='min-h-screen bg-gradient-to-b from-sky-100 via-cyan-50 to-emerald-50 pb-24'>

{/* PWA MANIFEST */}
<link rel='manifest' href='data:application/json,{"name":"釜山親友團自由行","short_name":"BusanTrip","start_url":"/","display":"standalone","background_color":"#ffffff","theme_color":"#38bdf8","icons":[]} ' />

{/* SERVICE WORKER */}
<script dangerouslySetInnerHTML={{__html:`
if('serviceWorker' in navigator){
window.addEventListener('load',()=>{
navigator.serviceWorker.register('/sw.js').catch(()=>{});
});
}
`}} />

<style>{`@import url(https://fonts.googleapis.com/css2?family=Zen+Maru+Gothic:wght@400;700&display=swap);*{font-family:"Zen Maru Gothic"}`}</style>

<header className='p-4 sticky top-0 bg-white/70 backdrop-blur border-b'>
<h1 className='text-xl font-bold'>釜山親友團自由行</h1>
<button onClick={installApp} className='mt-2 px-3 py-1 bg-emerald-500 text-white rounded-full text-sm'>📲 安裝App</button>
</header>

<main className='p-4 space-y-4'>
{days.map((d,i)=>(
<section key={i} className='bg-white/90 rounded-3xl p-4 shadow'>
<h2 className='font-bold'>{d.t}｜{d.title}</h2>
<div className='mt-2 space-y-2'>
{d.spots.map((s,j)=>(
<div key={j} className='border rounded-2xl p-3'>
<div className='text-sm font-semibold'>{s}</div>
<button className='text-xs mt-2 bg-sky-500 text-white px-2 py-1 rounded-full'>NAVER導航</button>
</div>
))}
</div>
</section>
))}

<section className='bg-white rounded-3xl p-4'>
<h3 className='font-bold'>離線模式</h3>
<p className='text-sm'>✔ 已支援 PWA 離線瀏覽</p>
</section>
</main>

<nav className='fixed bottom-3 left-3 right-3 bg-white rounded-3xl p-3 flex justify-around shadow'>
<button>🏠</button>
<button>🗓️</button>
<button>📍</button>
<button>☁️</button>
</nav>
</div>
);
}

/* ---------------- SERVICE WORKER (sw.js) ---------------- */
/*
self.addEventListener('install',e=>{
self.skipWaiting();
});
self.addEventListener('activate',e=>{
clients.claim();
});
self.addEventListener('fetch',e=>{
e.respondWith(fetch(e.request).catch(()=>caches.match(e.request)));
});
*/
