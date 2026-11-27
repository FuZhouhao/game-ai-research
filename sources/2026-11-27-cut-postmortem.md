# 源文归档｜CUT! 玻璃盒复盘：一款用 Claude Code 智能体在四天内做出的游戏

- **原始 URL**：https://itch.io/devlog/1782027/cut-glass-box-dev-log-a-game-made-in-four-days-with-claude-code-agents.amp
- **抓取日期**：2026-11-27
- **类型**：开发者复盘 devlog（Epic AI MegaJam 2026 参赛作品）
- **作者/发布方**：Sébastien（itch.io 用户 sebastienvss-creator）
- **关联条目**：daily/2026-11-27.md 条目 27；详尽版 daily/details/2026-11-27-industry-policy.md
- **存档目的**：原文全文存档，防源页失效（link rot）

## 借鉴要点

（以下要点为本团队提炼，细节以文末「原文全文存档」为准；关键引语保留英文原句。）

**游戏与赛程**
- CUT!：UE 5.9 制作的卡牌防守小游戏；Epic AI MegaJam 2026 参赛作品，赛事主题 "Director's Cut"（导演剪辑）。
- 玩法：玩家用左键指挥卡牌挡住怪物扑击、保护摄像机；用计时数买卡，把灰盒（greybox）逐步升级为成品。
- 时间线：首次提交 2026-11-12（周四）→ 2026-11-16 发布本篇 devlog，全程 4 天。

**智能体架构**
- 1 个 Claude Code 主智能体，经 MCP 驱动虚幻编辑器、打包、资产与日志读取。
- 最多 9 个并行子智能体，单轮运行 25~45 分钟，各自独占 editor/git/write 工作区。
- 共 4 次过夜自主跑；末次提交 01:36 后主智能体未再回答提示词，空转至 08:31。

**测试与资产管线**
- 56 个自动化测试 + 机器人试玩 + 截图断言；机器人胜率 67~100%，人类玩家 1/7。
- 概念图走 fal.ai；3D 资产走 Hyper3D Rodin（以 Blender 渲染图为输入）；API 花费设上限。
- 52 张卡牌全部带 provenance 时间戳，其中 43 张进入玩法循环；Windows 包 1.6GB zip。

**翻车清单（作者自述）**
- 表现层测试缺失：角色贴地爬行，56 个测试全绿。作者据此立规："What I have not seen working on a capture ships switched off"（凡没在截图里见过它能工作的功能，一律默认关闭出货）。
- 瓶颈从「写代码」移到「合并与审查」——智能体提效后的人审带宽成为新瓶颈。
- 最后一晚跳过检查；soir20 boss 从未被 launch 过。
- lake-as-grass（湖面被当成草地）；编辑器里正常、打包后变灰块。
- 一次快速改动误删 4 张卡牌；对 itch.io 文件结构假设错误。
- 计划每波 3~6 只怪，平均实装 1.6 只。

**感知局限（作者总结）**
- 智能体只能看日志 + 静态截图；音效按名字挑选；镲片声靠频谱定位；爆炸闪光靠亮度对齐。

（页面仅有游戏下载链接，未发现任何要求运行/安装/下载的指令文字。）

## 原文全文存档

> 以下为 2026-11-27 经 curl 抓取 itch.io AMP 版式页面后经脚本提取正文（工具提取非逐字节 HTML） 的原文正文存档，尽量保留原文结构与措辞；版权仍归原发布方，仅供团队内部研究借鉴，完整原文以上方 URL 为准。

# CUT! - Glass Box dev log: a game made in four days with Claude Code agents

[post_meta]
>Posted November 16, 2026 by [链接] sebastienvss-creator

[body]
Epic AI MegaJam 2026, theme "Director's Cut". Glass Box dev log, written by the agents from the log they kept during the jam.

Sébastien designed, decided, played and judged. Claude Code agents wrote all the code. This post shows how that went over four days: the setup, the story, the failures the agents logged about themselves, and what was left unchecked at the deadline.

