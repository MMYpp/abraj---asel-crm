
HTML

<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#123d32">
<title>CRM ابراج الاصیل</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#f2f5f3;font-family:Tahoma,Arial;color:#24352e}
header{background:#123d32;color:white;padding:22px 15px;text-align:center}
header h2{margin:0 0 8px}
nav{display:flex;flex-wrap:wrap;background:#fff;gap:5px;padding:9px;position:sticky;top:0}
button{border:0;border-radius:7px;padding:11px;background:#176b50;color:white;font-weight:bold;cursor:pointer}
nav button{flex:1;background:#e2eee8;color:#174b38}
nav button.active{background:#176b50;color:white}
main{padding:14px;max-width:750px;margin:auto}
.card{background:white;border-radius:12px;padding:15px;margin:12px 0;box-shadow:0 2px 8px #0001}
input,select,textarea{width:100%;padding:12px;margin:6px 0 12px;border:1px solid #ccd8d1;border-radius:7px;font-family:inherit}
label{font-size:13px;font-weight:bold}
h3{color:#176b50}
.item{border:1px solid #dce6df;padding:12px;border-radius:8px;margin:9px 0}
.item p{margin:7px 0;font-size:14px}
.danger{background:#a52d2d}
.secondary{background:#52665d}
.hidden{display:none}
.stat{font-size:23px;font-weight:bold;color:#176b50}
</style>
</head>
<body>
<header>
<h2>دفتر رهنمای معاملات</h2>
<strong>ابراج الاصیل</strong>
<p>سیستم مدیریت املاک و مشتریان</p>
</header>
<nav>
<button class="active" onclick="show('home',this)">خانه</button>
<button onclick="show('property',this)">ثبت ملک</button>
<button onclick="show('customer',this)">ثبت مشتری</button>
<button onclick="show('accounts',this)">حساب‌ها</button>
<button onclick="show('match',this)">تطبیق</button>
<button onclick="show('backup',this)">پشتیبان</button>
</nav>
<main>
<section id="home">
<div class="card">
<h3>خوش آمدید</h3>
<p>مدیریت معاملات دفتر ابراج الاصیل</p>
</div>
<div class="card">
تعداد املاک
<div class="stat" id="pc">۰</div>
</div>
<div class="card">
تعداد مشتریان
<div class="stat" id="cc">۰</div>
</div>
<div class="card">
<h3>آخرین املاک ثبت‌شده</h3>
<div id="recent"></div>
</div>
</section>

<section id="property" class="hidden">
<div class="card">
<h3>ثبت ملک جدید</h3>
<label>نام مالک</label><input id="owner">
<label>شماره تماس مالک</label><input id="ownerPhone" placeholder="07XXXXXXXX">
<label>نوع ملک</label>
<select id="ptype"><option>زمین</option><option>خانه</option><option>آپارتمان</option><option>دوکان</option><option>باغ</option><option>سایر</option></select>
<label>موقعیت و ناحیه</label><input id="location">
<label>مساحت به متر مربع</label><input id="area" type="number">
<label>قیمت به افغانی</label><input id="price" type="number">
<label>مشخصات ملک</label><textarea id="details"></textarea>
<label>وضعیت</label>
<select id="status"><option>فروشی</option><option>کرایی</option><option>بیع وفا</option><option>فروخته شد</option></select>
<button onclick="addProperty()">ثبت ملک</button>
</div>
<div class="card"><h3>فهرست املاک</h3><input id="ps" placeholder="جست‌وجو..." oninput="render()"><div id="plist"></div></div>
</section>

<section id="customer" class="hidden">
<div class="card">
<h3>ثبت مشتری جدید</h3>
<label>نام مشتری</label><input id="cname">
<label>شماره تماس</label><input id="cphone" placeholder="07XXXXXXXX">
<label>نوع درخواست</label><select id="need"><option>خرید زمین</option><option>خرید خانه</option><option>کرایه خانه</option><option>خرید دوکان</option><option>بیع وفا</option><option>سایر</option></select>
<label>بودجه به افغانی</label><input id="budget" type="number">
<label>موقعیت مورد نظر</label><input id="clocation">
<label>توضیحات</label><textarea id="cnote"></textarea>
<button onclick="addCustomer()">ثبت مشتری</button>
</div>
<div class="card"><h3>فهرست مشتریان</h3><input id="cs" placeholder="جست‌وجو..." oninput="render()"><div id="clist"></div></div>
</section>

<section id="accounts" class="hidden">
<div class="card">
<h3>ثبت حساب و کمیسیون</h3>
<label>نام شخص</label><input id="aname">
<label>نوع حساب</label><select id="atype"><option>کمیسیون دریافتی</option><option>کمیسیون طلب</option><option>بدهکاری</option><option>پرداخت</option></select>
<label>مبلغ به افغانی</label><input id="amount" type="number">
<label>توضیحات</label><textarea id="anote"></textarea>
<button onclick="addAccount()">ثبت حساب</button>
</div>
<div class="card"><h3>گزارش حساب‌ها</h3><div id="alist"></div></div>
</section>

<section id="match" class="hidden">
<div class="card">
<h3>تطبیق مشتری با ملک</h3>
<p>مشتری و املاک را بر اساس نوع درخواست، بودجه و موقعیت مقایسه می‌کنیم.</p>
<button onclick="matchNow()">شروع تطبیق</button>
<div id="matches"></div>
</div>
</section>

<section id="backup" class="hidden">
<div class="card">
<h3>پشتیبان اطلاعات</h3>
<p>برای جلوگیری از ضایع‌شدن اطلاعات، مرتباً نسخه پشتیبان بگیرید.</p>
<button onclick="backup()">دانلود نسخه پشتیبان</button>
<hr>
<label>بازیابی نسخه پشتیبان</label>
<input type="file" id="restoreFile" accept=".json">
<button onclick="restore()">بازیابی اطلاعات</button>
</div>
</section>
</main>

<script>
const get=k=>JSON.parse(localStorage.getItem(k)||"[]");
const save=(k,v)=>localStorage.setItem(k,JSON.stringify(v));
let properties=get("properties"),customers=get("customers"),accounts=get("accounts");

function show(id,b){
document.querySelectorAll("main section").forEach(s=>s.classList.add("hidden"));
document.getElementById(id).classList.remove("hidden");
document.querySelectorAll("nav button").forEach(x=>x.classList.remove("active"));
b.classList.add("active");render();
}
function val(id){return document.getElementById(id).value.trim()}
function addProperty(){
if(!val("owner")||!val("price"))return alert("نام مالک و قیمت را وارد کنید");
properties.unshift({id:Date.now(),owner:val("owner"),phone:val("ownerPhone"),type:val("ptype"),location:val("location"),area:val("area"),price:+val("price"),details:val("details"),status:val("status")});
save("properties",properties);alert("ملک ثبت شد");
["owner","ownerPhone","location","area","price","details"].forEach(x=>document.getElementById(x).value="");render();
}
function addCustomer(){
if(!val("cname"))return alert("نام مشتری را وارد کنید");
customers.unshift({id:Date.now(),name:val("cname"),phone:val("cphone"),need:val("need"),budget:+val("budget"),location:val("clocation"),note:val("cnote")});
save("customers",customers);alert("مشتری ثبت شد");
["cname","cphone","budget","clocation","cnote"].forEach(x=>document.getElementById(x).value="");render();
}
function addAccount(){
if(!val("aname")||!val("amount"))return alert("نام و مبلغ را وارد کنید");
accounts.unshift({name:val("aname"),type:val("atype"),amount:+val("amount"),note:val("anote")});
save("accounts",accounts);alert("حساب ثبت شد");
["aname","amount","anote"].forEach(x=>document.getElementById(x).value="");render();
}
function removeItem(type,id){
if(!confirm("آیا از حذف مطمئن هستید؟"))return;
if(type==="p")properties=properties.filter(x=>x.id!==id);
if(type==="c")customers=customers.filter(x=>x.id!==id);
save("properties",properties);save("customers",customers);render();
}
function shareItem(x){
let s=Object.entries(x).map(([k,v])=>k+": "+v).join("\n");
if(navigator.share)navigator.share({text:s}).catch(()=>{});
else{let t=document.createElement("textarea");t.value=s;document.body.appendChild(t);t.select();document.execCommand("copy");t.remove();alert("اطلاعات کپی شد");}
}
function render(){
document.getElementById("pc").textContent=properties.length;
document.getElementById("cc").textContent=customers.length;
document.getElementById("recent").innerHTML=properties.slice(0,4).map(p=>`<p>${p.type} - ${p.location} - ${p.price.toLocaleString("en-US")} افغانی</p>`).join("")||"هنوز ملکی ثبت نشده است";
let q=(document.getElementById("ps")?.value||"").toLowerCase();
document.getElementById("plist").innerHTML=properties.filter(p=>Object.values(p).join(" ").toLowerCase().includes(q)).map(p=>`<div class="item"><b>${p.type} | ${p.location}</b><p>مالک: ${p.owner} | تماس: ${p.phone}</p><p>مساحت: ${p.area} متر | قیمت: ${p.price.toLocaleString("en-US")} افغانی</p><p>وضعیت: ${p.status}</p><p>${p.details}</p><button onclick="shareItem(properties.find(x=>x.id===${p.id}))">اشتراک</button> <button class="danger" onclick="removeItem('p',${p.id})">حذف</button></div>`).join("")||"ملکی یافت نشد";
let c=(document.getElementById("cs")?.value||"").toLowerCase();
document.getElementById("clist").innerHTML=customers.filter(x=>Object.values(x).join(" ").toLowerCase().includes(c)).map(x=>`<div class="item"><b>${x.name}</b><p>تماس: ${x.phone}</p><p>درخواست: ${x.need}</p><p>بودجه: ${x.budget.toLocaleString("en-US")} افغانی</p><p>موقعیت: ${x.location}</p><button onclick="shareItem(customers.find(y=>y.id===${x.id}))">اشتراک</button> <button class="danger" onclick="removeItem('c',${x.id})">حذف</button></div>`).join("")||"مشتری یافت نشد";
document.getElementById("alist").innerHTML=accounts.map(a=>`<div class="item"><b>${a.name}</b><p>${a.type}: ${a.amount.toLocaleString("en-US")} افغانی</p><p>${a.note}</p></div>`).join("")||"حسابی ثبت نشده است";
}
function matchNow(){
let out=[];
customers.forEach(c=>properties.forEach(p=>{
let typeMatch=(c.need.includes("زمین")&&p.type==="زمین")||(c.need.includes("خانه")&&p.type==="خانه")||(c.need.includes("دوکان")&&p.type==="دوکان")||(c.need.includes("بیع")&&p.status==="بیع وفا")||c.need==="سایر";
let budgetMatch=!c.budget||p.price<=c.budget;
let locMatch=!c.location||!p.location||p.location.includes(c.location)||c.location.includes(p.location);
if(typeMatch&&budgetMatch&&locMatch&&p.status!=="فروخته شد")out.push(`<div class="item"><b>${c.name}</b> ← ${p.type} در ${p.location}<p>قیمت: ${p.price.toLocaleString("en-US")} افغانی</p></div>`);
}));
document.getElementById("matches").innerHTML=out.join("")||"تطبیق مناسبی پیدا نشد.";
}
function backup(){
let data={properties,customers,accounts};
let blob=new Blob([JSON.stringify(data,null,2)],{type:"application/json"});
let a=document.createElement("a");a.href=URL.createObjectURL(blob);a.download="abraj-crm-backup.json";a.click();URL.revokeObjectURL(a.href);
}
function restore(){
let f=document.getElementById("restoreFile").files[0];if(!f)return alert("فایل را انتخاب کنید");
let r=new FileReader();r.onload=()=>{try{let d=JSON.parse(r.result);properties=d.properties||[];customers=d.customers||[];accounts=d.accounts||[];save("properties",properties);save("customers",customers);save("accounts",accounts);render();alert("اطلاعات بازیابی شد");}catch(e){alert("فایل معتبر نیست")}};r.readAsText(f);
}
render();
</script>
</body>
</html>
