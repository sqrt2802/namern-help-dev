# Chapter 1 理论知识（可以跳过）

## 1.1 技能顺序

想必你已经知道了什么是技能的“熟练度”，但是仅仅知道这个是不够的。对于**每个名字**而言，它的技能存在**顺序**。这个顺序是在名字生成的时候就决定的，每个名字并不相同。

显然，一个号在同一回合内无法发动两个主动技能，当一个号在这一个回合，多个主动技能同时满足发动条件时，他会按照**顺序**依次进行概率检测是否发动（概率为熟练度/128）。顺序在前的技能越容易先发动，即使熟练度相同。

举例，假如一个号只有两个主动技能，技能 A 和技能 B。技能 A 和 技能 B 的熟练度分别为 64 和 96。在两个技能发动条件都满足的情况下，如果 A 在前，B 在后，那么发动 A 的概率为 1/2，发动 B 的概率为 \(1 - 1/2\) ÷ 3/4 = 3/8。如果 B 在前，A 在后，那么发动 B 的概率为 3/4，发动 A 的概率为 \(1 - 3/4\) ÷ 1/2 = 1/8。

实际上由于名字属性生成的方式（具体可以见 1.2 和 1.5），高熟练度的技能大概率只会在最后两个以及最后一个主动技（位置可能重合）出现，因此出现“熟练度高的技能总是在后面”是非常正常的现象，不要进行抱怨。

## 1.2 name_base 与属性

一个名字会根据某种方式生成 128 个 name_base（如果你对具体方式感兴趣，看 1.5）。其中 0~63 每个数出现两个。号的属性生成和这些 name_base 息息相关。

### 八围

HP 对应 10 个 name_base，其他七围属性对应 3 个 name_base。

HP 的值为 154 + 10 个 name_base 从小到大排序后的中间四个之和，其他七围属性为 36 + 3 个 name_base 的中位数。

### 技能

一个名字最多 16 个技能，每个技能对应 4 个 name_base。

技能熟练度的值为 4 个 name_base 的最小值 - 10。如果小于 0 则设为 0。

特别地，最后一个主动技能的熟练度翻倍（如果存在熟练度不为 0 的主动技能）。<br>
假如最后一个主动技能不是最后一个技能，那么会将熟练度加某两个新的 name_base 的最小值，但是不超过原技能本身的熟练度。<br>
假如最后一个主动技能不是倒数第二个技能，那么会将熟练度加某两个新的 name_base 的最小值，但是不超过原技能本身的熟练度。<br>
倒数第三再往前没有类似的操作。

如果看着抽象的话可以看代码：

```cpp
if (last != -1) freq[last] <<= 1;
if (freq[14] && last != 14)
	freq[14] += min({name_base[60], name_base[61], freq[14]});
if (freq[15] && last != 15)
	freq[15] += min({name_base[62], name_base[63], freq[15]});
```

## 1.3 加成方式以及“潜力”

### 加成方式

加成的基本原理是，通过某种方式给名字的 name_base 进行取 max 操作，所以不会出现加成属性超过上限的情况。

对于两个号 x,y，我们假设加成后的号为 X,Y，这么说是为了避免**原始** name_base 变动。他们会进行这样的操作：

```cpp
for (int k = 7; k < 128; k++)
    if (y.name_base[k - 1] == x.name_base[k])
      	X.name_base[k] = max(X.name_base[k], y.name_base[k]);

for (int k = 7; k < 128; k++)
    if (x.name_base[k - 1] == y.name_base[k])
    	Y.name_base[k] = max(Y.name_base[k], x.name_base[k]);
```

对于更多人组，两两进行这样的操作即可。注意前十个 name_base 应当是没有排序过的。

### “潜力”

由于属性生成的方式，某些号的一些属性会比别的属性更容易得到加成。

比如一个号的某个属性的三个 name_base 分别是 30,30,60，或者是 30,30,31。对于前者而言，两个 30 假如有一个被加成了，那么属性就会大幅提升。对于后者，三个属性假如有一个（且只有一个）被加成了，那么并不能怎么提升属性（最多 1）。由于在加成的时候，同时将一个属性的两个 name_base 加成的情况极难出现，我们基本可以认为，这个属性的加成“潜力”是有限的。