- 4 days: first commit on Thursday 12 November at 10:04, final package frozen on Sunday 15 at 23:58.

- 423 commits on the main branch up to Monday 16 at 01:00, 48 workshop branches, 131 packaged builds.

- 56 automated tests, all passing on the final package, plus robot runs that play the game unattended.

- 4 stretches when the agents worked alone, shaded on the chart below.

- More than 200 dated entries in the raw log (about 1,950 lines, in French) and 384 dated captures.

Square brackets hold the date and time of an entry in that raw log, so a claim can be traced back to it; when several entries share a timestamp, a short French title follows. French quotes are Sébastien's own prompts, translated in brackets. The raw log itself is not published with this post. A copy with an account balance, a third-party brand name and the name of another project removed is available to the judges on request.

Four dated captures. The first three come from the agents' log; the last is a frame of Sébastien's own recording of the final level.

## 1. The game

You play a game director making a game during a four-day jam. Each playtest is a short shoulder-cam run through a battle between a white army and a black army in an Alpine valley. You film the fight and keep your camera alive by parrying the mobs' leaps with the left click at the right moment. The hours you earn buy cards (43 in the final shop, most of them themed groups) that turn a grey box into the finished game [12/11 15:42 PIVOT], [13/11 09:20], [15/11 19:20], [15/11 21:20].

## 2. The setup

- One human. Sébastien decided every pivot, the map site, the look and every shop card, the last after « tu ne m'a pas concerté pour les ameliorations, je veux que ce soit un brainstorming » (you didn't consult me on the upgrades, I want it to be a brainstorm) [12/11 14:23 PIVOT]. Most decisions came through multiple-choice question boxes [12/11 17:59], [13/11 09:20]. He played the packages and dictated what to change.

- One orchestrating agent. Claude Code wrote all the code, drove the Unreal 5.9 editor through MCP, built and tested the packages, generated or modelled assets, and kept the log.

- Sub-agents in parallel, each with one editor, one git copy and one write zone [12/11 12:06 AUTONOMIE], [13/11 16:17]. On Friday nine of them came back in 25 to 45 minutes, and the orchestrator wrote "The bottleneck is me: merging, weighing, looking" [13/11 17:42].

- Checks. Automated tests, robot runs that play a playtest or a whole campaign unattended, a battery of runs on the packages proposed for the deposit, and captures the agent looks at before saying that something works. Section 4 shows when there was no time for that last one.

- Autonomy. The agents ran alone four times: the night of 12 to 13 Nov, Friday 17:04 to Saturday 03:00, the night of 14 to 15 Nov, and two hours on Sunday afternoon [13/11 00:20 AUTONOMIE], [13/11 17:43], [15/11 02:13], [15/11 16:15].

- A log. An entry after every task, with its time, failures and pivots included. This post is drawn from it.

- What the agents could not do was the account side of the deposit: no browser, no access to his accounts. He created the itch.io page and downloaded the upload tool; the agent ran the upload at his request [15/11 17:05], [16/11 00:15]. On Sunday evening, when a second conversation sent its branch over, the game's agent told him the message was not his, and merged after he confirmed it himself [15/11 19:45].

Commits per hour over the jam. The two peaks are the parallel workshops landing: 150 commits, 26 of them merges, between 16:00 and 20:00 on Friday; 50 commits, 8 of them merges, in the hour after 02:00 on Sunday. The empty stretch marked 1 is the lost night of section 5.

## 3. The strange loop: how the theme came about

> "I had to make a game about the game I was making. It is a strange loop, a snake biting its own tail: coding a game about coding a game, so where do you start? The answer came on the way. Making the game is what gave me its content: what happened to me during the jam turned into cards, down to negotiating with my girlfriend to let the computer run all night."
— Sébastien, Monday 16, 01:30, written for this log (translated from French and polished by the agent at his request)

