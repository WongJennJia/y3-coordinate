# 三年级 · 今天学了什么？ / Year 3 — Position & Direction Recap

A small static site students open at the end of the lesson to replay the day's two
activities and tick off what they learned. No build step, no dependencies — three
self-contained HTML pages.

**学习标准 8.1.1 · Position and Direction**

---

## 页面 / Pages

| 文件 | 说明 | 角色 |
| --- | --- | --- |
| `index.html` | 复习目录 + 「今天我学会了」自评清单 | 首页 |
| `position-lab.html` | **位置小侦探 · 镜头找位置** — 看图选词 / 拖动摆放 / **摄像头找位置** | ★ 今日主活动 |
| `direction-quest.html` | 东南西北闯关 — 9 关：指南针 → 右手找东 → 教室四面墙 → 转身测试 → 上北下南 NEWS | 复习 |

`position-lab.html` is the featured activity: it gets the hero card, the teal accent
bar, a `★ 今日主活动` badge and a highlighted `📷 摄像头实验` tag on the landing page,
so students land on it first.

原文件名 / original filenames:

- `position-vocabulary-lab_camera_classroom_v5.html` → `position-lab.html`
- `direction-quest_classroom.html` → `direction-quest.html`

Renamed for clean URLs. The activity content itself is unchanged — the only edits
were a `← 回目录` back link in each header (class `.y3-home`) and, for
`direction-quest.html`, a proper `<!doctype html>` / `<head>` wrapper with
`<meta charset="utf-8">`, which it was missing.

## 为什么用三个页面，而不是合成一个文件

Both activities are self-contained single-file apps that define **conflicting** global
CSS — `:root` custom properties, `.panel`, `.eyebrow`, `.btn`, `.mode` — with opposite
colour schemes. Pasting them into one document would break both. Keeping them as
separate pages behind a shared landing page preserves each app exactly as written.

## 自评清单 / The recap checklist

Seven statements drawn from both activities, in the students' own phrasing. Ticks are
stored per-device in `localStorage` under `y3-recap-v1`, so a student's progress
survives a refresh. `清空勾选` clears it. Theme choice is stored under `y3-recap-theme`;
with nothing stored, the page follows the system light/dark setting.

## 摄像头 / Camera activity

`position-lab.html` uses `getUserMedia` for the red-card / blue-card colour activity.
It needs **HTTPS or `localhost`** — it will not work from a `file://` path — and the
browser will ask for camera permission. Nothing is uploaded or stored; frames are read
on the page for colour position only. The camera tab is optional; the other two modes
work without it.

---

## 本地运行 / Run locally

```bash
python -m http.server 8000
# open http://localhost:8000
```

Any static server works (`npx serve`, VS Code Live Server, …). Serve it rather than
double-clicking the file, so the camera activity works.

## 发布到 GitHub / Publish to GitHub

```bash
git remote add origin https://github.com/<your-username>/y3-coordinate.git
git branch -M main
git push -u origin main
```

## 部署到 Vercel / Deploy to Vercel

Static site, no framework, no build command.

**Dashboard:** vercel.com → *Add New…* → *Project* → import the repo → framework
preset **Other**, build command **empty**, output directory **`./`** → *Deploy*.

**CLI:**

```bash
npx vercel          # preview deployment
npx vercel --prod   # production
```

`vercel.json` sets `cleanUrls: true`, so the pages are also served at `/position-lab`
and `/direction-quest`. Vercel serves everything over HTTPS, which is what the camera
activity needs.

## 课堂用法 / Classroom flow

1. 下课前 5–10 分钟打开首页。
2. 学生选 **位置小侦探** 再玩一次；小组用红蓝卡片做镜头活动，说出完整句子：**A 在 B 的 ____ 边**。
3. 忘了东南西北的，回 **东南西北闯关** 复习第 3 关（转身测试）和第 4 关（上北下南）。
4. 回首页勾「今天我学会了」，七项全勾上就完成。