技能熟练度也是同理，20,50,50,60 很明显会比 20,20,50,60 更加容易加成。

为了较为准确定量衡量一个号的“加成潜力”，我们采用这样的方式衡量：将这个号的其中一个 name_base 提升为 63，然后重新计算属性。将每一个位置的 name_base 都修改一次，选择最好的那一个。

至于“最好”这个概念怎么衡量，我们采用模型评分，比如虚评，或者一些其他的模型评分。具体你会在 2.3 中见到。

除此之外形如 x,y,x 的 name_base，其中 y 是一个很大的 name_base（比如 62 63 之类的）。这样的号在加成是会有一些妙妙性质使得他容易加成出更好的二人组，原因留作读者思考题。

## 1.4 嘲讽值理论

这个是进行战斗时的理论。

根据玩家【新纪元】研究发现，一个号的 \(攻-防\)+\(魔-抗\)+速+\(敏+智\)\*0.5，这项数值对对手的索敌十分关键。我们称其的两倍为**“嘲讽值”**。（群里有部分人/工具习惯不乘二，也有习惯乘二变成整数的，注意区分）

我们只讨论二人组，在二人组中如果一个号的嘲讽值高于另一个号，那么在对战中会**显著**更容易被**大部分攻击**索敌（有些技能的索敌机制不一样）。并且这样的嘲讽值差距是**突变**型的而非一个平滑的曲线。也就意味着，仅仅 2 点的属性改变可能会造成胜率，或者说强度的巨大差异。

在测强评的过程中，队友天卫的嘲讽值基本上分布可以认为是连续的。但是在测二人组的时候，队友是单一的。这将对配队产生巨大影响。

以潜行号举例，潜行号非常注重**不容易被打**这一个特质。由于在测强评的时候天卫的嘲讽值不定，所以嘲讽值越低越不容易被打，所以我们可以发现，大部分高强评潜行号的嘲讽值都偏低（具体表现通常为攻低防高，有时候敏低，其他四个属性对背刺来说比较重要所以一般不能低）。

但是在配二人组的时候，只需要背刺号的队友（我们一般称为辅助）嘲讽值高于他即可。所以我们会发现一些高嘲讽值的背刺在配合适的队友的情况下实战并不差，即使他的强评是偏低的。

同理，高强评的辅助号的嘲讽值一般偏高，但是实际上部分低嘲讽值、低强评的辅助号找到合适的背刺队友也能有不差的实战。

这就是为什么我们推荐多留一些号，降低阈值，虚评和强评并不一定准（具体见 2.1）。

## 1.5 算号属性的完整代码

自行参考，未经卡常加速，也许可用作自己的玩具测号器编写原料（速度会比较轮椅）。

<details><summary>点击展开代码</summary>

