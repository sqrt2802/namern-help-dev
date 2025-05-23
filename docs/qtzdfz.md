可以作为教程的一部分，也可以作为附录。但是不会像教程写得那么详细。

算是一个前辈传授的一点心得，不用全信，也不一定全部正确。大概会将从测号、开箱到配队的整个流程的相关经验，每个人有每个人自己的方法，也不一定要全听我的。

**需要明白的一点，不要小看配队，配队花太长时间浪费配队时间，配队花太少时间浪费测号时间！**

相关新工具（教程里没有提及到的）：pbb 测号器，xp-convert.zip，two.cpp。都可以去群文件里下载。

以及你最好有能力写一些简单的代码/脚本。

简写：测 111% cqp 的意思是，先测 1% cqp，将过阈值的二人组提出来，测 10% cqp，再将过阈值的组提出来，测 100% cqp。两个阈值可能不一样。

## 新工具介绍

### pbb 测号器

现在主要由我本人维护，强烈推荐。个人认为引导也很详尽了，应该不会有看不懂的。下载的时候直接下载那个 pbb-pack.zip。

### xp-convert.zip

将 xp 和 convert 的网页版代码进行 c++ 的改写。这样在测大量号的时候不会卡住。同时还有 diy-convert 的选项，和 [namerena diy](https://85d75eca.fast-namerena.pages.dev/branch/latest/) 的格式是适配的，方便对号进行属性、熟练度的修改等测改后的评分等。

用法：在同目录下叫做 `input.txt` 的文件里输入号，（因为我写的代码的判定的原因）最后一个号后面需要换行。运行 `xp.exe/convert.exe/sort-convert.exe/diy-convert.exe` 后会将结果输出在 `xp.txt/convert.txt/sort-convert.txt/diy-convert.txt` 中。

为了保证一定的自由度将 cpp 的源码也给出，可以自由修改。

附：https://85d75eca.fast-namerena.pages.dev/branch/latest/ 是 diy 网址。注意技能的顺序是不能随便改变的。

### two.cpp

一个 cpp 文件，用于将两个输入 `in1.txt` 和 `in2.txt` 里的号两两组合，输出加成达到一定标准的二人组。

为了保持高自由度，这个“一定标准”由你自己定，自己看代码的 `int check(Name &x,Name &y)` 部分。返回值默认虚评增量，可以改为是八围增量、熟练度增量、或者按照一定权重的八围、熟练度增量等。

在 main 函数里的 
```cpp
            int dt=check(name_list[0][i],name_list[1][j]);
            if (dt>200)
            {
                printf("%s+%s\n",name_list[0][i].NAME_SELF,name_list[1][j].NAME_SELF);
            }
```
意思是输出超过某个阈值的号。基本上只需要关注这两个地方就可以了。

这个程序默认是 `in1.txt` 和 `in2.txt` 中的号是两种不同类型的号，两者基本没有重复，然后进行两两配队。如果你需要在同种类型中进行两两配队，可以自己修改外面的 for 循环 和 `namelist[0/1][i/j]`。

### team_calc.html

一个用来直观测多人组加成的 html 文件。左侧输入一个多人组，右侧会显示加成后的各技能熟练度和变化量，以及对应的 diy 格式。


## 测号方面

推荐使用 pbb 测号器。方便一键多线程而且对顺序测号而言更加人性化，也更方便统计测号量。

pbb 测号器的八围相关阈值是内置曙光筛，就不需要你操心了。虚评和虚单阈值建议设低一点。如果感觉输出的号实在太多，采用不同技能不同阈值的方式。具体为，将虚评、虚单的阈值设得很低，输出大量号；改动虚评的源代码，无论你选择网页版虚评还是 cpp 版虚评都可以。这里给出我的一个例子：

```cpp
            if (score>=5300 || scoreQD>=5700) 
			{
				if ((FREQ[Map["潜行"]]<60 && FREQ[Map["净化"]]<60) || score>=5600 || scoreQD>=6300)
                {
					printf("%s %d %d",NAME_ALL,(int)score,(int)scoreQD);
                    if (FREQ[Map["铁壁"]]>=30) cout<<" !铁壁";
                    if (FREQ[Map["护盾"]]>=50) cout<<" !护盾";
                    if (FREQ[Map["铁壁"]]>=30 && FREQ[Map["护盾"]]>=1 && FREQ[Map["护盾"]]<=49) cout<<" !有盾";
                    if (FREQ[Map["幻术"]]>=50) cout<<" !幻术";
                    if (FREQ[Map["潜行"]]>=60) cout<<" !背刺";
                    if (FREQ[Map["净化"]]>=60) cout<<" !净化";
                    if (FREQ[Map["苏生"]]>=30) cout<<" !苏生";
                    if (FREQ[Map["地裂"]]>=50) cout<<" !地裂";
                    if (FREQ[Map["连击"]]>=50) cout<<" !连击";
                    if (FREQ[Map["加速"]]>=60) cout<<" !加速";
                    if (FREQ[Map["魅惑"]]>=50) cout<<" !魅惑";
                    if (FREQ[Map["护符"]]>=30) cout<<" !护符";
                    if (FREQ[Map["诅咒"]]>=60) cout<<" !诅咒";
                    if (FREQ[Map["瘟疫"]]>=60) cout<<" !瘟疫";
                    if (FREQ[Map["分身"]]>=20) cout<<" !分身";
                    if (FREQ[Map["吞噬"]]>=30) cout<<" !吞噬";
                    if (FREQ[Map["聚气"]]>=50) cout<<" !聚气";
                    if (FREQ[Map["火球"]]>=50) cout<<" !火球";
                    if (FREQ[Map["铁壁"]]<50 && FREQ[Map["地裂"]]<30 && FREQ[Map["连击"]]<50 && FREQ[Map["连击"]]+FREQ[Map["地裂"]]+FREQ[Map["铁壁"]]>=60) cout<<" !呃呃";
                    cout<<"\n";
                }
            }
```

这段代码表示，当号是净化号或背刺号（判断标准为熟练度）时阈值为 5600/6300，其他情况下阈值为 5300/5700。然后对于一些特殊的技能进行标识。

然后你可以将在这个条件下过阈值的号放进一个称为“垃圾堆”的地方。为什么称为“垃圾堆”，因为我是这么称呼的。里面有用的号的密度仍然很低，但是里面确实也有不少低强评强号。以及未来环境变了的时候，很有可能还需要在这些号里进行翻找。

不需要担心这垃圾堆的占空间的问题。真不如几张图片来得大吧。

## 开箱

开箱的频率随意，但是不建议超过一天一次。我个人比较特殊，我可能几个月才开一次箱（只有决定配队的时候才进行大规模开箱）。

如果选择和我一样屯很多号一起开，可以在每天测号中挑 xp xd 最高的几个测一测玩玩。如果一直没有出新号的感觉会憋得难受的。

## 配队

这里将我的开箱-配队流程一起说了。  

首先先开箱。我设的阈值是开垃圾堆里 xp 超过 5300 的号，qp 10% 超过 5600 的测 100%。100% 超过 5800，这样的号进入一个叫做“号库”的地方。

xd 超过 5700 的号开 10%，qd 10% 超过 6200 测 100%，qd 100% 超过 6500 进入一个叫做“单挑号库”的地方。6500 这个阈值其实有些过低，可以适当调高。

10% 超过 6200 的号集不要丢，拿去测 1% cqd。然后筛选出 46 以上的，测 10% cqd，筛选出 47 以上的，测 100% cqd。我的 100% cqd 榜单保留到 48 及以上。

---------------

然后是我认为最关键的一个步骤，二人组配队。我说一下我的步骤。  

首先确定你要配的二人组的类型，我一般会分为三个类型：辅助+背刺、常规无刺、双分身。  

常见二人组类型（详细）：  

辅助+背刺：包括 铁壁+背刺、地裂+背刺、连击+背刺、加速+背刺、减速+背刺、护符+背刺等。

常规无刺：包括 地裂 连击 瘟疫 诅咒 净化 铁壁等的两两组合。

双分身：包括 分身护符 分身魅惑 分身幻术 等的两两组合。

--------------

流程大概是这样的：

首先确定你要枚举的号库。我的背刺只在 5800 里枚举，辅助、常规无刺、双分身会在整个垃圾堆里枚举。  

如何使用垃圾堆？

建议是通过修改 xp 代码选择熟练度达标的号。建议“做加法”而不是“做减法”，意思是建议选出符合条件的号而不是剔除不符合条件的号剩下的枚举。

比如双分身我会选中所有分身熟练度大于 30 的号。辅助号会选出所有铁壁地裂连击加速减速护符达到熟练度阈值的号。

常规无刺，我的建议是选出垃圾堆里的地裂连击瘟疫诅咒，剩下的选出 5800 除了背刺以外的所有号。

--------------

但是直接枚举这么多二人组显然太多了，是不可接受的。我们需要一定的标准进行筛选。首先明确，肯定不能直接用强评来作为强度的一个标识。因此，我采用了，借助一个基准号，与这个基准号组成二人组测 cqp，将得到的结果作为某个类型的号的强度标识的方法。这个方法应该由我首创。

举例：我想测我的辅助号 `蓬莱山辉夜 8CELMML9@Squall` 和 `江Ebd5Oo7oitb5@Squall` 的强度，那我就找一个背刺基准，如 `Wispy #6uttTRg@Arcadia`，测 1% cqp。

结果为：
```txt
50.471875  蓬莱山辉夜 8CELMML9@Squall+Wispy #6uttTRg@Arcadia
43.659375  江Ebd5Oo7oitb5@Squall+Wispy #6uttTRg@Arcadia
```

那么我就认为 `蓬莱山辉夜 8CELMML9@Squall` 作为辅助的强度比 `江Ebd5Oo7oitb5@Squall` 高，即使前者强评只有 5401 而后者有 5862。  

如果时间多可以测 2% 或者 5% 甚至 10% 的 cqp 等，或者选两个号取平均等。也可以为了准确性先测一遍 1%，再测一遍 10%。

这里给出几个推荐的基准号（夹带私货）。

测背刺用地裂号 `雾雨魔理沙 FELEUOL6@Squall` 或铁壁号 `封焔の067750774622秒@Squall`。  
测辅助用背刺号 `Wispy #6uttTRg@Arcadia` 或背刺号 `星垂NMTUYAWNQ@涵虚`。  
测常规无刺用地裂号 `归墟CAHHOTHNE@涵虚` 或 地裂号 `雾雨魔理沙 FELEUOL6@Squall`。  
测双分身用分身号 `ilem ?MJxj&<^@LuoTianyi` 或 分身号 `CtC7gL9JNpvNpOl@新纪元`。

然后将结果排序，选取排名靠前的若干个进行两两组合测 111% cqp。

这里的“排名靠前”我一般取 70~100 个。

---------

这就完了吗？

不，你会发现我们开头介绍的工具 two.cpp 还没用到。接下来你将“排名靠前”这个基准限制放得更宽，我一般取 10% 46 以上，然后将更多的号喂进 `two.cpp` 里，但这次你只测加成达到一定标准的二人组 111% cqp。

大致就是这样。

## 配完队的后续处理

首先配队留多一点的二人组，建议至少十个，甚至一百个，你不知道下次环境变动后会变成怎样。  

其次建议分析一下自己配出的那些二人组，观察一下哪些号出现次数比较多，每种类型的号都找一下，把每种类型最容易配出强二人组的那几个记录一下。

后续在测号的时候假如发现了一个可能比较强的号，但不确定，可以和自己的这些“核心”号配队试一试，这样可以不大规模配队时也比较动态地更新自己的强二人组。

## 自己写工具

你需要有一定写工具的能力。

比如，你的垃圾堆是 xp 过阈值和 xd 过阈值混合在一起的，你怎么写一个代码把他们分开？

你怎么给你的号进行排序？

你想要用浏览器多开开箱，是否有方法可以快速的把你的号均匀地分在好几个文件中？