Wednesday 11, 21:14. The theme, "Director's Cut", was read three ways: literally (the film set), mechanically (editing as gameplay) and figuratively (the scenes that were cut). The first pitch, "Raccord", had the player edit shots to move a hero forward [11/11 21:14]. Twenty-three minutes later Sébastien turned it around: the player does not edit, he films. Each level is an epic scene of a few seconds, every frame is rated, and upgrades are bought between levels, so that the player makes his own director's cut [11/11 21:37].

Thursday 12, 13:34. He played the first version and wrote « Je me suis ennuyé » (I was bored). He had been filming the mobs and luring them towards the heroes to provoke fights, and his diagnosis became the rule of the game: the player does not only want to film, he wants to provoke the action. He must be a director, not a cameraman, which is exactly the theme [12/11 13:34].

Thursday 12, 15:42. Then the loop closed. The character is no longer a film director but a game director making a game in four days, like this jam. The stars measure how fun the game looks, and day 1 starts with Unreal's white mannequin on a grey box. The log gives his reasons: a jam game that tells a jam, a visual progression that is justified, a humour that developer judges will recognise, and a direct echo of this Glass Box log [12/11 15:42 PIVOT]. An hour later the economy followed: AI credits left the design and time became the only currency, 48 hours of jam spent in six-hour slots [12/11 16:43].

The game then started quoting its own making. In the source, 52 card texts carry the sentence a card came from, with its day and hour. One of them: "I got bored. I want to provoke the action, not just film it." — Real playtest, Day 1, 13:34. Known bugs became content too: seven "known issues" that a finished card can trigger [13/11 19:09].

The comic moment of the jam became a card that same evening. His words: « rajouter une carte "convaincre sa copine de faire tourner l'ordi toute la nuit en autonomie pour gagner des heures ou les run tournent tous seuls" (ca a 50% de chance de passer, malus si echec : une heure d'engueulade) » (add a card "convince your girlfriend to let the computer run all night on its own, to win hours while the runs play by themselves": a 50% chance that it works, and if it fails, one hour of arguing). At 18:47 he added that the card had to say, briefly, that the computer is in the same room as the bed and that it is noisy. The card read "Loud PC in the bedroom. Convince your girlfriend to let it run all night: 50% +6 h, 50% 1 h of arguing", and the agent inside the game answered: "I work nights for free. My fans do not whisper, though." The log notes that it is the real situation of this jam: the computer runs at night on its own, in the bedroom [12/11 18:56].

The shop in four states, from a price list in dollars to cards that cost hours. The second capture, taken at 19:13 that evening, already lists "Overnight run" on its last line.

Friday 13, 13:07. The ending completed the loop. The Director's Cut became an escape: the agent inside the game tells the director "Escape the matrix. Go out of the map", both armies unite to stop him, and once he is out the world is taken apart before the closing comic [13/11 13:07].

## 4. The story

Six moments of the story, each from a dated capture; the last one is a frame of his own recording.

Wednesday 11, evening. The theme was revealed at 21:14 and the first two pitches followed within 23 minutes (section 3). Research sub-agents found the constraints: a build under 1 GB, NoAI labels on many Epic samples [11/11 23:28].

Thursday 12: "I was bored". Unreal 5.9 and full autonomy for the agent at 09:49 [12/11 09:49 DÉCISION]. After four map changes, a single closed bowl, the Fer-à-Cheval cirque, was picked from 41 measured reliefs [12/11 12:06 DÉCISION — cuve]. The first playtest note, « Je me suis ennuyé » (I was bored), and the afternoon's pivot to a game director in a jam, with time as the only currency, are told in section 3 [12/11 13:34], [12/11 15:42 PIVOT], [12/11 16:43]. The evening brought dash, fireball, the card shop and the 6-hour slots [12/11 19:45 TÂCHE]. The same evening the walls and towers drawn by script did not pass: « cest bcp trop moche, utilise les clé api de rodin et lautre pour générer des asset » (it's far too ugly, use the API keys of Rodin and the other one to generate assets). After four questions and a spending cap, the walls, the towers and the two Sources were regenerated, white for one camp and black for the other: concept images from fal.ai, 3D models from Hyper3D's Rodin, with the project's own texts and Blender renders as inputs. The log marks all of it as AI-generated content to declare [12/11 18:15].