```cpp
typedef unsigned long long u64_t;
typedef unsigned char u8_t;
const int N=256;
const int skill_cnt=40;
struct Name
{
    u8_t val[N],ual[N],val_base[N],val_base2[N];
	u8_t name_base[M], freq[16], skill[skill_cnt], p, q;
    int prop[8];
	int q_len,V,seed;
	u8_t m()
	{
		q += val[++p];
		swap(val[p], val[q]);
		return val[val[p] + val[q] & 255];
	}
	int gen()
	{
		int u = m();
		return (u << 8 | m()) % skill_cnt;
	}
	void load_team(char *_team)
	{
		int t_len = strlen(_team)+1;
		u8_t s;
		for (int i = 0; i < N; i++) val_base[i] = i;
		for (int i = s = 0; i < N; ++i)
		{
			if (i % t_len)
				s += _team[i % t_len - 1];
			s += val_base[i];
			swap(val_base[i], val_base[s]);
		}
	}
	void load_name(const char *name)
	{
		memcpy(val, val_base, sizeof val);
		q_len = -1;
		u8_t s;
		int t_len=strlen(name)+1;
		for (int _ = 0; _ < 2; _++)
			for (int i = s = 0; i < N; i++)
			{
				if (i % t_len) s += name[i % t_len - 1];
				s += val[i];
				swap(val[i], val[s]);
			}
		for (int i = 0; i < N; i += 8) 
			ual[i] = val[i] * 181 + 160;
		for (int i = 0; i < N; i ++)
			if (ual[i] >= 89 && ual[i] < 217)
				name_base[++q_len] = ual[i] & 63;
		prop[1] = median(name_base[10], name_base[11], name_base[12]);
		prop[2] = median(name_base[13], name_base[14], name_base[15]);
		prop[3] = median(name_base[16], name_base[17], name_base[18]);
		prop[4] = median(name_base[19], name_base[20], name_base[21]);
		prop[5] = median(name_base[22], name_base[23], name_base[24]);
		prop[6] = median(name_base[25], name_base[26], name_base[27]);
		prop[7] = median(name_base[28], name_base[29], name_base[30]);
		sort(name_base, name_base + 10);
		prop[0] = (154 + name_base[3] + name_base[4] + name_base[5] + name_base[6])/ 3;
	}
	void calc_skills(const char *name)
	{
		q_len=-1;
		for (int i = 0; i < N; i += 8) 
			ual[i] = val[i] * 181 + 160;
		for (int i = 0; i < N; i ++)
			if (ual[i] >= 89 && ual[i] < 217)
				name_base[++q_len] = ual[i] & 63;

		u8_t *a = name_base + K;
		for (int i = 0; i < skill_cnt; i ++) skill[i] = i;
		memset(freq, 0, sizeof freq);
		p = q = 0;
		for (int s = 0, _ = 0; _ < 2; _ ++)
			for (int i = 0; i < skill_cnt; i ++) {
				s = (s + gen() + skill[i]) % skill_cnt;
				swap(skill[i], skill[s]);
			}
		int last = -1;
		for (int i = 0, j = 0; i < K; i += 4, j ++) {
			u8_t p = min({a[i], a[i + 1], a[i + 2], a[i + 3]});
			if (p > 10 && skill[j] < 35) {
				freq[j] = p - 10;
				if (skill[j] < 25) last = j;
			}
			else freq[j] = 0;
		}
		if (last != -1) freq[last] <<= 1;
		if (freq[14] && last != 14)
			freq[14] += min({name_base[60], name_base[61], freq[14]});
		if (freq[15] && last != 15)
			freq[15] += min({name_base[62], name_base[63], freq[15]});
	}
};
```

</details><br>

## 1.6 diy 技术

以前我们经常会口嗨“这个号如果改变什么东西会怎么样”。为了避免这方面的研究止于想象，diy 技术被开发了出来。

网址 <https://fast-namerena.pages.dev/>，正常操作和普通名竞一样，可以测评分、胜率等。
特别地，假如你的装备是类似 `+diy[]{}` 的形式的时候，他会变成，将这个名字的属性修改为一个由你决定的值。

**注意：由于技术原因，对于分身号的 diy 会有一定的误差，暂时无法修复。**

举例，`name@team` 这个名字，属性为 HP 291 攻 68 防 49 速 72 敏 60 魔 60 抗 67 智 79，技能为 会心 11 铁壁 21 地裂 8 苏生 8。它的 diy 格式为 `name@team+diy[68,49,72,60,60,67,79,291]{"SklCritical":11,"SklIron":21,"SklQuake":8,"SklRevive":8}`。比如说我们想要知道如果他的 HP 增加 50 会怎么样，将 291 改成 341 就能虚拟出一个这样的名字。

技能名称对照表（不区分大小写）：

