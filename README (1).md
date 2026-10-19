# What Makes Short-Form Content Go Viral?

**Paste a YouTube link, get a virality score, see why.**

A spring 2026 team project (UCLA Art.ificial x DataPath) that asks what actually drives short-form video success. We analyzed a dataset of roughly 47,600 TikTok and YouTube short-form videos, then turned the findings into a web tool that scores any YouTube video.

**Live demo:** https://notnavv.github.io/Projects-Spring-2026/

**Team:** Aarnav (lead), Andrew, Srikar, Serene, Nina, Darren, Amelia, Ibrahim

---

## What's in this project

1. **Exploratory analysis**: seven visualizations comparing video length, upload time, content category, and platform against views, engagement, and viral rate.
2. **Virality Score Predictor**: a front-end tool that takes a YouTube URL, pulls the video's stats from the YouTube Data API, and returns a score with an explanation.

## Key findings

| Question | Result |
|---|---|
| How long are videos? | Right-skewed. Most fall in the 20-25s range, with a sharp rise toward 15s and a sharp drop after 60s. |
| Does length matter? | Barely. 0-15s videos averaged the most views (about 93k) and 60-180s the fewest (about 87k), a gap of under 6k. |
| Does upload hour matter? | Slightly. 3:00 had the highest average views (about 97.5k), 2:00 the lowest (about 82.4k). The spread is small. |
| Weekday vs. weekend? | Almost no difference (about 90.9k vs. 90.5k). Wednesday was highest. |
| Which categories go viral most? | Music (11.1%), Pets (10.6%), Comedy (10.5%), Fashion (10.4%). Science was lowest at 9.2%. Margins between categories are narrow. |
| TikTok vs. YouTube? | TikTok had higher average engagement rate (0.092 vs. 0.051) and completion rate (67.6% vs. 57.4%). |

**Big picture:** no single factor dominates. Differences across length, timing, and category are all small, which suggests content quality matters more than any one posting trick.

## How the Virality Score works

The scorer is a **rule-based point system**, not a trained ML model. Benchmarks and point values come from patterns in our exploratory analysis.

**Determining virality (videos that already have views)**
- Points are added based on views, likes, comments, and duration against benchmark thresholds.
- If the total passes the "viral" threshold, the video is labeled viral. The threshold is based on the top 10% of views in our dataset.

**Predicting virality (new videos, under 50,000 views)**
- Points are added based on duration, upload hour, upload day, hashtag count, title length, and content category, using the best-performing values from our analysis (for example, best hours 3, 15, 5, 0, and 22 UTC, and best days Wednesday, Saturday, and Thursday).
- A high enough score means the video will most likely go viral.

## How the tool works

```
YouTube URL -> extractVideoId() -> fetchStats() -> scoring function -> result display
```

- `extractVideoId()` parses youtu.be, /watch, and /shorts URLs with regex.
- `fetchStats()` calls the YouTube Data API v3 and returns nine fields: title, views, likes, comments, duration, upload hour, upload day, title length, hashtag count, and category ID.
- `analyze()` ties it together and is bound to the Analyze button (Enter key also works).
- Error handling covers invalid URLs, missing videos, and failed API requests.

The tool needs a YouTube Data API key. Without one there is no data to score.

## Limitations

- **Heuristic, not validated.** The score has not been tested against held-out videos, so treat it as a guide, not a forecast.
- **Small effects.** Many of the differences above are small and we did not run significance tests, so some may be noise.
- **Speculative explanations.** Reasons given for results (for example, the 3 AM peak reflecting insomniacs or international viewers) are hypotheses, not findings.
- **Platform gap.** The analysis covers TikTok and YouTube, but the predictor only scores YouTube videos.
- **Time zones.** Upload hour comes from the API in UTC, not the viewer's local time.

## Run it locally

> TODO: confirm the steps below match the repo.

1. Clone the repo.
2. Add your YouTube Data API v3 key where the code expects it (do not commit it).
3. Open `index.html` in a browser, or serve the folder with a local server.

## Repo structure

> TODO: fill in once files are organized (data, notebooks, front-end code, figures, slides).

## My contributions

- Built the **scoring algorithm** (benchmarks and point rules for determining and predicting virality).
- Did the **video duration distribution** analysis.

## Data

> TODO: add the dataset source, size (about 47,600 videos), collection method, and date range.

## Contributors

Aarnav (lead), Andrew, Srikar, Serene, Nina, Darren, Amelia, Ibrahim