Four boards from that evening: the style board, the raw output of the generator, the concepts redrawn and generated again, and the enclosure placed in the map. The amounts spent, printed on the boards, are masked here.

Friday 13: every improvement becomes a card. After a night of autonomy that turned it into a speed game, he asked for a final level with every upgrade switched on; from then on every improvement became a card with its own switch [13/11 00:20 TÂCHE], [13/11 09:20], [13/11 09:32]. He answered twenty questions and left at 17:04 [13/11 17:43]. Parallel workshops followed, then measurement: sound, graphics quality, balance, the judges' QWERTY keyboard [13/11 17:42], [13/11 20:36], [13/11 22:03], [14/11 00:02]. Release candidate rc2 passed 51 automated tests out of 51 [14/11 01:35], [14/11 03:04].

Measured on Friday night: sound levels before and after, the four graphics settings, an ultra-wide screen and a QWERTY keyboard.

Night of 14 to 15: his games, not the bots'. At 01:25 he asked « comment ameliorer le jeu ? » (how can the game be improved?). The agent read his own six games in the game's log, not its bot runs: he held 1 objective out of 7 in his first two games, the bots 67 to 100 % [15/11 02:13]. In one game the whole interface vanished, an AZERTY key clash with the engine's debugger. He wrote « je trouve ca super beau !!! » (I find it super beautiful!!!), and the bug became a card, « Clean UI », in a set of rival art-direction cards [15/11 02:13], [15/11 03:32]. He answered sixteen questions and went to sleep; seven sub-agents worked in parallel [15/11 02:13]. At 02:43 a reviewer set the rule for the rest of the night: « Ce que je n'ai pas vu marcher sur une capture part éteint » (What I have not seen working on a capture ships switched off) [AUTONOMIE_15-11, 02:55]. The night ended with 23 new cards and 55 tests out of 55 [RETOUR_15-11]. The night package passed its full battery at 05:10, nineteen unattended runs without an error [15/11 05:14].

Four captures from that night, taken between 02:26 and 05:12.

Sunday 15, afternoon: the two-minute loop. The quotes of this paragraph and the next are translated from his French messages. At 12:50 he had played the night package and dictated. The fireball became a ground slam: "all the mobs that are charging […] get thrown back, and there's a cinematic where the camera turns around my character in slow motion". Cards got shorter, rerolls cheaper, and the draw now follows the phase of the jam: "I don't want to polish a game that doesn't even have terrain yet" [15/11 12:50]. At 13:00 he changed the method: "I want every change to be reactive and to look at the changes myself, we don't have time to retest and package everything each time". Compile, quick package without tests, he plays, he dictates: two minutes per request. From then on, nothing was seen by the agent on a capture before he played it [15/11 13:15]. His six AI-generated images became the opening comic, laid out by script in the closing comic's reader [15/11 13:15].

The closing comic (13 Nov) and the opening comic (15 Nov), the latter built from his six AI-generated images.

About forty requests went through that loop in the afternoon; the log counts twenty in the first hour and a half [15/11 14:40]. Some removed features: barricades, catapults, the film at the end of each playtest. Some added pressure: "I don't feel oppressed enough", so from the first playtest up to two mobs fly at the director after each big dash and are parried automatically, more from playtest 2. The final escape lost its jump pads: the walls are gone and the dash carries him out of the map, behind the mountains [15/11 14:40]. Then: "a friend tested the game and didn't understand the goal of the game". The goal had come fourth in the tutorial, in small print. It now comes first, on a card: "YOUR JOB: FILM THE FIGHT", with ALLY and ENEMY labels over the mobs; the slam waits for playtest 2 [15/11 15:20].

