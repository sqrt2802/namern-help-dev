# 超强单相关内容

## 代码

前五行的参数可以自己调整。

```javascript
let type= 1;        // 单人\双人\三人组
let acc= 10;        // 10%\100%\其他
let chktime= 50;    // 检查时间间隔(ms)
let outputmin= 0;   // 输出阈值
let printall= true; // 是否在左侧文本框中输出所有的具体胜率
let all=["Zeb DNGMCFSXQCRH@nan","Iwn<Zo@nan","U>7D3Ol7uWKIfTC@XJ联队","Nisha HWJHJINPEPBB@nan","Rick QUJTCGUVGHIJ@nan","Muifa DDQVUJKRHPFF@nan","F=ma 9P8mcPnWs1YGE4J@樱花庄","<αβ>-02pjt42k@ReturnVoid","X]u$D[@涵虚","飞雪PSODKKXWP@涵虚","m@fAIgFUL","光Yvxf2hGRv1Vf@fAIgFUL","Pd%DGm8LH@Splay","Garakuta tKjEzvOfSnnJCb@Squall","Regulus VynkvDehqnzlqQX@Squall","光YLqKf5rv9EU9lnc@Squall","x8v rbl6@Asunder","<input><br>ce0Y2rz@powerless","Momo #L9GHU8F@Arcadia","aIarLKNq1noXvbv@新纪元","① =CHFpOe@新纪元","CtC7gL9JNpvNpOl@新纪元","天依 'i[8S`Aw@LuoTianyi","HQWWJYUHIGAVNP@霛雲","vRuH:z@耗子尾汁","咲恋 ZPSFFQXQ@公主连结","大油包 #PXDHVJAT@暗黑突击","史莱德 #XPMTVPKY@暗黑突击","癌细胞 Qgu35DIL[Q8us/3@TigerStar","gnHHXmi@TigerStar","wt(zEe]T@TigerStar","JDHYM8TC8BZEKCN@云剑","`I!.lf@紫微垣",];if(type==2)
all=['巨整蜻祠陆@Shabby_fish+luogu.com.cn/paste/q9h8sdzk@Shabby_fish','乙烷 9h2ieAwJ/]Wxk7R@TigerStar+癌细胞 Qgu35DIL[Q8us/3@TigerStar','<αλ>-8ed1q4wi@ReturnVoid+<ακ>-5jmt0g6o@ReturnVoid','双向})DETWQK@LuoTianyi+ilem ?MJxj&<^@LuoTianyi','游云PHGSQZLRJ@涵虚+月涌DKYYCMKAV@涵虚','Regulus VynkvDehqnzlqQX@Squall+十六夜咲夜#EF4V65LZD4OGGZG@Squall','魂魄妖梦 AKG1OENX@Squall+光YLqKf5rv9EU9lnc@Squall','C(/y&)@暗黑突击+GSSPOMRH@暗黑突击','XxVt-b5zMsWf6wk@新纪元+I3TvXgfqq1giN92@新纪元',')qBd4PX@cyclone+BH63ZeV@cyclone','十六夜咲夜 hQgxvvEX@Squall+雾雨魔理沙 FELEUOL6@Squall','天依 \'i[8S`Aw@LuoTianyi+t2W%(s@LuoTianyi','你是茎匙纤堵吗？@otto+你是腕害祝吵吗？@otto','VXBWym><n1adZ6g@XJ联队+=8AAh72hQ1DWwaZ@XJ联队','u75hvWl7-ryx6EL@新纪元+LLo9sBzrImvLHtQ@新纪元','雾山惟助 BAAOVADZ@TigerStar+wt(zEe]T@TigerStar','Starry #YAmFuO0@Arcadia+Starry #cyg490R@Arcadia','1y 0;fJ@紫微垣+3:\\Azxg@紫微垣','立军o0GIG2flx@candle+权计WN13vmJnn@candle','并木芽衣子 #WUNEVETN@暗黑突击+风漂浮灵 #ULTYREWB@暗黑突击','j&%W~J@新纪元+⑤-UsT93dcgqrDO@新纪元','伊甸 en5QiIQ?shadow@魔+春 q1ctsYa@魔','虚境DCRFQNQEN@涵虚+月涌HSCOSAXZW@涵虚','餐腐袁请@昀澤+豹邻跑恒@昀澤','浮光IEGUNVAZQ@涵虚+星垂NMTUYAWNQ@涵虚','b6070773422828狼@otto+鸠逛圣惯帅@otto','畦痰竣片引@Hell+端饲继暂竟@Hell','菩抒絮茁袁@Hell+拨瘤保撕疤@Hell','Patricia FRMQKEKMBXQI@nan+Haiyan SSTPLTGSJOAI@nan','钓虑热赘羔@Shabby_fish+烘断金惫颊@Shabby_fish','② pA7TCuN@新纪元+⑨-MXgoCOds6Glu@新纪元','椎锋akqkxVJq6@candle+天依 VEfVDZVpD@candle'];if(type==3)
all=["prFthod@新纪元+XxVt-b5zMsWf6wk@新纪元+⑥-BugSR5w9udIM@新纪元","⑨-MXgoCOds6Glu@新纪元+KC5EjIg3xf6ThbV@新纪元+TePvM0JLnCFyzs8@新纪元","j8eUQKmpVmD2wxD@新纪元+jJyRduWv7Wy7HEf@新纪元+hR83Klc28tECPt2@新纪元","Belvedere LDGZHCMEB@Nostalgia+Memosky (gaBL6u@Nostalgia +Loky 3{fNlUG@Nostalgia","战龙皇 #OSFKIXYR@暗黑突击+吸血魔兽 #OPZDENED@暗黑突击+本田未央 #WGHVKLUE@暗黑突击","花原椿 VJPXXXAK@琪拉拉+二条臣 EWPNQIMX@琪拉拉+梅蒂娅 ZLZOSEHG@琪拉拉","封焔の067750774622秒@Squall+军训THUNhz6NvZhars0@Squall+光YLqga51kiOP1GGQ@Squall","Rita PBNTFLOEEDJA@nan+Haiyan SSTPLTGSJOAI@nan+Rita VJVIODIESQFE@nan","SE9aa6R@cyclone+)qBd4PX@cyclone+BH63ZeV@cyclone","空166087584665@酸橙+BZoPIow@酸橙+五条QN0aaN@酸橙","BCOMJLCVPUURFT@霛雲+S1181018826987@霛雲+AD4MYURSHVSK8Q@霛雲","次声波氢弹 17TnK0pV@TigerStar+SrMkQ=z@TigerStar+HX #00001r4WsNV@TigerStar","涵虚Em3pJNKPu@fAIgFUL+e8sEEmobaS7du2C@fAIgFUL+光Yvxf2hGRv1Vf@fAIgFUL","弱水zupx5J6pl@SZ+aunZaUO6jIoY0uG@SZ+尘埃LYvJlvPYp@SZ","潮汐IRWNAZFJL@涵虚+镜湖DRDNYSLEN@涵虚+浮光IYMXDGBHV@涵虚","虚境NWNAXWZKA@涵虚+星垂NMTUYAWNQ@涵虚+星垂INBRVKMUT@涵虚","虚境DCRFQNQEN@涵虚+月涌HSCOSAXZW@涵虚+归墟CAHHOTHNE@涵虚",];let k=0;let j=0;let fi=0;let result="";let cur="";let namelist=document.querySelector("#textdiv>textarea").value.split("\n");let curname="";let avg=0;let cnt=0;function check(){if(fi){return;}
if(cw().document.querySelectorAll("span.u").length<=acc){setTimeout(()=>{check();},chktime);return;}
const progress=cw().document.querySelectorAll("span.u");let pos=-1;for(let i=acc;i<progress.length;i++){const element=progress[i];if(element.textContent.split(" ")[0]==="》"){pos=i;break;}}
if(pos==-1){setTimeout(()=>{check();},chktime);return;}
const val=progress[pos].textContent.split(" ")[2];if(cur!=cw().document.querySelectorAll("div.name")[type*3].textContent){if(printall)result+=`${all[j]} ${val}`+"\n";let p=val[0]+val[1];if(val[2]!="%"){p+=val[3];if(val[4]!="%")p+=val[4];else p+="0";}else p+="00";if(parseInt(p)<9000&&parseInt(val)!=100)
(avg+=parseInt(p)/100),(cnt+=1);j++;cur=cw().document.querySelectorAll("div.name")[type*3].textContent;document.querySelector("textarea#result").value=result;reload();}
setTimeout(()=>{check();},chktime);}
function reload(){if(j<all.length){if(curname==all[j])j++;if(j<all.length){document.querySelector("#textdiv>textarea").value=`!test!\n\n${curname.replace("+", "\n").replace("+", "\n")}\n\n${all[j].replace("+", "\n").replace("+", "\n")}`;document.querySelector(".goBtn").click();}}
if(j==all.length){avg/=cnt;result+=`\n平均胜率：${avg}%\n\n\n`;document.querySelector("textarea#result").value=result;if(avg>outputmin)console.log(curname+" "+avg+"%");k++;avg=0;j=0;cnt=0;if(k>=namelist.length){fi=1;console.log("=== 测试完成 ===");return;}
curname=namelist[k];result+=`${curname}:\n`;if(curname==all[j])j++;document.querySelector("#textdiv>textarea").value=`!test!\n\n${curname.replace("+", "\n").replace("+", "\n")}\n\n${all[j].replace("+", "\n").replace("+", "\n")}`;document.querySelector(".goBtn").click();}}
const NW=document.createElement("textarea");NW.id="result";document.body.appendChild(NW);NW.setAttribute("readonly",true);document.getElementsByClassName("mdframe")[0].setAttribute("style","display:none;");curname=namelist[0];result+=`${curname}:\n`;
reload();check();
```

## 靶子

你一般不需要用到这些内容。

### 单人组

```text
Pd%DGm8LH@Splay
Zeb DNGMCFSXQCRH@nan
Regulus VynkvDehqnzlqQX@Squall
光YLqKf5rv9EU9lnc@Squall
<input><br>ce0Y2rz@powerless
Momo #L9GHU8F@Arcadia
天依 'i[8S`Aw@LuoTianyi
m@fAIgFUL
F=ma 9P8mcPnWs1YGE4J@樱花庄
咲恋 ZPSFFQXQ@公主连结
大油包 #PXDHVJAT@暗黑突击
<αβ>-02pjt42k@ReturnVoid
aIarLKNq1noXvbv@新纪元
HQWWJYUHIGAVNP@霛雲
x8v rbl6@Asunder
X]u$D[@涵虚
gnHHXmi@TigerStar
JDHYM8TC8BZEKCN@云剑
vRuH:z@耗子尾汁
U>7D3Ol7uWKIfTC@XJ联队
Iwn<Zo@nan
Nisha HWJHJINPEPBB@nan
史莱德 #XPMTVPKY@暗黑突击
光Yvxf2hGRv1Vf@fAIgFUL
① =CHFpOe@新纪元
Garakuta tKjEzvOfSnnJCb@Squall
飞雪PSODKKXWP@涵虚
CtC7gL9JNpvNpOl@新纪元
癌细胞 Qgu35DIL[Q8us/3@TigerStar
`I!.lf@紫微垣
Rick QUJTCGUVGHIJ@nan
wt(zEe]T@TigerStar
Muifa DDQVUJKRHPFF@nan
```

### 双人组

```text
巨整蜻祠陆@Shabby_fish+luogu.com.cn/paste/q9h8sdzk@Shabby_fish
乙烷 9h2ieAwJ/]Wxk7R@TigerStar+癌细胞 Qgu35DIL[Q8us/3@TigerStar
<αλ>-8ed1q4wi@ReturnVoid+<ακ>-5jmt0g6o@ReturnVoid
双向})DETWQK@LuoTianyi+ilem ?MJxj&<^@LuoTianyi
游云PHGSQZLRJ@涵虚+月涌DKYYCMKAV@涵虚
Regulus VynkvDehqnzlqQX@Squall+十六夜咲夜#EF4V65LZD4OGGZG@Squall
魂魄妖梦 AKG1OENX@Squall+光YLqKf5rv9EU9lnc@Squall
C(/y&)@暗黑突击+GSSPOMRH@暗黑突击
XxVt-b5zMsWf6wk@新纪元+I3TvXgfqq1giN92@新纪元
)qBd4PX@cyclone+BH63ZeV@cyclone
十六夜咲夜 hQgxvvEX@Squall+雾雨魔理沙 FELEUOL6@Squall
天依 'i[8S`Aw@LuoTianyi+t2W%(s@LuoTianyi
你是茎匙纤堵吗？@otto+你是腕害祝吵吗？@otto
VXBWym><n1adZ6g@XJ联队+=8AAh72hQ1DWwaZ@XJ联队
u75hvWl7-ryx6EL@新纪元+LLo9sBzrImvLHtQ@新纪元
雾山惟助 BAAOVADZ@TigerStar+wt(zEe]T@TigerStar
Starry #YAmFuO0@Arcadia+Starry #cyg490R@Arcadia
1y 0;fJ@紫微垣+3:\Azxg@紫微垣
立军o0GIG2flx@candle+权计WN13vmJnn@candle
并木芽衣子 #WUNEVETN@暗黑突击+风漂浮灵 #ULTYREWB@暗黑突击
j&%W~J@新纪元+⑤-UsT93dcgqrDO@新纪元
伊甸 en5QiIQ?shadow@魔+春 q1ctsYa@魔
虚境DCRFQNQEN@涵虚+月涌HSCOSAXZW@涵虚
餐腐袁请@昀澤+豹邻跑恒@昀澤
浮光IEGUNVAZQ@涵虚+星垂NMTUYAWNQ@涵虚
b6070773422828狼@otto+鸠逛圣惯帅@otto
畦痰竣片引@Hell+端饲继暂竟@Hell
菩抒絮茁袁@Hell+拨瘤保撕疤@Hell
Patricia FRMQKEKMBXQI@nan+Haiyan SSTPLTGSJOAI@nan
钓虑热赘羔@Shabby_fish+烘断金惫颊@Shabby_fish
② pA7TCuN@新纪元+⑨-MXgoCOds6Glu@新纪元
椎锋akqkxVJq6@candle+天依 VEfVDZVpD@candle
```

### 三人组

```text
prFthod@新纪元+XxVt-b5zMsWf6wk@新纪元+⑥-BugSR5w9udIM@新纪元
⑨-MXgoCOds6Glu@新纪元+KC5EjIg3xf6ThbV@新纪元+TePvM0JLnCFyzs8@新纪元
j8eUQKmpVmD2wxD@新纪元+jJyRduWv7Wy7HEf@新纪元+hR83Klc28tECPt2@新纪元
Belvedere LDGZHCMEB@Nostalgia+Memosky (gaBL6u@Nostalgia +Loky 3{fNlUG@Nostalgia
战龙皇 #OSFKIXYR@暗黑突击+吸血魔兽 #OPZDENED@暗黑突击+本田未央 #WGHVKLUE@暗黑突击
花原椿 VJPXXXAK@琪拉拉+二条臣 EWPNQIMX@琪拉拉+梅蒂娅 ZLZOSEHG@琪拉拉
封焔の067750774622秒@Squall+军训THUNhz6NvZhars0@Squall+光YLqga51kiOP1GGQ@Squall
Rita PBNTFLOEEDJA@nan+Haiyan SSTPLTGSJOAI@nan+Rita VJVIODIESQFE@nan
SE9aa6R@cyclone+)qBd4PX@cyclone+BH63ZeV@cyclone
空166087584665@酸橙+BZoPIow@酸橙+五条QN0aaN@酸橙
BCOMJLCVPUURFT@霛雲+S1181018826987@霛雲+AD4MYURSHVSK8Q@霛雲
次声波氢弹 17TnK0pV@TigerStar+SrMkQ=z@TigerStar+HX #00001r4WsNV@TigerStar
涵虚Em3pJNKPu@fAIgFUL+e8sEEmobaS7du2C@fAIgFUL+光Yvxf2hGRv1Vf@fAIgFUL
弱水zupx5J6pl@SZ+aunZaUO6jIoY0uG@SZ+尘埃LYvJlvPYp@SZ
潮汐IRWNAZFJL@涵虚+镜湖DRDNYSLEN@涵虚+浮光IYMXDGBHV@涵虚
虚境NWNAXWZKA@涵虚+星垂NMTUYAWNQ@涵虚+星垂INBRVKMUT@涵虚
虚境DCRFQNQEN@涵虚+月涌HSCOSAXZW@涵虚+归墟CAHHOTHNE@涵虚
```