| 技能 |    火球术     |     冰冻术     |   雷击术   |   地裂术   | 吸血攻击  |   投毒    |    连击    |  会心一击   |    瘟疫    |  生命之轮   |
| :--: | :-----------: | :------------: | :--------: | :--------: | :-------: | :-------: | :--------: | :---------: | :--------: | :---------: |
| 名称 |    SklFire    |     SklIce     | SklThunder |  SklQuake  | SklAbsorb | SklPoison |  SklRapid  | SklCritical |  sklHalf   | SklExchange |
| **技能** |    **狂暴术**     |      **魅惑**      |   **加速术**   |   **减速术**   |   **诅咒**    | **治愈魔法**  |   **苏生术**   |    **净化**     |    **铁壁**    |    **蓄力**     |
| 名称 |  SklBerserk   |    SklCharm    |  SklHaste  |  SklSlow   | SklCurse  |  SklHeal  | SklRevive  | SklDisperse |  SklIron   |  SklCharge  |
| **技能** |     **聚气**      |      **潜行**      |    **血祭**    |    **分身**    |   **幻术**    |   **防御**    |    **守护**    |  **伤害反弹**   |   **护身符**   |    **护盾**     |
| 名称 | SklAccumulate | SklAssassinate | SklSummon  |  SklClone  | SklShadow | SklDefend | SklProtect | SklReflect  | SklReraise |  SklShield  |
| **技能** |     **反击**      |      **吞噬**      |  **召唤亡灵**  |  **垂死抗争**  |   **隐匿**    |           |            |             |            |             |
| 名称 |  SklCounter   |    SklMerge    | SklZombie  | SklUpgrade |  SklHide  |           |            |             |            |             |

有一些工具可以方便地输出一个号的 diy 格式从而进行方便地修改，具体可以见 1.7。

这个技术有什么用？

实际上嘲讽值理论便是由这个技术发现的。此外在研究属性对技能的作用、技能搭配等方面也有重要作用。除此之外，在测出一个二人组之后，我们也可以测加成后的属性所对应的强评之类的。

## 1.7 一些小工具

具体来说在 Tools 文件夹。

### XP-convert

将一堆号丢进 xp 或者 convert 的 html 里的时候会测得很慢，所以玩家【Squall】开发了 cpp/exe 版本。

里面包含 XP convert sort-convert diy-convert 的功能。convert 和 sort-convert 的区别在于是否将技能按照熟练度排序。

在 `input.txt` 中输入号（按行分隔，**文末要换行**），然后运行 exe，会将结果输出在 `XP.txt` 或者 `convert.txt` 之类的里面。

同时提供了 cpp 源代码，可以自己进行修改，然后重新编译。

**确保你输入的时候是 utf-8！！！**

### team\_calc

**team_calc.html**

输入一个多人组，按照换行分隔，他会告诉你加成后的属性是怎样的，同时提供 diy 格式。

注意没有进行是否是同队的判断，请你自行保证输入的多人组是同队的。

**team_calc.cpp**

team_calc.html 的缺点之一在于对某些字符会炸（尤其是各种奇怪的 Unicode，比如 emoji），同时不能批量。所以提供了一个 cpp，用法和 XP-convert.zip 里的东西类似，用加号分隔多人组的每个号，用换行分隔不同多人组。

### base

感谢【新纪元】的贡献，这个工具基本由他一个人完成。

是 1.2 和 1.3 的加成潜力的具象化，不言而喻，一目了然。可能存在少量 bug。

输入在 `input.txt` 里，每一行一个号然后换行。输出在 `base.txt` 里。

### sort

后面这些东西其实和名竞无关了，但是有些人确实是不会编程的，因此也写了。

在 `input.txt` 中每一行先输入分数，然后单个空格，然后输入号/多人组，然后换行。**在文件的开头输入总量！**

然后运行 exe，输入 0 或者 1，表示不输出分数/输出分数，结果在 `sort.txt` 里。

### 一键分类战队并去除xpxd

感谢【abruce】的贡献，这个工具由他编写。

用法：将.exe文件放置于测号器out目录下，运行该程序，可按照战队进行分类到对应的.out文件（会删除该目录下原有.out文件）（如果电脑是GB2312，可能文件名为乱码，但实际不影响）（若文件中有特殊字体、emoji可能会出现未知问题）

### 编码转换

感谢【shabby\_fish】的贡献，这个工具由他从网上找到并推荐。

双击打开 UltraCodingSwitch.exe。这个工具和玩家自己编写的各种草台工具不一样，有明确的 UI，可以自己看。