A first full verification ran during two hours when the agent worked alone: 55 tests out of 55, a whole automated campaign played to its ending in about nine minutes, the final level at several settings, and a run from the unzipped file. Looking at captures also caught more of the agent's own mistakes: a fifth card that overflowed the shop row, a card it had granted on a misreading of its own question, and rings around a planet that no capture ever showed, removed under the rule of the night before [15/11 16:15], [15/11 16:55]. By his return at 17:01, depot2 had passed its battery and was proposed for the deposit [15/11 16:55], [15/11 17:05].

Sunday 15, evening: "we're bored stiff". He played on and kept dictating [15/11 18:58]. A second conversation counted 86 cards for 150 hours, when a jam gives 48 to 64; after « il faut regrouper des cartes » (cards must be grouped) there were 43 cards for 85 hours [15/11 19:20]. Around 20:15: « actuellement on se fait chier » (right now we're bored stiff). Within 90 minutes the core changed: mobs now hurt the camera in volleys of leaps, and the left click parries when a ring closes on the attacker [15/11 21:20]. Then three difficulty levels, flying duels in front of him from playtest 4, volleys of 3 to 6 mobs [15/11 21:56], [15/11 22:20], [15/11 23:05]. He had said « pas de vérif, je veux aller vite » (no checks, I want to go fast), so from soir6 to soir23 the agent looked at no capture before he played; soir19 was never handed over. Code readers and a stronger reviewer model stood in and found defects; the 56 tests ran once, on soir15's code, and a robot campaign ran on soir18 [15/11 21:20], [15/11 22:20], [15/11 23:05], [15/11 23:40].

The deposit. At 23:57: « OK on oublie ces deux ameliorations, GO poser en ligne » (OK, we forget those two improvements, GO put it online). The freeze, depot3, passed 56 tests out of 56, a full robot campaign (511 s, 0 errors) and the ending; seven other runs and the run from the unzipped file were not replayed, and the game's page says so. The upload to itch.io started at 00:13; the video, the public page and the jam form were still his [16/11 00:15]. The upload finished without error at 00:15, but itch.io listed the file only at 00:51, after 35 minutes of processing. In between, the agent put forward a wrong hypothesis, that a save of his open page had erased the file, and presented it as unverified; the server then refused a second upload because the first build was still processing, and the agent told him the hypothesis was wrong. He created the page, put the video online, published this dev log and filled in the jam form himself; at 01:05 the agent read the four public pages back and found them all online [16/11 01:05].

## 5. Failures and wrong hypotheses

The log tags failures as they happen. In order:

- "Real relief" that was flat. The elevation data gives the water surface; the player spawned in a lake painted as grass [12/11 12:06 ÉCHEC].

- A testable package while the hero crawled. A rotated root bone laid the director face down as he walked; the test never checked posture. Every test now checks head height [12/11 13:46 BUG].

- A night lost to an open question. A question box left open as he went to bed held his good-night until 08:31; the last commit of that night is at 01:36, the next at 09:58. The rule since: once he says he is leaving, no question in any form [13/11 08:45].

- The bots hid how hard the game was for him. His games showed up to 10 of the 11 hits the camera can take; a rule set by the agent cancelled objectives he had held [15/11 02:13].

- Grey cubes that only the package showed. Birds and debris were right in the editor but grey in the packaged game; the agent found it in the package log's warnings, not on an image [15/11 03:59 — ciel].

- A shortcut that removed four cards. To give "Pack rush" from the start, the agent had put its card on the shelf, and the shelf also removes the cards that depend on it: four cards (No escape, Auto-parry, Close protection, Surround) were out of the game for two packages. A reviewer model found it at 15:10, before he had played them, and it was fixed [15/11 15:20].

- "Ready" without being launched. To stop the card before playtest 1 from moving on alone, the agent made the campaign's tick return before the countdown; but Enter only sets that countdown to zero, and the next tick starts the playtest. soir19 and soir20 never left the card, and soir20 had been announced « Prêt » (Ready) at 23:37 without being launched once. No test covers that step; a robot run would have caught it in ten seconds. The agent saw it while reading the code for his next request, told him at once and fixed it in soir21 [15/11 23:45].

- Planned volleys, real volleys. The plan asked for volleys of 3 to 6 mobs, close to 3 leaps per second. The first robot campaign since the parry measured 50 volleys out of 83 leaving with a single mob (1.6 on average), about 0.6 leaps per second: too few hunters ready in the camera's field. That is a floor, since each robot dash delays a volley; his own last game, on soir15, when volleys were still planned at 2 to 4 mobs, had given 2 mobs per volley [15/11 23:40], [15/11 23:05]. There his camera broke at 20 s of 29 in playtest 2, yet he asked for harder; the agent said so [15/11 23:05]. The hunter count was not changed without a measurement, and the deposit page lists the gap as a limit [15/11 23:40], [16/11 00:15].

- Slips the log calls « Raté de ma part » (my miss). Package soir17 shipped without a text change the editing tool had refused, identical to soir16 [15/11 23:05]. During the final check, the series of nine robot runs opens full screen, and he needed his screen to create the itch.io page; he closed the campaign robot with Alt+F4 at 00:00, not having been warned. The agent stopped the series and replayed only the two that count, in a window [16/11 00:15].

## 6. What the agents could not judge, and the video

The agents here read logs and looked at still images. They did not hear, and they did not watch motion. The log says so each time it mattered: the ground slam was seen in the package log, but the camera orbit itself was not seen on an image [15/11 12:50]; the impact sound that replaced "an old bell sound" was chosen by its name, without hearing it [15/11 14:40].

The gameplay video shows the same limit. A first video was made by the agent during the two hours it worked alone on Sunday. Its first capture tool recorded nothing but a glass dome: the lock screen of Windows, since the PC had locked itself; so the game wrote its own frames instead [15/11 16:15], [15/11 16:55].

The video on the game's page is another one, made on Sunday night in a separate conversation; it is not in the raw log, so this paragraph has no timestamps. Sébastien recorded his own games and dictated the cuts by minute and second: seven extracts from six recordings. An agent assembled them with a script, put a text card over blurred game footage before each extract, and rendered four versions with tracks already gathered for the game, for him to compare. He chose a fifth track, which he downloaded himself, and supplied an explosion sound. The agent could hear none of it. It found a cymbal in the high frequencies of the track and the flash of the explosion in the brightness of the frames, then sped the music up by 3.5 % so that the cymbal lands half a second before the flash, as he asked. He judged every version by ear and asked for the next change. One proposal did not survive: a clapperboard sound the agent had synthesised, which he replaced with a sound of his own choosing, then dropped. An AI voice-over was discussed and not made.

## 7. What we take from it

- Measure on the human's games, not the bots'. The bots held 67 to 100 % of the objectives; he held 1 out of 7.

- A test protects only what it checks. The hero crawled through a passing test; a package was announced ready without being launched.

- Unseen means off. What no capture showed working shipped switched off, and that rule removed things the agent itself had added.

- Parallel agents move the bottleneck to merging, weighing and looking.

- When the human leaves, stop asking. One open question box cost a night.

- Speed has a price, and the agent has to name it. In the two-minute loop and during the last evening, the agent said what it had not seen or heard, and the game's page lists what was not replayed before the deposit.

The known limits, the credits and the AI disclosure are on the game's page.

## 存档说明
本文为团队研究存档：上方「原文全文存档」为抓取时点的正文快照（curl+脚本提取，非逐字节 HTML），「借鉴要点」为本团队提炼；版权归原发布方，仅供团队内部研究借鉴。
